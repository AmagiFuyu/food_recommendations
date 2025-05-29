# Laporan Proyek Machine Learning - Submission 2: Sistem Rekomendasi Makanan Berbasis Hybrid Filtering

# 1. Pendahuluan

## Latar Belakang

Dalam dunia modern, konsumen menghadapi banyak pilihan makanan yang tersedia. Untuk membantu pengguna dalam memilih makanan yang sesuai dengan selera dan preferensinya, sistem rekomendasi makanan menjadi sangat penting. Sistem ini dapat meningkatkan pengalaman pengguna dan menghemat waktu pencarian.

## Permasalahan

Pengguna sering kali kesulitan menemukan makanan yang cocok dengan selera mereka. Diperlukan sistem yang dapat memberikan rekomendasi makanan secara otomatis berdasarkan histori preferensi dan kemiripan konten makanan.

## Solusi

Solusi yang ditawarkan adalah membangun sistem rekomendasi makanan dengan pendekatan Hybrid Filtering, yaitu gabungan dari Content-Based Filtering dan Collaborative Filtering. Sistem ini mampu memberikan rekomendasi yang lebih akurat dengan mempertimbangkan konten makanan serta histori interaksi pengguna.

# 2. Data Understanding

# Dataset

Dataset yang digunakan diunduh dari Kaggle: https://www.kaggle.com/datasets/schemersays/food-recommendation-system

Terdapat dua file utama:

1. food.csv: berisi metadata makanan (id, name, cuisine, course, diet)

2. ratings.csv: berisi data rating makanan oleh pengguna (userId, foodId, rating)

## Statistik Deskriptif

Jumlah makanan: 400 makanan

Jumlah rating: 511

Distribusi rating menunjukkan bahwa sebagian besar makanan memiliki rating antara 3 hingga 5. Jenis makanan (cuisine) yang paling populer adalah Indian, Healthy Food, dan Dessert.

# 3. Data Preparation

## Pra-pemrosesan Teks

Membersihkan teks dengan menghilangkan karakter non-alfabet, mengubah menjadi huruf kecil, dan menghapus stopwords.

Menggabungkan kolom name, cuisine, course, dan diet untuk dijadikan fitur teks.

## Pembentukan Matriks

Membentuk matriks TF-IDF dari gabungan teks untuk menghitung similarity antar makanan.

Membentuk matriks user-item dari data rating.

Menggunakan Truncated SVD untuk dekomposisi matriks rating (Collaborative Filtering).

# 4. Modeling

## Content-Based Filtering

Menggunakan cosine similarity dari matriks TF-IDF untuk menghitung kemiripan antar makanan.

## Collaborative Filtering

Menggunakan teknik Matrix Factorization dengan Truncated SVD untuk memprediksi rating makanan oleh pengguna yang belum pernah memberikan rating.

## Hybrid Recommendation

Menggabungkan hasil Content-Based dan Collaborative Filtering dengan skor gabungan:

**final_score = alpha * similarity_score + (1 - alpha) * predicted_rating**
- similarity_score: skor kemiripan makanan berbasis konten.

- predicted_rating: rating yang diprediksi dari Collaborative Filtering.

- alpha: parameter untuk mengatur proporsi antara kedua pendekatan

# 5. Evaluation

## Evaluasi Manual

Menampilkan metadata makanan hasil rekomendasi untuk melihat relevansinya secara manual.

## Evaluasi Numerik

Menggunakan metrik:

1. Precision: 0.25

2. Recall: 0.25

Interpretasi:

1. Precision sebesar 0.25 berarti 25% dari makanan yang direkomendasikan masuk dalam daftar makanan favorit user.

2. Recall sebesar 0.25 berarti 25% dari makanan favorit user berhasil direkomendasikan.

Nilai ini cukup, namun dapat ditingkatkan lagi dengan menggunakan data rating yang lebih lengkap atau model yang lebih kompleks.

# 6. Kesimpulan

Sistem rekomendasi makanan berbasis Hybrid Filtering berhasil dibangun dengan menggabungkan dua pendekatan: content-based dan collaborative. Meskipun nilai Precision dan Recall belum tinggi, sistem ini menunjukkan potensi untuk memberikan rekomendasi yang relevan.

# 7. Saran Pengembangan

Menambahkan data rating dari lebih banyak pengguna.

Menambahkan fitur seperti harga, bahan utama, waktu memasak, dll.

Menggunakan model deep learning untuk content dan collaborative filtering.

# 8. Referensi

https://www.kaggle.com/datasets/schemersays/food-recommendation-system

https://scikit-learn.org

https://www.nltk.org

https://developers.google.com/machine-learning/recommendation

