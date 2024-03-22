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


**“(5) Multithreaded server using Threadpool “**

Dalam pembelajaran dari Multithreaded berdasarkan dokumentasi Rust, jujur dari saya sendiri hal ini lumayan rumit, namun dalam kenyataannya dapat sangat membantu dalam kerjanya suatu server jika dihadapi dengan load yang banyak. Untuk Multithread ini, dibutuhkannya suatu `Threadpool`. `Threadpool` sendiri adalah suatu "group of spawned threads" yang menunggu dan siap untuk menangani suatu task. Jika suatu program menerima suatu task baru, `Threadpool` akan melakukan task tersebut dengan salah satu 'thread' nya, dimana thread lainnya akan siap untuk mengerjakan task lainnya. Untuk membuat `Threadpool` ini, dibutuhkannya suatu modul `Threadpool` untuk diimplementasi kepada `main.rs` dengan membuat library terpisah, seperti `lib.rs`. Setelah itu, `Threadpool` baru dapat digunakan. Ukuran dari `Threadpool` dapat dipilih untuk mengakomodasi kebutuhan dari server itu sendiri menggunakan `size`. Lalu untuk membuat `Threadpool` yang dapat melakukan suatu task ketika suatu thread telah dibuat, dibutuhkannya struktur data baru, dimana pada tutorial ini dibuatnya suatu "Worker". Worker mengambil code yang dibutuhkan dan menjalankan code tersebut pada suatu Worker thread. Selanjutnya mengirim request ke Threads melalui Channels dapat menggunakan fungsi `execute` dimana akan mengirim suatu job untuk di execute oleh suatu sender yang dibuat dan ditahan oleh `Threadpool`. Menggunakan Worker sebagai reciever yang akan loop dan meng-execute job yang diterima. 