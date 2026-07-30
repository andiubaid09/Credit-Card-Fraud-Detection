# 💳 Credit Card Fraud Detection Menggunakan Machine Learning

<p align="center">

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python)
![scikit-learn](https://img.shields.io/badge/scikit--learn-Machine%20Learning-orange?logo=scikitlearn)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-013243?logo=numpy)

</p>

---

# 💡 Tentang Project

Repository ini berisi implementasi dan perbandingan berbagai algoritma **Machine Learning** untuk mendeteksi transaksi **Credit Card Fraud**.

Fokus utama proyek ini bukan hanya membangun model klasifikasi, tetapi juga menerapkan workflow Machine Learning yang konsisten, menangani **imbalanced dataset**, melakukan **hyperparameter tuning**, serta membandingkan performa berbagai algoritma menggunakan proses preprocessing dan evaluasi yang sama.

Dengan pendekatan tersebut, setiap algoritma dapat dibandingkan secara objektif untuk mengetahui kelebihan dan kekurangannya pada permasalahan deteksi fraud.

---

# ✨ Highlights

- 📊 Dataset Credit Card Fraud dari Kaggle
- ⚖️ Penanganan Imbalanced Dataset (98.49% : 1.51%)
- 🔄 Pipeline Machine Learning menggunakan Scikit-Learn
- 🔁 Feature Engineering (Cyclical Encoding)
- ⚙️ StandardScaler
- 🧪 Perbandingan Baseline, Class Weight, dan SMOTE
- 🎯 Hyperparameter Tuning menggunakan GridSearchCV
- 📈 Evaluasi menggunakan berbagai metrik klasifikasi
- 📌 Analisis Feature Importance
- 🤖 Perbandingan berbagai algoritma Machine Learning

---

# ⭐ Fitur Repository

- ✅ Workflow Machine Learning End-to-End
- ✅ Eksperimen yang Reproducible
- ✅ Feature Engineering
- ✅ Penanganan Imbalanced Dataset
- ✅ Hyperparameter Optimization
- ✅ Model Tersimpan (.joblib)
- ✅ Dokumentasi Lengkap Setiap Algoritma
- ✅ Perbandingan Hasil Seluruh Model

---

# 📑 Daftar Isi

- [Dataset](#-dataset)
- [Struktur Repository](#-struktur-repository)
- [Workflow Machine Learning](#️-workflow-machine-learning)
- [Preprocessing](#-preprocessing)
- [Penanganan Imbalanced Dataset](#️-penanganan-imbalanced-dataset)
- [Model Machine Learning](#-model-machine-learning)
- [Ringkasan Hasil](#-ringkasan-hasil)
- [Dokumentasi](#-dokumentasi)
- [Pengembangan Selanjutnya](#-pengembangan-selanjutnya)

---

# 📊 Dataset

| Informasi | Nilai |
|-----------|-------|
| Sumber Dataset | Kaggle |
| Jumlah Data | 10.000 |
| Transaksi Normal | 9.849 |
| Transaksi Fraud | 151 |
| Rasio Kelas | 98.49% : 1.51% |

Dataset terdiri dari beberapa fitur transaksi, antara lain:

- Transaction ID
- Merchant Category
- Amount
- Transaction Hour
- Merchant Category
- Foreign Transaction
- Location Mismatch
- Device Trust Score
- Velocity Last 24 Hours
- Cardholder Age
- is_fraud

---

# 📁 Struktur Repository

```text
Credit-Card-Fraud-Detection/
│
├── docs/
|   ├── images/
│       ├── Confusion Matrix/
|           ├── cm AdaBoost.png
|           ├── cm Decision Tree.png
|           ├── cm Gradient Boosting.png
|           ├── cm K-Nearest Neighbor.png
|           ├── cm Logistic Regression.png
|           ├── cm Random Forest.png
|           └── cm Support Vector Machine.png
│       ├── Feature Importances/
|           ├── Top Feature AdaBoost.png
|           ├── Top Feature Decision Tree.png
|           ├── Top Feature Gradient Boosting.png
|           ├── Top Feature K-Nearest Neighbor.png
|           ├── Top Feature Logistic Regression.png
|           ├── Top Feature Random Forest.png
|           └── Top Feature Support Vector Machine.png
│   ├── results/
|       ├── AdaBoost.md
|       ├── dataset.md
|       ├── Decision_Tree.md
|       ├── evaluation.md
|       ├── Gradient_Boosting.md
│       ├── K_Nearest_Neighbor.md
|       ├── Logistic_Regression.md
|       ├── methodolgy.md
|       ├── Random_Forest.md
|       ├── Support_Vector_Machine.md
│
├── models/
|   ├── AdaBoost_Model.joblib
│   ├── Decision_Tree_Model.joblib
|   ├── Gradient_Boosting_Model.joblib
│   ├── K-Nearest_Neighbor.joblib
│   ├── Logistic_Regression_Model.joblib
│   ├── Random_Forest_Model.joblib
│   └── Support_Vector_Machine.joblib
|
├── notebooks/
│   ├── 01_Logistic_Regression_CCFD.ipynb
│   ├── 02_Decision_Tree_CCFD.ipynb
│   ├── 03_Random_Forest_CCFD.ipynb
│   ├── 04_Support_Vector_Machine.ipynb
│   ├── 05_K-Nearest_Neighbor.ipynb
|   ├── 06_AdaBoost_CCFD.ipynb
|   └── 07_Gradient_Boosting_CCFD.ipynb
│
├── requirements.txt
├── README.md
└── .gitignore
```

---

# ⚙️ Workflow Machine Learning

```
   Dataset
      │
      ▼
Feature Engineering
      │
      ▼
Train-Test Split
      │
      ▼
Data Preprocessing
      │
      ▼
Baseline Model
      │
      ▼
Penanganan Imbalanced Dataset
(Class Weight / SMOTE)
      │
      ▼
Hyperparameter Tuning
(GridSearchCV)
      │
      ▼
Evaluasi Model
      │
      ▼
Perbandingan Seluruh Model
```

Workflow tersebut diterapkan secara konsisten pada seluruh algoritma sehingga hasil eksperimen dapat dibandingkan secara adil.

---

# 🔄 Preprocessing

Tahapan preprocessing yang digunakan meliputi:

- Feature Engineering menggunakan **Cyclical Encoding**
- StandardScaler
- Train-Test Split menggunakan **Stratified Sampling**
- Pipeline Scikit-Learn

Fitur yang dilakukan scaling:

- Amount
- Device Trust Score
- Velocity Last 24 Hours
- Cardholder Age

Sedangkan fitur kategorikal dan biner tidak dilakukan proses scaling.

---

# ⚖️ Penanganan Imbalanced Dataset

Karena dataset memiliki distribusi kelas yang tidak seimbang, dilakukan tiga pendekatan berbeda.

| Pendekatan | Status |
|------------|:------:|
| Baseline | ✅ |
| Class Weight | ✅ |
| SMOTE | ✅ |

> **Catatan:** Tidak semua algoritma mendukung parameter `class_weight`, misalnya K-Nearest Neighbor, AdaBoost.

---

# 🤖 Model Machine Learning

| Model | Baseline | Class Weight | SMOTE | Tuning | Dokumentasi |
|---------|:--------:|:------------:|:-----:|:------:|------------|
| Logistic Regression | ✅ | ✅ | ✅ | ✅ | 📄 [Lihat Dokumentasi](docs/results/Logistic_Regression.md) |
| Decision Tree | ✅ | ✅ | ✅ | ✅ | 📄 [Lihat Dokumentasi](docs/results/Decision_Tree.md) |
| Random Forest | ✅ | ✅ | ✅ | ✅ | 📄 [Lihat Dokumentasi](docs/results/Random_Forest.md) |
| Support Vector Machine | ✅ | ✅ | ✅ | ✅ | 📄 [Lihat Dokumentasi](docs/results/Support_Vector_Machine.md) |
| K-Nearest Neighbor | ✅ | N/A | ✅ | ✅ | 📄 [Lihat Dokumentasi](docs/results/K-Nearest_Neighbor.md) |
| AdaBoost | ✅ | N/A | ✅ | ✅ |  📄 [Lihat Dokumentasi](docs/results/AdaBoost.md)|
| Gradient Boosting | ✅ | N/A | ✅ | ✅ | [Lihat Dokumentasi](docs/results/Gradient_Boosting.md) |
| Extra Trees | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |
| XGBoost | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |
| LightBGM | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |
| CatBoost | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |
| Gaussien Naive Bayes | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |
| Multi-Layer Perceptron | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |

---

# 🏆 Ringkasan Hasil

| Algoritma | Konfigurasi Terbaik | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------------|---------------------|---------:|----------:|-------:|---:|--------:|
| Logistic Regression | SMOTE + GridSearchCV | 96.20% | 28% | 100% | 44% | 99.32% |
| Decision Tree | Class Weight + GridSearchCV | 99.90% | 94% | 100% | 97% | 99.95% |
| Random Forest | SMOTE + GridSearchCV | 99.85% | 93.55% | 97% | 95% | 99.99% |
| Support Vector Machine | Class Weight + GridSearchCV | 99.10% | 65% | 86.67% | 74% | 99.49% |
| K-Nearest Neighbor | SMOTE + GridSearchCV | 98.10% | 43.10% | 83.33% | 57% | 95.82% |
| AdaBoost           | Baseline + GridSearchCV | 100% | 100% | 100% | 100% | 100% |
| Gradient Boosting  | SMOTE + GridSearchCV    | 99% | 93.75% | 100% | 97% | 99% |

> Dokumentasi lengkap setiap eksperimen dapat dilihat pada folder **results/**.

---

# 📚 Dokumentasi

## Dokumentasi Umum

| Dokumentasi | Deskripsi |
|-------------|-----------|
| [📂](docs/results/dataset.md) | Penjelasan dataset |
| [⚙️](docs/results/methodolgy.md) | Workflow Machine Learning |
| [📊](docs/results/evaluation.md) | Penjelasan metrik evaluasi |

---

## Hasil Eksperimen

| Model | Dokumentasi |
|--------|-------------|
| 📈 Logistic Regression | [Lihat Dokumentasi](docs/results/Logistic_Regression.md) |
| 🌳 Decision Tree | [Lihat Dokumentasi](docs/results/Decision_Tree.md) |
| 🌲 Random Forest | [Lihat Dokumentasi](docs/results/Random_Forest.md) |
| 🔵 Support Vector Machine | [Lihat Dokumentasi](docs/results/Support_Vector_Machine.md) |
| 👥 K-Nearest Neighbor | [Lihat Dokumentasi](docs/results/K-Nearest_Neighbor.md) |
| 🚀 AdaBoost  | [Lihat Dokumentasi](docs/results/AdaBoost.md)|
| 🚂 Gradient Boosting | [Lihat Dokumentasi](docs/results/Gradient_Boosting.md)

---

# 🚀 Pengembangan Selanjutnya

Repository ini akan terus dikembangkan dengan menambahkan beberapa algoritma Machine Learning lainnya.

- [ ] Extra Trees
- [ ] XGBoost
- [ ] LightBGM
- [ ] CatBoost
- [ ] Gaussien Naive Bayes
- [ ] Multi-Layer Perceptron

---

# 📚 Repository Terkait

Repository **Exploratory Data Analysis (EDA)** dapat diakses melalui:

https://github.com/andiubaid09/Exploratory-Data-Analysis/tree/main/Credit%20Card%20Fraud

---

# 🛠️ Library

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-Learn
- Imbalanced-Learn
- Joblib

---

# 👨‍💻 Author

**Muhammad Andi Ubaidillah**

GitHub:
https://github.com/andiubaid09