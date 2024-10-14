# system-recomendation-film


# Latar Belakang
Sistem rekomendasi telah menjadi elemen penting dalam pengalaman pengguna di berbagai platform digital, terutama dalam industri film. Dengan adanya berbagai pilihan film yang tersedia, pengguna sering kali merasa kesulitan untuk memilih film yang sesuai dengan selera mereka. Oleh karena itu, sistem rekomendasi film yang efektif dapat membantu pengguna menemukan film yang relevan dan menarik berdasarkan preferensi dan perilaku mereka sebelumnya. Dalam proyek ini, kami akan mengembangkan sistem rekomendasi film dengan menggunakan dua pendekatan utama: content-based filtering dan collaborative filtering.
# Bussines Understanding
Problem Statement:
Platform streaming atau layanan film sering menghadapi tantangan untuk menyediakan rekomendasi film yang relevan kepada penggunanya. Dengan meningkatnya jumlah film yang tersedia, pengguna sering kali kesulitan menemukan film yang sesuai dengan selera mereka.

Masalah yang ingin diselesaikan:

* Bagaimana sistem dapat memberikan rekomendasi film yang sesuai dengan preferensi pengguna?
* Apakah sistem rekomendasi dapat membantu mengurangi waktu yang dihabiskan pengguna dalam mencari film?
## Goals:
Tujuan utama adalah membangun sistem rekomendasi film yang:

* Personalisasi: Memberikan rekomendasi film yang cocok dengan selera pengguna berdasarkan film yang sudah pernah mereka tonton atau nilai.
Efisiensi: Mengurangi waktu pencarian film bagi pengguna, sehingga mereka lebih cepat menemukan film yang sesuai.
* Akurat: Menggunakan pendekatan yang mampu memberikan hasil rekomendasi yang akurat dan relevan.
## Solution Approach:
Content-Based Filtering: Pendekatan ini fokus pada karakteristik film itu sendiri, seperti genre dan rating. Sistem akan merekomendasikan film yang mirip dengan yang telah ditonton oleh pengguna. Dalam hal ini, kemiripan antar film dihitung menggunakan cosine similarity berdasarkan fitur yang diekstraksi dari teks (genre dan rating).

Kelebihan:

Mudah dipahami dan diimplementasikan.
Cocok untuk pengguna baru yang belum memiliki banyak interaksi.
Kekurangan:

Terbatas hanya pada film yang memiliki kemiripan fitur. Tidak dapat memberikan rekomendasi film di luar preferensi pengguna sebelumnya.
Collaborative Filtering: Pendekatan ini melibatkan data dari berbagai pengguna untuk menemukan pola dalam rating atau preferensi film. Sistem ini merekomendasikan film berdasarkan kesamaan preferensi antar pengguna, sehingga memungkinkan untuk memberikan rekomendasi film yang belum pernah ditonton oleh pengguna namun disukai oleh orang dengan selera yang mirip.

Kelebihan:

Dapat merekomendasikan film yang belum pernah ditonton oleh pengguna.
Menggunakan informasi dari berbagai pengguna, memungkinkan rekomendasi lebih variatif.
Kekurangan:

Membutuhkan jumlah data interaksi pengguna yang besar.
Rentan terhadap masalah cold-start, di mana pengguna baru atau film baru tidak memiliki cukup informasi untuk direkomendasikan.

# Data Understanding
Data Understanding adalah tahap awal proyek yang bertujuan untuk memahami data yang tersedia. Dalam konteks sistem rekomendasi film ini, kita memiliki beberapa file terpisah yang berisi informasi mengenai film, pengguna, dan rating yang diberikan oleh pengguna. Data ini akan menjadi dasar untuk pengembangan sistem rekomendasi dan perlu dieksplorasi untuk mendapatkan wawasan awal mengenai karakteristik dan struktur data.
* Source Data from => https://www.kaggle.com/datasets/jaidalmotra/movies-review
Jumlah data: 1400
Jumlah data duplicated : 264
Jumlah data duplicated : 0
Index: 1136 entries, 0 to 1399
Data columns (total 10 columns):
## Movie Dataset Overview

| Column         | Non-Null Count | Data Type |
| -------------- | -------------- | --------- |
| name           | 1136           | object    |
| year           | 1136           | int64     |
| movie_rated    | 1136           | object    |
| run_length     | 1136           | object    |
| genres         | 1136           | object    |
| release_date   | 1136           | object    |
| rating         | 1136           | float64   |
| num_raters     | 1136           | int64     |
| num_reviews    | 1136           | int64     |
| review_url     | 1136           | object    |


# Univariate Exploratory Data Analysis
Pada tahap ini, kami akan melakukan analisis dan eksplorasi setiap variabel dalam data. Kami akan mengevaluasi distribusi rating film, genre yang paling umum, serta karakteristik pengguna, seperti usia dan preferensi genre. Analisis ini bertujuan untuk memberikan pemahaman yang lebih baik tentang bagaimana variabel-variabel ini saling berinteraksi dan pengaruhnya terhadap rekomendasi film. Selain itu, jika diperlukan, eksplorasi lebih lanjut mengenai hubungan antar variabel akan dilakukan untuk mengidentifikasi pola yang relevan.
![image](https://github.com/user-attachments/assets/ce6a4aaf-b31c-4a9d-b67d-3c9cf173a747)

# Data Preprocessing
Data Preprocessing adalah tahap persiapan data sebelum digunakan dalam proses pemodelan. Dalam tahap ini, beberapa file yang berkaitan akan digabungkan untuk membentuk satu dataset yang utuh. Proses ini termasuk penggabungan data mengenai film, pengguna, dan rating. Selain itu, kami juga akan melakukan pembersihan data untuk menghapus duplikasi dan memastikan konsistensi format data agar siap digunakan dalam tahap selanjutnya.
*Data outlier yang  sudah dibersihkan
![image](https://github.com/user-attachments/assets/b08a9c09-eab8-491a-9997-e36a2191ce9f)
pengecekan head data film yang sudah dibersihkan
![image](https://github.com/user-attachments/assets/9570ab01-3e62-4fc2-b555-bcb8660b96e9)
# Data Preparation
Pada tahap ini, kami akan mempersiapkan data dengan beberapa teknik untuk mengatasi masalah seperti missing value. Kami akan memastikan bahwa setiap film memiliki informasi yang lengkap, termasuk genre dan rating. Selain itu, untuk sistem rekomendasi berbasis konten yang akan dikembangkan, kami perlu memverifikasi bahwa setiap film memiliki satu genre yang jelas. Ini penting agar rekomendasi yang diberikan relevan dengan preferensi pengguna.
* Mengatasi Missing Values
Pada langkah awal, dilakukan pembersihan data dengan menghapus baris yang memiliki nilai yang hilang (missing values). Ini penting untuk memastikan bahwa data yang akan digunakan bersih dan tidak ada kekurangan informasi yang dapat mempengaruhi hasil model.

* Menyamakan Genre Film
Jika kolom genres berisi lebih dari satu genre, hanya genre pertama yang diambil. Hal ini dilakukan untuk menyederhanakan representasi genre dan memastikan konsistensi dalam data.

* Encoding untuk Variabel Kategorikal (Genres)
Variabel kategorikal pada kolom genres diubah menjadi bentuk numerik menggunakan teknik One-Hot Encoding. Teknik ini mengubah kategori menjadi representasi numerik biner, di mana setiap kategori (genre) direpresentasikan sebagai kolom terpisah.

* Normalisasi Fitur Numerik
Fitur numerik seperti rating, num_raters, dan num_reviews dinormalisasi menggunakan metode StandardScaler. Normalisasi ini penting untuk memastikan semua fitur berada dalam skala yang sama, sehingga model dapat memperlakukan semua fitur secara seimbang.

* Membangun Fitur Gabungan
Untuk mempersiapkan representasi fitur yang lebih kompleks, beberapa fitur digabungkan menjadi satu. Misalnya, genre dan rating digabungkan menjadi sebuah string, yang akan digunakan untuk membangun representasi teks.

* Ekstraksi Fitur Menggunakan TF-IDF
Pada tahap ini, TF-IDF (Term Frequency-Inverse Document Frequency) digunakan untuk membangun representasi fitur berbasis teks dari kolom gabungan genre dan rating. TF-IDF membantu menilai pentingnya kata (dalam hal ini genre dan rating) dalam setiap film, berdasarkan frekuensi kemunculannya di seluruh dataset.
``berikut kode nya ``
![image](https://github.com/user-attachments/assets/3c41de09-cbc3-45cf-b578-072e11ec769f)

Menghitung Similaritas Cosine
Setelah membangun matriks TF-IDF, dihitung similaritas cosine antar film. Similaritas cosine digunakan untuk mengukur kemiripan antara dua film berdasarkan fitur gabungan yang telah dihasilkan, dengan hasilnya berupa nilai antara 0 dan 1, di mana 1 menunjukkan kesamaan penuh.<br>
![image](https://github.com/user-attachments/assets/687a2554-55de-41e1-86a1-5b6aa71dccca)


# Model Development dengan Content-Based Filtering
* Pada tahap ini, kami akan mengembangkan sistem rekomendasi menggunakan teknik content-based filtering. Teknik ini akan merekomendasikan film yang mirip dengan film yang disukai pengguna di masa lalu. Kami akan menggunakan tf-idf vectorizer untuk menemukan representasi fitur penting dari setiap genre film dan menghitung tingkat kesamaan menggunakan cosine similarity. Berdasarkan hasil perhitungan ini, sistem akan memberikan sejumlah rekomendasi film untuk pengguna berdasarkan film yang telah mereka tonton dan sukai sebelumnya.
* Pada tahap ini, pendekatan content-based filtering digunakan untuk merekomendasikan film berdasarkan kemiripan fitur antarfilm. Pendekatan ini bekerja dengan cara mencari film-film yang memiliki fitur serupa dengan film yang diinputkan oleh pengguna, berdasarkan genre, rating, atau atribut lain yang relevan. Model yang digunakan untuk mengukur kesamaan antarfilm adalah Cosine Similarity, yang umum digunakan dalam analisis berbasis teks atau fitur yang direpresentasikan dalam bentuk vektor.

* Penjelasan Detail Model
Content-Based Filtering
Content-based filtering adalah metode rekomendasi yang menganalisis berbagai fitur konten film (seperti genre, rating, dll.) untuk mencari kesamaan dengan film lain. Pendekatan ini hanya menggunakan data film itu sendiri tanpa memperhitungkan preferensi pengguna lain, sehingga menghasilkan rekomendasi yang didasarkan pada konten serupa.

* Cosine Similarity sebagai Model
Cosine similarity adalah teknik untuk mengukur kesamaan antar dokumen (dalam hal ini antar film) yang direpresentasikan dalam bentuk vektor. Cosine similarity menghitung sudut antara dua vektor dalam ruang multidimensi, dengan nilai yang berkisar antara 0 hingga 1. Semakin dekat nilai cosine similarity ke 1, semakin mirip kedua film tersebut.

* Vektor film dibangun menggunakan TF-IDF (Term Frequency-Inverse Document Frequency), yang mewakili teks (genre dan rating) dalam bentuk numerik, dengan mempertimbangkan seberapa sering sebuah genre muncul dalam seluruh dataset. Hal ini memastikan bahwa genre yang lebih unik mendapat bobot yang lebih tinggi.
Cosine similarity kemudian diterapkan pada vektor ini untuk mengukur kesamaan antara film yang dipilih dengan film lain.
Fungsi Rekomendasi
Fungsi get_recommendations bekerja dengan cara sebagai berikut:

* Mencari Indeks Film: Berdasarkan judul film yang diberikan, fungsi mencari indeks film tersebut dalam dataset.
Menghitung Skor Kesamaan: Cosine similarity digunakan untuk menghitung skor kesamaan antara film yang dituju dengan semua film lain dalam dataset.
Mengurutkan Skor Kesamaan: Setelah skor kesamaan dihitung, film-film diurutkan berdasarkan skor tertinggi, sehingga film dengan konten paling mirip berada di urutan teratas.
Mengambil 10 Film Teratas: Setelah diurutkan, fungsi akan memilih 10 film teratas yang direkomendasikan (kecuali film itu sendiri).
Mengembalikan Rekomendasi: Fungsi mengembalikan daftar film yang direkomendasikan, termasuk informasi seperti nama film, genre, dan rating.
* Hasil Rekomendasi
Pengguna dapat menginput judul film (misalnya, V for Vendetta), dan model akan mengembalikan daftar film yang paling mirip berdasarkan genre dan rating. Daftar rekomendasi ini dapat digunakan untuk membantu pengguna menemukan film-film lain yang mungkin sesuai dengan preferensi mereka.
![image](https://github.com/user-attachments/assets/097c2815-2bf7-4b05-996a-da242ca6ea70)
# Evaluation
## Masalah yang Ingin Diselesaikan:

* Rekomendasi Film Berdasarkan Preferensi: Sistem ini bertujuan untuk memberikan rekomendasi film yang sesuai dengan preferensi pengguna berdasarkan kesamaan konten film seperti genre dan rating. Dengan pendekatan content-based filtering, sistem menggunakan informasi yang tersedia dari film yang sudah pernah ditonton atau dinilai pengguna untuk mencari film-film lain yang memiliki kemiripan konten.
* Mengurangi Waktu Pencarian Film: Salah satu masalah umum yang dihadapi pengguna adalah lamanya waktu yang dihabiskan dalam mencari film yang sesuai dengan selera mereka. Sistem ini berusaha menyelesaikan masalah tersebut dengan memberikan daftar rekomendasi yang langsung relevan dan berkualitas tinggi, sehingga mengurangi waktu pencarian.
## Goals
* Personalisasi: Tujuan pertama dari sistem ini adalah untuk memberikan rekomendasi yang dipersonalisasi berdasarkan film yang telah dipilih pengguna. Melalui metode cosine similarity yang membandingkan genre dan rating antarfilm, sistem mampu memberikan film yang serupa secara konten. Misalnya, jika pengguna menyukai V for Vendetta, sistem akan merekomendasikan film dengan genre yang sama seperti Action, Drama, atau Sci-Fi, seperti terlihat pada hasil rekomendasi yang relevan.

* Efisiensi: Efisiensi merupakan salah satu tujuan utama sistem ini, di mana pengguna dapat dengan cepat menemukan film yang sesuai dengan preferensi mereka. Dengan menggunakan pendekatan content-based filtering, sistem mampu memproses dan menganalisis data secara efisien, menghasilkan rekomendasi dalam waktu singkat tanpa perlu melakukan perbandingan yang terlalu kompleks dengan preferensi pengguna lain, seperti pada collaborative filtering.

* Akurasi: Akurasi dari sistem ini diukur berdasarkan kemampuan untuk merekomendasikan film yang relevan dengan film input. Pada hasil rekomendasi (V for Vendetta), sebagian besar film yang direkomendasikan memiliki kemiripan dari segi genre, seperti Action, Drama, Thriller, atau Sci-Fi. Ini menunjukkan bahwa sistem mampu memberikan rekomendasi yang akurat dan relevan dengan preferensi pengguna berdasarkan kesamaan konten.

* Evaluasi Akurasi: Berdasarkan output yang dihasilkan, rekomendasi yang diberikan oleh sistem sebagian besar relevan dengan film yang diminta. Film-film seperti Batman Begins, Indiana Jones and the Last Crusade, serta Die Hard yang memiliki genre Action dan Adventure sangat cocok direkomendasikan setelah input film V for Vendetta. Ini menunjukkan bahwa sistem memberikan hasil yang akurat sesuai dengan harapan.

* Efisiensi: Pengguna dapat dengan cepat menemukan film yang sesuai tanpa harus melalui proses panjang untuk mencari satu per satu dari seluruh katalog film. Dalam hitungan detik, rekomendasi yang relevan disajikan, sehingga menghemat waktu pengguna dalam memilih film.

* Personalisasi: Meskipun sistem sudah memberikan rekomendasi yang relevan berdasarkan konten film yang dipilih, tingkat personalisasi ini masih terbatas pada kesamaan konten. Untuk peningkatan personalisasi yang lebih mendalam, kombinasi dengan metode lain seperti collaborative filtering atau pengumpulan feedback pengguna lebih lanjut dapat meningkatkan kemampuan rekomendasi sistem.

## Kesimpulan Evaluasi
Sistem rekomendasi ini telah memenuhi tujuan utamanya, yakni memberikan hasil yang akurat, efisien, dan relevan. Pengguna dapat menikmati rekomendasi film yang sesuai dengan preferensi mereka secara cepat, mengurangi waktu yang dihabiskan dalam pencarian film. Meski begitu, untuk personalisasi yang lebih mendalam, sistem ini dapat diintegrasikan dengan metode lain di masa depan.
* ![image](https://github.com/user-attachments/assets/c25fee73-d3b9-4129-a467-2fd4a3037121)

# Referensi Jurnal
* Linden, G., Smith, B. A., & York, J. (2003). "Amazon.com recommendations: Item-to-item collaborative filtering." IEEE Internet Computing, 7(1), 76-80. DOI: 10.1109/MIC.2003.1167344
* Sebastiani, F. (2002). "Machine learning in automated text categorization." ACM Computing Surveys (CSUR), 34(1), 1-47. DOI: 10.1145/505230.505235
Jannach, D., & Adomavicius, G. (2016). "Recommendation Systems: Challenges and Solutions." Computer Science Review, 20, 1-18. DOI: 10.1016/j.cosrev.2016.01.002
# Daftar Pustaka
* Linden, G., Smith, B. A., & York, J. (2003). Amazon.com recommendations: Item-to-item collaborative filtering. IEEE Internet Computing, 7(1), 76-80. DOI: 10.1109/MIC.2003.1167344
* Sebastiani, F. (2002). Machine learning in automated text categorization. ACM Computing Surveys (CSUR), 34(1), 1-47. DOI: 10.1145/505230.505235
Jannach, D., & Adomavicius, G. (2016). Recommendation Systems: Challenges and Solutions. Computer Science Review, 20, 1-18. DOI: 10.1016/j.cosrev.2016.01.002
