# Topology
It separate like modular monolith. Each service separately and using a monolithic database.
It may deploy separate UI layer.

It may have a gateway api
![](images/Pasted%20image%2020251013154222.png)
The problem is when you change the schema we need to make sure that it won't effect the other service.
# Cloud Consider
It better cause it can freely deploy separately.
# Risks
Service that separate is too much communicate between service fix by combine.
Too much domain may cause domain.
Coupling between database
# Governance
Make sure that when change it won't effect other.
Amount of communication between domain services.
