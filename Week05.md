## 1. Measuring and Governing Architecture Characteristics.
It use for ensuring that the software architecture following the desired quality attributes using measurable metrics and governance mechanisms.
### Types of Measures:
1. **Operational Measures**: Used to track runtime qualities like (**Performance**, **Availability**(Up time service), **Scalability**). **Example** Web server need to measuring the response time stays below 200ms under 1000 concurrent users.
2. **Structural Measures**: Focuses on modularity and coupling (check dependence between software modules). **Cyclomatic Complexity (CC)**: Measures code complexity; CC < 10 is considered maintainable. **Example**: A function with 5 if statements and 2 loops may have a high CC and be harder to maintain.
3. **Process Measures**: Concerned with agility like **Testability** (code coverage), **Deployability** (success rate & duration of deployments), **Maintainability** (time to make and test changes). **Agility = Testability + Deployability + Maintainability**
### Governance - Fitness Functions:
- **Definition**: Automated checks to validate architecture characteristics.
- **Types**:
	- **Atomic**: Focused on one characteristic.
	- **Holistic**: Evaluate multiple characteristics together.
**Examples**:
- **JDepend**: Detect component dependency cycles (modularity).
- **ArchUnit**: Validate layered architecture.
- **Netflix's Chaos Monkey**: Tests resilience by randomly shutting down services.
## 2. Scope of Architecture Characteristics
### Two Levels of Architecture Characteristics:
**1. System-Level**:
Affects the entire architecture:
- Examples: Availability, Security, Performance, Scalability, Usability.
**2. Component-Level**:
Applies to individual services or modules.:
- Sam  attributes, but scoped smaller.
### Architecture Quantum
A unit of architecture that is independently deployable, with:
- High Cohesion
- Synchronous Connascence (tight internal dependencies)
### Example
**Quantum of One:**
- A tightly coupled monolith or UI + service bundle.
- One unit = one quantum
**Multiple Quanta:**
- Microservices, each  with its own UI and logic
## 3. Abstract Factory & Memento Patterns
### SOLID & OOP Principles Recap:
- **Single Responsibility**, **Open/Closed**, **Liskov**, **Interface Segregation**, **Dependency Inversion**
- **Encapsulate what varies**, **Program to interfaces**, **Favor composition**
---
### Abstract Factory Pattern
**Problem**: Too many dependencies on concrete classes.
**Solution**:
Create **families of related objects** without specifying exact classes.
**Use Case Example:**
PizzaStore (New York & Chicago)
```c#
PizzaStore nyStore = new NYPizzaStore()l
Pizza pizza = nyStore.orderPizza("cheese");
```
- It use PizzaIngredientFactory interface
- Different ingredients per = region (Mozzarella vs. Reggiano)
**Benefit:** Flexible, scalable code that follows **Dependency Inversion Principle**
---
### Memento Pattern
**Problem:** Need to save and restore object state (e.g., undo in a text editor).
**Solution:**
Use three roles:
- **Originator:** Creates state snapshot
- **Caretaker:** Manages history
- **Memento:** Stores snapshot
**Example:**
```java
editor.setContent("Software");
history.save(editor.createState());

editor.setContent("Design");
history.save(editor.createState());

history.revert(editor);
```
**Benifit:** Encapsulation preserved. Originator onl  knows how to restore its own state.


