# Laporan Proyek Machine Learning - Rifky Muhammad Shidiq

## Project Overview

Perpustakaan memberikan akses pada informasi yang penting bagi mahasiswa untuk mendalami materi perkuliahan. Namun, mencari buku yang sesuai dengan minat pengunjung perpustakaan bisa menjadi sulit tanpa bantuan. Oleh karena itu, pengembangan sistem rekomendasi otomatis menjadi penting. Sistem ini membantu mahasiswa menemukan buku yang sesuai dengan minat mereka, menggantikan proses manual yang rumit. Salah satu pendekatan yang umum digunakan dalam sistem rekomendasi adalah collaborative filtering, yang mempertimbangkan preferensi dan penilaian dari sekelompok pengguna untuk memberikan rekomendasi. Metode item-based collaborative filtering, misalnya, menyarankan buku yang mirip dengan buku yang disukai oleh pengguna. Pendekatan ini membagi jenis rekomendasi menjadi dua, yaitu user-based dan item-based, di mana item-based lebih fokus pada kesamaan antar item.


  





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

## Data Preprocessing
Ini merupakan tahap persiapan data sebelum data digunakan untuk proses selanjutnya. Pada tahap ini, Anda akan melakukan penggabungan beberapa file sehingga menjadi satu kesatuan file yang utuh dan siap digunakan dalam tahap pemodelan
1. Penggabungan Data
- **Merge ratings dengan books** : Menggabungkan data frame "ratings" dengan data frame "books" berdasarkan atribut "ISBN". Hal ini dilakukan untuk menggabungkan informasi peringkat buku dengan informasi judul buku.
- **Drop kolom yang tidak diperlukan dari books** : Kolom yang tidak diperlukan seperti "ISBN", "Image-URL-S", dan "Image-URL-M" dihapus dari data frame hasil merge untuk mengurangi redundansi dan memperbaiki kejelasan data.
- **Merge hasil sebelumnya dengan data pengguna (users)** : Menggabungkan data frame yang telah di-merge sebelumnya dengan data frame "users" berdasarkan atribut "User-ID". Ini dilakukan untuk menambahkan informasi pengguna ke dalam data frame, sehingga informasi lengkap tentang peringkat buku, judul buku, dan pengguna dapat diakses dalam satu data frame.
- **Drop kolom "Age" dari users**: Menghapus kolom "Age" dari data frame pengguna karena tidak diperlukan dalam data frame yang lengkap.

## Data Preparation
Data mentah yang telah diperoleh dari kaggle harus melakukan data preparation terlebih dahulu dengan tujuan agar data mentah tersebut dapat digunakan ke tahap selanjutnya yaitu permodelan. Proses yang harus dilakukan pada data preparation adalah :
1. Cek Missing Value
- Dataframe "books" mengalami missing value di beberapa atribut seperti book_author, publisher, dan image_l_url. Namun, jumlah nilai yang hilang relatif kecil dibandingkan dengan total entri data. Oleh karena itu, akan digunakan fungsi drop() untuk menghapus baris yang memiliki nilai kosong pada atribut tersebut.
- Dataframe "Users" memiliki sebanyak 110,762 nilai yang hilang pada fitur usia. Untuk menangani masalah ini, nilai-nilai yang hilang akan diganti dengan angka 0. Tujuan dari penggantian nilai yang hilang dengan angka 0 adalah untuk memberikan representasi yang jelas bahwa nilai usia tersebut tidak tersedia atau tidak diketahui. Dengan menggunakan angka 0, kita secara eksplisit menandai bahwa tidak ada nilai usia yang tersedia untuk entri data tersebut yang dapat membantu dalam analisis data, karena nilai 0 akan membedakan entri yang memiliki nilai usia yang diketahui dengan entri yang tidak memiliki nilai usia

2. Cek duplikasi data
Setelah dilakukan pengecekan, tidak ditemukan adanya duplikasi data pada ketiga tabel yaitu buku, users, dan ratings. Sehingga dapat dilakukan ke tahap selanjutnya


## Modeling
1. Cosine Similarity
Cosine similarity adalah metode yang umum digunakan dalam sistem rekomendasi untuk mengukur kesamaan antara dua item berdasarkan vektor representasinya. Kemudian fungsi recommend() digunakan untuk merekomendasikan buku yang mirip dengan buku yang diberikan oleh pengguna. Langkah-langkahnya adalah sebagai berikut:

Pertama, indeks buku yang sesuai dengan judul buku yang diberikan dicari dalam matriks pivot table (pt). Setiap baris mewakili sebuah buku, sehingga indeks buku tersebut diidentifikasi.
Kemudian, kesamaan kosinus antara buku yang diberikan dan semua buku lainnya dihitung menggunakan metode cosine_similarity. Similaritas ini merepresentasikan seberapa mirip setiap buku dengan buku yang diberikan.
Hasil kesamaan kosinus diurutkan dari yang tertinggi ke terendah, dan 5 buku dengan kesamaan tertinggi (kecuali buku itu sendiri) dipilih sebagai rekomendasi.
Informasi tentang buku-buku yang direkomendasikan, termasuk judul, penulis, dan URL gambar, diambil dari DataFrame "books" berdasarkan indeks buku yang sesuai.
Data tentang buku-buku yang direkomendasikan disusun dalam bentuk list dan dikembalikan sebagai output dari fungsi recommend().

Berdasarkan langkah-langkah tersebut akan dilakukan pencarian menggunakan fungsi recomend() pada buku "A Walk to Remember" maka hasilnya seperti berikut:

Berdasarkan Gambar 1. hasil rekomendasi buku untuk buku dengan judul "A Walk to Remember". Rekomendasi ini didasarkan pada kesamaan dengan buku yang diberikan menggunakan metode cosine similarity. Berikut adalah penjelasan untuk setiap buku yang direkomendasikan:

1. The Rescue oleh Nicholas Sparks: Buku ini ditulis oleh penulis yang sama dengan buku yang diberikan, yaitu Nicholas Sparks. Hal ini menunjukkan adanya kesamaan dalam gaya penulisan atau tema antara kedua buku tersebut.
2. Nights in Rodanthe oleh Nicholas Sparks: Ini adalah buku yang ditulis oleh Nicholas Sparks, menunjukkan adanya kesamaan dengan buku yang diberikan.
3. The Notebook oleh Nicholas Sparks: Buku ini juga ditulis oleh Nicholas Sparks, yang menunjukkan bahwa penulis ini memiliki beberapa buku yang mirip atau relevan dengan buku yang diberikan.
4. Granny Dan oleh DANIELLE STEEL: Meskipun buku ini ditulis oleh penulis yang berbeda, yaitu DANIELLE STEEL, buku ini direkomendasikan karena memiliki kesamaan dengan buku yang diberikan, mungkin dalam hal genre atau tema tertentu.
5. A Bend in the Road oleh Nicholas Sparks: Sekali lagi, buku ini ditulis oleh Nicholas Sparks, menunjukkan adanya kesamaan dengan buku yang diberikan.


3. Algoritma Singular Value Decomposition (SVD) untuk membangun model rekomendasi berbasis kolaboratif.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
