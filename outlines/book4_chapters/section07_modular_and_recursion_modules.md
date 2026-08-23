# วิทยาการคำนวณ 4: สื่อการเรียนรู้ดิจิทัลและคู่มือปฏิบัติการเสมือนจริงบนระบบ MOOC
## หมวดหมู่ที่ 7 การเขียนโปรแกรมเชิงโมดูลและฟังก์ชันเรียกซ้ำ (Modular & Recursion Modules)
**ผู้พัฒนาหลักสูตร:** ผู้ช่วยศาสตราจารย์ ดร.ชีวะ ทัศนา • สาขาวิชาฟิสิกส์ คณะวิทยาศาสตร์และเทคโนโลยี มหาวิทยาลัยราชภัฏรำไพพรรณี

---

## 🎯 ผลลัพธ์การเรียนรู้ประจำหมวดที่ 7
1. ออกแบบฟังก์ชันตามหลักการ Pure Functions, กฎขอบเขตตัวแปร LEGB, และ `*args`, `**kwargs`
2. จัดการไฟล์ข้อมูล CSV / JSON ด้วย Context Manager ปลอดภัย 100%
3. ทำความเข้าใจฟังก์ชันเรียกซ้ำ (Recursion) และแก้ปัญหาหอคอยฮานอยผ่านแอนิเมชัน 3 มิติ

---

## 📚 รายละเอียด 5 โมดูลบทเรียนดิจิทัล

### 🔹 โมดูล 7.0: เรื่องเล่าเปิดบทเรียนและสถาปัตยกรรมโค้ดที่สะอาดและยั่งยืน (Clean Architecture)
* **เนื้อหาสื่อการสอน:** ปรัชญา UNIX "Do One Thing and Do It Well" และการป้องกัน Monolithic Spaghetti Code
* **ชุดจำลองเสมือนจริงในระบบ:**
  * Interactive Code Refactoring & Complexity Visualizer

---

### 🔹 โมดูล 7.1: การออกแบบฟังก์ชัน พารามิเตอร์ และค่าคืนกลับ (Functions & Return)
* **เนื้อหาสื่อการสอน:** Positional vs Keyword Args, Default Parameters, `*args`, `**kwargs`, Lambda Expressions
* **ชุดจำลองเสมือนจริงในระบบ:**
  * Function Parameter Scope & LEGB Stack Frame Simulator

---

### 🔹 โมดูล 7.2: การสร้างโมดูลและการใช้งานไลบรารีมาตรฐาน (Python Modules)
* **เนื้อหาสื่อการสอน:** การสร้างโมดูล `.py` นำกลับมาใช้ซ้ำ, โมดูลมาตรฐาน `math`, `random`, `time`
* **ชุดจำลองเสมือนจริงในระบบ:**
  * Physics Vector Math Module Test Runner

---

### 🔹 โมดูล 7.3: การอ่านเขียนไฟล์และการจัดการข้อมูล CSV / JSON
* **เนื้อหาสื่อการสอน:** `with open(..., encoding='utf-8')`, `csv.DictReader`, `json.dump()`, Data Aggregation
* **ชุดจำลองเสมือนจริงในระบบ:**
  * Interactive CSV/JSON File Parser & Live Stats Generator

---

### 🔹 โมดูล 7.4: ฟังก์ชันเรียกซ้ำ (Recursion) และปริศนาหอคอยฮานอย
* **เนื้อหาสื่อการสอน:** Base Case, Recursive Step, Call Stack Frame, ปริศนาหอคอยฮานอย ($2^n - 1$)
* **ชุดจำลองเสมือนจริงในระบบ:**
  * 3D Animated Tower of Hanoi Recursive Solver
* **แบบทดสอบท้ายหมวดที่ 7 (Formative Quiz 5 ข้อ):** ประเมินทักษะการคำนวณ Call Stack และการจัดการไฟล์
