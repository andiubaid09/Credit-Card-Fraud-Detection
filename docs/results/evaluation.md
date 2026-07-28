# 📊 Model Evaluation

## 📖 Overview

Seluruh algoritma dievaluasi menggunakan metrik klasifikasi yang sama sehingga performa masing-masing model dapat dibandingkan secara objektif.

Karena dataset bersifat **imbalanced**, evaluasi tidak hanya berfokus pada Accuracy, tetapi juga mempertimbangkan Precision, Recall, F1-Score, ROC-AUC, dan Confusion Matrix.

---

# 🎯 Accuracy

Accuracy mengukur persentase prediksi yang benar terhadap seluruh data uji.

Formula:

```
Accuracy = (TP + TN) / (TP + TN + FP + FN)
```

Kelemahan Accuracy pada dataset tidak seimbang adalah nilai yang tinggi belum tentu menunjukkan kemampuan model dalam mendeteksi transaksi fraud.

---

# 🎯 Precision

Precision mengukur seberapa banyak prediksi fraud yang benar-benar merupakan fraud.

Formula:

```
Precision = TP / (TP + FP)
```

Semakin tinggi Precision, semakin sedikit transaksi normal yang salah diklasifikasikan sebagai fraud (*False Positive*).

---

# 🎯 Recall

Recall mengukur kemampuan model dalam mendeteksi seluruh transaksi fraud.

Formula:

```
Recall = TP / (TP + FN)
```

Pada kasus **Credit Card Fraud Detection**, Recall merupakan salah satu metrik yang sangat penting karena transaksi fraud yang tidak terdeteksi (*False Negative*) dapat menyebabkan kerugian finansial.

---

# 🎯 F1-Score

F1-Score merupakan rata-rata harmonik antara Precision dan Recall.

Formula:

```
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

F1-Score memberikan gambaran keseimbangan antara Precision dan Recall.

---

# 🎯 ROC-AUC

ROC-AUC (*Receiver Operating Characteristic - Area Under Curve*) mengukur kemampuan model dalam membedakan transaksi fraud dan transaksi normal pada berbagai nilai threshold.

Interpretasi umum ROC-AUC:

| ROC-AUC | Interpretation |
|---------:|---------------|
| 0.50 | No discrimination |
| 0.60–0.70 | Poor |
| 0.70–0.80 | Fair |
| 0.80–0.90 | Good |
| 0.90–1.00 | Excellent |

Semakin mendekati **1.00**, semakin baik kemampuan model membedakan kedua kelas.

---

# 📊 Confusion Matrix

Confusion Matrix digunakan untuk melihat jumlah prediksi yang benar maupun salah.

| | Predicted Normal | Predicted Fraud |
|---|---:|---:|
| **Actual Normal** | True Negative (TN) | False Positive (FP) |
| **Actual Fraud** | False Negative (FN) | True Positive (TP) |

Interpretasi:

- **True Positive (TP)** : Fraud berhasil dideteksi.
- **True Negative (TN)** : Transaksi normal berhasil diprediksi dengan benar.
- **False Positive (FP)** : Transaksi normal diprediksi sebagai fraud.
- **False Negative (FN)** : Transaksi fraud diprediksi sebagai normal.

Pada deteksi fraud, **False Negative** merupakan kesalahan yang paling berisiko karena transaksi fraud gagal terdeteksi.

---

# 📈 Model Interpretation

Selain metrik evaluasi, setiap algoritma juga dianalisis menggunakan metode interpretasi yang sesuai.

| Algorithm | Interpretation Method |
|------------|----------------------|
| Logistic Regression | Feature Coefficients |
| Decision Tree | Feature Importance |
| Random Forest | Feature Importance |
| Support Vector Machine | Permutation Importance |
| K-Nearest Neighbor | Permutation Importance |
| XGBoost | Feature Importance & SHAP |
| LightGBM | Feature Importance & SHAP |
| CatBoost | Feature Importance & SHAP |

Pendekatan ini digunakan untuk mengetahui fitur yang paling berpengaruh terhadap proses klasifikasi.

---

# 🏆 Model Selection

Pemilihan model terbaik tidak hanya didasarkan pada Accuracy, tetapi mempertimbangkan seluruh metrik evaluasi.

Kriteria utama yang digunakan dalam proyek ini adalah:

1. Kemampuan mendeteksi transaksi fraud (Recall).
2. Kemampuan mengurangi False Positive (Precision).
3. Keseimbangan antara Precision dan Recall (F1-Score).
4. Kemampuan diskriminasi model (ROC-AUC).

Dengan pendekatan tersebut, model terbaik dipilih berdasarkan performa keseluruhan sesuai karakteristik permasalahan Credit Card Fraud Detection.