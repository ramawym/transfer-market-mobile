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
