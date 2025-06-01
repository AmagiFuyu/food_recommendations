Laporan Proyek Machine Learning - Submission 2: Sistem Rekomendasi Makanan Berbasis Hybrid Filtering

Project Overview

Dalam dunia modern, konsumen menghadapi banyak pilihan makanan yang tersedia. Untuk membantu pengguna dalam memilih makanan yang sesuai dengan selera dan preferensinya, sistem rekomendasi makanan menjadi sangat penting. Sistem ini dapat meningkatkan pengalaman pengguna dan menghemat waktu pencarian.

Business Understanding

Problem Statements

Pengguna sering kali kesulitan menemukan makanan yang cocok dengan selera mereka. Diperlukan sistem yang dapat memberikan rekomendasi makanan secara otomatis berdasarkan histori preferensi dan kemiripan konten makanan.

Goals

Solusi yang ditawarkan adalah membangun sistem rekomendasi makanan dengan pendekatan Hybrid Filtering, yaitu gabungan dari Content-Based Filtering dan Collaborative Filtering. Sistem ini mampu memberikan rekomendasi yang lebih akurat dengan mempertimbangkan konten makanan serta histori interaksi pengguna.

Data Understanding

Dataset

Dataset yang digunakan diunduh dari Kaggle: https://www.kaggle.com/datasets/schemersays/food-recommendation-system

Terdapat dua file utama:

food.csv: berisi metadata makanan dengan fitur:

Food_ID: ID unik untuk makanan

Name: Nama makanan

C_Type: Jenis masakan (misal: Indian, Italian)

Veg_Non: Kategori makanan (veg/non-veg)

Describe: Deskripsi singkat makanan

ratings.csv: berisi data rating makanan oleh pengguna dengan fitur:

User_ID: ID pengguna

Food_ID: ID makanan yang dirating

Rating: Nilai rating antara 1 sampai 10

Statistik Deskriptif

food.csv

Jumlah makanan: 400

Jenis makanan populer: Indian (88), Italian, Chinese

Duplikat data ditemukan pada 2 nama makanan

ratings.csv

Jumlah entri: 511

Ditemukan 1 baris dengan nilai kosong dan telah dibuang pada tahap Data Preparation

Rata-rata rating: 5.44

Data Preparation

Pra-pemrosesan Teks

Menggabungkan kolom Name, C_Type, Veg_Non, dan Describe untuk dijadikan fitur teks

Membersihkan teks: mengubah huruf menjadi kecil, menghapus karakter non-alfabet, dan stopwords

Membentuk vektor fitur menggunakan TF-IDF

Penanganan Missing Values

Ditemukan satu baris kosong dalam ratings.csv yang dihapus sebelum digunakan untuk modeling

Pembentukan Matriks

Membentuk user-item matrix untuk collaborative filtering

Menggunakan teknik matrix factorization (Truncated SVD)

Modeling

Content-Based Filtering

Menggunakan cosine similarity dari matriks TF-IDF untuk menghitung kemiripan antar makanan.

Collaborative Filtering

Menggunakan Truncated SVD untuk memprediksi rating makanan oleh pengguna yang belum memberikan rating.

Hybrid Recommendation

Menggabungkan hasil Content-Based dan Collaborative Filtering dengan skor gabungan:

> final_score = 0.5 * similarity_score + 0.5 * predicted_rating

Contoh Output Rekomendasi

Contoh hasil rekomendasi untuk user 1 dan input "chicken curry":

1. red rice
2. black rice
3. brown rice
4. mushroom rice
5. rice kheer

Evaluation

Evaluasi Numerik

Menggunakan metrik:

Precision@5: 0.25

Recall@5: 0.25

Interpretasi:

Precision@5 sebesar 0.25 berarti 25% dari makanan yang direkomendasikan termasuk dalam makanan yang pernah disukai oleh user.

Recall@5 sebesar 0.25 berarti 25% dari makanan favorit user berhasil direkomendasikan.

Hubungan dengan Business Understanding

Model telah menjawab permasalahan utama dalam project ini, yaitu memberikan rekomendasi makanan berbasis histori pengguna dan kemiripan konten.
Sistem dapat mencapai tujuan memberikan rekomendasi yang relevan. Nilai metrik evaluasi bisa ditingkatkan dengan menambah data rating dan menggunakan model yang lebih kompleks.

Kesimpulan

Sistem rekomendasi makanan berbasis Hybrid Filtering berhasil dibangun dengan menggabungkan dua pendekatan: content-based dan collaborative. Meskipun nilai Precision dan Recall belum tinggi, sistem ini menunjukkan potensi untuk memberikan rekomendasi yang relevan.

Saran Pengembangan

Menambahkan data rating dari lebih banyak pengguna.

Menambahkan fitur seperti harga, bahan utama, waktu memasak, dll.

Menggunakan model deep learning untuk content dan collaborative filtering.

Referensi

https://www.kaggle.com/datasets/schemersays/food-recommendation-system

https://scikit-learn.org

https://www.nltk.org

https://developers.google.com/machine-learning/recommendation

