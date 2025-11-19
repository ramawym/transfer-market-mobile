# transfer_market

## Tugas 7

### Apa itu widget tree pada Flutter dan bagaimana hubungan parent-child bekerja?
Widget tree adalah struktur hierarkis dari semua widget yang membangun UI aplikasi Flutter. Mirip pohon silsilah, dimulai dari satu widget  root. Hubungan parent-child adalah inti dari pohon ini, di mana widget induk (seperti Column atau Row) bertanggung jawab untuk menampung, memposisikan, dan mengonfigurasi widget anak yang ada di dalamnya. Seluruh tata letak dan tampilan aplikasi ditentukan oleh bagaimana widget-widget ini bersarang satu sama lain dalam pohon tersebut.

### Widget yang digunakan dalam proyek ini dan fungsinya
Proyek ini menggunakan MaterialApp sebagai widget akar untuk tema dan navigasi, serta Scaffold yang menyediakan struktur halaman dengan AppBar dan body berisi konten. Tata letak diatur menggunakan Column (menyusun vertikal), Row (menyusun info NPM/Nama secara horizontal), dan GridView (menampilkan tombol menu), dengan bantuan Padding dan SizedBox untuk memberi spasi. Widget utama untuk tampilan adalah Card (untuk membungkus info), Text, dan Icon. Tombol menu kustom (ItemCard) dibuat dari Material (untuk warna dan bentuk) dan InkWell (untuk efek klik), yang kemudian memicu ScaffoldMessenger untuk menampilkan SnackBar (notifikasi pop-up).

### Fungsi widget `MaterialApp` dan mengapa sering digunakan sebagai widget root?
MaterialApp adalah widget inti yang membungkus seluruh aplikasi dan menyediakan fungsionalitas dasar berstandar Material Design. Fungsi utamanya adalah untuk mengonfigurasi tema global aplikasi (seperti colorScheme), mengelola tumpukan navigasi (routes) sehingga Anda bisa berpindah antar halaman, dan menentukan widget home (halaman pertama yang ditampilkan). Ia wajib digunakan sebagai widget root karena menyediakan "konteks" dan layanan fundamental (seperti pewarisan tema) yang dibutuhkan oleh widget-widget Material Design lain di bawahnya, seperti Scaffold dan Card, agar dapat berfungsi dengan benar.

### Perbedaan `StatelessWidget` dan `StatefulWidget`. Kapan penggunaannya?
Perbedaan utamanya terletak pada pengelolaan "state" atau data internal. StatelessWidget bersifat immutable (statis); UI-nya digambar hanya sekali berdasarkan data awal dan tidak akan pernah berubah. Ini cocok untuk tampilan seperti ikon, label, atau halaman info statis. Sebaliknya, StatefulWidget bersifat mutable (dinamis) dan memiliki objek State internal yang dapat menyimpan data yang berubah seiring waktu. Ketika data tersebut perlu diubah (misalnya karena input pengguna), Anda memanggil setState(), yang memicu widget tersebut untuk membangun ulang (rebuild) UI-nya dengan data baru, sehingga cocok untuk form, checkbox, atau data yang di-fetch dari internet.

### Apa itu `BuildContext` dan mengapa penting di Flutter? Bagaimana penggunaannya di metode build?
BuildContext adalah sebuah objek yang merepresentasikan "lokasi" atau "alamat" unik sebuah widget di dalam widget tree. Ia sangat penting karena berfungsi sebagai penghubung antara widget dan lingkungannya (terutama para leluhurnya atau ancestors). Dalam metode build, context yang diterima sebagai parameter digunakan untuk berinteraksi dengan pohon; contohnya, Theme.of(context) menggunakan context untuk "naik" ke atas pohon mencari data Theme terdekat, atau ScaffoldMessenger.of(context) menggunakannya untuk menemukan Scaffold terdekat guna menampilkan SnackBar.
 
### Konsep "hot reload" di Flutter dan bagaimana bedanya dengan "hot restart"
Hot Reload adalah fitur pengembangan super cepat yang menyuntikkan file kode baru ke dalam Dart Virtual Machine (VM) yang sedang berjalan, memungkinkan developer melihat perubahan UI secara instan (biasanya di bawah satu detik) tanpa kehilangan state aplikasi (misalnya, data yang sedang diketik di form tetap ada). Sebaliknya, Hot Restart akan memuat ulang kode aplikasi, namun ia menghancurkan state aplikasi dan memulai ulang aplikasi dari awal (mirip seperti menutup dan membuka aplikasi lagi, namun jauh lebih cepat daripada full restart). Hot Restart digunakan ketika perubahan kode terlalu fundamental untuk ditangani Hot Reload, seperti mengubah state global atau struktur main().

## Tugas 8

### Jelaskan perbedaan antara Navigator.push() dan Navigator.pushReplacement() pada Flutter. Dalam kasus apa sebaiknya masing-masing digunakan pada aplikasi Football Shop kamu?
- Navigator.push() menambahkan halaman baru ke atas tumpukan navigasi, sehingga pengguna dapat kembali ke halaman sebelumnya dengan tombol back. 
- Navigator.pushReplacement() mengganti halaman saat ini dengan halaman baru, menghapus halaman sebelumnya dari tumpukan, sehingga pengguna tidak dapat kembali. 

Pada aplikasi Transfer Market, Navigator.push() digunakan untuk navigasi ke halaman tambah produk dari halaman utama, karena pengguna mungkin ingin kembali setelah menambah produk. Navigator.pushReplacement() bisa digunakan saat login/logout untuk mencegah kembali ke halaman login setelah berhasil masuk.

### Bagaimana kamu memanfaatkan hierarchy widget seperti Scaffold, AppBar, dan Drawer untuk membangun struktur halaman yang konsisten di seluruh aplikasi?
Scaffold menyediakan struktur dasar halaman dengan AppBar di atas dan body di tengah, serta drawer untuk navigasi. AppBar menampilkan judul halaman dengan warna konsisten dari tema aplikasi. Drawer berisi menu navigasi yang dapat diakses dari semua halaman, memungkinkan perpindahan antar halaman utama dan tambah produk. Hierarki ini memastikan konsistensi visual dan fungsionalitas di seluruh aplikasi, dengan tema warna yang diwariskan dari MaterialApp.

### Dalam konteks desain antarmuka, apa kelebihan menggunakan layout widget seperti Padding, SingleChildScrollView, dan ListView saat menampilkan elemen-elemen form? Berikan contoh penggunaannya dari aplikasi kamu.
Padding memberikan ruang di sekitar elemen untuk menghindari tampilan yang terlalu padat dan meningkatkan readability. SingleChildScrollView memungkinkan konten form dapat di-scroll jika melebihi tinggi layar, mencegah overflow dan memastikan semua elemen dapat diakses. ListView berguna untuk daftar elemen dinamis, namun pada form statis, Column dengan Padding sudah cukup. Pada halaman tambah produk, SingleChildScrollView membungkus Column form untuk scrollability, Padding digunakan di sekitar form dan antar elemen untuk spacing yang baik.

### Bagaimana kamu menyesuaikan warna tema agar aplikasi konsisten dengan brand toko?
Tema aplikasi disesuaikan melalui ThemeData di MaterialApp dengan colorScheme yang menggunakan primarySwatch Colors.blueGrey dan secondary Colors.blueAccent[400]. Warna ini konsisten dengan AppBar dan Drawer. ItemCard menggunakan warna spesifik per item (biru, hijau, merah).

## Tugas 9

### Mengapa kita perlu membuat model Dart saat mengambil/mengirim data JSON? Apa konsekuensinya jika langsung memetakan Map<String, dynamic> tanpa model (terkait validasi tipe, null-safety, maintainability)?
Kita perlu membuat Model Dart (seperti ProductEntry yang kita gunakan) untuk merepresentasikan struktur data JSON yang diterima dari atau dikirim ke endpoint Django. Model ini berfungsi sebagai kontrak atau skema yang menentukan nama, tipe data, dan hubungan antar field dalam data tersebut.

Jika kita langsung memetakan Map<String, dynamic> tanpa model, konsekuensinya adalah:

Validasi Tipe dan Null-Safety:
- Kehilangan Keamanan Tipe (Type Safety): Kita harus secara manual melakukan casting untuk setiap nilai (json['price'] as int?), yang rentan terhadap runtime error (misalnya, jika Django mengirimkan harga sebagai string tetapi Dart mengharapkannya int).
- Null-Safety: Dart tidak akan mengetahui secara pasti field mana yang opsional (nullable) dan mana yang wajib. Kita harus menggunakan operator null-assertion (!) atau null-aware (?) secara berlebihan, yang meningkatkan risiko crash jika kita mengakses data yang sebenarnya null.

Maintainability (Keterawatan):
- Perubahan Data Sulit Dilacak: Jika struktur JSON di Django berubah (misalnya, name menjadi product_name), kita harus mencari dan mengubah setiap widget atau business logic yang menggunakan key tersebut, menyebabkan kode menjadi sulit dipertahankan (hard to maintain).
- Kode Berulang (Boilerplate): Proses casting dan pengecekan null harus diulang di banyak tempat, membuat kode panjang dan tidak efisien.
- Intellisense/Code Completion Buruk: Tanpa model, IDE tidak dapat memberikan saran otomatis untuk nama field, memperlambat proses pengembangan.

### Apa fungsi package http dan CookieRequest dalam tugas ini?
Package http:
- Ini adalah paket dasar yang digunakan Flutter untuk membuat request HTTP (GET, POST, PUT, DELETE). Paket ini menangani koneksi jaringan tingkat rendah, pengiriman request, dan penerimaan response.

Package CookieRequest:
- Ini adalah wrapper yang dibuat di atas paket http. Fungsi utamanya adalah manajemen session dan cookies. Dalam konteks otentikasi, CookieRequest secara otomatis menangani pengiriman dan penyimpanan cookies otentikasi (misalnya sessionid dan csrftoken) antara request login, request data, dan request logout.

### Jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
Instance CookieRequest perlu dibagikan ke semua komponen (biasanya melalui Provider seperti yang kita lakukan dengan context.watch<CookieRequest>()) karena:
- Otentikasi Global: Hanya satu instance CookieRequest yang menyimpan status otentikasi pengguna (cookies otentikasi dan CSRF token).
- State Management: Ketika pengguna berhasil login, instance CookieRequest diperbarui dengan cookie session baru. Komponen lain (seperti halaman daftar produk, form tambah produk) harus menggunakan instance yang sama ini untuk memastikan request mereka terotentikasi dan Django tahu siapa yang mengirim data.
- Keterpeliharaan: Dengan membagikannya, Anda menghindari passing instance ini melalui setiap konstruktor widget secara manual.

### Jelaskan konfigurasi konektivitas yang diperlukan agar Flutter dapat berkomunikasi dengan Django. Mengapa kita perlu menambahkan 10.0.2.2 pada ALLOWED_HOSTS, mengaktifkan CORS dan pengaturan SameSite/cookie, dan menambahkan izin akses internet di Android? Apa yang akan terjadi jika konfigurasi tersebut tidak dilakukan dengan benar?
Konektivitas lokal memerlukan beberapa konfigurasi penting. Kita perlu menambahkan 10.0.2.2 pada ALLOWED_HOSTS di Django karena emulator Android menggunakan alamat ini sebagai alias untuk localhost PC host, sehingga Django perlu mengizinkan koneksi dari alamat tersebut. CORS (Cross-Origin Resource Sharing) harus diaktifkan agar Django mengizinkan client Flutter, yang dianggap memiliki origin berbeda, untuk mengambil sumber daya. Pengaturan SameSite/cookie harus disesuaikan (SAMESITE='Lax') agar cookies otentikasi dapat berhasil dikirim melintasi origin berbeda. Terakhir, izin akses internet harus ditambahkan ke AndroidManifest.xml agar aplikasi Android diizinkan melakukan operasi jaringan. Jika konfigurasi ini gagal, kita akan menghadapi kegagalan koneksi (400 Bad Request), pemblokiran response karena batasan origin, atau kegagalan otentikasi cookie dan CSRF check.

### Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.
Mekanisme pengiriman data dimulai ketika pengguna mengisi formulir di ProductFormPage dan data diekstrak dari TextFormField Controllers. Data ini kemudian dikemas dalam format JSON dan dikirimkan melalui request POST oleh CookieRequest ke endpoint Django /create-flutter/. Django, dalam fungsi create_product_flutter, mengurai JSON tersebut, membuat objek Product baru di database, dan mengembalikan response sukses. Setelah sukses, Flutter menavigasi ke halaman daftar (ProductListPage), yang kemudian memicu widget FutureBuilder untuk memanggil endpoint JSON (/json/). Django mengambil semua data Product dan menserialisasikannya menjadi JSON, yang kemudian diterima oleh Flutter, di-deserialisasi menjadi list ProductEntry, dan ditampilkan sebagai daftar ProductCard di layar.

### Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
Mekanisme autentikasi sepenuhnya mengandalkan instance CookieRequest yang dibagikan secara global. Proses dimulai dari Registrasi dengan mengirimkan kredensial ke /auth/register/. Setelah berhasil, pengguna beralih ke halaman Login, di mana CookieRequest mengirimkan request login ke Django. Jika kredensial valid, Django mengembalikan cookies otentikasi (sessionid, csrftoken), yang secara otomatis disimpan oleh CookieRequest, menetapkan request.loggedIn menjadi True, dan mengarahkan ke menu utama (MyHomePage). Sejak saat itu, cookies yang tersimpan digunakan pada setiap request data baru (seperti fetch data produk) untuk memverifikasi identitas pengguna. Proses Logout melibatkan CookieRequest yang mengirimkan request ke /auth/logout/, menghapus cookies yang tersimpan, dan mengakhiri session, mengembalikan pengguna ke halaman Login.

### Implementasi Checklist Secara Step-by-Step

1. Persiapan Django & Konektivitas:
- Memastikan Django sudah di-deploy secara lokal (python manage.py runserver).
- Mengimplementasikan model Product di models.py dengan field yang sesuai (name, price, description, rating, category, is_featured) dan kategori merchandise.
- Mengaktifkan endpoint JSON di urls.py dan views.py (/json/) untuk mengekspor semua data Product.
- Mengatur konektivitas (menambahkan 10.0.2.2 ke ALLOWED_HOSTS, mengatur CORS, dan izin internet di Flutter) untuk komunikasi emulator-Django.

2. Sistem Autentikasi (Django & Flutter):
- Mengimplementasikan fungsi register, login_user, dan logout_user di Django views.py.
- Mengintegrasikan paket pbp_django_auth (CookieRequest) ke dalam proyek Flutter dan membagikannya menggunakan Provider (di root aplikasi).
- Membuat RegisterPage dan LoginPage di Flutter, yang menggunakan CookieRequest.postJson dan CookieRequest.login untuk berinteraksi dengan endpoint autentikasi Django.
- Memastikan navigasi setelah login berhasil mengarahkan ke MyHomePage.

3. Menampilkan Daftar Item (List Item):
- Membuat ProductEntry model Dart (products_entry.dart) untuk deserialization data JSON.
- Membuat ProductCard widget untuk tampilan setiap item.
- Membuat ProductListPage (halaman daftar) yang menggunakan FutureBuilder untuk memanggil fetchProducts.
- fetchProducts melakukan request GET ke /json/ menggunakan CookieRequest dan memetakan hasilnya ke daftar ProductEntry.

4. Halaman Detail Item:
- Membuat ProductDetailPage yang menerima objek ProductEntry sebagai argumen.
- Menambahkan widget untuk menampilkan seluruh atribut (name, price, description, rating, dll.) dari objek ProductEntry tersebut.
- Menambahkan logika Navigator.push pada ProductCard.onTap di ProductListPage untuk berpindah ke halaman detail.

5. Fitur Tambahan dan Filter:
- Filter Item Pengguna: Mengubah fetchProducts di ProductListPage untuk memfilter data berdasarkan parameter (misalnya /json/?filter=my_items) dan menggunakan logika Django Product.objects.filter(user=request.user) di show_json_products untuk hanya menampilkan item milik pengguna yang sedang login. (Dalam implementasi yang kita lihat, filter ini diterapkan di show_main, tetapi logika serupa harus diterapkan di endpoint JSON jika diperlukan).
- Membuat ProductFormPage untuk mengirim data baru ke Django melalui endpoint /create-flutter/.