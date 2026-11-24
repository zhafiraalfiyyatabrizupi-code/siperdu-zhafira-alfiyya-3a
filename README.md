# SiPerdu – Sistem Perpustakaan Terpadu (Template Praktikum Pertemuan 13)

Template proyek praktikum **Pemrograman Internet** menggunakan **Laravel 12**.
Repository ini berisi kondisi akhir **Pertemuan 12 (CRUD Data Buku pada POV Admin)** dan menjadi titik awal untuk **Pertemuan 13 (Authentication dengan Laravel Breeze serta Role User & Admin)**.

Pada kondisi ini semua halaman sudah membaca database, tetapi **belum ada login**. Siapa pun yang mengetik alamat `/admin/dashboard` dapat masuk ke halaman admin dan menghapus buku. Masalah inilah yang diselesaikan pada Pertemuan 13.

## Isi Template

| Bagian | Isi |
| --- | --- |
| Routing | `routes/web.php`: halaman user, dashboard admin, dan `Route::resource('buku')` |
| Controller | `HomeController`, `Admin/DashboardController`, `Admin/BukuController` (CRUD lengkap + validasi) |
| Model | `Kategori` (hasMany Buku), `Buku` (belongsTo Kategori), `User` (bawaan Laravel) |
| Database | Migration `kategori` dan `buku`, `KategoriSeeder`, `BukuSeeder`, `BukuFactory` |
| Layout Blade | `layout/user.blade.php`, `layout/admin.blade.php`, `layout/sidebar-admin.blade.php` |
| View User | `user/home.blade.php`, `user/buku/katalog.blade.php` (membaca database) |
| View Admin | `admin/dashboard.blade.php`, `admin/data-buku.blade.php`, `admin/buku/*` (create, edit, show, _form) |
| Aset | `public/assetsUser` (template Eduleb) dan `public/assetsAdmin` (Spark Admin) |

| URL | Halaman | Status saat ini |
| --- | --- | --- |
| `/` | Home (POV user) | Terbuka untuk umum |
| `/katalog-buku` | Katalog Buku (POV user) | Terbuka untuk umum |
| `/admin/dashboard` | Dashboard (POV admin) | **Masih terbuka untuk umum** |
| `/admin/buku` | Data Buku + CRUD (POV admin) | **Masih terbuka untuk umum** |

## Kebutuhan

- XAMPP (Apache + MySQL)
- PHP **8.2 atau lebih baru** (lihat catatan versi PHP di bawah)
- Composer
- **Node.js 18 atau lebih baru beserta npm** (baru dipakai pada Pertemuan 13 untuk membangun tampilan Laravel Breeze). Cek dengan `node -v` dan `npm -v`.
- Git dan VS Code

## Cara Memakai Template

1. Klik tombol hijau **Use this template → Create a new repository** di halaman GitHub ini.
2. Beri nama repository kalian, misalnya `perpustakaan-auth-nim`, lalu klik **Create repository**.
3. Clone repository kalian ke folder `htdocs`:

   ```bash
   cd C:\xampp\htdocs
   git clone https://github.com/<username>/<nama-repo>.git perpustakaan
   cd perpustakaan
   ```

4. Pasang dependency dan siapkan file `.env`:

   ```bash
   composer install
   copy .env.example .env
   php artisan key:generate
   ```

5. Nyalakan **MySQL** di XAMPP. Bagian database di `.env` sudah diisi untuk XAMPP bawaan:

   ```env
   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=perpustakaan
   DB_USERNAME=root
   DB_PASSWORD=
   ```

6. Buat ulang semua tabel lalu isi data contoh (ketik `yes` jika ditanya membuat database):

   ```bash
   php artisan migrate:fresh --seed
   ```

7. Jalankan server:

   ```bash
   php artisan serve
   ```

8. Buka `http://127.0.0.1:8000`.

> Pengguna macOS/Linux: ganti `copy .env.example .env` dengan `cp .env.example .env`.

## Catatan Versi PHP

Jika `composer install` menampilkan error seperti *"requires php >=8.4.1"*, jalankan `composer update`. Composer akan memilih versi paket yang cocok dengan PHP kalian (Laravel 12 mendukung PHP 8.2 ke atas). Cek versi PHP dengan `php -v`.

Jika `php artisan serve` gagal dengan pesan *Failed to listen on 127.0.0.1:8000 (reason: ?)*, jalankan `php artisan serve --no-reload`.

## Catatan Front-End

SiPerdu memakai Bootstrap dari folder `public/assetsUser` dan `public/assetsAdmin`, sehingga Tailwind bawaan skeleton Laravel 12 sudah dihapus dari `package.json` dan `vite.config.js`. Pada Pertemuan 13, Laravel Breeze akan memasang Tailwind versinya sendiri khusus untuk halaman login, register, dan profil.

## Masalah yang Sering Terjadi

| Gejala | Solusi |
| --- | --- |
| `vendor/autoload.php` not found | Jalankan `composer install` |
| No application encryption key | Jalankan `php artisan key:generate` |
| Connection refused | Nyalakan MySQL di XAMPP |
| Tabel tidak muncul di phpMyAdmin | Pastikan `DB_CONNECTION=mysql`, lalu `php artisan config:clear` |
| Data buku kosong | Jalankan `php artisan migrate:fresh --seed` |
| Perubahan `.env` tidak terbaca | Jalankan `php artisan config:clear` |

## Alur Pertemuan

| Pertemuan | Materi | Status |
| --- | --- | --- |
| 10 | Laravel Fundamental: struktur folder, routing, controller, Blade, layouting | Selesai |
| 11 | MVC, Migration, Seeder & Factory, Model & Eloquent, koneksi `.env` | Selesai |
| 12 | CRUD Data Buku pada POV Admin: form, validasi, simpan, ubah, hapus | Isi template ini |
| 13 | Authentication dengan Laravel Breeze, Role User & Admin, Middleware | Dikerjakan saat live coding |

---

Modul Praktikum Pemrograman Internet · Pendidikan Sistem dan Teknologi Informasi · UPI Kampus Purwakarta
