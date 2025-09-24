# 🌍 Intel Image Classification – CNN + Transfer Learning

Bu proje, **Akbank Derin Öğrenme Bootcamp** kapsamında hazırlanmıştır. Amacı, doğal ve yapay ortamları sınıflandırmak ve modern derin öğrenme yöntemlerini uygulamaktır.

---

## 🎯 Projenin Amacı
Bilgisayarla görü (Computer Vision) teknikleri kullanarak **Intel Image Classification** veri setindeki resimleri doğru sınıflandırmak hedeflenmiştir.

Bu proje ile:
- Derin öğrenme tabanlı CNN modeli sıfırdan eğitilmiş,
- Transfer Learning yaklaşımıyla VGG16 modeli kullanılmış,
- Model performansları karşılaştırılmıştır.

---

## 📂 Veri Seti
- **Kaynak**: [Intel Image Classification – Kaggle](https://www.kaggle.com/datasets/puneet6060/intel-image-classification)
- **İçerik**:
  - ~25.000 eğitim görseli
  - ~14.000 test görseli
  - Toplam **6 sınıf**:
    - **Buildings**
    - **Forest**
    - **Glacier**
    - **Mountain**
    - **Sea**
    - **Street**

### Veri Seti Klasör Yapısı
```plaintext
📂 intel-image-classification
├── 📂 seg_train
│   ├── 📂 buildings
│   ├── 📂 forest
│   ├── 📂 glacier
│   ├── 📂 mountain
│   ├── 📂 sea
│   └── 📂 street
├── 📂 seg_test
│   ├── 📂 buildings
│   ├── 📂 forest
│   ├── 📂 glacier
│   ├── 📂 mountain
│   ├── 📂 sea
│   └── 📂 street
```

---

## 🧹 Veri Önişleme & Data Augmentation
- Görüntüler **150x150 px** boyutuna dönüştürüldü.  
- Normalizasyon (0-1 arası ölçekleme).
- Eğitim setinde uygulanan işlemler:
  - Döndürme (rotation)  
  - Zoom  
  - Yatay çevirme (Horizontal Flip)  
  - Width/Height Shift

---

## 🏗️ Kullanılan Yöntemler

### 1. Baseline CNN Modeli
- 3 Convolutional Layer + MaxPooling Katmanı 
- Fully Connected Dense Layer  
- Dropout (%50)  
- Aktivasyon: ReLU + Softmax  
- Kayıp Fonksiyonu: **Categorical Crossentropy**  
- Optimizasyon: **Adam**  

---

### 3. Transfer Learning – VGG16
- ImageNet ağırlıkları kullanıldı.
- Üst katmanlar donduruldu.
- Eklenen katmanlar:
  - Flatten
  - Dense (256, ReLU)
  - Dropout (%50)
  - Dense (6, Softmax)

### 4. Callback Mekanizmaları
- **TensorBoard** ile görselleştirme
- **Weights & Biases (W&B)** ile metrik kaydı
- **ModelCheckpoint** ile model kaydı


## 📊 Elde Edilen Sonuçlar

### CNN Baseline
- Eğitim doğruluğu: ~**%80.7**
- Doğrulama doğruluğu: ~**%82.8**
- Test doğruluğu: ~**%86**
- CNN modeli başlangıç için yeterli performans sağlamış, fakat sınırlı genelleme göstermiştir. Özellikle bazı sınıflarda (ör. mountain, glacier) performans diğerlerine göre düşük kalmıştır.

### VGG16 Transfer Learning
- Eğitim doğruluğu: ~**%82.6**
- Doğrulama doğruluğu: ~**%84.8**
- Test doğruluğu: ~**%87**
- Transfer Learning, CNN baseline modeline kıyasla +1% test doğruluğu artışı sağlamış ve genelleme kabiliyeti daha yüksek olmuştur. Özellikle forest, street, buildings sınıflarında daha iyi sonuçlar elde edilmiştir.

---

## 🔥 Grad-CAM Görselleştirme
Modelin karar verirken odaklandığı bölgeleri göstermek için Grad-CAM yöntemi kullanılmıştır.  

Örnek: Glacier sınıfı için modelin buzluk alanlara odaklandığı görülmüştür.  

---

## ✅ Sonuçlar
- Transfer Learning, sınırlı eğitim verisine sahip senaryolarda bile CNN’e kıyasla daha yüksek başarı sağlamıştır.
- VGG16 modeli, farklı sınıflar arasında daha iyi genelleme yapmıştır.
- Proje, **Data Augmentation + Transfer Learning** stratejisinin güçlü bir örneğidir. 

| Model                 | Test Accuracy| Önemli Notlar |
|-----------------------|--------------|---------------|
| CNN (Baseline)        | %86          | Sıfırdan eğitildi |
| VGG16 TransferLearning| %87          | Daha stabil, genelleme gücü yüksek |

---

## 🚀 Kullanılan Araçlar
- TensorFlow / Keras  
- Weights & Biases (W&B)  
- Matplotlib, Seaborn  
- Scikit-learn (classification_report, confusion matrix)  
- Grad-CAM  

---

## 📌 Kaggle Notebook
📎 [Projeyi Kaggle’da İncele](https://www.kaggle.com/code/semateksen/intel-cnn-semateksen)  
