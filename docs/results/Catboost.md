# 🐱 CatBoost

| Item | Value |
|------|-------|
| Algorithm | CatBoost |
| Problem | Binary Classification |
| Dataset | Credit Card Fraud Detection |
| Samples | 10,000 |
| Features | 10 |
| Imbalanced Handling | SMOTE |
| Hyperparameter Tuning | GridSearchCV (5-Fold CV) |
| Best Configuration | Baseline + GridSearchCV |

---

# 📖 Deskripsi

CatBoost merupakan algoritma *gradient boosting* yang dikembangkan oleh Yandex dan dirancang untuk menghasilkan performa tinggi dengan proses pelatihan yang efisien. Algoritma ini menggunakan teknik *ordered boosting* untuk mengurangi prediction shift selama proses training serta mampu memberikan kemampuan generalisasi yang baik pada berbagai permasalahan klasifikasi maupun regresi.

Pada proyek ini, CatBoost dievaluasi menggunakan beberapa strategi penanganan data tidak seimbang, yaitu **Baseline**, **SMOTE**, serta **Hyperparameter Tuning** menggunakan GridSearchCV. Pendekatan **Class Weight** tidak digunakan karena implementasi parameter pembobotan pada CatBoost berbeda dengan mekanisme `class_weight='balanced'` yang digunakan secara konsisten pada algoritma lain dalam penelitian ini.

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
| iterations | 100, 150, 200 |
| depth | 4, 6, 8 |
| learning_rate | 0.01, 0.05, 0.1 |
| l2_leaf_reg | 3, 5, 7 |
| subsample | 0.8, 1.0 |

---

## 🎯 Best Hyperparameter

| Parameter | Value |
|-----------|-------|
| iterations | 200 |
| depth | 8 |
| learning_rate | 0.1 |
| l2_leaf_reg | 3 |
| subsample | 1.0 |

---

# 📊 Hasil Eksperimen

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 100.00% | 100.00% | 100.00% | 100.00% | 100.00% |
| SMOTE | 99.90% | 93.75% | 100.00% | 96.77% | 99.95% |
| Baseline + GridSearchCV | 100.00% | 100.00% | 100.00% | 100.00% | 100.00% |

---

# 📈 Confusion Matrix

<p align="center">
<img src="../images/Confusion Matrix/cm CatBoost.png" width="600">
</p>

---

# 📌 Feature Importance

<p align="center">
<img src="../images/Feature Importances/Top Feature CatBoost.png" width="700">
</p>

---

# 🔍 Analisis

## Baseline

Model CatBoost baseline berhasil mencapai performa sempurna pada data uji dengan Accuracy, Precision, Recall, F1-Score, dan ROC-AUC masing-masing sebesar **100%**. Hasil ini menunjukkan bahwa seluruh transaksi fraud maupun transaksi normal berhasil diklasifikasikan dengan benar tanpa kesalahan prediksi.

---

## SMOTE

Penerapan SMOTE tidak memberikan peningkatan performa dibandingkan model baseline. Meskipun Recall tetap mencapai **100%**, Precision menurun menjadi **93.75%** sehingga F1-Score juga mengalami sedikit penurunan. Hal ini menunjukkan bahwa CatBoost telah mampu mempelajari pola kelas minoritas dengan sangat baik tanpa memerlukan proses oversampling.

---

## Hyperparameter Tuning

Hyperparameter tuning dilakukan menggunakan GridSearchCV pada model baseline karena model tersebut telah memberikan performa terbaik pada tahap eksperimen sebelumnya.

Hasil tuning menghasilkan konfigurasi optimal dengan **200 iterations**, **depth 8**, **learning rate 0.1**, **L2 regularization sebesar 3**, dan **subsample 1.0**. Evaluasi pada data uji tetap menghasilkan performa sempurna dengan seluruh metrik bernilai **100%**.

Berdasarkan hasil tersebut, model hasil tuning dipilih sebagai model terbaik karena mempertahankan performa optimal sekaligus menggunakan konfigurasi hyperparameter yang telah divalidasi melalui proses pencarian parameter.

---

# 💡 Interpretasi Feature Importance

CatBoost menghitung **Feature Importance** berdasarkan kontribusi masing-masing fitur terhadap proses pembentukan model selama pelatihan. Nilai importance menggambarkan seberapa besar pengaruh suatu fitur dalam meningkatkan kualitas prediksi pada seluruh pohon keputusan yang membentuk model.

Semakin tinggi nilai Feature Importance, semakin besar kontribusi fitur tersebut dalam proses klasifikasi. Visualisasi berikut membantu mengidentifikasi fitur-fitur yang paling berpengaruh dalam mendeteksi transaksi fraud menggunakan CatBoost.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

- CatBoost menunjukkan performa yang sangat baik pada permasalahan Credit Card Fraud Detection dengan menghasilkan nilai Accuracy, Precision, Recall, F1-Score, dan ROC-AUC yang sangat tinggi.
- Model baseline telah mampu mencapai performa sempurna tanpa memerlukan proses penanganan data tidak seimbang menggunakan SMOTE.
- Hyperparameter tuning menggunakan GridSearchCV berhasil memperoleh konfigurasi terbaik tanpa mengubah performa model, yang menunjukkan bahwa konfigurasi baseline CatBoost sudah sangat sesuai untuk dataset ini.
- Model terbaik pada eksperimen ini menggunakan konfigurasi:
  - Iterations: **200**
  - Depth: **8**
  - Learning Rate: **0.1**
  - L2 Leaf Regularization: **3**
  - Subsample: **1.0**

  dengan hasil evaluasi:
  - Accuracy : **100.00%**
  - Precision : **100.00%**
  - Recall : **100.00%**
  - F1-Score : **100.00%**
  - ROC-AUC : **100.00%**

Secara keseluruhan, CatBoost menjadi salah satu algoritma dengan performa terbaik pada proyek ini. Model mampu mengklasifikasikan seluruh transaksi pada data uji dengan benar serta menunjukkan kemampuan yang sangat baik dalam mendeteksi transaksi fraud tanpa memerlukan teknik penyeimbangan data tambahan.