# Tugas 7

---

## 1. Jelaskan apa itu widget tree pada Flutter dan bagaimana hubungan parent-child (induk-anak) bekerja antar widget.
Widget Tree (Pohon Widget) adalah representasi hirarkis dari antarmuka pengguna (UI) aplikasi Flutter Anda. Setiap elemen visual yang Anda lihat di layar (teks, tombol, layout, dll.) adalah sebuah Widget, dan widget-widget ini tersusun seperti struktur pohon.
- Hubungan Parent-Child (Induk-Anak): Hubungan ini menentukan layout dan konfigurasi. Parent (Induk)adalah ebuah widget yang menampung atau mengelola widget lain. Induk menentukan batasan (constraints) ukuran dan posisi bagi anak-anaknya. Contoh: Column adalah induk bagi Row dan SizedBox.
- Child (Anak): Widget yang ditempatkan di dalam widget lain. Anak menerima batasan dari induknya dan bertanggung jawab untuk menentukan ukuran yang diinginkannya. Contoh: Text adalah anak dari AppBar

## 2. Sebutkan semua widget yang kamu gunakan dalam proyek ini dan jelaskan fungsinya.
- MaterialApp: Widget root (akar) yang menyediakan struktur dasar aplikasi mengikuti desain Material Design (tema, navigasi, dll.).
- StatelessWidget: Kelas dasar untuk widget yang tampilannya statis (tidak berubah) setelah dibangun.
- Scaffold: Menyediakan kerangka layout dasar halaman, mencakup area-area seperti `AppBar`, `body`, dan `FloatingActionButton`.
- AppBar: Menampilkan bilah judul di bagian atas halaman.
- Padding: Memberikan ruang kosong (padding) di sekeliling child widget.
- SingleChildScrollView: Membuat konten di dalamnya dapat digulir secara vertikal (scrollable), mencegah overflow jika konten melebihi ukuran layar.
- Column: Menyusun child widget secara vertikal dalam urutan linier.
- Row: Menyusun child widget secara horizontal dalam urutan linier.
- SizedBox: Menciptakan jarak kosong (spasi) vertikal atau horizontal dengan ukuran tetap.
- Center: Memposisikan child widget tepat di tengah ruang yang tersedia.
- GridView.count: Menyusun child widget dalam bentuk grid 2 dimensi dengan jumlah kolom (crossAxisCount) yang sudah ditentukan.
- Card: Menampilkan informasi dalam bentuk kotak dengan elevasi (bayangan) dan sudut membulat, digunakan untuk `InfoCard`.
- Material: Widget yang memberikan Material Design ink (efek klik visual) dan bentuk dasar, digunakan untuk `ItemCard`.

## 3. Apa fungsi dari widget MaterialApp? Jelaskan mengapa widget ini sering digunakan sebagai widget root.
- Navigasi: Menyediakan sistem navigasi (`Navigator`) untuk berpindah antar layar.
- Theming: Mendefinisikan tema aplikasi (font, warna dasar, colorScheme, dll.) yang akan diwariskan oleh semua widget di bawahnya.
- Struktur: Menyediakan widget tingkat tinggi seperti Banner (debug), lokalitas (localization), dan routing.

Tanpa `MaterialApp`, widget yang bergantung pada Material Design (seperti `Scaffold`, `AppBar`, `Card`, dll.) tidak akan berfungsi dengan benar atau akan terlihat sangat basic.

## 4. Jelaskan perbedaan antara StatelessWidget dan StatefulWidget. Kapan kamu memilih salah satunya?
- StatelessWidget adalah widget yang tidak berubah (immutable). Tampilannya hanya bergantung pada data yang diterima saat dibuat. StatelessWidget digunakan untuk elemen statis seperti ikon, teks judul, atau layout yang tidak bereaksi terhadap interaksi pengguna.
- StatefulWidget adalah widget yang dapat berubah (mutable). Tampilannya dapat diperbarui secara dinamis. StatefulWidget digunakan untuk elemen interaktif yang perlu menyimpan dan mengubah data, seperti form input, tombol counter, checkbox, atau animasi.

## 5. Apa itu BuildContext dan mengapa penting di Flutter? Bagaimana penggunaannya di metode build?
`BuildContext` adalah pegangan (handle) atau referensi ke lokasi widget di dalam Widget Tree. `BuildContext` penting karena:
- Ia memungkinkan Flutter mengetahui di mana widget berada dalam hierarki, yang sangat penting untuk layout.
- Melalui `BuildContext`, widget dapat mengakses informasi dan layanan dari widget yang lebih tinggi di tree.

Pneggunaannya di metode build: setiap method build (baik di StatelessWidget maupun StatefulWidget) wajib menerima `BuildContext` context sebagai argumennya. Contoh:

        @override
        Widget build(BuildContext context) {
            // ...
            // Menggunakan BuildContext untuk mengakses tema:
            backgroundColor: Theme.of(context).colorScheme.primary,
            // ...
        }

## 6. Jelaskan konsep "hot reload" di Flutter dan bagaimana bedanya dengan "hot restart".
Keduanya adalah fitur dalam flutter untuk melihat perubahan kode dengan cepat. "Hot reload" mempertahankan state (keadaan) aplikasi saat ini. Contoh: Jika kita berada di halaman ke-5, halaman tersebut tetap terbuka. Yang membedakan dengan "hot restart" adalah "hot restart" mereset semua state ke kondisi awal. Aplikasi selalu kembali ke layar pertama.

## 7. Jelaskan bagaimana kamu menambahkan navigasi untuk berpindah antar layar di aplikasi Flutter.
Untuk berpindah antar layar, Flutter menggunakan konsep Stack-based Navigation yang dikelola oleh Navigator. Layar baru "didukung" ke atas tumpukan layar yang sudah ada.

# Tugas 8

---

## 1. Jelaskan perbedaan antara Navigator.push() dan Navigator.pushReplacement() pada Flutter. Dalam kasus apa sebaiknya masing-masing digunakan pada aplikasi Football Shop kamu?
- Navigator.push(): Menambahkan halaman baru di atas halaman sebelumnya di dalam navigation stack dan cocok digunakan saat saya ingin menavigasi sementara, dan masih ingin kembali ke halaman asal. Di aplikasi saya sebaiknya digunakan untuk dari Home ke Create Product Form, agar pengguna bisa kembali dengan tombol back.
- Navigator.pushReplacement(): Mengganti halaman saat ini dengan halaman baru tanpa menyimpannya di stack dan cocok digunakan saat saya ingin mengganti halaman utama secara permanen, seperti berpindah antar menu utama. Di aplikasi saya sebaiknya digunakan untuk berpindah dari Drawer: Home ke All Products atau Create Product.

## 2. Bagaimana kamu memanfaatkan hierarchy widget seperti Scaffold, AppBar, dan Drawer untuk membangun struktur halaman yang konsisten di seluruh aplikasi?
- Scaffold: Setiap halaman (menu.dart, product_form.dart) menggunakan Scaffold agar layout konsisten.
- AppBar: Semua halaman memakai warna biru tua (Colors.indigo) agar seragam.
- Drawer: Dibuat di widgets/left_drawer.dart dan dipanggil di setiap halaman lewat drawer: LeftDrawer().


## 3. Dalam konteks desain antarmuka, apa kelebihan menggunakan layout widget seperti Padding, SingleChildScrollView, dan ListView saat menampilkan elemen-elemen form? Berikan contoh penggunaannya dari aplikasi kamu.
- Padding: Memberi jarak antar elemen agar tampilan tidak menempel dan membuat form lebih rapi dan mudah dibaca. Contoh: Setiap TextFormField dibungkus dengan Padding(const EdgeInsets.all(8.0)).
- SingleChildScrollView: Membuat seluruh isi halaman bisa discroll dan menghindari overflow ketika keyboard muncul atau layar kecil. Contoh: Di ProductFormPage, seluruh Column yang berisi field form dibungkus SingleChildScrollView sehingga user bisa scroll semua input tanpa error meskipun form banyak.
- ListView: Menampilkan daftar data dengan kemampuan scroll otomatis dan cocok untuk menampilkan list produk atau item dengan panjang tidak tetap. Contoh: Di LeftDrawer, ListView membungkus DrawerHeader dan beberapa ListTile (Halaman Utama, Tambah Produk), sehingga jika menu drawer ditambah banyak pun tetap bisa discroll dengan rapi.

## 4. Bagaimana kamu menyesuaikan warna tema agar aplikasi Football Shop memiliki identitas visual yang konsisten dengan brand toko?

    theme: ThemeData(
        colorScheme: ColorScheme.fromSwatch(primarySwatch: Colors.blue)
        .copyWith(secondary: Colors.blueAccent[400]),
    ),

    