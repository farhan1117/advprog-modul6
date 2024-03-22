# Reflections Tutorial6

Muhammad Farhan Ramadhan </br>
1906306155</br>
Adpro C


**“(1) Handle-connection, check response”**

Berdasarkan dari dokumentasi Rust, fungsi dari method handle_connection adalah untuk melakukan suatu "Reading the Request" dari browser. 
Method handle_connection akan membaca data dari TCP stream dan akan mengeluarkan/print data tersebut agar dapat dilihat. 
Code for loop yang ada di main akan call handle_connection dan "pass the stream". 
Lalu pada handle_connection, dibuatlah suatu instance BufReader yang mengambil mutable reference dari stream.
