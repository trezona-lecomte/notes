# Fielding's dissertation #

## Background: Defining Software Architecture ##

## Context: what's the problem? ##
The WWW succeeded in large part due to it's architecture - it was designed to 
scale. It was developed iteratively, using the principles of REST. "REST 
emphasizes scalability of component interactions, generality of interfaces,
independent deployment of components, and intermediary components to reduce
interaction latency, enforce security, and encapsulate legacy systems" [xvii]

 - Why do component interactions need to scale, and what are the challenges in 
 doing so?
 - Why should interfaces be general, what are the challenges in making them so, 
 and what does a general interface look like?
     + HTTP and URIs are the two specifications that define the generic 
     interface used by all component interactions on the Web.
 - Why should components be deployed independently?
 - How do intermediary components reduce interaction latency, enforce security 
 and encapsulate legacy systems?

*Complexity* has driven the componentization of systems.

 - How did componentization solve the complexity problem?

*Context* - 'form follows function'

*Conflicting frontiers* - software and networking. "Software research has long 
been concerned with the categorization of software designs and the development 
of design methodologies, but has rarely been able to objectively evaluate the 
impact of various design choices on system behavior. Networking research, in 
contrast, is focused on the details of generic communication behavior between 
systems and improving the performance of particular communication techniques, 
often ignoring the fact that changing the interaction style of an application 
can have more impact on performance than the communication protocols used for 
that interaction."

One of the key challenges of web architecture is interconnecting info systems 
*across organizational boundaries*. Web architecture must be considered in the 
context of sharing *large-grain data objects* across *high-latency* networks 
and multiple *trust boundaries*. 

## Definitions: what is software architecture? ##
### Run-time Abstraction ###
"A software architecture is an *abstraction of the run-time elements* of a
software system during some phase of its operation. A system may be composed of 
many *levels of abstraction* and many phases of operation, each with its own 
software architecture." [5]

Why do we abstract (hide detail)? In order to better identify and sustain it's 
properties. Each level of abstraction has *it's own architecture*. 

"An architecture represents an abstraction of system behavior at level, such 
that architectural elements are delineated by the abstract interfaces they 
provide to other elements at that level" [5]
L. Bass, P. Clements, and R. Kazman. Software Architecture in Practice. Addison
Wesley, Reading, Mass., 1998

"Within each element may be found another architecture, defining the system of 
sub-elements that implement the behaviour represented by the abstract interface.
This recusion of architectures continues down to the most basic system elements:
those that cannot be decomposed into less abstract elements." [6]

Shaw and Clements [122]:
“A component is a unit of software that performs some function at run-time. 
Examples include programs, objects,  processes, and filters.”

### Elements ###
A software architecture is defined by a configuration of architectural elements 
— components, connectors, and data — constrained in their relationships in order
to achieve a desired set of architectural properties.

Perry and Wolf present a definition of architecture that includes the rationale
behind the architectural elements and their form. 
D. E. Perry and A. L. Wolf. Foundations for the study of software architecture. 
ACM SIGSOFT Software Engineering Notes, 17(4), Oct. 1992, pp. 40-52.

Fielding argues that the rationale should not be considered a part of the 
architecture, much as the blueprints of a building are not an inseparable part
of the building's architecture. Rationale is not part of the run-time system.
Once determined, architecture is independent of it's reasons for being.

The distinction between elements is an important aspect of architecture:
 - Processing elements: perform transformations on data
 - Data elements: contain the information that is used & transformed
 - Connecting elements: glue the different pieces together
 
There are two more prevalent terms, *Components* and *Connectors*, that can be
used to refer to Processing and Connecting elements respectively.

Architecture cannot, however be reduced to architecture diagrams, boxes 
(components) and lines (connectors). Data elements, along with many of the
dynamic aspects of real software architectures are ignored by such diagrams.
These models are incapable of describing network-based architectures because
*the nature, location, and movement of data elements within the system is often
the single most important determinant of system behaviour*.

#### Components ####
"A component is an abstract unit of software instructions and internal state 
that provides a transformation of data via its interface."

"A component is defined by its interface and the services it provides to other 
components, rather than by its implementation behind the interface."

#### Connectors ####
"A connector is an abstract mechanism that mediates communication, coordination,
or cooperation among components."

Examples include:
 - shared representations
 - remote procedure calls
 - message-passing protocols
 - data streams
 
Connectors enable communication between components by transferring data from one
interface to another *without changing the data*. Internally a connector may 
well contain a system of sub-components, for transforming the data for transfer,
executing the transfer, and then reversing the transformation for delivery, but
the external behaviour is that of non-transformational transfer.

#### Data ####
"A datum is an element of information that is transferred from a component, or 
received by a component, via a connector."

Examples include:
 - byte-sequences
 - messages
 - marshalled parameters
 - serialized objects
 
This doesn't include information that is permanently resident or hidden within
a component.

#### Configurations ####
"A configuration is the structure of architectural relationships among 
components, connectors, and data during a period of system run-time."

#### Properties ####
These include functional and non-functional, for example:
 - relative ease of evolution
 - reusability of components
 - efficiency
 - dynamic extensibility

"The goal of architectural design is to create an architecture with a set of 
architectural properties that form a superset of the system requirements."

#### Styles ####
"An architectural style is a coordinated set of architectural constraints that 
restricts the roles/features of architectural elements and the allowed 
relationships among those elements within any architecture that conforms to 
that style."

Formal: "a pattern of interactions among typed components" -but this doesn't 
leave much room for thinking of the architecture as a running system...

One goal of a style is to capture the essence of a pattern of interaction by
ignoring the incidental details of the rest of the architecure.
M. Shaw. Toward higher-level abstractions for software systems. Data & Knowledge 
Engineering, 5, 1990, pp. 119-128.

Another goal is to encapsulate *important* decisions about the architectural 
elements and emphasize *important* constraints on the elements & their relations.

## Architectural views ##
An architectural viewpoint is often application-specific and varies widely 
based on the application domain. ... we have seen architectural viewpoints that 
address a variety of issues, including: 
 - temporal issues
 - state and control approaches
 - data representation
 - transaction life cycle
 - security safeguards
 - and peak demand and graceful degradation
No doubt there are many more possible viewpoints."
^
N. L. Kerth and W. Cunningham. Using patterns to improve our architectural 
vision. IEEE Software, 14(1), Jan. 1997, pp. 53-59.
 
Perry and Wolf describe 3 important views: processing, data & connection views.

## Network-based application architectures ##
When interactions between components are capable of being realised in network
communication, we are dealing with the highest level of abstraction in 
software architecture.

"The primary distinction between network-based architectures and software
architectures in general is that communication between components is restricted
to message passing, or the equivalent of message passing if a more efficient
mechanism can be selected at run-time based on the location of components."

### Network-based vs. Distributed ###
"a distributed system is one that looks to its users like an ordinary 
centralized system, but runs on multiple, independent CPUs. In contrast, 
network-based systems are those capable of operation across a network, but not 
necessarily in a fashion that is transparent to the user."
A. S. Tanenbaum and R. van Renesse. Distributed operating systems. ACM Computing 
Surveys, 17(4), Dec. 1985, pp. 419-470.
 ????????
 
### Evaluation of Software Architecture ###
"In order to evaluate an architectural design, we need to examine the design 
rationale behind the constraints it places on a system, and compare the 
properties derived from those constraints to the target application's 
objectives."

 - first level of evaluation: application's functional requirements
 - next, consider the relative emphasis on the various non-functional 
   requirements
 
Architectural Properties:
Performance
    + Component interactions can be the dominant factor in determining the 
      performance that a user perceives in a network-based system
    + Performance is bound by:
        1. the application requirements, then by
        2. the chosen interaction style, then by 
        3. the realized architecture, and finally by
        4. the implementation of each component
    + Software can't avoid the basic cost of achieving the application needs.
    + An architecture can't be more efficient than its interaction style allows
    + Finally, no interaction can take place faster than a component 
      implementation can produce data & its recipient can consume data.

Network Performance Measures:
 - Throughput: rate at which information is transferred between components
 - Overhead: initial setup overhead & per-interaction overhead, which is a 
             distinction that is useful for identifying connectors that can
             share setup overhead across multiple interactions (amortization)
 - Bandwidth: the maximum available throughput over a given network link
 - Usable Bandwidth: portion of bandwidth available to the application

Styles impact network performance by their influence on the number of
interactions per user action and the granularity of data elements:

"A style that encourages small, strongly typed interactions will be efficient in
an application involving small data transfers among known components, but will 
cause excessive overhead within applications that involve large data transfers 
or negotiated interfaces. Likewise, a style that involves the coordination of 
multiple components arranged to filter a large data stream will be out of place 
in an application that primarily requires small control messages."

#### User-perceived performance ####
The primary measures for this are latency & completion time. 

Latency is the time period between initial stimuls and the first indication of
a response. Latency occurs during the processing of a network-based app:
 1. time needed for app to recognize the event that initiated the action
 2. time required to set up the interactions between components
 3. time required to transmit each interaction to the components
 4. time required to process each interaction on those components
 5. time required to complete the sufficient transfer and processing of the 
   result of the interactions before the app is able to render a usable result

Although only 3 & 5 represent actual network communication, all five points can
be impacted by the architectural style. Further, multiple component interactions
per user action are additive to latency unless they take place in parallel.

Completion is the amount of time taken to complete an application action. The 
difference between completion time and latency is that latency can represent
increments of processing.

*Important*: optimizations that improve latency will often degrade completion
time, and vice versa: " For example, compression of a data stream can produce a 
more efficient encoding if the algorithm samples a significant portion of the 
data before producing the encoded transformation, resulting in a shorter 
completion time to transfer the encoded data across the network. However, if 
this compression is being performed on-the-fly in response to a user action, 
then buffering a large sample before transfer may produce an unacceptable 
latency. Balancing these trade-offs can be difficult, particularly when it is 
unknown whether the recipient cares more about latency (e.g., Web browsers) or 
completion (e.g., Web spiders)."
 
*Interesting* The best strategy for peformance is to minimize network usage!
This can be done through caching, reduction of the frequency of network 
interactions in relation to user actions (replicated data and disconnected
operation) and by removing the need for some interactions by moving the 
processing closer to the source of the data (*mobile code*).

The properties of a style must be framed in relation to the appropriate 
interaction distance:
 - within a single process
 - across processes on single host
 - inside a local-area network (WAN)
 - spread across a wide-area network (WAN)
 - across the internet (many trust boundaries)]

#### Scalability ####
This refers to the ability of an architecture to support large numbers of 
components, or interactions among components, within an active configuration.
This can be improved by simplifying components, distributing services across 
many components (decentralizing the interactions), and by controlloing
interactions & configurations as a result of monitoring. "Styles influence 
these factors by determining the location of application state, the extent of
distribution, and the coupling between components."

Some more factors that impact scalability:
 - frequency of interactions
 - distribution of load on a component (time: peaks or consistent)
 - level of guarantee provided by component (best effort, guaranteed delivery)
 - whether a request is synchronous or asynchronous
 - whether the environment is controlled or anarchic (trusted components?)

#### Simplicity ####
The primary means by which an architectural style can achieve simplicity is 
through the separation of concerns. The clean allocation of functionality across
components leads to an architecture that is easier to reason about. 

Simplicity includes:
 - the level of complexity
 - understandability
 - verifiability

Another contributing factor to simplicity is generality - the more general the
elements within an architecture, the less variation.

#### Modifiability ####
The ease with which changes can be made to an application architecture, this
encompases:
 - evolvability
 - extensibility
 - customizability
 - configurability 
 - reusability

Particular to network-based systems is dynamic modifiability, where changes are
made to a deployed application without stopping & restarting the system.

The end-goal is to be prepared for gradual and fragmented change, as any 
network-based application will be distributed across multiple organizational
boundaries so will encounter staggered changes between old & new implementations
of a variety of other systems.

Evolvability: how easily a component can change without negatively impacting
other components.

Extensibility: how easily functionality can be added to a system. Dynamic 
extensiblity is how easily it can be added without impacing the rest of the 
system. This can be increased by decoupling components (such as with event-based
integration)

Customizability: how easily the behaviour of an architectural element can be
temporarily specialized for one client without adversely impacting other clients.
This is induced by the remote evaluation and code-on-demand styles.

Configurability: related to both extensibility and reusability, as it refers to
post-deployment modification of components (or configurations of components),
such that they're made capable of new services/data element types. The pipe-and-
filter and code-on-demand styles are examples that induce configurability (of
components and configurations, respectively).

Reusability: the degree to which components, connectors or data elements can be
reused (without modification) in other applications. The primary mechanisms for
achieving this in architectural styles are reduction of coupling (knowledge of
identity) between components and the constraint of generality of component
interfaces. The uniform pipe-and-filter style exemplifies these constraints.

#### Visiblity ####
The ability of a component to monitor or mediate the interactions between two 
other components. Architectural styles can also influence the visiblity of 
interactions within a network-based app by restricting interfaces via generality
or providing access to monitoring. 

This can improve performance via shared caching or interactions, scalability via
layered services, reliability via reflective monitoring, and security via 
allowing interactions to be inspected by mediators (e.g. firewalls). The mobile
agent style is an example where the lack of visiblity may lead to security 
concerns.

#### Portability ####
Software is portable if it can

#### Reliablity ####


## Styles for Network-based Hypermedia systems ##

### Data-flow Styles ###

| Style  | Deriv.  | Net perf | UP perf | Eff. | Scal. | Simp. |Evo. | Ext. | Cust. | Conf. | Reus. | Vis. | Port. | Rel. |
| :-----:|:-------:|:--------:|:-------:|:----:|:-----:|:-----:|:---:|:----:|:-----:|:-----:|:-----:|:----:|:-----:|:----:|
| PF     |         |          | +-      |      |       | +     | +   | +    |       | +     | +     |      |       |      |
| UPF    | PF      | -        | +-      |      |       | ++    | +   | +    |       | ++    | ++    | +    |       |      |

#### Pipe and Filter (PF) ####
In this style, each component (filter) reads streams of data on its inputs and
produces streams of data on its outputs, usually while applying a transformation
to the input streams and processing them incrementally so that output begins 
before the input is completely consumed. This style is also referred to as a 
one-way data flow network. The constraint here is that a filter must be 
completely independent of other filters (zero coupling): it must not share 
state, control thread, or identify with the other filters on its upstream and
downstream interfaces.

Advantages:
 - Simplicity: overall i/o of system is a simple composition of the behaviours
   of the individual filters. 
 - Reusability: any two filters can be hooked together, provided they are agreed
   on the data that is being transmitted between them.
 - Extensibility: new filters can easily be added to existing systems.
 - Evolvability: existing filters can be replace by improved ones.
 - Verifiability: they permit certain kinds of specialized analysis such as
   throughput and deadlock analysis.
 - User-Perceived Performance: they naturally support concurrent execution

Disadvantages:
 - propogation delay is added through long pipelines
 - batch sequential processing occurs if a filter cannot incrementally process
   its inputs
 - no interactivity is allowed because a filter cannot know that any particular 
   output stream shares a controller with any particular input stream.
   
The controller function (or invisible hand) that configures the filters prior to
activation is considered a separate operational phase of the system, hence a 
separate architecture, even though one cannot exist without the other.

#### Unfiform Pipe and Filter (UPF) ####
This style adds the constraint that all filters must have the *same interface*.
A prime example of this is found in the Unix Operating System, where filter 
processes have an interface consisting of one input data stream of characters 
(stdin) and two output data streams of characters (stdout and stderr). 
Restricting the interface allows independently developed filters to be arranged
at will to form new applications. It also simplifies the task of understanding
how a given filter works.

A disadvantage to this approach is that it may reduce network performance as
the data needs to be converted to and from it's natural format.


### Replication Styles ###

| Style  | Deriv.  | Net perf | UP perf | Eff. | Scal. | Simp. |Evo. | Ext. | Cust. | Conf. | Reus. | Vis. | Port. | Rel. |
| :-----:|:-------:|:--------:|:-------:|:----:|:-----:|:-----:|:---:|:----:|:-----:|:-----:|:-----:|:----:|:-----:|:----:|
| RR     |         |          | ++      |      | +     |       |     |      |       |       |       |      |       | +    |
| $      | RR      |          | +       | +    | +     | +     |     |      |       |       |       |      |       |      |

### Replicated Repository (RR) ###
This style improves the accessibilit of data and scalability of services by 
having more than one process provide the same service. These decentralized
servers interact to provide clients the illusion that there is only one service.
Distributed systems such as XMS and remote versioning systems such as CVS are
primary examples.

The main advantage is user-perceived performance, both in terms of latency and
in terms of the enablement of disconnected operation in the event of primary
server failure or intentional off-network roaming. Simplicity is neutral, since
the complexity of replication is offset by the savings of allowing network-
unaware components to operate transparently on locally replicated data.
Maintaining consistency is the main difficulty.

### Cache ($) ###
The Cache style is a derivative of the RR style. This is where the result of an
individual request is replicated such that it may be reused by later requests.
This style is most often found where the potential data set far exceeds the 
capacity of any one client, as in the WWW, or where complete access to the
repository isn't necessary. *Lazy replication* is where data is replicated upon
a not-yet-cached response for a request, relying on locality of reference and
commonality of interest to propogate useful items into the cache for later
reuse. Active replication is where cacheable entries are pre-fetched based on
the anticipated requests. 

Caching provides slightly less improvement that the RR style in terms of user-
perceived performance, since more requests will miss the cache and only the 
recently accessed data will be available for disconnected operation. On the 
other hand, caching is much easier to implement, doesn't request as much 
processing and storage, and is more efficient. The Cache style becomes network-
based when it is used in conjunction with a client-stateless-server style.


## Hierarchical Styles ##

| Style  | Deriv.   | Net perf | UP perf | Eff. | Scal. | Simp. |Evo. | Ext. | Cust. | Conf. | Reus. | Vis. | Port. | Rel. |
| :-----:|:--------:|:--------:|:-------:|:----:|:-----:|:-----:|:---:|:----:|:-----:|:-----:|:-----:|:----:|:-----:|:----:|
| CS     |          |          |         |      | +     | +     | +   |      |       |       |       |      |       |      |
| LS     |          |          | -       |      | +     |       | +   |      |       |       | +     |      | +     |      |
| LCS    | CS+LS    |          | -       |      | ++    | +     | ++  |      |       |       | +     |      | +     |      |
| CSS    | CS       | -        |         |      | ++    | +     | +   |      |       |       |       | +    |       | +    |
| C$SS   | CSS+$    | -        | +       | +    | ++    | +     | +   |      |       |       |       | +    |       | +    |
| LC$SS  | LCS+C$SS | -        | +-      | +    | +++   | ++    | ++  |      |       |       | +     | +    | +     | +    |
| RS     | CS       |          |         | +    |       | +     | +   |      |       |       |       | -    |       |      |
| RDA    | CS       |          |         | +    |       |       |     |      |       |       |       | +    |       | -    |

### Client-Server (CS) ###
This is the most frequently encountered architectural style for network-based
applications. 

A server component, offering a set of services, listens for requests upon those
services. A Client component, desiring that service to be performed, sends a
request to the server via a connector. The server either rejects or performs the
request and sends a response back to the client. 

The main principle behind this style is the separation of concerns. This leads
to increased simplicitly, scalability and evolvability.

This base form of client-server does not constrain how application state is
partitioned between client and server components. It is often referred to by
the mechanisms used for connector implementation, such as RPC or message-
oriented middleware.

### Layered System (LS) and Layered-Client-Server (LCS) ###
A layered system is organized hierarchically, with each layer providing services
to the layer above and consuming services from the layer below. 

Layered system reduce coupling between layers by hiding layers from all but the
layer immediately above them (that consumes them). This improves evolvability
and reusability. 

Examples include layered communication protocals such as TCP/IP and OSI protocol
stacks, and hardware interface libraries. 

The main disadvantage of layered systems is the additional overhead and latency,
reducing user-perceived performance.

Layered-Client-Server adds proxy and gateway components to the Client-Server
style. A proxy is a shared server for one or more components, forwarding 
requests (with possible translation) to servers. A gateway components appears
as a normal server to client & proxies, but it actually forwards requests to
'inner-layer' servers. 

These addition mediator components can be added in multiple layers to add
features like load balancing and security checking.

Architectures based on layered-client-server are referred to as two-tiered, 
three-tiered or multi-tiered architectures.

LCS is also a solution to managing identity in large scale distributed systems,
where complete knowledge of all servers would be prohibitively expensive. 

### Client-Stateless-Server (CSS) ###
A derivative of the CS style, but with the additional constraint that no 
*session state* is allowed on the server component. Each request from client to
server must contain all the information necessary to understand the request,
and cannot take advantage of any stored context on the server. 

This constraint improves the following properties:
 - Visibility: monitoring systems don't have to look beyond single requests
 - Realiability: the task of recovering from partial failures is easier
 - Scalability: the server can quickly free resources following a request as it
                doesn't have to maintain any state for further requests in the
                same session

The disadvantage is that network performance may be decreased by the repetitive
data (per-interaction overhead) sent in a series of requests.

### Client-Cache-Stateless-Server (C$SS) ###
This is the client-stateless-server with cache component(s) added. The cache
acts as a mediator between client and server, so cacheable requests can be 
reused. An example of this is Sun Microsystems NFS.

The advantage of an added cache component with client-server style architectures
is the complete or partial elimination of some interactions, improving efficieny
and user-perceived performance.

### Layerered-Client-Cache-Stateless-Server (LC$SS) ###
This style derives from both the layered-client-server and 
client-cache-stateless-server styles, through the addition of proxy and/or 
gateway components to the latter. An example of this is the Internet domain 
name system (DNS).

The advantages/disadvantages are simply a combination of those for LCS and C$SS,
however note that we don't count the contributions of the CS style twice since
the benefits aren't additive when they come from the same ancestral derivation.

### Remote Session (RS) ###
This style is a variant of client-server that attempts to minimize complexity
or maximize reuse of child components rather than the server component.

Each client initiates a session on the server then invokes a series of services.
Application state is kept entirely on the server. Examples include TELNET & FTP.

The advantages are:
 - its easier to centrally maintain the interface of the server
 - efficiency is increased if the interactions make extended use of the session
   context on the server
   
The disadvantages are:
 - reduced scalability of the server, due to stored state
 - reduced visibility of interactions, since monitoring components would have to
   know the state on the server
   
### Remote Data Access (RDA) ###
A variant of clinet-server that spreads state between the client and the server.

Clients send database queries in a standard format such as SQL to remote 
servers. The server allocates a workspace & performs the query. The client then
may make further operations on the resulting set, or retrieve the result on
piece at a time. The client is, clearly, required to know about the data 
structure of the service. 

The advantage of this style is that large datasets can be reduced while on the
server (reducing network traffic, efficiency). Visibility is also improved by
using a standard query language. 

The disadvantages are that the client needs to understand the same database
manipulation concepts as the server (reducing simplicity) and storing the 
application context on the server reduces scalability. Reliability also suffers,
as partial failure can leave the workspace in an unkown state. Transaction
mechanisms like two-phase commit can be used to fix this problem, though at a
cost of added complexity and interaction overhead.


## Mobile Code Styles ##
These styles tackle the challenge of distance using mobility - they dynamically
change the distance between processing and data source/data destination. The 
concept of location is introduced at an architectural level, making it possible 
to model the cost of interactions between components. In all of the mobile code
styles, a *data element is dynamically transformed into a component*.

| Style    | Deriv.    | Net perf | UP perf | Eff. | Scal. | Simp. |Evo. | Ext. | Cust. | Conf. | Reus. | Vis. | Port. | Rel. |
| :-------:|:---------:|:--------:|:-------:|:----:|:-----:|:-----:|:---:|:----:|:-----:|:-----:|:-----:|:----:|:-----:|:----:|
| VM       |           |          |         |      |       | +-    |     | +    |       |       |       | -    | +     |      |
| REV      | CS+VM     |          |         | +    | -     | +-    |     | +    | +     |       |       | -    | +     | -    |
| COD      | CS+VM     |          | +       | +    | +     | +-    |     | +    |       | +     |       | -    |       |      |
| LCODC$SS | LC$SS+COD | -        | ++      | ++   | +4+   | ++-+  | ++  | +    |       | +     | +     | +-   | +     | +    |
| MA       | REV+COD   |          | +       | ++   |       | +-    |     | ++   | +     | +     |       | -    | +     |      |


### Virtual Machine (VM) ###
The notion of a Virtual Machine, or interpreter, style unerpins all of the 
mobile code styles. It isn't inherently a network-based style, but is commonly
used as such in conjunction with a component in the client-server style.

The primary benefits are portability (separation of instruction & implementation
) and extensibility. Visibility and Simplicity are generally reduced.

### Remote Evaluation (REV) ###
This is derived from the client-server and virtual machine styles. A client
component has the knowledge necessary to perform a service, but lacks the 
resources required. These resources are located at a remote site, so the client
sends the knowledge to a server at the remote site which executes the code 
using the resources available there. The results are sent back to the client.
This style assumes that the code will be executed in an isolated environment,
so it won't impact other clients aside from the resource usage.

Advantages include extensibility & customizability (due to the ability to 
customize the server's services) and better efficiency as the code can adapt
its actions to the environment in the server. Simplicity is reduced, because
the evaluation environment must be managed. Scalability is reduced, but the
most significant sacrifice is then lack of visibility due to the client sending
code instead of standardized queries. 

### Code on Demand (COD) ###
In this style, a client component has access to resources, but not the 
knowledge of how to process them. It sends a request to a remote server for the
code representing that knowledge, then executes it locally.

Advantages include extendsibility and configurability (as you can add features
to the deployed client) and better user-perceived performance and efficieny
as the code can adapt its actions to the client's environment and interact with
the user locally rather than through remote interactions. Scalability of the 
server is also improved since it can off-load work to the client.

Simplicity is reduced due to managing the evaluation environment. Like remote
evaluation, the most significant limitation is the lack of visibility due to
the server sending code instead of simple data.

### Layered-Code-on-Demand-Client-Cache-Stateless-Server (LCODC$SS) ###
This syle is an example of complementary architectural styles. It involves the
addition of code on demand to the layered-client-cache-stateless-server style.
Here, the code is treated as just another data element, so it doesn't interfere
with the advantages of the LC$SS style. An example is HotJava Web browser which
allows applets and protocol extensions to be downloaded as typed media. The
pros and cons are simply the sum of those for COD and LC$SS.

### Mobile Agent (MA) ###
In this style, entire computational units are moved to a remote site along with
their state, the code they need and possibly some data required to perform their
task. This is a derivation of the REV and COD styles since the mobility goes
both ways. 

The biggest advantage here (beyond those of REV and COD) is the greater
dynamism in the selection of when to move the code. An app can be in the midst
of processing information at one location when it decides to move to another
location (presumably to reduce the distance between it and the next set of data
it wishes to process). Also, the reliability problem of partial failure is
reduced because the app state is only in one location at a time.

## Peer to Peer styles ##

| Style| Deriv.  | Net perf | UP perf | Eff. | Scal. | Simp. |Evo. | Ext. | Cust. | Conf. | Reus. | Vis. | Port. | Rel. |
| :---:|:-------:|:--------:|:-------:|:----:|:-----:|:-----:|:---:|:----:|:-----:|:-----:|:-----:|:----:|:-----:|:----:|
| EBI  |         |          |         | +    | --    | +-    | +   | +    |       | +     | +     | -    |       | -    |
| C2   | EBI+LCS |          | -       | +    |       | +     | ++  | +    |       | +     | ++    | +-   | +     | +-   |
| DO   | CS+CS   | -        |         | +    |       |       | +   | +    |       | +     | +     | -    |       | -    |
| BDO  | DO+LCS  | -        | -       |      |       |       | ++  | +    |       | +     | ++    | -    | +     |      |


### Event-based Integartion (EBI) ###
This is also known as implicit invovation or event system style. EBI reduces
coupling between components by removing the need for identity on the connector
interface. Instead of invoking another component directly, a component can
broadcast one or more events. Other components then register intererst in that
type of event and are invoked by the system when an event is announced. Examples
include the MVC paradigm in Smalltalk-80.

Advantages:
 - extensibility: easy to add new components that listen for events
 - reusability: encourages a general event interface & integration mechanism
 - evolvability: allows replacement of components w/o affecting other interfaces
 - efficiency: can remove need for polling
 
 Disadvantages:
 - scalability: event storms as events trigger more events
 - reliability: single point of failure in the event bus, partial failure risk
 - simplicity: its hard to anticipate what will happen in response to an action

### C2 ###
This style is directed at supporting large-grain reuse and flexible composition
of components by enforcing *substrate independence*. This is done by combining
event-based integration with layered-client-server. Asynchronous notification
messages going down & asynchronous request messages going up are the sole means
of intercomponent communication. This enforces loose coupling with higher layers
(service requests may be ignored) and zero coupling with lower layers (no 
knowledge of notification usage).

Notifications are announcements of state change within a component. Connectors
are responsible for routing and broadcasting message, as well as message
filtering. Layered filtering of messages solves EBIs scalability problems, while
improving evolvability and reusability. Heavyweight connectors that include
monitoring can improve visibility and reduce reliability problems.

### Distributed Objects (DO) ###
This style views a system as a set of peer components. An object is 
 - an entity that encapsulates some private state information or data
 - a set of associated operations or procedures that manipulate the data
 - possibly a thread of control
such that these parts can be considered a single unit. Generally an object's
state is completely hidden and protected from all other objects. The only  way
it can be accessed is by a request/invocation on one of it's publicly accessible
operations. 

An operation may invoke operations on the same object or another object. A chain
of related invocations is referred to as an *action*. State is distributed 
among the objects, which is advantageous in terms of keeping state in the 
location where it is most likely to be up-to-date, but is a disadvantage in that
its difficult to obtain an overall system activity view (poor visibility).

In order for one object to interact with another, it must know the identity of
that other object. When an identity changes all of the invoking objects must
also be changed. The must also be a controller object that is responsible for
maintaining the system state. 

Issues encountered when using DO can be:
 - object management
 - object interaction management
 - resource management
 
Due to the isolation of data, data streaming is not generally supported. This is
better for object mobility than the mobile agent style, however.

### Brokered Distributed Objects (BDO) ###
To reduce the impact of identity, modern DO systems use more intermediary styles
to facilitate communication, including event-based integration and brokered
client-server. The BDO style introduces name resolver components who answer
client requests for general service names. This improves reusability and
evolvability but reduces efficiency and user-perceived performance.

An example of this style is CORBA. These systems fare poorly when compared to
most other network-based architectural styles. They're best for apps that 
involve the remote invocation of encapsulated services (such as hardware 
devices) where the efficiency & frequency of network interactions is not so
paramount.

## Designing the Web Architecture: Problems and Insights ##

### WWW Application Domain Requirements ###
The "Web's major goal was to be a shared information space through which people
and machines could communicate."

So we need:
 - universally consistent interface to structured information
 - availability of wide range of platforms
 - incrementally deployable as new people/organizations join

### Low Entry-Barrier ###
Hypermedia was chosen as the user interface because of its simplicity and
generality:
 - the same interface can be used regardless of the information source
 - the flexibility of hypermedia relationship (links) allows for unlimited
    structuring
 - the direct manipulation of links allows the complex relationship within the
    information to guide the reader through an application


Since information within large databases is often much easier to access via a 
search interface rather than browsing, the Web also incorporated the ability to
perform simple queries by providing user-entered data to a service and rendering
the result as hypermedia.

Goals:
 - Reliability: partail availability of the overall system must not prevent the
   authoring of content. 
 - hypertext language needs to be simple & capable of being created using common
   tools
 - must be able to create references to information before that information
   exists
 - simplicity: all protocols were defined as text so that communication could be
   viewed and interatively tested using existing network tools

### Distributed Hypermedia ###
This is defined by *the presence of application control information embedded
within, or as a layer before, the presentation of information*. Distributed
Hypermedia allows the presentation and control information to be stored at 
remote locations. By it's nature, user actions within a distributed hypermedia
system require the transfer of large amounts of data from where the data is
stored to where it is used. Thus, the Web architecture must be designed for 
large-grain data transfer. 

The usability of hypermedia is highly sensitive to user-perceived latency: the
time between selecting a link and the rendering of a usable result. Since the
Web's information sources are distributed across the global Internet, the 
architecture needs to minimize network transactions (round-trips within the 
data transfer protocols).

### Internet Scale ###
Scale for the WWW is more than just geographical dispersion - it's about 
interconnecting networks across multiple organizational boundaries. 

#### Anarchic Scalability ####
Many software systems are underpinned by the assumption that there is a single
controlling entity or that at least all entities are acting towards a common
goal. This assumption is folly on the Internet. Anarchic scalability refers to
the need for architectural elements to *continue operation* when they are 
subjected to *unanticipated load* or *malformed/malicious data*.

The requirement of anarchic scalability *applies to all architectural elements*.
Clients can't maintain knowledge of all servers, and servers can't maintain 
knowledge of state across requests. 

Hypermedia data elements can't retain 'back-pointers' (an id for each data
element that references them), since the number of refs to a resource is
proportional to the number of people interested in that info. 

Security is also a significant concern. Multiple organizational boundaries 
implies multiple trust boundaries. Intermediary applications, such as firewalls,
should be able to inspect interactions to enforce security constraints. 
Assumptions should be able to be made about authentication & authorization,
however since authentication degrades scalability, the architectures default
operation should be limited to actions that don't need trusted data: a safe set
of operations with well-defined schematics.

#### Independent Deployment ####
Multiple organizational boundaries also means:
 - gradual & fragmented change
 - co-existence of old & new implementations
 - encapsulation of older implementations
 - identification of old vs. new implementations
 - easy deployment of elements in partial, iterative fashion

### Problem ###

#### Architectural Style of the early WWW ####
Basis 1. The design rationale behind the WWW architecture can be described by an 
architectural style consisting of a set of constraints applied to the elements
within the Web architecture.

Basis 2. Constraints can be added to the WWW architectural style to derive a
new hybrid style that better reflects the desired properties of a modern Web
architecture.

Basis 3. Proposals to modify the Web architecture can be compared to the 
updated WWW architectural style & analysed for conflicts prior to deployment.

## Representational State Transfer (REST) ##
REST is a hybrid style derived from several other network-based architectural
styles, combined with the additional constraints that define a uniform connector
interface. 

REST was designed with the 'Null style' as a starting point: a system in which
there are no distinguished boundaries between components.

![alt text](https://www.ics.uci.edu/~fielding/pubs/dissertation/null_style.gif "Null Style")

#### Client-Server ####
The first constraints added are those of the client-server style, namely it's
core principle of the separation of concerns. We improve the portability of the
UI across multiple platforms by separating the UI concerns from the data storage
concerns. This also simplifies the server components, improving scalability.
Perhaps the most significant advantage for the WWWs purpose is that this 
separation allows the components to evolve independently, thus allowing for 
multiple organizational domains.

![alt text](https://www.ics.uci.edu/~fielding/pubs/dissertation/client_server_style.gif "CS Style")

#### Stateless ####
Next we add a constraint to the client-server communication: it must be 
stateless. This means that each request from the client must contain all the 
info necessary for the server to understand it, and can't take advantage of any
*stored context* on the server. Session state is kept entirely on the client.

![alt text](https://www.ics.uci.edu/~fielding/pubs/dissertation/stateless_cs.gif "Stateless")

This induces the properties of:
 - visibility: monitoring systems can determine full nature of a request from 
               inspecting just that request
 - reliability: partial failures are easier to recover from
 - scalability: servers can quickly free-up resources
 - simplicity: servers don't have to manage resource usage across requests

The trade-off is that it induces the disadvantages of:
 - network performance: increase of repetitive data (per-interaction overhead)

#### Cache ####
In order to improve network efficiency, we add cache constraints. This requires
that data within a response to a request must be implicitly or explicitly 
labelled as cacheable or non-cacheable. Cacheable responses are allowed to be
reused by clients for later, equivalent requests.

![alt text](https://www.ics.uci.edu/~fielding/pubs/dissertation/ccss_style.gif "Cache")

The advantage is the potential for partially or completely eliminating some
interactions, improving:
 - efficiency
 - scalability
 - user-perceieved performance (reduction of average latency for series of 
                                interactions)
The trade-off is that a cache can decrease reliability if stale data differs
significantly from the current data. 

The design rationale of the Web architecture prior to 1994 focused on stateless
client-server interaction for the exchange of static documents over the Internet.
There was rudimentary support for non-shared caches, but there was no constraint
on the interface to provide a consistent set of semantics for all resources to
be cached. 

![alt text](https://www.ics.uci.edu/~fielding/pubs/dissertation/early_web_arch.gif "Early Web Arch.")

The following styles were then added to the Web's architectural style in order
to guide the extensions that form the modern Web.

#### Uniform Interface ####
The core of REST, at least opposed to other network-based styles, is its
emphasis on a *uniform interface* between components. This provides the
following benefits:
 - simplicity
 - visibility
 - evolvability (implementations are decoupled from the services they provide)

The trade-off is that efficiency is degraded, since information is transferred
in a standardized form rather than one that is native to each application's
needs. The REST interface is designed to be efficient for *large-grain 
hypermedia* data transfer.

![alt text](https://www.ics.uci.edu/~fielding/pubs/dissertation/uniform_ccss.gif "Uniform Interface")

But how do we actually obtain a uniform interface? It is through a combination
of architectural constraints on the interface:
 - *identification* of resources
 - manipulation of resources *through representations*
 - *self-descriptive* messages
 - *HATEOAS* - hypermedia as the engine of application state

#### Layered System ####
Next, the layered system style is added to contrain the Web architecture to be
composed of hierarchical layers, because each component cannot 'see' beyond the
immediate layer with which they are interacting. By restricting this line-of-
sight, a bound is placed on overall system complexity and substrate independence
is promoted. Legacy services can be encapsulated and intermediaries can be used
to improve system scalability by enabling load balancing.

![alt text](https://www.ics.uci.edu/~fielding/pubs/dissertation/layered_uccss.gif "Layered System")

The trade-off is that layers add overhead and latency to the processing of data,
reducing user-perceived performance. This can be offset by shared caching at
intermediaries. 

--
The combination of a uniform interface and a layered system induces properties
similar to those of the uniform pipe-and-filter style. Although REST interaction
is two-way, the large-grain data flows of hypermedia interaction can be 
processed like a data-flow network, with filter components selectively applied
to the data stream in order to transform the content as it passes. 
--
What enables intermediary components to actively transform the content of 
messages? It's the fact that the messages are *self-descriptive* and their
semantics are *visible* to the intermediaries.

#### Code-On-Demand ####
The final addition to our constraint set for REST is code-on-demand. REST allows
client functionality to be extended by downloading & executing code in the form
of applets or scripts. The induces:
 - simplicity (reduces the number of features that have to be pre-implemented)
 - extensibility

The trade-off is that visibility is reduced, and so this constraint is actually
an *optional* one within REST.

![alt text](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_style.gif "Code-On-Demand")

#### Style Summary ####

![alt text](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_derivation.gif "Code-On-Demand")

## REST Architectural Elements ##

### Data Elements ###
Unlike the Distributed Object style, where all data is encapsulated within
and hidden by the processing components, the nature and state of an
architecture's data elements is a key aspect of REST. The reason for this lies
in the nature of *distributed hypermedia*. When a link is selected, information 
needs to be moved from the location where it is stored to the location where it
will be used by, in most cases, a human reader. This is unlike many other 
distributed processing paradigms, where it is possible, and usually more 
efficient, to move the "processing agent" (e.g., mobile code, stored procedure,
search expression, etc.) to the data rather than move the data to the 
processor.

Thus, there are only 3 fundamental options:
    1. render the data where it is located and send a fixed-format image
    2. encapsulate the data with a rendering engine and send both
    3. send the raw data to the recipient along with its metadata, so the 
       recipient can choose their own rendering engine

These all have their pros and cons:

1. (traditional client-server):
 - client implementation is easier as no knowledge of the data is needed
 - functionality on the client is severely restricted
 - processing load is almost entirely on the server, reducing scalability

 2. (mobile object):
 - provides information hiding (as with #1)
 - enables specialized processing of the data via the unique rendering engine
 - again restricts the functionality of the recipient to what is built into
   its engine
 - may vastly increase the amount of data transferred

 3. (sending raw data w/ metadata):
 - server remains scalable
 - loses the advantage of information hiding
 - requires that both the server and client understand the same data types

REST actually uses a *hybrid* of all 3 options, by focusing on a shared 
understanding of data types with metadata, but limiting the scope of what is
revealed to a standardized interface. In REST, components comminicate by 
transferring a *representation* of a resource in a format matching *one of an
evolving set* of standard data types, *selected dynamically* based on the 
capabilities or desires of the client and the nature of the resource. Whether
the representation is in the same format as the raw source, or is derived from
the source, remains hidden behind the interface. The benefits of the mobile
object style are approximated by sending a *representation that consists of
instructions* in the standard data format of an encapsulated rendering engine
(e.g., Java). REST thus gains the separation of concerns of a client-server
style without the scalability problems on the server side, it allows information
hiding through a generic interface to enable encapsulation and evolution of
services, and it provides for a diverse set of functionality through 
downloadable feature-engines.

The REST data elements can be summarized as:

| Data Element            | Modern Web Examples                               |
| :-----------------------|:--------------------------------------------------|
| resource                | the intended conceptual target of a hypertext ref |
| resource identifier     | URL, URN                                          |
| representation          | HTML Document, JPEG image                         |
| representation metadata | media type, last-modified time                    |
| resource metadata       | source link, alternates, vary                     |
| control data            | if-modified-since, cache-control                  |

#### Resources ####
The key abstraction of information in REST is a *resource*. Any information that
*can be named* can be a resource. This could be a document, image, temporal
service (e.g., "reviews written today"), a collection of other resources, a
non-virtual object (e.g., a person) and so on. In simple terms, any concept
that might be the *target of an author's hypertext reference* must fit within
the definition of a resource. 

The only aspect of a resource that must be *static* is the *semantics of the 
mapping*, since semantics is what identifies the resource. For example, the 
"author's preferred version" of an academic paper is a mapping whose value
changes over time, whereas a mapping to "the paper published in the proceedings
of conference X" is static. These are two distinct resources, even if they
happen to map to the same value at some point in time.

This abstraction enables some key features of the Web:
 - generality by encompassing many sources of information without artificially
   distinguishing them by type or implementation
 - late binding to the reference of a representation, enabling conneg based on
   characteristics of the request
 - an author can reference the concept rather than some singular representation
   of that concept, removing the need to change all existing links whenever
   the representation changes

#### Resource Identifiers ####
REST uses resource identifiers to identify particular resources in interactions
between components. REST connectors provide a generic interface for accessing
and manipulating the value set of a resource. The naming authority that 
assigned the resource identifier is responsible for maintaining the semantic
validity of the mapping over time.

Traditional closed/local hypertext systems relied on unique node or document
identifiers that changed every time the information changed, thus requiring
link servers to maintain references separately from the content. Since 
centralized link servers are anathema to the immense scale and multi-
organizational domain requirements of the Web, REST relies instead on the 
author choosing a resource identifier that best fits the nature of the concept
being identified. The downside of this is that the quality of an identifier
is often dependent on the amount of money spent maintaining its validity.

#### Representations ####
Representations are used by components to capture the current or intended state
of resources. This representation is then transferred between components as 
part of actions. A representation is a sequence of bytes, plus representation
metadata to describe those bytes. Other common but less precise names for a
representation include document, file, HTTP message, instance or variant.

A representation consists of:
 - data
 - metadata (name:value pairs, names correspond to standards defining the 
             structure & semantics of the values)
 - (sometimes) metadata to describe the metadata

The metadata can be resource metadata or representation metadata.

Control data defines the purpose of a message between components, such as the
action being requested or the meaning of a response. It is also used to 
parameterize requests and override the default behaviour of some connecting
elements (such as caches). The control data helps define whether the 
representation may indicate the current state, desired state, or value of some
other resource.

The data format of a representation is known as a media type. The design of the
media type can impact the user-perceived performance of a distributed hypermedia
system. They key is to place the most important rendering information up front,
such that the initial information can be incrementally rendered while the rest
of the info is received.

### Connectors ###
Connectors provide an abstract interface for component communication, 
enhancing simplicity (through separation of concerns) and hiding the underlying
implementation of resources and communication mechanisms. 

| Connector | Modern Web Examples                |
| :---------|:-----------------------------------|
| client    | libwww, libwww-perl                |
| server    | libwww, Apache API, NSAPI          |
| cache     | browser cache, Akami cache network |
| resolver  | bind (DNS lookup library)          |
| tunnel    | SOCKS, SSL after HTTP CONNECT      |

All REST interactions are stateless. This restriction accomplishes 4 functions:
 - removes the need for any connectors to retain application state (scalability)
 - allows interactions to be processed in parallel without knowing semantics
 - allows intermediaries to view & understand requests in isolation
 - forces all information that might affect reusability of cached requests to
   be present in each request

The connector interface is similar to procedural invocation, but with important
differences in the passing of parameters & results. The in-parameters consist
of request control data, a resource identifier indicating the target of the 
request, and an optional representation. The out-parameters consist of response
control data, optional resource metadata and an optional representation.

From an abstract viewpoint the invocation is synchronous, however both the 
in-parameters and the out-parameters can be passed as data streams, so 
processing can be invoked before the value of the parameters is completely
known (thus avoiding latency for large transfers).

Server and Client are the primary connector types. The difference is that a 
client initiates communication with a request, and the server listens for 
connections and responds to requests. A component *may include both client and
server connectors*.

The third connector type, Cache, can be located on the interface to a client
or a server connector. The client uses it to avoid repetition of network comms,
and the server to avoid repeating the process of generating a response. Caches
are typically implemented within the address space of the connector that uses
them.

Some cache connectors are shared, so that cached responses may be used in
answer to a client other than the one for which the response was originally
cached. Shared caching can thus reduce the impact of 'flash crowds' on popular
servers. This can lead to errors if the cached response does not match what
would have been obtained by a new request. 

A cache is able to determine the cacheability of a response because the 
interface is generic rather than resource-specific. By default, responses to
retrieval requests are cacheable and all others are non-cacheable. If the 
request requires authentication then the response is only cacheable by a non
shared cache. Control data can be used to override these defaults. 

A resolver translates partial or complete resource identifiers into the network
address info needed to establish an inter-component connection. For example, 
most URI include a DNS hostname as the means for identifying the naming 
authority for a resource. A Web browser will extract the hostname from the URI
and make use of a DNS resolver to obtain the IP address for that authority.
Use of one or more intermediate resolvers can improve the longevity of resource
references through indirection, with the trade-off of added latency.

Finally, a tunnel is a simple relay of comms across a connection boundary, such
as a firewall or lower-level network gateway. The only reason it's modeled as
part of REST and not abstracted away is that some REST components may
dynamically switch from active component behaviour to that of a tunnel. The 
primary example is an HTTP proxy that switches to a tunnel in response to a 
CONNECT method request, thus allowing its client to directly communicate with
a remote server using a different protocol such as TLS that doesn't allow 
proxies. The tunnel then disappears when both ends terminate their connection.

### Components ###

| Component     | Modern Web Examples                  |
| :-------------|:-------------------------------------|
| origin server | Apache httpd, Microsoft IIS          |
| gateway       | Squid, CGI, Reverse Proxy            |
| proxy         | CERN Proxy, Netscape Proxy, Gauntlet |
| user agent    | Netscape Navigator, Lynx, MOMspider  |

A user agent uses a client connector to initiate a request and becomes the 
ultimate recipient of the response. The most common example is a Web browser.

An origin server uses a server connector to govern the namespace for a 
requested resource. It is the definitive source for representations of its
resources and must be the ultimate recipient of nany request that intends to
modify the value of its resources. Origin servers provide a generic interface
to their services as a resource hierarchy, with the resource implementation
details hidden behind the interface.

Proxies act as intermediaries selected by clients to provide interface
encapsulation of other services, data translation, performance enhancement or
security protection. Gateways (a.k.a reverse proxies) act as intermediaries
imposed by the network or origin server to provide interface encapsulation of
other services, for data translatino, performance enhancement or security
enforcement. 

## REST Architectural Views ##

### Process View ###
This follows the path of data as it flows through the system. Example (of 
three parellel requests):

![alt text](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_process_view.gif "Process View")

REST's client-server separation of concerns simplifies component implementation
, reduces the complexity of connector semantics, improves the effectiveness of 
performance tuning, and increases the scalability of pure server components. 

Layered system constraints allow intermediaries--proxies, gateways, and 
firewalls--to be introduced at various points in the communication without 
changing the interfaces between components, thus allowing them to assist in 
communication translation or improve performance via large-scale, shared 
caching. 

REST enables intermediate processing by constraining messages to be 
self-descriptive: interaction is stateless between requests, standard methods 
and media types are used to indicate semantics and exchange information, and 
responses explicitly indicate cacheability.

 - components are connected dynamically
 - similar to pipe-and-filter style
 - bidirectional streams, but each direction is independent (so can use stream
   transducers (filters))
 - generic connector interface allows components to be placed on the stream
   based on the properties of each request/response
 - stateless nature of REST allows interactions to be independent, *removing the
   need for an awareness of the overall component topology (impossible!)
 - also allowing components to act as either destinations or intermediaries,
   determined dynamically on a per-request basis
 - connectors only need be aware of each other's existence
 
### Connector View ###
This concentrates on the mechanics of comms between components. For REST, we're
particularly interesetd in the constraints that define the generic resource
interface.

Client connectors examine the resource identifier in order to select an 
appropriate comms mechanism for each request. For example, a client may be
configured to connect to a specific proxy component, perhaps acting as an 
annotation filter, when the identifier indicates that it is a local resource.

REST doesn't restrict comms to a particular protocol, but it does constrain the
interface between components & hence the scope of interaction & implementation
assumptions that might otherwise be made between components. 

For example, the Web's primary transfer protocol is HTTP, but the architecture 
also includes seamless access to resources that originate on pre-existing 
network servers, including FTP, Gopher, and WAIS. Interaction with those 
services is restricted to the semantics of a REST connector. This constraint 
sacrifices some of the advantages of other architectures, such as the stateful 
interaction of a relevance feedback protocol like WAIS, in order to retain the 
advantages of a single, generic interface for connector semantics. In return, 
the generic interface makes it possible to access a multitude of services 
through a single proxy. If an application needs the additional capabilities of 
another architecture, it can implement and invoke those capabilities as a 
separate system running in parallel, similar to how the Web architecture 
interfaces with "telnet" and "mailto" resources.

### Data View ###
This reveals the *application state* as information flows through the 
components. Since REST is specifically targeted at distributed information 
systems, it views an application as a cohesive structure of information and 
control alternatives through which a user can perform a desired task.

Component interactions occur in the form of dynamically sized messages. Small 
or medium-grain messages are used for control semantics, but the bulk of 
application work is accomplished via large-grain messages containing a 
complete resource representation. The most frequent form of request semantics 
is that of retrieving a representation of a resource (e.g., the "GET" method 
in HTTP), which can often be cached for later reuse.

REST concentrates all of the control state into the representations received 
in response to interactions. The goal is to improve server scalability by 
eliminating any need for the server to maintain an awareness of the client 
state beyond the current request. An application's state is therefore defined 
by its pending requests, the topology of connected components (some of which 
may be filtering buffered data), the active requests on those connectors, the 
data flow of representations in response to those requests, and the processing 
of those representations as they are received by the user agent.

An application reaches a steady-state whenever it has no outstanding requests; 
i.e., it has no pending requests and all of the responses to its current set 
of requests have been completely received or received to the point where they 
can be treated as a representation data stream.

The user-perceived performance of a browser application is determined by the 
latency between steady-states: the period of time between the selection of a 
hypermedia link on one web page and the point when usable information has been 
rendered for the next web page.

Since REST-based architectures communicate primarily through the transfer of 
representations of resources, latency can be impacted by both the design of 
the communication protocols and the design of the representation data formats. 
The ability to *incrementally render the response data* as it is received is 
determined by the design of the *media type* and the availability of *layout 
information* (visual dimensions of in-line objects) within each representation.

An interesting observation is that the most efficient network request is one 
that doesn't use the network. In other words, the ability to reuse a cached 
response results in a considerable improvement in application performance. 
Although *use of a cache adds some latency to each individual request* due to 
lookup overhead, the *average request latency is significantly reduced* when 
even a small percentage of requests result in usable cache hits.

The next control state of an application resides in the representation of the 
*first requested resource*, so obtaining that first representation is a 
priority. REST interaction is therefore improved by protocols that "respond 
first and think later." In other words, a protocol that requires multiple 
interactions per user action, in order to do things like negotiate feature 
capabilities prior to sending a content response, will be perceptively slower 
than a protocol that sends whatever is most likely to be optimal first and then
provides a *list of alternatives* for the client to retrieve if the first 
response is unsatisfactory.

The *application state* is controlled and stored by the *user agent* and can be 
composed of representations from multiple servers. In addition to freeing the 
server from the scalability problems of storing state, this allows the user to 
*directly manipulate the state* (e.g., a Web browser's history), *anticipate 
changes to that state* (e.g., link maps and prefetching of representations), 
and *jump from one application to another* (e.g., bookmarks and URI-entry 
dialogs).

The model application is therefore an engine that moves from one state to the 
next by examining and *choosing from among the alternative state transitions* 
in the current set of representations. Not surprisingly, this exactly matches 
the user interface of a hypermedia browser. However, the style does not assume 
that all applications are browsers. In fact, the application details are hidden
from the server by the *generic connector interface*, and thus a user agent 
could equally be an automated robot performing information retrieval for an 
indexing service, a personal agent looking for data that matches certain 
criteria, or a maintenance spider busy patrolling the information for broken 
references or modified content.

REST component interactions are structured in a layered client-server style, 
but the added constraints of the *generic resource interface* create the 
opportunity for *substitutability* and *inspection by intermediaries*.

Requests and responses have the appearance of a *remote invocation style*, but 
REST messages are targeted at a *conceptual resource* rather than an 
implementation identifier.
 
The interaction method of sending representations of resources to consuming 
components has some parallels with event-based integration (EBI) styles. The 
key difference is that EBI styles are *push-based*. In the REST style, 
consuming components usually pull representations. Although this is less 
efficient when viewed as a single client wishing to monitor a single resource, 
the scale of the Web makes an unregulated push model infeasible.

The principled use of the REST style in the Web, with its clear notion of 
components, connectors, and representations, relates closely to the C2 
architectural style. The C2 style supports the development of distributed, 
dynamic applications by focusing on *structured use of connectors* to obtain 
*substrate independence*. C2 applications rely on asynchronous notification of 
state changes and request messages. As with other event-based schemes, C2 is 
nominally *push-based*, though a C2 architecture could operate in REST's pull 
style by *only emitting a notification* upon receipt of a request. However, the 
C2 style *lacks the intermediary-friendly constraints* of REST, such as the 
generic resource interface, guaranteed stateless interactions, and intrinsic 
support for caching.

REST provides a set of architectural constraints that, when applied as a whole,
emphasizes scalability of component interactions, generality of interfaces, 
independent deployment of components, and intermediary components to reduce 
interaction latency, enforce security, and encapsulate legacy systems.


## Experience & Evolution ##
The name "Representational State Transfer" is intended to evoke an image of how
a well-designed Web application behaves: a network of web pages (a virtual 
state-machine), where the user progresses through the application by selecting
links (state transitions), resulting in the next page (representing the next 
state of the application) being transferred to the user and rendered for their
use.

### REST Applied to URI ###
Uniform Resource Identifiers (URI) are both the simplest element of the Web 
architecture and the most important. 

URI = URL + URN

The early Web architecture defined URI as *document* identifiers. This was
unsatisfactory because it implied that the author is identifying the content
rather than a representation of it, therefore implying that URI should change
with the content, and because not all addresses correspond to documents. 

REST defines a resource to be the semantics of what the author intends to
identify, rather than the value corresponding to those semantics at the time
the reference is created. It is then left to the author to ensure that the
identifier does indeed identify the intended semantics.

So, how does a user access, manipulate, or transfer a concept such that they 
can get something useful when a hypertext link is selected? REST answers that 
question by defining the things that are manipulated to be representations of 
the identified resource, rather than the resource itself. An origin server 
maintains a mapping from resource identifiers to the set of representations 
corresponding to each resource. A resource is therefore manipulated by 
transferring representations through the generic interface defined by the 
resource identifier.
