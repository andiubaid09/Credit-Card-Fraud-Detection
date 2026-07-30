# 📈 Gradient Boosting

| Item | Value |
|------|-------|
| Algorithm | Gradient Boosting |
| Problem | Binary Classification |
| Dataset | Credit Card Fraud Detection |
| Samples | 10,000 |
| Features | 10 |
| Imbalanced Handling | SMOTE |
| Hyperparameter Tuning | GridSearchCV (5-Fold CV) |
| Best Configuration | SMOTE + GridSearchCV |

---

# 📖 Deskripsi

Gradient Boosting merupakan algoritma *ensemble learning* yang membangun model secara bertahap (*sequential boosting*). Setiap model baru dilatih untuk memperbaiki kesalahan (*residual error*) yang dihasilkan oleh model sebelumnya sehingga performa prediksi meningkat secara bertahap. Berbeda dengan Random Forest yang membangun pohon secara independen, Gradient Boosting membangun setiap pohon berdasarkan hasil pembelajaran pohon sebelumnya.

Pada proyek ini, Gradient Boosting dievaluasi menggunakan dua pendekatan, yaitu **Baseline** dan **SMOTE**, kemudian dilakukan **Hyperparameter Tuning** menggunakan **GridSearchCV** untuk memperoleh konfigurasi terbaik.

---

# 📚 Dokumentasi Pendukung

Beberapa tahapan umum pada seluruh eksperimen dijelaskan pada dokumentasi berikut.

- 📂 [Dataset](./dataset.md)
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
| n_estimators | 100, 200 |
| learning_rate | 0.01, 0.05, 0.1 |
| max_depth | 3, 5, 6 |
| min_samples_split | 2, 5, 10 |
| min_samples_leaf | 2, 4 |
| subsample | 0.8, 1.0 |

---

## 🎯 Best Hyperparameter

| Parameter | Value |
|-----------|-------|
| n_estimators | 100 |
| learning_rate | 0.1 |
| max_depth | 6 |
| min_samples_split | 2 |
| min_samples_leaf | 2 |
| subsample | 0.8 |

---

# 📊 Hasil Eksperimen

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 99.65% | 89.66% | 86.67% | 88% | 99.99% |
| SMOTE | 99.35% | 70.73% | 96.67% | 82% | 99.99% |
| SMOTE + GridSearchCV | 99.90% | 93.75% | 100% | 97% | 99.99% |

---

# 📈 Confusion Matrix

<p align="center">
<img src="../images/Confusion Matrix/cm Gradient Boosting.png" width="600">
</p>

---

# 📌 Feature Importance

<p align="center">
<img src="../images/Feature Importances/Top Feature Gradient Boosting.png" width="700">
</p>

---

# 🔍 Analisis

## Baseline

Model Gradient Boosting baseline telah menunjukkan performa yang sangat baik dengan Accuracy sebesar **99.65%**, Precision **89.66%**, Recall **86.67%**, dan F1-Score **88%**. Hasil ini menunjukkan bahwa tanpa penanganan tambahan terhadap ketidakseimbangan kelas, Gradient Boosting sudah mampu mendeteksi sebagian besar transaksi fraud dengan tingkat kesalahan yang rendah.

---

## SMOTE

Penerapan **SMOTE** meningkatkan Recall menjadi **96.67%**, sehingga lebih banyak transaksi fraud berhasil dideteksi dibandingkan model baseline. Namun, peningkatan tersebut diikuti oleh penurunan Precision menjadi **70.73%**, yang menunjukkan bertambahnya jumlah transaksi normal yang diprediksi sebagai fraud (*false positive*). Dengan demikian, penggunaan SMOTE menghasilkan trade-off antara kemampuan mendeteksi fraud dan ketepatan prediksi.

---

## Hyperparameter Tuning

Hyperparameter tuning dilakukan menggunakan **GridSearchCV** pada model **SMOTE**, karena pendekatan tersebut memberikan kemampuan deteksi fraud (Recall) yang lebih tinggi dibandingkan model baseline.

Proses tuning menghasilkan konfigurasi terbaik dengan **100 estimator**, **learning rate 0.1**, **maximum depth 6**, **minimum samples split 2**, **minimum samples leaf 2**, dan **subsample 0.8**.

Dibandingkan model SMOTE sebelum tuning, performa meningkat secara signifikan. Precision meningkat dari **70.73%** menjadi **93.75%**, sementara Recall juga meningkat dari **96.67%** menjadi **100%**, sehingga seluruh transaksi fraud pada data uji berhasil dideteksi. Peningkatan tersebut menghasilkan F1-Score sebesar **97%** dengan Accuracy **99.90%** dan ROC-AUC **99.99%**.

Berdasarkan hasil eksperimen pada dataset ini, konfigurasi hasil tuning dipilih sebagai model terbaik karena memberikan keseimbangan performa yang sangat baik pada seluruh metrik evaluasi.

---

# 💡 Interpretasi Feature Importance

Gradient Boosting menghitung **Feature Importance** berdasarkan total kontribusi setiap fitur dalam mengurangi impurity pada seluruh pohon keputusan yang membentuk model. Nilai tersebut menggambarkan seberapa besar peran masing-masing fitur selama proses pembelajaran model.

Semakin tinggi nilai Feature Importance, semakin besar kontribusi fitur tersebut dalam membedakan transaksi normal dan transaksi fraud. Visualisasi berikut menampilkan urutan fitur berdasarkan tingkat kepentingannya sehingga dapat membantu memahami faktor-faktor yang paling berpengaruh dalam proses klasifikasi.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

- Model Gradient Boosting menunjukkan performa yang sangat baik pada permasalahan Credit Card Fraud Detection dengan menghasilkan nilai Accuracy dan ROC-AUC yang tinggi pada seluruh skenario pengujian.
- Pendekatan **SMOTE** meningkatkan kemampuan model dalam mendeteksi transaksi fraud dibandingkan model baseline melalui peningkatan nilai Recall.
- Hyperparameter tuning menggunakan **GridSearchCV** berhasil meningkatkan performa model secara signifikan dengan meningkatkan Precision sekaligus mempertahankan Recall hingga **100%**.
- Model terbaik pada eksperimen ini menggunakan konfigurasi:
  - Learning Rate: **0.1**
  - Maximum Depth: **6**
  - Minimum Samples Leaf: **2**
  - Minimum Samples Split: **2**
  - Number of Estimators: **100**
  - Subsample: **0.8**

  dengan hasil evaluasi:
  - Accuracy : **99.90%**
  - Precision : **93.75%**
  - Recall : **100.00%**
  - F1-Score : **97.00%**
  - ROC-AUC : **99.99%**

Berdasarkan hasil eksperimen yang dilakukan pada proyek ini, **Gradient Boosting dengan SMOTE dan GridSearchCV** menjadi konfigurasi terbaik karena mampu memberikan keseimbangan yang sangat baik antara kemampuan mendeteksi seluruh transaksi fraud (Recall), menjaga ketepatan prediksi (Precision), serta menghasilkan F1-Score dan ROC-AUC yang sangat tinggi.