# Laporan Proyek Machine Learning
**Evlin Sitanggang**

## Domain Proyek

Nama *Project* : **Movie Recommendation - CF and CBF**

## Project Overview

Sistem rekomendasi film adalah teknologi yang membantu pengguna menemukan film berdasarkan preferensi mereka. Contohnya dapat dilihat pada platform seperti Netflix, Prime Video, ViU dan WeTV, yang menggunakan data perilaku pengguna, seperti riwayat tontonan dan rating film, untuk memberikan saran yang relevan. Sistem ini memanfaatkan teknik collaborative filltering, yang menangkap kesamaan antara pengguna atau film berdasarkan pola historis. Namun, tantangan seperti kelangkaan data dan pertumbuhan jumlah film dan pengguna memerlukan strategi khusus untuk menjaga akurasi dan relevansi rekomendasi.

referensi dari proyek overview yang saya buat dapat dilihat dari tautan berikut :
[Jurnal: Techno.Com](https://publikasi.dinus.ac.id/index.php/technoc/article/view/8556)

## Business Understanding

### Problem Statements

Bagaimana cara merekomendasikan film yang populer di kalangan pengguna tertentu kepada pengguna lainnya?

### Goals

Mampu membangun sistem rekomendasi yang tepat dengan mengandalkan rating dan riwayat aktivitas pengguna sebelumnya.

### Solution approach

Solusi yang saya kembangkan melibatkan penggunaan dua algoritma Machine Learning untuk sistem rekomendasi, yaitu:

- **Content-Based Filtering**: Algoritma ini merekomendasikan item yang serupa dengan preferensi pengguna, berdasarkan interaksi mereka sebelumnya atau umpan balik yang diberikan.
- **Collaborative Filtering**: Algoritma ini memanfaatkan pendapat atau preferensi pengguna lain dalam komunitas. Algoritma ini tidak memerlukan atribut spesifik dari setiap item.

Algoritma Content-Based Filtering digunakan untuk merekomendasikan film berdasarkan riwayat aktivitas pengguna, sementara Collaborative Filtering digunakan untuk memberikan rekomendasi film berdasarkan rating tertinggi dari pengguna lain.

## Data Understanding

Data atau dataset yang digunakan pada proyek machine learning ini adalah data **Movie Recommendation Data** yang didapat dari situs kaggle. Link dataset dapat dilihat dari tautan berikut [movie-recommendation-data](https://www.kaggle.com/rohan4050/movie-recommendation-data)

File dataset terdiri dari:

- ratings.csv: Penilaian pengguna terhadap film.
- movies.csv: Daftar judul dan genre film.
- links.csv: Link referensi film.
- tags.csv: Kata kunci yang relevan dengan film.
  
Variabel-variabel pada movie-recommendation-data adalah sebagai berikut :

- links : merupakan daftar link movie tersebut.
- movies : merupakan daftar movie yang tersedia.
- ratings : merupakan daftar penilaian yang diberikan pengguna terhadap movie.
- tags : merupakan daftar kata kunci dari movie tersebut.

tahapan yang dilakukan mengenai data adalah dengan melakukan exploratory data analysis, yaitu dengan melihat-lihat hubungan antar variabel bersarkan id. Serta menggabungkan seluruh variabel movie_all berdasarkan movieId dan variabel user_all berdasarkan userId

## Data Preparation

Data preparation yang digunakan oleh saya yaitu :

- Menangani data kosong: Mengecek apakah ada data yang hilang dan menghapus baris yang memiliki nilai kosong.
- Pembagian data: Memisahkan data menjadi dua set, yaitu data untuk pelatihan dan untuk validasi.
- Menggabungkan kolom: Mengintegrasikan beberapa kolom dengan ID unik agar data lebih terstruktur.
- Menyusun data: Mengurutkan data berdasarkan ID film (movieId) secara menaik.
- Mengatasi duplikasi: Mengidentifikasi dan menghapus data yang memiliki nilai atau informasi yang sama.
- Mengonversi data ke dalam list: Mengubah struktur data menjadi dalam bentuk list.
- Membuat kamus data: Mengorganisasi data ke dalam format dictionary.
- Menggunakan TfidfVectorizer: Mengaplikasikan teknik pembobotan untuk memperhitungkan pentingnya kata-kata dalam data.
- Melakukan pembersihan data: Menyelesaikan masalah yang bisa mengganggu hasil analisis atau pelatihan model.
- Pemetaan data: Menyesuaikan dan menghubungkan data dengan format yang diperlukan untuk analisis.

## Modeling and Result

- Proses pemodelan yang saya terapkan pada data ini melibatkan dua algoritma machine learning, yaitu content-based filtering dan collaborative filtering. Pada content-based filtering, saya fokus pada preferensi pengguna berdasarkan interaksi mereka sebelumnya dengan film yang telah mereka tonton. Sedangkan pada collaborative filtering, saya menggunakan data rating dari pengguna untuk merekomendasikan film yang paling disukai.

- Berikut adalah hasil dari kedua algoritma tersebut :

1. hasil dari **content based filtering**  
   berikut adalah movie yang disukai pengguna dimasa lalu :  
   |id	      |movie_name	           |genre|
   |-----------|----------------------|-----|
   |1284	30820	|Woodsman, The (2004)  |Drama|

   dari hasil di atas dapat dilihat bahwa pengguna menyukai movie yang berjudul Woodsman, The (2004) yang bergenre Drama.
   maka hasil top 5 rekomendasi berdasarkan algoritma conten based filtering adalah sebagai berikut :  
   |    |movie_name	                                       |genre|
   |----|---------------------------------------------------|-----|
   |0	  |Friendly Persuasion (1956)	                        |Drama|
   |1	  |Gospel According to St. Matthew, The (Vangelo ...	|Drama|
   |2	  |Lost Horizon (1937)	                              |Drama|
   |3   |Ikiru (1952)	                                    |Drama|
   |4   |Luther (2003)	                                    |Drama|
   
   dari hasil di atas dapat dilihat bahwa movie yang bergenre antar Adventuyre, Children, dan Fantasy menjadi yang direkomendasikan oleh sistem. Hal ini didasarkan pada kesukaan penonton atau pengguna pada masa lalu.

3. hasil dari **collaborative content filtering**  
   berikut adalah movie berdasarkan rating yang adalah:
   
   Showing movie recommendations for users: 525
   
   Movie with highest ratings from user
   - Ferris Bueller's Day Off (1986) : Comedy
   - Dogma (1999) : Adventure|Comedy|Fantasy
   - Virgin Suicides, The (1999) : Drama|Romance
   
   Top 10 movie recommendation
   |Movie Name          | Genre|
   |--------------------|------|
   |Pulp Fiction (1994) | Comedy,Crime,Drama,Thriller|
   | One Flew Over the Cuckoo's Nest (1975) | Drama|
   | Good, the Bad and the Ugly, The (Buono, il brutto, il cattivo, Il) (1966) | Action,Adventure,Western|
   | Lawrence of Arabia (1962) | Adventure,Drama,War|
   | Apocalypse Now (1979) | Action,Drama,War|
   | Goodfellas (1990) | Crime,Drama|
   | Ran (1985) | Drama,War|
   | Godfather: Part II, The (1974) | Crime,Drama|
   | Amadeus (1984) | Drama|
   | Cool Hand Luke (1967) | Drama|
   
   dari hasi di atas movie yang bergenre comedy menjadi movie yang paling tinggi ratingnya yang direkomendasikan untuk user 525. Kemudian top 10 movie yang direkomendasikan sistem adalah movie dengan genre comedy dan drama.

## Evaluation

1. hasil Evaluasi untuk Content Based Filtering

Dari hasil rekomendasi di atas, diketahui bahwa Woodsman, The (2004) termasuk ke dalam genre Drama Dari 5 item yang direkomendasikan semuanya memiliki genre Drama (similar). Artinya, precision sistem kita sebesar 5/5 atau 100%.

Teknik Evaluasi di atas adalah dengan menggunakan precission, rumus dari teknik ini adalah :
![662c4327f27ee08d3e4d4b34_65777ee1fd55288155f28d37_precision_recall_k2](https://github.com/user-attachments/assets/2855fac9-acab-4ba5-9e96-4403431f0f5c)

2. hasil Evaluasi untuk Collaborative Filtering

Metrik yang digunakan untuk mengevaluasi kinerja model dalam kasus ini adalah RMSE (Root Mean Squared Error).

RMSE digunakan untuk mengukur sejauh mana hasil prediksi model mendekati nilai yang sebenarnya. Ini dihitung dengan mengambil akar kuadrat dari rata-rata kuadrat selisih antara nilai yang diprediksi dan nilai yang teramati. Model dengan nilai RMSE yang lebih kecil dianggap memiliki akurasi yang lebih tinggi, karena kesalahan prediksinya lebih kecil.

Berikut adalah beberapa kelebihan dan kekurangan dari metrik ini:

- Kelebihan: RMSE memberikan penalti yang lebih besar pada kesalahan besar, sehingga dapat lebih akurat dalam kasus di mana kesalahan besar sangat merugikan.
- Kekurangan: RMSE cenderung memberikan bobot yang lebih besar pada kesalahan besar, yang dapat menyebabkan hasil yang terlalu sensitif terhadap nilai ekstrem, terutama dalam dataset yang mengandung nilai yang sangat jauh dari prediksi.

Formula RMSE:

![RMSE1](https://github.com/user-attachments/assets/9ce93817-6087-488b-ab93-7d2866900378)

cara menerapkan metrik tersebut adalah dengan menambahkan **_'metrics=[tf.keras.metrics.RootMeanSquaredError()]'_** pada model.compile.

hasil dari model evaluasi visualisasi matriks adalah sebagai berikut :  
![download (13)](https://github.com/user-attachments/assets/f484b79c-53c8-4cc9-a62d-5bf84952fd5b)

dari visualisasi proses training model di atas model berhenti di epochs sekitar 20. Dari proses ini, kita memperoleh nilai error akhir sebesar sekitar 0.195 dan error pada data validasi sebesar 0.207. 

## Kesimpulan

Dalam proyek ini, saya berhasil membangun sistem rekomendasi film menggunakan dua algoritma machine learning: Content-Based Filtering (CBF) dan Collaborative Filtering (CF). Kedua metode ini digunakan untuk memberikan rekomendasi film yang relevan berdasarkan riwayat aktivitas pengguna dan rating yang diberikan oleh pengguna lain.

- Content-Based Filtering (CBF): Algoritma ini memberikan rekomendasi berdasarkan film yang disukai oleh pengguna di masa lalu. Berdasarkan hasil pengujian, sistem ini berhasil memberikan rekomendasi film dengan genre yang sangat mirip dengan genre film yang sebelumnya disukai oleh pengguna, menunjukkan akurasi yang tinggi dengan precision mencapai 100%.

- Collaborative Filtering (CF): Algoritma ini menggunakan rating dari pengguna lain untuk memberikan rekomendasi. Dengan menggunakan RMSE untuk evaluasi, model ini menunjukkan bahwa hasil prediksi memiliki tingkat error yang rendah, yaitu sekitar 0.195 pada data pelatihan dan 0.207 pada data validasi. Hal ini menunjukkan bahwa model memiliki akurasi yang cukup baik dalam memprediksi film yang mungkin disukai oleh pengguna berdasarkan preferensi orang lain.

  
**---Ini adalah bagian akhir laporan---**
