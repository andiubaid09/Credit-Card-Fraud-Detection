# 📈 AdaBoost

| Item | Value |
|------|-------|
| Algorithm | AdaBoost |
| Problem | Binary Classification |
| Dataset | Credit Card Fraud Detection |
| Samples | 10,000 |
| Features | 10 |
| Imbalanced Handling | SMOTE |
| Hyperparameter Tuning | GridSearchCV (5-Fold CV) |
| Best Configuration | Baseline + GridSearchCV |

---

# 📖 Deskripsi

AdaBoost (*Adaptive Boosting*) merupakan algoritma *ensemble learning* yang membangun model secara bertahap menggunakan serangkaian *weak learner* (umumnya Decision Tree dengan kedalaman rendah). Pada setiap iterasi, bobot data yang salah diklasifikasikan akan ditingkatkan sehingga model berikutnya lebih berfokus pada sampel yang sulit diprediksi. Pendekatan ini memungkinkan AdaBoost meningkatkan performa klasifikasi dengan menggabungkan banyak model sederhana menjadi satu model yang lebih kuat.

Pada proyek ini, AdaBoost dievaluasi menggunakan dua pendekatan, yaitu **Baseline** dan **SMOTE**, kemudian dilakukan **Hyperparameter Tuning** menggunakan **GridSearchCV** untuk memperoleh konfigurasi terbaik.

---

# 📚 Dokumentasi Pendukung

Beberapa tahapan umum pada seluruh eksperimen dijelaskan pada dokumentasi berikut.

- 📂 [Dataset](./dataset.md)
- ⚙️ [Methodology](./methodolgy.md)
- 📊 [Evaluation Metrics](./evaluation.md)

Dokumentasi tersebut mencakup:

- Dataset dan distribusi kelas
- Feature Engineering
- Data Preprocessing
- Train-Test Split
- Handling Imbalanced Dataset
- Evaluation Metrics
- Experiment Workflow

---

# 🌲 Hyperparameter Search

Hyperparameter tuning dilakukan menggunakan **GridSearchCV** dengan **5-Fold Cross Validation**.

### Parameter yang diuji

| Parameter | Candidate |
|-----------|-----------|
| n_estimators | 50, 100, 200 |
| learning_rate | 0.01, 0.1, 0.5, 1 |
| algorithm | SAMME, SAMME.R |

---

## 🎯 Best Hyperparameter

| Parameter | Value |
|-----------|-------|
| n_estimators | 200 |
| learning_rate | 1 |
| algorithm | SAMME |

---

# 📊 Hasil Eksperimen

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 99.95% | 100% | 96.67% | 98% | 100% |
| SMOTE | 99.25% | 66.67% | 100% | 80% | 100% |
| Baseline + GridSearchCV | 100% | 100% | 100% | 100% | 100% |

---

# 📈 Confusion Matrix

<p align="center">
<img src="../images/Confusion Matrix/cm AdaBoost.png" width="600">
</p>

---

# 📌 Feature Importance

<p align="center">
<img src="../images/Feature Importances/Top Feature AdaBoost.png" width="700">
</p>

---

# 🔍 Analisis

## Baseline

Model AdaBoost baseline telah menunjukkan performa yang sangat baik pada dataset ini. Model mencapai Accuracy sebesar **99.95%**, Precision **100%**, Recall **96.67%**, serta ROC-AUC **100%**. Hasil tersebut menunjukkan bahwa tanpa penanganan tambahan terhadap ketidakseimbangan kelas, AdaBoost sudah mampu mengidentifikasi hampir seluruh transaksi fraud dengan tingkat kesalahan yang sangat rendah.

---

## SMOTE

Penerapan **SMOTE** berhasil meningkatkan Recall menjadi **100%**, sehingga seluruh transaksi fraud pada data uji berhasil terdeteksi. Namun, peningkatan tersebut diikuti oleh penurunan Precision menjadi **66.67%**, yang menunjukkan bertambahnya jumlah transaksi normal yang diprediksi sebagai fraud (*false positive*). Dengan demikian, pada dataset ini penggunaan SMOTE menghasilkan trade-off antara kemampuan mendeteksi seluruh fraud dan ketepatan prediksi.

---

## Hyperparameter Tuning

Hyperparameter tuning dilakukan menggunakan **GridSearchCV** pada model baseline karena pendekatan tersebut telah memberikan performa terbaik pada tahap eksperimen sebelumnya.

Proses tuning menghasilkan konfigurasi terbaik dengan **200 estimator**, **learning rate sebesar 1**, dan algoritma **SAMME**. Berdasarkan hasil evaluasi pada data uji, model mencapai Accuracy, Precision, Recall, F1-Score, dan ROC-AUC masing-masing sebesar **100%**.

Berdasarkan hasil eksperimen pada dataset ini, konfigurasi hasil tuning dipilih sebagai model terbaik karena memberikan performa tertinggi pada seluruh metrik evaluasi yang digunakan.

---

# 💡 Interpretasi Feature Importance

AdaBoost menghitung **Feature Importance** berdasarkan kontribusi masing-masing fitur terhadap penurunan kesalahan (*weighted impurity reduction*) selama proses boosting. Nilai tersebut merupakan akumulasi kontribusi setiap fitur dari seluruh *weak learner* yang membentuk model.

Semakin tinggi nilai Feature Importance, semakin besar kontribusi fitur tersebut terhadap proses klasifikasi. Visualisasi berikut menunjukkan urutan fitur berdasarkan tingkat kepentingannya dalam mendeteksi transaksi fraud pada model AdaBoost.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

- Model AdaBoost menunjukkan performa yang sangat tinggi pada dataset Credit Card Fraud Detection bahkan tanpa penanganan tambahan terhadap ketidakseimbangan kelas.
- Pendekatan **SMOTE** berhasil meningkatkan Recall menjadi **100%**, namun menyebabkan penurunan Precision akibat meningkatnya jumlah *false positive*.
- Hyperparameter tuning menggunakan **GridSearchCV** menghasilkan konfigurasi terbaik dengan:
  - Algorithm: **SAMME**
  - Learning Rate: **1**
  - Number of Estimators: **200**
- Model hasil tuning mencapai performa terbaik pada dataset ini dengan:
  - Accuracy : **100.00%**
  - Precision : **100%**
  - Recall : **100%**
  - F1-Score : **100%**
  - ROC-AUC : **100%**

Berdasarkan hasil eksperimen yang dilakukan pada proyek ini, **AdaBoost dengan GridSearchCV** menjadi konfigurasi terbaik karena menghasilkan performa evaluasi tertinggi dibandingkan konfigurasi AdaBoost lainnya yang diuji.