# 📂 Dataset

## 📖 Overview

Proyek ini menggunakan dataset **Credit Card Fraud Detection** yang berisi data transaksi kartu kredit untuk membangun model klasifikasi biner dalam mendeteksi transaksi fraud.

Dataset terdiri dari transaksi normal dan transaksi fraud dengan distribusi kelas yang tidak seimbang (*imbalanced dataset*), sehingga diperlukan teknik khusus untuk meningkatkan kemampuan model dalam mengenali kelas minoritas.

---

# 📊 Dataset Information

| Attribute | Value |
|-----------|-------|
| Problem Type | Binary Classification |
| Total Samples | 10,000 |
| Total Features | 10||
| Target Variable | is_fraud |
| Source | Kaggle |

---

# 🎯 Target Variable

Target yang diprediksi adalah:

| Label | Description |
|-------|-------------|
| 0 | Normal Transaction |
| 1 | Fraud Transaction |

---

# 📈 Class Distribution

Distribusi data menunjukkan ketidakseimbangan kelas yang cukup tinggi.

| Class | Total | Percentage |
|-------|-------:|-----------:|
| Normal | 9,849 | 98.49% |
| Fraud | 151 | 1.51% |

Karena hanya sekitar **1.51%** data merupakan transaksi fraud, penggunaan metrik evaluasi selain Accuracy menjadi sangat penting.

---

# 📑 Feature Description

Dataset terdiri dari delapan fitur yang digunakan sebagai variabel prediktor.

| Feature | Description |
|----------|-------------|
| transaction_id | Unique ID assigned to each transaction for identification|
| merchant_category | Category or type of the merchant business |
| amount | Transaction amount |
| transaction_hour | Hour of transaction (0–23) |
| foreign_transaction | Indicates whether the transaction occurred abroad |
| location_mismatch | Indicates whether transaction location differs from customer's usual location |
| device_trust_score | Trust score of the device used for the transaction |
| velocity_last_24h | Number of transactions within the last 24 hours |
| cardholder_age | Customer age |
| is_fraud | Target label |

---

# 🔧 Feature Engineering

Feature engineering dilakukan pada fitur waktu transaksi.

Fitur:

```
transaction_hour
```

ditransformasikan menjadi dua fitur baru menggunakan **Cyclical Encoding**.

- hour_sin
- hour_cos

Transformasi ini bertujuan agar model memahami bahwa waktu memiliki pola siklik.

Sebagai contoh:

- 23.00 berdekatan dengan 00.00
- 01.00 lebih dekat ke 00.00 dibandingkan 12.00

Setelah proses feature engineering, fitur `transaction_hour` tidak lagi digunakan secara langsung.

---

# 📋 Final Features

Fitur yang digunakan pada seluruh eksperimen adalah:

| Feature |
|----------|
| amount |
| hour_sin |
| hour_cos |
| foreign_transaction |
| location_mismatch |
| device_trust_score |
| velocity_last_24h |
| cardholder_age |

Seluruh algoritma menggunakan fitur yang sama agar hasil eksperimen dapat dibandingkan secara objektif.