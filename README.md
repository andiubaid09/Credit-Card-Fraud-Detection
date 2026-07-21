# 💳 Credit Card Fraud Detection using Machine Learning

<p align="center">

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python)
![scikit-learn](https://img.shields.io/badge/scikit--learn-Machine%20Learning-orange?logo=scikitlearn)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-013243?logo=numpy)

</p>

---

# 💡 Tentang Project

Repository ini berisi implementasi dan perbandingan berbagai algoritma **Machine Learning** untuk mendeteksi transaksi **Credit Card Fraud**. Fokus utama project ini bukan hanya membangun model klasifikasi, tetapi juga mengevaluasi berbagai teknik penanganan **imbalanced dataset**, melakukan **hyperparameter tuning**, serta membandingkan performa beberapa algoritma menggunakan workflow yang konsisten. Seluruh model menggunakan preprocessing dan metode evaluasi yang sama sehingga hasil eksperimen dapat dibandingkan secara objektif.

---

# ✨ Highlights

- 📊 Dataset Credit Card Fraud dari Kaggle
- ⚖️ Menangani **Imbalanced Dataset (98.49% vs 1.51%)**
- 🔄 Pipeline Machine Learning menggunakan Scikit-Learn
- 🔁 Feature Engineering (Cyclical Encoding)
- ⚙️ StandardScaler
- 🧪 Baseline vs Class Weight vs SMOTE
- 🎯 Hyperparameter Tuning menggunakan GridSearchCV
- 📈 Evaluasi menggunakan berbagai metrik klasifikasi
- 📊 Visualisasi Confusion Matrix
- 📌 Analisis Feature Importance
- 🤖 Perbandingan berbagai algoritma Machine Learning

---

# 📑 Daftar Isi

- [Dataset](#-dataset)
- [Struktur Repository](#-struktur-repository)
- [Workflow Machine Learning](#-workflow-machine-learning)
- [Preprocessing](#-preprocessing)
- [Penanganan Imbalanced Dataset](#-penanganan-imbalanced-dataset)
- [Model Machine Learning](#-model-machine-learning)
- [Metrik Evaluasi](#-metrik-evaluasi)
- [Hasil Eksperimen](#-hasil-eksperimen)
- [Visualisasi](#-visualisasi)
- [Kesimpulan](#-kesimpulan)
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
├── notebooks/
│   ├── Logistic Regression.ipynb
│   ├── Decision Tree.ipynb
│   ├── Random Forest.ipynb
│   ├── Support Vector Machine.ipynb
│   ├── XGBoost.ipynb
│   ├── LightGBM.ipynb
│   └── K-Nearest Neighbor.ipynb
│
├── docs/
│   └── images/
│       ├── workflow.png
│       ├── confusion_matrix/
│       ├── feature_importance/
│       └── comparison/
│
├── requirements.txt
├── .gitignore
└── README.md
```

---

# ⚙️ Workflow Machine Learning

Workflow yang digunakan pada setiap model adalah sebagai berikut.

```
                 💳 Credit Card Fraud Detection Workflow

┌────────────┐
│ Dataset    │
└────────────┘
       │
       ▼
┌──────────────────────┐
│ Feature Engineering  │
└──────────────────────┘
       │
       ▼
┌──────────────────────┐
│ Train-Test Split     │
└──────────────────────┘
       │
       ▼
┌──────────────────────┐
│ Data Preprocessing   │
└──────────────────────┘
       │
       ▼
┌──────────────────────┐
│ Baseline Model        │
└──────────────────────┘
       │
       ▼
┌────────────────────────────────────┐
│ Handle Imbalanced Dataset          │
│  • Class Weight                    │
│  • SMOTE                           │
└────────────────────────────────────┘
       │
       ▼
┌──────────────────────┐
│ Hyperparameter Tuning│
└──────────────────────┘
       │
       ▼
┌──────────────────────┐
│ Model Evaluation     │
└──────────────────────┘
       │
       ▼
┌──────────────────────┐
│ Compare All Models   │
└──────────────────────┘
```

Workflow tersebut diterapkan secara konsisten pada seluruh algoritma sehingga setiap model dapat dibandingkan secara adil.

---

# 🔄 Preprocessing

Tahapan preprocessing yang digunakan:

- Feature Engineering menggunakan **Cyclical Encoding** pada fitur `transaction_hour`
- StandardScaler untuk fitur numerik
- Train-Test Split menggunakan `stratify`
- Pipeline Scikit-Learn

Fitur yang dilakukan scaling:

- Amount
- Device Trust Score
- Velocity Last 24 Hours
- Cardholder Age

Fitur biner tidak dilakukan scaling.

---

# ⚖️ Penanganan Imbalanced Dataset

Karena dataset memiliki distribusi kelas yang tidak seimbang, dilakukan tiga pendekatan berbeda.

| Pendekatan | Status |
|------------|:------:|
| Baseline | ✅ |
| Class Weight | ✅ |
| SMOTE | ✅ |

---

# 🤖 Model Machine Learning

| Model | Baseline | SMOTE | Tuning | Status |
|---------|:--------:|:-----:|:------:|:------:|
| Logistic Regression | ✅ | ✅ | ✅ | ✅ |
| Decision Tree | ⏳ | ⏳ | ⏳ | Coming Soon |
| Random Forest | ⏳ | ⏳ | ⏳ | Coming Soon |
| Support Vector Machine | ⏳ | ⏳ | ⏳ | Coming Soon |
| XGBoost | ⏳ | ⏳ | ⏳ | Coming Soon |
| LightGBM | ⏳ | ⏳ | ⏳ | Coming Soon |
| K-Nearest Neighbor | ⏳ | ⏳ | ⏳ | Coming Soon |

---

# 📈 Metrik Evaluasi

Model dievaluasi menggunakan:

- Accuracy
- Precision
- Recall
- F1-Score
- ROC-AUC Score
- Confusion Matrix

---

# 🏆 Hasil Eksperimen

## Logistic Regression

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 98.95% | 71%     | 50%    | 59% | 99.33% |
| Class Weight | 95.20% | 24% | 100% | 38% | 99.33% |
| SMOTE     | 96%    | 27%   | 100%   | 43%   | 99.33% |
| SMOTE + GridSearchCV | 96.20% | 28% | 100% | 44% | 99.32% |

---

# 📊 Visualisasi

## Confusion Matrix

<p align="center">
<img src="docs/images/Confusion Matrix/cm_logistic_regression.png" width="550">
</p>

---

## Feature Importance

<p align="center">
<img src="docs/images/Feature Importances/Top Feature Logistic Regression.png" width="700">
</p>

---

# 💡 Kesimpulan

Eksperimen menunjukkan bahwa:

- Logistic Regression baseline memiliki precision tertinggi (**0.71**) namun hanya mampu mendeteksi **50%** transaksi fraud.
- Penerapan **SMOTE** meningkatkan recall menjadi **100%**, sehingga seluruh transaksi fraud berhasil dideteksi.
- Hyperparameter tuning menggunakan **GridSearchCV** memberikan peningkatan kecil pada Accuracy dan F1-Score dibandingkan SMOTE tanpa tuning.
- Nilai **ROC-AUC sekitar 0.993** menunjukkan bahwa Logistic Regression memiliki kemampuan yang sangat baik dalam membedakan transaksi normal dan fraud.

---

# 🚀 Pengembangan Selanjutnya

Repository ini akan terus dikembangkan dengan menambahkan berbagai algoritma Machine Learning lainnya.

- [ ] Decision Tree
- [ ] Random Forest
- [ ] Support Vector Machine
- [ ] XGBoost
- [ ] LightGBM
- [ ] K-Nearest Neighbor
- [ ] Perbandingan seluruh model
- [ ] ROC Curve Comparison
- [ ] SHAP Explainability

---

# 📚 Repository Terkait

Repository ini berfokus pada pembangunan model Machine Learning.

Repository Exploratory Data Analysis (EDA):

> https://www.kaggle.com/datasets/miadul/credit-card-fraud-detection-dataset

---

# 🛠️ Library

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-Learn
- Imbalanced-Learn

---

# 👨‍💻 Author

**Muhammad Andi Ubaidillah**

GitHub: https://github.com/andiubaid09
