# วิทยาการคำนวณ 2 โครงสร้างข้อมูลเชิงลึกและการวิเคราะห์ขั้นตอนวิธี
## บทที่ 10 โครงงานบูรณาการการวิเคราะห์ข้อมูลทางวิทยาศาสตร์และการสร้างภาพข้อมูลเชิงลึก
**ผู้เขียน** ผู้ช่วยศาสตราจารย์ ดร.ชีวะ ทัศนา  
**สังกัด** สาขาวิชาฟิสิกส์ คณะวิทยาศาสตร์และเทคโนโลยี มหาวิทยาลัยราชภัฏรำไพพรรณี  
**เอกสารประกอบรายวิชา** 4122105 โครงสร้างข้อมูลและการวิเคราะห์ขั้นตอนวิธี

---

## 📋 แผนบริหารการสอนประจำบทที่ 10

### 1. หัวข้อเนื้อหาประจำบท
1. **วงจรชีวิตโครงงานวิทยาการข้อมูล (Data Science Project Lifecycle):** Problem Definition, Data Ingestion, Cleaning, Modeling, Visualization
2. **การวิเคราะห์ข้อมูลขนาดใหญ่ด้วยโครงสร้างข้อมูลประสิทธิภาพสูง:** Dictionary Hashing, Pandas DataFrames, NumPy Arrays
3. **การประมวลผลสัญญาณและการวิเคราะห์ข้อมูลเซนเซอร์ IoT:** Moving Average Filter, Fast Fourier Transform (FFT) Concept
4. **การสร้างภาพข้อมูลขั้นสูง (Advanced Scientific Visualization):** กราฟ 2D/3D Scatter, Heatmap, Vector Field
5. **คู่มือโครงงาน Capstone ประจำเล่มที่ 2:** ระบบพยากรณ์สภาพอากาศอัจฉริยะและการวิเคราะห์การใช้พลังงานในอาคาร

### 2. วัตถุประสงค์เชิงพฤติกรรม
เมื่อศึกษาบทเรียนนี้จบแล้ว ผู้เรียนสามารถ
1. **วิเคราะห์และสังเคราะห์** ปัญหาทางวิทยาศาสตร์ให้อยู่ในรูปของโครงงานการประมวลผลข้อมูลเชิงคำนวณได้อย่างเป็นระบบ
2. **เลือกใช้** โครงสร้างข้อมูลที่เหมาะสมเพื่อเพิ่มประสิทธิภาพเชิงเวลา ($O(1)$ หรือ $O(N \log N)$) ในการจัดการชุดข้อมูลขนาดใหญ่
3. **พัฒนา** ระบบจำลองการวิเคราะห์ข้อมูลและสร้างแผนภูมิสรุปผลเชิงภาพได้อย่างแม่นยำ 100%
4. **นำเสนอ** ผลการดำเนินงานโครงงานพร้อมการประเมินความซับซ้อนของอัลกอริทึมอย่างเป็นมืออาชีพ

---

## 📊 10.1 สถาปัตยกรรมโครงงานวิทยาการข้อมูล

ในการทำโครงงานวิทยาศาสตร์ยุคใหม่ การบูรณาการโครงสร้างข้อมูลเช่น Hash Tables ร่วมกับอัลกอริทึม Binary Search และ QuickSort ช่วยให้การประมวลผลข้อมูลเซนเซอร์ระดับหลายแสนรายการสามารถทำได้ในเวลาไม่กี่มิลลิวินาที

<div align="center" style="margin: 24px 0; page-break-inside: avoid;">
  <img src="../assets/book2_images/fig_ml_workflow.jpg" alt="วงจรการพัฒนาโมเดลและวิเคราะห์ข้อมูล" style="max-width: 100%; max-height: 440px; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.08);" />
  <p style="color: #64748b; font-size: 0.88em; margin-top: 6px;"><em>ภาพที่ 10.1 แผนภาพวงจรการประมวลผลข้อมูลและการพัฒนาโมเดลการวิเคราะห์ทางวิทยาศาสตร์</em></p>
</div>

### โค้ดตัวอย่างการกรองและวิเคราะห์สัญญาณข้อมูลเซนเซอร์ (Moving Average Filter)

```python
from typing import List

def moving_average_filter(data: List[float], window_size: int = 5) -> List[float]:
    """กรองสัญญาณรบกวนในข้อมูลเซนเซอร์ด้วยอัลกอริทึม Moving Average O(N)"""
    if not data or window_size <= 0 or window_size > len(data):
        return data
    
    smoothed = []
    window_sum = sum(data[:window_size])
    smoothed.append(window_sum / window_size)
    
    for i in range(window_size, len(data)):
        window_sum += data[i] - data[i - window_size]
        smoothed.append(window_sum / window_size)
        
    return smoothed

# ทดสอบกับข้อมูลอุณหภูมิเซนเซอร์ที่มีสัญญาณรบกวน (Noise)
raw_sensor_data = [25.1, 25.4, 29.8, 25.3, 25.2, 25.6, 31.2, 25.5, 25.4, 25.7]
cleaned_data = moving_average_filter(raw_sensor_data, window_size=3)

print("ข้อมูลดิบจากเซนเซอร์:", raw_sensor_data)
print("ข้อมูลหลังผ่านการกรอง (Smoothed):", [round(x, 2) for x in cleaned_data])
```
