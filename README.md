# 📄 Proyek Case-Based Reasoning untuk Analisis Putusan Narkotika

Proyek ini mengimplementasikan sistem Case-Based Reasoning (CBR) sederhana menggunakan Python untuk mendukung analisis putusan pengadilan, khususnya dalam domain pidana Narkotika. Sistem ini dirancang untuk dapat dijalankan di Google Colaboratory (Colab).

## 📝 Deskripsi Proyek

Sistem CBR ini memanfaatkan data putusan Mahkamah Agung Republik Indonesia terkait kasus Narkotika. Alur kerja sistem mengikuti siklus CBR:

1. **Pembangunan Case Base**: Pengumpulan dan pembersihan dokumen putusan.
2. **Representasi Kasus**: Ekstraksi metadata dan fitur penting dari setiap putusan.
3. **Retrieval Kasus**: Pencarian kasus lama yang paling mirip dengan kasus baru menggunakan representasi vektor (TF-IDF atau BERT).
4. **Penggunaan Kembali Solusi**: Mengambil amar putusan dari kasus termirip sebagai prediksi solusi.
5. **Evaluasi Model**: Pengukuran performa sistem menggunakan metrik standar.

## 🚀 Cara Menjalankan Proyek (End-to-End Pipeline)

### 1️⃣ Persiapan File Data

- **Unduh File ZIP Data Anda**: Pastikan Anda memiliki file ZIP yang berisi minimal 30 dokumen putusan Narkotika (PDF atau TXT).
- **Unggah ke Google Drive**.
- **Atur Izin Berbagi**: "Anyone with the link" dengan akses "Viewer".
- **Dapatkan File ID**: Dari link Google Drive, salin file\_id (contoh: `1SFLWcPuvggeTYbFMNrTAnzz0BxCisDM8`).

### 2️⃣ Membuka dan Menjalankan di Google Colab

1. Buka Google Colab dan buat notebook baru.
2. (Opsional) Ganti runtime ke GPU: `Runtime > Change runtime type > GPU`.
3. Salin setiap blok kode (SEL 0.1 hingga SEL 5) ke sel terpisah di notebook Anda.
4. Modifikasi SEL 0.1: Ubah `file_id_zip` menjadi ID file Drive Anda.
5. Jalankan sel secara berurutan dan perhatikan output.

### 3️⃣ Struktur Direktori Hasil

```plaintext
/cbr_narkotika_project/
├── data/
│   ├── raw/                   # File putusan .txt
│   ├── processed/             # cases.csv
│   ├── eval/                  # queries.json, retrieval_metrics.csv, retrieval_performance_bar_chart.png
│   └── results/               # predictions.csv
├── logs/                      # cleaning.log (opsional)
├── notebooks/                 # Notebook Colab (.ipynb)
├── scripts/                   # data_processor.py, dll.
├── requirements.txt           # Library Python yang dibutuhkan
└── README.md                  # File ini
```

## 📦 requirements.txt

Contoh isi:

```plaintext
pandas
numpy
scikit-learn
transformers
beautifulsoup4
requests
pdfminer.six
gdown
matplotlib
torch
```

> Anda bisa membuatnya dengan menjalankan `!pip freeze > requirements.txt` di Colab.

## ⚙️ Contoh Penggunaan

```python
# Contoh Retrieval
query_baru = "kasus kepemilikan ganja dengan berat 5 kilogram"
top_kasus_ids, skor_kemiripan = retrieve(
    query_baru, k=3, df_cases=df_cases, vectorizer_tfidf=vectorizer_tfidf,
    tfidf_matrix=tfidf_matrix, retrieval_type='tfidf'
)
print(f"Query: {query_baru}")
print(f"Top 3 Kasus Termirip (IDs): {top_kasus_ids}")
print(f"Skor Kemiripan: {skor_kemiripan}")

# Contoh Prediksi Solusi
solusi_terprediksi, kasus_dasar_ids = predict_outcome(
    query_baru, k=5, df_cases=df_cases, vectorizer_tfidf=vectorizer_tfidf,
    tfidf_matrix=tfidf_matrix, retrieval_type='tfidf'
)
print(f"Solusi Terprediksi: {solusi_terprediksi}")
print(f"Berdasarkan kasus ID: {kasus_dasar_ids}")
```

## 📚 Sumber

- Data putusan diambil dari [Direktori Putusan Mahkamah Agung RI](https://putusan3.mahkamahagung.go.id).
- Library dan model NLP seperti IndoBERT digunakan melalui `transformers`.

---

✅ Proyek ini diharapkan dapat menjadi contoh sederhana implementasi CBR untuk mendukung analisis hukum berbasis data.

