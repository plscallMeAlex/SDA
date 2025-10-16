It want to solve the microservice 
It want to change from http sync to async .
# Topology
**Broker topology** is like broadcast to everyone and handle some of the service will handle event signal.
Disadvantage is can't control the workflow don't know what will happened first.

**Mediator topology** is use to control the workflow to send the signal.
# Database Topology
Can be one DB or multiple DB.
Like if have multiple DB it might need data from other to access.
If having a one DB if change it might not freely.
# Cloud Consider
Better to cloud
# Risk
Don't know event processing, it too much static coupling. Workflow
# Governance 
Check the coupling and dynamic coupling through synchronous calls.