# 💡 LightGBM

| Item | Value |
|------|-------|
| Algorithm | LightGBM |
| Problem | Binary Classification |
| Dataset | Credit Card Fraud Detection |
| Samples | 10,000 |
| Features | 10 |
| Imbalanced Handling | Class Weight, SMOTE |
| Hyperparameter Tuning | GridSearchCV (5-Fold CV) |
| Best Configuration | Baseline + GridSearchCV |

---

# 📖 Deskripsi

LightGBM (*Light Gradient Boosting Machine*) merupakan algoritma *gradient boosting* berbasis pohon keputusan yang dikembangkan oleh Microsoft. LightGBM menggunakan pendekatan **leaf-wise tree growth**, sehingga mampu menghasilkan proses pelatihan yang lebih cepat, penggunaan memori yang lebih efisien, serta performa prediksi yang tinggi dibandingkan banyak algoritma boosting lainnya.

Pada proyek ini, LightGBM dievaluasi menggunakan beberapa strategi penanganan data tidak seimbang, yaitu **Baseline**, **Class Weight**, **SMOTE**, serta **Hyperparameter Tuning** menggunakan GridSearchCV.

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
| learning_rate | 0.01, 0.05, 0.1 |
| max_depth | -1, 3, 5, 7, 10 |
| num_leaves | 31, 50, 70 |
| min_child_samples | 10, 20, 30 |
| subsample | 0.8, 1.0 |
| colsample_bytree | 0.8, 1.0 |

---

## 🎯 Best Hyperparameter

| Parameter | Value |
|-----------|-------|
| n_estimators | 200 |
| learning_rate | 0.1 |
| max_depth | 3 |
| num_leaves | 31 |
| min_child_samples | 10 |
| subsample | 0.8 |
| colsample_bytree | 0.8 |

---

# 📊 Hasil Eksperimen

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 100% | 100% | 100% | 100% | 100% |
| Class Weight | 99.90% | 93.75% | 100% | 97% | 100% |
| SMOTE | 99.90% | 93.75% | 100% | 97% | 100% |
| Baseline + GridSearchCV | 100% | 100% | 100% | 100% | 100% |

---

# 📈 Confusion Matrix

<p align="center">
<img src="../images/Confusion Matrix/cm LightGBM.png" width="600">
</p>

---

# 📌 Feature Importance

<p align="center">
<img src="../images/Feature Importances/Top Feature LightGBM.png" width="700">
</p>

---

# 🔍 Analisis

## Baseline

Model LightGBM baseline menghasilkan performa sempurna pada data uji dengan Accuracy, Precision, Recall, F1-Score, dan ROC-AUC masing-masing mencapai **100%**. Seluruh transaksi fraud berhasil dideteksi tanpa menghasilkan *false positive* maupun *false negative*. Hasil ini menunjukkan bahwa LightGBM mampu mempelajari pola transaksi fraud secara sangat efektif pada dataset yang digunakan.

---

## Class Weight

Penerapan `class_weight='balanced'` tidak meningkatkan performa dibandingkan model baseline. Meskipun Recall tetap mencapai **100%**, Precision menurun menjadi **93.75%** sehingga muncul beberapa prediksi fraud yang sebenarnya merupakan transaksi normal. Hal ini menunjukkan bahwa pembobotan kelas membuat model menjadi lebih agresif dalam mendeteksi kelas minoritas tanpa memberikan peningkatan kemampuan deteksi.

---

## SMOTE

Pendekatan SMOTE menghasilkan performa yang identik dengan Class Weight. Recall tetap berada pada **100%**, namun Precision turun menjadi **93.75%** dibandingkan baseline. Pada dataset ini, penambahan sampel sintetis tidak memberikan keuntungan dibandingkan pelatihan menggunakan data asli.

---

## Hyperparameter Tuning

Hyperparameter tuning dilakukan menggunakan GridSearchCV pada model baseline karena pendekatan baseline telah memberikan performa terbaik pada tahap sebelumnya.

Proses tuning menghasilkan konfigurasi optimal dengan nilai **n_estimators = 200**, **learning_rate = 0.1**, **max_depth = 3**, **num_leaves = 31**, **min_child_samples = 10**, **subsample = 0.8**, dan **colsample_bytree = 0.8**.

Hasil evaluasi menunjukkan bahwa model hasil tuning mempertahankan performa sempurna yang telah dicapai model baseline, dengan Accuracy, Precision, Recall, F1-Score, dan ROC-AUC seluruhnya mencapai **100%**. Oleh karena itu, tuning tidak meningkatkan performa, tetapi berhasil menemukan konfigurasi parameter yang optimal dengan hasil yang setara.

---

# 💡 Interpretasi Feature Importance

LightGBM menghitung **Feature Importance** berdasarkan kontribusi setiap fitur selama proses pembentukan seluruh pohon keputusan pada model boosting. Nilai importance menunjukkan seberapa besar peran suatu fitur dalam mengurangi kesalahan prediksi selama proses pelatihan.

Semakin tinggi nilai Feature Importance, semakin besar kontribusi fitur tersebut terhadap proses klasifikasi. Visualisasi Feature Importance membantu mengidentifikasi fitur-fitur yang paling berpengaruh dalam mendeteksi transaksi fraud pada model LightGBM.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

- LightGBM menghasilkan performa yang sangat tinggi pada dataset Credit Card Fraud Detection.
- Model baseline telah mencapai performa sempurna dengan Accuracy, Precision, Recall, F1-Score, dan ROC-AUC sebesar **100%**.
- Pendekatan **Class Weight** maupun **SMOTE** tidak memberikan peningkatan performa dibandingkan baseline, bahkan sedikit menurunkan Precision.
- Hyperparameter tuning menggunakan **GridSearchCV** berhasil menemukan konfigurasi parameter terbaik dengan performa yang tetap setara dengan model baseline.

Model terbaik pada eksperimen ini menggunakan konfigurasi:

- Number of Estimators: **200**
- Learning Rate: **0.1**
- Maximum Depth: **3**
- Number of Leaves: **31**
- Minimum Child Samples: **10**
- Subsample: **0.8**
- Column Sample by Tree: **0.8**

dengan hasil evaluasi:

- Accuracy : **100%**
- Precision : **100%**
- Recall : **100%**
- F1-Score : **100%**
- ROC-AUC : **100%**

Secara keseluruhan, LightGBM menjadi salah satu algoritma dengan performa terbaik pada proyek ini karena mampu mengidentifikasi seluruh transaksi fraud pada data uji tanpa menghasilkan kesalahan klasifikasi.