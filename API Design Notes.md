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
 REST:
 - Abstract model of HTTP outlined by Roy Fielding:
     + Client-server, stateless (self-contained), & therefore cacheable, layered (reliable)
     + Uniform interface: regardless of your domain, it's the same interface:
        * resources that have addresses
        * representations of those resources
        * stateless messages (cacheable)
        * hypermedia (using the web for business applications)
    + Code on demand: if nothing else works, write client-executable code to fill-in the blanks
- The combination of Web Services with Web Linking is key:
    + HTTP is treated as a transfer protocol using hypermedia: for business apps, we're not just linking from one place to another, but we're *describing* those links.
    + In a nutshell: A representation lets you know the things that are possible at that point, you then use links to transfer state information.
- The notion of a Web of APIs has spawned several implementation models:
    + MVC (adopted from UIs)
    + CRUD (URI style - using HTTP to share objects)
    + Hypermedia (Media types are how we transfer info)

In summary, we have Pages, Apps, Services and APIs.
 - The web of Pages
     + Document centric
 - The web of apps
     + Application centric
 - The web of services
     + Component centric
 - The web of APIs
     + Interface centric


## API Targeting ##
 - API Consumers
 - Acquisition Targets
 - Product Modeling

### API Consumers ###
Private consumers:
usually inside your own organization. Often this means that the product of their work is private or internal. This audience is highly skilled, normally tailored to your technology. You have a lot of control over how they code (you can review & train them). Your API is inherently going to be quite well understood so you may not need to document the API as extensively as you otherwise would. If the documentation might go stale, then don't waste time on it. you can use more jargon that with external consumers. You control the code & the deployment. Your agenda with private consumers is *alignment*. Private APIs can help you strengthen your existing position & reduce costs, or create option value.
Private APIs *Strengthen* your market position by:
     - reducing back-office costs
     - Increasing underlying component reuse
     - speeding time-to-market

Partner Consumers: 
This is where you attempt to create mutual benefit by teaming up in a 'strategic partnership'. Often you'll have SLAs & agreements about QoS. You will have less influence & control over their code & deployment (including release dates). The idea of *alignment* isn't present as much here. Your product might be an SDK - because your partners might not be technically as savy, or you may want to maintain control over some intellectual property.You control when features are available. The agenda here is *co-operation*. Often there are opportunities here to extend your market reach, and in this case you want you API to look like the domain that you're expanding into.
Partner APIs *Extend* your market position by:
     - customize your interface for market segments
     - Gain access to related markets
     - show up in more locations or devices

Public Consumers:
Third parties, app developers, etc. Often no direct relationship with you. You've got no idea how they'll use it or what their skill level will be. Documentation is key here, because the API is your product. The agenda here is *wide open*. Public APIs, despite the risk, offer the chance to discover entirely new markets and build new relationships.
Public APIs help to *discover* new markets by:
 - test entirely new business models
 - dicover new communities
 - treat APIs as product research

Why have an interface at all?

### Acquisition: Reach ###
The measure: do I have more installations/instances? If you want to get into a new space, or raise awareness, then you need to increase your reach. Focusing on reach allows you to leverage existing products.

### Acquisition: Content ###
You may want to increase user-contributed content, even just to have it on hand for analysis. You may want to make new content connections, you can make an API that makes it easy to share. You may also want to just gather behaviour data.

### Acquisition: User ###
You may want to expand the user base, increase user traffic, get into your users *daily workflow*. This helps to deepen customer relationships. You can try levelling up with a user - trading features for user data.

### Product Modeling ###
 - Know your product inside-out
 - Monitoring is vital, as is deep analysis
 - Who is using your API?
 - Are there any potential partners out there?
 - When are your consumers using your API? are there cycles?
 - Measure, measure, measure
 - What are your metrics?
     + API Performance:
         * Latency
         * Uptime
         * Reliability (consistency)
     + Developer Performance
         * "installs"
         * traffic
         * stability
 - You can't improve what your don't measure
 - So, once measures, *improve*!
     + small changes can mean big results
     + test new ideas
     + turn feedback into features
 - You are your own best source of big data


## The USE Paradigm ##
Usable, Scalable, Evolvable.

### Usable ###
The ease of use and learnability of a human-made object. This is all about feedback. An API is an interface just like a tablet or a GUI. 

How do we measure usability?
 - Present use-cases and test them: how many steps? how much indirection?
 - Know who you users are
 - Do empirical measurement: hackathons, codejams, how often do they have to read the documentation?
 - Do all of this as early as possible - iterate

### Scalable ###
This is the ability of a system, network or process to handle a growing amount of work in a capable manner.
 - scaling on hardware only gives minimal gains
 - scaling on the code gets you only so far
 - scaling the *architecture* gives the biggest win: being able to add machines without impacting the system

Scaling out is better than scaling out (for network-based systems). It's harder at first, but over time it's much more reliable.

HOW????
 - Stateless messages on the outside
 - Queues on the inside
==> Stop blocking! 
 - Once you have queues as a pattern, you can start to add more machines to read from the queues! 
 - Take advantage of DevOps: agile infrastructure, scale machines, people, processes around deployment and operations. Get rid of ceremony! Example: Etsi, lots of people can push to production - they've scaled the surface of their workforce that can release to prod.

### Evolvable ###
This is the capacity for a system to *adapt*. 

Small changes over time: being able to change the interface, not the code, is what adds adaptability. 
 - Minor, non-breaking changes
 - New features w/o breaking === evolvability

HOW????
 - Extend (pandere or 'to stretch'): 
     + existing elements *can't be removed* (that's breaking it)
     + can't change the *meaning* of existing processes
     + new elements must be *optional*
 - Versioning (vertere or 'to turn'):
     + don't unless you have to (it's a fork in the road, creating a dead-end)
     + make it easy to identify the version
     + make it hard for users to mistake the version
     + be prepared for clients to ignore version details
     + don't create 'Dodo' apps - don't make dead ends!


## The Discovery Phase for API Design ##
Collect info from stakeholders, aiming to end up with a consolidated, condensed set of crucial information. Define shared actions & vocabulary. Iterative on 'collect' and 'define' until 'done'. Most of the time you'll be done before you're 100% sure - *close enough*.

### Collect ###
 - Figure out what to collect
     + Identify *data* elements
         * Get down to the lowest level of detail (productId, firstName etc)
         * Don't leave anything assumed
         * Even if you think you know all your objects, get them listed out!
         * Identify mandatory/optional
     + Identify *actions* & the data needed for each action
         * again, get rid down to the nitty gritty
     + Identify *critical* paths
         * the order in which actions take place
     + *Don't evaluate*, just collect.
 - one-on-one with key stakeholders
     + come armed with questions
     + ask people to describe the process (rather than asking for data/actions/order)
     + use the 'echo technique'
     + share your notes with them once your done!
 - group discussion
     + focus on sharing the notes from the one-on-ones
     + invite discussion & collabortion
     + work to distill the information
     + moderate, don't edit
 - workshop: present back to complete the feedback loop

### Define ###
When defining data elements:
 - focus on vocab - you're building a dictionary
 - don't try to define objects or hierarchy
 - create a single vocab
 - consolidate but don't create multiple meanings per word
 - use tagging: associations not hierarchies

When defining actions:
 - work to fully describe actions (state transitions)
 - *don't* consolidate - actions are cheap
 - allow for a wide set of actions
 - link actions to categories /tags
 - make actions as specific as possible

Iterative, but know when you're done: *close enough is close enough*

## API Styles ##


## Implement a Solid Foundation ##

## Implementing API Servers ##

## Documenting APIs ##

## Implementing API Clients ##

## Versioning Web APIs ##



