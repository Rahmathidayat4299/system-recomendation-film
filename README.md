# system-recomendation-film


# Latar Belakang
Sistem rekomendasi telah menjadi elemen penting dalam pengalaman pengguna di berbagai platform digital, terutama dalam industri film. Dengan adanya berbagai pilihan film yang tersedia, pengguna sering kali merasa kesulitan untuk memilih film yang sesuai dengan selera mereka. Oleh karena itu, sistem rekomendasi film yang efektif dapat membantu pengguna menemukan film yang relevan dan menarik berdasarkan preferensi dan perilaku mereka sebelumnya. Dalam proyek ini, kami akan mengembangkan sistem rekomendasi film dengan menggunakan dua pendekatan utama: content-based filtering dan collaborative filtering.

# Data Understanding
Data Understanding adalah tahap awal proyek yang bertujuan untuk memahami data yang tersedia. Dalam konteks sistem rekomendasi film ini, kita memiliki beberapa file terpisah yang berisi informasi mengenai film, pengguna, dan rating yang diberikan oleh pengguna. Data ini akan menjadi dasar untuk pengembangan sistem rekomendasi dan perlu dieksplorasi untuk mendapatkan wawasan awal mengenai karakteristik dan struktur data.
Jumlah data: 1400
Jumlah data duplicated : 264
Jumlah data null: name            0
year            0
movie_rated     0
run_length      0
genres          0
release_date    0
rating          0
num_raters      0
num_reviews     0
review_url      0
dtype: int64
Jumlah data duplicated : 0
Index: 1136 entries, 0 to 1399
Data columns (total 10 columns):
 #   Column        Non-Null Count  Dtype  
---  ------        --------------  -----  
 0   name          1136 non-null   object 
 1   year          1136 non-null   int64  
 2   movie_rated   1136 non-null   object 
 3   run_length    1136 non-null   object 
 4   genres        1136 non-null   object 
 5   release_date  1136 non-null   object 
 6   rating        1136 non-null   float64
 7   num_raters    1136 non-null   int64  
 8   num_reviews   1136 non-null   int64  
 9   review_url    1136 non-null   object
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

![image](https://github.com/user-attachments/assets/687a2554-55de-41e1-86a1-5b6aa71dccca)


# Model Development dengan Content-Based Filtering
Pada tahap ini, kami akan mengembangkan sistem rekomendasi menggunakan teknik content-based filtering. Teknik ini akan merekomendasikan film yang mirip dengan film yang disukai pengguna di masa lalu. Kami akan menggunakan tf-idf vectorizer untuk menemukan representasi fitur penting dari setiap genre film dan menghitung tingkat kesamaan menggunakan cosine similarity. Berdasarkan hasil perhitungan ini, sistem akan memberikan sejumlah rekomendasi film untuk pengguna berdasarkan film yang telah mereka tonton dan sukai sebelumnya.
![image](https://github.com/user-attachments/assets/097c2815-2bf7-4b05-996a-da242ca6ea70)

# Referensi Jurnal
* Linden, G., Smith, B. A., & York, J. (2003). "Amazon.com recommendations: Item-to-item collaborative filtering." IEEE Internet Computing, 7(1), 76-80. DOI: 10.1109/MIC.2003.1167344
* Sebastiani, F. (2002). "Machine learning in automated text categorization." ACM Computing Surveys (CSUR), 34(1), 1-47. DOI: 10.1145/505230.505235
Jannach, D., & Adomavicius, G. (2016). "Recommendation Systems: Challenges and Solutions." Computer Science Review, 20, 1-18. DOI: 10.1016/j.cosrev.2016.01.002
# Daftar Pustaka
* Linden, G., Smith, B. A., & York, J. (2003). Amazon.com recommendations: Item-to-item collaborative filtering. IEEE Internet Computing, 7(1), 76-80. DOI: 10.1109/MIC.2003.1167344
* Sebastiani, F. (2002). Machine learning in automated text categorization. ACM Computing Surveys (CSUR), 34(1), 1-47. DOI: 10.1145/505230.505235
Jannach, D., & Adomavicius, G. (2016). Recommendation Systems: Challenges and Solutions. Computer Science Review, 20, 1-18. DOI: 10.1016/j.cosrev.2016.01.002
