Monilithic deploy it together
Closed layer cannot program to  another layer (program layer by layer can't break through)

Isolation concept if make change in anything it won't impact to the lower layer.

Closed layers good for isolation.

Sinkhole if all closed (have a bit) have to go through multiple layered and layered do nothing.

Data Topologies - Single monolithic DB if want implement on cloud each partition can deployed on separate place but it will have latency between communicate.

excellent for governance can write the fitness function to control. 


Singleton is creational
comes from have a class definition and want to create that type on the system otherwise it behave something bad. It ensure the class have 1 instant only 

# Microkernal
IT separate the logic to core part and plugin component.
For the core part is **definition** is minimal function to run the system and happy path a general processing flow. Main logic is in the core.

Example is like recycling application.

Plugin Component is going to be independent component. don't talk to each other plugin component. It talk to core only. (No dependency between plugin)

Point to point **plugin is package name** (namespaces).
It a monolithic because it need to go through the core.

Remote plugin
- Scalability
- Better Decoupling
Not Easy to impl.

To make the core know how many plugin.
Then need to registry (plugin registry) the module 

Contract
Standard contracts: 
Custom contracts: need adapter for (in cast using external plugin)

Microservice Database.
Core system have it own database
Plugin component could have a embedded database (in-memory) don't need a storage. It need a memento to help on in memory.

Iterator & Composite Pattern
Iterator - have a object that implement different kind of data structure but we want to interface that into the same way.

Design Principle
Class should have only one reason to change.

Composite structural patterns.
When dealing with tree-structured data like GUI, we want to handle node in the same way.