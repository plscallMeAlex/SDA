# Identifying Architecture Characteristics
## Architecture characteristics
It consist of the word that end with -ity. So it have quite a lot of words but we don't know which one need for the system ?
## 1. Three Source of arch characteristics.
- Domain Requirements.
- Implicit domain knowledge.
- Domain Concerns.
### Domain Requirement (Explicitly stated)
It explicit "must-have" and coming from stakeholder (ผู้มีส่วนได้ส่วนเสีย).
**Example**
Like in the banking system have a requirement

>"Transaction must complete within 2 minute "

The arch char is the performance.
**Can pulling it from the statement**

### Implicit Domain Knowledge (Unstated but expected)
It assumed/expected to have these qualities. It not written down but everyone agree with that (comes from assumption).
**Example**
Healthcare Patient Records like the patient data must  be recorded but it need to secure and confidential (security, confidentiality)
Implicit Expectation: Doctors/nurses need records updated in real time.
Architecture Characteristic: **Consistency / Integrity**.

### Domain Concerns (Broader ecosystem issues)
It used to indicate for the long term process and effect the system that will be designed and operated. Make understand in the broader context (scaling, maintain, ecosystem, long-term use)
มองมุมกว้างว่าระบบต้องการอะไรบ้างในระยะยาวถ้าเกิดเหตุการ์ณนี้จะเป็นอะไรบ้าง
**Example**
Ecommerce Platform
- Concern: Sales spike during **Black Friday**.
- Architecture Characteristic: **Scalability / Elasticity**
- Concern: Continuous addition of new features (discounts, loyalty, new payment methods).
- Architecture Characteristic: **Modifiability / Maintainability**
- Concern: Global customers across time zones.
- Architecture Characteristic: **Availability / Fault Tolerance**
### Domain Stakeholder
- User satisfaction
- Time to market
- Mergers and acquisitions
- Competitive advantage
- Time and Budget

## 2. Translating from domain concerns into architecture characteristics
![[Pasted image 20250819211031.png]]
## 3. Composite Architectural Characteristics
It is the bundle of qualities tied to business goals. So the architecture task is to break them down to the measurable, specific characteristics from the stakeholder business describing. 
**Example**
"We need agility / fast time-to-market"
- Broke down to **Maintainability** (how long to apply changed), **Testability** (how long of the test), **Deployability** (How long before deployed).
### Why decompose
We need to decompose or translate the composite arch char to make it measurable and then it can design and test for it.

## 4. Prioritize the architecture characteristics
The characteristics are not equally important but the **important depends on the business context**.
**Example**
For the banking the security and reliability comes first before the performance.

## 5. Document Architecture Characteristics
We need to write down the explicitly so the whole will understands helps it won't assume  the design and their characteristics.

## 6. Final List of Characteristics
Keep the list (list of char) short and focused on the business context (don't overengineering).
We need to **ask the stakeholder what is the most important thing characteristics**.
- It forces to discuss the important (meeting).
- Helps architecture analyze the trade-offs.

## Design vs. Architecture and Trade-offs
Architecture  must evaluate trade-offs: performance, coupling, cost, and which solution better supports the chosen characteristics.
The design is resides of architecture