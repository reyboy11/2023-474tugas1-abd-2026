# Dokumentasi Dataset IDN News

## 1. Informasi Dataset

**Nama dataset:** Indonesian News Dataset (`idn-news-az`)

**Sumber:** [Hugging Face, esteler-ai/idn-news-az](https://huggingface.co/datasets/esteler-ai/idn-news-az)

**Lisensi:** CC BY 4.0, sesuai metadata README sumber dataset.

Dataset ini berisi kumpulan berita berbahasa Indonesia dari berbagai portal berita daring. Dataset digunakan untuk tugas Analisis Big Data dengan menerapkan Polars dan DuckDB.

## 2. Struktur Dataset Mentah

Dataset mentah tersedia dalam format Parquet dengan rincian berikut.

| Informasi | Keterangan |
|---|---|
| Jumlah file | 441 file Parquet |
| Ukuran total | Sekitar 1,558 GB |
| Jumlah baris awal | 1.149.789 baris |
| Format penyimpanan | Parquet |

### Struktur Kolom

| Kolom | Tipe awal | Deskripsi |
|---|---|---|
| `date` | String | Tanggal publikasi berita |
| `link` | String | URL artikel berita |
| `title` | String | Judul berita |
| `text` | String | Isi artikel berita |

## 3. Lokasi Penyimpanan

Dataset mentah disimpan pada direktori:

`data/raw/idn-news/data_files/`

Notebook analisis disimpan pada direktori:

`notebooks/`

Dataset hasil cleaning disimpan pada:

`data/processed/idn_news_cleaned.parquet`

Laporan kualitas data tersedia pada:

`output/tables/data_quality_report.json`

Ringkasan statistik DuckDB tersedia pada:

`output/tables/duckdb_summarize.csv`

## 4. Hasil Milestone 2

Pembersihan data dilakukan menggunakan Polars, sedangkan validasi dan profiling hasil dilakukan menggunakan DuckDB melalui perintah `SUMMARIZE`.

| Indikator | Hasil |
|---|---:|
| Jumlah baris awal | 1.149.789 |
| Baris dengan kolom wajib kosong atau null | 0 |
| Baris bertanggal di luar periode | 4 |
| Duplikasi identik yang dihapus | 108.391 |
| Jumlah baris setelah cleaning | 1.041.394 |
| Tanggal tidak tersedia setelah cleaning | 101.403 |
| Duplikasi identik tersisa | 0 |

### Aturan Cleaning

1. Mempertahankan tanggal asli pada kolom `date_raw`.
2. Mengonversi tanggal ke tipe `Date`. Nilai `NaT` yang tidak dapat dikonversi menjadi null pada kolom `date`.
3. Mempertahankan artikel yang tanggalnya tidak tersedia agar informasi berita tidak langsung hilang.
4. Menghapus empat record bertanggal di luar rentang penelitian, yaitu 1 Januari 2022 sampai 31 Oktober 2023.
5. Menghapus duplikasi identik berdasarkan kombinasi `date_raw`, `link`, `title`, dan `text`.
6. Tidak menghapus seluruh artikel hanya karena memiliki URL yang sama.
7. Menyimpan hasil cleaning secara terpisah tanpa mengubah dataset mentah.

## 5. Validasi Kualitas Data

Setelah cleaning, pemeriksaan ulang menunjukkan bahwa kolom `link`, `title`, dan `text` tidak memiliki nilai null maupun string kosong. Duplikasi identik berdasarkan aturan yang digunakan juga tidak ditemukan pada dataset hasil cleaning.

Sebanyak 101.403 record masih memiliki tanggal yang tidak tersedia. Record tersebut dipertahankan dan ditandai melalui nilai null pada kolom `date`, sementara nilai aslinya tetap tersedia pada `date_raw`.

Hasil validasi dan ringkasan statistik disimpan agar proses cleaning dapat diperiksa kembali.

## 6. Reproduksibilitas

Jalankan notebook secara berurutan:

1. `notebooks/01_data_profiling.ipynb`
2. `notebooks/02_data_cleaning.ipynb`

Pastikan dataset mentah tersedia pada direktori yang ditentukan sebelum menjalankan notebook.

Dataset mentah dan hasil Parquet berukuran besar tidak perlu dimasukkan ke repository GitHub apabila melampaui batas atau dikecualikan oleh aturan repository. Dokumentasi, notebook, serta laporan yang relevan dapat disimpan di repository agar proses analisis mudah ditinjau kembali.
