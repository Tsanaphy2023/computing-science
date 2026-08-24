# วิทยาการคำนวณ 2 โครงสร้างข้อมูลเชิงลึกและการวิเคราะห์ขั้นตอนวิธี
## บทที่ 9 สถาปัตยกรรมโปรแกรมเชิงวัตถุและการออกแบบคลาสในงานวิทยาศาสตร์
**ผู้เขียน** ผู้ช่วยศาสตราจารย์ ดร.ชีวะ ทัศนา  
**สังกัด** สาขาวิชาฟิสิกส์ คณะวิทยาศาสตร์และเทคโนโลยี มหาวิทยาลัยราชภัฏรำไพพรรณี  
**เอกสารประกอบรายวิชา** 4122105 โครงสร้างข้อมูลและการวิเคราะห์ขั้นตอนวิธี

---

## 📋 แผนบริหารการสอนประจำบทที่ 9

### 1. หัวข้อเนื้อหาประจำบท
1. **กระบวนทัศน์การโปรแกรมเชิงวัตถุ (Object-Oriented Programming Paradigm):** เปรียบเทียบ Procedural vs OOP
2. **4 เสาหลักของ OOP (The Four Pillars of OOP):**
   * การห่อหุ้มข้อมูล (Encapsulation & Information Hiding)
   * การสืบทอดคุณสมบัติ (Inheritance & Class Hierarchies)
   * พหุสัณฐาน (Polymorphism & Method Overriding)
   * การคิดเชิงนามธรรม (Abstraction & Abstract Base Classes)
3. **การออกแบบคลาสและการสร้างอ็อบเจกต์ใน Python 3.11:** `__init__`, `__str__`, `__repr__`, Properties and Decorators (`@property`)
4. **การประยุกต์ใช้ OOP ในการจำลองระบบฟิสิกส์:** คลาส `Vector2D`, `Particle`, และ `GravitySimulationSystem`
5. **คู่มือห้องปฏิบัติการเสมือนจริง 3D AR MediaPipe:** การจับวัตถุ 3 มิติและถ่ายทอดสถานะคลาสด้วยท่าทางมือ

### 2. วัตถุประสงค์เชิงพฤติกรรม
เมื่อศึกษาบทเรียนนี้จบแล้ว ผู้เรียนสามารถ
1. **อธิบาย** หลักการ 4 เสาหลักของกระบวนทัศน์เชิงวัตถุได้อย่างถูกต้องตามหลักวิศวกรรมซอฟต์แวร์
2. **ออกแบบและสร้าง** คลาสในภาษา Python ที่มีการห่อหุ้มข้อมูลและเมธอดอย่างเป็นระบบ
3. **ประยุกต์ใช้** การสืบทอดคุณสมบัติและพหุสัณฐานในการจำลองวัตถุทางวิทยาศาสตร์ที่มีพฤติกรรมหลากหลาย
4. **พัฒนา** โปรแกรมจำลองระบบอนุภาคที่มีความเสถียรและโครงสร้างโค้ดแบบ Reusable Component 100%

---

## 🏛️ 9.1 รากฐานกระบวนทัศน์การโปรแกรมเชิงวัตถุ

ในการพัฒนาระบบซอฟต์แวร์ขนาดใหญ่ การจัดระเบียบข้อมูลและฟังก์ชันที่กระจัดกระจายมักนำไปสู่ความผิดพลาดที่ซับซ้อน กระบวนทัศน์เชิงวัตถุ (OOP) จึงถูกคิดค้นขึ้นเพื่อรวมเอา **ข้อมูล (State / Attributes)** และ **พฤติกรรมการทำงาน (Behavior / Methods)** เข้าไว้ด้วยกันเป็นหน่วยเดียวที่เรียกว่า **คลาส (Class)** และ **อ็อบเจกต์ (Object)**

<div align="center" style="margin: 24px 0; page-break-inside: avoid;">
  <img src="../assets/book2_images/fig_oop_pillars.jpg" alt="แผนผัง 4 เสาหลักของ OOP" style="max-width: 100%; max-height: 440px; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.08);" />
  <p style="color: #64748b; font-size: 0.88em; margin-top: 6px;"><em>ภาพที่ 9.1 โครงสร้าง 4 เสาหลักของการเขียนโปรแกรมเชิงวัตถุ: Encapsulation, Inheritance, Polymorphism, Abstraction</em></p>
</div>

### โค้ดตัวอย่างการสร้างคลาสเวกเตอร์ 2 มิติทางฟิสิกส์ (Vector2D Class)

```python
import math

class Vector2D:
    """คลาสสำหรับจัดการเวกเตอร์ 2 มิติในระบบฟิสิกส์"""
    def __init__(self, x: float = 0.0, y: float = 0.0):
        self._x = float(x)
        self._y = float(y)

    @property
    def x(self) -> float:
        return self._x

    @property
    def y(self) -> float:
        return self._y

    def magnitude(self) -> float:
        """คำนวณขนาดของเวกเตอร์ |v| = sqrt(x^2 + y^2)"""
        return math.sqrt(self._x**2 + self._y**2)

    def normalize(self) -> 'Vector2D':
        """แปลงเป็นเวกเตอร์หนึ่งหน่วย"""
        mag = self.magnitude()
        if mag == 0:
            return Vector2D(0, 0)
        return Vector2D(self._x / mag, self._y / mag)

    def __add__(self, other: 'Vector2D') -> 'Vector2D':
        return Vector2D(self._x + other._x, self._y + other._y)

    def __sub__(self, other: 'Vector2D') -> 'Vector2D':
        return Vector2D(self._x - other._x, self._y - other._y)

    def __mul__(self, scalar: float) -> 'Vector2D':
        return Vector2D(self._x * scalar, self._y * scalar)

    def __repr__(self) -> str:
        return f"Vector2D(x={self._x:.2f}, y={self._y:.2f}, mag={self.magnitude():.2f})"

# ทดสอบการใช้งาน
v1 = Vector2D(3.0, 4.0)
v2 = Vector2D(1.0, 2.0)
v_result = v1 + v2
print(f"ผลรวมเวกเตอร์: {v_result}")
print(f"ขนาดเวกเตอร์ v1: {v1.magnitude():.2f}")
```

---

## 🔬 9.2 คู่มือปฏิบัติการเสมือนจริง 3D AR OOP System

ผู้เรียนสามารถเปิดห้องปฏิบัติการเสมือนจริงเพื่อทดสอบการสร้างและควบคุมอินสแตนซ์ของคลาส Particle ในอวกาศ 3 มิติ ด้วยการขยับมือจับปล่อยวัตถุผ่านกล้องเว็บแคมได้ทันที
