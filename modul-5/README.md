# 📘 Pembahasan Modul 5 – Fault Tolerance

## 1. Load Balancing Aplikasi

Pada modul ini dibahas konsep **fault tolerance** dengan fokus pada **load balancing**. Load balancing bertujuan untuk meningkatkan *high availability* dengan cara menjalankan lebih dari satu instance aplikasi, lalu mendistribusikan request ke beberapa instance tersebut melalui proxy (nginx).

Aplikasi yang digunakan adalah aplikasi Python berbasis framework Blacksheep. Aplikasi ini hanya digunakan sebagai contoh sederhana untuk memahami konsep distribusi beban dalam sistem terdistribusi.

---

## 2. Pembuatan dan Konfigurasi Aplikasi

Tahapan awal meliputi:
- Menyiapkan environment Python (uv / miniconda / micromamba)
- Menginstall library `blacksheep` dan `blacksheep-cli`
- Membuat aplikasi web sederhana

Setelah aplikasi berhasil dijalankan di port 44777, aplikasi kemudian dikonfigurasi agar dapat berjalan di dalam Docker dengan port 80.

Hal ini penting karena nantinya nginx akan menggunakan port tersebut untuk melakukan load balancing.

---

## 3. Docker dan Docker Compose

Dalam implementasi load balancing, terdapat beberapa komponen utama:

### a. Aplikasi (bs_app)
Aplikasi dijalankan dalam container dan dapat di-scale menjadi beberapa instance.

### b. Nginx
Berfungsi sebagai load balancer yang:
- Menerima request dari client
- Mendistribusikan request ke beberapa instance aplikasi

### c. Docker Compose
Digunakan untuk mengelola semua container, termasuk:
- Build aplikasi
- Menjalankan nginx
- Scaling aplikasi (misalnya menjadi 2 instance)

---

## 4. Implementasi Load Balancing

Setelah semua container dijalankan:
- Aplikasi diakses melalui `localhost` (port 80)
- Semua request masuk melalui nginx

Ciri load balancing berhasil:
- Terdapat lebih dari satu instance aplikasi
- Request didistribusikan ke instance yang berbeda (terlihat dari log)

Dengan ini, sistem menjadi lebih siap menangani banyak request.

---

## 5. Failure Detection

Failure detection adalah proses untuk mengetahui apakah suatu komponen gagal.

### Heartbeat
Heartbeat digunakan untuk memantau kondisi layanan:
- Jika ada respon → layanan aktif
- Jika tidak ada respon → layanan dianggap gagal

Perbedaan kondisi:
- Saat aplikasi mati → tidak ada respon
- Saat aplikasi hidup → sistem merespon normal

---

## 6. Retry Mechanism (Tenacity)

Retry digunakan untuk mencoba ulang request ketika terjadi kegagalan.

Karakteristik:
- Akan mencoba beberapa kali sebelum benar-benar gagal
- Bisa diberi jeda waktu antar percobaan

Perbedaan kondisi:
- Aplikasi aktif → langsung berhasil
- Aplikasi mati → terjadi retry lalu gagal

Hal ini membantu sistem lebih tahan terhadap gangguan sementara.

---

## 7. Circuit Breaker

Circuit breaker adalah pola untuk mencegah kegagalan berantai.

### State Circuit Breaker:

- **Closed**
  - Semua request berjalan normal
  - Sistem memantau error

- **Open**
  - Terjadi banyak error
  - Request langsung ditolak

- **Half-Open**
  - Mencoba beberapa request
  - Jika berhasil → kembali ke closed
  - Jika gagal → kembali ke open

### Hasil Pengujian:
- Aplikasi aktif → tetap di state closed
- Aplikasi mati → berpindah ke open
- Setelah beberapa waktu → masuk half-open

---

## 8. Kesimpulan

Modul ini menunjukkan pentingnya fault tolerance dalam sistem terdistribusi.

Beberapa teknik utama:
- Load balancing → membagi beban
- Failure detection → mendeteksi error
- Retry → mencoba ulang
- Circuit breaker → mencegah kegagalan berantai

Dengan menerapkan semua ini, sistem menjadi:
- Lebih stabil
- Lebih scalable
- Lebih tahan terhadap kegagalan 
