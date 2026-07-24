# 💳 Credit Card Fraud Detection using Machine Learning

<p align="center">

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python)
![scikit-learn](https://img.shields.io/badge/scikit--learn-Machine%20Learning-orange?logo=scikitlearn)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-013243?logo=numpy)

</p>

---

# 💡 Tentang Project

Repository ini berisi implementasi dan perbandingan berbagai algoritma **Machine Learning** untuk mendeteksi transaksi **Credit Card Fraud**. Fokus utama project ini bukan hanya membangun model klasifikasi, tetapi juga mengevaluasi berbagai teknik penanganan **imbalanced dataset**, melakukan **hyperparameter tuning**, serta membandingkan performa beberapa algoritma menggunakan workflow yang konsisten. Seluruh model menggunakan preprocessing dan metode evaluasi yang sama sehingga hasil eksperimen dapat dibandingkan secara objektif.

---

# ✨ Highlights

- 📊 Dataset Credit Card Fraud dari Kaggle (https://www.kaggle.com/datasets/miadul/credit-card-fraud-detection-dataset)
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
│   ├── 01_Logistic_Tree_CCFD.ipynb
│   ├── 02_Decision_Tree_CCFD.ipynb
│   ├── 03_Random_Forest_CCFD.ipynb
|   ├── 04_Support_Vector_Machine.ipynb
│
├── docs/
│   └── images/
│       ├── confusion_matrix/
|           ├── cm Decision Tree.png
|           ├── cm Random Forest.png
|           ├── cm Support Vector Machine.png 
|           ├── cm_logistic_regression.png
│       ├── feature_importance/
|           ├── Top Feature Decision Tree.png
|           ├── Top Feature Logistic Regression.png
|           ├── Top Feature Random Forest.png
|           ├── Top Feature Support Vector Machine.png
│
|
├── models/
|   ├── Decision_Tree_Model.joblib
|   ├── Logistic_Regression_Model.joblib
|   ├── Random_Forest_Model.joblib
|   ├── Support_Vector_Machine.joblib
|
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
│ Baseline Model       │
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

| Model | Baseline | Class Weight | SMOTE | Tuning | Status |
|---------|:--------:|:-----:|:------:|:------:| :------:|
| Logistic Regression | ✅ | ✅ |✅| ✅ | ✅ |
| Decision Tree | ✅ | ✅ | ✅ |✅| ✅ |
| Random Forest | ✅ | ✅ | ✅| ✅ | ✅ |
| Support Vector Machine | ✅ | ✅ | ✅ | ✅ | ✅ |
| K-Nearest Neighbor| ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |
| AdaBoost | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |
| Gradient Boosting | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |
| Extra Trees | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |
| XGBoost | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |
| LightGBM | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |
| CatBoost | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |
| Gaussian Naive Bayes | ⏳ | ⏳ | ⏳ | ⏳ | Coming Soon |

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

## Decision Tree

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 99.75% | 86%     | 100%    | 92% | 99.87% |
| Class Weight | 99.80% | 88% | 100% | 94% | 99.89% |
| SMOTE     | 99.60%    | 81%   | 97%   | 88%   | 98.15% |
| Class Weight + GridSearchCV | 99.90% | 94% | 100% | 97% | 99.95% |

## Random Forest
| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 99.45% | 100%     | 63.33%    | 78% | 99.99% |
| Class Weight | 99.35% | 100% | 57% | 72% | 99.98% |
| SMOTE     | 99.80%    | 96.43%   | 90%   | 93%   | 99.98% |
| SMOTE + GridSearchCV | 99.85% | 93.55% | 97% | 95% | 99.99% |

## Support Vector Machine
| Model                | Accuracy | Precision | Recall | F1    | ROC-AUC |
|----------------------|---------:|----------:|-------:|------:|--------:|
| Baseline             |  99.30%  |  94.44%   | 56.67% | 71%   | 99.59%  |
| Class Weight         |  98.40%  |  48.21%   | 90%    | 63%   | 99.61%  |
| SMOTE                |  98.15%  |  44.26%   | 90%    | 59%   | 99.62%  |
| Class Weight + GridSearchCV |    99.10%    |    65%     |  86.67%    |   74%   |  99.49%    |

---

# 📊 Visualisasi

## Logistic Regression
### Confusion Matrix

<p align="center">
<img src="docs/images/Confusion Matrix/cm Logistic Regression.png" width="550">
</p>

---

### Interpretasi model menggunakan Feature Importances / Coefficient Analysis

<p align="center">
<img src="docs/images/Feature Importances/Top Feature Logistic Regression.png" width="700">
</p>

## Decision Tree
### Confusion Matrix
<p align="center">
<img src="docs/images/Confusion Matrix/cm Decision Tree.png" width="550">
</p>

### Feature Importance
<p align="center">
<img src="docs/images/Feature Importances/Top Feature Decision Tree.png" width="700">
</p>

## Random Forest
### Confusion Matrix
<p align="center">
<img src="docs/images/Confusion Matrix/cm Random Forest.png" width="550">
</p>

### Feature Importance
<p align="center">
<img src="docs/images/Feature Importances/Top Feature Random Forest.png" width="700">
</p>

## Support Vector Machine
### Confusion Matrix
<p align="center">
<img src="docs/images/Confusion Matrix/cm Support Vector Machine.png" width="550">
</p>

### Feature Importance
<p align="center">
<img src="docs/images/Feature Importances/Top Feature Support Vector Machine.png" width="550">
</p>

---

# 💡 Kesimpulan

Berdasarkan eksperimen yang telah dilakukan pada dataset Credit Card Fraud, diperoleh beberapa temuan:

## Logistic Regression
- Logistic Regression baseline memiliki precision tertinggi (**71%**) namun hanya mampu mendeteksi **50%** transaksi fraud.
- Penerapan **SMOTE** meningkatkan recall menjadi **100%**, sehingga seluruh transaksi fraud pada data uji berhasil dideteksi.
- Hyperparameter tuning menggunakan **GridSearchCV** memberikan sedikit peningkatan pada Accuracy dan F1-Score dibandingkan SMOTE tanpa tuning.
- Nilai **ROC-AUC sekitar 99.3%** menunjukkan bahwa Logistic Regression memiliki kemampuan yang sangat baik dalam membedakan transaksi normal dan fraud.

## Decision Tree
- Decision Tree dengan Class_Weight balanced menunjukkan performa yang lebih baik dibandingkan pendekatan Baseline maupun SMOTE
- Hyperparameter tuning berhasil meningkatkan hampir seluruh metrik evaluasi, terutama Recall (88% -> 94%) dan F1-Score (94% -> 97%) sambil mempertahankan recall di angka 100%.
- Model terbaik menggunakan Entropy Criterion, Maximum Depth = 10, Minimum Samples Split = 2 dan minimum Samples Leaf = 1.
- Decision Tree menghasilkan keseimbangan yang lebih baik antara Precision dan Recall.

## Random Forest
- Pada eksperimen yang dilakukan, kombinasi SMOTE + Hyperparameter Tuning menghasilkan performa terbaik untuk algoritma Random Forest
- Hyperparameter Tuning meningkatkan recall dari 90.00% menjadi 97%, sehingga model mampu mendeteksi hampir seluruh transaksi fraud pada data uji.
- Meskipun precision menurun dibandingkan model smote tanpa tuning, peningkatan recall menghasilkan F1-Score yang lebih baik yakni 95%
- Random Forest memperoleh ROC-AUC sebesar 99.99%, menunjukkan kemampuan yang sangat baik dalam membedakan transaksi normal dan fraud.

## Support Vector Machine
- Model baseline menghasilkan precision yang sangat tinggi (94.44%), namun hanya mampu mendeteksi 56.67% transaksi fraud.
- Penerapan Class Weight meningkatkan recall menjadi 90% , sehingga model mampu mendeteksi lebih banyak transaksi fraud meskipun precision menurun.
- Hyperparameter tuning pada model Class Weight menghasilkan keseimbangan performa yang lebih baik dengan accuracy 99.10%, precision 65%, Recall 86.67% dan F1-Score 74%.
- Meskipun recall sedikit menurun dibandingkan sebelum tuning, peningkatan precision dan F1-Score menunjukkan bahwa model menjadi lebih selektif dalam mendeteksi fraud dengan mengurangi jumlah false positive.
- Support Vector Machine memperoleh ROC-AUC sebesar 99.49%, menunjukkan kemampuan yang sangat baik dalam membedakan transaksi normal dan transaksi fraud.

## Temuan
Secara keseluruhan, hasil eksperimen menunjukkan bahwa setiap algoritma memiliki karakteristik yang berbeda dalam menangani data tidak seimbang. 

- Logistic Regression memberikan performa terbaik setelah dikombinasikan dengan SMOTE dan Hyperparameter Tuning, terutama dalam meningkatkan Precision dan F1-Score.
- Decision Tree mencapai performa terbaik melalui Hyperparameter Tuning dengan peningkatan yang signifikan pada F1-Score dan Precision dengan mempertahankan recall di angka 100%.
- Random Forest memperoleh hasil terbaik menggunakan kombinasi SMOTE dan Hyperparameter Tuning, sehingga mampu mendeteksi hampir semua transaksi fraud.
- Support Vector Machine menunjukkan performa terbaik setelah Hyperparameter Tuning pada model Class Weight, menghasilkan keseimbangan yang lebih baik antara precision dan recall.

Hasil tersebut menunjukkan bahwa tidak ada satu pendekatan penanganan imbalanced dataset yang selalu menjadi pilihan terbaik untuk semua algoritma. Oleh karena itu, strategi seperti Class Weight dan SMOTE perlu dipilih sesuai dengan karakteristik masing-masing model.
---

# 🚀 Pengembangan Selanjutnya

Repository ini akan terus dikembangkan dengan menambahkan berbagai algoritma Machine Learning lainnya.

- [x] Logistic Regression
- [x] Decision Tree
- [x] Random Forest
- [x] Support Vector Machine
- [ ] K-Nearest Neighbor
- [ ] AdaBoost
- [ ] Gradient Boosting
- [ ] Extra Trees
- [ ] XGBoost
- [ ] LightGBM
- [ ] CatBoost
- [ ] Gaussien Naive Bayes

---

# 📚 Repository Terkait

Repository ini berfokus pada pembangunan model Machine Learning.

📊 Repository Exploratory Data Analysis (EDA):

> https://github.com/andiubaid09/Exploratory-Data-Analysis/tree/main/Credit%20Card%20Fraud 

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
