# ☕ Aroma Jaya Coffee Shop: Operational & Sales Optimization Analysis

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Cleaning-orange.svg)](https://pandas.pydata.org/)
[![Seaborn](https://img.shields.io/badge/Seaborn-Data%20Visualization-green.svg)](https://seaborn.pydata.org/)

## 📌 Business Scenario & Problem Statement
Owner Kedai Kopi **Aroma Jaya (Cabang Sudirman)** menghadapi anomali operasional yang serius: secara visual terjadi **antrean pelanggan yang sangat panjang**, namun **pendapatan cabang stagnan** (sama seperti hari biasa). Di sisi lain, manajemen telah menyetok banyak bahan baku segar berdasarkan asumsi keramaian tersebut, yang berujung pada kerugian akibat penumpukan stok (*deadstock/spoilage*).

Proyek ini bertujuan untuk membedah data transaksi POS selama 6 bulan terakhir guna menjawab 3 pertanyaan kunci:
1. Bagaimana tren penjualan Aroma Jaya dari waktu ke waktu?
2. Hari apa saja dalam seminggu yang memiliki volume penjualan tertinggi?
3. Pada jam berapa saja puncak kepadatan transaksi (*peak hours*) terjadi?

---

## 🛠️ Data Cleaning & Tech Stack
Sebelum analisis dilakukan, dataset melalui tahap *data cleaning* intensif untuk menjamin validitas hasil:
* **Handling Missing Values:** Mengisi data lokasi kosong dengan nilai modus dan interpolasi kuantitas.
* **Removing Duplicates:** Mengeliminasi data transaksi ganda akibat kegagalan sistem kasir.
* **Inconsistent Text Fix:** Menyamakan variasi *typo* teks pada lokasi cabang dan tipe order.
* **Outlier Removal:** Menyaring anomali kuantitas pembelian (seperti nilai minus atau angka input eror `99`).

*Library yang digunakan:* `pandas`, `numpy`, `matplotlib`, `seaborn`.

---

## 📊 Key Insights & Visualizations

### 1. Tren Penjualan Bulanan (Stagnan)
Tingkat pertumbuhan omzet bulanan cenderung datar dengan fluktuasi di bawah 5%. Ini mengonfirmasi bahwa kapasitas operasional kedai saat ini telah mencapai titik jenuh (*saturation point*).

### 2. Analisis Hari Sibuk (Jumat - Minggu)
Lebih dari **60% total transaksi dalam seminggu menumpuk di hari Jumat, Sabtu, dan Minggu**. Menyamaratakan suplai bahan baku di hari kerja (Senin-Kamis) adalah penyebab utama kerugian operasional.

### 3. Peta Jam Puncak Kunjungan (Extreme Peak Hours)
Melalui visualisasi *Heatmap Multi-Faceted*, ditemukan pola lonjakan transaksi ekstrem yang sangat terlokalisasi:
* **Weekdays (Jumat):** Padat ekstrem pada jam istirahat kantor (**12.00 - 14.00**).
* **Weekend (Sabtu-Minggu):** Padat ekstrem pada sore menjelang malam (**16.00 - 20.00**).

> 💡 **Akar Masalah:** Antrean terlihat panjang bukan karena jumlah pembeli harian meningkat drastis, melainkan akibat terjadinya *bottleneck* kapasitas produksi mesin dan barista yang kewalahan menerima pesanan massal di jam yang sama, memicu tingginya *customer drop-off rate*.

*(Tips: Masukkan screenshot grafik Heatmap per cabang/hari kamu di sini dengan syntax: ![](path_to_image.png) )*

---

## 💡 Actionable Recommendations
Berdasarkan temuan data, rekomendasi taktis yang diajukan kepada Owner Aroma Jaya adalah:

1. **Dynamic Stock Allocation:** Menurunkan suplai bahan baku sebesar 35% pada hari Senin-Kamis, dan mengalokasikan anggarannya untuk memperkuat stok menu cepat saji di hari Jumat-Minggu.
2. **Agile Shifting Staff:** Menerapkan jadwal kerja dinamis dengan menempatkan kapasitas penuh tim (*Full Team*) hanya pada jendela jam sibuk (Jumat siang & Weekend sore).
3. **Pre-Order & Bypass System:** Menyediakan jalur antrean khusus atau sistem QR-code/WhatsApp *Pre-Order* untuk pelanggan *Takeaway* guna memecah *bottleneck* di kasir utama pada jam-jam kritis.

---

## 📁 Repository Structure
```text
├── dataset/
│   └── kopi_srawung_dirty_6months.csv  # Dataset mentah sebelum dibersihkan
├── notebooks/
│   └── EDA.ipynb                       # Notebook proses Cleaning & Visualisasi
├── reports/
│   └── LAPORAN ANALISIS OPERASIONAL.pdf # Laporan resmi format bisnis (PDF)
└── README.md                           # Ringkasan proyek
