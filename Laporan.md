# Laporan Proyek Machine Learning
**Evlin Sitanggang**

## Domain Proyek

Nama *Project* : **Movie Recommendation - CF and CBF**

## Project Overview

Sistem rekomendasi film adalah teknologi yang dirancang untuk membantu pengguna menemukan film yang sesuai dengan preferensi mereka [[1]](https://publikasi.dinus.ac.id/index.php/technoc/article/view/8556). Contohnya dapat ditemukan pada platform seperti Netflix, Prime Video, ViU, dan WeTV, yang memanfaatkan data perilaku pengguna seperti riwayat tontonan dan penilaian (rating) film untuk memberikan saran yang relevan. Sistem ini menggunakan berbagai teknik, salah satunya adalah **Collaborative Filtering**, yang mengidentifikasi pola kesamaan antara pengguna atau film berdasarkan data historis.

Namun, dalam pengembangan sistem ini, terdapat beberapa masalah yang harus diatasi:  
1. **Kelangkaan Data**: Banyak pengguna memberikan sedikit atau bahkan tidak ada penilaian terhadap film, sehingga sistem kekurangan informasi untuk memberikan rekomendasi yang relevan.  
2. **Lonjakan Data**: Dengan meningkatnya jumlah pengguna dan film, sistem harus mampu menangani volume data yang besar sambil tetap mempertahankan akurasi rekomendasi.  
3. **Bias Data**: Sistem sering kali cenderung merekomendasikan film populer, sehingga genre atau film yang kurang dikenal menjadi kurang terekspos.  

Latar belakang pemilihan masalah ini didasari oleh kebutuhan industri hiburan untuk meningkatkan keterlibatan pengguna melalui personalisasi konten. Dengan menyediakan rekomendasi yang tepat, platform dapat mempertahankan pelanggan lebih lama dan meningkatkan kepuasan pengguna. Oleh karena itu, pengembangan sistem rekomendasi yang efektif sangat penting untuk mengatasi tantangan ini sekaligus mendukung pengalaman pengguna yang lebih baik.

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

Sebelum melakukan *modeling* dan *evaluation* dengan algoritma *Machine Learning* pada Notebook "Google Colaboratory", mari melihat sekilas pada *dataset* yang digunakan. Di bawah ini akan ditampilkan cuplikan dari dataset.

Tabel 1 : Berikut adalah tampilan data links yang terdiri dari 9742 baris data dan 3 kolom, dengan semua data tidak ada yang missing atau hilang serta duplikasi:

|	|movieId	|imdbId	|tmdbId|
|-|---------|-------|------|
|0	|1	|114709	|862.0|
|1	|2	|113497	|8844.0|
|2	|3	|113228	|15602.0|
|3	|4	|114885	|31357.0|
|4	|5	|113041	|11862.0|
|...	|...	|...	|...|
|9737	|193581	|5476944	|432131.0|
|9738	|193583	|5914996	|445030.0|
|9739	|193585	|6397426	|479308.0|
|9740	|193587	|8391976	|483455.0|
|9741	|193609	|101726	|37891.0|

Berikut adalah informasi setiap variabel dalam Tabel 1:

- `movieId`: ID unik yang mengidentifikasi sebuah film dalam dataset.
- `imdbId`: ID unik dari film yang terdaftar di IMDb (Internet Movie Database).
- `tmdbId`: ID unik dari film yang terdaftar di TMDb (The Movie Database).

Tabel 2 : Berikut adalah tampilan data movies (daftar film) yang terdiri dari 9742 baris data dan 3 kolom, terdiri dari id, judul dan genre movie nya , dengan semua data tidak ada yang missing atau hilang serta duplikasi:

|	  |movieId	|title	|genres|
|---|---------|-------|------|
|0	|1	|Toy Story (1995)	|Adventure, Animation, Children, Comedy, Fantasy|
|1	|2	|Jumanji (1995)	|Adventure, Children, Fantasy|
|2	|3	|Grumpier Old Men (1995)	|Comedy, Romance|
|3	|4	|Waiting to Exhale (1995)	|Comedy, Drama, Romance|
|4	|5	|Father of the Bride Part II (1995)	|Comedy|
|...	|...	|...	|...|
|9737	|193581	|Black Butler: Book of the Atlantic (2017)	|Action, Animation, Comedy, Fantasy|
|9738	|193583	|No Game No Life: Zero (2017)	|Animation, Comedy, Fantasy|
|9739	|193585	|Flint (2017)	|Drama|
|9740	|193587	|Bungo Stray Dogs: Dead Apple (2018)	|Action, Animation|
|9741	|193609	|Andrew Dice Clay: Dice Rules (1991)	|Comedy|

Berikut adalah informasi setiap variabel dalam Tabel 2:

- `movieId`: ID unik yang mengidentifikasi sebuah film dalam dataset.
- `title`: Judul film, termasuk tahun rilis dalam tanda kurung.
- `genres`: Kategori genre yang menggambarkan jenis film (misalnya, Action, Drama, Comedy, dll.).

Tabel 3 : Berikut adalah tampilan data ratings yang terdiri dari 100836 baris data dan 4 kolom, data yang berasal dari hasil rating yang diberikan penonton untuk sebuah movie. Data ini berisikan id user yang memberi rating, movie id yang diberikan rating, nilai ratingnya dan waktu saat user memberikan rating, dengan semua data tidak ada yang missing atau hilang dan outlier serta duplikasi:

|	|userId	|movieId	|rating	|timestamp|
|-|-------|---------|-------|---------|
|0	|1	|1	|4.0	|964982703|
|1	|1	|3	|4.0	|964981247|
|2	|1	|6	|4.0	|964982224|
|3	|1	|47	|5.0	|964983815|
|4	|1	|50	|5.0	|964982931|
|...	|...	|...	|...	|...|
|100831	|610	|166534	|4.0	|1493848402|
|100832	|610	|168248	|5.0	|1493850091|
|100833	|610	|168250	|5.0	|1494273047|
|100834	|610	|168252	|5.0	|1493846352|
|100835	|610	|170875	|3.0	|1493846415|

Berikut adalah informasi setiap variabel dalam Tabel 3:

- `userId`: ID unik pengguna (penonton) yang memberikan rating.
- `movieId`: ID film yang diberi rating.
- `rating`: Nilai rating yang diberikan oleh pengguna (antara 0.5 hingga 5.0).
- `timestamp`: Waktu ketika pengguna memberikan rating, dalam format waktu UNIX (jumlah detik sejak 1970-01-01).

Dari tabel di atas, diketahui bahwa nilai maksimum ratings adalah 5.0 atau 5 dan nilai minimumnya adalah 0.5. Artinya, skala rating berkisar antara 0.5 hingga 5. 

Tabel 4 : Berikut adalah tampilan data tags (tagar) yang terdiri dari 3683 baris data dan 4 kolom, yang berisi tagar konteks yang relevan dengan movie yang ditonton, movie id nya dan waktu memberikan tag nya, dengan semua data tidak ada yang missing atau hilang serta duplikasi:

|	|userId	|movieId	|tag	|timestamp|
|-|-------|---------|-----|---------|
|0	|2	|60756	|funny	|1445714994|
|1	|2	|60756	|Highly quotable	|1445714996|
|2	|2	|60756	|will ferrell	|1445714992|
|3	|2	|89774	|Boxing story	|1445715207|
|4	|2	|89774	|MMA	|1445715200|
|...	|...	|...	|...	|...|
|3678	|606	|7382	|for katie	|1171234019|
|3679	|606	|7936	|austere	|1173392334|
|3680	|610	|3265	|gun fu	|1493843984|
|3681	|610	|3265	|heroic bloodshed	|1493843978|
|3682	|610	|168248	|Heroic Bloodshed	|1493844270|

Berikut adalah informasi setiap variabel dalam Tabel 4:

- `userId`: ID unik pengguna yang memberikan tag.
- `movieId`: ID film yang diberi tag.
- `tag`: Kata kunci atau tag yang diberikan untuk mendeskripsikan film, biasanya berupa kata atau frasa yang menggambarkan film tersebut (misalnya, "funny", "action-packed", dll.).
- `timestamp`: Waktu ketika tag diberikan, dalam format waktu UNIX.

## Data Preparation

Proses data preparation adalah langkah penting dalam mempersiapkan data agar dapat digunakan secara efektif dalam pengembangan model machine learning. Berikut adalah tahapan yang dilakukan dalam proyek ini:

1. Menggabungkan Movie
   
    Menggabungkan berbagai file (seperti links, movies, ratings, dan tags) menggunakan fungsi np.concatenate().
Proses ini bertujuan untuk menggabungkan data berdasarkan kolom movieId, sehingga seluruh data terkait film dapat diintegrasikan dalam satu tempat.
Data yang dihasilkan diurutkan menggunakan np.sort() dan nilai duplikat dihapus dengan np.unique().

    Output : Jumlah keseluruhan movieId yang unik.

2. Menggabungkan Seluruh User
   
    Menggabungkan data userId dari file ratings dan tags menggunakan np.concatenate().
Data diurutkan dan nilai duplikat dihapus.
Proses ini memastikan bahwa semua informasi pengguna diintegrasikan tanpa ada pengulangan.

    Output : Jumlah keseluruhan userId yang unik.

3. Membuat Dataframe movie_info

    Data dari links, movies, ratings, dan tags digabungkan menjadi satu dataframe menggunakan pd.concat().
Selanjutnya, dataframe movie_info digabungkan dengan ratings berdasarkan movieId menggunakan pd.merge().
Tujuan: Untuk menyatukan seluruh informasi film dengan data rating pengguna.
Setelah penggabungan, dilakukan pengecekan missing values dengan movie.isnull().sum() untuk mengetahui data yang perlu dibersihkan atau diimputasi.

4. Mengelompokkan Rating Berdasarkan movieId

    Data rating dikelompokkan menggunakan movie.groupby('movieId').sum().
Langkah ini memungkinkan kita untuk menganalisis total skor atau jumlah interaksi pada setiap film.

5. Menggabungkan Data dengan Fitur Nama Movie

    Data rating disimpan dalam variabel all_movie_rate.
Kemudian, dataframe movies digabungkan dengan all_movie_rate berdasarkan movieId menggunakan pd.merge(). Proses ini menambahkan informasi title dan genres dari setiap film.
Selanjutnya, dataframe tags digabungkan dengan hasil penggabungan sebelumnya berdasarkan movieId untuk menambahkan kata kunci (tags) yang relevan.
Hasil akhir disimpan dalam variabel all_movie.

6. Mengatasi Missing Value

    Mengecek missing value pada dataset all_movie dengan all_movie.isnull().sum().
Kolom tag ditemukan memiliki 52.549 data kosong. Data ini dibersihkan menggunakan fungsi dropna(), yang menghapus seluruh baris dengan nilai kosong.

    |       |0|
    |-------|-|
    |userId	|0|
    |movieId	|0|
    |rating	|0|  
    |timestamp	|0|
    |title	|0|
    |genres	|0|
    |tag	|52549|

    Output: Dataset baru, all_movie_clean, dengan jumlah baris berkurang dari 285.762 menjadi 233.213.
Memastikan kembali tidak ada missing value pada dataset dengan all_movie_clean.isnull().sum().

7. Mengurutkan Data Berdasarkan movieId

    Dataset all_movie_clean diurutkan berdasarkan kolom movieId menggunakan sort_values() dan disimpan dalam variabel fix_movie.
Hal ini bertujuan untuk mempermudah proses pemetaan dan analisis.
Mengecek jumlah movieId unik dengan len(fix_movie.movieId.unique()).

8. Menghapus Data Duplikat
  
    Dataset fix_movie disimpan kembali ke dalam variabel preparation.
Dilakukan penghapusan data duplikat berdasarkan kolom movieId dengan drop_duplicates('movieId').
Langkah ini memastikan setiap film hanya muncul sekali dalam dataset.

9. Konversi Data ke Bentuk List

    Data dari kolom movieId, title, dan genres diubah menjadi list menggunakan fungsi tolist():
    - movie_id: List dari semua movieId.
    - movie_name: List dari semua judul film.
    - movie_genre: List dari semua genre film.

    Output: Tiga variabel berbentuk list dengan jumlah elemen yang sama.

10. Membuat Dictionary Dataframe

    Menggunakan tiga list yang telah dibuat (movie_id, movie_name, movie_genre), dibuat sebuah dataframe movie_new dengan pasangan key-value:
    - id: Berisi movie_id.
    - movie_name: Berisi movie_name.
    - genre: Berisi movie_genre.
      
    Dataframe ini merupakan hasil akhir dari data preparation, yang siap digunakan untuk pemodelan.

## Preparation Collaborative Filtering

Proses data preparation terdiri dari beberapa langkah yang terstruktur dan terperinci, yang dimulai dengan encoding ID pengguna dan film, hingga membagi data untuk pelatihan dan validasi, serta mempersiapkan model rekomendasi berbasis neural network. Berikut adalah tahapannya:

1. User Encoding

Mengambil ID pengguna yang unik dan mengubahnya menjadi format numerik menggunakan dua kamus:
- user_to_user_encoded: Mempetakan userId ke angka numerik.
- user_encoded_to_user: Membalikkan pemetaan tersebut untuk mengonversi angka numerik kembali ke userId.

2. Movie Encoding

Proses serupa dilakukan untuk kolom movieId:
- movie_to_movie_encoded: Mempetakan movieId ke angka numerik.
- movie_encoded_to_movie: Membalikkan pemetaan tersebut.

3. Menambahkan Kolom ke Dataframe

Kolom genres dan movies ditambahkan ke dataframe dengan memetakan userId dan movieId ke ID terencode.

4. Menampilkan Statistik Dasar

- Menghitung jumlah pengguna dan film dalam dataset.
- Mengonversi kolom rating menjadi tipe data float32 dan mencari nilai rating minimum dan maksimum.

5. Pembagian Data untuk Training dan Validasi

- Dilakukan pengacakan (shuffling) pada data untuk memastikan distribusi yang acak pada saat melakukan pemodelan, dengan menggunakan `sample(frac=1, random_state=42)` untuk memastikan distribusi yang acak.
- Membagi data menjadi training dan validation set dengan proporsi 80:20.
- Variabel x berisi fitur genres dan movies, sedangkan variabel y berisi rating yang dinormalisasi.


## Modeling and Result

- Proses pemodelan yang saya terapkan pada data ini melibatkan dua algoritma machine learning, yaitu content-based filtering dan collaborative filtering. Pada content-based filtering, saya fokus pada preferensi pengguna berdasarkan interaksi mereka sebelumnya dengan film yang telah mereka tonton. Sedangkan pada collaborative filtering, saya menggunakan data rating dari pengguna untuk merekomendasikan film yang paling disukai. Berikut adalah hasil dari kedua algoritma tersebut :
 ### 1. Content-Based Filtering

**Cara Kerja**:

Prinsip Dasar: Rekomendasi diberikan berdasarkan karakteristik item (film) yang disukai pengguna di masa lalu. Menerapkan konsep TF-IDF (Term Frequency-Inverse Document Frequency) adalah sebuah metode yang digunakan untuk mengukur seberapa penting suatu kata dalam sebuah dokumen, dengan cara ini, kata-kata yang relevan dan spesifik dalam konteks dokumen akan lebih dihargai daripada kata yang terlalu umum. Lalu Cosine Similarity yang digunakan untuk mengukur seberapa mirip dua item (misalnya dua film atau dua pengguna) berdasarkan fitur atau interaksi pengguna dengan item tersebut. Seperti mengukur seberapa mirip film berdasarkan genre atau deskripsi film.

Langkah:
1. Representasi Data: Setiap item direpresentasikan menggunakan fitur-fitur tertentu, misalnya genre film.
2. Vectorization: Fitur item diubah menjadi representasi vektor numerik menggunakan metode seperti TF-IDF Vectorizer.
3. Kesamaan Item: Menghitung kesamaan antar item menggunakan metrik seperti Cosine Similarity.
4. Rekomendasi: Film yang mirip dengan film yang sudah diberi rating tinggi oleh pengguna direkomendasikan.

**Kelebihan**:
- Tidak memerlukan data dari pengguna lain (independen per pengguna).
- Rekomendasi relevan dengan preferensi spesifik pengguna.
- Mudah diimplementasikan untuk dataset dengan deskripsi item yang kaya.

**Kekurangan**:
- Cold Start Problem untuk Item Baru: Tidak dapat merekomendasikan item yang tidak memiliki informasi fitur (deskripsi).
- Overspecialization: Rekomendasi hanya berpusat pada item serupa, sehingga sulit memberikan variasi.
- Tidak memanfaatkan data dari pengguna lain untuk meningkatkan rekomendasi.

**Parameter yang Digunakan**:

1.TF-IDF Vectorizer:
- max_features: Jumlah maksimal kata unik yang digunakan untuk representasi.
- ngram_range: Panjang n-gram untuk analisis (misalnya unigram, bigram).
- min_df & max_df: Frekuensi minimum dan maksimum kata yang akan dipertimbangkan.
  
2.Cosine Similarity: Tidak memiliki parameter langsung, tetapi dihitung berdasarkan vektor item.

### 2. Collaborative Filtering

**Cara Kerja**:

Prinsip Dasar: Rekomendasi diberikan berdasarkan perilaku atau pola interaksi antar pengguna dan item. Konsep model yang digunakan adalah RecommenderNet yang merupakan sebuah model neural network yang digunakan untuk implementasi collaborative filtering dalam sistem rekomendasi. Model ini memanfaatkan konsep embedding untuk pengguna dan item (movie) untuk mempelajari representasi numerik yang menggambarkan preferensi pengguna terhadap item tersebut.

Pendekatan:

1. User-Based Collaborative Filtering:
- Mencari pengguna dengan pola preferensi serupa (misalnya riwayat rating film).
- Rekomendasi diberikan berdasarkan apa yang disukai oleh pengguna serupa.

2. Item-Based Collaborative Filtering:
- Mencari item yang sering dinilai sama oleh pengguna.
- Rekomendasi diberikan berdasarkan hubungan antara item tersebut.

3. Model-Based Collaborative Filtering (RecommenderNet):

Struktur dan Proses RecommenderNet:

1. Embedding Layer:
- User Embedding: Setiap pengguna diwakili oleh vektor embedding yang berisi sejumlah nilai (ditentukan oleh embedding_size). Embedding ini memungkinkan model untuk mempelajari representasi unik dari setiap pengguna berdasarkan interaksi mereka dengan item (film).
- Movie Embedding: Setiap film juga diwakili oleh vektor embedding yang mirip dengan embedding pengguna. Model mempelajari representasi film yang berbeda berdasarkan interaksi yang diterima oleh film tersebut dari berbagai pengguna.
- User Bias dan Movie Bias: Selain embedding, model ini juga mempelajari bias untuk masing-masing pengguna dan film, yang mencerminkan preferensi umum pengguna dan atribut film.

2. Dot Product:
- Untuk memprediksi rating atau preferensi pengguna terhadap sebuah film, dot product antara vektor embedding pengguna dan vektor embedding film dihitung. Proses ini menghasilkan angka yang merepresentasikan tingkat interaksi atau kesukaan pengguna terhadap film tersebut.

3. Penambahan Bias:
- Setelah perhitungan dot product, nilai bias untuk pengguna dan film ditambahkan. Bias ini membantu model menyesuaikan prediksi dengan preferensi umum yang lebih tinggi atau lebih rendah, misalnya, pengguna yang selalu memberikan rating tinggi atau film dengan rating tinggi secara umum.

4. Aktivasi Sigmoid:

- Hasil dari semua operasi ini, yang terdiri dari dot product dan penambahan bias, kemudian diproses menggunakan fungsi sigmoid untuk mendapatkan output yang terletak antara 0 dan 1. Fungsi sigmoid ini digunakan untuk memodelkan kemungkinan bahwa pengguna akan menyukai film tersebut atau tidak.

5. Proses Training:
- Model dilatih menggunakan data interaksi pengguna (misalnya, rating atau preferensi) terhadap film. Selama pelatihan, model mengoptimalkan parameter (embedding, bias) menggunakan algoritma optimasi seperti Adam untuk meminimalkan fungsi kerugian (loss function), yang biasanya menggunakan binary cross-entropy atau mean squared error.
- Fungsi binary cross-entropy sering digunakan jika rating dikategorikan menjadi dua kelas (misalnya, suka atau tidak suka), sedangkan root mean squared error (RMSE) digunakan untuk prediksi rating yang lebih kontinu.

**Kelebihan**:

- Mampu merekomendasikan item yang tidak memiliki informasi deskriptif (fitur minimal).
- Menghasilkan rekomendasi dengan variasi yang lebih luas (menemukan hidden preferences).
- Memanfaatkan pola interaksi seluruh pengguna, sehingga lebih fleksibel.

**Kekurangan**:

- Cold Start Problem untuk Pengguna Baru: Tidak dapat merekomendasikan jika pengguna belum memiliki riwayat interaksi.
- Scalability Issue: Sulit diterapkan untuk dataset besar tanpa optimasi yang baik.
- Sparsity Problem: Jika data interaksi sangat jarang, model sulit memberikan rekomendasi yang akurat.


**Hasil dari **content based filtering****  
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

**Hasil dari **collaborative content filtering****  
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

![prediction](https://github.com/evlinzxxx/FinalProject/blob/b6339346092a9e262285c68d6b72ffac3022522b/prediction.png)

2. hasil Evaluasi untuk Collaborative Filtering

Metrik yang digunakan untuk mengevaluasi kinerja model dalam kasus ini adalah RMSE (Root Mean Squared Error).

RMSE digunakan untuk mengukur sejauh mana hasil prediksi model mendekati nilai yang sebenarnya. Ini dihitung dengan mengambil akar kuadrat dari rata-rata kuadrat selisih antara nilai yang diprediksi dan nilai yang teramati. Model dengan nilai RMSE yang lebih kecil dianggap memiliki akurasi yang lebih tinggi, karena kesalahan prediksinya lebih kecil.

Berikut adalah beberapa kelebihan dan kekurangan dari metrik ini:

- Kelebihan: RMSE memberikan penalti yang lebih besar pada kesalahan besar, sehingga dapat lebih akurat dalam kasus di mana kesalahan besar sangat merugikan.
- Kekurangan: RMSE cenderung memberikan bobot yang lebih besar pada kesalahan besar, yang dapat menyebabkan hasil yang terlalu sensitif terhadap nilai ekstrem, terutama dalam dataset yang mengandung nilai yang sangat jauh dari prediksi.

Formula RMSE:

![RMSE](https://github.com/evlinzxxx/FinalProject/blob/ec2a34d4eb04ceb554efe339fb458872c250473d/RMSE.jpg)


cara menerapkan metrik tersebut adalah dengan menambahkan **_'metrics=[tf.keras.metrics.RootMeanSquaredError()]'_** pada model.compile.

hasil dari model evaluasi visualisasi matriks adalah sebagai berikut :  

![evaluation](https://github.com/evlinzxxx/FinalProject/blob/ec2a34d4eb04ceb554efe339fb458872c250473d/evaluation.png)

dari visualisasi proses training model di atas model berhenti di epochs sekitar 20. Dari proses ini, kita memperoleh nilai error akhir sebesar sekitar 0.195 dan error pada data validasi sebesar 0.207. 

## Kesimpulan

Dalam proyek ini, saya berhasil membangun sistem rekomendasi film menggunakan dua algoritma machine learning: Content-Based Filtering (CBF) dan Collaborative Filtering (CF). Kedua metode ini digunakan untuk memberikan rekomendasi film yang relevan berdasarkan riwayat aktivitas pengguna dan rating yang diberikan oleh pengguna lain.

- Content-Based Filtering (CBF): Algoritma ini memberikan rekomendasi berdasarkan film yang disukai oleh pengguna di masa lalu. Berdasarkan hasil pengujian, sistem ini berhasil memberikan rekomendasi film dengan genre yang sangat mirip dengan genre film yang sebelumnya disukai oleh pengguna, menunjukkan akurasi yang tinggi dengan precision mencapai 100%.

- Collaborative Filtering (CF): Algoritma ini menggunakan rating dari pengguna lain untuk memberikan rekomendasi. Dengan menggunakan RMSE untuk evaluasi, model ini menunjukkan bahwa hasil prediksi memiliki tingkat error yang rendah, yaitu sekitar 0.195 pada data pelatihan dan 0.207 pada data validasi. Hal ini menunjukkan bahwa model memiliki akurasi yang cukup baik dalam memprediksi film yang mungkin disukai oleh pengguna berdasarkan preferensi orang lain.


## Referensi 
* [[1]](https://publikasi.dinus.ac.id/index.php/technoc/article/view/8556) Faurina, R., & Sitanggang, E. (2023). Implementasi metode content-based filtering dan collaborative filtering pada sistem rekomendasi wisata di Bali. Tugas Cendekia, 22(4). https://doi.org/10.33633/tc.v22i4.8556 

  
**---Ini adalah bagian akhir laporan---**
