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
