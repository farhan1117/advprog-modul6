# Reflections Tutorial6

Muhammad Farhan Ramadhan </br>
1906306155</br>
Adpro C


**“(1) Handle-connection, check response”**

Berdasarkan dari dokumentasi Rust, fungsi dari method handle_connection adalah untuk melakukan suatu "Reading the Request" dari browser. 
Method handle_connection akan membaca data dari TCP stream dan akan mengeluarkan/print data tersebut agar dapat dilihat. 
Code for loop yang ada di main akan call handle_connection dan "pass the stream". 
Lalu pada handle_connection, dibuatlah suatu instance BufReader yang mengambil mutable reference dari stream.

**“(2) Returning HTML”**
![Commit 2 screen capture](/assets/images/commit2.png)

Berdasarkan dari dokumentasi Rust, menggunakan `format!` untuk menambahkan file konten sebagai body dari HTTP response yang valid. lalu menambahkan `Content-Length` header yang mengatur sesuai response body, dimana dari `hello.html`.

**“(3) Validating request and selectively responding”**
![Commit 3 screen capture](/assets/images/commit3.png)

Mengikuti dokumentasi Rust pada bagian ketiga ini, awalnya digunakan `if else` untuk melakukan `handle_connection` dimana adanya HTTP request yang tidak ditemukan. Jika HTTP request yang diminta ada, pada contoh ini terdapat pada request line dari GET menuju path `/`, sehingga menampilkan HTML `hello.html`. Pada kondisi selain dari HTTP request tersebut, akan ditampilkannya halaman HTML `404.html` karena HTTP request `NOT FOUND`. Selanjutnya melakukan refactoring terhadap `main.rs` karena `if else` statement yang terlihat banyak repetisi.

**“(4) Simulation of slow request. “**

Berdasarkan dokumentasi Rust, pertama dimodifikasi code `main.rs` dimana awalnya menggunakan `if` menjadi `match` untuk melakukan tiga case. `match` tidak dapat reference dan dereference layaknya equality method, maka perlu secara explisit menyebutkan potongan `request_line`. Pada kasus ini, match pertama sama seperti awal, yang kedua me-request ke `/sleep` dan ketika adanya request ke `/sleep`, server akan sleep selama 10 detik sebelum me render halaman HTML dengan benar. Terakhir, sama seperti `else` yang sebelumnya, menampilkan jika HTTP request tidak ditemukan.