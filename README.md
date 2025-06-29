## Deskripsi Project
Project ini bertujuan untuk membangun dan mengevaluasi model machine learning yang mampu mengidentifikasi transaksi penipuan (fraud) pada kartu kredit. Dengan dataset yang sangat tidak seimbang (hanya sekitar 0.58% transaksi adalah fraud), project ini fokus pada rekayasa fitur (feature engineering) yang mendalam dan penggunaan model klasifikasi yang efektif untuk memaksimalkan akurasi dan metrik penting lainnya seperti *recall* dan *precision*.

Model yang digunakan adalah **Logistic Regression** sebagai _baseline_ dan **Random Forest** sebagai model yang lebih kompleks untuk perbandingan performa.

## Akses Dataset
https://drive.google.com/file/d/1yj5Pq3mBsbLXuuwJgaqwfA4IETaQ535e/view

## Analisis dan Rekayasa Fitur (Feature Engineering)
Analisis data eksplorasi (EDA) dan rekayasa fitur adalah inti dari project ini untuk menghasilkan variabel prediktor yang kuat. Beberapa fitur kunci yang dibuat antara lain:

1.  **Fitur Berbasis Waktu:**
    * Ekstraksi informasi detail dari waktu transaksi seperti hari, minggu, bulan, tahun, dan jam untuk menangkap pola temporal.
    * `diff_trans`: Waktu (dalam menit) antara transaksi saat ini dan transaksi sebelumnya untuk satu kartu yang sama.
    * `velocity_1h`: Jumlah transaksi yang terjadi dalam periode 1 jam terakhir untuk kartu yang sama.

2.  **Fitur Berbasis Transaksi:**
    * `RollingAvg_3`: Rata-rata nominal dari 3 transaksi terakhir untuk kartu yang sama.
    * `AvgTransactionAmount`: Rata-rata nominal transaksi untuk setiap nomor kartu kredit.
    * `AboveAvgFlag`: Penanda biner jika sebuah transaksi memiliki nominal yang secara signifikan (misalnya, 2x) di atas rata-rata transaksi pengguna.

3.  **Fitur Geospasial:**
    * `distance`: Menghitung jarak Haversine (dalam km) antara lokasi geografis pemegang kartu (`lat`, `long`) dan lokasi merchant (`merch_lat`, `merch_long`) untuk mendeteksi transaksi yang tidak wajar.

4.  **Fitur Demografis dan Kontekstual:**
    * `age_cc_owner`: Usia pemegang kartu saat transaksi dilakukan.
    * Kategorisasi pekerjaan ke dalam industri dan estimasi rentang gaji untuk memberikan konteks sosio-ekonomi.
    * Pengkodean manual untuk variabel `category` agar dapat digunakan oleh model.

## Model yang Digunakan

1.  **Regresi Logistik (Logistic Regression):**
    Digunakan sebagai model dasar (baseline) karena interpretasinya yang mudah dan komputasinya yang cepat.

2.  **Random Forest Classifier:**
    Dipilih karena kemampuannya menangani hubungan non-linear, interaksi antar fitur, dan memberikan *feature importance*. Parameter `class_weight='balanced'` digunakan untuk mengatasi masalah dataset yang tidak seimbang.
