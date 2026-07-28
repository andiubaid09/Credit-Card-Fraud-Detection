# ⚙️ Methodology

## 📖 Overview

Seluruh algoritma Machine Learning pada proyek ini menggunakan workflow yang konsisten agar setiap model dapat dibandingkan secara objektif. Perbedaan setiap eksperimen hanya terletak pada algoritma yang digunakan serta proses hyperparameter tuning.

---

# 🔄 Workflow

```text
Dataset
    │
    ▼
Data Understanding
    │
    ▼
Feature Engineering
(Cyclical Encoding)
    │
    ▼
Train-Test Split
(Stratify)
    │
    ▼
Data Preprocessing
(StandardScaler)
    │
    ▼
Baseline Model
    │
    ▼
Handle Imbalanced Dataset
├── Class Weight*
└── SMOTE
    │
    ▼
Hyperparameter Tuning
(GridSearchCV)
    │
    ▼
Model Evaluation
```

> **Note:** Tidak semua algoritma mendukung `class_weight`. Sebagai contoh, K-Nearest Neighbor (KNN) tidak memiliki parameter tersebut sehingga hanya menggunakan Baseline, SMOTE, dan Hyperparameter Tuning.

---

# 📂 Dataset

Dataset yang digunakan merupakan dataset **Credit Card Fraud Detection** yang berisi transaksi kartu kredit dengan dua kelas.

| Keterangan | Nilai |
|------------|--------|
| Jumlah Data | 10.000 |
| Jumlah Fitur | 10 |
| Target | Fraud / Normal |
| Jenis Masalah | Binary Classification |

Distribusi kelas:

| Class | Total |
|--------|------:|
| Normal | 9.849 |
| Fraud | 151 |

Dataset memiliki distribusi yang sangat tidak seimbang sehingga diperlukan teknik penanganan imbalanced dataset.

---

# 🧹 Data Preprocessing

Tahapan preprocessing diterapkan secara konsisten pada seluruh algoritma.

---

## Feature Engineering

Fitur waktu transaksi (`transaction_hour`) ditransformasikan menggunakan **Cyclical Encoding** menjadi dua fitur baru.

- hour_sin
- hour_cos

Transformasi dilakukan karena waktu bersifat siklik sehingga pukul **23.00** dan **00.00** memiliki kedekatan secara matematis.

Rumus yang digunakan:

```python
hour_sin = np.sin(2 * np.pi * transaction_hour / 24)
hour_cos = np.cos(2 * np.pi * transaction_hour / 24)
```

---

## StandardScaler

Normalisasi hanya diterapkan pada fitur numerik.

| Feature |
|----------|
| Amount |
| Device Trust Score |
| Velocity Last 24 Hours |
| Cardholder Age |

Sedangkan fitur biner seperti berikut tidak dilakukan scaling.

- foreign_transaction
- location_mismatch

Preprocessing dibangun menggunakan **ColumnTransformer** sehingga seluruh eksperimen menggunakan pipeline yang konsisten.

---

# ✂️ Train-Test Split

Data dibagi menggunakan stratified sampling agar proporsi kelas tetap terjaga.

| Parameter | Nilai |
|-----------|--------|
| Train Size | 80% |
| Test Size | 20% |
| Stratify | Yes |
| Random State | 42 |

---

# ⚖️ Handling Imbalanced Dataset

Karena jumlah transaksi fraud jauh lebih sedikit dibanding transaksi normal, dilakukan beberapa pendekatan untuk mengatasi ketidakseimbangan data.

## 1. Baseline

Model dilatih menggunakan distribusi data asli tanpa penanganan kelas minoritas.

---

## 2. Class Weight

Beberapa algoritma mendukung parameter `class_weight='balanced'`.

Pendekatan ini memberikan bobot lebih besar kepada kelas fraud sehingga model memberikan perhatian lebih terhadap kelas minoritas.

Algoritma yang mendukung pendekatan ini antara lain:

- Logistic Regression
- Decision Tree
- Random Forest
- Support Vector Machine

---

## 3. SMOTE

SMOTE (*Synthetic Minority Over-sampling Technique*) digunakan untuk menghasilkan sampel sintetis pada kelas fraud sehingga distribusi data menjadi lebih seimbang.

SMOTE hanya diterapkan pada data latih melalui **imblearn Pipeline** untuk menghindari data leakage.

---

# 🔍 Hyperparameter Tuning

Setelah memperoleh model terbaik dari tahap sebelumnya, dilakukan optimasi hyperparameter menggunakan **GridSearchCV**.

Konfigurasi umum:

| Parameter | Nilai |
|-----------|--------|
| Cross Validation | 5-Fold |
| CV | 5 |
| Parallel Processing | n_jobs = -1 |

Parameter yang diuji berbeda pada setiap algoritma dan dijelaskan pada dokumentasi masing-masing model.

---

# 📊 Evaluation Metrics

Seluruh model dievaluasi menggunakan metrik berikut.

| Metric | Deskripsi |
|---------|-----------|
| Accuracy | Persentase prediksi yang benar terhadap seluruh data uji. |
| Precision | Proporsi transaksi yang diprediksi fraud dan benar-benar fraud. |
| Recall | Kemampuan model mendeteksi seluruh transaksi fraud. |
| F1-Score | Rata-rata harmonik antara Precision dan Recall. |
| ROC-AUC | Kemampuan model membedakan kelas fraud dan normal pada berbagai threshold. |

Karena dataset bersifat tidak seimbang (*imbalanced dataset*), metrik **Precision**, **Recall**, **F1-Score**, dan **ROC-AUC** menjadi perhatian utama dibandingkan hanya menggunakan Accuracy.

---

# 📌 Feature Importance

Interpretasi model dilakukan menggunakan metode yang sesuai dengan karakteristik masing-masing algoritma.

| Algorithm | Interpretation Method |
|------------|----------------------|
| Logistic Regression | Feature Coefficients |
| Decision Tree | Feature Importance |
| Random Forest | Feature Importance |
| Support Vector Machine | Permutation Importance |
| K-Nearest Neighbor | Permutation Importance |
| XGBoost | Feature Importance & SHAP |
| LightGBM | Feature Importance & SHAP |
| CatBoost | Feature Importance & SHAP |

Pendekatan ini digunakan untuk mengetahui fitur yang paling berkontribusi terhadap proses klasifikasi transaksi fraud.

---

# 📁 Experiment Workflow

Setiap algoritma mengikuti tahapan eksperimen berikut.

1. Melatih model baseline.
2. Menerapkan teknik penanganan imbalanced dataset (Class Weight atau SMOTE).
3. Membandingkan performa seluruh pendekatan.
4. Memilih model terbaik.
5. Melakukan Hyperparameter Tuning menggunakan GridSearchCV.
6. Mengevaluasi model menggunakan berbagai metrik klasifikasi.
7. Menganalisis Confusion Matrix.
8. Menginterpretasikan Feature Importance atau metode interpretasi lain yang sesuai.
9. Menentukan model terbaik berdasarkan hasil eksperimen.

Seluruh proses dilakukan menggunakan workflow yang konsisten sehingga performa setiap algoritma dapat dibandingkan secara objektif.