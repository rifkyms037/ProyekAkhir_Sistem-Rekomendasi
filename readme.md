# Laporan Proyek Machine Learning - Rifky Muhammad Shidiq

## Project Overview

Perpustakaan memberikan akses pada informasi yang penting bagi mahasiswa untuk mendalami materi perkuliahan. Namun, mencari buku yang sesuai dengan minat pengunjung perpustakaan bisa menjadi sulit tanpa bantuan. Oleh karena itu, pengembangan sistem rekomendasi otomatis menjadi penting. Sistem ini membantu mahasiswa menemukan buku yang sesuai dengan minat mereka, menggantikan proses manual yang rumit. Salah satu pendekatan yang umum digunakan dalam sistem rekomendasi adalah collaborative filtering, yang mempertimbangkan preferensi dan penilaian dari sekelompok pengguna untuk memberikan rekomendasi. Metode item-based collaborative filtering, misalnya, menyarankan buku yang mirip dengan buku yang disukai oleh pengguna. Pendekatan ini membagi jenis rekomendasi menjadi dua, yaitu user-based dan item-based, di mana item-based lebih fokus pada kesamaan antar item.


  



**Rubrik/Kriteria Tambahan (Opsional)**:
- Jelaskan mengapa proyek ini penting untuk diselesaikan.
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
  
  Format Referensi: [Judul Referensi](https://scholar.google.com/) 

## Business Understanding

Pada bagian ini, membahas proses klarifikasi masalah yang menjadi dasar dari proyek rekomendasi sistem perpustakaan.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah:
- Bagaimana membuat sistem rekomendasi dengan teknik collaborative filtering untuk mempermudah pengguna memperoleh rekomendasi?
- Bagaimana hasil evaluasi model algoritma SVD dalam sistem rekomendasi menggunakan MSE?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Untuk membuat sistem rekomendasi buku menggunakan teknik collaborative filtering
- Untuk mengetahui hasil evaluasi model algoritma SVD dalam sistem rekomendasi menggunakan MSE



## Data Understanding
Dalam tahapan ini, berfokus pada pemahaman tentang data yang digunakan dalam proyek sistem rekomendasi buku. Dataset yang digunakan diperoleh dari penyedia dataset online yaitu website [Kaggle](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset/) yang terdiri dari 3 file csv yaitu Buku dengan 271360 record dan 8 atribut, User dengan 1149780 record dan 3 atribut, dan ratings dengan 278858 dan 3 atribut.

Tabel 1. Tabel Buku
| ISBN       | Book-Title                                        | Book-Author          | Year-Of-Publication | Publisher                  | Image-URL-S                                       |
|------------|---------------------------------------------------|----------------------|---------------------|----------------------------|---------------------------------------------------|
| 0195153448 | Classical Mythology                               | Mark P. O. Morford   | 2002                | Oxford University Press    | http://images.amazon.com/images/P/0195153448.0... |
| 0002005018 | Clara Callan                                      | Richard Bruce Wright | 2001                | HarperFlamingo Canada      | http://images.amazon.com/images/P/0002005018.0... |
| 0060973129 | Decision in Normandy                              | Carlo D'Este         | 1991                | HarperPerennial            | http://images.amazon.com/images/P/0060973129.0... |
| 0374157065 | Flu: The Story of the Great Influenza Pandemic... | Gina Bari Kolata     | 1999                | Farrar Straus Giroux       | http://images.amazon.com/images/P/0374157065.0... |
| 0393045218 | The Mummies of Urumchi                            | E. J. W. Barber      | 1999                | W. W. Norton &amp; Company | http://images.amazon.com/images/P/0393045218.0... |

Atribut dalam Tabel 1. adalah :

1. ISBN: International Standard Book Number, merupakan kode unik yang digunakan untuk mengidentifikasi sebuah buku secara global.
2. Book-Title: Judul dari buku.
3. Book-Author: Nama penulis atau penulis-penulis buku.
4. Year-Of-Publication: Tahun publikasi buku.
5. Publisher: Penerbit buku.
6. Image-URL-S, Image-URL-M, Image-URL-L: URL gambar cover buku dalam tiga ukuran berbeda (kecil, sedang, besar).

Tabel 2. Tabel User
| User-ID |                           Location |  Age |
|--------:|-----------------------------------:|-----:|
|       1 |                 nyc, new york, usa |  NaN |
|       2 |          stockton, california, usa | 18.0 |
|       3 |    moscow, yukon territory, russia |  NaN |
|       4 |          porto, v.n.gaia, portugal | 17.0 |
|       5 | farnborough, hants, united kingdom |  NaN |

Atribut dalam Tabel 2. adalah :

1. User-ID: Identifikasi unik untuk setiap pengguna. Setiap pengguna memiliki nomor ID yang berbeda.
2. Location: Menunjukkan lokasi geografis dari pengguna, di mana pengguna tersebut tinggal atau berada. 
3. Age: Usia pengguna. 

Tabel 3. Tabel Ratings
| User-ID |       ISBN | Book-Rating |
|--------:|-----------:|------------:|
|  276725 | 034545104X |           0 |
|  276726 | 0155061224 |           5 |
|  276727 | 0446520802 |           0 |
|  276729 | 052165615X |           3 |
|  276729 | 0521795028 |           6 |

Atribut dalam Tabel 3. adalah :

1. User-ID: Ini adalah identifikasi unik untuk setiap pengguna yang memberikan peringkat pada buku tertentu.
2. ISBN: International Standard Book Number, merupakan kode unik yang digunakan untuk mengidentifikasi sebuah buku secara global.
3. Book-Rating: Ini adalah peringkat yang diberikan oleh pengguna (dalam skala tertentu) terhadap buku yang sesuai dengan ISBN tertentu. Di mana 0 mungkin menunjukkan bahwa pengguna tidak memberikan peringkat, dan peringkat yang lebih tinggi menunjukkan tingkat kepuasan atau preferensi yang lebih tinggi terhadap buku tersebut.


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
