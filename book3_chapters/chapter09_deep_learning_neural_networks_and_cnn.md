# วิทยาการคำนวณ 3 การสร้างแบบจำลองทางฟิสิกส์ ปัญญาประดิษฐ์ และคอมพิวเตอร์วิทัศน์
## บทที่ 9 โครงข่ายประสาทเทียมเชิงลึกและการรู้จำภาพด้วย Convolutional Neural Networks
**ผู้เขียน** ผู้ช่วยศาสตราจารย์ ดร.ชีวะ ทัศนา  
**สังกัด** สาขาวิชาฟิสิกส์ คณะวิทยาศาสตร์และเทคโนโลยี มหาวิทยาลัยราชภัฏรำไพพรรณี  
**เอกสารประกอบรายวิชา** 4122106 ปัญญาประดิษฐ์และการสร้างแบบจำลองทางวิทยาศาสตร์

---

## 📋 แผนบริหารการสอนประจำบทที่ 9

### 1. หัวข้อเนื้อหาประจำบท
1. **รากฐานโครงข่ายประสาทเทียม (Artificial Neural Networks Foundations):** เพอร์เซปตรอน (Perceptron), ฟังก์ชันกระตุ้น (ReLU, Sigmoid, Softmax), และอัลกอริทึม Backpropagation
2. **สถาปัตยกรรม Convolutional Neural Networks (CNN):** Convolutional Layer, Kernel Filters, Pooling Layer, และ Dense Classification Layer
3. **การประยุกต์ใช้ CNN ในการจำแนกภาพทางวิทยาศาสตร์:** การจำแนกชนิดผลึกแร่ และการตรวจจับเซลล์จุลชีพ
4. **เทคนิค Transfer Learning และ Fine-tuning โมเดลยุคใหม่:** MobileNetV3, ResNet, EfficientNet
5. **คู่มือห้องปฏิบัติการเสมือนจริง 3D AR MediaPipe:** การจำแนกวัตถุและแสดงแผนที่ความร้อน (Heatmap Visualization) แบบสด

### 2. วัตถุประสงค์เชิงพฤติกรรม
เมื่อศึกษาบทเรียนนี้จบแล้ว ผู้เรียนสามารถ
1. **อธิบาย** หลักการทางคณิตศาสตร์ของการส่งผ่านข้อมูลไปข้างหน้า (Forward Pass) และการแพร่ย้อนกลับ (Backpropagation) ได้อย่างถูกต้อง
2. **ออกแบบและพัฒนา** โครงข่ายประสาทเทียมแบบคอนโวลูชัน (CNN) ในภาษา Python ด้วยไลบรารี PyTorch หรือ TensorFlow
3. **ประเมินผล** ความแม่นยำของโมเดลด้วยเมทริกซ์ Confusion Matrix, Precision, Recall, และ F1-Score
4. **ประยุกต์ใช้** คอมพิวเตอร์วิทัศน์ในการแก้ปัญหาทางวิทยาศาสตร์จริงได้อย่างมีจริยธรรม

---

## 🧠 9.1 สถาปัตยกรรมโครงข่ายประสาทเทียมเชิงลึก

โครงข่ายประสาทเทียมคอนโวลูชัน (CNN) ได้รับแรงบันดาลใจจากระบบการมองเห็นของสมองสิ่งมีชีวิต (Visual Cortex) โดยใช้ตัวกรองขนาดเล็ก (Kernels) เลื่อนกวาดผ่านเมทริกซ์ของภาพ เพื่อสกัดคุณลักษณะเด่น (Feature Maps) ตั้งแต่ระดับเส้นขอบ รูปทรงเรขาคณิต ไปจนถึงวัตถุที่สมบูรณ์

<div align="center" style="margin: 24px 0; page-break-inside: avoid;">
  <img src="../assets/book3_images/fig_cnn_model.jpg" alt="สถาปัตยกรรมโครงข่าย CNN" style="max-width: 100%; max-height: 440px; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.08);" />
  <p style="color: #64748b; font-size: 0.88em; margin-top: 6px;"><em>ภาพที่ 9.1 แผนภาพสถาปัตยกรรมโครงข่ายประสาทเทียมเชิงลึกแบบคอนโวลูชัน (CNN Feature Extraction & Classification)</em></p>
</div>

### โค้ดตัวอย่างการสร้างโมเดลจำแนกภาพอย่างง่ายด้วย PyTorch

```python
import torch
import torch.nn as nn

class ScientificCNN(nn.Module):
    """โครงข่ายประสาทเทียม CNN สำหรับจำแนกภาพตัวอย่างทางวิทยาศาสตร์"""
    def __init__(self, num_classes: int = 10):
        super(ScientificCNN, self).__init__()
        self.features = nn.Sequential(
            nn.Conv2d(in_channels=1, out_channels=16, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(kernel_size=2, stride=2),
            nn.Conv2d(in_channels=16, out_channels=32, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(kernel_size=2, stride=2)
        )
        self.classifier = nn.Sequential(
            nn.Linear(32 * 7 * 7, 64),
            nn.ReLU(),
            nn.Linear(64, num_classes)
        )

    def forward(self, x: torch.Tensor) -> torch.Tensor:
        x = self.features(x)
        x = x.view(x.size(0), -1)  # Flatten
        return self.classifier(x)

# ตรวจสอบโครงสร้างโมเดล
model = ScientificCNN(num_classes=5)
dummy_input = torch.randn(1, 1, 28, 28)
output = model(dummy_input)
print("ขนาดผลลัพธ์จากโมเดล (Batch, Classes):", output.shape)
```
