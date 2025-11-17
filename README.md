Our Private Space - Panduan Lengkap Deploy ke GitHub
Panduan ini akan memandu Anda dari awal untuk meng-hosting website "Our Private Space" Anda di GitHub Pages dan memastikannya hanya bisa diakses oleh Anda dan pasangan Anda.
Ikuti langkah-langkah ini dengan urut.
Langkah 1: Persiapan Repositori GitHub
Kita akan siapkan GitHub dulu agar kita mendapatkan URL website-nya.
 * Login ke GitHub.
 * Klik ikon + di pojok kanan atas, pilih "New repository".
 * Repository name: Beri nama, misalnya our-space.
 * PENTING: Pilih "Public".
   * Kenapa? GitHub Pages untuk repositori Private adalah fitur berbayar.
   * Amankah? Ya. Meskipun kode Anda (HTML/CSS/JS) terlihat publik, tidak ada yang bisa login. Kunci rahasia Anda (API Key, dll.) ada di Google Cloud, dan data Anda aman di folder Google Drive pribadi Anda.
 * Klik "Create repository".
 * Setelah repositori dibuat, buka tab "Settings".
 * Di menu samping kiri, klik "Pages".
 * Di bawah "Branch", pilih main (jika tidak ada, lanjutkan ke Langkah 4 dulu, lalu kembali lagi ke sini).
 * Di sebelahnya, biarkan /(root). Klik "Save".
 * GitHub akan menampilkan URL website Anda, seperti:
   https_://NAMA-ANDA.github.io/our-space/
 * Catat URL ini. Kita akan membutuhkannya.
Langkah 2: Konfigurasi Google Cloud (Kunci Keamanan)
Ini adalah bagian terpenting untuk membatasi akses.
 * Buka Google Cloud Console dan buat proyek baru (misal: "Our Space Project").
 * Di menu (☰), buka APIs & Services > Library.
 * Cari dan Enable (Aktifkan) Google Drive API.
 * Sekarang, di menu (☰), buka APIs & Services > Credentials.
A. Buat API Key
 * Klik + CREATE CREDENTIALS > API key.
 * Salin API Key yang muncul. Simpan ini. (Kita sebut: API_KEY)
B. Buat OAuth Consent Screen (Di sinilah "Mode Testing" diatur)
 * Buka tab OAuth consent screen.
 * Pilih External dan klik Create.
 * App name: Beri nama (misal: "Our Private Space").
 * User support email: Pilih email Anda.
 * Developer contact information: Masukkan email Anda lagi.
 * Klik SAVE AND CONTINUE.
 * Halaman "Scopes": Lewati saja, klik SAVE AND CONTINUE.
 * Halaman "Test users": INI YANG PENTING!
   * Biarkan "Publishing status" sebagai "Testing". JANGAN DIUBAH KE "PRODUCTION".
   * Klik + ADD USERS.
   * Masukkan alamat email Google Anda.
   * Klik + ADD USERS lagi.
   * Masukkan alamat email Google Anda.
   * Klik SAVE AND CONTINUE.
 * Anda akan kembali ke Dashboard. Ini sudah selesai. Aplikasi Anda sekarang terkunci hanya untuk 2 email tersebut.
C. Buat OAuth Client ID
 * Kembali ke tab Credentials.
 * Klik + CREATE CREDENTIALS > OAuth client ID.
 * Application type: Pilih Web application.
 * Name: Beri nama (misal: "GitHub Web Client").
 * DI BAWAH "Authorized JavaScript origins" (SANGAT PENTING):
   * Klik + ADD URI.
   * Masukkan URL origin dari Langkah 1. (Contoh: https_://NAMA-ANDA.github.io - tanpa /our-space/ di belakangnya).
   * Klik + ADD URI lagi untuk pengetesan lokal (opsional tapi disarankan):
     * http://localhost:5500
     * http://127.0.0.1:5500
 * Klik CREATE.
 * Google akan menampilkan Your Client ID. Salin ini. Simpan ini. (Kita sebut: CLIENT_ID)
Langkah 3: Konfigurasi Folder Google Drive
 * Buka Google Drive.
 * Buat folder baru (misal: "Our Memories").
 * Klik kanan pada folder itu > Share > Share.
 * Bagikan folder ini dengan email pasangan Anda (beri akses Editor).
 * Buka folder tersebut. Lihat URL di browser Anda:
   drive.google.com/drive/folders/1aBcDeFgHiJkLmNoPqRsTuVwXyZ_12345
 * Salin ID unik di akhir URL. Simpan ini. (Kita sebut: FOLDER_ID)
Langkah 4: Edit dan Unggah Kode ke GitHub
 * Buka file index.html yang saya berikan di text editor.
 * Cari bagian CONFIG di dalam tag <script>:
   // --- KONFIGURASI (WAJIB DIISI!) ---
const CONFIG = {
    CLIENT_ID: "", // <-- PASTE CLIENT_ID ANDA DI SINI
    API_KEY: "",     // <-- PASTE API_KEY ANDA DI SINI
    FOLDER_ID: ""    // <-- PASTE FOLDER_ID ANDA DI SINI
};
// ------------------------------------

 * Isi ketiga nilai tersebut dengan yang sudah Anda simpan.
 * Simpan file index.html.
 * Kembali ke halaman repositori GitHub Anda.
 * Klik Add file > Upload files.
 * Tarik (drag) file index.html yang sudah Anda edit ke area unggah.
 * Klik Commit changes.
Langkah 5: Selesai!
Tunggu 1-2 menit hingga GitHub Pages selesai mem-publish.
Sekarang, buka URL website Anda (https_://NAMA-ANDA.github.io/our-space/).
Hasil Akhir:
 * Website Anda live dan bisa diakses dari mana saja.
 * Saat Anda atau pasangan Anda mengklik "Login", prosesnya akan berhasil.
 * Jika orang lain (dengan email yang tidak terdaftar) mencoba mengklik "Login", mereka akan melihat halaman error dari Google yang mengatakan "Access blocked: This app is in testing mode...".
Anda telah berhasil membuat website galeri pribadi yang aman.
