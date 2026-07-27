# 📈 Logistic Regression

## 📖 Deskripsi

Logistic Regression merupakan salah satu algoritma klasifikasi linear yang digunakan untuk memprediksi probabilitas suatu data termasuk ke dalam kelas tertentu. Pada penelitian ini, Logistic Regression digunakan sebagai **baseline model** karena memiliki interpretabilitas yang tinggi, proses pelatihan yang cepat, serta sering dijadikan acuan dalam permasalahan klasifikasi biner seperti deteksi fraud.

Seluruh eksperimen dilakukan menggunakan workflow yang konsisten sehingga hasilnya dapat dibandingkan secara objektif dengan algoritma Machine Learning lainnya.

---

# ⚙️ Workflow

```
Dataset
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
├── Class Weight
└── SMOTE
    │
    ▼
Hyperparameter Tuning
(GridSearchCV)
    │
    ▼
Model Evaluation
```

---

# 🔄 Preprocessing

Tahapan preprocessing yang diterapkan pada Logistic Regression adalah sebagai berikut.

### Feature Engineering

Fitur `transaction_hour` diubah menggunakan **Cyclical Encoding** menjadi dua fitur baru.

- hour_sin
- hour_cos

Transformasi ini dilakukan karena waktu bersifat siklik, sehingga pukul **23.00** dan **00.00** berada berdekatan.

---

### StandardScaler

Scaling hanya diterapkan pada fitur numerik.

| Feature |
|----------|
| Amount |
| Device Trust Score |
| Velocity Last 24 Hours |
| Cardholder Age |

Sedangkan fitur biner seperti `foreign_transaction` dan `location_mismatch` tidak dilakukan scaling.

---

### Train-Test Split

| Parameter | Nilai |
|-----------|-------|
| Train Size | 80% |
| Test Size | 20% |
| Stratify | Yes |
| Random State | 42 |

---

# ⚖️ Penanganan Imbalanced Dataset

Dataset memiliki distribusi kelas:

| Kelas | Jumlah |
|-------|--------|
| Normal | 9.849 |
| Fraud | 151 |

Sehingga dilakukan tiga pendekatan berbeda.

- Baseline
- Class Weight (`balanced`)
- SMOTE

---

# 🎯 Hyperparameter Terbaik

Hyperparameter diperoleh menggunakan **GridSearchCV**.

| Parameter | Nilai |
|------------|--------|
| Penalty | l2 |
| Solver | liblinear |
| C | 10 |
| Max Iteration | 1000 |

---

# 📊 Hasil Eksperimen

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 98.95% | 71% | 50% | 59% | 99.33% |
| Class Weight | 95.20% | 24% | 100% | 38% | 99.33% |
| SMOTE | 96.00% | 27% | 100% | 43% | 99.33% |
| SMOTE + GridSearchCV | 96.20% | 28% | 100% | 44% | 99.32% |

---

# 📈 Confusion Matrix

<p align="center">
<img src="../images/Confusion Matrix/cm Logistic Regression.png" width="600">
</p>

---

# 📌 Feature Coefficients

<p align="center">
<img src="../images/Feature Importances/Top Feature Logistic Regression.png" width="700">
</p>

---

# 🔍 Analisis

## Baseline

Model Logistic Regression tanpa penanganan imbalance menghasilkan akurasi yang sangat tinggi (98.95%). Namun, nilai tersebut kurang merepresentasikan kemampuan model dalam mendeteksi transaksi fraud karena dataset didominasi oleh transaksi normal.

Model hanya mampu mendeteksi sekitar **50% transaksi fraud** dengan precision sebesar **71%**, yang menunjukkan bahwa prediksi fraud relatif akurat tetapi masih banyak kasus fraud yang terlewat.

---

## Class Weight

Pendekatan `class_weight='balanced'` meningkatkan recall menjadi **100%**, sehingga seluruh transaksi fraud berhasil dideteksi.

Namun peningkatan recall tersebut diikuti penurunan precision menjadi **24%**, yang berarti jumlah false positive meningkat secara signifikan.

---

## SMOTE

SMOTE menghasilkan performa yang lebih seimbang dibandingkan Class Weight.

Recall tetap mencapai **100%**, sedangkan precision meningkat menjadi **27%**.

Hal ini menunjukkan bahwa oversampling sintetis membantu model mempelajari pola transaksi fraud dengan lebih baik.

---

## Hyperparameter Tuning

Hyperparameter tuning menggunakan GridSearchCV memberikan peningkatan kecil dibandingkan model SMOTE.

Perubahan yang diperoleh meliputi:

- Accuracy meningkat dari **96.00% menjadi 96.20%**
- Precision meningkat dari **27% menjadi 28%**
- F1-Score meningkat dari **43% menjadi 44%**

Sementara nilai Recall tetap berada pada **100%**, sehingga seluruh transaksi fraud pada data uji berhasil dideteksi.

---

# 💡 Interpretasi Feature Coefficients

Karena Logistic Regression merupakan model linear, setiap koefisien menunjukkan besar pengaruh suatu fitur terhadap peluang transaksi diklasifikasikan sebagai fraud.

- Koefisien positif menunjukkan bahwa peningkatan nilai fitur meningkatkan probabilitas fraud.
- Koefisien negatif menunjukkan bahwa peningkatan nilai fitur menurunkan probabilitas fraud.
- Semakin besar nilai absolut koefisien, semakin besar pengaruh fitur terhadap prediksi model.

Visualisasi Feature Coefficients memberikan gambaran mengenai fitur yang paling berkontribusi dalam proses klasifikasi.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

- Logistic Regression mampu menjadi baseline yang kuat untuk permasalahan Credit Card Fraud Detection.
- Penanganan dataset tidak seimbang menggunakan **SMOTE** meningkatkan kemampuan model dalam mendeteksi transaksi fraud dibandingkan model baseline.
- Hyperparameter tuning memberikan peningkatan performa meskipun tidak terlalu signifikan.
- Model terbaik pada eksperimen ini adalah **SMOTE + GridSearchCV**, dengan Accuracy **96.20%**, Recall **100%**, F1-Score **44%**, dan ROC-AUC **99.32%**.

Walaupun precision masih relatif rendah, model ini berhasil mendeteksi seluruh transaksi fraud pada data uji, sehingga lebih sesuai apabila tujuan utama adalah meminimalkan kasus fraud yang terlewat (*false negative*).