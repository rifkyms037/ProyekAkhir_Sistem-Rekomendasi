# Laporan Proyek Machine Learning - Nama Anda

## Project Overview

Perpustakaan memberikan akses pada informasi yang penting bagi mahasiswa untuk mendalami materi perkuliahan. Namun, mencari buku yang sesuai dengan minat pengunjung perpustakaan bisa menjadi sulit tanpa bantuan. Oleh karena itu, pengembangan sistem rekomendasi otomatis menjadi penting. Sistem ini membantu mahasiswa menemukan buku yang sesuai dengan minat mereka, menggantikan proses manual yang rumit. Salah satu pendekatan yang umum digunakan dalam sistem rekomendasi adalah collaborative filtering, yang mempertimbangkan preferensi dan penilaian dari sekelompok pengguna untuk memberikan rekomendasi. Metode item-based collaborative filtering, misalnya, menyarankan buku yang mirip dengan buku yang disukai oleh pengguna. Pendekatan ini membagi jenis rekomendasi menjadi dua, yaitu user-based dan item-based, di mana item-based lebih fokus pada kesamaan antar item.


  



**Rubrik/Kriteria Tambahan (Opsional)**:
- Jelaskan mengapa proyek ini penting untuk diselesaikan.
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
  
  Format Referensi: [Judul Referensi](https://scholar.google.com/) 

## Business Understanding

Pada bagian ini, Anda perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah:
- Pengunjung perpustakaan sering kesulitan menemukan buku yang sesuai dengan minat mereka di perpustakaan.
- Proses pencarian buku di perpustakaan masih dilakukan secara manual, yang memakan waktu dan tidak efisien.

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Mengembangkan sistem rekomendasi yang dapat membantu pengunjung perpustakaan menemukan buku yang sesuai dengan minat mereka.
- Mengimplementasikan sistem rekomendasi untuk mempercepat dan mempermudah proses pencarian buku di perpustakaan
- Jawaban pernyataan masalah n

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.


## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [Kaggle](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).
Dalam tahapan ini, berfokus pada pemahaman tentang data yang digunakan dalam proyek sistem rekomendasi buku. Dataset yang digunakan diperoleh dari penyedia dataset online yaitu website [Kaggle](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset/) yang terdiri dari 3 file csv yaitu Buku dengan 271360 record dan 8 atribut, User dengan 1149780 record dan 3 atribut, dan ratings dengan 278858 dan 3 atribut.

Tabel 1. Tabel Buku


Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
