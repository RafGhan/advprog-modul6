# TUTORIAL 6 ADPRO
### Rafi Ghani Harditama (2206081364)
### Advanced Programming A/VRO

## COMMIT 1 REFLECTION NOTES

Yang dilakukan oleh fungsi `handle_connection`:
``` rust
fn handle_connection(mut stream: TcpStream) { 
    let buf_reader = BufReader::new(&mut stream);
    let http_request: Vec<_> = buf_reader
        .lines()
        .map(|result| result.unwrap())
        .take_while(|line| !line.is_empty())
        .collect();
    println!("Request: {:#?}", http_request);
}
```

* `handle connection` adalah fungsi yang bertanggung jawab untuk menangani koneksi TCP dari klien. Fungsi ini membaca permintaan HTTP dari klien yang terhubung dan mencetaknya ke konsol untuk keperluan pemeriksaan respons koneksi. 

* penjelasan per line:

``` rust
let buf_reader = BufReader::new(&mut stream);
``` 
Pada baris ini, sebuah `BufReader` baru dibuat dengan menggunakan `&mut stream`, yaitu referensi mutable ke TcpStream yang diberikan sebagai parameter fungsi `handle_connection`. 

``` rust
let http_request: Vec<_> = buf_reader
    .lines()
    .map(|result| result.unwrap())
    .take_while(|line| !line.is_empty())
    .collect();
```
Baris tersebut menginisialisasi `http_request` sebagai sebuah vector yang berisi data dari permintaan HTTP yang diterima dari klien. `buf_reader.lines()` digunakan untuk membaca setiap baris dari TcpStream. `map(|result| result.unwrap())` digunakan untuk mengkonversi hasil  yang awalnya berbentuk `Result` menjadi `String`.`take_while(|line| !line.is_empty())` digunakan untuk mengambil baris-baris sampai ditemukan baris kosong yang menandakan akhir dari permintaan HTTP. Dan `.collect()` digunakan untuk mengumpulkan baris-baris tersebut ke dalam bentuk vector

``` rust
println!("Request: {:#?}", http_request);
```

Baris ini mencetak `http_request` ke konsol. `{:#?}` digunakan untuk mencetak struktur data secara format dengan lebih mudah dibaca. 