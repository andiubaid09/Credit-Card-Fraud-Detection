# 📈 Logistic Regression

| Item | Value |
|------|-------|
| Algorithm | Logistic Regression |
| Problem | Binary Classification |
| Dataset | Credit Card Fraud Detection |
| Samples | 10,000 |
| Features | 8 |
| Imbalanced Handling | Class Weight, SMOTE |
| Hyperparameter Tuning | GridSearchCV (5-Fold CV) |
| Best Model | SMOTE + GridSearchCV |

---

# 📖 Deskripsi

Logistic Regression merupakan algoritma klasifikasi linear yang digunakan untuk memprediksi probabilitas suatu observasi termasuk ke dalam salah satu dari dua kelas. Pada proyek ini, Logistic Regression digunakan sebagai **baseline model** karena memiliki interpretabilitas yang tinggi, proses pelatihan yang cepat, serta sering dijadikan acuan dalam permasalahan klasifikasi biner seperti deteksi transaksi fraud.

Seluruh eksperimen dilakukan menggunakan workflow yang konsisten sehingga hasilnya dapat dibandingkan secara objektif dengan algoritma Machine Learning lainnya.

---

# 📚 Dokumentasi Pendukung

Beberapa tahapan umum pada seluruh eksperimen dijelaskan pada dokumentasi berikut.

- 📂 [Dataset](/docs/results/dataset.md)
- ⚙️ [Methodology](/docs/results/methodolgy.md)
- 📊 [Evaluation Metrics](/docs/results/evaluation.md)

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
| penalty | l1, l2 |
| C | 0.01, 0.1, 1, 10, 100 |
| solver | liblinear, lbfgs, newton-cg |
| max_iter | 1000, 2000 |

---

## 🎯 Best Hyperparameter

| Parameter | Value |
|-----------|-------|
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

Model baseline menghasilkan akurasi yang tinggi (**98.95%**), namun hanya mampu mendeteksi sekitar **50%** transaksi fraud. Hal ini menunjukkan bahwa Accuracy saja kurang cukup untuk mengevaluasi model pada dataset yang tidak seimbang.

---

## Class Weight

Pendekatan `class_weight='balanced'` meningkatkan Recall menjadi **100%**, sehingga seluruh transaksi fraud berhasil dideteksi. Namun peningkatan tersebut menyebabkan Precision turun menjadi **24%**, yang menunjukkan meningkatnya jumlah *false positive*.

---

## SMOTE

SMOTE menghasilkan keseimbangan performa yang lebih baik dibandingkan Class Weight. Recall tetap mencapai **100%**, sedangkan Precision meningkat menjadi **27%**. Hal ini menunjukkan bahwa oversampling sintetis membantu model mempelajari pola transaksi fraud dengan lebih efektif.

---

## Hyperparameter Tuning

Hyperparameter tuning menggunakan GridSearchCV memberikan peningkatan kecil dibandingkan model SMOTE.

Perubahan performa meliputi:

- Accuracy meningkat dari **96.00%** menjadi **96.20%**
- Precision meningkat dari **27%** menjadi **28%**
- F1-Score meningkat dari **43%** menjadi **44%**
- Recall tetap berada pada **100%**

Walaupun peningkatannya relatif kecil, hasil tuning menunjukkan bahwa optimasi parameter mampu meningkatkan performa model tanpa mengurangi kemampuan mendeteksi transaksi fraud.

---

# 💡 Interpretasi Feature Coefficients

Logistic Regression merupakan model linear sehingga setiap koefisien menunjukkan kontribusi masing-masing fitur terhadap probabilitas suatu transaksi diklasifikasikan sebagai fraud.

- Koefisien positif meningkatkan probabilitas transaksi diprediksi sebagai fraud.
- Koefisien negatif menurunkan probabilitas transaksi diprediksi sebagai fraud.
- Semakin besar nilai absolut koefisien, semakin besar pengaruh fitur terhadap keputusan model.

Visualisasi Feature Coefficients membantu mengidentifikasi fitur yang paling berkontribusi dalam proses klasifikasi.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

- Logistic Regression memberikan performa baseline yang kuat untuk permasalahan Credit Card Fraud Detection.
- Penanganan data tidak seimbang menggunakan **SMOTE** secara signifikan meningkatkan kemampuan model dalam mendeteksi transaksi fraud.
- Hyperparameter tuning memberikan peningkatan performa meskipun tidak terlalu besar.
- Model terbaik pada eksperimen ini adalah **SMOTE + GridSearchCV**, dengan Accuracy **96.20%**, Precision **28%**, Recall **100%**, F1-Score **44%**, dan ROC-AUC **99.32%**.

Secara keseluruhan, Logistic Regression menunjukkan bahwa model linear masih mampu memberikan performa yang kompetitif pada dataset Credit Card Fraud Detection. Meskipun Precision relatif rendah setelah penanganan data tidak seimbang, model berhasil mendeteksi seluruh transaksi fraud pada data uji sehingga sangat sesuai apabila prioritas utama adalah meminimalkan *false negative*.