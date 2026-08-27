📚 UKK Perpustakaan SMK N 1 Sanden

Sistem Informasi Perpustakaan Digital yang dibuat untuk UKK (Uji Kompetensi Keahlian) RPL SMK N 1 Sanden.

Aplikasi ini membantu pengelolaan katalog buku, data siswa, data petugas, peminjaman, persetujuan peminjaman, pengembalian, rating, ulasan, notifikasi, dan laporan perpustakaan.

🌐 Demo & Repository

Repository: github.com/Ayu155/perpusukk2

Demo: ayu155.github.io/perpusukk2
https://stitch.withgoogle.com/projects/17320341967523360622?pli=1

Catatan: Source aplikasi pada repository menggunakan PHP dan MySQL sehingga untuk menjalankan fungsi backend secara penuh diperlukan server PHP + MySQL. URL demo dapat digunakan sebagai halaman/demo frontend sesuai deployment yang tersedia.

✨ Fitur

👨‍💼 Admin

Admin memiliki akses untuk mengelola data utama sistem perpustakaan.

Dashboard statistik perpustakaan

Mengelola data buku

Menambah buku

Mengedit buku

Menghapus buku

Mengelola data siswa

Menambah siswa

Mengedit siswa

Menghapus siswa

Mengelola data petugas

Melihat laporan peminjaman

Melihat notifikasi pengajuan peminjaman

Melihat statistik buku dan peminjaman

Melihat buku populer

Melihat data keterlambatan

Melihat stok buku yang menipis

Melihat statistik kategori buku

Melihat rating dan kualitas buku

👨‍🏫 Petugas

Petugas bertanggung jawab terhadap pengelolaan buku dan proses peminjaman/pengembalian.

Dashboard petugas

Melihat data buku

Menambah data buku

Mengedit data buku

Menghapus data buku

Melihat data siswa

Mengelola persetujuan peminjaman

Menyetujui pengajuan peminjaman

Menolak pengajuan peminjaman

Memproses pengembalian buku

Menghitung denda keterlambatan

Mencatat kondisi buku saat pengembalian

Melihat riwayat peminjaman

👨‍🎓 Siswa

Siswa dapat menggunakan sistem untuk mencari dan meminjam buku.

Registrasi anggota

Login menggunakan username atau NIS

Dashboard siswa

Melihat koleksi buku

Mencari dan memilih buku

Mengajukan peminjaman

Membatalkan pengajuan yang masih menunggu

Melihat buku yang sedang dipinjam

Melihat buku yang akan jatuh tempo

Melihat riwayat peminjaman

Memberikan rating buku

Memberikan ulasan/komentar

Mengelola profil

Mengubah username

Mengubah password

🔐 Hak Akses

Role

Dashboard

Buku

Siswa

Petugas

Peminjaman

Pengembalian

Laporan

Rating & Ulasan

Admin

✅

✅

✅

✅

👁️

👁️

✅

👁️

Petugas

✅

✅

✅

❌

✅

✅

❌

👁️

Siswa

✅

👁️

👤

❌

✅

👁️

❌

✅

Keterangan:

✅ = memiliki akses/pengelolaan

👁️ = dapat melihat data

👤 = mengelola profil sendiri

❌ = tidak tersedia

🔄 Alur Peminjaman

┌─────────────┐
│    SISWA    │
└──────┬──────┘
       │
       ▼
     Login
       │
       ▼
Lihat Koleksi Buku
       │
       ▼
Ajukan Peminjaman
       │
       ▼
Status: MENUNGGU
       │
       ▼
┌──────────────┐
│   PETUGAS    │
└──────┬───────┘
       │
       ▼
Cek Pengajuan
       │
   ┌───┴────┐
   │        │
   ▼        ▼
SETUJUI    TOLAK
   │        │
   │        └──────► Status: DITOLAK
   │
   ▼
Cek Stok Buku
   │
   ▼
Stok Tersedia
   │
   ▼
Status: DIPINJAM
   │
   ▼
Stok Tersedia - 1
   │
   ▼
Siswa Mengembalikan Buku
   │
   ▼
Cek Keterlambatan & Kondisi
   │
   ▼
Hitung Denda
   │
   ▼
Status: DIKEMBALIKAN
   │
   ▼
Stok Buku + 1
   │
   ▼
Rating & Ulasan

🗄️ Struktur Database

Aplikasi terhubung ke database MySQL dengan nama database:

perpus_ukk2

Berdasarkan query yang digunakan oleh source code, tabel utama yang digunakan adalah:

user

Menyimpan akun dan data pengguna sistem.

user
├── id
├── id_user
├── nis
├── username
├── password
├── nama
├── level
├── alamat
└── no_telp

Level pengguna:

admin
petugas
siswa

anggota

Digunakan dalam proses peminjaman sebagai data anggota/siswa.

anggota
├── id_anggota
└── id_user

Struktur kolom di atas ditulis berdasarkan kolom yang dipanggil oleh source code. Repository ini tidak menyertakan dump SQL sehingga definisi lengkap tipe data/constraint database perlu disesuaikan dengan database yang digunakan saat deployment.

petugas

Menyimpan data petugas perpustakaan.

petugas
├── id_petugas
├── username
├── password
├── nama_petugas
└── level

buku

Menyimpan katalog dan stok buku.

buku
├── id_buku
├── kode_buku
├── judul
├── pengarang
├── kategori
├── tahun_terbit
├── cover
├── stok_total
├── stok_tersedia
└── rak

peminjaman

Menyimpan seluruh proses peminjaman dan pengembalian.

peminjaman
├── id_peminjaman
├── id_anggota
├── id_buku
├── tgl_pinjam
├── tgl_kembali
├── tgl_dikembalikan
├── status
├── denda
└── kondisi

Status yang digunakan antara lain:

menunggu
dipinjam
ditolak
dikembalikan

ulasan

Menyimpan rating dan komentar siswa terhadap buku.

ulasan
├── id_ulasan
├── id_buku
├── id_user
├── rating
└── komentar

🔗 Relasi Data

Gambaran hubungan data pada aplikasi:

                 ┌──────────────┐
                 │     USER     │
                 └──────┬───────┘
                        │
             ┌──────────┴──────────┐
             │                     │
             ▼                     ▼
       ┌───────────┐          ┌───────────┐
       │  ANGGOTA  │          │  ULASAN   │
       └─────┬─────┘          └─────┬─────┘
             │                      │
             │                      │
             ▼                      ▼
       ┌──────────────┐       ┌───────────┐
       │ PEMINJAMAN   │──────►│   BUKU    │
       └──────────────┘       └───────────┘

                 ┌──────────────┐
                 │   PETUGAS    │
                 └──────────────┘

📁 Struktur Folder

Struktur berikut disesuaikan dengan source code pada repository:

perpusukk2/
│
├── admin/
│   ├── dashboard.php
│   ├── data_buku.php
│   ├── data_petugas.php
│   ├── data_siswa.php
│   ├── edit_buku.php
│   ├── edit_siswa.php
│   ├── hapus_buku.php
│   ├── hapus_siswa.php
│   ├── laporan.php
│   ├── notifikasi.php
│   ├── tambah_buku.php
│   └── tambah_siswa.php
│
├── petugas/
│   ├── dashboard.php
│   ├── data_buku.php
│   ├── data_siswa.php
│   ├── pengembalian.php
│   └── persetujuan.php
│
├── siswa/
│   ├── dashboard.php
│   └── profil.php
│
├── assets/
│   └── cover/
│       ├── cover buku
│       └── ...
│
├── gambar/
│   ├── logo_rpl.png
│   ├── logo_sekolah.png
│   ├── cover buku
│   └── ...
│
├── video/
│   └── vidd.mp4
│
├── cek_login.php
├── daftar.php
├── index.php
├── koneksi.php
├── login.php
└── logout.php

🛠️ Teknologi

Teknologi

Penggunaan

PHP

Backend dan server-side processing

MySQL

Penyimpanan data

HTML5

Struktur halaman

CSS3

Tampilan antarmuka

JavaScript

Interaksi halaman

Bootstrap 5.3.3

Komponen dan layout responsif

Google Fonts

Tipografi antarmuka

XAMPP

Local development

Git & GitHub

Version control dan repository

🚀 Cara Menjalankan di Localhost

1. Clone Repository

git clone https://github.com/Ayu155/perpusukk2.git

Masuk ke folder project:

cd perpusukk2

2. Pindahkan ke XAMPP

Letakkan folder project ke:

C:\xampp\htdocs\perpusukk2

3. Jalankan XAMPP

Aktifkan:

Apache
MySQL

4. Buat Database

Buka:

http://localhost/phpmyadmin

Buat database:

perpus_ukk2

Kemudian buat/import tabel sesuai struktur database yang digunakan oleh aplikasi.

Penting: file source yang tersedia tidak menyertakan file dump .sql, sehingga database harus dibuat dari struktur database yang digunakan pada server/local environment.

5. Konfigurasi Koneksi

File koneksi berada di:

koneksi.php

Konfigurasi default pada source:

$koneksi = mysqli_connect(
    "localhost",
    "root",
    "",
    "perpus_ukk2"
);

Sesuaikan username, password, dan nama database apabila konfigurasi MySQL Anda berbeda.

6. Jalankan Aplikasi

Buka:

http://localhost/perpusukk2/

🔑 Sistem Login

Login menggunakan satu sistem autentikasi dengan pilihan level pengguna.

                  LOGIN
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
        ADMIN     PETUGAS    SISWA
          │         │         │
          ▼         ▼         ▼
       Admin/     Petugas/   Siswa/
       dashboard  dashboard  dashboard

Siswa dapat melakukan login menggunakan:

Username

NIS

Sedangkan sistem menentukan halaman tujuan berdasarkan level akun:

admin   → admin/dashboard.php
petugas → petugas/dashboard.php
siswa   → siswa/dashboard.php

📊 Dashboard

Dashboard admin menyediakan informasi seperti:

Jumlah buku

Jumlah siswa

Jumlah petugas

Jumlah peminjaman aktif

Pengajuan yang menunggu

Peminjaman terbaru

Buku populer

Buku yang terlambat dikembalikan

Stok buku yang menipis

Statistik kategori buku

Statistik peminjaman berdasarkan periode

Rating/kualitas buku

Dashboard petugas menyediakan informasi operasional seperti:

Jumlah buku

Jumlah peminjaman aktif

Jumlah siswa

Jumlah pengajuan yang menunggu

Dashboard siswa menyediakan informasi personal seperti:

Buku yang sedang dipinjam

Pengajuan yang menunggu

Riwayat peminjaman

Buku yang mendekati jatuh tempo

Buku populer

Rating dan ulasan

📖 Pengelolaan Buku

Data buku memiliki informasi:

Kode Buku
Judul
Pengarang
Kategori
Tahun Terbit
Cover
Stok Total
Stok Tersedia
Rak

Admin dan petugas dapat melakukan pengelolaan data buku sesuai hak akses masing-masing.

🔄 Pengembalian & Denda

Saat buku dikembalikan, sistem dapat mencatat:

Tanggal pengembalian

Kondisi buku

Denda keterlambatan

Status pengembalian

Perubahan stok buku

Riwayat peminjaman kemudian dapat ditampilkan kembali pada halaman persetujuan/riwayat dan laporan.

⭐ Rating & Ulasan

Setelah peminjaman selesai, siswa dapat memberikan:

⭐ Rating buku

💬 Komentar/ulasan

Data rating digunakan pada halaman utama dan dashboard untuk menampilkan kualitas serta popularitas buku.

📸 Screenshot

Tambahkan screenshot aplikasi pada folder:

docs/
└── screenshots/
    ├── landing-page.png
    ├── login.png
    ├── dashboard-admin.png
    ├── dashboard-petugas.png
    ├── dashboard-siswa.png
    ├── data-buku.png
    ├── peminjaman.png
    └── laporan.png

Kemudian tampilkan di README dengan format:

![Landing Page](docs/screenshots/landing-page.png)
![Dashboard Admin](docs/screenshots/dashboard-admin.png)
![Dashboard Siswa](docs/screenshots/dashboard-siswa.png)

📌 Status Project

Status: 🟢 Completed / Portfolio Project

Project ini dikembangkan sebagai tugas UKK RPL SMK N 1 Sanden dengan fokus pada pembuatan sistem perpustakaan digital yang memiliki beberapa level pengguna dan alur peminjaman buku.

👩‍💻 Developer

Ayu Rahmawati

🎓 Siswa RPL

🏫 SMK N 1 Sanden

📅 Tahun: 2026

👩‍🏫 Pembimbing: Salsa Bella Putri, S.Kom.

⏱️ Durasi pengerjaan: ± 3 bulan

🏷️ Tags

PHP
MySQL
Perpustakaan
Sistem Informasi
UKK
RPL
SMK
Library Management System
Web Application
Bootstrap

📄 Lisensi

Project ini dibuat untuk keperluan pembelajaran, UKK, dan portfolio.

© 2026 Ayu Rahmawati
