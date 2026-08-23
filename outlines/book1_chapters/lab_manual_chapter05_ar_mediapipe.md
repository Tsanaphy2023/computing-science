# 🔬 คู่มือปฏิบัติการเสมือนจริง 3D AR/XR MediaPipe Hands ประจำบทที่ 5
## ชุดห้องปฏิบัติการโครงสร้างข้อมูลและอัลกอริทึมการค้นหา (Touchless Search Labs)
### รายวิชา: 4122104 วิทยาการคำนวณสำหรับการสอนวิทยาศาสตร์ (CS2026)
**ผู้ออกแบบและพัฒนาสื่อ:** ผู้ช่วยศาสตราจารย์ ดร.ชีวะ ทัศนา • คณะวิทยาศาสตร์และเทคโนโลยี มหาวิทยาลัยราชภัฏรำไพพรรณี

---

## 🌌 1. ภาพรวมชุดปฏิบัติการ 5 ห้องทดลอง 3D AR MediaPipe Hands ประจำบทที่ 5

```mermaid
graph TD
    CH5["ชุดปฏิบัติการเสมือนจริง AR MediaPipe ประจำบทที่ 5"]
    CH5 --> L50["5.0 Data Storage Architecture\n• chapter05_data_storage_arch.html\n• จัดเรียงบล็อกข้อมูลลงในสล็อตหน่วยความจำ 3D"]
    CH5 --> L51["5.1 Dynamic List Visualizer\n• chapter05_dynamic_list_visualizer.html\n• ใช้มือ AR ทดสอบการ append, insert, pop สมาชิกใน List"]
    CH5 --> L52["5.2 Hash Table Dictionary Sandbox\n• chapter05_hash_table_sandbox.html\n• จำลองการคำนวณ Hash Function และการเข้าถึงข้อมูล O(1)"]
    CH5 --> L53["5.3 Linear Search Visualizer\n• chapter05_linear_search_visualizer.html\n• สังเกตแสงสแกนค้นหาข้อมูลทีละรายการจากซ้ายไปขวา"]
    CH5 --> L54["5.4 Binary vs Linear Speed Race\n• chapter05_binary_search_race.html\n• แข่งขันความเร็วการค้นหาข้อมูล 1 ล้านสมาชิกแบบ Real-time"]
```

---

## 📋 2. ตารางบันทึกผลการทดลองการแข่งขันความเร็ว (Lab 5.4 Benchmark Sheet)

| ขนาดชุดข้อมูล ($N$) | ค่าเป้าหมาย (Target) | จำนวนรอบ Linear Search | จำนวนรอบ Binary Search | อัตราความเร็วที่เหนือกว่า |
| :---: | :---: | :---: | :---: | :---: |
| **1,000** | 995 | 995 รอบ | 10 รอบ | 99.5 เท่า |
| **10,000** | 9,990 | 9,990 รอบ | 14 รอบ | 713.6 เท่า |
| **100,000** | 99,990 | 99,990 รอบ | 17 รอบ | 5,881.8 เท่า |
| **1,000,000** | 999,999 | 1,000,000 รอบ | 20 รอบ | **50,000.0 เท่า!** |
