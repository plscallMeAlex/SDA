# Scope of Architectural Characteristics
## Architecture Characteristics
Can used in any scope or applied to the different scopes like **system-level** (applied the entire system) and **component-level** (applied to the individual component or service).
So many characteristics can applied both of them (It like we grouping the characteristics base on the scope that we like). 
## Architecture Quantum Concept
An architecture quantum = **smallest deployable unit**
Use to help architects decide the scope of architecture characteristics whether they should **apply to the whole system or just to a specific quantum** (subsystem).
- **Independently deployable** (can release or deploy separately from another part) 
- High functional cohesion (does one purposeful job)
- Synchronous connascence (if parts change, other must too, and they communicate synchronously)
**Example**
- **Quantum of One:** A monolith (everything deploy together).
- **Multiple Quanta:** Microservice (separate service) we can deploy separate services.
- **Service + UI Quantum:** each service + UI can be deployed as its quantum.
- **Shared Database Quantum:** If 2 services or more use the same database it will be force grouped  to the same quantum (can't deploy separate)
### Quatum ?
We use quantum (**subsystem**) to determine smallest scope that can deploy and work freely.

## Case Study: Going, Going, Gone
Is the case study that will give the requirement and their background with additional context so we can create the quantum that contain the characteristics (each quantum might have the same).