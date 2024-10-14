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
Pada tahap ini, kami akan mengembangkan sistem rekomendasi menggunakan teknik content-based filtering. Teknik ini akan merekomendasikan film yang mirip dengan film yang disukai pengguna di masa lalu. Kami akan menggunakan tf-idf vectorizer untuk menemukan representasi fitur penting dari setiap genre film dan menghitung tingkat kesamaan menggunakan cosine similarity. Berdasarkan hasil perhitungan ini, sistem akan memberikan sejumlah rekomendasi film untuk pengguna berdasarkan film yang telah mereka tonton dan sukai sebelumnya.
![image](https://github.com/user-attachments/assets/097c2815-2bf7-4b05-996a-da242ca6ea70)
# Evaluation
* Akurasi: Sebagian besar film yang direkomendasikan relevan dan memiliki kemiripan dengan film input berdasarkan genre dan rating. Ini menunjukkan bahwa sistem sudah memenuhi tujuan akurasi.

* Efisiensi: Pengguna dapat menemukan film yang relevan dengan cepat tanpa harus menelusuri seluruh katalog. Sistem membantu dalam mengurangi waktu pencarian.

* Personalisasi: Sistem telah memberikan hasil yang dipersonalisasi berdasarkan film yang sudah dipilih pengguna. Namun, untuk personalisasi lebih mendalam, kombinasi dengan metode lain seperti collaborative filtering dapat dilakukan.
* ![image](https://github.com/user-attachments/assets/c25fee73-d3b9-4129-a467-2fd4a3037121)

# Referensi Jurnal
* Linden, G., Smith, B. A., & York, J. (2003). "Amazon.com recommendations: Item-to-item collaborative filtering." IEEE Internet Computing, 7(1), 76-80. DOI: 10.1109/MIC.2003.1167344
* Sebastiani, F. (2002). "Machine learning in automated text categorization." ACM Computing Surveys (CSUR), 34(1), 1-47. DOI: 10.1145/505230.505235
Jannach, D., & Adomavicius, G. (2016). "Recommendation Systems: Challenges and Solutions." Computer Science Review, 20, 1-18. DOI: 10.1016/j.cosrev.2016.01.002
# Daftar Pustaka
* Linden, G., Smith, B. A., & York, J. (2003). Amazon.com recommendations: Item-to-item collaborative filtering. IEEE Internet Computing, 7(1), 76-80. DOI: 10.1109/MIC.2003.1167344
* Sebastiani, F. (2002). Machine learning in automated text categorization. ACM Computing Surveys (CSUR), 34(1), 1-47. DOI: 10.1145/505230.505235
Jannach, D., & Adomavicius, G. (2016). Recommendation Systems: Challenges and Solutions. Computer Science Review, 20, 1-18. DOI: 10.1016/j.cosrev.2016.01.002
