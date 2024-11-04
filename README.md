    Nama       : Afiftha Ravi Aufa

    NIM        : H1D022095

    Shift Baru : A

 # Penjelasan Cara Kerja Login pada Ionic menggunakan API Native PHP

### Setup Koneksi Database
Buat file `koneksi.php` untuk mengatur sambungan ke database MySQL, yang di dalamnya terdapat tabel `user` dengan kolom `username` dan `password`.

### Penerimaan dan Pengolahan Data Login
Pada file `login.php`, data yang diterima dari permintaan login berupa `username` dan `password` dalam format JSON. Password yang diterima kemudian di-hash menggunakan MD5 dan dibandingkan dengan data yang ada di database.

### Validasi Login pada API
Jika `username` dan `password` yang dikirim cocok dengan data di database, API akan memberikan respons JSON dengan `status_login` berisi "berhasil", bersama dengan `username` dan token unik. Jika data tidak cocok, API akan mengembalikan `status_login` sebagai "gagal".

### Mengirim Permintaan Login dari Ionic
Di halaman login, ketika pengguna menekan tombol login, data `username` dan `password` akan dikirim ke API `login.php` menggunakan metode post dalam `authentication.service.ts`.

### Penyimpanan Informasi Login
Jika API merespons dengan `status_login` "berhasil", maka `AuthenticationService` menyimpan token dan `username` ke dalam penyimpanan lokal (preferences) untuk menandai status autentikasi. Nilai `isAuthenticated` akan diubah menjadi `true`, menunjukkan bahwa pengguna berhasil login.

### Pengalihan ke Halaman Utama
Setelah login berhasil, pengguna akan secara otomatis diarahkan ke halaman utama.

### Guard untuk Mengamankan Rute
Guard `authGuard` memeriksa status login (`isAuthenticated`) saat pengguna mencoba mengakses halaman yang membutuhkan autentikasi, seperti halaman utama. Jika pengguna belum login, `authGuard` akan mengarahkan mereka kembali ke halaman login.

### Guard Auto-login
Guard `autoLoginGuard` mencegah pengguna yang sudah login untuk kembali ke halaman login. Jika pengguna yang telah login mencoba mengakses halaman login, `autoLoginGuard` akan langsung mengarahkan mereka ke halaman utama.

### Logout
Saat logout, `AuthenticationService` menghapus data token dan `username` dari penyimpanan lokal serta mengubah nilai `isAuthenticated` menjadi `false`. 

---

<div align="center">
  <img src="src/assets/1.png" style="width: 27%;">
&nbsp;&nbsp;&nbsp;&nbsp&nbsp;&nbsp;&nbsp;&nbsp&nbsp;&nbsp;&nbsp;&nbsp;
  <img src="src/assets/2.png" style="width: 27%;">
</div>
