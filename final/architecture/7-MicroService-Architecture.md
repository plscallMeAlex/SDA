# Topology
Each service have it own resource it **can work without** need other service.
concept it want to reduce the coupling. So it **prefer the duplicate than coupling**.
It deeply domain partitioning.
![](images/Pasted%20image%2020251013160458.png)
So we can deploy separately to another service because it the same. It called **sidecar**
![](images/Pasted%20image%2020251013160715.png)
# Communication
It can use any protocol can be async or sync can separate another service to called another service.
![](images/Pasted%20image%2020251013160922.png)
# Data Topology
We can separate the database to each service to prevent the data change and effect the service.
# Cloud Topology
- VM
- Container
- Databases
# Risks
Service is too small
Too much communication make it high communication.
# Governance
Handle the coupling like combine the service and re separate.