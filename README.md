# Laporan Proyek _Machine Learning_ - Stevanus Sembiring

## _CONTENT-BASED RECOMMENDATION_ PADA _SPOTIFY MUSIC DATASET_

Spotify adalah salah satu platform streaming musik dan podcast terbesar di dunia yang telah merevolusi cara kita mendengarkan musik dan konten audio lainnya. Dalam beberapa tahun terakhir, Spotify tidak hanya menjadi sarana hiburan, tetapi juga telah berkembang menjadi alat yang berguna dalam berbagai bidang, termasuk pendidikan dan pengembangan keterampilan.

Content-based recommendation adalah salah satu metode yang digunakan dalam sistem rekomendasi musik untuk menyarankan lagu-lagu kepada pengguna berdasarkan karakteristik konten dari lagu-lagu tersebut. Dalam konteks Spotify, metode ini memanfaatkan berbagai fitur audio dan metadata yang tersedia dalam dataset Spotify untuk memberikan rekomendasi yang sesuai dengan preferensi musik pengguna.

Pendekatan content-based recommendation pada Spotify melibatkan penggunaan fitur-fitur audio seperti energi, valensi, danceability, tempo, dan lainnya untuk menyarankan lagu-lagu yang mirip dengan lagu-lagu yang disukai pengguna[1]. Metode ini mengandalkan analisis data yang mendalam dan teknik pembelajaran mesin untuk mengidentifikasi pola dan hubungan dalam data yang dapat digunakan untuk memberikan rekomendasi yang dipersonalisasi[2].  

Salah satu teknik yang umum digunakan dalam content-based recommendation adalah cosine similarity, yang mengukur kesamaan antara vektor-vektor fitur audio dari lagu-lagu dalam dataset. Cosine similarity mengukur kesamaan antara dua vektor dengan menghitung kosinus dari sudut di antara mereka. Semakin dekat nilai cosine similarity ke 1, semakin mirip kedua item tersebut[3]. Teknik ini sering digunakan dalam sistem rekomendasi musik untuk mengidentifikasi lagu-lagu yang memiliki karakteristik audio yang serupa[4].

Selain cosine similarity, Euclidean distance juga digunakan untuk mengukur kesamaan antara lagu-lagu. Euclidean distance adalah jarak garis lurus antara dua titik dalam ruang Euclidean. Teknik ini berguna untuk situasi di mana magnitudo data penting dalam menentukan kesamaan[5]. Dalam beberapa proyek, kedua teknik ini digunakan secara bersamaan untuk meningkatkan akurasi rekomendasi[6].

## Business Understanding
### Problem Statements
- Bagaimana gambaran data yang digunakan dalam membuat _system recommendation_?
- Bagaimana perbandingan metode _content-based recommendation_ terhadap hasil rekomendasi?

### Goals
- Mengetahui gambaran data yang digunakan dalam membuat _system recommendation_.
- Mengetahui perbandingan metode dari _content-based recommendation_ terhadap hasil rekomendasi.

### Solution Statements

- Melakukan _Exploratory Data Analysis_ untuk mengetahui gambaran data yang digunakan dalam membuat _system recommendation_
- Menggunakan metode _cosine similarity_ dan _euclidean distance_ untuk penerapan _content-based recommendation_ pada _spotify music dataset_ 

## Data Understanding

Dataset yang digunakan dalam proyek ini adalah dataset spotify yang dikoleksi lengkap dari berbagai genre yang tersedia di [Kaggle Datasets](https://www.kaggle.com/datasets/ambaliyagati/spotify-dataset-for-playing-around-with-sql/data). Dataset ini memiliki 6300 baris dan 8 kolom dan tidak terdapat data yang kosong (_missing value_). Sehingga secara keseluruhan dataset ini sudah bersih dan tidak perlu melakukan penanganan _missing value_.  

### Variabel-variabel pada dataset adalah sebagai berikut:
- id: Pengidentifikasi unik untuk lagu di Spotify.
- name: Nama lagu.
- genre: Genre dari lagu.
- artists: Nama-nama artis yang membawakan lagu, dipisahkan dengan koma jika terdapat lebih dari satu artis.
- album: Nama album tempat lagu tersebut berada.
- popularity: Skor popularitas lagu (0-100, dimana nilai yang lebih tinggi menunjukkan lagu yang lebih populer).
- duration_ms: Durasi lagu dalam milidetik.
- explicit: Boolean yang menunjukkan apakah lagu tersebut mengandung konten eksplisit.

### Statistika Deskriptif
| Statistic | Popularity     | Duration (ms)    |
|-----------|----------------|------------------|
| count     | 6300.000000    | 6.300000e+03     |
| mean      | 30.754762      | 2.028477e+05     |
| std       | 19.948991      | 1.210299e+05     |
| min       | 0.000000       | 3.006000e+04     |
| 25%       | 16.000000      | 1.476870e+05     |
| 50%       | 29.000000      | 1.916070e+05     |
| 75%       | 45.000000      | 2.369625e+05     |
| max       | 90.000000      | 3.601658e+06     |


Interpretasi
- Popularity: Lagu-lagu dalam dataset ini memiliki nilai popularity yang bervariasi dari 0 hingga 90, dengan rata-rata sekitar 30.75. Sebagian besar lagu memiliki nilai popularity di bawah 45, yang ditunjukkan oleh kuartil ketiga.
- Duration_ms: Durasi lagu berkisar dari sekitar 30 detik hingga lebih dari satu jam, tetapi sebagian besar durasi berada di sekitar 2 hingga 4 menit, dengan rata-rata sekitar 3 menit 22.8 detik.
