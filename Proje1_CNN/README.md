# CNN Sınıflandırma Projesi

## 📋 Proje Açıklaması

Bu proje, kendi verisetimiz üzerinde üç farklı CNN (Convolutional Neural Network) modeli geliştirerek görsel sınıflandırma problemi çözmektedir. Projede Transfer Learning, Basit CNN ve Hiperparametre Optimizasyonu teknikleri uygulanmıştır.

---

## 📁 Proje Yapısı

```
Proje1_CNN/
├── README.md                 # Proje açıklaması
├── model1.ipynb             # Transfer Learning (VGG16)
├── model2.ipynb             # Basit CNN Mimarisi
├── model3.ipynb             # Hiperparametre Optimizasyonu
└── dataset/
    ├── sinif1/              # Sınıf 1 görüntüleri
    └── sinif2/              # Sınıf 2 görüntüleri
```

---

## 🎯 Proje Hedefleri

1. **Model1:** Transfer Learning kullanarak veri çeşitliliği az olsa bile yüksek doğruluk elde etmek
2. **Model2:** Sıfırdan bir CNN oluşturarak basit bir mimari ile öğrenmeyi anlamak
3. **Model3:** Hiperparametreleri optimize edererek model performansını artırmak

---

## 📊 Model Açıklamaları

### Model 1: Transfer Learning (VGG16)

**Teknik:** Transfer Learning + Fine-tuning

**Mimari:**
```
ImageNet eğitilmiş VGG16 (donmuş katmanlar)
        ↓
    Flatten (128×128×3 → vektor)
        ↓
    Dense(256, ReLU)
        ↓
    Dropout(0.5)
        ↓
    Dense(num_classes, Softmax)
```

**Avantajları:**
- ImageNet'teki genel özellikleri kullanır
- Az veriyle hızlı eğitim
- Genellikle en yüksek doğruluk

**Parametreler:**
- Epochs: 10
- Batch Size: 32
- Optimizer: Adam
- Loss: Categorical Crossentropy

---

### Model 2: Basit CNN

**Teknik:** Sıfırdan CNN mimarisi (no transfer learning)

**Mimari:**
```
Input(128×128×3)
    ↓
Conv2D(32) → MaxPool → Dropout(0.25)
    ↓
Conv2D(64) → MaxPool → Dropout(0.25)
    ↓
Conv2D(128) → MaxPool → Dropout(0.25)
    ↓
Flatten → Dense(512, ReLU) → Dropout(0.5) → Output
```

**Özellikler:**
- Tüm katmanlar sıfırdan eğitilir
- Verisetine özel özellikler öğrenir
- Daha fazla eğitim süresi gerektirebilir

**Parametreler:**
- Epochs: 20
- Batch Size: 32
- Optimizer: Adam
- Loss: Categorical Crossentropy

---

### Model 3: Hiperparametre Optimizasyonu

**Teknik:** Farklı konfigürasyonlarla 6 deney

**Deneyler:**
1. **Baseline:** Model2 konfigürasyonu
2. **Batch Size Artışı:** 32 → 64
3. **Learning Rate Azalması:** 0.001 → 0.0005
4. **Dropout Artışı:** 0.25 → 0.4
5. **Data Augmentation:** Rotation, Shift, Flip
6. **Kombinasyon:** Batch↑ + Dropout↑ + Aug

**Data Augmentation Parametreleri:**
```python
rotation_range=15        # ±15° döndürme
width_shift_range=0.1    # ±10% yatay kaydırma
height_shift_range=0.1   # ±10% dikey kaydırma
horizontal_flip=True     # Yatay çevirme
```

**Beklentiler:**
- Data augmentation aşırı uydurmayı azaltır
- Batch size değişimi stabiliteyi etkileyebilir
- Dropout artışı genelleştirmeyi iyileştirebilir
- Kombinasyon en iyi sonuçları verebilir

---

## 📈 Beklenen Sonuçlar

### Model Karşılaştırması

| Aspect | Model1 | Model2 | Model3 |
|--------|--------|--------|--------|
| **Hız** | Hızlı | Yavaş | Orta-Hızlı |
| **Doğruluk** | Yüksek | Orta | Değişken |
| **Veri Talebı** | Düşük | Yüksek | Orta |
| **Eğitim Süresi** | Kısa | Uzun | Orta |

**Genel Tahmin:**
- **Model1** genellikle en yüksek doğruluk
- **Model3** verisetine bağlı olarak Model1'i geçebilir
- **Model2** baseline olarak işlev görür

---

## 📸 Veri Seti Hazırlığı

### Gereksinimler:
- **Sınıf Sayısı:** 2 (en az)
- **Görsel Sayısı:** Her sınıf için en az 50 (toplam 100+)
- **Görsel Boyutu:** Minimum 64×64, tercih edilen 128×128
- **Çeşitlilik:** Farklı açı, ışık, arka plan

### Dataset Yapısı:
```
dataset/
├── sinif1/
│   ├── img001.jpg
│   ├── img002.jpg
│   └── ...
└── sinif2/
    ├── img001.jpg
    ├── img002.jpg
    └── ...
```

### Veri Önişleme:
- Rescaling: 1/255 (0-1 aralığına normalize)
- Validation Split: 20%
- Image Size: 128×128 (tüm görseller)

---

## 🚀 Çalıştırma

### Gerekli Kütüphaneler:
```bash
pip install tensorflow keras matplotlib pandas numpy
```

### Çalıştırma Adımları:

1. **Fotoları Ekleyin:**
   ```
   dataset/sinif1/ ve dataset/sinif2/ klasörlerine fotoları kopyalayın
   ```

2. **Model1 Çalıştırın:**
   ```
   Jupyter Notebook'de model1.ipynb → Run All
   ```

3. **Model2 Çalıştırın:**
   ```
   Jupyter Notebook'de model2.ipynb → Run All
   ```

4. **Model3 Çalıştırın:**
   ```
   Jupyter Notebook'de model3.ipynb → Run All
   Grafikler ve karşılaştırma tablosunu inceleyiniz
   ```

---

## 📝 Önemli Notlar

### Transfer Learning vs. Sıfırdan Eğitim
- **Transfer Learning (Model1):** ImageNet'teki genel özelliklerden yararlanır
- **Sıfırdan Eğitim (Model2):** Verisetine özel özellikler öğrenir

### Aşırı Uydurmayı (Overfitting) Azaltma Teknikleri
1. **Dropout:** Rastgele nöronları devre dışı bırakma
2. **Data Augmentation:** Eğitim setini çeşitlendirme
3. **Batch Normalization:** (opsiyonel) Katman çıktılarını normalize etme
4. **Early Stopping:** (opsiyonel) Doğrulama doğruluğu düştüğünde durdurma

### Hiperparametre Tuning
```
Best Practices:
- Bir parametre bir seferde değiştir
- Her deneyden sonra sonuçları kaydet
- Deneylerin sayısı çok olsa iyi olur (5-10+)
- Random seed ayarla tekrarlanabilirlik için
```

---

## 📊 Sonuç Analizi

Modeller eğitildikten sonra:

1. **Grafikleri İnceleyiniz:**
   - Doğruluk ve kayıp eğrileri
   - Eğitim vs. doğrulama farkı
   - Aşırı uydurmayı kontrol et

2. **Karşılaştırma Tablosunu Analiz Edin:**
   - Hangi hiperparametre en etkili?
   - Model3 vs. Model1 farkı nedir?
   - Neden böyle sonuçlar çıktı?

3. **Sorulara Cevap Verin:**
   - Transfer Learning neden avantajlı?
   - Data Augmentation etkisi nedir?
   - Batch size artışı neden önemli?

---

## 🎓 Eğitim Çıkarımları

Bu proje sayesinde şunları öğreneceksiniz:

✓ CNN mimarilerinin temel prensipleri  
✓ Transfer Learning ve fine-tuning  
✓ Hiperparametre optimizasyonu  
✓ Data augmentation teknikleri  
✓ Model karşılaştırması ve analizi  
✓ Overftting / Underfitting anlamı  

---

## 🔍 Gelecek İyileştirmeler

Proje geliştirildikçe şunlar yapılabilir:

1. **Daha İyi Mimariler:** ResNet50, EfficientNet, Inception
2. **Learning Rate Scheduling:** Epoch'lar arttıkça learning rate azalt
3. **Early Stopping:** Doğrulama doğruluğu düştüğünde durdur
4. **Class Weights:** Dengesiz verisetleri için ağırlık atama
5. **K-Fold Cross Validation:** Daha güvenilir sonuçlar için
6. **Model Ensemble:** Birden fazla modeli birleştir

---

## 📚 Kaynaklar

- [Keras Documentation](https://keras.io/)
- [TensorFlow Transfer Learning](https://www.tensorflow.org/tutorials/images/transfer_learning)
- [VGG Paper](https://arxiv.org/abs/1409.1556)
- [CNN Visualization](https://distill.pub/2019/computing-receptive-fields/)

---

## ✍️ Yazar Bilgileri

**Adı:** [ADINI YAZ]  
**Soyadı:** [SOYADINI YAZ]  
**Okul Numarası:** [NUMARANI YAZ]  
**GitHub:** https://github.com/kullanici_adi/CNN_siniflandirma

---

## 📄 Lisans

Bu proje eğitim amaçlı olarak hazırlanmıştır.

---

**Son Güncelleme:** Aralık 2025
