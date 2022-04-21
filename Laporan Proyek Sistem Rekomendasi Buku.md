# Laporan Proyek Machine Learning Sistem Rekomendasi Buku - Mellania Permata Sylvie
---
 
## Domain Problem
Buku    merupakan    sumber    informasi    semua    aspek    kehidupan    khususnya pendidikan.  Ada pepatah menyebutkan bahwa membaca adalah jendela dunia. Dari sini, dapat diketahui bahwa membaca itu penting. Namun  rendahnya  minat  baca  dikalangan  masyarakat  menjadi  persoalan penting    di    dunia    pendidikan    saat    ini. Untuk meningkatkan minat baca di kalangan masyarakat, maka dibuatlah proyek sistem rekomendasi buku.

Proyek ini berfokus pada domain dunia pendidikan. Dengan memanfaatkan data yang ada, peneliti menerapkan metode content based filtering dan collaborative filtering dalam proyek ini. Dengan mendapatkan rekomendasi buku yang sesuai, pembaca dapat mengetahui informasi mengenai buku yang sesuai dengan minatnya sehingga nantinya minat baca dikalangan masyarakat akan naik.
Dalam mengerjakan proyek ini, peneliti memulai dengan studi literatur. Adapun referensi yang digunakan oleh peneliti diantaranya :
- [Jurnal 1]  -  Sistem Rekomendasi Buku pada Perpustakaan Daerah Provinsi Kalimantan Selatan Menggunakan Metode Content-Based Filtering 
- [Jurnal 2]  -  Sistem Rekomendasi: Buku Online dengan Metode Collaborative Filtering
- [Jurnal 3]  -  Sistem Rekomendasi Buku Pada Aplikasi Perpustakaan Menggunakan Metode Collaborative Filtering Pada SMKN 1 BANGIL

## Business Understanding
### Problem Statements
Seperti yang dijelaskan sebelumnya, proyek ini akan membuat  sistem rekomendasi buku. Sehingga permasalahan yang perlu untuk diselesaikan yaitu sebagai berikut.
- Bagaimana membuat sistem rekomendasi dengan content-based filtering ?
- Dengan data rating yang dimiliki, bagaimana membuat rekomendasi buku lain yang mungkin disukai dan belum pernah dibaca oleh pembaca?  ?

### Goals
Sesuai dengan permasalahan yang ada, maka goals dalam proyek ini diantaranya sebagai berikut.
- Menghasilkan sejumlah rekomendasi restoran yang dipersonalisasi untuk pembaca dengan teknik content-based filtering.
- Menghasilkan sejumlah rekomendasi buku yang sesuai dengan preferensi pengguna dan belum pernah dibaca sebelumnya dengan teknik collaborative filtering.

### Solution Statements
Agar bisa menjawab masalah di atas dan mencapai goals yang sudah ditentukan, maka solusi yang dilakukan yaitu membuat model development dengan algoritma content based filtering dan collaborative filtering. Berikut penjelasannya.
- **Content Based Filtering**
Content-based filtering mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna. Algoritma ini bekerja dengan menyarankan item serupa yang pernah disukai di masa lalu atau sedang dilihat di masa kini kepada pengguna. Semakin banyak informasi yang diberikan pengguna, semakin baik akurasi sistem rekomendasi.
Kelebihan dari teknik ini yaitu baik dipakai ketika skala user yang besar, dapat menemukan ketertarikan spesifik dari seorang user dan dapat merekomendasikan item yang jarang disukai orang lain.
Kekurangan dari teknik ini yaitu karena meta feature yang digunakan kita yang menentukan sendiri, kualitas dari rekomendasi tergantung kualitas dari meta feature itu sendiri.

- **Collaborative Filtering**
Collaborative filtering adalah metode yang digunakan untuk memprediksi kegunaan item berdasarkan penilaian pengguna sebelumnya, misalnya cara pemberian rating terhadap suatu item (Lam, 2004). Metode ini merekomendasikan item-item yang dipilih oleh   pengguna lain dengan kemiripan model item dari pengguna saat ini.

## Data Understanding
Proyek ini menggunakan dataset goodbooks-10k. Dataset ini berisi . Dataset ini berisi data sepuluh ribu buku, satu juta peringkat. Juga buku yang ditandai untuk dibaca, dan tag. Dataset ini memiliki 5 file terpisah mengenai data buku, data label buku (genre) dan rating pembaca. Berikut merupakan penjelasan setiap file csvnya. 
1. **File book_tags.csv**
File yang berisi data tag buku (label), diurutkan berdasarkan ascending goodreadsbookid dan count descending.
    - **goodreads_id** : ID dari goodreads
    - **tag_id** : ID tag (label)
    - **count** : Jumlah goodreads
2. **books.csv**
File yang berisi mengenai informasi buku.
    - **id** : ID dari file books
    - **book_id** : ID buku
    - **best_book_id** : ID dari buku populer
    - **work_id** : ID karya
    - **books_count** : jumlah edisi buku tertentu
    - **isbn** : Nomor isbn
    - **authors** : Nama penulis
    - **original_publication_year** : Tahun rilis buku
    - **original_title** : Judul asli buku
3. **ratings.csv**
File yang berisi tentang rating buku sesuai id pengguna.
    - **book_id** : ID buku
    - **user_id** : ID Pengguna
    - **rating** : rating buku
4. **tags.csv**
File yang berisi tentang pemetaan id-nama tag.
    - **tag_id** : ID tag (label/genre)
    - **tag_name** : Nama tag (label/genre)
5. **to_read.csv**
File mengenai buku yang ditandai oleh pengguna "untuk dibaca". Diurutkan berdasarkan user_id dan book_id.
    - **user_id** : ID pengguna/pembaca
    - **book_id** : ID buku

Pada proyek kali ini, file yang digunakan untuk pemodelan ada 2 file yaitu file **books.csv dan ratings.csv**. Pada model content based filtering, kolom yang digunakan yaitu **book_id, original_title, authors, original_publication_year**. Sedangkan pada model collaborative filtering kolom yang digunakan yaitu **user_id, book_id, authors, original_title**.
Dataset ini bisa diunduh di Kaggle. Berikut linknya [Klik Disini].

## Data Preparation
Dalam proyek ini, tahapan data preparation yang digunakan yaitu mengatasi missing value, encode fitur, membagi dataset. Berikut merupakan penjelasannya :
- **Mengatasi Missing Value**
Pada tahap ini akan dilakukan proses pengecekan data yang bernilai null atau kosong. Fungsi yang digunakan yaitu fungsi isnull() dari library pandas. Untuk menghilangkan data yang null atau kosong, maka digunakan fungsi dropna() untuk menghapus missing valuenya.
- **Encoding Fitur**
Teknik selanjutnya yang digunakan yaitu teknik encoding fitur. persiapan data untuk menyandikan (encode) fitur user_id dan book_id  ke dalam indeks integer. Data preparation ini digunakan dalam model collaborative filtering.
- **Membagi Dataset**
Sebelum membuat model, penting bagi kita untuk membagi dataset menjadi data latih (train) dan data uji (test). Proses membagi dataset ini menggunakan library Scikitlearn. Disini datasetnya dibagi menjadi 80% data train dan 20% data test.

## Modeling
Proyek ini menggunakan 2 jenis model development. Pertama yaitu model algoritma content based filtering dan kedua yaitu menggunakan collaborative filtering.
1. **Content Based Filtering**
Dalam proses modeling dengan content based filtering, penulis menggunakan metode TF-IDF Vectorizer untuk membangun sistem rekomendasi sederhana berdasarkan jenis penulis buku. 
Setelah dilakukan model development dengan content based filtering, berikut merupakan hasil output modelnya :
**Data Pencarian Buku**
![pencarian buku](https://i.postimg.cc/y8cp3rHY/Screenshot-12.jpg "Pencarian buku")
**Hasil Rekomendasi**
![hasil rekomendasi](https://i.postimg.cc/dVZ32rH0/Screenshot-13.jpg "hasil rekomendasi")
Berdasarkan hasil di atas dapat diketahui bahwa buku yang direkomendasikan itu adalah buku dengan penulis yang sama.

2. **Collaborative Filtering**
Dalam proses modeling dengan collaborative filtering dilakukan proses embedding terhadap data user dan buku. Selanjutnya, lakukan operasi perkalian dot product antara embedding user dan buku. Model ini menerapkan keras model class.
Berikut merupakan hasil dari output model ini :
![Hasil collaborative filtering](https://i.postimg.cc/CLcYR5wx/Screenshot-14.jpg "hasil rekomendasi")
Hasil diatas menyebutkan bahwa sistem merekomendasikan buku untuk pembaca dengan user id tertentu. Lalu diberi rekomendasi buku yang memiliki rating paling tinggi dan Top 10 rekomendasi buku.

## Evaluation
Proyek ini menggunakan metrik Precision dan Mean Squared Error (MSE). Pada model content based filtering metrik yang digunakan yaitu precision, sedangkan pada model collaborative filtering menggunakan MSE. Berikut penjelasannya :

**Metrik Precision**
Metrik Precision merupakan metrik untuk evaluasi model machine learning dimana metrik ini yang mengkuantifikasi jumlah prediksi positif yang benar yang dibuat. Berikut merupakan rumus dari metrik precision.
![rumus presisi](https://i.postimg.cc/g2qnJ2mq/dos-819311f78d87da1e0fd8660171fa58e620211012160253.png "Rumus Presisi")
Sebelumnya sudah kita ketahui bahwa di output rekomendasi model content based filtering, kita mencari rekomendasi buku berdasarkan penulis. Penulis yang dicari adalah Bret Easton Ellis. Kemudian sistem memberikan 5 rekomendasi buku sebagai berikut.
![hasil rekomendasi](https://i.postimg.cc/dVZ32rH0/Screenshot-13.jpg "hasil rekomendasi")
Berdasarkan hasil rekomendasi di atas, ada 4 rekomendasi yang sesuai dan sama dengan penulis yang dicari. Hasil perhitungan metrik precisionnya yaitu:
Precision = Recommendation that are relevant/item we recommend Precission = 4/5 = 80%
Jadi hasil dari presisinya yaitu 80%.

**Mean Squared Error (MSE)**
Metrik ini menghitung selisih rata-rata nilai sebenarnya dengan nilai prediksi. Berikut merupakan rumus dari MSE :
![rumus mse](https://i.postimg.cc/zvgr6S9t/Screenshot-13.jpg "Rumus MSE")
Keterangan:
N = jumlah dataset
yi = nilai sebenarnya
y_pred = nilai prediksi

Kelebihan dari metrik ini yaitu metrik ini berguna jika kita memiliki nilai tak terduga yang harus kita pedulikan. Nilai sangat tinggi atau rendah yang harus kita perhatikan. Sedangkan kekurangan dari metrik ini yaitu Jika kita membuat satu prediksi yang sangat buruk, kuadrat akan membuat kesalahan lebih buruk dan itu mungkin membuat metrik cenderung melebih-lebihkan keburukan model.
cara menerapkan metrik ini ke dalam kode yaitu dengan kode berikut :
```sh
model.compile(
    loss = tf.keras.losses.BinaryCrossentropy(),
    optimizer = keras.optimizers.Adam(learning_rate=0.001),
    metrics=[tf.keras.metrics.MeanSquaredError()]
)
```
Berikut merupakan hasil visualisasi dari proses training model collaborative filtering :
![grafik](https://i.postimg.cc/3JzB3jzj/Screenshot-15.jpg "grafik MSE")
MSE nya terus menurun seiring bertambahnya epoch dan MSE nya berada di bawah angka 0.05.
---

[//]: # (berikut merupakan daftar link yang digunakan)

[Jurnal 1]: <https://journal.universitasbumigora.ac.id/index.php/matrik/article/view/617>
[Jurnal 2]: <https://ejournal.akprind.ac.id/index.php/technoscientia/article/view/612>
[Jurnal 3]: <https://www.jurnal.stmik-yadika.ac.id/index.php/spirit/article/view/52>
[Klik Disini]: <https://www.kaggle.com/zygmunt/goodbooks-10k>


