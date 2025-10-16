## **Slide 1 – หัวข้อเอกสาร**

**Software Design and Architecture – Architecture Characteristics Defined**

- เป็นการเกริ่นนำว่าเอกสารนี้อธิบาย **คุณลักษณะทางสถาปัตยกรรม (Architectural Characteristics)** ซึ่งเป็นปัจจัยที่ใช้กำหนดทิศทางการออกแบบซอฟต์แวร์
    

---

## **Slide 2 – Scalability และ Elasticity**

- **Scalability (การปรับขยาย)**
    
    - ความสามารถของระบบในการ _รักษาการตอบสนองได้ดี_ เมื่อจำนวนผู้ใช้เพิ่มขึ้นอย่างต่อเนื่อง (โหลดเพิ่มแบบค่อยเป็นค่อยไป)
        
    - ระบบต้องรองรับผู้ใช้จำนวนมากพร้อมกันโดย _ประสิทธิภาพไม่ตก_
        
- **Elasticity (ความยืดหยุ่นปรับโหลด)**
    
    - ความสามารถของระบบในการ _ตอบสนองทันที_ เมื่อมีโหลดเพิ่มขึ้นอย่างฉับพลัน
        
    - ตัวอย่าง: ช่วงพักเที่ยงมีผู้ใช้เพิ่มขึ้นหลายพันคน ระบบต้องขยายทรัพยากรได้เร็ว
        

---

## **Slide 3 – ผลกระทบของ Scalability และ Elasticity ต่อ Modularity**

- การออกแบบระบบให้ **ขยายได้ (Scalability)** และ **ปรับโหลดได้ (Elasticity)**
    
    - มักต้องออกแบบให้ **โมดูลแยกจากกัน (Modularity)** เพื่อเพิ่มความคล่องตัวในการปรับเปลี่ยนหรือเพิ่มทรัพยากรเฉพาะจุด
        
    - ถ้าโมดูลมีการเชื่อมโยงกันแน่น (coupling สูง) จะทำให้ปรับขยายได้ยาก
        

---

## **Slide 4 – Architectural Characteristics**

- **รายการคุณลักษณะสำคัญ**:
    
    - Scalability
        
    - Elasticity
        
    - Modularity
        
    - อื่น ๆ (“...ilities”) เช่น availability, reliability, security
        
- **แนวคิดหลัก:**
    
    - _Functional requirements_ → กำหนดว่า “ระบบต้องทำอะไร”
        
    - _Architectural characteristics_ → กำหนดว่า “จะทำอย่างไรให้สำเร็จ” และ “ทำไมต้องออกแบบแบบนั้น”
        

---

## **Slide 5 – Characteristics เป็น Non-domain Design Considerations**

- คุณลักษณะเหล่านี้ **ไม่ได้ขึ้นกับธุรกิจหรือโดเมนโดยตรง** แต่เป็นเรื่องของคุณภาพการออกแบบซอฟต์แวร์
    
- เช่น _performance, security, maintainability_ ที่ต้องพิจารณาในทุกระบบ ไม่ว่าจะเป็นธุรกิจใด
    

---

## **Slide 6 – ตัวอย่าง Elasticity**

- ข้อความ:
    
    > “We must support thousands of users during lunch period!”
    
- หมายความว่า **ระบบต้องรองรับโหลดพุ่งสูงทันที** → เป็นตัวอย่างชัดเจนของ _Elasticity_
    
- แสดงให้เห็นว่า _Architectural Characteristics_ แปลความต้องการเชิงธุรกิจออกมาเป็นปัจจัยเชิงเทคนิค
    

---

## **Slide 7 – Limit Characteristics to Prevent Overengineering**

- **อย่ารองรับคุณลักษณะมากเกินไป** (Overengineering)
    
    - รองรับหลายคุณลักษณะพร้อมกัน → ออกแบบซับซ้อน → ไม่มีประโยชน์ชัดเจน
        
    - สถาปนิกต้องรู้ว่า **คุณลักษณะใด “Critical” ต่อความสำเร็จของระบบ** เพื่อใช้เป็น “ตัวกรอง”
        
- ตัวอย่าง: เพิ่ม _Security_ มาก → อาจทำให้ _Performance_ แย่ลงเพราะต้องเข้ารหัสมากขึ้น
    

---

## **Slide 8–9 – Explicit และ Implicit Capabilities**

- **Explicit Architectural Characteristics** – เขียนระบุชัดในเอกสาร requirement
    
    - เช่น “ระบบต้องรองรับผู้ใช้หลายพันคนในช่วงพักกลางวัน” → _Elasticity_
        
- **Implicit Architectural Characteristics** – ไม่ได้เขียนชัด แต่ต้องมี
    
    - เช่น availability, reliability, security ที่มักไม่ได้ระบุแต่ระบบใด ๆ ก็ต้องการ
        
- แนวทางสำหรับสถาปนิก → **ต้องพิจารณาทั้ง explicit และ implicit** เพื่อให้ระบบสำเร็จจริง
    

---

## **Slide 10 – Some Architecture Characteristics**

- กล่าวถึงว่ามีคุณลักษณะอีกมากมาย ไม่ได้จำกัดแค่ 2-3 ตัว
    
- นำไปสู่การจัดหมวดหมู่ในสไลด์ถัดไป
    

---

## **Slide 11 – Categories of Architecture Characteristics**

คุณลักษณะทางสถาปัตยกรรมแบ่งออกได้เป็น 4 หมวด:

1. **Operational Characteristics** – เกี่ยวกับการทำงานและความเสถียรของระบบ
    
2. **Structural Characteristics** – เกี่ยวกับโครงสร้างและการปรับเปลี่ยนระบบ
    
3. **Cloud Characteristics** – เกี่ยวกับคุณสมบัติของระบบบนคลาวด์
    
4. **Cross-Cutting Characteristics** – คุณลักษณะที่ครอบคลุมทั้งระบบ ไม่ขึ้นกับโดเมน
    

---

## **Slide 12 – Operational Architecture Characteristics**

- **Availability** – ระบบต้องพร้อมใช้งานมากแค่ไหน (เช่น 24/7)
    
- **Continuity** – ความสามารถในการกู้คืนเมื่อเกิดภัยพิบัติ
    
- **Performance** – ประสิทธิภาพและความเร็วของระบบ (วัดด้วย stress test, peak analysis ฯลฯ)
    
- **Recoverability** – ความเร็วในการฟื้นฟูระบบให้กลับมาใช้งานได้ (รวมกลยุทธ์สำรองข้อมูล)
    

---

## **Slide 13 – Structural Architecture Characteristics**

- **Maintainability** – ความง่ายในการแก้ไขหรือเพิ่มฟังก์ชัน
    
- **Portability** – ความสามารถในการทำงานบนหลายแพลตฟอร์ม
    
- **Upgradeability** – ความสะดวกในการอัปเกรดระบบ
    
- **Extensibility** – ความสามารถในการรองรับการเพิ่มฟีเจอร์ใหม่โดยไม่กระทบระบบหลัก
    

---

## **Slide 14 – Cloud Characteristics**

- **On-demand scalability** – ปรับทรัพยากรขึ้น/ลงอัตโนมัติตามโหลด
    
- **On-demand elasticity** – ขยายตัวทันทีเมื่อโหลดพุ่งสูง
    
- **Zone-based availability** – แยกทรัพยากรตาม zone เพื่อเพิ่มความทนทาน
    
- **Region-based privacy and security** – ปฏิบัติตามกฎหมายการเก็บข้อมูลของแต่ละประเทศ/ภูมิภาค
    

---

## **Slide 15 – Cross-Cutting Architecture Characteristics**

- **Privacy** – ป้องกันข้อมูลแม้จากบุคลากรภายใน
    
- **Security** – การเข้ารหัส การยืนยันตัวตน กฎควบคุมด้านความปลอดภัย
    
- **Supportability** – ความสะดวกในการ debug และสนับสนุนทางเทคนิค (logging, monitoring)
    
- **Usability / Achievability** – ความง่ายในการใช้งานและระดับการฝึกอบรมที่ผู้ใช้ต้องการ
    

---

## **Slide 16 – Structural Considerations for an Architecture**

- สิ่งที่ต้องพิจารณาในการออกแบบสถาปัตยกรรม:
    
    - **Architectural characteristics** (คุณลักษณะคุณภาพระบบ)
        
    - **Logical architecture components** (โครงสร้างเชิงตรรกะของระบบ)
        

---

## **Slide 17–18 – Logical Architecture Components**

- ส่วนประกอบเชิงตรรกะของระบบที่ทำหน้าที่เป็น “block” ในการแก้ปัญหา (problem domain)
    
- ส่วนประกอบเหล่านี้รวมกันเป็นสถาปัตยกรรมรูปแบบต่าง ๆ → **ขึ้นอยู่กับว่าคุณลักษณะใดสำคัญที่สุด** ต่อความสำเร็จของระบบ
    

---

## **Slide 19 – Limit Characteristics to Prevent Overengineering (เพิ่มเติม)**

- แอปพลิเคชันรองรับคุณลักษณะได้เพียงบางอย่างเท่านั้น เพราะ:
    
    - แต่ละคุณลักษณะใช้ effort และโครงสร้างรองรับ
        
    - คุณลักษณะบางอย่างกระทบกัน (เช่น security ลด performance)
        

---

## **Slide 20 – Trade-offs and Least Worst Architecture**

- การออกแบบสถาปัตยกรรมคือ **การเลือก trade-off ระหว่างปัจจัยต่าง ๆ**
    
- สถาปนิกควรออกแบบแบบ **iterative (Agile)** เพื่อหาทางออกที่ “แย่น้อยที่สุด” (least worst set of trade-offs)