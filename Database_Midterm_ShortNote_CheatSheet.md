# ⚡ Short Note & Cheat Sheet สรุปฐานข้อมูล Midterm (จำไว้อ่านก่อนเข้าห้องสอบ)
> สรุปย่อสาระสำคัญ 4 บท สำหรับทบทวนด่วน 10 นาทีก่อนสอบ

---

## 📌 บทที่ 1: Database Approach & Overview

### 1. คำศัพท์หัวใจสำคัญ
- **Data (ข้อมูลดิบ):** ตัวเลข/ข้อความที่ยังไม่ประมวลผล ไร้ความหมายในตัวเอง เช่น `25`
- **Information (สารสนเทศ):** ข้อมูลที่ผ่านการประมวลผล จัดรูปแบบ จนเกิดความหมายและมีคุณค่า เช่น `อายุ 25 ปี`
- **Metadata:** ข้อมูลที่ใช้อธิบายข้อมูล (เช่น ชนิดข้อมูล, ขนาดฟิลด์)
- **Data Redundancy:** ข้อมูลซ้ำซ้อน นำไปสู่ปัญหา **Anomalies 3 อย่าง** (Insert, Update, Delete)
- **DBMS:** ตัวกลางจัดการฐานข้อมูล มีหน้าที่เด่นคือ Data Dictionary, Multi-user access, Security, Backup & Recovery, Data Integrity

### 2. ชนิดของ Database (แบ่งตามการใช้งาน)
- **OLTP (Operational):** งานประจำวัน, รายการย่อยเยอะ, Real-time, เน้นเร็วและแม่นยำ (เช่น เซเว่น, ตู้ ATM)
- **OLAP (Data Warehouse):** ข้อมูลสะสมย้อนหลัง เพื่อนำไปวิเคราะห์และทำนายแนวโน้มทางธุรกิจของผู้บริหาร

---

## 📌 บทที่ 2: Data Models & Abstraction Levels

### 1. วิวัฒนาการแบบจำลองข้อมูล (Data Models)
1. **Hierarchical:** ต้นไม้ (Parent-Child 1:M) แข็งทื่อ ไม่ยืดหยุ่น
2. **Network:** กราฟ (Owner-Member M:N) เริ่มมี Schema / Subschema / DDL / DML
3. **Relational (RDBMS):** ตาราง 2 มิติ เชื่อมด้วย PK/FK ใช้งานง่ายด้วยภาษา SQL
4. **Object-Oriented (OODBMS):** รวม Data + Methods (Encapsulation, Inheritance, Polymorphism)
5. **NoSQL:** ไม่ใช้ตาราง รองรับ Big Data 3V (Volume, Velocity, Variety) เช่น Key-Value, Document

### 2. ระดับการซ่อนข้อมูล (Degrees of Data Abstraction - ANSI/SPARC)
```
ระดับภายนอก:   [ 1. External Model ]   <-- มองโดย User / UI (ไม่ขึ้นกับ DBMS, ไม่ขึ้นกับ HW)
ระดับแนวคิด:   [ 2. Conceptual Model ] <-- มองโดย Designer / ER Diagram (ไม่ขึ้นกับ DBMS, ไม่ขึ้นกับ HW)
ระดับภายใน:    [ 3. Internal Model ]   <-- มองโดย DBA / Table Schema (*ขึ้นกับ DBMS*, ไม่ขึ้นกับ HW)
ระดับกายภาพ:   [ 4. Physical Model ]   <-- มองโดย Storage / Bytes/Disk (*ขึ้นกับ DBMS*, *ขึ้นกับ HW*)
```

---

## 📌 บทที่ 3: Relational Model Characteristics

### 1. สรุปประเภทของ Keys (ออกสอบ 100%)
- **Superkey:** คีย์ใดๆ ที่ระบุแถวได้ไม่ซ้ำ (มีของแถมติดมาได้)
- **Candidate Key:** Superkey ที่สั้นที่สุด/ไม่มีของแถม (Minimal)
- **Primary Key (PK):** Candidate Key ที่ถูกเลือกใช้จริง **(ห้ามซ้ำ และห้ามเป็น NULL)**
- **Foreign Key (FK):** คอลัมน์ที่ชี้ไปหา PK ตารางแม่ (ต้องตรงกับแม่ หรือเป็น NULL)
- **Composite Key:** คีย์ที่ต้องใช้ตั้งแต่ 2 คอลัมน์ขึ้นไปรวมกัน
- **Surrogate Key:** คีย์จำลอง/เลขรันอัตโนมัติ (1, 2, 3...) ที่ระบบสร้างขึ้น

### 2. กฎความถูกต้อง (Integrity Rules)
- **Entity Integrity:** ตรวจ Primary Key $\rightarrow$ ห้าม NULL, ห้ามซ้ำ
- **Referential Integrity:** ตรวจ Foreign Key $\rightarrow$ ต้องชี้ไปยัง PK ที่มีจริง หรือปล่อยเป็น NULL

### 3. ตัวดำเนินการ Relational Algebra
- **Select ($\sigma$):** กรองเอาเฉพาะ **แถว (Rows)** ตามเงื่อนไข
- **Project ($\pi$):** เลือกเอาเฉพาะ **คอลัมน์ (Columns)** ที่ต้องการ
- **Join ($\bowtie$):** ผูกตารางเข้าด้วยกันผ่านคีย์ที่ตรงกัน
- **Cartesian Product ($\times$):** จับคู่ทุกแถว ($M \times N$)

---

## 📌 บทที่ 4: Normalization (ขั้นตอนลดความซ้ำซ้อน)

### 1. ชนิดของ Functional Dependency (FD)
- **Full Dependency:** ขึ้นกับ PK ทุกตัวรวมกัน (ถูกต้องตามมาตรฐาน)
- **Partial Dependency:** ดันไปขึ้นกับ PK แค่บางตัว (เกิดเมื่อ PK เป็นคีย์ผสม)
- **Transitive Dependency:** Non-Key ชี้ไปหา Non-Key ด้วยกันเอง ($X \rightarrow Y \rightarrow Z$)

### 2. สูตรท่องจำระดับ Normalization
| ลำดับขั้น | กฎเหล็กที่ต้องจำ | วิธีแก้ |
| :---: | :--- | :--- |
| **UNF $\rightarrow$ 1NF** | 1 ช่องต้องมี 1 ค่า (Atomic) + ไม่มี Repeating Group + มี PK | เติมช่องว่างให้เต็ม, กำหนด PK |
| **1NF $\rightarrow$ 2NF** | **กำจัด Partial Dependency** (ถ้า PK มีตัวเดียว ผ่านทันที) | แตกตารางส่วนที่ขึ้นกับ PK แค่ครึ่งเดียวออกไป |
| **2NF $\rightarrow$ 3NF** | **กำจัด Transitive Dependency** (ห้าม Non-Key ชี้ Non-Key) | แตกตารางตัวที่เป็น Non-Key ชี้กันเองออกไป |
| **3NF $\rightarrow$ BCNF** | **ทุกตัวกำหนด (Determinant) ต้องเป็น Candidate Key** | แตกตารางตัวกำหนดที่เป็นปัญหาออกไป |
| **BCNF $\rightarrow$ 4NF** | **กำจัด Multivalued Dependency** (ห้ามมี 1:M 2 ชุดปนกัน) | แตกเป็น 2 ตารางย่อย |

---

## 🎯 3 คำถามเช็คความเข้าใจก่อนเข้าห้องสอบ
1. *ถ้าตารางอยู่ใน 1NF และมี Primary Key เป็นคอลัมน์เดี่ยว (`StudentID`) ตารางนี้อยู่ใน 2NF หรือยัง?*  
   👉 **ตอบ:** อยู่ใน 2NF แล้วทันที! เพราะจะเกิด Partial Dependency ได้ก็ต่อเมื่อ Primary Key เป็นคีย์ผสม (Composite Key) เท่านั้น
2. *ความแตกต่างระหว่าง Superkey กับ Candidate Key คืออะไร?*  
   👉 **ตอบ:** Candidate Key คือ Superkey ขั้นต่ำสุดที่ไม่มีคอลัมน์ส่วนเกิน (Minimal)
3. *ทำไมระบบ Data Warehouse ถึงนิยมทำ Denormalization?*  
   👉 **ตอบ:** เพื่อลดจำนวนการ `JOIN` ตารางหลายๆ ชั้น ทำให้ดึงข้อมูลและออกรายงานได้เร็วขึ้นอย่างมาก (Trade-off ระหว่าง Speed กับ Redundancy)
