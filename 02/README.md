# Laporan Praktikum

## Praktikum Minggu Kedua

**Nama:** Yoga Prima Aditama  
**Judul Modul:** Komunikasi Antar Proses pada Sistem Terdistribusi  

---

## Langkah Praktikum

### 1. Menampilkan proses yang berjalan

Langkah yang dilakukan:
- Menekan tombol **Ctrl + Shift + Esc** pada keyboard
- Task Manager akan terbuka

Pada tab **Processes**, terlihat berbagai proses yang sedang berjalan pada komputer seperti:
- System
- Windows Explorer
- Google Chrome
- Discord
- dan lain-lain

---

## Hasil Screenshot
![Screenshot](img/screenshot.png)



## Pembahasan: Menggunakan Strawberry untuk GraphQL Server

Pada praktikum ini dilakukan pembuatan GraphQL server menggunakan library **Strawberry** pada bahasa pemrograman Python. Strawberry merupakan library yang digunakan untuk membangun GraphQL API secara sederhana dengan memanfaatkan fitur *type hint* yang ada pada Python sehingga struktur data dan query dapat didefinisikan dengan lebih jelas.

Langkah pertama yang dilakukan adalah membuat workspace dan environment Python. Environment digunakan agar proses pengembangan terisolasi dari konfigurasi Python yang ada pada sistem utama. Setelah environment aktif, dilakukan instalasi paket yang diperlukan menggunakan perintah berikut:

uv pip install 'strawberry-graphql[cli]'

Setelah instalasi selesai, dibuat sebuah file `schema.py` yang berfungsi sebagai definisi struktur data serta query yang dapat diakses oleh client. Pada file tersebut didefinisikan tipe data `Book` yang memiliki atribut `title` dan `author`. Selain itu dibuat juga kelas `Query` yang berfungsi untuk menyediakan data buku yang dapat diminta oleh client melalui GraphQL.

Strawberry kemudian digunakan untuk membangun schema GraphQL dengan memanfaatkan decorator `@strawberry.type`. Schema ini menjadi dasar dari server GraphQL yang akan memproses setiap permintaan query dari client.

Server dijalankan menggunakan perintah:

strawberry server schema


Ketika server berhasil dijalankan, endpoint GraphQL dapat diakses melalui browser pada alamat:

http://localhost:8000/graphql


Pada halaman tersebut terdapat antarmuka GraphQL yang memungkinkan pengguna menuliskan query secara langsung. Query dituliskan pada bagian kiri layar, sedangkan hasil dari query akan ditampilkan pada bagian kanan layar.

Contoh query yang digunakan pada praktikum ini adalah sebagai berikut:

{
books {
title
author
}
}


Query tersebut digunakan untuk mengambil data buku yang berisi informasi judul buku dan nama penulis dari server. Setelah tombol **Run** ditekan, server akan memproses query tersebut dan mengembalikan data dalam bentuk JSON.

Melalui praktikum ini dapat dipahami bahwa GraphQL memungkinkan komunikasi antara client dan server menjadi lebih fleksibel karena client dapat menentukan sendiri data apa saja yang ingin diminta dari server. Dengan menggunakan Strawberry, proses pembuatan GraphQL server pada Python menjadi lebih mudah dan terstruktur.
