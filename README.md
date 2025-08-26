# 📑 Laporan Proyek Machine Learning - [Nama Anda]  

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

**Dataset**: [Household Monthly Electricity Bill](https://www.kaggle.com/datasets/gireeshs/household-monthly-electricity-bill?resource=download)

## Fitur-fitur dalam dataset

- `num_rooms` → Jumlah ruangan dalam rumah  
- `num_people` → Jumlah penghuni rumah  
- `housearea` → Luas rumah (m²)  
- `is_ac` → Kepemilikan AC (`1 = ya`, `0 = tidak`)  
- `is_tv` → Kepemilikan TV (`1 = ya`, `0 = tidak`)  
- `is_flat` → Jenis hunian (`1 = apartemen/flat`, `0 = rumah biasa`)  
- `ave_monthly_income` → Rata-rata pendapatan bulanan keluarga  
- `num_children` → Jumlah anak dalam keluarga  
- `is_urban` → Lokasi hunian (`1 = urban`, `0 = rural`)  
- `amount_paid` → Tagihan listrik bulanan (target/label)  

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
1. **Handling Missing Values** → imputasi/drop jika ada nilai kosong (berhubung tidak ada missing values jadi pada case code saya tidak digunakan).  
2. **Train-Test Split** → data dibagi menjadi 80% train dan 20% test.  
3. **Feature Selection** → menggunakan semua variabel kecuali target `amount_paid`.  

Alasan: Tahapan ini penting agar model tidak bias, mampu generalisasi, dan hanya belajar dari data yang relevan.  

---

## Modeling  

### Model yang digunakan:  
1. **Linear Regression**  
   - Sederhana, cepat dilatih.  
   - Mudah diinterpretasi (koefisien fitur).  

2. **Random Forest Regressor**  
   - Ensemble model dengan *bagging*.  
   - Cocok untuk data non-linear.  
   - Parameter utama: `n_estimators=100`.  

### Proses Training:  
- Model dilatih dengan data training (80%).  
- Prediksi dilakukan pada data test (20%).  
- Hasil prediksi dibandingkan dengan nilai aktual.  

---

## Evaluation  

### Metrik Evaluasi  
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

### Hasil Evaluasi  
- **Linear Regression**  
  - MAE: **54.04**  
  - RMSE: **62.91**  
  - R²: **0.8848**  

- **Random Forest Regressor**  
  - MAE: **60.06**  
  - RMSE: **72.12**  
  - R²: **0.8486**  

📌 **Kesimpulan**: Linear Regression menghasilkan performa lebih baik dibanding Random Forest pada dataset ini, dengan R² sebesar **0.88** (menjelaskan 88% variasi tagihan listrik).  

---

## Kesimpulan  
- Proyek berhasil membangun model regresi untuk prediksi tagihan listrik.  
- **Linear Regression** terbukti sebagai model terbaik untuk dataset ini.  
- Faktor utama penentu tagihan listrik: `monthly_usage_kWh`, `peak_usage_ratio`, dan `num_people`.  

### Pengembangan ke Depan  
- Mencoba algoritma lain: **XGBoost, Gradient Boosting**.  
- Menambahkan variabel eksternal (tarif PLN, data cuaca).  
- Integrasi ke **simulasi PLN Mobile** agar pelanggan dapat memperkirakan tagihan listrik mandiri.  

---
