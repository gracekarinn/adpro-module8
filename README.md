### 1. Perbedaan Unary, Server Streaming, dan Bi-Directional Streaming

* **Unary**: Client mengirim satu permintaan dan mendapatkan satu jawaban. Ideal untuk operasi sederhana dengan satu hasil, seperti login atau mengambil data pengguna.
* **Server Streaming**: Client mengirim satu permintaan, tetapi server membalas dalam bentuk aliran data bertahap. Cocok untuk laporan besar atau hasil proses yang lama.
* **Bi-Directional Streaming**: Kedua pihak saling mengirim dan menerima data secara bersamaan. Paling pas untuk aplikasi real-time seperti chat atau game online.

### 2. Pertimbangan Keamanan dalam gRPC Rust

* Implementasi keamanan harus mencakup **authentication**, **authorization**, dan **encryption** data. Tujuannya untuk menjaga kerahasiaan komunikasi dan memastikan hanya pihak yang sah dapat mengakses layanan.

### 3. Tantangan pada Bi-Directional Streaming di Rust gRPC

* Mengelola koneksi dua arah membutuhkan sinkronisasi yang baik, termasuk buffering dan error handling. Hal ini penting dalam aplikasi real-time seperti chat agar pertukaran pesan tetap lancar.

### 4. Kelebihan & Kekurangan `ReceiverStream`

* **Kelebihan**: Memudahkan streaming data secara asinkron menggunakan channel.
* **Kekurangan**: Bisa menimbulkan bottleneck dan sulit diskalakan jika data masuk terlalu besar atau terlalu cepat tanpa pengaturan resource yang tepat.

### 5. Struktur Kode gRPC Rust untuk Reusabilitas

* Kode sebaiknya dibagi ke dalam modul fungsional (misalnya auth, logic, proto). Gunakan trait untuk service abstraction, dan pisahkan utilitas ke file terpisah agar mudah diperluas dan dikelola.

### 6. Tambahan untuk MyPaymentService

* Untuk skenario pembayaran yang kompleks, perlu disiapkan integrasi dengan payment gateway, validasi tambahan, retry mechanism, serta pencatatan transaksi untuk audit.

### 7. Dampak gRPC pada Arsitektur Sistem Terdistribusi

* gRPC menyederhanakan komunikasi internal antar layanan dengan performa baik, tapi interoperabilitas dengan sistem lain (misalnya REST) bisa memerlukan bridge tambahan seperti API Gateway.

### 8. HTTP/2 vs HTTP/1.1/WebSocket

* **HTTP/2** lebih efisien karena mendukung koneksi paralel (multiplexing) dan kompresi header.
* **WebSocket** cocok untuk komunikasi real-time yang berkelanjutan, meskipun tidak seoptimal HTTP/2 dalam beberapa aspek teknis.

### 9. Perbandingan REST vs gRPC Streaming

* REST berbasis satu permintaan satu jawaban, cocok untuk interaksi yang tidak memerlukan koneksi terus-menerus.
* gRPC streaming memungkinkan pertukaran data dua arah secara langsung, memberikan pengalaman responsif dalam komunikasi real-time.

### 10. Implikasi Schema Protobuf vs JSON

* **Protobuf** memaksa struktur yang ketat dan efisien untuk proses dan transmisi data.
* **JSON** lebih bebas dan mudah dibaca manusia, cocok untuk API yang cepat dikembangkan namun kurang efisien dalam performa dan ukuran data.