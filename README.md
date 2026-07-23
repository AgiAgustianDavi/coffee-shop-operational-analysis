# ☕ Aroma Jaya Coffee Shop: Operational & Sales Optimization Analysis

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Cleaning-orange.svg)](https://pandas.pydata.org/)
[![Seaborn](https://img.shields.io/badge/Seaborn-Data%20Visualization-green.svg)](https://seaborn.pydata.org/)
[![Tableau](https://img.shields.io/badge/Tableau-Interactive%20Dashboard-hex%20#E97627.svg?style=flat&logo=Tableau&logoColor=white)](https://public.tableau.com/shared/NGC76SMC2?:display_count=n&:origin=viz_share_link)

## 📌Executive Summary
Owner Kedai Kopi **Aroma Jaya (Cabang Sudirman)** menghadapi anomali operasional yang serius: secara visual terjadi **antrean pelanggan yang sangat panjang**, namun **pendapatan bulanan stagnan**. Di sisi lain, manajemen mengalami kerugian akibat penumpukan stok bahan baku (*deadstock*) akibat strategi penyediaan pasokan yang kurang tepat. Berdasarkan analisis data transaksi 6 bulan terakhir, ditemukan tiga temuan utama:

#### 1.	Kecilnya Nilai Keranjang Belanja (Basket Size)
Antrean panjang di kasir tidak mencerminkan lonjakan omzet karena 75% transaksi pelanggan hanya membeli 1–2 item dengan nominal yang sangat kecil dan seragam (Rp43.000-an) per struk. Kedai sibuk melayani ribuan transaksi kecil yang belum dioptimalkan secara finansial.

#### 2.	Kunjungan Ekstrem (Normal vs Weekend Spike)
Penjualan tidak tersebar merata. Volume penjualan hari Jumat–Minggu melonjak hingga 2x lipat dibandingkan hari Senin–Kamis. Kebijakan menyamaratakan volume pasokan bahan baku setiap hari menjadi penyebab utama penumpukan stok.

#### 3.	Pola Kunjungan Tersentralisasi (Extreme Peak Hours)
Penumpukan antrean terjadi akibat pesanan datang bersamaan pada waktu yang sangat sempit (jam berangkat kerja, makan siang, dan waktu hangout akhir pekan). Hal ini membuat mesin espresso dan kapasitas staf mengalami overload sesaat.

---

## 📌 Business Scenario & Problem Statement
Owner Aroma Jaya memerlukan kejelasan data agar tidak salah mengambil tindakan (seperti menambah staf harian atau memperluas kedai secara gegabah). Laporan ini berfokus menjawab 3 pertanyaan kunci:
1. Bagaimana tren penjualan Aroma Jaya dari waktu ke waktu (bulanan)?
2. Hari apa saja dalam seminggu yang cenderung menghasilkan volume penjualan tertinggi?
3. Waktu/jam berapa saja yang menjadi puncak kepadatan transaksi (*peak hours*)?

---

## 🛠️ Data Cleaning & Tech Stack
Sebelum analisis dilakukan, dataset melalui tahap *data cleaning* untuk menjamin validitas hasil:
* **Removing Duplicates:** Mengeliminasi data duplikat.
* **Handling Missing Values:** Penanganan data kosong (*missing values*) pada kolom store_location.
* **Inconsistent Text Fix:** Standarisasi teks dan perbaikan variasi penulisan input sistem.
* **Outlier Removal:** Pembersihan data *outlier* pada kolom quantity agar hasil agregat tidak bias.

*Tech Stack:* `pandas`, `matplotlib`, `seaborn`.

---

## 📊 Key Insights & Deep-Dive Visualizations

### 1. Tren Penjualan Bulanan & Analisis Nilai Struk (*Basket Size*)
Grafik pendapatan makro menunjukkan tren datar (*stagnant*) dengan fluktuasi tipis di bawah 5%, bergerak di rentang **Rp99 Juta hingga Rp113 Juta**.

![](just_support_images/trend_months.png)

Investigasi pada nilai belanja per transaksi menunjukkan rata-rata nominal struk sangat statis di angka **~Rp43.300 hingga ~Rp44.400**.

![](just_support_images/aov_months.png)

Berdasarkan analisis histogram di bawah, nilai Kuartil 1 dan Median berada tepat di angka **1 item**, sementara Kuartil 3 berada di angka **2 item**.

![](just_support_images/qty_distribution.png)

> 💡 **Insight:** Sebanyak 75% transaksi pelanggan hanya membeli 1–2 item saja. Stagnansi omzet terjadi karena kecilnya ukuran keranjang belanja (*basket size*). Kasir terlihat sangat sibuk mengantre bukan karena lonjakan omzet besar, melainkan karena melayani ribuan transaksi kecil yang nilainya seragam.

---

### 2. Analisis Kunjungan Harian (*Normal vs Weekend Spike*)
Volume penjualan harian secara konsisten terbagi menjadi dua kategori yang kontras di setiap bulannya:
* **Senin–Kamis (Normal):** Penjualan stabil bermutu volume rendah (**~2.600 - ~3.300 item**).
* **Jumat–Minggu (Spike):** Penjualan melonjak **2x lipat** (**~5.100 - ~6.200 item**) dan menyumbang lebih dari 60% total transaksi mingguan.

![](just_support_images/day_busy.png)

Analisis tren harian antar-bulan mengonfirmasi bahwa pola ini berulang konstan setiap bulan tanpa adanya perubahan anomali musiman. Cabang Sudirman terbukti merupakan cabang berbasis *lifestyle & hangout*.

![](just_support_images/day_busy_months.png)

> 💡 **Insight:** Volume penjualan akhir pekan melonjak hingga 2x lipat dibandingkan hari biasa. Pola ini terbukti berulang konstan setiap bulan dari Januari hingga Juni tanpa ada anomali tren. Kebijakan menyamaratakan stok harian terbukti menjadi pemicu utama kerugian penumpukan bahan baku (deadstock) di hari Senin–Kamis.

---

### 3. Jam Puncak Kunjungan (*Extreme Peak Hours*)
Kepadatan transaksi per jam menunjukkan konsistensi pola yang sangat tebal di sepanjang semester pertama tahun 2026:
* **Senin – Jumat:** Penumpukan pesanan terpusat pada jam berangkat kantor (**07.00–09.00**) dan istirahat makan siang (**12.00–13.00**).
* **Khusus Hari Jumat:** Terjadi gelombang keramaian susulan pada pukul **17.00–21.00**.
* **Sabtu & Minggu:** mulai ramai sejak pukul 13.00 dan memuncak pada pukul **16.00–21.00**.

![](just_support_images/hour_busy.png)

Visualisasi *Heatmap* di bawah menunjukkan stabilitas struktur jam sibuk yang konsisten mengalir dari bulan Januari hingga Juni:

![grafik](just_support_images/hour_busy_months.png)

> 💡 **Akar Masalah:** Antrean panjang bersifat semu secara finansial. Kapasitas operasional (mesin espresso, kecepatan barista, dan kasir) mengalami *overload* parah hanya pada jam-jam kritis tersebut, memicu tingginya angka pembatalan pesanan (*customer drop-off*). Sebaliknya, di luar jam tersebut kedai cenderung sepi dan aset operasional menganggur (*idle*).

---

## 🖥️ Interactive Sales Dashboard (Tableau)
Untuk melengkapi analisis operasional ini, dibangun sebuah dashboard interaktif menggunakan **Tableau Public** untuk memantau performa bisnis di tingkat makro secara berkala.

👉 **[Klik di sini untuk mengakses Tableau Dashboard Interaktif](https://public.tableau.com/shared/NGC76SMC2?:display_count=n&:origin=viz_share_link)**

---

## 💡 Actionable Recommendations
1. **Optimalisasi Stok & Manajemen Rantai Pasok:** Menurunkan suplai pasokan bahan baku sebesar **30–40% pada hari Senin–Kamis** untuk memotong biaya pembuangan stok. Alihkan anggarannya untuk mempertebal pasokan menu cepat saji menjelang akhir pekan.

2. **Penjadwalan Staf Dinamis (*Dynamic Shifting*):** Hentikan kebijakan jumlah staf yang sama rata setiap hari. Jadwalkan kapasitas penuh tim (*Full Team*) khusus pada hari Jumat malam serta Sabtu–Minggu sore (pukul 16.00–21.00). Alokasikan staf seminimal mungkin di luar jam sibuk untuk menghemat biaya upah harian.
  
3. **Mengurai Antrean & Peningkatan *Basket Size*:**
   * Terapkan sistem *Pre-Order* mandiri via WhatsApp Otomatis atau QR Code di meja khusus untuk pesanan *Takeaway* di jam sibuk guna memecah *bottleneck* kasir.
   * Edukasi staf kasir untuk melakukan *cross-selling* produk camilan (Croissant/Roti Bakar) lewat paket *bundling* cepat saat melayani pembelian single-item, dengan target menaikkan rata-rata nilai struk ke angka Rp60.000-an dalam 3 bulan.

---

## 📁 Repository Structure
```text
├── dataset/
│   ├── dataset_pos_aromajaya.csv      # Dataset mentah sebelum dibersihkan
│   └── cleaned_data.csv               # Dataset sesudah dibersihkan
├── notebooks/
│   ├── data_preparation.ipynb          # Notebook proses Data Cleaning
│   └── eda.ipynb                      # Notebook proses EDA & Visualisasi
├── reports/
│   └── laporan_analisis_operasional.pdf # Laporan bisnis final (PDF)
└── README.md                          # Ringkasan proyek (Dokumen ini)
