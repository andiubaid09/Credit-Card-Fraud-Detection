# 📈 K-Nearest Neighbor

| Item | Value |
|------|-------|
| Algorithm | K-Nearest Neighbor (KNN) |
| Problem | Binary Classification |
| Dataset | Credit Card Fraud Detection |
| Samples | 10,000 |
| Features | 10 |
| Imbalanced Handling | N/A, SMOTE |
| Hyperparameter Tuning | GridSearchCV (5-Fold CV) |
| Best Configuration | SMOTE + GridSearchCV |

---

# 📖 Deskripsi

K-Nearest Neighbor (KNN) merupakan algoritma *instance-based learning* yang melakukan klasifikasi berdasarkan mayoritas kelas dari sejumlah tetangga terdekat (*nearest neighbors*). Berbeda dengan algoritma lain yang membangun model selama proses pelatihan, KNN menyimpan seluruh data latih dan melakukan proses prediksi saat data baru diberikan.

Pada proyek ini, KNN dievaluasi menggunakan pendekatan **Baseline**, **SMOTE**, serta **Hyperparameter Tuning** menggunakan GridSearchCV. Algoritma KNN tidak mendukung parameter `class_weight`, sehingga pendekatan penyeimbangan kelas hanya dilakukan menggunakan SMOTE.

---

# 📚 Dokumentasi Pendukung

Beberapa tahapan umum pada seluruh eksperimen dijelaskan pada dokumentasi berikut.

- 📂 [Dataset](./dataset.md)
- ⚙️ [Methodology](methodology.md)
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

# 🔍 Hyperparameter Search

Hyperparameter tuning dilakukan menggunakan **GridSearchCV** dengan **5-Fold Cross Validation**.

### Parameter yang diuji

| Parameter | Candidate |
|-----------|-----------|
| n_neighbors | 1, 2, 3, 4, 5, 6, 7, 9, 11, 13, 15 |
| weights | uniform, distance |
| metric | euclidean, manhattan, minkowski |
| p (Minkowski) | 1, 2 |

---

## 🎯 Best Hyperparameter

| Parameter | Value |
|-----------|-------|
| n_neighbors | 4 |
| weights | uniform |
| metric | manhattan |

---

# 📊 Hasil Eksperimen

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 98.75% | 64.71% | 36.67% | 47% | 92.70% |
| Class Weight | N/A | N/A | N/A | N/A | N/A |
| SMOTE | 97.45% | 36.71% | 96.67% | 53% | 97.46% |
| SMOTE + GridSearchCV | 98.10% | 43.10% | 83.33% | 57% | 95.82% |

---

# 📈 Confusion Matrix

<p align="center">
<img src="../images/Confusion Matrix/cm K-Nearest Neighbor.png" width="600">
</p>

---

# 📌 Feature Importance

<p align="center">
<img src="../images/Feature Importances/Top Feature K-Nearest_Neighbor.png" width="700">
</p>

---


# 🔍 Analisis

## Baseline

Model KNN baseline menghasilkan **Accuracy sebesar 98.75%** dengan **Precision mencapai 64.71%**, namun hanya mampu mendeteksi **36.67%** transaksi fraud pada data uji. Nilai Recall yang relatif rendah menunjukkan bahwa model masih melewatkan cukup banyak kasus fraud sehingga kurang optimal apabila digunakan secara langsung pada dataset yang tidak seimbang.

---

## SMOTE

Penerapan **SMOTE** memberikan perubahan yang cukup signifikan terhadap performa model. Nilai **Recall meningkat menjadi 96.67%**, menunjukkan bahwa hampir seluruh transaksi fraud berhasil dideteksi. Akan tetapi, peningkatan tersebut diikuti oleh penurunan **Precision menjadi 36.71%**, sehingga jumlah transaksi normal yang salah diprediksi sebagai fraud menjadi lebih banyak. Kondisi ini menghasilkan peningkatan F1-Score dibandingkan model baseline meskipun Accuracy sedikit menurun.

---

## Hyperparameter Tuning

Hyperparameter tuning dilakukan menggunakan **GridSearchCV** pada model KNN dengan pendekatan **SMOTE**, karena pendekatan tersebut memberikan kemampuan deteksi fraud terbaik pada tahap sebelumnya.

Hasil tuning menghasilkan konfigurasi optimal dengan **metric Manhattan**, **4 tetangga terdekat (n_neighbors = 4)**, dan **uniform weighting**. Setelah tuning, Accuracy meningkat dari **97.45% menjadi 98.10%**, sementara Precision meningkat dari **36.71% menjadi 43.10%**. Meskipun Recall sedikit menurun dari **96.67% menjadi 83.33%**, nilai F1-Score meningkat menjadi **57%**, menunjukkan keseimbangan yang lebih baik antara kemampuan mendeteksi transaksi fraud dan mengurangi prediksi positif yang salah.

---

# 💡 Interpretasi Model

K-Nearest Neighbor melakukan klasifikasi berdasarkan kedekatan jarak antar data. Untuk setiap data baru, model akan mencari sejumlah tetangga terdekat (*nearest neighbors*) berdasarkan metrik jarak yang digunakan, kemudian menentukan kelas berdasarkan mayoritas tetangga tersebut.

Pada eksperimen ini, konfigurasi terbaik menggunakan **Manhattan Distance** dengan **4 tetangga terdekat**. Pemilihan metrik Manhattan menunjukkan bahwa pengukuran jarak berdasarkan selisih absolut antar fitur memberikan hasil yang lebih baik dibandingkan Euclidean maupun Minkowski pada dataset ini.

Karena KNN merupakan algoritma berbasis jarak (*distance-based algorithm*), model ini **tidak menghasilkan Feature Importance maupun koefisien fitur** seperti Logistic Regression atau Decision Tree. Oleh karena itu, interpretasi pengaruh masing-masing fitur memerlukan metode explainability seperti **Permutation Importance** atau **SHAP**.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

- Model KNN baseline menghasilkan Precision yang cukup baik, namun kemampuan mendeteksi transaksi fraud masih terbatas karena Recall relatif rendah.
- Pendekatan **SMOTE** berhasil meningkatkan kemampuan deteksi fraud secara signifikan dengan meningkatkan Recall hingga **96.67%**, meskipun Precision mengalami penurunan akibat meningkatnya jumlah *false positive*.
- Hyperparameter tuning menggunakan **GridSearchCV** berhasil menghasilkan keseimbangan yang lebih baik antara Precision dan Recall dibandingkan model SMOTE tanpa tuning, sehingga meningkatkan F1-Score menjadi **57%**.
- Model terbaik pada eksperimen ini menggunakan konfigurasi:
  - Metric : **Manhattan**
  - Number of Neighbors : **4**
  - Weights : **Uniform**

  dengan hasil evaluasi:
  - Accuracy : **98.10%**
  - Precision : **43.10%**
  - Recall : **83.33%**
  - F1-Score : **57.00%**
  - ROC-AUC : **95.82%**

Secara keseluruhan, KNN mampu meningkatkan kemampuan deteksi transaksi fraud melalui penerapan SMOTE dan hyperparameter tuning. Meskipun performanya masih berada di bawah beberapa algoritma lain seperti Random Forest maupun SVM, KNN tetap memberikan hasil yang kompetitif sebagai algoritma berbasis jarak dan menjadi pembanding yang baik dalam proyek Credit Card Fraud Detection ini.