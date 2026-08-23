# 🔬 คู่มือปฏิบัติการเสมือนจริง 3D AR/XR MediaPipe Hands ประจำบทที่ 8
## ชุดห้องปฏิบัติการวิทยาศาสตร์เชิงคำนวณและแบบจำลองฟิสิกส์ (Computational Physics Labs)
### รายวิชา: 4122104 วิทยาการคำนวณสำหรับการสอนวิทยาศาสตร์ (CS2026)
**ผู้ออกแบบและพัฒนาสื่อ:** ผู้ช่วยศาสตราจารย์ ดร.ชีวะ ทัศนา • คณะวิทยาศาสตร์และเทคโนโลยี มหาวิทยาลัยราชภัฏรำไพพรรณี

---

## 🌌 1. ภาพรวมชุดปฏิบัติการ 5 ห้องทดลอง 3D AR MediaPipe Hands ประจำบทที่ 8

```mermaid
graph TD
    CH8["ชุดปฏิบัติการเสมือนจริง AR MediaPipe ประจำบทที่ 8"]
    CH8 --> L80["8.0 Multi-Scale Universe Sim\n• chapter08_multiscale_universe.html\n• ย่อ-ขยายสเกลจักรวาลจากอนุภาคควาร์กสู่กาแล็กซี 3 มิติ"]
    CH8 --> L81["8.1 NumPy Vector Speed Sandbox\n• chapter08_numpy_speed_sandbox.html\n• แข่งขันความเร็วการคำนวณเวกเตอร์ 1,000,000 จุดระหว่าง For-loop vs NumPy"]
    CH8 --> L82["8.2 Matplotlib 2D/3D Plotter\n• chapter08_matplotlib_2d_plotter.html\n• หมุนดูพื้นผิวความสูง 3D Surface และสนามเวกเตอร์ความเร็ว"]
    CH8 --> L83["8.3 3D Projectile Cannon\n• chapter08_3d_projectile_cannon.html\n• ปรับมุมยิงลูกปืนใหญ่ด้วยมือ AR และวัดพิสัยไกลสุด"]
    CH8 --> L84["8.4 3D Spring Oscillator & Scope\n• chapter08_3d_spring_oscillator.html\n• ดึงยืดสปริง 3 มิติด้วยมือเปล่า และดูคลื่นไซน์บนออสซิลโลสโคปสด"]
```

---

## 📋 2. ตารางบันทึกผลการทดลองโพรเจกไทล์ (Lab 8.3 Projectile Motion Sheet)

| มุมยิง $\theta$ (องศา) | ความเร็วต้น $v_0$ (m/s) | เวลาการบิน $T$ (วินาที) | พิสัยไกลสุด $R$ (เมตร) | ความสูงสูงสุด $H$ (เมตร) |
| :---: | :---: | :---: | :---: | :---: |
| **$15^\circ$** | $50.0\text{ m/s}$ | $2.64\text{ s}$ | $127.46\text{ m}$ | $8.54\text{ m}$ |
| **$30^\circ$** | $50.0\text{ m/s}$ | $5.10\text{ s}$ | $220.78\text{ m}$ | $31.86\text{ m}$ |
| **$45^\circ$ (มุมวิกฤต)** | **$50.0\text{ m/s}$** | **$7.21\text{ s}$** | **$254.93\text{ m}$ (ไกลสุด)** | **$63.73\text{ m}$** |
| **$60^\circ$** | $50.0\text{ m/s}$ | $8.83\text{ s}$ | $220.78\text{ m}$ | $95.59\text{ m}$ |
| **$75^\circ$** | $50.0\text{ m/s}$ | $9.85\text{ s}$ | $127.46\text{ m}$ | $118.92\text{ m}$ |
