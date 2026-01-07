<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&height=80&section=header&color=0:0A2540,50:0F4C81,100:2F80ED&text=%F0%9F%98%B7+YOLO+Nesil+Benchmark+-+YOLOv8n+%E2%80%A2+YOLO10n+%E2%80%A2+YOLO11n+%7C+Maske+Tespiti&fontColor=42FFF0&fontSize=20&animation=neon" />
</p>





## 📖 Proje Özeti

Bu proje, Ultralytics'in en güncel hafif modelleri olan **YOLOv8n**, **YOLOv10n** ve **YOLO11n**'nin yüz maskesi tespiti performanslarını **aynı koşullar** altında karşılaştırmaktadır.

Tüm modeller şu parametrelerle eğitilmiştir:
- **Epoch**: 15
- **Görüntü Boyutu**: 320×320
- **Donanım**: Google Colab (Tesla T4 GPU)
- **Framework**: Ultralytics 8.3.249
- **Veri Seti**: 100 validasyon görüntüsü → 327 kutu (49 mask, 278 no_mask)

<br>

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&height=60&section=header&color=0:0A2540,50:0F4C81,100:2F80ED&text=%F0%9F%9A%80+Performans+Kar%C5%9F%C4%B1la%C5%9Ft%C4%B1rma+Tablosu&fontColor=42FFF0&fontSize=18&animation=neon" />
</p>

| Model       | mAP50   | mAP50-95 | Parametre | GFLOPs | Inference (ms) | Ağırlık Boyutu | mask mAP50 | no_mask mAP50 | Öne Çıkan Özellik                          |
|-------------|---------|----------|-----------|--------|----------------|----------------|------------|---------------|--------------------------------------------|
| **YOLO11n** | 0.722   | 0.384    | 2.58M     | 6.3    | 2.6            | ~5.4 MB        | **0.585**  | 0.859         | **En iyi maske tespiti**                   |
| **YOLOv8n** | **0.723**| **0.389**| 3.01M     | 8.1    | **2.1**        | ~6.2 MB        | 0.605      | **0.840**     | **En yüksek genel doğruluk**               |
| **YOLO10n** | 0.637   | 0.338    | **2.27M** | 6.5    | **2.1**        | ~5.7 MB        | 0.488      | 0.786         | **En hafif & NMS-free**                    |

<br>

## 📊 Detaylı Model Analizleri
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
<p align="">
  <img src="https://img.shields.io/badge/Model-YOLO11n-2F80ED?style=for-the-badge">
  <img src="https://img.shields.io/badge/Role-Mask_Detection_Specialist-ff69b4?style=for-the-badge">
</p>
En güncel mimari sayesinde küçük nesneleri (maske) daha iyi yakalar.

**Sınıf Metrikleri**  
- `mask` → Precision: 0.803 | Recall: 0.498 | **mAP50: 0.585**  
- `no_mask` → Precision: 0.877 | Recall: 0.809 | mAP50: 0.859

<table align="center">
  <tr>
    <td align="center">
      <img src="https://raw.githubusercontent.com/nihatbayramm/YoloMaskeTespitModeli/main/results_yolo11.png"
           width="300" alt="YOLO11 Sonuç"/>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/nihatbayramm/YoloMaskeTespitModeli/main/confusion_matrix_yolo11.png"
           width="300" alt="YOLO11 Confusion Matrix"/>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/4cac18bb-016e-4c76-9f2d-c7e235e586fa"
           width="300" alt="YOLO11 Samples"/>
    </td>
  </tr>
</table>






------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<p align="">
  <img src="https://img.shields.io/badge/Model-YOLOv8n-00c853?style=for-the-badge">
  <img src="https://img.shields.io/badge/Role-High_Accuracy_Leader-ffd600?style=for-the-badge">
</p>
Genel doğrulukta lider, özellikle maskesiz yüzleri çok güvenilir tespit eder.

**Sınıf Metrikleri**  
- `mask` → Precision: 0.779 | Recall: 0.574 | mAP50: 0.605  
- `no_mask` → Precision: 0.814 | Recall: 0.806 | **mAP50: 0.840**

<table align="center">
  <tr>
    <td align="center">
      <img src="https://raw.githubusercontent.com/nihatbayramm/YoloMaskeTespitModeli/main/results_v8.png"
           width="300" alt="YOLOv8 Sonuç"/>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/nihatbayramm/YoloMaskeTespitModeli/main/confusion_matrix_v8.png"
           width="300" alt="YOLOv8 Confusion Matrix"/>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/1139d31e-f52f-4bbb-9869-6708adeb81de"
           width="300" alt="YOLOv8 Samples"/>
    </td>
  </tr>
</table>



------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<p align="">
  <img src="https://img.shields.io/badge/Model-YOLO10n-ff9100?style=for-the-badge">
  <img src="https://img.shields.io/badge/Role-Edge_%26_Mobile_Friendly-29b6f6?style=for-the-badge">
</p>
NMS gerektirmeyen yapısıyla en düşük parametre sayısı ve yüksek hız.

**Sınıf Metrikleri**  
- `mask` → Precision: 0.622 | Recall: 0.449 | mAP50: 0.488  
- `no_mask` → Precision: 0.693 | Recall: 0.809 | mAP50: 0.786

<table align="center">
  <tr>
    <td align="center">
      <img src="https://raw.githubusercontent.com/nihatbayramm/YoloMaskeTespitModeli/main/results_v10.png"
           width="300" alt="YOLO10 Sonuç"/>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/nihatbayramm/YoloMaskeTespitModeli/main/confusion_matrix_v10.png"
           width="300" alt="YOLO10 Confusion Matrix"/>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/3f390dff-ae23-4713-b83f-3f5230cda0a7"
           width="300" alt="YOLO10 Samples"/>
    </td>
  </tr>
</table>



------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<p align="left">
  <img src="https://readme-typing-svg.herokuapp.com?size=20&duration=2200&pause=900&color=2F80ED&center=false&vCenter=true&width=440&lines=⚙️+Kurulum+%26+Eğitim;🚀+Birleşik+Benchmark+Pipeline" />
</p>

```bash
╔════════════════════════════════════════════════════════════╗
║ ⚙️  Kurulum · 🚀 Eğitim · 🔍 Tespit (Pro Sürüm)            ║
╟────────────────────────────────────────────────────────────╢
║  🎯 Epoch: 15     🖼️ Görüntü Boyutu: 320×320               ║
║  ⚡ Donanım: T4 GPU   🧩 Çerçeve: Ultralytics               ║
╚════════════════════════════════════════════════════════════╝


📦 Gerekli Kütüphanelerin Kurulumu
────────────────────────────────────────────────────────────
pip install ultralytics opencv-python


🚀 Model Eğitimi (Tüm Modeller Aynı Koşullarda)
────────────────────────────────────────────────────────────
# 🟦 YOLOv8n — Dengeli doğruluk
yolo train model=yolov8n.pt data=mask_dataset.yaml epochs=15 imgsz=320

# 🟨 YOLO10n — NMS-Free · Hafif · Edge cihazlar için uygun
yolo train model=yolo10n.pt data=mask_dataset.yaml epochs=15 imgsz=320

# 🟥 YOLO11n — Yeni nesil · Küçük nesne tespitinde güçlü
yolo train model=yolo11n.pt data=mask_dataset.yaml epochs=15 imgsz=320


🔍 Tespit Çalıştırma (Python API — Önerilen Yöntem)
────────────────────────────────────────────────────────────
from ultralytics import YOLO

# Eğitilmiş en iyi modeli yükle
model = YOLO("runs/detect/mask_train_yolo11/weights/best.pt")

# Tek görüntü üzerinde tespit çalıştır
results = model("test_image.jpg")[0]

# Sonucu ekranda göster
results.show()

# Sonucu dosyaya kaydetmek istersen:
# results.save("sonuc.jpg")
╚════════════════════════════════════════════════════════════╝


```

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


### 🏆 Sonuç Karşılaştırması

<p align="center">
  <img src="https://github.com/andreasbm/readme/blob/master/assets/lines/fire.png" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Winner-YOLOv8n-%23FFD700?style=for-the-badge">
  <img src="https://img.shields.io/badge/Best_Mask-YOLO11n-%23FF4081?style=for-the-badge">
  <img src="https://img.shields.io/badge/Fastest-YOLO10n-%2300B0FF?style=for-the-badge">
</p>

| Kategori         | Kazanan         | Açıklama |
|------------------|-----------------|---------|
| Genel Doğruluk   | **YOLOv8n**     | mAP50: **0.723** — Dengeli performans |
| Maske Tespiti    | **YOLO11n**     | mask sınıfı mAP50: **0.585** — Küçük nesnelerde güçlü |
| Hız & Hafiflik   | **YOLO10n / YOLOv8n** | ~**2.1 ms inference** — Mobil & edge cihazlar için ideal |

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


## ✨ Geliştirici / Hazırlayan

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=2600&pause=900&center=true&vCenter=true&width=460&height=70&color=5BFA7A&background=001B11&lines=NIHAT+BAYRAM" />
</p>

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


