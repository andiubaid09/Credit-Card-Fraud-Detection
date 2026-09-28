# 🧠 Multi-Layer Perceptron (Neural Network)

| Item | Value |
| :--- | :--- |
| **Algorithm** | Multi-Layer Perceptron (MLP) |
| **Problem** | Binary Classification |
| **Dataset** | Credit Card Fraud Detection |
| **Framework** | TensorFlow / Keras |
| **Imbalanced Handling** | Class Weight, SMOTE |
| **Hyperparameter Tuning** | Architecture Tuning |
| **Best Configuration** | **Tuned Baseline** |

### 📖 Deskripsi

Multi-Layer Perceptron (MLP) adalah kelas dari *feed-forward Artificial Neural Network* (ANN) yang terdiri dari setidaknya tiga lapisan node: lapisan input, lapisan tersembunyi (*hidden layer*), dan lapisan output. Algoritma ini menggunakan teknik *backpropagation* untuk pelatihan. MLP sangat tangguh dalam menangani data yang tidak dapat dipisahkan secara linear karena kemampuannya mempelajari representasi fitur yang sangat kompleks melalui fungsi aktivasi non-linear.

Pada eksperimen ini, model MLP dibangun menggunakan framework **Keras/TensorFlow**. Evaluasi dilakukan secara bertahap mulai dari Arsitektur Baseline, penggunaan Class Weight, implementasi SMOTE, hingga Tuning Arsitektur untuk mendapatkan konfigurasi jaringan terbaik.

### ⚙️ Arsitektur Jaringan

**1. Arsitektur Baseline**
Model dasar dibangun dengan struktur sederhana yang berfokus pada pencegahan *overfitting* menggunakan *Dropout*:
* **Input Layer** menyesuaikan dimensi fitur.
* **Hidden Layer 1**: Dense (64 units), fungsi aktivasi `ReLU`.
* **Dropout**: Rate 0.3.
* **Hidden Layer 2**: Dense (32 units), fungsi aktivasi `ReLU`.
* **Dropout**: Rate 0.2.
* **Output Layer**: Dense (1 unit), fungsi aktivasi `Sigmoid` untuk probabilitas klasifikasi biner.

**2. Arsitektur Hasil Tuning (Best Model)**
Berdasarkan hasil eksperimen, arsitektur dasar dimodifikasi (*tuned*) untuk mengoptimalkan stabilisasi gradien dan mempercepat konvergensi menggunakan *Normalization* dan *Batch Normalization*:
* **Input Layer**: `(None, 8)`
* **Normalization Layer**: Mengamankan skala fitur langsung di dalam jaringan.
* **Hidden Layer**: Dense (128 units) yang lebih lebar untuk menangkap representasi lebih banyak.
* **Batch Normalization**: Menstabilkan input pada layer aktivasi.
* **Activation**: `ReLU` (direpresentasikan terpisah).
* **Dropout Layer**: Mencegah overfitting.
* **Output Layer**: Dense (1 unit, `Sigmoid`).

*Total params: 1,682 (6.57 KB)* | *Trainable params: 1,409 (5.50 KB)*

### 🔍 Analisis

**Baseline**

Arsitektur baseline mencatatkan performa awal yang cukup baik dengan **Accuracy 99.15%** dan **ROC-AUC 99.47%**. Namun, karena ketidakseimbangan kelas pada data, model ini memiliki **Recall 66.67%**, yang artinya sekitar sepertiga dari total transaksi penipuan (*fraud*) gagal dideteksi oleh sistem, meskipun prediksi positifnya cukup akurat (**Precision 74.07%**).

**Class Weight**

Untuk memaksa jaringan lebih memperhatikan kelas minoritas (fraud), parameter `class_weight` diterapkan. Pendekatan ini secara instan mendongkrak **Recall menjadi 96.67%** (hampir semua fraud terdeteksi). Sayangnya, penalti yang terlalu besar untuk kelas normal membuat model menjadi terlalu sensitif, sehingga **Precision anjlok drastis ke 32.22%**. Hal ini memicu banyaknya peringatan palsu (*False Positives*).

**SMOTE**

Pendekatan oversampling dengan SMOTE memberikan keseimbangan yang lebih baik dibandingkan Class Weight. Model mampu mencapai **Recall 93.33%** dengan **Precision 54.90%** (F1-Score 69.14%). Model SMOTE berhasil mendeteksi sebagian besar transaksi fraud dengan tingkat kesalahan tebakan (*False Positive*) yang lebih bisa ditoleransi dibandingkan model Class Weight.

**Hyperparameter / Architecture Tuning**

Melanjutkan dengan data SMOTE, eksperimen dilanjutkan dengan melakukan *tuning* arsitektur pada data baseline. Jaringan diperlebar menjadi 128 unit (dengan penambahan *Batch Normalization*). 
Hasilnya sangat memuaskan: model mengalami konvergensi yang sangat stabil (Loss sangat kecil: 0.0093). Metrik evaluasi menunjukkan performa yang sangat seimbang dan presisi, di mana **Precision dan Recall masing-masing berada di angka 86.67%** (menghasilkan F1-Score 86.67%). Nilai **ROC-AUC juga menyentuh angka hampir sempurna: 99.92%**.

### 💡 Interpretasi Feature Importance

Berbeda dengan algoritma berbasis *Decision Tree* (seperti Random Forest atau CatBoost) yang secara bawaan dapat mengukur *feature importance*, model berbasis *Neural Network* seperti MLP sering kali dianggap sebagai *black-box*. Jaringan saraf mengevaluasi fitur secara holistik melalui pembaruan bobot (*weights*) antar koneksi neuron. 

Namun, penggunaan lapisan `Normalization` di awal arsitektur hasil *tuning* mengindikasikan bahwa menjaga skala (*scaling*) dari fitur input memainkan peran sangat vital dalam memastikan bobot jaringan tidak didominasi oleh fitur dengan rentang nilai yang sangat besar (misalnya fitur nilai transaksi atau umur), sehingga seluruh fitur berkontribusi secara proporsional.

### ✅ Kesimpulan

Berdasarkan keseluruhan evaluasi pada Multi-Layer Perceptron (MLP):

1. **Pendekatan Baseline yang Di-Tuning (Tuned Baseline) adalah yang terbaik.** Peningkatan lebar *hidden layer* (menjadi 128) serta penambahan *Batch Normalization* terbukti lebih efektif dalam mengenali pola rumit transaksi fraud dibandingkan sekadar memanipulasi distribusi data (SMOTE) atau membobotkan error (Class Weight).
2. Konfigurasi model terbaik berhasil memberikan keseimbangan yang sangat kuat antara kemampuan mendeteksi fraud (*Recall*) dan ketepatan deteksi (*Precision*).
3. **Hasil evaluasi model terbaik (Tuned Architecture):**
   * **Accuracy** : 99.60%
   * **Precision** : 86.67%
   * **Recall** : 86.67%
   * **F1-Score** : 86.67%
   * **ROC-AUC** : 99.92%
   * **Loss** : 0.0093

MLP menunjukkan potensi luar biasa sebagai model non-linear yang handal untuk deteksi anomali pada data transaksi, menjadikannya salah satu kandidat model yang paling optimal dalam repositori ini.