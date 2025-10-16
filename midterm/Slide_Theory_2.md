# SDA Modularity
เราต้องการที่จะแบ่งระบบออกเป็นชิ้นย่อยๆ ที่ไม่ส่งผลต่อกันเพื่อให้ระบบดูแลง่าย (Maintainability)
- เพิ่ม, แก้ไข, อัปเดต ระบบได้โดยไม่กระทบส่วนอื่น
แบ่งไปเป็น
- Module - ส่วนย่อยของระบบ ที่สามารถนำมาประกอบได้ไหม
- Modularity - **ระดับ**ที่ module **สามารถแยกหรือรวมกลับ** ได้ยืดหยุ่นมาแค่ไหน (breaking system into smaller pieces)
## Modularity vs. Granularity
- **Modularity** - แบ่งระบบเป็นส่วนๆ
- **Granularity** - determines the optimal size of modules or services (ขนาดที่ควร)
### สิ่งที่เอาไว้ตัดสิน Granularity (ขนาดของ module)
- Single Responsibility Principle (SRP) - แต่ละ module มีหน้าที่เดียว
- Cohesion (สอดคล้องภายใน) - รวมสิ่งที่เกี่ยวข้องไว้ด้วยกัน 
- Future Growth Potential - คิดถึง future อย่าแยกจนมันซับซ้อน
- Dependency Analysis  - ลด dependency ระหว่าง module.
- Communication Overhead - ถ้าเป็นแบบกระจาย (Distributed or Microservices) ต้องไม่ให้มันติดต่อ (call method หรือดึงข้อมูล) บ่อยเกินไป
## Modularity Measuring.
3 Key concept that make the architecture understandable.
![[Pasted image 20250822164425.png]]
### **Cohesion**: (สอดคล้องใน module)
high = good mean module ทำงานชัดเจนเรื่องเดียว
if we split the high cohesion module it will cause a high coupling and make the code harder to read.
#### Type of Cohesion
1. **Functional cohesion** → ทุกส่วนจำเป็นต่อฟังก์ชันเดียวกัน
2. **Sequential cohesion** → ผลลัพธ์ของส่วนหนึ่งถูกใช้เป็นอินพุตของอีกส่วน 
3. **Communicational cohesion** → ส่วนต่าง ๆ ใช้ข้อมูลชุดเดียวกัน
4. **Procedural cohesion** → ส่วนต่าง ๆ รันเรียงลำดับเสมอ
5. **Temporal cohesion** → ส่วนต่าง ๆ ทำงานในเวลาเดียวกัน (เช่น ขั้นตอนเริ่มต้นระบบ)
6. **Logical cohesion** → รวมกันเพราะ “ดูคล้ายกัน” (เช่น ฟังก์ชัน I/O)
7. **Coincidental cohesion** → รวมกันโดยบังเอิญ ไม่เกี่ยวข้องกันเลย (แย่ที่สุด)
#### Example 
โมดูล “Customer Maintenance” มี
- add customer
- update customer
- get customer
- notify customer
- get customer orders
- cancel customer orders

สถาปนิกต้องตัดสินใจว่า **สองฟังก์ชันสุดท้าย** (เกี่ยวกับ order) ควรอยู่ที่นี่หรือแยกเป็น “Order Maintenance” โมดูลแยก?

- ถ้ามีแค่นี้ อาจรวมไว้ด้วยกันก็ได้
    
- ถ้าโมดูล Customer โตขึ้น → อาจแยกดีกว่า
    
- ถ้า Order ขึ้นกับ Customer มาก → การแยกอาจทำให้ _coupling สูงขึ้น_
### **Coupling**: (สอดคล้องกันระหว่าง Module (Dependency))
ยิ่งต่ำยิ่งดี module ไม่สอดคล้องกัน
#### **Coupling Type**
- Afferent coupling (Ca) - incoming (module โดนเรียก) 
- Efferent coupling (Ce) - outgoing (เรียก module อื่น)
#### ตัวชี้วัดจาก Coupling
- **Abstractness (A)** =  สัดส่วนของ class / interface แบบ abstract  (A = 0 ไม่มี abstract A = 1 มีแต่ Abstract)
- **Instability (I)** = (Ce / (Ca + Ce) ) -> ยื่งมากยิ่งไม่สเถียร เอาไว้ check module ใน software ว่าต้องพึ่งคนอื่นมากน้อยแค่ไหน และมีแนวโน้มจะเปลี่ยนบ่อยเพราะอะไร (I = 0 very stable (not depend on other), I = 1 not stable (rely on other))
- **Distance from Main Sequence (D)** = |A + I - 1| วัดความห่างจากโครงสร้างอุดมคติแค่ไหน
	The module with high abstractness and high instability (with no dependents) are in the zone of uselessness. (abstract สูงแต่ไม่มีใครใช้)
	The module with low abstractness and low instability are in the zone of pain. (concrete สูงและเสถียรสูง -> เปลี่ยนยากมาก)
### Connascence (การพึ่งพาที่ลึกว่า coupling)
Connascence เมื่อ module เปลี่ยนอีก module ต้องเปลี่ยนตาม เพื่อทำให้ระบบยังทำงานถูกต้อง
**Static connascence** (ระดับ code)
- CoN (Name) -> ใช้ชื่อเดียวกัน
- CoT (Type) -> ใช้ข้อมูลชนิดเดียวกัน
- CoM/CoC (Meaning/Convention) -> ต้องตีความค่าข้อมูลเหมือนกัน
- CoP (Position) -> เรียงลำดับ parameter ตรงกัน
- CoA (Algorithm) ->ใช้วิธีคำนวณเดียวกัน
**Dynamic connascence** (ระดับ runtime)
- **CoE (Execution)** → ต้องรันเรียงลำดับที่แน่นอน
    
- **CoT (Timing)** → ต้องรันในเวลาเหมาะสม
    
- **CoV (Values)** → ค่าหลายค่าต้องเปลี่ยนพร้อมกัน
    
- **CoI (Identity)** → ต้องอ้างอิง object เดียวกัน
    
**คุณสมบัติสำคัญ:**
- **Strength** → ยิ่ง coupling แข็ง ยิ่ง refactor ยาก
- **Locality** → ถ้าอยู่ในโมดูลเดียวกันไม่เป็นไร แต่ถ้าอยู่คนละโมดูลควรลดลง
- **Degree** → ถ้าองค์ประกอบเยอะที่ต้องเปลี่ยนพร้อมกัน → ปัญหาใหญ่

**แนวทางปรับปรุง:**
- ลด connascence ข้าม boundary (โมดูล)
- เพิ่ม connascence ภายใน boundary (โมดูลเดียวกัน)
- **Rule of Degree:** แปลง coupling ที่แข็ง → coupling ที่อ่อน
- **Rule of Locality:** ยิ่งห่างไกล → ควรใช้ coupling ที่อ่อนลง