# 📈 Decision Tree

| Item | Value |
|------|-------|
| Algorithm | Decision Tree |
| Problem | Binary Classification |
| Dataset | Credit Card Fraud Detection |
| Samples | 10,000 |
| Features | 10 |
| Imbalanced Handling | Class Weight, SMOTE |
| Hyperparameter Tuning | GridSearchCV (5-Fold CV) |
| Best Model | Class Weight + GridSearchCV |

---

# 📖 Deskripsi

Decision Tree merupakan algoritma klasifikasi berbasis pohon keputusan (*tree-based classifier*) yang membagi data ke dalam beberapa cabang berdasarkan fitur yang memberikan pemisahan terbaik. Berbeda dengan Logistic Regression yang membangun batas keputusan linear, Decision Tree mampu mempelajari hubungan non-linear sehingga mampu menangkap pola yang lebih kompleks pada data.

Pada proyek ini, Decision Tree dievaluasi menggunakan beberapa strategi penanganan data tidak seimbang, yaitu **Baseline**, **Class Weight**, **SMOTE**, serta **Hyperparameter Tuning** menggunakan GridSearchCV.

---

# 📚 Dokumentasi Pendukung

Beberapa tahapan umum pada seluruh eksperimen dijelaskan pada dokumentasi berikut.

- 📂 [Dataset](/docs/results/dataset.md)
- ⚙️ [Methodology](methodolgy.md)
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

# 🌳 Hyperparameter Search

Hyperparameter tuning dilakukan menggunakan **GridSearchCV** dengan **5-Fold Cross Validation**.

### Parameter yang diuji

| Parameter | Candidate |
|-----------|-----------|
| criterion | gini, entropy, log_loss |
| max_depth | None, 3, 5, 7, 10, 15 |
| min_samples_split | 2, 5, 10, 20 |
| min_samples_leaf | 1, 2, 5, 10 |
| ccp_alpha | 0.0, 0.001, 0.005, 0.01 |

---

## 🎯 Best Hyperparameter

| Parameter | Value |
|-----------|-------|
| Criterion | entropy |
| Max Depth | 10 |
| Min Samples Split | 2 |
| Min Samples Leaf | 1 |
| CCP Alpha | 0.0 |

---

# 📊 Hasil Eksperimen

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 99.75% | 86% | 100% | 92% | 99.87% |
| Class Weight | 99.80% | 88% | 100% | 94% | 99.89% |
| SMOTE | 99.60% | 81% | 97% | 88% | 98.15% |
| Class Weight + GridSearchCV | 99.90% | 94% | 100% | 97% | 99.95% |

---

# 📈 Confusion Matrix

<p align="center">
<img src="/docs/images/Confusion Matrix/cm Decision Tree.png" width="600">
</p>

---

# 📌 Feature Importance

<p align="center">
<img src="../images/Feature Importances/Top Feature Decision Tree.png" width="700">
</p>

---

# 🔍 Analisis

## Baseline

Model Decision Tree baseline menghasilkan performa yang cukup baik dengan **Accuracy sebesar 99.75%**, **Precision 86%**, dan **Recall 100%**. Dibandingkan Logistic Regression baseline, Decision Tree mampu mendeteksi lebih banyak transaksi fraud sehingga menghasilkan keseimbangan yang lebih baik antara Precision dan Recall.

---

## Class Weight

Penerapan `class_weight='balanced'` bertujuan memberikan perhatian lebih besar terhadap kelas minoritas. Namun pada eksperimen ini, pendekatan tersebut mengalami peningkatan performa dibandingkan model baseline. Accuracy pada 99.80%, Precision 88%, Recall 100%, dan F1-Score 94% menunjukkan sedikit peningkatan pada model Decision Tree.

---

## SMOTE

SMOTE digunakan untuk menghasilkan sampel sintetis pada kelas fraud sehingga distribusi data menjadi lebih seimbang. Pendekatan ini dievaluasi untuk melihat pengaruh oversampling terhadap kemampuan Decision Tree dalam mendeteksi transaksi fraud. Hasil lengkap dapat dilihat pada tabel hasil eksperimen.

---

## Hyperparameter Tuning

Hyperparameter tuning menggunakan GridSearchCV menghasilkan peningkatan performa dibandingkan model class-weight.

Perubahan yang diperoleh meliputi:

- Accuracy meningkat dari **99.80% menjadi 99.90%**
- Precision meningkat dari **88% menjadi 94%**
- Recall tetap dari **100% menjadi 100%**
- F1-Score meningkat dari **94% menjadi 97%**
- ROC-AUC meningkat dari **99.89% menjadi 99.95%**

Peningkatan tersebut menunjukkan bahwa optimasi hyperparameter berhasil menghasilkan model yang lebih baik dalam membedakan transaksi fraud dan transaksi normal tanpa mengorbankan keseimbangan antara Precision dan Recall.

---

# 💡 Interpretasi Feature Importance

Decision Tree menghitung **Feature Importance** berdasarkan seberapa besar setiap fitur berkontribusi dalam mengurangi impurity (*Gini* atau *Entropy*) selama proses pembentukan pohon keputusan.

- Nilai Feature Importance yang lebih besar menunjukkan bahwa suatu fitur lebih sering digunakan untuk membagi node pada pohon keputusan.
- Semakin tinggi nilainya, semakin besar kontribusi fitur tersebut terhadap proses klasifikasi.
- Feature Importance membantu mengidentifikasi faktor-faktor yang paling berpengaruh dalam mendeteksi transaksi fraud.

Visualisasi di atas memberikan gambaran mengenai fitur-fitur yang paling berkontribusi terhadap keputusan model.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

- Decision Tree mampu mempelajari hubungan non-linear antar fitur dengan baik.
- Hyperparameter tuning berhasil meningkatkan performa model secara signifikan dibandingkan model class weight.
- Model terbaik diperoleh menggunakan **class-weight + GridSearchCV** dengan Accuracy **99.90%**, Precision **94%**, Recall **100%**, F1-Score **97%**, dan ROC-AUC **99.95%**.
- Dibandingkan Logistic Regression, Decision Tree memberikan keseimbangan yang lebih baik antara Precision dan Recall sehingga lebih efektif dalam mendeteksi transaksi fraud tanpa menghasilkan terlalu banyak *false positive*.

Secara keseluruhan, Decision Tree menunjukkan performa yang sangat kompetitif pada dataset Credit Card Fraud Detection. Kemampuannya dalam mempelajari hubungan non-linear, dikombinasikan dengan hyperparameter tuning, menghasilkan model yang lebih seimbang dalam mendeteksi transaksi fraud sekaligus mempertahankan tingkat kesalahan prediksi yang rendah.