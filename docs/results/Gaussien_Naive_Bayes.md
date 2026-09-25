# 🔔 Gaussian Naive Bayes

| Item | Value |
|------|-------|
| Algorithm | Gaussian Naive Bayes |
| Problem | Binary Classification |
| Dataset | Credit Card Fraud Detection |
| Samples | 10,000 |
| Features | 10 |
| Imbalanced Handling | SMOTE |
| Hyperparameter Tuning | GridSearchCV (5-Fold CV) |
| Best Configuration | Baseline |

---

# 📖 Deskripsi

Gaussian Naive Bayes (GNB) merupakan algoritma klasifikasi probabilistik yang didasarkan pada Teorema Bayes dengan asumsi bahwa setiap fitur bersifat independen satu sama lain. Varian "Gaussian" digunakan karena algoritma ini mengasumsikan bahwa fitur-fitur numerik (kontinu) pada dataset memiliki distribusi normal (Gaussian). Algoritma ini dikenal sangat cepat, ringan dan sering dijadikan sebagai model probabilitas dasar yang kuat.

Pada proyek ini, Gaussian Naive Bayes dievaluasi menggunakan tiga pendekatan: Baseline, penanganan imbalanced dataset dengan SMOTE serta hyperparameter tuning (mencari nilai priors dan var_smoothing terbaik) menggunakan GridSearchCV.

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

Hyperparameter tuning dilakukan menggunakan **GridSearchCV** dengan **5-Fold Cross Validation** untuk mencari penyesuaian probabilitas awal kelas (priors) dan stabilitas varians.

### Parameter yang diuji

| Parameter | Candidate |
|-----------|-----------|
| var_smoothing | 10 nilai dari np.logspace(1, -10, num=10) |
| priors | [0.99, 0.1], [0.95, 0.05], [0.90, 0.10], [0.80,0.20], [0.50, 0.50] |

---

## 🎯 Best Hyperparameter

| Parameter | Value |
|-----------|-------|
| var_smoothing | 2.78e-08(2.7825594022071144e-08) |
| priors | [0.99, 0.01] |

---

# 📊 Hasil Eksperimen

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------|---------:|----------:|-------:|---:|--------:|
| Baseline | 98.05% | 42.11% | 80% | 55.18% | 98.64% |
| SMOTE | 90.85% | 14.08% | 100.00% | 25% | 98.91% |
| Baseline + GridSearchCV | 98.35% | 46.51% | 66.67% | 54.79% | 100.00% |

---

# 📈 Confusion Matrix

<p align="center">
<img src="../images/Confusion Matrix/cm Gaussien Naive Bayes.png" width="600">
</p>

---

# 📌 Feature Importance

<p align="center">
<img src="../images/Feature Importances/Top Feature Gaussien Naive Bayes.png" width="700">
</p>

---

# 🔍 Analisis

## Baseline

Model Gaussian Naive Bayes baseline menghasilkan performa yang cukup seimbang untuk algoritma probabilistik sederhana. Model ini mencetak accuracy 98.05% dan ROC-AUC yang sangat tinggi (98.64%). Dari segi deteksi, model memiliki recall 80% (berhasil mendeteksi 80% dari total transaksi fraud) dan precision 42.11% (sekitar 42% dari tebakan fraud benar-benar fraud)

---

## SMOTE

Penerapan SMOTE secara drastis mengubah karakteristik prediksi model. Recall meningkat hingga 100% yang berarti tidak ada satupun transaksi fraud yang lolos. Namun, hal ini mengorbankan ketepatan prediksi; Precision anjlok drastis ke angka 14.08%. Akibatnya, sistem menghasilkan terlalu banyak False Positive (alarm palsu) yang ditandai dengan turunnya F1-Score menjadi 25%.

---

## Hyperparameter Tuning

Hasil tuning dengan GridSearchCV(priors menyesuaikan rasio asli dan penyesuaian var_smoothing) mencoba menyeimbangkan kembali metrik tersebut. Dibandingkan model SMOTE, Precision berhasil naik menjadi 46.51% (F1-Score 55%), namun Recall justru turun menjadi 66.67%. Menurunnya Recall berarti akan semakin banyak transaksi fraud yang gagal terdeteksi (False Negative)

Berdasarkan perbandingan di atas, model Baseline dipilih sebagai model terbaik. Model baseline memberikan trade-off yang paling masuk akal antara Precision (42.11%) dan Recall (80%) tanpa menghasilkan False Positive berlebihan seperti pada SMOTE dan tidak kehilangan kemampuan deteksi seperti pada model yang di-tuning.

---

# 💡 Interpretasi Feature Importance

Mengingat Gaussian Naive Bayes tidak memiliki atribut bawaan *.feature_importances_* seperti algoritma berbasis tree (pohon keputusan), tingkat kepetingan fitur biasanya dievaluasi menggunakan metode *Permutation Importance*. Berdasarkan hasil analisis, fitur yang berpengaruh adalah *device_trust_score* dengan nilai mean tertinggi yakni 0.062625. Fitur paling krusial yang menentukan indikasi penipuan. Sebaliknya fitur amount dengan nilai mean terendah yakni - 0.003882 menunjukkan nilai negatif yang mengindikasikan bahwa fitur ini lebih bersifat noise (tidak memberikan kontribusi signifikan atau distribusinya tumpang tindih antara kelas normal dan fraud) pada perhitungan probabilistik Naive Bayes di dataset ini.

---

# ✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan pada Gaussian Naive Bayes, dapat disimpulkan bahwa:

- Meskipun algoritma probabilistik ini sangat sederhana, model mampu memisahkan distribusi kelas dengan baik, dibuktikan dengan nilai ROC-AUC yang sangat konsisten di atas 98% pada semua skenario.
- Karakteristik GNB pada dataset ini sangat sensitif terhadap metode *oversampling*. Menggunakan SMOTE memaksa model mengklasifikasikan hampir semua borderline case sebagai fraud (Recall 100% namun precision anjlok).
- Model baseline dipilih sebagai konfigurasi terbaik karena menghasilkan keseimbangan metrik evaluasi yang paling praktis untuk diterapkan dengan hasil evaluasi:
  - Accuracy : **98.05%**
  - Precision : **42.11%**
  - Recall : **80%**
  - F1-Score : **55.18%**
  - ROC-AUC : **98.64%**

Meskipun secara absolut nilainya belum mampu menyaingi algoritma berbasis Ensemble dan Boosting, Gaussian Naive Bayes tetap menjadi baseline probabilistik yang cepat, ringan, solid untuk referensi deteksi anomali.