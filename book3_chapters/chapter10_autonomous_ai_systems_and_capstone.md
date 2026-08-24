# วิทยาการคำนวณ 3 การสร้างแบบจำลองทางฟิสิกส์ ปัญญาประดิษฐ์ และคอมพิวเตอร์วิทัศน์
## บทที่ 10 ระบบตัวแทนปัญญาประดิษฐ์อัตโนมัติและโครงงานวิจัยนวัตกรรมทางวิทยาศาสตร์
**ผู้เขียน** ผู้ช่วยศาสตราจารย์ ดร.ชีวะ ทัศนา  
**สังกัด** สาขาวิชาฟิสิกส์ คณะวิทยาศาสตร์และเทคโนโลยี มหาวิทยาลัยราชภัฏรำไพพรรณี  
**เอกสารประกอบรายวิชา** 4122106 ปัญญาประดิษฐ์และการสร้างแบบจำลองทางวิทยาศาสตร์

---

## 📋 แผนบริหารการสอนประจำบทที่ 10

### 1. หัวข้อเนื้อหาประจำบท
1. **วิวัฒนาการสู่ระบบตัวแทนปัญญาประดิษฐ์อัตโนมัติ (Autonomous AI Agents):** Sense-Plan-Act Cycle, ReAct Prompting, Tool Calling
2. **การบูรณาการคอมพิวเตอร์วิทัศน์ 3 มิติเข้ากับระบบควบคุมหุ่นยนต์:** MediaPipe 21-Joint 3D Hand Tracking และการสั่งการไร้สัมผัส
3. **การสร้างระบบจำลองปรากฏการณ์ฟิสิกส์แบบเรียลไทม์ (Real-Time Physics Engine):** Numerical Integration (Euler vs Verlet), Particle Collision
4. **จริยธรรมปัญญาประดิษฐ์และความปลอดภัยทางไซเบอร์ (AI Ethics & Safety):** AI Bias, Privacy, และการปฏิบัติตาม พ.ร.บ. คุ้มครองข้อมูลส่วนบุคคล (PDPA)
5. **คู่มือโครงงานนวัตกรรม Capstone ประจำเล่มที่ 3:** ระบบควบคุมห้องปฏิบัติการอัจฉริยะแบบไร้สัมผัส (Touchless Smart Lab System)

### 2. วัตถุประสงค์เชิงพฤติกรรม
เมื่อศึกษาบทเรียนนี้จบแล้ว ผู้เรียนสามารถ
1. **สังเคราะห์** แนวคิดการเขียนโปรแกรมเชิงคำนวณ โครงสร้างข้อมูล และปัญญาประดิษฐ์เข้าเป็นโครงงานนวัตกรรมที่แก้ปัญหาได้จริง
2. **พัฒนา** ระบบจำลองทางฟิสิกส์หรือปัญญาประดิษฐ์ที่ทำงานร่วมกับระบบติดตามท่าทางมือ 3 มิติ MediaPipe Hands
3. **จัดทำ** รายงานการวิจัยฉบับสมบูรณ์ตามมาตรฐานวิชาการสากล พร้อมการนำเสนอผลงานสู่สาธารณะได้อย่างสง่างาม

---

## 🤖 10.1 สถาปัตยกรรมระบบตัวแทนปัญญาประดิษฐ์อัตโนมัติ

<div align="center" style="margin: 24px 0; page-break-inside: avoid;">
  <img src="../assets/book3_images/fig_mediapipe_ar.jpg" alt="ระบบติดตามมือ 3 มิติ MediaPipe Hands" style="max-width: 100%; max-height: 440px; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.08);" />
  <p style="color: #64748b; font-size: 0.88em; margin-top: 6px;"><em>ภาพที่ 10.1 โครงข่ายกระดูกมือ 21 จุด 3 มิติ (21 3D Hand Landmarks) สำหรับการควบคุมระบบตัวแทนปัญญาประดิษฐ์แบบไร้สัมผัส</em></p>
</div>

### โค้ดตัวอย่างการจำลองการเคลื่อนที่ของอนุภาคในสนามโน้มถ่วง (Verlet Integration)

```python
class VerletParticle:
    """อนุภาคจำลองการเคลื่อนที่ด้วยวิธี Verlet Integration ที่มีความแม่นยำสูง"""
    def __init__(self, x: float, y: float, vx: float, vy: float, mass: float = 1.0):
        self.x = x
        self.y = y
        self.mass = mass
        self.old_x = x - vx * 0.016  # dt = 0.016s (60 FPS)
        self.old_y = y - vy * 0.016

    def update(self, fx: float, fy: float, dt: float = 0.016):
        ax = fx / self.mass
        ay = fy / self.mass
        
        new_x = 2 * self.x - self.old_x + ax * dt**2
        new_y = 2 * self.y - self.old_y + ay * dt**2
        
        self.old_x, self.old_y = self.x, self.y
        self.x, self.y = new_x, new_y

    def __repr__(self) -> str:
        return f"Particle(x={self.x:.2f}, y={self.y:.2f})"

# ทดสอบจำลองการตกอย่างอิสระใต้แรงโน้มถ่วง (g = -9.8 m/s^2)
p = VerletParticle(x=0.0, y=100.0, vx=10.0, vy=0.0)
for step in range(5):
    p.update(fx=0.0, fy=-9.8 * p.mass, dt=0.1)
    print(f"Step {step + 1}: {p}")
```
