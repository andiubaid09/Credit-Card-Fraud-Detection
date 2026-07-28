# 📈 Random Forest

| Item | Value |
|------|-------|
| Algorithm | Random Forest |
| Problem | Binary Classification |
| Dataset | Credit Card Fraud Detection |
| Samples | 10,000 |
| Features | 10 |
| Imbalanced Handling | Class Weight, SMOTE |
| Hyperparameter Tuning | GridSearchCV (5-Fold CV) |
| Best Configuration | SMOTE + GridSearchCV |

---

# 📖 Deskripsi

Random Forest merupakan algoritma *ensemble learning* berbasis kumpulan Decision Tree yang menggunakan teknik **bagging (Bootstrap Aggregating)** untuk meningkatkan performa prediksi. Setiap pohon dibangun menggunakan subset data dan subset fitur yang berbeda sehingga menghasilkan model yang lebih stabil, mampu mengurangi overfitting, serta memiliki kemampuan generalisasi yang lebih baik dibandingkan Decision Tree tunggal.

Pada proyek ini, Random Forest dievaluasi menggunakan beberapa strategi penanganan data tidak seimbang, yaitu **Baseline**, **Class Weight**, **SMOTE**, serta **Hyperparameter Tuning** menggunakan GridSearchCV.

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
| max_depth | None, 10, 20 |
| min_samples_split | 2, 5, 10 |
| min_samples_leaf | 1, 2, 4 |
| max_features | sqrt, log2 |
| criterion | gini, entropy |

---

## 🎯 Best Hyperparameter

| Parameter | Value |
|-----------|-------|
| n_estimators | 200 |
| max_depth | 10 |
| min_samples_split | 2 |
| min_samples_leaf | 1 |
| max_features | log2 |
| criterion | entropy |

---

# 📊 Hasil Eksperimen

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 99.45% | 100% | 63.33% | 78% | 99.99% |
| Class Weight | 99.35% | 100% | 57% | 72% | 99.98% |
| SMOTE | 99.80% | 96.43% | 90% | 93% | 99.98% |
| SMOTE + GridSearchCV | 99.85% | 93.55% | 97% | 95% | 99.99% |

---

# 📈 Confusion Matrix

<p align="center">
<img src="../images/Confusion Matrix/cm Random Forest.png" width="600">
</p>

---

# 📌 Feature Importance

<p align="center">
<img src="../images/Feature Importances/Top Feature Random Forest.png" width="700">
</p>

---

# 🔍 Analisis

## Baseline

Model Random Forest baseline menghasilkan performa yang sangat baik dengan precision mencapai 100%, yang menunjukkan bahwa seluruh transaksi yang diprediksi sebagai fraud merupakan prediksi yang benar. Namun, model hanya mampu mendeteksi 63.33% transaksi fraud pada data uji (recall), sehingga masih terdapat beberapa kasus fraud yang tidak teridentifikasi. Hasil ini menunjukkan bahwa meskipun Random Forest memiliki kemampuan klasifikasi yang kuat, model baseline masih cenderung lebih konservatif dalam memberikan prediksi fraud.

---

## Class Weight

Penerapan class_weight='balanced' belum memberikan peningkatan performa dibandingkan model baseline. Meskipun tetap mempertahankan precision sebesar 100%, nilai recall menurun menjadi 57%, sehingga semakin banyak transaksi fraud yang tidak berhasil dideteksi. Berdasarkan hasil tersebut, pendekatan pembobotan kelas kurang efektif untuk meningkatkan kemampuan Random Forest pada dataset ini.

---

## SMOTE

Penerapan SMOTE memberikan peningkatan performa yang signifikan dibandingkan baseline maupun Class Weight. Recall meningkat dari 63.33% menjadi 90%, sementara precision tetap tinggi sebesar 96.43%, menghasilkan F1-Score sebesar 93%. Hasil ini menunjukkan bahwa penambahan sampel sintetis pada kelas minoritas membantu Random Forest mempelajari pola transaksi fraud dengan lebih baik tanpa mengorbankan performa secara signifikan pada kelas mayoritas.

---

## Hyperparameter Tuning
Hyperparameter tuning dilakukan menggunakan GridSearchCV pada model Random Forest dengan pendekatan SMOTE, karena pendekatan tersebut memberikan keseimbangan performa terbaik pada tahap sebelumnya.

Proses tuning menghasilkan konfigurasi optimal yang meningkatkan kemampuan model dalam mendeteksi transaksi fraud. Dibandingkan model SMOTE sebelum tuning, Recall meningkat dari 73.33% menjadi 90%, sehingga lebih banyak transaksi fraud berhasil teridentifikasi. Meskipun Precision sedikit menurun, peningkatan Recall menghasilkan F1-Score yang lebih tinggi, sementara Accuracy tetap berada pada 99.00% dan ROC-AUC tetap sangat tinggi (≈99.6%).

Berdasarkan hasil tersebut, model hasil tuning dipilih sebagai model terbaik karena memberikan keseimbangan yang lebih baik antara kemampuan mendeteksi transaksi fraud (Recall) dan menjaga kualitas prediksi secara keseluruhan (F1-Score).

---

# 💡 Interpretasi Feature Importance

Random Forest menghitung Feature Importance berdasarkan rata-rata penurunan impurity (Mean Decrease in Impurity) dari seluruh pohon keputusan yang membentuk model (ensemble). Nilai tersebut menunjukkan seberapa besar kontribusi masing-masing fitur dalam proses pengambilan keputusan selama pelatihan.

Semakin tinggi nilai Feature Importance, semakin besar pengaruh fitur tersebut terhadap prediksi model. Karena dihitung dari agregasi banyak pohon keputusan, nilai Feature Importance pada Random Forest umumnya lebih stabil dan lebih robust dibandingkan Decision Tree tunggal.

Visualisasi berikut menampilkan urutan fitur berdasarkan tingkat kepentingannya, sehingga memudahkan analisis terhadap fitur-fitur yang paling berkontribusi dalam mendeteksi transaksi fraud pada model Random Forest.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

- Random Forest menunjukkan performa yang sangat baik pada permasalahan Credit Card Fraud Detection dengan menghasilkan nilai Accuracy dan ROC-AUC yang tinggi pada seluruh skenario pengujian.
- Pendekatan **SMOTE** memberikan peningkatan kemampuan model dalam mendeteksi transaksi fraud dibandingkan model baseline maupun Class Weight, yang ditunjukkan oleh peningkatan nilai Recall.
- Hyperparameter tuning menggunakan **GridSearchCV** semakin meningkatkan performa model, terutama dengan meningkatkan Recall menjadi **90%**, sehingga lebih banyak transaksi fraud berhasil diidentifikasi tanpa penurunan performa yang signifikan pada metrik lainnya.
- Model terbaik pada eksperimen ini menggunakan konfigurasi:
  - Criterion: **Entropy**
  - Max Depth: **10**
  - Max Features: **log2**
  - Min Samples Leaf: **2**
  - Min Samples Split: **10**
  - Number of Estimators: **100**

  dengan hasil evaluasi:
  - Accuracy : **99.00%**
  - Precision : **61.36%**
  - Recall : **90.00%**
  - F1-Score : **73.00%**
  - ROC-AUC : **99.60%**

Secara keseluruhan, Random Forest menjadi salah satu model dengan performa terbaik pada proyek ini karena mampu memberikan keseimbangan yang baik antara kemampuan mendeteksi transaksi fraud (Recall) dan kualitas prediksi secara keseluruhan (Precision, F1-Score, dan ROC-AUC).