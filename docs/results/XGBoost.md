# 🚀 XGBoost

| Item | Value |
|------|-------|
| Algorithm | Extreme Gradient Boosting (XGBoost) |
| Problem | Binary Classification |
| Dataset | Credit Card Fraud Detection |
| Samples | 10,000 |
| Features | 10 |
| Imbalanced Handling | SMOTE |
| Hyperparameter Tuning | GridSearchCV (5-Fold CV) |
| Best Configuration | Baseline + GridSearchCV |

---

# 📖 Deskripsi

XGBoost (Extreme Gradient Boosting) merupakan algoritma *ensemble learning* berbasis **gradient boosting** yang membangun pohon keputusan secara bertahap (*sequential learning*) untuk memperbaiki kesalahan model sebelumnya. XGBoost dikenal memiliki performa tinggi, efisiensi komputasi, serta kemampuan regularisasi yang baik sehingga menjadi salah satu algoritma yang paling banyak digunakan pada kompetisi machine learning maupun permasalahan klasifikasi data tabular.

Pada proyek ini, XGBoost dievaluasi menggunakan beberapa pendekatan, yaitu **Baseline**, **SMOTE**, serta **Hyperparameter Tuning** menggunakan GridSearchCV.

---

# 📚 Dokumentasi Pendukung

Beberapa tahapan umum pada seluruh eksperimen dijelaskan pada dokumentasi berikut.

- 📂 [Dataset](dataset.md)
- ⚙️ [Methodology](methodolgy.md)
- 📊 [Evaluation Metrics](evaluation.md)

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
| n_estimators | 100, 150, 200 |
| max_depth | 3, 5, 7 |
| learning_rate | 0.01, 0.1, 0.3 |
| subsample | 0.5, 0.8, 1 |
| colsample_bytree | 0.5, 0.8, 1 |
| gamma | 0, 0.1 |
| min_child_weight | 1, 3 |

---

## 🎯 Best Hyperparameter

| Parameter | Value |
|-----------|-------|
| n_estimators | 200 |
| max_depth | 3 |
| learning_rate | 0.3 |
| subsample | 0.8 |
| colsample_bytree | 0.5 |
| gamma | 0.1 |
| min_child_weight | 1 |

---

# 📊 Hasil Eksperimen

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 100.00% | 100.00% | 100.00% | 100% | 100.00% |
| SMOTE | 99.90% | 93.75% | 100.00% | 97% | 100.00% |
| Baseline + GridSearchCV | 100.00% | 100.00% | 100.00% | 100% | 100.00% |

---

# 📈 Confusion Matrix

<p align="center">
<img src="../images/Confusion Matrix/cm XGBoost.png" width="600">
</p>

---

# 📌 Feature Importance

<p align="center">
<img src="../images/Feature Importances/Top Feature XGBoost.png" width="700">
</p>

---

# 🔍 Analisis

## Baseline

Model XGBoost baseline memberikan performa yang sangat baik dengan berhasil mengklasifikasikan seluruh transaksi pada data uji secara benar. Seluruh transaksi fraud berhasil terdeteksi tanpa menghasilkan False Positive maupun False Negative, sehingga Accuracy, Precision, Recall, F1-Score, dan ROC-AUC semuanya mencapai **100%**.

Hasil tersebut menunjukkan bahwa konfigurasi default XGBoost sudah mampu mempelajari pola transaksi fraud secara sangat efektif pada dataset yang digunakan.

---

## SMOTE

Penerapan SMOTE tetap mampu mempertahankan Recall sebesar **100%**, sehingga seluruh transaksi fraud berhasil dideteksi. Namun, Precision menurun menjadi **93.75%** karena muncul beberapa False Positive yang tidak ditemukan pada model baseline.

Hasil tersebut menunjukkan bahwa oversampling tidak memberikan peningkatan performa pada XGBoost untuk dataset ini, bahkan sedikit menurunkan kualitas prediksi dibandingkan model baseline.

---

## Hyperparameter Tuning

Hyperparameter tuning dilakukan menggunakan **GridSearchCV** pada model baseline karena model tersebut telah memberikan performa terbaik sebelum proses tuning.

Hasil tuning menghasilkan konfigurasi optimal tanpa mengubah performa evaluasi pada data uji. Accuracy, Precision, Recall, F1-Score, dan ROC-AUC tetap mencapai **100%**, yang menunjukkan bahwa konfigurasi hasil tuning mampu mempertahankan performa sempurna yang telah dicapai oleh model baseline.

Berdasarkan hasil tersebut, model hasil tuning dipilih sebagai model terbaik karena menghasilkan konfigurasi yang telah dioptimalkan melalui proses pencarian hyperparameter sekaligus mempertahankan performa terbaik pada seluruh metrik evaluasi.

---

# 💡 Interpretasi Feature Importance

XGBoost menghitung **Feature Importance** berdasarkan kontribusi setiap fitur terhadap proses pembentukan pohon keputusan selama proses boosting. Nilai importance menunjukkan seberapa besar suatu fitur membantu mengurangi kesalahan prediksi (*loss reduction*) pada keseluruhan model.

Semakin tinggi nilai Feature Importance, semakin besar kontribusi fitur tersebut dalam membedakan transaksi normal dan transaksi fraud. Visualisasi Feature Importance membantu mengidentifikasi fitur-fitur yang paling berpengaruh dalam proses klasifikasi serta memberikan interpretasi terhadap keputusan model.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

- XGBoost menghasilkan performa terbaik pada proyek ini dengan mencapai nilai sempurna pada seluruh metrik evaluasi.
- Model baseline sudah mampu mengklasifikasikan seluruh transaksi pada data uji tanpa kesalahan prediksi.
- Pendekatan SMOTE tidak memberikan peningkatan performa, melainkan sedikit menurunkan Precision akibat munculnya False Positive.
- Hyperparameter tuning menggunakan GridSearchCV berhasil memperoleh konfigurasi optimal tanpa mengubah performa model, sehingga konfigurasi tersebut dipilih sebagai model terbaik.

Model terbaik pada eksperimen ini menggunakan konfigurasi:

- Number of Estimators: **200**
- Maximum Depth: **3**
- Learning Rate: **0.3**
- Subsample: **0.8**
- Column Sample by Tree: **0.5**
- Gamma: **0.1**
- Minimum Child Weight: **1**

dengan hasil evaluasi:

- Accuracy : **100.00%**
- Precision : **100.00%**
- Recall : **100.00%**
- F1-Score : **100.00%**
- ROC-AUC : **100.00%**

Secara keseluruhan, XGBoost menjadi model dengan performa terbaik pada proyek ini karena mampu mendeteksi seluruh transaksi fraud tanpa menghasilkan kesalahan klasifikasi pada data uji, sekaligus mempertahankan performa sempurna setelah proses optimasi hyperparameter.