# Klasifikasi Kematangan Buah Sawit

**Binary Image Classification menggunakan Deep Learning (CNN) dengan pendekatan Transfer Learning**

---

## Deskripsi Proyek

Proyek ini merupakan bagian dari **Capstone Project kategori AI Engineer** yang bertujuan untuk membangun model **klasifikasi kematangan buah sawit berbasis citra digital**. Model melakukan klasifikasi ke dalam dua kelas utama:

* **Matang**
* **Mentah** (gabungan kelas Mentah dan Mangkel)

Model dikembangkan menggunakan **TensorFlow & Keras** dengan pendekatan **Transfer Learning** berbasis **MobileNetV2**, serta dirancang menggunakan pipeline yang terstruktur dan profesional sehingga siap untuk pengembangan lanjutan maupun tahap deployment.

---

## Dataset

Dataset yang digunakan merupakan dataset publik dari Roboflow.

**Sumber Dataset:**
[https://universe.roboflow.com/klasifikasi-testing/klasifikasi-kematangan-sawit/dataset/1](https://universe.roboflow.com/klasifikasi-testing/klasifikasi-kematangan-sawit/dataset/1)

### Distribusi Dataset

| Split      | Jumlah Gambar |
| ---------- | ------------- |
| Train      | 1020          |
| Validation | 97            |
| Test       | 49            |

### Distribusi Kelas

| Kelas  | Train | Valid | Test |
| ------ | ----- | ----- | ---- |
| Matang | 378   | 44    | 13   |
| Mentah | 642   | 53    | 36   |

---

## Preprocessing & Augmentasi

Dataset melalui beberapa tahapan preprocessing dan augmentasi untuk meningkatkan generalisasi model, meliputi:

* Auto-orient
* Resize ke **224 × 224**
* Normalisasi pixel ke rentang **0–1**

**Augmentasi data:**

* Horizontal & Vertical Flip
* Rotasi acak ±15°
* Rotasi 90° (Clockwise, Counter-Clockwise, Upside Down)
* Random Crop
* Brightness Adjustment (±25%)

---

## Pipeline Pengembangan Model

Pengembangan model dilakukan secara bertahap menggunakan pipeline berikut:

1. Data Understanding
2. Dataset Preparation & Preprocessing
3. Dataset Validation & Sanity Check
4. Model Building (Transfer Learning)
5. Model Training
6. Model Evaluation
7. Model Saving & Class Mapping
8. Inference Pipeline

### Visualisasi Pipeline

<img width="2752" height="1536" alt="Gemini_Generated_Image_1vqnic1vqnic1vqn" src="https://github.com/user-attachments/assets/3dab4d8b-bea3-4f12-8e62-36fd8cb7a450" />

---

## Arsitektur Model

Model menggunakan **MobileNetV2** sebagai feature extractor dengan konfigurasi sebagai berikut:

* Input Shape: `(224, 224, 3)`
* Global Average Pooling
* Batch Normalization
* Dropout
* Dense Output Layer (Activation: Sigmoid)

**Ringkasan parameter:**

* Total parameter: ±2.26 juta
* Trainable parameter (baseline): ±3.8 ribu

---

## Hasil Training

* Optimizer: **Adam**
* Loss Function: **Binary Crossentropy**
* Callback yang digunakan:

  * EarlyStopping
  * ReduceLROnPlateau
  * ModelCheckpoint

Model terbaik dipilih dan disimpan berdasarkan **validation loss terendah**.

---

## Evaluasi Model

Evaluasi dilakukan menggunakan **Test Set** yang tidak pernah digunakan selama proses training.

### Hasil Evaluasi

| Metric    | Nilai      |
| --------- | ---------- |
| Accuracy  | **91.84%** |
| Precision | **97.06%** |
| Recall    | **91.67%** |
| Loss      | **0.2119** |

### Classification Report

| Class  | Precision | Recall | F1-Score |
| ------ | --------- | ------ | -------- |
| Matang | 0.80      | 0.92   | 0.86     |
| Mentah | 0.97      | 0.92   | 0.94     |

---

## Visualisasi Evaluasi Model

<img width="558" height="490" alt="image" src="https://github.com/user-attachments/assets/d0fc8f7e-4ef2-4f03-9b54-072d192fab4a" />

<img width="590" height="490" alt="image" src="https://github.com/user-attachments/assets/00881f66-88ef-4348-938b-42405e18bf05" />

<img width="1189" height="490" alt="image" src="https://github.com/user-attachments/assets/6bbe0843-4301-4493-8612-3867af76b1e1" />

---

## Inference Pipeline

Model dapat digunakan untuk melakukan inferensi pada gambar baru dengan alur sebagai berikut:

1. Load model `.keras`
2. Load `class_mapping.json`
3. Preprocessing image
4. Prediction
5. Output label dan confidence score

**Class mapping** disimpan dalam format JSON untuk menjaga konsistensi label:

```json
{
  "0": "Matang",
  "1": "Mentah"
}
```

