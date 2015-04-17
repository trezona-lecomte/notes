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
