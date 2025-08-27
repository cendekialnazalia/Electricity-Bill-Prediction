# 📑 Laporan Proyek Machine Learning - Cendekia Luthfieta Nazalia

---

## DOMAIN PROYEK  
Energi listrik merupakan kebutuhan utama rumah tangga. Tagihan listrik bulanan sangat bergantung pada jumlah konsumsi (kWh), jumlah penghuni, ukuran rumah, serta pola penggunaan (peak/off-peak).  

Masalah ini penting karena:  
- Pelanggan sering kesulitan memperkirakan besarnya tagihan listrik.  
- PLN membutuhkan insight untuk analisis pola konsumsi dan efisiensi energi.  

Referensi:  
- International Energy Agency (IEA). *Electricity Information: Overview* (2022).  
- S. Rahman et al., “A review of electricity consumption prediction using machine learning methods,” *Energy Reports*, vol. 8, 2022.  

---

## BUSINESS UNDERSTANDING

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

## DATA UNDERSTANDING 

Data yang Anda gunakan pada proyek kali ini adalah Household Monthly Electricity Bill dataset yang diunduh dari Kaggle. 
**Dataset**: [Household Monthly Electricity Bill](https://www.kaggle.com/datasets/gireeshs/household-monthly-electricity-bill?resource=download)
Untuk tahap latihan, Anda hanya akan menggunakan dataset ini sehingga tidak perlu menambahkan data lain atau melakukan penggabungan dataset. Dataset ini cukup sederhana dan bersih sehingga tidak terlalu banyak memerlukan proses data cleaning. Dataset ini terdiri dari 1000 data yang berisi informasi mengenai jumlah ruangan (num_rooms), jumlah penghuni rumah (num_people), luas rumah (house area), kepemilikan AC (is_ac), kepemilikan TV (is_tv), tipe rumah (is_flat), rata-rata pemasukan (ave_monthly_income), jumlah anak(num_children), lokasi rumah (is_urban), jumlah tagihan listrik bulanan (amount_paid). Fitur numerik yang digunakan dalam analisis ini adalah jumlah orang dalam rumah (num_people) dan luas rumah (house area), sedangkan fitur target adalah jumlah tagihan listrik yang dibayarkan (amount_paid). Kesempuluh fitur ini yang akan digunakan untuk menemukan pola pada data, sedangkan tagihan merupakan fitur target.

Dalam membuat model prediktif dengan machine learning kita akan  menggunakan tools google colaboratory.

## EDA (Exploratory Data Analysis)  
- Eksploratory Data Analysis - Deskiprsi Variabel dilakukan dengan melihat informasi dataset `.info()` dan statistik deskriptif `.describe()`.   
- Eksploratory Data Analysis - Missing Value dilakukan untuk menghitung jumlah nilai kosong pada setiap kolom dataset 
- Eksploratory Data Analysis - Univariate Analysis  dilakukan untuk fitur numerik dengan melihat histogram masing-masing fitur.
- Eksploratory Data Analysis - Multivariate Analysis dilakukan untuk mengamati hubungan antar fitur numerik.

---

## DATA PREPARATION  
Langkah persiapan data:  
1. **Train-Test Split** → data dibagi menjadi 80% train dan 20% test.  

Alasan: Tahapan ini penting agar model tidak bias, mampu generalisasi, dan hanya belajar dari data yang relevan.  

---

## MODEL DEVELOPMENT  

### Model Development dengan Linear Regression  
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

**Proses Training:**  
- Model dilatih dengan data training (80%).  
- Prediksi dilakukan pada data test (20%).  
- Hasil prediksi dibandingkan dengan nilai aktual.  

---

### Model Development dengan Random Forest Regressor  
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


**Proses Training:** 
- Model dilatih dengan data training (80%).  
- Prediksi dilakukan pada data test (20%).  
- Hasil prediksi dibandingkan dengan nilai aktual.  

---

## EVALUASI MODEL

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
- **Evaluasi Model Linear Regression**  
  - MAE: **54.04** → rata-rata prediksi meleset sekitar 54 ribu rupiah  
  - RMSE: **62.91**  
  - R²: **0.8848** → model menjelaskan 88% variasi tagihan listrik  

- **Evaluasi Model Random Forest Regressor**  
  - MAE: **60.06**  
  - RMSE: **72.12**  
  - R²: **0.8486** → model menjelaskan 84.8% variasi tagihan listrik
 
## VISUALISASI HASIL PREDIKSI & NILAI AKTUAL
Melakukan perbanding nilai aktual (y_test) dengan hasil prediksi random forest (biru) dan linear regression (orange) dimana jika mendekatai garis putus-putus (diagonal) sama dengan mendekati sempurna. dan setelah dijalankan code didapatkan hasil bahwa Grafik membandingkan nilai tagihan listrik sebenarnya dengan prediksi dari dua model, Random Forest dan Linear Regression. Kedua model berhasil memprediksi dengan cukup baik karena titik-titiknya dekat dengan garis diagonal yang menunjukkan prediksi sama dengan nilai asli. Linear Regression terlihat sedikit lebih rapat di sekitar garis tersebut, tapi kedua model punya performa yang cukup mirip.

## FEATURE IMPORTANCE DARI RANDOM FOREST 
Melakukan analisis fitur penting untuk mengetahui kontribusi setiap fitur terhadap prediksi model Random FOrest dan didapatkanlah hasil bahwa Fitur is_urban paling berpengaruh dalam prediksi konsumsi energi,
diikuti oleh num_children dan is_ac. Fitur lain seperti housearea, ave_monthly_income, dan is_tv memiliki pengaruh kecil, sedangkan num_people dan num_rooms memberikan kontribusi paling sedikit.

## KESIMPULAN
**Kesimpulan Percobaan Modelling**: Linear Regression memberikan performa lebih baik dibanding Random Forest untuk dataset ini.

### Hasil Percobaan
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


### Pengembangan ke Depan
- Mencoba algoritma lain: **XGBoost, Gradient Boosting**.  
- Menggunakan dataset real Indonesia (tarif PLN, data cuaca).  
- Integrasi ke **simulasi PLN Mobile** agar pelanggan dapat memperkirakan tagihan listrik secara mandiri.
