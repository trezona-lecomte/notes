## DETOUR: Fielding's dissertation ##
The WWW succeeded in large part due to it's architecture - it was designed to scale. It was developed iteratively, using the principles of REST. "REST emphasizes scalability of component interactions, generality of interfaces,
independent deployment of components, and intermediary components to reduce
interaction latency, enforce security, and encapsulate legacy systems" [xvii]

 - Why do component interactions need to scale, and what are the challenges in doing so?
 - Why should interfaces be general, what are the challenges in making them so, and what does a general interface look like?
     + HTTP and URIs are the two specifications that define the generic interface used by all component interactions on the Web.
 - Why should components be deployed independently?
 - How do intermediary components reduce interaction latency, enforce security and encapsulate legacy systems?

*Complexity* has driven the componentization of systems.

 - How did componentization solve the complexity problem?

*Context* - 'form follows function'

*Conflicting frontiers* - software and networking. "Software research has long been concerned with the categorization of software designs and the development of design methodologies, but has rarely been able to objectively evaluate the impact of various design choices on system behavior. Networking research, in contrast, is focused on the details of generic communication behavior between systems and improving the performance of particular communication techniques, often ignoring the fact that changing the interaction style of an application can have more impact on performance than the communication protocols used for that interaction."

One of the key challenges of web architecture is interconnecting info systems across organizational boundaries. Web architecture must be considered in the context of sharing *large-grain data* objects across *high-latency* networks and multiple *trust boundaries*. 

## Definitions of Software Architecture ##

### Run-time Abstraction ###
"A software architecture is an *abstraction of the run-time elements* of a
software system during some phase of its operation. A system may be composed of many *levels of abstraction* and many phases of operation, each with its own software architecture." [5]

Why do we abstract (hide detail)? In order to better identify and sustain it's properties. Each level of abstraction has *it's own architecture*. 

"An architecture represents an abstraction of system behavior at level, such that architectural elements are delineated by the abstract interfaces they provide to other elements at that level" [5]
L. Bass, P. Clements, and R. Kazman. Software Architecture in Practice. Addison
Wesley, Reading, Mass., 1998

"Within each element may be found another architecture, defining the system of sub-elements that implement the behaviour represented by the abstract interface. This recusion of architectures continues down to the most basic system elements: those that cannot be decomposed into less abstract elements." [6]

Shaw and Clements [122]:
“A component is a unit of software that performs some function at run-time. Examples include programs, objects,  processes, and filters.”

### Elements ###
A software architecture is defined by a configuration of architectural elements — components, connectors, and data — constrained in their relationships in order to achieve a desired set of architectural properties.






















