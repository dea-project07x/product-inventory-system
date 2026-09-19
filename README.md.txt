# Laporan Mini Project 1 & Evaluasi - Pemrograman Web

## Mini Project 1: Product Information System (Desain Arsitektur)

### 1. Data Layer (`products.php`)
* **Peran:** Bertindak sebagai tempat penyimpanan data (*data source*) berbasis *multidimensional associative array*.
* **Komponen Atribut:** Menyimpan atribut produk lengkap meliputi ID, Nama, Kategori, Harga, Stok, dan Deskripsi.
* **Konsep Rencana:** Menyimpan data produk dalam struktur array berderet yang siap dipanggil oleh fungsi pengolahan data.

### 2. Processing Layer (`functions.php`)
* **Peran:** Menampung seluruh logika bisnis (*business logic*) dan pengolahan data.
* **Fungsi Utama:**
  * `hitungTotalNilaiStok()`: Mengkalkulasi total aset gudang berdasarkan perkalian harga dan stok tiap produk.
  * **Logika Conditional Warna:** Memeriksa stok produk. Jika stok di bawah 3 (< 3), fungsi akan mengembalikan penanda khusus (class CSS) untuk mewarnai baris tabel menjadi merah/kritis.

### 3. Presentation Layer (`index.php`)
* **Peran:** Menampilkan antarmuka pengguna (UI) berbasis tabel HTML.
* **Alur Kerja:**
  * Memuat file `products.php` dan `functions.php` menggunakan perintah `require_once`.
  * Merender data ke dalam layout tabel HTML menggunakan perulangan `foreach`.

---

## Pertanyaan Evaluatif / Sesi Diskusi Kelas

### 1. Mengapa *associative array* jauh lebih representatif dan aman dibanding *indexed array*?
* **Keterbacaan:** *Associative array* menggunakan kunci bernama (seperti `'harga'`, `'stok'`) yang jelas menggambarkan atribut data, sedangkan *indexed array* hanya menggunakan angka (`[0]`, `[1]`) yang abstrak.
* **Keamanan Data:** Jika posisi urutan data berubah, *indexed array* rentan salah panggil. *Associative array* jauh lebih aman dan stabil karena data diakses spesifik melalui nama kuncinya.

### 2. Konsekuensi fatal penggunaan `include` dibanding `require` untuk file koneksi database vendor:
* `include` hanya menghasilkan *Warning* saat file tidak ditemukan dan tetap melanjutkan eksekusi program. Akibatnya, query database akan dipaksa berjalan tanpa koneksi yang menyebabkan kebocoran error (*stack trace*) ke layar pengguna.
* `require` langsung menghasilkan *Fatal Error* dan menghentikan program seketika, sehingga mencegah kebocoran data dan eksekusi kode yang rusak.

### 3. Mengapa *logic error* memakan durasi pencarian lebih lama dibanding *syntax error*?
* **Syntax Error:** Langsung dideteksi oleh interpreter PHP beserta nomor baris tempat kesalahannya.
* **Logic Error:** Program tetap berjalan tanpa pesan error sama sekali, namun output yang dihasilkan salah. Pengembang harus menelusuri logika data baris demi baris secara manual untuk menemukan letak kekeliruannya.

### 4. Bahaya *nesting* multidimensional array yang terlalu dalam dari sudut pandang optimasi memori:
* **Overhead Memori:** Semakin dalam tingkatan bersarang (*nesting*), alokasi memori server untuk struktur array (*hashtable*) akan melonjak drastis.
* **Penurunan Performa:** Perulangan bersarang (*nested loop*) memerlukan waktu proses CPU yang sangat tinggi, yang berpotensi menyebabkan aplikasi lambat atau memicu error *Memory Limit Exceeded*.