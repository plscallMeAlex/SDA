# Software Design and Architecture ?
โครงสร้างระดับสูงของซอฟต์แวร์ ถูกแบ่งกันยังไง ทำงานร่วมกันยังไง เป็นสิ่งที่เราตัดสินใจและจะส่งผลในระยะยาวของทั้งระบบ
## Architecture Components
1. Architecture Style - Monolithic (Pipeline, Microkernel), Distributed (Microservices, Event-driven)
2. Architecture Characteristics - -ilities like scalability, performance, security.
3. Logical Components - Module creating the workflow of the system ![[Pasted image 20250822153644.png]]
4. Architecture Decisions - Rule or reason that use for create architecture. (Doesn't allow to directly access database)

## Different Architecture and Design
![[Pasted image 20250822154241.png]]
Architecture is effect for the long term purpose.
Design is effect less in short term.

## Architectural Thinking
- Need to know the differ between architecture and design can work with developer.
- เป็นเป็ด (รู้เยอะมากกว่าลึก)
- มองทุกอย่างมีสิ่งแลกเปลี่ยนเสมอ (trade-off ) no correct 100%
- Know the business change (like increase the specific characteristics = performance, availability (พร้อม))
### Architecture Law's
- Everything is trade-off.
- Why important than How.
- การตัดสินใจมีหลายระดับ
 
## Expectation of Architecture
- Architecture decision - don't strict to something (like "use reactive framework" didn't specific to React.js)
- Analyze and ปรับปรุงโครงสร้างเสมอ
- Follow the new trend
- ensure ว่าปฎิบัติตามที่กำหนดตาม architecture decision
- Know business domain
- Leadership and collaborating.
- Understand the organization.

# Refactoring ?
ปรับปรุงสิ่งที่อยู่ภายใน แต่ภายนอกยังทำเหมือนเดิม
Make the code cleaner and maintainable.
- ทำเป็นชิ้นเล็กๆ จะได้ทดสอบได้ตลอดเวลาและแก้ไขได้ทันที

## Signal that code should Refactor ("Bad Smells")
- Code dupe
- Long Method or Huge class (hard to understand)
- Feature envy (depend on another class มากไป)
- Shotgun surgery (แก้หนึ่งอย่างกระทบกับอีกหลายอย่าง)
- Switch Statement (Polymorphism แทน)
- Primitive obsession / data clumps (data design not good)
- Lazy Class, middle man (คลาสที่ไม่ได้ทำอะไร หรือ แค่ส่งต่ออย่างเดียว)

## Refactoring Technique Mostly Found
- Extract Method (extract to clearly name group)
- Move Method (move the method to another class that suitable)
- Replace Conditional With Polymorphism (Using sub class instead of if/switch )
- Introduce NULL object (create a null object to prevent null checking)
- Encapsulate Collection (prevent to directly editing the collection)
- Introduce Parameter Object (combine multiple parameter to one object)
- Replace Nested Conditional With Guard Clauses (ออกจาก condition ซ้อนก่อน)
