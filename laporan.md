# Laporan Proyek Machine Learning - Submission 2: Sistem Rekomendasi Makanan Berbasis Hybrid Filtering

## Project Overview

Dalam dunia modern, konsumen menghadapi banyak pilihan makanan yang tersedia. Untuk membantu pengguna dalam memilih makanan yang sesuai dengan selera dan preferensinya, sistem rekomendasi makanan menjadi sangat penting. Sistem ini dapat meningkatkan pengalaman pengguna dan menghemat waktu pencarian.

## Business Understanding

### Problem Statements

1. Pengguna sering kesulitan menemukan makanan yang sesuai dengan selera mereka.

2. Diperlukan sistem yang dapat merekomendasikan makanan secara otomatis berdasarkan histori preferensi dan kemiripan konten makanan.

### Goals

1. Membangun sistem rekomendasi makanan berbasis Hybrid Filtering untuk membantu pengguna menemukan makanan yang sesuai.

2. Memastikan sistem mampu memberikan rekomendasi yang relevan dengan mempertimbangkan histori interaksi pengguna dan kemiripan konten makanan.

## Data Understanding

### Dataset

Dataset yang digunakan diunduh dari Kaggle: https://www.kaggle.com/datasets/schemersays/food-recommendation-system

Terdapat dua file utama:

1. food.csv: berisi metadata makanan dengan 400 baris dan 5 kolom:

- Food_ID: ID unik untuk setiap makanan

- Name: Nama makanan• C_Type: Jenis masakan (misal: Indian, Italian)

- Veg_Non: Kategori makanan (veg/non-veg)

- Describe: Deskripsi singkat makanan

2. ratings.csv: berisi data rating makanan oleh pengguna dengan 512 baris dan 3 kolom:

- User_ID: ID pengguna

- Food_ID: ID makanan yang dirating

- Rating: Nilai rating antara 1 sampai 10

### Kondisi Data Awal

food.csv memiliki 400 baris dan 5 kolom, tidak ada baris duplikat sepenuhnya (food_df.duplicated().sum() = 0), tetapi terdapat 2 nilai Name yang sama.

ratings.csv memiliki 512 baris dan 3 kolom, dengan 1 baris mengandung nilai kosong di kolom Rating.

## Data Preparation

### Penanganan Missing Values

Menghapus baris pada ratings.csv yang memiliki nilai kosong pada kolom `Rating (dropna())`, sehingga tersisa 511 baris.

### Pra-pemrosesan Teks

1. Mengisi nilai kosong di food.csv pada kolom teks (Name, C_Type, Veg_Non, Describe) dengan string kosong (fillna("")).

2. Membersihkan teks pada tiap kolom tersebut menggunakan fungsi `clean_text`:

- Mengubah huruf menjadi huruf kecil

- Menghapus karakter non-alfabet (dengan regex)

- Menghapus stopwords (menggunakan daftar NLTK)

3. Menggabungkan kolom`Name`, `C_Type`, `Veg_Non`, dan `Describe` menjadi satu kolom baru combined untuk ekstraksi fitur.

### Pembentukan Matriks Fitur (Content-Based)

1. Membentuk vektor fitur **TF-IDF** dari kolom `combined` (maksimal 5000 fitur).

2. Menghitung **cosine similarity** antar makanan berdasarkan vektor TF-IDF.

### Pembentukan Matriks Rating (Collaborative)

1. Membentuk user-item matrix dari hasil ratings.csv (511 pengguna × 400 makanan), mengisi nilai kosong dengan 0.

2. Menggunakan **Truncated SVD** (n_components=20) untuk dekomposisi matrix rating menjadi matriks faktor pengguna (user_factors) dan faktor item (item_factors).

3. Menghitung perkiraan rating (`predicted_ratings`) sebagai hasil perkalian `user_factors × item_factors.T`

## Modeling

### Content-Based Filtering

Menggunakan **cosine similarity** dari matriks TF-IDF untuk menghitung kemiripan antar makanan dan mendapatkan skor similarity.

### Collaborative Filtering

Menggunakan **Matrix Factorization** (Truncated SVD) pada user-item matrix untuk memprediksi rating makanan oleh pengguna.

Hybrid Recommendation

Menggabungkan hasil Content-Based dan Collaborative Filtering dengan skor gabungan:

> final_score = 0.5 * similarity_score + 0.5 * predicted_rating

### Contoh Output Rekomendasi

Berikut adalah output rekomendasi Top-5 untuk **user_id = 1** dan **input = "rice"** di notebook:

1. red rice
2. black rice
3. brown rice
4. mushroom rice
5. rice kheer

Catatan: Fungsi  hybrid_recommendation(1, "rice", top_n=5) menggunakan user_id = 1 (numerik), bukan string.

## Evaluation

### Evaluasi Numerik

Menggunakan metrik:

- Precision@4: 0.25

- Recall@4: 0.25

Interpretasi:

- Precision@4 sebesar 0.25 berarti 25% dari 4 rekomendasi teratas cocok dengan makanan favorit user.

- Recall@4 sebesar 0.25 berarti 25% dari makanan favorit user direkomendasikan.

### Hubungan dengan Business Understanding

- Model ini telah menjawab problem statement: memberikan rekomendasi otomatis yang relevan berdasarkan histori preferensi dan konten.

- Goals terpenuhi dengan membangun sistem hybrid yang menggabungkan kedua pendekatan.

- Dengan metrik evaluasi tersebut, sistem memberikan rekomendasi yang cukup relevan, namun perlu ditingkatkan untuk akurasi yang lebih tinggi.

## Kesimpulan

Sistem rekomendasi makanan berbasis Hybrid Filtering berhasil dibangun dengan menggabungkan dua pendekatan: content-based dan collaborative. Output rekomendasi telah diverifikasi sesuai notebook. Meskipun metrik Precision dan Recall masih rendah, sistem menunjukkan potensi yang baik.

## Saran Pengembangan

- Menambahkan data rating dari lebih banyak pengguna untuk meningkatkan kualitas Collaborative Filtering.

- Menambahkan fitur tambahan (harga, bahan utama, waktu memasak) ke dalam content-based filtering.

- Mengeksplorasi model machine learning atau deep learning yang lebih kompleks.

## Referensi

1. https://www.kaggle.com/datasets/schemersays/food-recommendation-system

2. https://scikit-learn.org

3. https://www.nltk.org

4. https://developers.google.com/machine-learning/recommendation

