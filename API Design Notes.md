# API Design Notes #
WHY?
 - Asynchonousity - thrown around but why is it so important?
 - Statelessness - why is it important and where does it fit in?
 - APIs vs RPC/Remote Objects
 - RESTful - why?
 - 'Design-by-buzzword'

## Inside vs. Outside ##
The important notion of a system barrier - needed for scalability & recoverability

 - Pat Helland's paper 'Data on the Outside versus Data on the Inside'

How do we treat things on the inside as opposed to the outside?

Often our tools are only looking at the world from 1 perspective.

Newton taught use about a mechanistic, sequential way of looking at the world.
Einstein thought about things in a more random/chaotic way, and then we make
them sequential (relativistic).

Often we build our systems using the mechanistic view. For example, the original
implementation of the HTTP caching was based on an expires header that had an
absolute expiry time. Not every machine in the world had a different clock, 
which caused problems with cache expiration. In HTTP 1.1 the protocol was 
changed, including the use of *relative* time. 

Why does this notion of relative/absolute matter?
 - Inside a machine, imperative sequential code works
 - The concept of a 'machine' can be expanded to include anything that *shares
   a clock*
 - On a wide scale network like the web, Einsteins rules apply because we don't
   have a shared clock. 
 - We can't lock the web, we can't do transactions
 - Time is an architectural element

Distance affects systems. There is no simultaneity at a distance!
 - Similar to the speed of light bounding information
 - By the time you see a distance object, it may be gone/have changed
 - By the time you see a message, the data may have changed!

Services, Transactions & Locks all bound simultaneity!
 - Inside a transaction or service, things are simultaneous
 - This isn't a choice, we have to apply these rules at the right place/time

There is no shared "Now" on the outside. Services on the outside don't share 
clocks. 

Rubber meets the road?
When we're coding on the inside, we can do things like if-then-else, test for
truth, and create transactions and lock resources because this is all done 
inside the clock-space. We can do this because 
 - we have sequential, near-instant execution
 - we can have complex object models & pass things around knowing that their meaning is understood
 - Logic is consistent - from line to line we have guaruntees
 - We can do transactions such as placing things on queues
 - We have full control (inside a machine, a rack, a controlled network)
 - We can write functional, procedural and object-oriented code

When we're coding on the outside, we
 - Take complex objects and turn them into flat messages (sometimes representing nesting such as in XML or JSON)
 - We send these messages, *hoping* that they will be receieved, but with no gaurantee
 - Once we cross the boundary of our system, our object has become frozen and may not represent it's object's state in the system
 - We've got delayed, non-sequential execution
 - We could get conflicting logic (we might get a message that is no longer true when we recieve it)
 - So we can't do transactions
 - It's important not to try and fight against this system
 - We only have relative control over the outside. We can control the messages we send, and how we recieve messages.
 - We must treat messages from the outside *very* differently to how we treat messages on this inside.

Some falacies of distributed computing:
 - The network is reliable
 - Latency is zero. This is a big problem with RPC/Tunneling - when calls to the outside look like functions, the fact that latency (& blocking) may be involved is hidden. If we then make function calls as normal, but one turns out to be a blocking item then any slowdowns will block all of our client-side code)
 - Bandwith is infinite. Big requests or lots of requests are evil. 
 - The network is secure. We need to be sceptical of every message we receive.
 - Topology doesn't change. We bind ourselves to features on our database servers, Content Management servers, middleware servers. If one of those moves or changes, suddenly we're screwed. We need to assume that the rearrangement of things is going to happen over *time*.
 - There is always one administrator. There will generally be more than 1 place we'll need to go to in order to orchestrate functionality.
 - Transport cost is zero. 
 - The network is homogeneous. We won't always use the same languages, platforms and frameworks. WSDL and interface description languages try to solve this.

### Boundaries ###
It's important to know where you are at any given moment. It's not a choice of either-or, it's a choice of *when*. Don't treat everything as if it's the outside, or you'll end up doing lots of extra work. 

Internal Systems:
 - Trusted boundary: you should be able to trust messages once their inside your system
 - Synchronized clocks: you can use imperative logic, and take advantage of this. You don't need to question yourself on every line of code.
 - Things are under your control: you can do locks & transactions, so take advantage of them

### External Systems ###
Ensure that you have solid trust management on the periphery of your system.
 - Untrusted Boundary
 - Lack of cooridnation: you don't know what other systems will do, or how
 - Unreliable data: you have to assume that data you receive is outdated. You *do* need to second-guess yourself in certain places

### Why is this distinction important? ###
Great companies don't just accept these as 'rules we have to follow', they embrace them as architectural inspiration. For example, node used the restriction of not been able to use blocking code in a world where latency was a factor, and designed an event loop that utilises the available clock cycles to continue processing requests while the (otherwise blocking) code waits, executes & returns. 

When you're designing a system for the web, embrace the nature of distributed systems and take advantage of it. *embrace both worlds*

Like Newton's & Einstein's views, when we look at systems at a low level and then at a high level we will start to see that different rules are relevent.


## Webs and Services ##
The web, the protocol & the messages.

The Web:
"A way to link and access information of various kinds as a web of nodes in which the user can browse at will."

The Protocol:
HTTP/0.9 (1991)
 - GET only
 - HTML only
HTTP full (1992)
 - POST, PUT, DELETE
 - Content Negotiation
 - Headers (metadata)
 - Status Codes (*network-level* self information)
HTTP/1.0 (1996)
 - RFC1945
HTTP/1.1 (1997)
 - Inadequacies are seen, so RFC2068 comes
 - Starts to recognise some key differences in Distributed Systems
 - Conditional GET (takes advantage of caching)
 - Cache-Controls (relative cache timing)
HTTP/1.1 (1999)
 - RFC2616 (the one we use today)
 - Minor updates

A key aspect of HTTP as a low level protocol is that new versions *don't break* previous versions.

### The Message Model ###
Content negotiation: we can negotiate for the format we want to use to communicate.

MIME - Multipurpose Internet Mail Extensions
 - RFC2046 (1996)
 - Designed for email
 - Borrowed the MIME model for WWW
 - although the HTTP header might announce that html is to come, there are lots of embedded types (scripts, images etc)
 - Allows HTTP to provide *representations* (FTP only give you copies of files. In HTTP we can ask for different representations of objects. This forms an key aspect of HTTP - the ability to abstract the format of representation from the underlying protocol)
 - Examples:
     + text/html
     + application/xml
     + application/x-www-forms-urlencoded (how html forms send data, a lot like a query string, the most common means for transferring state)
 - IANA Registers MIME Media Types: if you want to create a message model you register it here. Also registers protocols, link relations, URI schemes, port numbers etc. So the IANA is crucial for scaling applications over message models.
 - MIME Type (classic)
 - Media Type (modern version of roughly the same thing as MIME type, the type of message that's registered)
 - Important: we negotiative the type of *message*, not the type of object, when using HTTP
 - Content Type (HTTP Header that's used to define the Media type in HTTP)

Summary so far: 
 - The WWW (1989)
     + Establishes idea of 'a web of linked nodes'
 - The Protocol (1992)
     + HTTP establishes representation & resource
 - The Messages (1996)
     + Repurposes Email format identifiers for web representations

Another way of thinking about the evolution of the web:
 * The Web of Pages
 * The Web of Apps
 * The Web of Services
 * The Web of APIs

The Web of Pages:
This was originally a web of documents. It was read-only, hyper-linked text. Competed with others:
 - FTP
 - GOPHER
 - WAIS
 - ARCHIE
Most of these counted on a central index server. The idea behind the Web was to be distributed.

Next, the Web of Apps:
This starts with the idea of a 'form' in HTML. Now we've got the transfer of state from the client to the server. Now that we can change data on the server, we can use the Web as an application platform. 
Next comes along XmlHttpRequest which creates a tunneled version of the HTTP client on the client (the web browser). This mimics desktop applications and provides a desktop-like experience in the browser. This gets packed into Ajax in 2005, which gives us the notion of unqiue web apps that can run across any device that supports a browser.

Around the same time that we're moving from a web of documents to a web of apps, we also started to think about a Web of Services.
 - SOAP 1.0 (2001)
     + Roots in CORBA & other IDLs
     + Dave Winder's RSS (& XML-RPC) - the notion of describing services in an XML message and then describing function calls in the same message became a means for exposing a service model to the Web so that it can be integrated into other applications. 
     + SOAP has the notion of 3 parts:
         * Message (envelope & body)
         * Encoding rules for data types (images get base64 encoded & wrapped in XML for example)
         * RPC rules (ways to describe functions, their arguments & return values)
     + It was originally protocol-agnostic (not designed for HTTP only), but the HTTP implementation became the most popular
     + The implementation of SOAP over HTTP is sub-optimal though, because HTTP has a different messaging model:
         * Early SOAP messages couldn't be cached
         * They were unreliable
     + SOAP Made Web Services possible
         * Treats SOAP as a IDL (Interface Description Language)
     + SOAP 1.2 (2007)
         * Caching some aspects of SOAP calls, clean up
         * most apps still run SOAP 1.1

Finally, the Web of APIs:
We've gotten progressively more abstract. From pages, to apps, to services and now just the interface. A lot of the notion of web APIs have their roots in Roy Fielding's 'Architectural Styles and the Design of Network-based Software Architectures'.



## API Targeting ##

## The USE Paradigm ##

## The Discovery Phase for API Design ##

## API Styles ##

## Implement a Solid Foundation ##

## Implementing API Servers ##

## Documenting APIs ##

## Implementing API Clients ##

## Versioning Web APIs ##