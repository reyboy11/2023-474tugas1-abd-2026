# tugas1-reyboy11

# Indonesian News Big Data Analysis

## Deskripsi Project

Project ini merupakan implementasi eksplorasi dan analisis Big Data menggunakan **Indonesian News Dataset (`idn-news-az`)**, yaitu dataset yang berisi kumpulan artikel berita berbahasa Indonesia dari berbagai portal berita daring.

Dataset diproses menggunakan pendekatan Big Data dengan **Polars Lazy API** agar pembacaan dan transformasi data dapat dilakukan secara efisien tanpa harus memuat seluruh dataset ke memori sejak awal.

Project ini dikembangkan secara bertahap mulai dari profiling data, data cleaning dan validasi kualitas, analisis menggunakan DuckDB, eksplorasi data, analisis temporal, visualisasi interaktif, hingga penyusunan insight berdasarkan hasil analisis.

---

## Dataset

**Nama Dataset:**  
Indonesian News Dataset (`idn-news-az`)

**Sumber Dataset:**  
https://huggingface.co/datasets/esteler-ai/idn-news-az

Dataset berisi kumpulan artikel berita berbahasa Indonesia yang berasal dari berbagai sumber berita daring.

### Informasi Dataset

- Format data: Parquet
- Jumlah file: 441 file Parquet
- Ukuran dataset lokal: sekitar 1.5 GB
- Jumlah data: 1.149.789 baris
- Bahasa: Indonesia
- Unit analisis: satu artikel berita

### Struktur Kolom

| Kolom | Deskripsi |
|---|---|
| `date` | Tanggal publikasi berita |
| `link` | URL sumber artikel berita |
| `title` | Judul artikel berita |
| `text` | Isi artikel berita |

Dataset memenuhi ketentuan Tugas 1 karena memiliki ukuran lebih dari 500 MB dan jumlah observasi lebih dari satu juta baris.

---

## Tujuan Project

Project ini bertujuan untuk:

- Melakukan profiling awal terhadap dataset berita berukuran besar.
- Mengetahui struktur, ukuran, dan karakteristik dataset.
- Menggunakan Polars Lazy API untuk pemrosesan data secara efisien.
- Melakukan pemeriksaan missing values, duplikasi, outlier, dan aturan kualitas data.
- Menggunakan DuckDB untuk profiling dan query analitik berbasis SQL.
- Melakukan eksplorasi serta analisis pola temporal pada data berita.
- Membuat visualisasi interaktif untuk mendukung hasil analisis.
- Menghasilkan insight berdasarkan hasil pengolahan data.
- Menyediakan environment yang dapat dijalankan ulang melalui Docker.

---

## Teknologi yang Digunakan

Project ini menggunakan:

- Python
- Polars
- DuckDB
- PyArrow
- Plotly
- JupyterLab
- Docker
- Git dan GitHub
- Parquet

Polars digunakan sebagai library utama untuk manipulasi data dengan pendekatan Lazy API, sedangkan DuckDB digunakan untuk query analitik berbasis SQL.

---

## Struktur Repository

```text
tugas1-reyboy11/
├── .github/
│   └── workflows/
│       └── lint_check.yml
├── data/
│   ├── README.md
│   └── raw/
│       └── idn-news/
│           └── data_files/
│               └── *.parquet
├── notebooks/
│   ├── 01_data_profiling.ipynb
│   ├── 02_data_cleaning.ipynb
│   └── 03_eda_and_insights.ipynb
├── output/
│   └── figures/
├── src/
├── Dockerfile
├── requirements.txt
├── .gitignore
└── README.md
```

Folder `data/raw/` tidak dimasukkan ke repository GitHub karena berisi dataset mentah berukuran besar.

---

## Tahapan Analisis

### 1. Data Profiling

Notebook:

`notebooks/01_data_profiling.ipynb`

Tahap profiling meliputi:

- Membaca kumpulan file Parquet menggunakan `pl.scan_parquet()`.
- Menghitung jumlah file dan ukuran dataset.
- Memeriksa schema dataset.
- Menghitung jumlah observasi.
- Menampilkan sampel data.
- Memeriksa missing values.
- Memeriksa rentang tanggal publikasi.

### 2. Data Cleaning

Notebook:

`notebooks/02_data_cleaning.ipynb`

Tahap ini digunakan untuk melakukan pemeriksaan dan penanganan kualitas data menggunakan Polars serta profiling analitik menggunakan DuckDB.

### 3. EDA dan Insight

Notebook:

`notebooks/03_eda_and_insights.ipynb`

Tahap ini digunakan untuk eksplorasi data, analisis temporal, visualisasi interaktif, dan penyusunan insight berdasarkan hasil analisis.

---

## Hasil Profiling Awal

Berdasarkan profiling awal diperoleh:

- Dataset terdiri dari 441 file Parquet.
- Ukuran dataset lokal sekitar 1.5 GB.
- Dataset memiliki 1.149.789 baris.
- Dataset memiliki empat kolom utama, yaitu `date`, `link`, `title`, dan `text`.
- Pada profiling awal tidak ditemukan nilai null pada empat kolom utama.
- Dataset dapat diproses menggunakan Polars Lazy API.

Hasil profiling menjadi dasar untuk proses data cleaning dan analisis pada tahap selanjutnya.

---

## Cara Mendapatkan Dataset

Dataset tidak disimpan langsung pada repository karena ukuran file yang besar.

Dataset dapat diperoleh melalui:

https://huggingface.co/datasets/esteler-ai/idn-news-az

Dataset kemudian ditempatkan pada:

```text
data/raw/idn-news/data_files/
```

Struktur lokal:

```text
data/
└── raw/
    └── idn-news/
        └── data_files/
            ├── *.parquet
            └── ...
```

---

## Menjalankan Project

Install dependency menggunakan:

```bash
pip install -r requirements.txt
```

Kemudian jalankan JupyterLab:

```bash
jupyter lab
```

Project juga dapat dijalankan menggunakan Docker.

Build Docker image:

```bash
docker build -t tugas1-bigdata .
```

Jalankan container:

```bash
docker run --rm -p 8888:8888 -v "$(pwd)":/home/jovyan/work tugas1-bigdata
```

Kemudian buka:

```text
http://localhost:8888/lab
```

---

## Catatan

Dataset mentah tidak dimasukkan ke repository GitHub.

Repository hanya menyimpan kode, notebook, dokumentasi, serta file konfigurasi yang diperlukan agar proses analisis dapat dijalankan ulang.

---

## AI Disclosure Statement

**Alat AI yang digunakan:**  
ChatGPT

**Bagian yang dibantu:**  
AI digunakan untuk membantu memahami instruksi tugas, menjelaskan konsep, membantu debugging error, melakukan review dokumentasi project, serta membantu pengecekan struktur repository.

**Verifikasi yang dilakukan:**  
Setiap kode dijalankan ulang secara mandiri. Hasil analisis diperiksa kembali dan setiap bagian project dipahami sebelum dilakukan pengumpulan.

---

## Author

**Nama:** M. Raihan Abdi  
**NIM:** 202310370311474
