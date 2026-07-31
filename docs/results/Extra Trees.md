# 🌳 Extra Trees

| Item | Value |
|------|-------|
| Algorithm | Extra Trees |
| Problem | Binary Classification |
| Dataset | Credit Card Fraud Detection |
| Samples | 10,000 |
| Features | 10 |
| Imbalanced Handling | Class Weight, SMOTE |
| Hyperparameter Tuning | GridSearchCV (5-Fold CV) |
| Best Configuration | SMOTE + GridSearchCV |

---

# 📖 Deskripsi

Extra Trees (*Extremely Randomized Trees*) merupakan algoritma *ensemble learning* berbasis kumpulan Decision Tree yang memperkenalkan tingkat randomisasi lebih tinggi dibandingkan Random Forest. Selain menggunakan subset data secara acak, Extra Trees juga memilih titik pemisahan (*split point*) secara acak sehingga mampu mengurangi varians model, meningkatkan kemampuan generalisasi, serta mengurangi risiko overfitting.

Pada proyek ini, Extra Trees dievaluasi menggunakan beberapa pendekatan, yaitu **Baseline**, **Class Weight**, **SMOTE**, serta **Hyperparameter Tuning** menggunakan GridSearchCV.

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
| n_estimators | 100, 200, 250 |
| criterion | gini, entropy |
| max_depth | None, 10, 20 |
| min_samples_split | 2, 5, 8 |
| min_samples_leaf | 1, 2, 5 |
| max_features | sqrt, log2 |

---

## 🎯 Best Hyperparameter

| Parameter | Value |
|-----------|-------|
| n_estimators | 250 |
| criterion | gini |
| max_depth | None |
| min_samples_split | 8 |
| min_samples_leaf | 2 |
| max_features | log2 |

---

# 📊 Hasil Eksperimen

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 99.55% | 100.00% | 70.00% | 82% | 99.85% |
| Class Weight | 99.40% | 100.00% | 60.00% | 75% | 99.80% |
| SMOTE | 99.70% | 90.00% | 90.00% | 90% | 99.87% |
| SMOTE + GridSearchCV | 99.55% | 80.00% | 93.33% | 86% | 99.93% |

---

# 📈 Confusion Matrix

<p align="center">
<img src="../images/Confusion Matrix/cm Extra Trees.png" width="600">
</p>

---

# 📌 Feature Importance

<p align="center">
<img src="../images/Feature Importances/Top Feature Extra Trees.png" width="700">
</p>

---

# 🔍 Analisis

## Baseline

Model Extra Trees baseline menunjukkan performa yang sangat baik dengan Precision mencapai **100%**, yang berarti seluruh transaksi yang diprediksi sebagai fraud merupakan prediksi yang benar. Namun, Recall sebesar **70%** menunjukkan bahwa masih terdapat beberapa transaksi fraud yang belum berhasil dideteksi. Hasil ini menunjukkan bahwa model baseline cenderung lebih konservatif dalam memberikan prediksi fraud.

---

## Class Weight

Penerapan **class_weight='balanced'** tidak memberikan peningkatan performa dibandingkan model baseline. Meskipun Precision tetap berada pada **100%**, Recall menurun menjadi **60%** sehingga lebih banyak transaksi fraud yang tidak berhasil diidentifikasi. Berdasarkan hasil eksperimen ini, pendekatan Class Weight kurang efektif untuk meningkatkan performa Extra Trees pada dataset yang digunakan.

---

## SMOTE

Penerapan **SMOTE** menghasilkan peningkatan performa yang signifikan. Precision dan Recall sama-sama mencapai **90%**, menghasilkan **F1-Score sebesar 90%**, yang menunjukkan keseimbangan yang sangat baik antara kemampuan mendeteksi transaksi fraud dan menjaga kualitas prediksi. Selain itu, Accuracy meningkat menjadi **99.70%** dengan ROC-AUC sebesar **99.87%**, sehingga pendekatan SMOTE memberikan performa terbaik pada tahap sebelum dilakukan hyperparameter tuning.

---

## Hyperparameter Tuning

Hyperparameter tuning dilakukan menggunakan **GridSearchCV** pada model **SMOTE**, karena pendekatan tersebut memberikan keseimbangan performa terbaik pada tahap sebelumnya.

Proses tuning menghasilkan konfigurasi terbaik berdasarkan hasil pencarian parameter menggunakan validasi silang. Pada data uji, Recall meningkat dari **90%** menjadi **93.33%**, sehingga lebih banyak transaksi fraud berhasil dideteksi. Selain itu, ROC-AUC juga meningkat menjadi **99.93%**.

Namun demikian, peningkatan Recall diikuti dengan penurunan Precision dari **90%** menjadi **80%**, sehingga F1-Score turun dari **90%** menjadi **86%**. Berdasarkan hasil evaluasi pada data uji, model **SMOTE tanpa tuning** memberikan keseimbangan Precision dan Recall yang lebih baik dibandingkan model hasil tuning, meskipun model tuning memiliki Recall dan ROC-AUC yang sedikit lebih tinggi.

---

# 💡 Interpretasi Feature Importance

Extra Trees menghitung **Feature Importance** berdasarkan rata-rata penurunan impurity (*Mean Decrease in Impurity*) dari seluruh pohon keputusan yang membentuk model. Nilai tersebut menunjukkan seberapa besar kontribusi masing-masing fitur dalam proses klasifikasi.

Semakin tinggi nilai Feature Importance, semakin besar pengaruh fitur tersebut terhadap prediksi model. Karena dihitung dari banyak pohon keputusan yang dibangun secara acak, nilai Feature Importance pada Extra Trees cenderung stabil serta mampu memberikan gambaran yang baik mengenai fitur-fitur yang paling berkontribusi dalam mendeteksi transaksi fraud.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

- Extra Trees menghasilkan performa yang sangat baik pada permasalahan Credit Card Fraud Detection dengan Accuracy dan ROC-AUC yang tinggi pada seluruh skenario pengujian.
- Pendekatan **SMOTE** memberikan keseimbangan terbaik antara Precision dan Recall dengan menghasilkan **Precision 90%**, **Recall 90%**, dan **F1-Score 90%**.
- Hyperparameter tuning menggunakan **GridSearchCV** berhasil meningkatkan Recall menjadi **93.33%** dan ROC-AUC menjadi **99.93%**, namun diikuti penurunan Precision sehingga F1-Score sedikit menurun.
- Model hasil tuning menggunakan konfigurasi:
  - Criterion: **Gini**
  - Max Depth: **None**
  - Max Features: **log2**
  - Min Samples Leaf: **2**
  - Min Samples Split: **8**
  - Number of Estimators: **250**

  dengan hasil evaluasi:
  - Accuracy : **99.55%**
  - Precision : **80.00%**
  - Recall : **93.33%**
  - F1-Score : **86.00%**
  - ROC-AUC : **99.93%**

Secara keseluruhan, Extra Trees menunjukkan performa yang sangat kompetitif pada proyek ini. Berdasarkan hasil evaluasi pada data uji, pendekatan **SMOTE tanpa tuning** memberikan keseimbangan terbaik antara Precision dan Recall, sedangkan model hasil tuning lebih unggul dalam Recall dan ROC-AUC sehingga lebih sesuai apabila prioritas utama adalah meminimalkan transaksi fraud yang tidak terdeteksi.