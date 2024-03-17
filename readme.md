# Laporan Proyek Machine Learning - Rifky Muhammad Shidiq

## Project Overview

Sistem rekomendasi telah menjadi bagian integral dari platform digital yang menawarkan berbagai produk dan layanan, termasuk buku. Dalam konteks industri penerbitan dan perdagangan buku online, penting untuk memiliki sistem yang dapat memberikan rekomendasi yang relevan dan personal kepada pengguna. Salah satu pendekatan yang umum digunakan dalam pengembangan sistem rekomendasi adalah collaborative filtering.

Collaborative filtering adalah teknik yang memanfaatkan data historis tentang preferensi pengguna untuk menghasilkan rekomendasi untuk pengguna lain yang memiliki profil serupa. Pendekatan ini telah terbukti efektif dalam berbagai domain, termasuk e-commerce dan hiburan.

Dalam konteks sistem rekomendasi buku, collaborative filtering memungkinkan identifikasi pola perilaku pembaca dan preferensi buku berdasarkan riwayat interaksi pengguna dengan buku-buku tertentu. Dengan menggunakan metode ini, platform dapat merekomendasikan buku-buku yang kemungkinan besar diminati oleh pengguna berdasarkan kesamaan preferensi dengan pengguna lain yang memiliki profil serupa.

Dengan memahami pola pembaca dan preferensi buku, diharapkan bahwa pengembangan sistem rekomendasi buku berbasis collaborative filtering akan memberikan manfaat bagi industri penerbitan dan perdagangan buku online dengan meningkatkan pengalaman pengguna dan meningkatkan penjualan buku.


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
Ini merupakan tahap persiapan data sebelum data digunakan untuk proses selanjutnya. 

1. Melakukan penggabungan beberapa file sehingga menjadi satu kesatuan file yang utuh dan siap digunakan dalam tahap pemodelan

- **Merge ratings dengan books** : Menggabungkan data frame "ratings" dengan data frame "books" berdasarkan atribut "ISBN". Hal ini dilakukan untuk menggabungkan informasi peringkat buku dengan informasi judul buku.
- **Drop kolom yang tidak diperlukan dari books** : Kolom yang tidak diperlukan seperti "ISBN", "Image-URL-S", dan "Image-URL-M" dihapus dari data frame hasil merge untuk mengurangi redundansi dan memperbaiki kejelasan data.
- **Merge hasil sebelumnya dengan data pengguna (users)** : Menggabungkan data frame yang telah di-merge sebelumnya dengan data frame "users" berdasarkan atribut "User-ID". Ini dilakukan untuk menambahkan informasi pengguna ke dalam data frame, sehingga informasi lengkap tentang peringkat buku, judul buku, dan pengguna dapat diakses dalam satu data frame.
- **Drop kolom "Age" dari users**: Menghapus kolom "Age" dari data frame pengguna karena tidak diperlukan dalam data frame yang lengkap.

2. Pemfilteran dan Seleksi Data untuk Collaborative Filtering

- Seleksi Pengguna dengan Lebih dari 200 Penilaian Buku: Di sini, kita memilih pengguna yang memiliki lebih dari 200 penilaian buku sebagai ambang batas minimum untuk pengguna yang berpengetahuan. Ini dilakukan untuk memastikan kita hanya mempertimbangkan pengguna yang cukup aktif dan berpengetahuan saat membangun model rekomendasi.
- Perhitungan Jumlah Penilaian Buku per Pengguna: Langkah ini melibatkan penghitungan jumlah penilaian buku yang diberikan oleh setiap pengguna.
- Pemfilteran Pengguna Berpengetahuan: Setelah perhitungan jumlah penilaian buku per pengguna, kita memfilter pengguna yang memiliki lebih dari ambang batas minimum penilaian (200) untuk dianggap sebagai pengguna yang berpengetahuan.
- Pemfilteran Penilaian dari Pengguna yang Berpengetahuan: Di sini, kita hanya mempertimbangkan penilaian buku dari pengguna yang telah dipilih sebelumnya sebagai pengguna yang berpengetahuan.
- Pemfilteran Buku yang Populer: Langkah ini melibatkan perhitungan jumlah penilaian untuk setiap judul buku dan pemfilteran hanya pada buku-buku yang telah menerima sejumlah penilaian yang memenuhi ambang batas minimum tertentu (50 penilaian dalam kasus ini).
- Pivot Table (Tabel Pivot): Data yang telah difilter dan diproses selanjutnya diubah menjadi bentuk tabel pivot, di mana barisnya mewakili judul buku dan kolomnya mewakili ID pengguna, dengan nilai-nilai penilaian buku diisi di dalam sel-selnya. Hal ini akan memudahkan analisis dan pemodelan lebih lanjut.
- Pengisian Nilai NaN dengan 0: Langkah terakhir adalah mengisi nilai-nilai yang hilang (NaN) dalam tabel pivot dengan nilai 0. Hal ini dilakukan agar kita dapat menggunakan metode yang sesuai untuk pemodelan lebih lanjut tanpa kehilangan data.

## Data Preparation
Data mentah yang telah diperoleh dari kaggle harus melakukan data preparation terlebih dahulu dengan tujuan agar data mentah tersebut dapat digunakan ke tahap selanjutnya yaitu permodelan. Proses yang harus dilakukan pada data preparation adalah :
1. Cek Missing Value

- Dataframe "books" mengalami missing value di beberapa atribut seperti book_author, publisher, dan image_l_url. Namun, jumlah nilai yang hilang relatif kecil dibandingkan dengan total entri data. Oleh karena itu, akan digunakan fungsi drop() untuk menghapus baris yang memiliki nilai kosong pada atribut tersebut.
- Dataframe "Users" memiliki sebanyak 110,762 nilai yang hilang pada fitur usia. Untuk menangani masalah ini, nilai-nilai yang hilang akan diganti dengan angka 0. Pengisian nilai NaN dengan 0 bertujuan untuk memastikan konsistensi dan ketersediaan data dalam analisis atau pemodelan. Dengan mengisi nilai NaN dengan 0, data memiliki struktur yang konsisten, dan setiap sel memiliki nilai numerik yang dapat diproses secara konsisten oleh model atau algoritma. Hal ini juga menghindari kesalahan saat pemrosesan data, serta memastikan bahwa model atau algoritma yang tidak memahami nilai hilang dapat digunakan tanpa kegagalan. Dengan demikian, pengisian nilai NaN dengan 0 membantu memastikan bahwa data siap digunakan dalam berbagai analisis dan pemodelan, tanpa adanya kekosongan data yang dapat mengganggu proses.

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


2. Algoritma Singular Value Decomposition (SVD) untuk membangun model sistem rekomendasi

Algoritma Singular Value Decomposition (SVD) digunakan untuk membangun model sistem rekomendasi. Proses ini melibatkan beberapa langkah, seperti definisi skala peringkat, pembagian dataset menjadi set pelatihan dan pengujian, serta pelatihan model menggunakan data pelatihan.

Setelah dataset dimuat ke dalam format yang sesuai dengan library Surprise, skala peringkat dari 0 hingga 10 didefinisikan menggunakan objek Reader. Dataset kemudian dibagi menjadi set pelatihan dan pengujian dengan proporsi pengujian sebesar 20% dari total data. Ini bertujuan untuk menguji kinerja model pada data yang tidak digunakan selama pelatihan.

Model SVD kemudian didefinisikan dan dilatih pada set pelatihan menggunakan metode fit(). Model ini menggunakan teknik SVD untuk melakukan faktorisasi matriks pada data peringkat, yang kemudian digunakan untuk membuat prediksi peringkat buku untuk pengguna yang belum pernah dilihat sebelumnya.

Setelah model dilatih, prediksi peringkat dibuat pada set pengujian menggunakan metode test(). Prediksi ini kemudian dievaluasi menggunakan metode accuracy.rmse() untuk menghitung nilai Root Mean Square Error (RMSE) antara prediksi dan nilai sebenarnya pada set pengujian. Semakin kecil nilai RMSE, semakin baik kinerja modelnya dalam memprediksi peringkat buku.

3. Mendapatkan Rekomendasi

Berdasarkan langkah-langkah pada Cosine Similarity akan dilakukan pencarian menggunakan fungsi recomend() pada buku "A Walk to Remember" maka hasilnya seperti berikut:

<div><img src="https://github.com/rifkyms037/ProyekAkhir_Sistem-Rekomendasi/assets/114732976/09fcdadc-3230-4b42-9586-4d8f77828e88" width="500"/></div>
Gambar 1. Mendapatkan rekomendasi

Berdasarkan Gambar 1. hasil rekomendasi buku untuk buku dengan judul "A Walk to Remember". Rekomendasi ini didasarkan pada kesamaan dengan buku yang diberikan menggunakan metode cosine similarity. Berikut adalah penjelasan untuk setiap buku yang direkomendasikan:

1. The Rescue oleh Nicholas Sparks: Buku ini ditulis oleh penulis yang sama dengan buku yang diberikan, yaitu Nicholas Sparks. Hal ini menunjukkan adanya kesamaan dalam gaya penulisan atau tema antara kedua buku tersebut.
2. Nights in Rodanthe oleh Nicholas Sparks: Ini adalah buku yang ditulis oleh Nicholas Sparks, menunjukkan adanya kesamaan dengan buku yang diberikan.
3. The Notebook oleh Nicholas Sparks: Buku ini juga ditulis oleh Nicholas Sparks, yang menunjukkan bahwa penulis ini memiliki beberapa buku yang mirip atau relevan dengan buku yang diberikan.
4. Granny Dan oleh DANIELLE STEEL: Meskipun buku ini ditulis oleh penulis yang berbeda, yaitu DANIELLE STEEL, buku ini direkomendasikan karena memiliki kesamaan dengan buku yang diberikan, mungkin dalam hal genre atau tema tertentu.
5. A Bend in the Road oleh Nicholas Sparks: Sekali lagi, buku ini ditulis oleh Nicholas Sparks, menunjukkan adanya kesamaan dengan buku yang diberikan.


## Evaluation
1. Mendapatkan nilai evaluasi RMSE

Setelah dilakukan proses permodelan menggunakan algoritma SVD, maka akan dilakukan evaluasi model menggunakan RMSE. Berikut merupakan hasil dari evaluasi RMSE menggunakan algoritma SVD

<div><img src="https://raw.githubusercontent.com/rifkyms037/ProyekAkhir_Sistem-Rekomendasi/main/assets/RMSE.png" width="500"/></div>
Gambar 2. Evaluasi RMSE

Berdasarkan Gambar 2. hasil evaluasi performa model menggunakan Root Mean Square Error (RMSE) sebesar 3.5195 menunjukkan tingkat kesalahan rata-rata dari prediksi model terhadap nilai sebenarnya adalah sekitar 3.52. Semakin rendah nilai RMSE, semakin baik kualitas prediksi model, karena nilai RMSE yang lebih rendah menunjukkan bahwa model memiliki kesalahan prediksi yang lebih kecil.

3. Mendapatkan rekomendasi Buku
Setelah melatih model dengan menggunakan data latih, kemudian mengevaluasi kinerja model dengan menghitung Root Mean Square Error (RMSE) pada data uji. Hasil evaluasi menunjukkan bahwa RMSE yang diperoleh adalah 3.5195, menunjukkan tingkat kesalahan yang relatif tinggi dalam prediksi model. Namun demikian, dilanjutkan dengan membuat rekomendasi buku untuk pengguna tertentu menggunakan model yang telah dilatih.

<div><img src="https://raw.githubusercontent.com/rifkyms037/ProyekAkhir_Sistem-Rekomendasi/main/assets/rekomenadsi%20buku.png" width="500"/></div>
Gambar 3. Daftar 10 buku teratas untuk pengguna dengan ID 271705

Hasil rekomendasi tersebut kemudian disajikan dalam Gambar 3. berupa daftar 10 buku teratas untuk pengguna dengan ID 271705. Langkah-langkah ini untuk meningkatkan pengalaman pengguna dalam menemukan buku yang sesuai dengan minat mereka.


