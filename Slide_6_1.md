# SDA Component
## Component-Based Thinking
We can think the software as a component that each of it have it own role.
- component => one of the system that have a clear its responsibility and the boundary can test dev and improve standalone.
## Logical & Physical Architecture.
### Logical Components
- using function
- categorize or order by the namespace or directory of the source code.
- show what system does.
### Physical Architecture
- what will deploy like UI, database, services
- show how system does.
### Example
- **Logical** - "Order Placement Component"
- **Physical** - Microservice on AWS Lambda + use Postgres database.

## Creating Logical Architecture
It an iterative process that will do while identifying and restructuring (ปรับโครงสร้า ) the logical architecture.
1. **Identifying Core Component** - Think of the work of the user as a journey then create a component around that activity.
   ![[Pasted image 20250821024932.png]]
2. **Assigning User Stories to Components** - For each user story or requirement must in some component we may need to create, separate and combine a new component. 
	**Example**
	- User story: _“Email customer after order placed.”_
	- ควรอยู่ใน **Customer Notification component** ไม่ใช่ Order Placement
3. **Analyzing Roles and Responsibilities** - Don't make a god component ! Each must have their own task.
	**Example**
	- ก่อน refactor: 
		Order Placement ทำ validate order, แสดง cart, เก็บ payment, ปรับ stock, ส่ง email → หนักเกินไป
	- หลัง refactor:
		- Order Placement: validate, show cart, keep data
		- Payment Processing: payment
		- Inventory Management: stock adjustment.
		- Customer Notification: email sending.
4. **Analyzing Architectural Characteristics** - If make a small component it easy to maintain, scaling,  agile.
	**Example**
	- Component A for User must capable with 500 concurrent user.
	- Component B for Admin have a few people 
	- We need to design not the same.
5. **Restructuring Components** - Refactor component if we found the edge case !
## Component Coupling
Coupling is used to check the dependency between component .
If high coupling the code is hard to refactor hard on testing.
- **Static Coupling:** component communicate direct synchronous (Afferent coupling (คนอื่นพึ่งเรากี่ตัว), Efferent coupling (เราพึ่งคนอื่นกี่ตัว).
- **Temporal Coupling:** component need to work in order.
- **Law of Demeter:** Principle of Least Knowledge will make the system loose coupling
## Architecture Role.
- Architecture need to define / refine / manage component
- need to understand the partition architecture correctly.
## Architecture Partitioning
Two main partitioning.
- **Domain Partitioning** - used to distributed the component based on business domain or workflow.
	**Advantage is** it inline wit  the business align with cross-functional teams, migrate easy to go with microservice.
	**Disadvantage** - code customization might distributed in many placed
	like Catalog, as top-level components
- **Technical Partitioning** - it distributed the component follow by the technical layer like the UI, Service, Database
	**Advantage is** it clarify everything separate technique.
	**Disadvantage** - high coupling, duplicated data, align with hard business.
## Conway's Law
	> Organization want to design the structur like the communication in that organization
- If team be like "UI Team / Backend Team" -> technical partitioned system.
- If team "Checkout team / Catalog team" -> domain partitioned system
- **Inverse Conway Maneuver:** use to change the team architecture as the aspected.
## Example
1. Good Component design =>
	- Customer Notification: sending email only
	- Payment Processing: payment only
2. Loose coupling =>
	- Communicate via interface not related to internal side.
3. Domain Partitioning => 
	- Catalog, Checkout, Orders rely on the business workflow.
4. Technical Partitioning =>
	- Frontend, API, Database distributed to technology stack.
