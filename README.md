# 😷 YOLO Generations Benchmark  
**Yüz Maskesi Tespiti Karşılaştırması: YOLOv8n • YOLOv10n • YOLO11n**

## 📖 Proje Özeti

Bu proje, Ultralytics'in en güncel hafif modelleri olan **YOLOv8n**, **YOLOv10n** ve **YOLO11n**'nin yüz maskesi tespiti performanslarını **aynı koşullar** altında karşılaştırmaktadır.

Tüm modeller şu parametrelerle eğitilmiştir:
- **Epoch**: 15
- **Görüntü Boyutu**: 320×320
- **Donanım**: Google Colab (Tesla T4 GPU)
- **Framework**: Ultralytics 8.3.249
- **Veri Seti**: 100 validasyon görüntüsü → 327 kutu (49 mask, 278 no_mask)

<br>

## 🚀 Performans Karşılaştırma Tablosu

| Model       | mAP50   | mAP50-95 | Parametre | GFLOPs | Inference (ms) | Ağırlık Boyutu | mask mAP50 | no_mask mAP50 | Öne Çıkan Özellik                          |
|-------------|---------|----------|-----------|--------|----------------|----------------|------------|---------------|--------------------------------------------|
| **YOLO11n** | 0.722   | 0.384    | 2.58M     | 6.3    | 2.6            | ~5.4 MB        | **0.585**  | 0.859         | **En iyi maske tespiti**                   |
| **YOLOv8n** | **0.723**| **0.389**| 3.01M     | 8.1    | **2.1**        | ~6.2 MB        | 0.605      | **0.840**     | **En yüksek genel doğruluk**               |
| **YOLO10n** | 0.637   | 0.338    | **2.27M** | 6.5    | **2.1**        | ~5.7 MB        | 0.488      | 0.786         | **En hafif & NMS-free**                    |

<br>

## 📊 Detaylı Model Analizleri

### 🥇 YOLO11n – En Yeni Nesil
En güncel mimari sayesinde küçük nesneleri (maske) daha iyi yakalar.

**Sınıf Metrikleri**  
- `mask` → Precision: 0.803 | Recall: 0.498 | **mAP50: 0.585**  
- `no_mask` → Precision: 0.877 | Recall: 0.809 | mAP50: 0.859

<p align="center">
  <img src="https://raw.githubusercontent.com/nihatbayramm/YoloMaskeTespitModeli/main/results_yolo11.png" width="450" alt="YOLO11 Sonuç"/>
  <img src="https://raw.githubusercontent.com/nihatbayramm/YoloMaskeTespitModeli/main/confusion_matrix_yolo11.png" width="370" alt="YOLO11 Confusion Matrix"/>
  <img width="1280" height="1280" alt="image" src="https://github.com/user-attachments/assets/4cac18bb-016e-4c76-9f2d-c7e235e586fa" />
</p>

### 🥈 YOLOv8n – Endüstri Standardı
Genel doğrulukta lider, özellikle maskesiz yüzleri çok güvenilir tespit eder.

**Sınıf Metrikleri**  
- `mask` → Precision: 0.779 | Recall: 0.574 | mAP50: 0.605  
- `no_mask` → Precision: 0.814 | Recall: 0.806 | **mAP50: 0.840**

<p align="center">
  <img src="https://raw.githubusercontent.com/nihatbayramm/YoloMaskeTespitModeli/main/results_v8.png" width="450" alt="YOLOv8 Sonuç"/>
  <img src="https://raw.githubusercontent.com/nihatbayramm/YoloMaskeTespitModeli/main/confusion_matrix_v8.png" width="370" alt="YOLOv8 Confusion Matrix"/>
</p>

### 🥉 YOLO10n – En Verimli
NMS gerektirmeyen yapısıyla en düşük parametre sayısı ve yüksek hız.

**Sınıf Metrikleri**  
- `mask` → Precision: 0.622 | Recall: 0.449 | mAP50: 0.488  
- `no_mask` → Precision: 0.693 | Recall: 0.809 | mAP50: 0.786

<p align="center">
  <img src="https://raw.githubusercontent.com/nihatbayramm/YoloMaskeTespitModeli/main/results_v10.png" width="450" alt="YOLO10 Sonuç"/>
  <img src="https://raw.githubusercontent.com/nihatbayramm/YoloMaskeTespitModeli/main/confusion_matrix_v10.png" width="370" alt="YOLO10 Confusion Matrix"/>
</p>

<br>

## ⚙️ Kurulum ve Kullanım

### 1️⃣ Gerekli Kütüphaneler
```
pip install ultralytics opencv-python
```
### 2️⃣ Model Eğitimi (CLI)

# YOLOv8n
yolo train model=yolov8n.pt data=mask_dataset.yaml epochs=15 imgsz=320

# YOLO10n
yolo train model=yolo10n.pt data=mask_dataset.yaml epochs=15 imgsz=320

# YOLO11n
yolo train model=yolo11n.pt data=mask_dataset.yaml epochs=15 imgsz=320


### 3️⃣ Tespit Yapma (Python)

```
from ultralytics import YOLO

# En iyi modeli yükleyin (örnek: YOLO11n)
model = YOLO("runs/detect/mask_train_yolo11/weights/best.pt")

# Tek görüntü testi
results = model("test_image.jpg")[0]
results.show()          # Görüntüyü ekranda göster
# results.save("sonuc.jpg")   # Dosyaya kaydetmek için

```
### 🏆 Sonuç Karşılaştırması

| Kategori         | Kazanan         | Açıklama |
|------------------|-----------------|---------|
| Genel Doğruluk   | **YOLOv8n**     | mAP50: **0.723** — Dengeli performans |
| Maske Tespiti    | **YOLO11n**     | mask sınıfı mAP50: **0.585** — Küçük nesnelerde güçlü |
| Hız & Hafiflik   | **YOLO10n / YOLOv8n** | ~**2.1 ms inference** — Mobil & edge cihazlar için ideal |

