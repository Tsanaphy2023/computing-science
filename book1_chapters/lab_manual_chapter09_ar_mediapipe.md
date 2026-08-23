# 🔬 คู่มือปฏิบัติการเสมือนจริง 3D AR/XR MediaPipe Hands ประจำบทที่ 9
## ชุดห้องปฏิบัติการปัญญาประดิษฐ์ คอมพิวเตอร์วิทัศน์ และ IoT
### รายวิชา: 4122104 วิทยาการคำนวณสำหรับการสอนวิทยาศาสตร์ (CS2026)
**ผู้ออกแบบและพัฒนาสื่อ:** ผู้ช่วยศาสตราจารย์ ดร.ชีวะ ทัศนา • คณะวิทยาศาสตร์และเทคโนโลยี มหาวิทยาลัยราชภัฏรำไพพรรณี

---

## 🌌 1. ภาพรวมชุดปฏิบัติการ 5 ห้องทดลอง 3D AR MediaPipe Hands ประจำบทที่ 9

```mermaid
graph TD
    CH9["ชุดปฏิบัติการเสมือนจริง AR MediaPipe ประจำบทที่ 9"]
    CH9 --> L90["9.0 Smart Agro-Factory Map\n• chapter09_smart_agro_factory.html\n• แผนที่โรงงานเกษตร 4.0 จำลองการไหลเวียนของข้อมูลเซนเซอร์"]
    CH9 --> L91["9.1 ML KNN Classifier Sandbox\n• chapter09_ml_classifier_sandbox.html\n• พล็อตจุดข้อมูลการทดลองและจำแนกกลุ่มด้วย K-Nearest Neighbors 3D"]
    CH9 --> L92["9.2 Real-Time Color Tracker\n• chapter09_realtime_color_tracker.html\n• ใช้กล้องเว็บแคมตรวจจับสีวัตถุจริงและลากเส้นติดตามวิถี"]
    CH9 --> L93["9.3 3D Cyber Skeleton Tracker\n• chapter09_cyber_skeleton_tracker.html\n• แสดงพิกัด 21 ข้อต่อนิ้วมือและทดสอบท่าทาง Pinch / Grab / Point"]
    CH9 --> L94["9.4 Cloud IoT Telemetry Dashboard\n• chapter09_cloud_iot_telemetry.html\n• แดชบอร์ดมอนิเตอร์เซนเซอร์อุณหภูมิและความชื้นแบบ Real-Time"]
```

---

## 📋 2. ตารางบันทึกผลการทดลองการตรวจจับท่าทาง (Lab 9.3 Landmark Sheet)

| ท่าทางมือ (Hand Gesture) | ข้อต่อที่ใช้ตรวจจับ (Landmarks) | เงื่อนไขคณิตศาสตร์ (Math Condition) | ผลลัพธ์ในระบบ 3D AR |
| :---: | :---: | :---: | :---: |
| **Point (☝️ ชี้พิกัด)** | Index Tip (8) เหยียดตรง, นิ้วอื่นพับ | $y_8 < y_6$ และ $y_{12} > y_{10}$ | ฉายลำแสงเลเซอร์เล็งพิกัดในอวกาศ 3 มิติ |
| **Pinch (🤏 จีบนิ้ว)** | Thumb Tip (4) ชิด Index Tip (8) | $\text{Distance}(4, 8) < 0.08$ | **จับยึดวัตถุ 3D (Pick & Place)** + เสียง Chime |
| **Fist Grab (✊ กำหมัด)** | ปลายนิ้ว 8, 12, 16, 20 พับเข้าหาฝ่ามือ (0) | $\text{Avg Distance} < 0.12$ | **หมุนมุมมองฉาก 360 องศา (Spatial Orbit)** |
| **Open Palm (🖐️ แบมือ)** | ปลายนิ้วทุกนิ้วเหยียดตรงออก | $\text{Avg Distance} > 0.35$ | **เปิดแถบเมนูโฮโลแกรม (Holographic HUD)** |
