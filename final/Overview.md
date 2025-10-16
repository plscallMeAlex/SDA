# Monolith Architecture
## Layered Architecture
Consist of 4 layered to separate by a role
- Presentation Layer like a UI
- Business Layer like the logic is here
- Persistence Layer is the base
It using a layered isolation that protected the each layer communicate
The problem is if something broke down then it will down
## Pipe
It use to connect every function it like a connect flow.
## Modular
To make the service faster but the problem is when some function down then it need to fix all
## Microkernel
Doing like a plugin that attach to the core every one develop their own feature then attach but the problem is like everything.
# Distributed Architecture
## SOA
It will create the central to manage the service but it will occur problem that if we develop a new feature then it must followed the rules of central ;
## Microservice
It will separate resource like db so it isolated the space but it will problem about communicated 
## Event Driven
It the service try to broadcast (in central area) to every service that it have this event occur then another service will handle.
## Space Base
Is like copy the data in DB to itself to handle a multiple request then it will save to the DB later (caching). 