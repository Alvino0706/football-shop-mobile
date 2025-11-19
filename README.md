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

# Tugas 9

---

## 1. Jelaskan mengapa kita perlu membuat model Dart saat mengambil/mengirim data JSON? Apa konsekuensinya jika langsung memetakan Map<String, dynamic> tanpa model (terkait validasi tipe, null-safety, maintainability)?
Saat kita ambil/kirim data JSON dari/ke Django, sebenarnya yang kita tangani adalah teks (String) yang baru di-decode jadi Map<String, dynamic>. Kalau tidak dibuat model Dart:
- Semua data akan jadi Map<String, dynamic> “liar”.
- Setiap kali dipakai kita harus ngetik manual: map['name'] as String, map['price'] as int, dll.
- Salah nama key (typo) atau salah tipe (harusnya int, ternyata String) baru ketahuan saat runtime, bukan saat kompilasi.

Dengan membuat model dart ada:
- Type-safety & null-safety
- Validasi struktur & dokumentasi implicit
- Maintainability
- Lebih mudah dipakai di widget

## 2. Apa fungsi package http dan CookieRequest dalam tugas ini? Jelaskan perbedaan peran http vs CookieRequest.
(1) Package http
- Library umum untuk melakukan HTTP request: GET, POST, dll.
- Biasa dipakai untuk API tanpa autentikasi cookie
- Kita sendiri yang harus mengurus header, cookie, body, dll.

(2) CookieRequest
- Abstraksi khusus yang dibuat untuk mengintegrasikan Flutter dengan Django pada tugas PBP.
- Menyimpan dan mengelola session cookie Django secara otomatis
- Menyediakan method khusus seperti login(url, data), logout(url), get(url), post(url, data)

Perbedaan perannya yaitu:
(1) http lebih low level, generik, tidak tahu apa-apa soal Django / session.
(2) CookieRequest lebih high level, sudah di-wrap supaya cocok dengan mekanisme login Django (session-based auth).

## 3. Jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
Hal ini dikarenakan CookieRequest menyimpan state autentikasi apakah sudah login, cookie session dari Django, dan info user yang login. Kalau setiap halaman membuat instance CookieRequest baru, maka cookie-nya tidak sama, halaman A mungkin login, halaman B seperti belum login, dan request ke backend jadi tidak konsisten. Namun, dengan membagikan instance yang sama,semua widget memakai session yang sama, sekali login di halaman Login → halaman lain otomatis bisa mengakses endpoint terproteksi, dan memudahkan pengelolaan global state.

## 4. Jelaskan konfigurasi konektivitas yang diperlukan agar Flutter dapat berkomunikasi dengan Django. Mengapa kita perlu menambahkan 10.0.2.2 pada ALLOWED_HOSTS, mengaktifkan CORS dan pengaturan SameSite/cookie, dan menambahkan izin akses internet di Android? Apa yang akan terjadi jika konfigurasi tersebut tidak dilakukan dengan benar?
Konfigurasi konektivitas yang diperlukan agar Flutter dapat berkomunikasi dengan Django:
- 10.0.2.2 di ALLOWED_HOSTS: Kalau 10.0.2.2 tidak ada di ALLOWED_HOSTS, Django menolak request dengan error DisallowedHost.
- CORS (Cross-Origin Resource Sharing): Dengan mengaktifkan CORS (misalnya using django-cors-headers) dan mengizinkan origin yang sesuai, Flutter boleh mengakses API Django.
- Pengaturan SameSite / cookie: Jika SameSite terlalu ketat (Strict) atau cookie tidak diatur dengan benar, cookie bisa tidak terkirim pada request berikutnya. Makanya perlu atur SESSION_COOKIE_SAMESITE, SESSION_COOKIE_SECURE, dll. agar cocok dengan cara Flutter mengakses.
- Izin akses internet di Android (AndroidManifest.xml): Tanpa ini, aplikasi tidak boleh melakukan request ke jaringan → semua HTTP request gagal

Yang akan terjadi jika konfigurasi tersebut tidak dilakukan dengan benar:
- Request bisa terus-menerus gagal (timeout / error 500 / DisallowedHost)
- Login terlihat “berhasil” di Flutter tapi Django tidak pernah menerima cookie
- Endpoint yang butuh autentikasi selalu menganggap user sebagai AnonymousUser

## 5. Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.
(1) Input di Flutter (User mengisi form, misal TextFormField untuk name, price, dsb.)
(2) Data dikemas dalam bentuk Map
(3) Dikirim ke Django lewat CookieRequest.post
(4) Di sisi Django, view menerima POST request dengan request.POST atau json.loads(request.body) dan Django memvalidasi data. Jika valid, data disimpan ke database dan Django mengirim response JSON.

## 6. Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
(1) Register
- User mengisi form register di Flutter (username, password, dsb.).
- Flutter mengirim data ke endpoint Django (misal /auth/register/) menggunakan CookieRequest.post.
- Django menerima data, membuat user baru, dan mengembalikan JSON
- Flutter menampilkan pesan error/berhasil.

(2) Login
- User mengisi username dan password di Flutter.
- Flutter memanggil:

        final response = await request.login(
        "http://10.0.2.2:8000/auth/login/",
        {
            'username': username,
            'password': password,
        },
        );

- Django memvalidasi username & password (authenticate, login). Jika sukses, Django membuat session dan mengirim session cookie ke client.
- CookieRequest menyimpan cookie tersebut dan menandai state bahwa user sudah login.
- Jika login sukses Flutter memindahkan ke halaman menu utama. Jika gagal → tampilkan snackbar / alert.

(3) Mengakses endpoint yang butuh login
- Saat memanggil request.get("http://10.0.2.2:8000/my-products/"), CookieRequest otomatis menyertakan session cookie.
- Django mengenali cookie → meng-set request.user menjadi user yang login.
- View dapat memfilter data berdasarkan request.user.

(4) Logout
- Flutter memanggil:

        final response = await request.logout("http://10.0.2.2:8000/auth/logout/");

- Django menjalankan logout(request) → menghapus session.
- CookieRequest membersihkan cookie di sisi Flutter.
- Flutter menampilkan pesan sukses dan mengarahkan user kembali ke halaman login

## 7. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial).
(1) Memastikan deployment proyek tugas Django kamu telah berjalan dengan baik.
- Pastikan proyek Django sudah dijalankan dengan python manage.py runserver
- Tambahkan endpoint JSON yang mengembalikan data item dalam format JSON.
- Cek respon di browser

(2) Mengimplementasikan fitur registrasi akun pada proyek tugas Flutter.
- Membuat file baru di flutter yaitu register.dart dan app baru di django yang bernama authentication yang views.py nya berisi method baru yaitu register.
- Ketika tombol register ditekan, flutter mengirim data ke endpoint Django:

        final response = await request.post(
        "http://localhost:8000/auth/register/",
        {"username": username, "password": password},
        );

- Jika django mengembalikan status sukses, saya menampilkan snackbar dan mengarahkan user ke halaman login.
        
(3) Membuat halaman login pada proyek tugas Flutter.
- Membuat file baru di flutter yaitu login.dart dan method baru di django views.py (app authentication) yaitu login.
- Ketika tombol login ditekan, flutter mengirim data ke endpoint Django:

        final response = await request.login(
        "http://localhost:8000/auth/login/",
        {"username": username, "password": password},
        );

- Jika sukses, CookieRequest menyimpan session cookie Django dan Flutter langsung menavigasikan user ke MenuPage.

(4) Mengintegrasikan sistem autentikasi Django dengan proyek tugas Flutter.
- Integrasi dilakukan dengan menempatkan Provider<CookieRequest> di root aplikasi:

        return Provider(
            create: (_) => CookieRequest(),
            child: const MyApp(),
            );

- Dampaknya yaitu CookieRequest bisa diakses dari seluruh widget, Session login Django otomatis ikut pada setiap request (get dan post), Endpoint seperti /my-products/ bisa tahu siapa user yang sedang login melalui request.user.

(5) Membuat model kustom sesuai dengan proyek aplikasi Django.
- Saya membuat file product_entry.dart sesuai struktur model Django
- Tujuannya untuk mengubah JSON Django menjadi object Dart, menjamin type-safety dan null-safety, dan memudahkan tampilan UI (misalnya product.name, bukan map['name']).

(6) Membuat halaman yang berisi daftar semua item yang terdapat pada endpoint JSON di Django yang telah kamu deploy.
Saya membuat halaman ProductEntryListPage di mana data diambil dengan `final response = await request.get("http://localhost:8000/json/");`, data JSON diubah menjadi `List<ProductEntry>` menggunakan model. 

(7) Membuat halaman detail untuk setiap item yang terdapat pada halaman daftar Item.
Saya membuat ProductDetailPage di mana:
- Halaman menerima ProductEntry product lewat Navigator.
- Menampilkan seluruh field, termasuk gambar.
- Card pada halaman list menavigasikan user ke detail:

        onTap: () {
            Navigator.push(
                context,
                MaterialPageRoute(
                builder: (_) => ProductDetailPage(product: product),
                ),
            );
            }


(8) Melakukan filter pada halaman daftar item dengan hanya menampilkan item yang terasosiasi dengan pengguna yang login.
Saya membuat endpoint Django khusus:

        @login_required
        def my_products(request):
            user = request.user
            products = Product.objects.filter(user=user)
            data = []

            for p in products:
                data.append({
                    "id": p.id,
                    "name": p.name,
                    "price": p.price,
                    "description": p.description,
                    "stock": p.stock,
                    "condition": p.condition,
                    "thumbnail": p.thumbnail,
                    "category": p.category,
                    "is_featured": p.is_featured,
                    "user_id": p.user.id,
                })

            return JsonResponse(data, safe=False)

Pada Flutter saya membuat halaman MyProductsPage: `final response = await request.get("http://10.0.2.2:8000/my-products/");`. Data kemudian ditampilkan dengan ListView.builder sama seperti halaman all products. Karena session cookie terintegrasi lewat CookieRequest, Django dapat mengenali: `request.user == pengguna yang login`.


