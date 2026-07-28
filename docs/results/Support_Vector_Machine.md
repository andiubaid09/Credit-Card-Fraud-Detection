# 📈 Support Vector Machine

| Item | Value |
|------|-------|
| Algorithm | Support Vector Machine (SVM) |
| Problem | Binary Classification |
| Dataset | Credit Card Fraud Detection |
| Samples | 10,000 |
| Features | 10 |
| Imbalanced Handling | Class Weight, SMOTE |
| Hyperparameter Tuning | GridSearchCV (5-Fold CV) |
| Best Configuration | Class Weight + GridSearchCV |

---

# 📖 Deskripsi

Support Vector Machine (SVM) merupakan algoritma Machine Learning yang bekerja dengan mencari **hyperplane optimal** untuk memisahkan dua kelas. Dengan memanfaatkan **kernel function**, SVM mampu menangani data yang tidak dapat dipisahkan secara linear sehingga sering digunakan pada permasalahan klasifikasi dengan batas keputusan yang kompleks.

Pada proyek ini, SVM dievaluasi menggunakan beberapa strategi penanganan data tidak seimbang, yaitu **Baseline**, **Class Weight**, **SMOTE**, serta **Hyperparameter Tuning** menggunakan GridSearchCV.

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
| Kernel | linear, rbf, poly |
| C | 0.1, 1, 10, 100 |
| Gamma | scale, auto, 0.01 |
| Degree | 2, 3 |

---

## 🎯 Best Hyperparameter

| Parameter | Value |
|-----------|-------|
| Kernel | rbf |
| C | 100 |
| Gamma | auto |
| Degree | 2 |

---

# 📊 Hasil Eksperimen

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 99.30% | 94.44% | 56.67% | 71% | 99.59% |
| Class Weight | 98.40% | 48.21% | 90.00% | 63% | 99.61% |
| SMOTE | 98.15% | 44.26% | 90.00% | 59% | 99.62% |
| Class Weight + GridSearchCV | 99.10% | 65.00% | 86.67% | 74% | 99.49% |

---

# 📈 Confusion Matrix

<p align="center">
<img src="../images/Confusion Matrix/cm Support Vector Machine.png" width="600">
</p>

---

# 📌 Feature Importance

<p align="center">
<img src="../images/Feature Importances/Top Feature Support Vector Machine.png" width="700">
</p>

---

# 🔍 Analisis

## Baseline

Model SVM baseline menghasilkan **precision yang sangat tinggi (94.44%)**, menunjukkan bahwa sebagian besar transaksi yang diprediksi sebagai fraud merupakan prediksi yang benar. Namun, nilai **recall sebesar 56.67%** mengindikasikan bahwa masih terdapat cukup banyak transaksi fraud yang belum berhasil dideteksi. Dengan kata lain, model baseline cenderung bersifat konservatif dalam memberikan prediksi fraud.

---

## Class Weight

Penerapan `class_weight='balanced'` meningkatkan kemampuan model dalam mendeteksi transaksi fraud secara signifikan. Nilai **recall meningkat menjadi 90%**, sehingga sebagian besar transaksi fraud berhasil diidentifikasi. Namun, peningkatan tersebut diikuti oleh penurunan **precision menjadi 48.21%**, yang menunjukkan bertambahnya jumlah *false positive*. Pendekatan ini lebih sesuai apabila tujuan utama adalah meminimalkan transaksi fraud yang terlewat.

---

## SMOTE

Pendekatan **SMOTE** juga meningkatkan kemampuan deteksi fraud dengan menghasilkan **recall sebesar 90%**, sama seperti Class Weight. Akan tetapi, nilai **precision menurun menjadi 44.26%**, sehingga performanya sedikit lebih rendah dibandingkan pendekatan Class Weight. Berdasarkan hasil tersebut, SMOTE belum memberikan keseimbangan Precision dan Recall yang lebih baik pada SVM untuk dataset ini.

---

## Hyperparameter Tuning

Hyperparameter tuning dilakukan menggunakan **GridSearchCV** pada model SVM dengan pendekatan **Class Weight**, karena pendekatan tersebut memberikan keseimbangan performa terbaik sebelum proses tuning.

Proses tuning menghasilkan konfigurasi optimal yang meningkatkan kualitas prediksi model. Dibandingkan model Class Weight tanpa tuning, **Accuracy meningkat dari 98.40% menjadi 99.10%**, sementara **Precision meningkat dari 48.21% menjadi 65.00%** dengan **Recall tetap tinggi sebesar 86.67%**. Peningkatan tersebut menghasilkan **F1-Score sebesar 74%**, menunjukkan keseimbangan yang lebih baik antara kemampuan mendeteksi transaksi fraud dan mengurangi prediksi fraud yang salah.

---

# 💡 Interpretasi Model

Support Vector Machine menentukan batas keputusan (**decision boundary**) berdasarkan **support vectors**, yaitu sejumlah kecil data yang berada paling dekat dengan hyperplane. Data-data inilah yang memiliki pengaruh terbesar terhadap proses pembentukan model.

Penggunaan **kernel RBF** memungkinkan SVM mempelajari hubungan non-linear antar fitur sehingga model mampu memisahkan transaksi normal dan fraud secara lebih efektif dibandingkan pendekatan linear.

Karena menggunakan kernel **RBF**, model tidak menghasilkan **Feature Importance** atau **koefisien fitur** yang dapat diinterpretasikan secara langsung seperti pada Logistic Regression maupun algoritma berbasis Decision Tree. Oleh karena itu, interpretasi kontribusi fitur memerlukan metode *model explainability* seperti **Permutation Importance** atau **SHAP**.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

- Support Vector Machine menunjukkan performa yang sangat baik pada permasalahan Credit Card Fraud Detection dengan menghasilkan nilai Accuracy dan ROC-AUC yang tinggi pada seluruh skenario pengujian.
- Pendekatan **Class Weight** lebih efektif dibandingkan **SMOTE** dalam meningkatkan kemampuan deteksi fraud pada dataset ini, karena menghasilkan keseimbangan Precision dan Recall yang lebih baik.
- Hyperparameter tuning menggunakan **GridSearchCV** berhasil meningkatkan Accuracy, Precision, dan F1-Score tanpa mengurangi kemampuan model secara signifikan dalam mendeteksi transaksi fraud.
- Model terbaik pada eksperimen ini menggunakan konfigurasi:
  - Kernel : **RBF**
  - C : **100**
  - Gamma : **auto**
  - Degree : **2**

  dengan hasil evaluasi:
  - Accuracy : **99.10%**
  - Precision : **65.00%**
  - Recall : **86.67%**
  - F1-Score : **74.00%**
  - ROC-AUC : **99.49%**

Secara keseluruhan, Support Vector Machine menjadi salah satu model dengan performa yang cukup baik pada proyek ini. Model hasil tuning mampu memberikan keseimbangan yang baik antara kemampuan mendeteksi transaksi fraud (Recall) dan menjaga kualitas prediksi (Precision), sehingga layak dipertimbangkan sebagai salah satu model terbaik untuk kasus Credit Card Fraud Detection.