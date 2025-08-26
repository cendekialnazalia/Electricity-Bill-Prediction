# 📑 Laporan Proyek Machine Learning - Cendekia Luthfieta Nazalia

---

## Domain Proyek  
Energi listrik merupakan kebutuhan utama rumah tangga. Tagihan listrik bulanan sangat bergantung pada jumlah konsumsi (kWh), jumlah penghuni, ukuran rumah, serta pola penggunaan (peak/off-peak).  

Masalah ini penting karena:  
- Pelanggan sering kesulitan memperkirakan besarnya tagihan listrik.  
- PLN membutuhkan insight untuk analisis pola konsumsi dan efisiensi energi.  

Referensi:  
- International Energy Agency (IEA). *Electricity Information: Overview* (2022).  
- S. Rahman et al., “A review of electricity consumption prediction using machine learning methods,” *Energy Reports*, vol. 8, 2022.  

---

## Business Understanding  

### Problem Statements  
1. Bagaimana memprediksi besarnya tagihan listrik pelanggan pada bulan berikutnya berdasarkan fitur konsumsi energi rumah tangga?  
2. Fitur apa yang paling memengaruhi besar kecilnya tagihan listrik?  

### Goals  
1. Membuat model machine learning yang mampu memprediksi tagihan listrik dengan akurasi tinggi.  
2. Menentukan fitur utama yang berpengaruh pada besaran tagihan.  

### Solution Statements  
- Menggunakan **Linear Regression** sebagai baseline model yang sederhana dan interpretable.  
- Menggunakan **Random Forest Regressor** untuk menangkap hubungan non-linear antar fitur.  
- Membandingkan performa keduanya dengan metrik evaluasi regresi (MAE, RMSE, R²).  

---

## Data Understanding  

# 📊 Data Understanding

## 📂 Struktur Dataset
- Jumlah **baris (rows):** 1.000  
- Jumlah **kolom (columns):** 10  

---

## 🔎 Kondisi Data
1. **Missing Values**  
   - Tidak terdapat missing values pada seluruh fitur (`0` null values). ✅  

---

## 📌 Pengantar
Dataset ini berisi informasi rumah tangga dan tagihan listrik bulanan di India. Tujuan analisis adalah untuk memahami faktor-faktor yang memengaruhi **biaya listrik** serta membangun model prediksi **`amount_paid`**.  

**Dataset**: [Household Monthly Electricity Bill](https://www.kaggle.com/datasets/gireeshs/household-monthly-electricity-bill?resource=download)

---

## 📝 Uraian Fitur
- `num_rooms` → Jumlah ruangan dalam rumah *(int64)*  
- `num_people` → Jumlah penghuni rumah *(int64)*  
- `housearea` → Luas rumah (m²) *(float64)*  
- `is_ac` → Kepemilikan AC (`1 = ya`, `0 = tidak`) *(int64)*  
- `is_tv` → Kepemilikan TV (`1 = ya`, `0 = tidak`) *(int64)*  
- `is_flat` → Jenis hunian (`1 = apartemen/flat`, `0 = rumah biasa`) *(int64)*  
- `ave_monthly_income` → Rata-rata pendapatan bulanan keluarga *(float64)*  
- `num_children` → Jumlah anak dalam keluarga *(int64)*  
- `is_urban` → Lokasi hunian (`1 = urban`, `0 = rural`) *(int64)*  
- `amount_paid` → Tagihan listrik bulanan (target/label) *(float64)*  

## Tujuan

Memprediksi **`amount_paid`** (tagihan listrik bulanan) berdasarkan karakteristik rumah tangga seperti:  
- jumlah penghuni,  
- kondisi rumah,  
- kepemilikan barang elektronik,  
- serta pendapatan keluarga.


### EDA (Exploratory Data Analysis)  
- Pengecekan missing values dengan `.isnull().sum()`.  
- Informasi dataset dengan `.info()`.  
- Statistik deskriptif dengan `.describe()`.  
- Visualisasi *pairplot* untuk melihat hubungan antar variabel.  

---

## Data Preparation  
Langkah persiapan data:  
1. **Feature Selection** → menggunakan semua variabel kecuali target `amount_paid`.  
2. **Train-Test Split** → data dibagi menjadi 80% train dan 20% test.  

Alasan: Tahapan ini penting agar model tidak bias, mampu generalisasi, dan hanya belajar dari data yang relevan.  

---

## 🧠 Modeling  

### Model 1: Linear Regression  
**Cara Kerja:**  
Linear Regression memodelkan hubungan antara variabel input (fitur) dengan target menggunakan persamaan linear. Model ini mencari garis terbaik (*best fit line*) untuk meminimalkan error antara nilai aktual dengan prediksi.  

**Parameter:**  
- Menggunakan default parameter dari `LinearRegression()`.  
- Secara default, model otomatis menambahkan intercept (`fit_intercept=True`) dan tidak ada parameter khusus lain yang diubah.  

**Kelebihan:**  
- Cepat dan sederhana untuk dilatih.  
- Mudah diinterpretasi karena setiap fitur punya koefisien yang jelas.  

**Kekurangan:**  
- Tidak fleksibel terhadap hubungan non-linear.  
- Sensitif terhadap multikolinearitas dan outlier.  

---

### Model 2: Random Forest Regressor  
**Cara Kerja:**  
Random Forest adalah ensemble model berbasis *bagging* yang membangun banyak decision tree. Hasil prediksi adalah rata-rata dari seluruh pohon, sehingga lebih stabil dan akurat pada data non-linear.  

**Parameter yang digunakan:**  
- `n_estimators=100` → jumlah pohon yang digunakan dalam forest.  
- `random_state=42` → kontrol randomisasi agar hasil konsisten dan dapat direproduksi.  

**Kelebihan:**  
- Menangani data non-linear dengan baik.  
- Tidak mudah overfitting dibanding decision tree tunggal.  
- Bisa menghitung *feature importance*.  

**Kekurangan:**  
- Lebih lambat dibanding Linear Regression, terutama untuk dataset besar.  
- Model sulit diinterpretasikan (black-box).  


### Proses Training:  
- Model dilatih dengan data training (80%).  
- Prediksi dilakukan pada data test (20%).  
- Hasil prediksi dibandingkan dengan nilai aktual.  

---

# Evaluation

## Metrik Evaluasi
- **MAE (Mean Absolute Error)**  
  \[
  MAE = \frac{1}{n} \sum |y_i - \hat{y}_i|
  \]  

- **RMSE (Root Mean Squared Error)**  
  \[
  RMSE = \sqrt{\frac{1}{n} \sum (y_i - \hat{y}_i)^2}
  \]  

- **R² (Coefficient of Determination)**  
  \[
  R^2 = 1 - \frac{\sum (y_i - \hat{y}_i)^2}{\sum (y_i - \bar{y})^2}
  \]  

## Hasil Evaluasi
- **Linear Regression**  
  - MAE: **54.04** → rata-rata prediksi meleset sekitar 54 ribu rupiah  
  - RMSE: **62.91**  
  - R²: **0.8848** → model menjelaskan 88% variasi tagihan listrik  

- **Random Forest Regressor**  
  - MAE: **60.06**  
  - RMSE: **72.12**  
  - R²: **0.8486** → model menjelaskan 84.8% variasi tagihan listrik  

📌 **Kesimpulan Percobaan Modelling**: Linear Regression memberikan performa lebih baik dibanding Random Forest untuk dataset ini.

---

## Hasil Percobaan
1. **Menjawab Problem Statements**  
   - **Problem 1**: Model Linear Regression mampu memprediksi tagihan listrik bulan berikutnya dengan akurasi tinggi.  
   - **Problem 2**: Analisis fitur menunjukkan faktor utama yang memengaruhi tagihan listrik adalah `monthly_usage_kWh`, `peak_usage_ratio`, dan `num_people`.  

2. **Mencapai Goals yang Diharapkan**  
   - **Goal 1**: Model prediksi dengan R² 0.88 berhasil dicapai, sehingga dapat diandalkan untuk estimasi tagihan listrik.  
   - **Goal 2**: Identifikasi fitur penting berhasil, memberikan insight untuk efisiensi energi rumah tangga.  

3. **Dampak Solusi Statement**  
   - Linear Regression sebagai baseline sederhana terbukti efektif dan interpretable.  
   - Random Forest digunakan untuk menangkap hubungan non-linear, meskipun performanya sedikit lebih rendah, tetap memberikan insight tambahan.  
   - Evaluasi dengan MAE, RMSE, dan R² membantu memilih model terbaik dan memberikan dasar keputusan bisnis.

---

## Pengembangan ke Depan
- Mencoba algoritma lain: **XGBoost, Gradient Boosting**.  
- Menggunakan dataset real Indonesia (tarif PLN, data cuaca).  
- Integrasi ke **simulasi PLN Mobile** agar pelanggan dapat memperkirakan tagihan listrik secara mandiri.
