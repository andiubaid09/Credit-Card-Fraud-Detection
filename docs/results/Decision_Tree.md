📈 Decision Tree
📖 Deskripsi

Decision Tree merupakan algoritma klasifikasi berbasis pohon keputusan (tree-based classifier) yang membagi data ke dalam beberapa cabang berdasarkan fitur yang memberikan pemisahan terbaik. Berbeda dengan Logistic Regression yang membangun batas keputusan linear, Decision Tree mampu mempelajari hubungan non-linear sehingga sering digunakan sebagai salah satu model dasar dalam berbagai permasalahan klasifikasi.

Pada proyek ini, Decision Tree dievaluasi menggunakan beberapa strategi penanganan data tidak seimbang, yaitu baseline, class weight, SMOTE, serta hyperparameter tuning menggunakan GridSearchCV.

⚙️ Workflow

Workflow lengkap dapat dilihat pada:

➡️ Methodology

🌳 Hyperparameter Search

Hyperparameter terbaik diperoleh menggunakan GridSearchCV dengan 5-Fold Cross Validation.

Parameter yang diuji:

Parameter	Candidate
criterion	gini, entropy
max_depth	None, 5, 10, 15, 20
min_samples_split	2, 5, 10
min_samples_leaf	1, 2, 4
ccp_alpha	0.0, 0.001, 0.01
🎯 Best Hyperparameter
Parameter	Nilai
Criterion	entropy
Max Depth	10
Min Samples Split	5
Min Samples Leaf	1
CCP Alpha	0.0
📊 Hasil Eksperimen
Model	Accuracy	Precision	Recall	F1	ROC-AUC
Baseline	98.80%	58%	70%	64%	84.62%
Class Weight	98.55%	54%	67%	60%	83.20%
SMOTE	(isi sesuai hasil Anda)	(isi)	(isi)	(isi)	(isi)
Baseline + GridSearchCV	99.20%	71%	80%	75%	94.74%

Ganti baris SMOTE dengan hasil eksperimen Decision Tree SMOTE yang sudah Anda miliki.

🔍 Analisis
Baseline

Model Decision Tree baseline menghasilkan performa yang cukup baik dengan akurasi sebesar 98.80% dan F1-Score sebesar 64%. Model mampu mendeteksi sekitar 70% transaksi fraud, namun masih terdapat sejumlah transaksi fraud yang salah diklasifikasikan sebagai transaksi normal.

Class Weight

Penerapan Class Weight bertujuan meningkatkan perhatian model terhadap kelas minoritas. Namun pada eksperimen ini peningkatan tersebut belum memberikan hasil yang lebih baik dibandingkan baseline sehingga Decision Tree masih mengalami kesulitan dalam mempertahankan keseimbangan antara precision dan recall.

SMOTE

SMOTE digunakan untuk menghasilkan sampel sintetis pada kelas fraud sehingga distribusi data menjadi lebih seimbang. Hasil eksperimen menunjukkan perubahan performa dibandingkan baseline. Analisis akhir mengikuti nilai yang diperoleh pada notebook.

Hyperparameter Tuning

Hyperparameter tuning menghasilkan peningkatan performa dibandingkan model baseline.

Perubahan yang diperoleh antara lain:

Accuracy meningkat menjadi 99.20%
Precision meningkat menjadi 71%
Recall meningkat menjadi 80%
F1-Score meningkat menjadi 75%

Model hasil tuning mampu memberikan keseimbangan yang lebih baik antara precision dan recall sehingga menjadi model terbaik pada eksperimen Decision Tree.

📈 Confusion Matrix
<p align="center"> <img src="../images/Confusion Matrix/cm Decision Tree.png" width="600"> </p>
📌 Feature Importance
<p align="center"> <img src="../images/Feature Importances/Top Feature Decision Tree.png" width="700"> </p>
💡 Interpretasi Feature Importance

Decision Tree menghitung Feature Importance berdasarkan seberapa besar setiap fitur berkontribusi dalam mengurangi impurity (Gini atau Entropy) selama proses pembentukan pohon keputusan.

Semakin tinggi nilai Feature Importance, semakin besar kontribusi fitur tersebut dalam proses klasifikasi transaksi fraud.

Visualisasi Feature Importance memberikan gambaran fitur-fitur yang paling berpengaruh terhadap keputusan model.

✅ Kesimpulan

Berdasarkan seluruh eksperimen yang dilakukan, dapat disimpulkan bahwa:

Decision Tree mampu mempelajari hubungan non-linear antar fitur dengan baik.
Hyperparameter tuning berhasil meningkatkan performa model dibandingkan baseline.
Model terbaik diperoleh menggunakan Baseline + GridSearchCV dengan Accuracy 99.20%, Precision 71%, Recall 80%, F1-Score 75%, dan ROC-AUC 94.74%.
Dibandingkan Logistic Regression, Decision Tree memberikan keseimbangan yang lebih baik antara precision dan recall sehingga lebih efektif dalam mendeteksi transaksi fraud tanpa menghasilkan terlalu banyak false positive.