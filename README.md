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
