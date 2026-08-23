# 🔬 คู่มือปฏิบัติการเสมือนจริง 3D AR/XR MediaPipe Hands ประจำบทที่ 7
## ชุดห้องปฏิบัติการการเขียนโปรแกรมเชิงโมดูลและฟังก์ชันเรียกซ้ำ
### รายวิชา 4122104 วิทยาการคำนวณสำหรับการสอนวิทยาศาสตร์
**ผู้ออกแบบและพัฒนาสื่อ** ผู้ช่วยศาสตราจารย์ ดร.ชีวะ ทัศนา • คณะวิทยาศาสตร์และเทคโนโลยี มหาวิทยาลัยราชภัฏรำไพพรรณี

---

## 🌌 1. ภาพรวมชุดปฏิบัติการ 5 ห้องทดลอง 3D AR MediaPipe Hands ประจำบทที่ 7

```mermaid
graph TD
    CH7["ชุดปฏิบัติการเสมือนจริง AR MediaPipe ประจำบทที่ 7"]
    CH7 --> L70["7.0 Clean Code & SRP Visualizer\n• chapter07_clean_code_visualizer.html\n• จัดหมวดหมู่ฟังก์ชันตามหลักการ Single Responsibility Principle"]
    CH7 --> L71["7.1 LEGB Scope Simulator\n• chapter07_legb_scope_simulator.html\n• ส่องกล้องดูขอบเขตตัวแปร Local, Enclosing, Global, Built-in 3D"]
    CH7 --> L72["7.2 Vector Math Module Runner\n• chapter07_vector_math_runner.html\n• หมุนและคำนวณผลคูณ Dot Product ของเวกเตอร์ฟิสิกส์ 3 มิติ"]
    CH7 --> L73["7.3 Live CSV/JSON Data Parser\n• chapter07_csv_json_parser.html\n• ลากไฟล์ข้อมูลจำลองมาปล่อยเพื่อแปลงเป็นโครงสร้าง Dictionary"]
    CH7 --> L74["7.4 3D Tower of Hanoi Recursion\n• chapter07_hanoi_recursion_3d.html\n• ใช้มือ AR จีบนิ้วย้ายแผ่นจานหอคอยฮานอยและดู Call Stack 3D"]
```

---

## 📋 2. ตารางบันทึกผลการทดลองหอคอยฮานอย

| จำนวนแผ่นจาน ($N$) | จำนวนขั้นตอนตามทฤษฎี ($2^N - 1$) | เวลาที่อัลกอริทึมเรียกซ้ำใช้แก้ปัญหา | สถานะ Stack Overflow |
| :---: | :---: | :---: | :---: |
| **3 จาน** | $2^3 - 1 = \mathbf{7}\text{ ขั้นตอน}$ | $0.0001\text{ วินาที}$ | ✅ ผ่าน (Call Stack ลึก 3 ชั้น) |
| **5 จาน** | $2^5 - 1 = \mathbf{31}\text{ ขั้นตอน}$ | $0.0005\text{ วินาที}$ | ✅ ผ่าน (Call Stack ลึก 5 ชั้น) |
| **10 จาน** | $2^{10} - 1 = \mathbf{1,023}\text{ ขั้นตอน}$ | $0.015\text{ วินาที}$ | ✅ ผ่าน (Call Stack ลึก 10 ชั้น) |
| **20 จาน** | $2^{20} - 1 = \mathbf{1,048,575}\text{ ขั้นตอน}$ | $1.25\text{ วินาที}$ | ⚠️ ใช้เวลาในการประมวลผลสูง |
