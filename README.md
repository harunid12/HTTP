# Tugas 1 : Analisis Komunikasi TCP dengan Socket Programming dan Wireshark

Tugas ini bertujuan untuk mempelajari komunikasi TCP antara client dan server menggunakan socket programming serta melakukan monitoring jaringan dengan Wireshark. Proses ini mencakup pengiriman data sederhana dan analisis paket TCP untuk memahami alur komunikasi, termasuk Connection establishment using three-way handshaking, Data Transfer dan Connection termination using three-way handshaking.

## Deskripsi Singkat

Pada tugas ini, saya memanfaatkan socket programming sederhana dari [Repository Github](https://github.com/ferryastika/socket-programming-simple-server-and-client) untuk mengimplementasikan komunikasi client-server. Server dijalankan pada port **8000**, dan client terhubung ke server tersebut. Data yang dikirim berupa karakter **A** dan selanjutnya dianalisis alur transmisinya menggunakan Wireshark.

hasil analisis Wireshark digambarkan dalam diagram TCP Sequence, yang menunjukkan detail komunikasi TCP secara berurutan dimulai dari connection establishment hingga connection termination

## TCP Sequence Diagram

**Connection Establishment (Three-way handshaking)**

- **Step 1: SYN (Synchronize)**  
   Client mengirimkan paket **SYN** dengan `Seq=0` ke Server untuk memulai koneksi.

- **Step 2: SYN-ACK (Synchronize-Acknowledgment)**
  Server merespons dengan paket **SYN+ACK** yang memiliki Seq=0, Ack=1, menunjukkan bahwa server siap untuk menerima komunikasi.

- **Step 3: ACK**
  Client mengirimkan paket **ACK** dengan Seq=1, Ack=1, mengonfirmasi koneksi telah terjalin.

**Data Transfer**
pada tahap ini, **Client** dan **Server** saling bertukar data. prosesnya melibatkan flag **PSH + ACK** dan **ACK**.

- **Step 4: PSH + ACK**  
   Client mengirimkan data dengan paket : Seq = 1, Ack = 1.

- **Step 5: ACK**
  Server mengkonfirmasi penerimaan data dengan paket: Seq = 1, Ack = 2.

- **Step 6: PSH + ACK**
  Server mengirimkan data balik ke Client dengan paket : Seq = 1, Ack = 2.

- **Step 7: ACK**
  Client mengkonfirmasi penerimaan data dengan paket : Seq = 2, Ack =2.

**Connection termination (three-way handshaking)**
Tahap ini adalah proses untuk menutup koneksi setelah pertukaran data selesai.

- **Step 8: FIN + ACK**
  Client mengirimkan paket : Seq = 2, Ack = 2. paket **FIN** menunjukan bahwa Client ingin mengakhiri koneksi

- **Step 9: ACK**
  Server mengonfirmasi permintaan dengan paket: Seq = 2, Ack = 3

- **Step 10: FIN + ACK**
  Server mengirimkan FIN untuk mengakhiri koneksi dari sisi Server: Seq = 2, Ack = 3.

- **Step 11: ACK**
  Client mengonfirmasi dengan paket: Seq = 3, Ack = 3. koneksi telah tertutup sepenuhnya.

## Penjelasan Tambahan

- **Seq (Sequence Number):** Nomor urut yang digunakan untuk melacak byte data yang dikirimkan.
- **Ack (Acknowledgment Number):** Nomor untuk mengonfirmasi byte data yang telah diterima.
- **PSH (PUSH) :** Memberitahu penerima untuk segera memproses data.
- **FIN (Final) :** Digunakan untuk mengakhiri koneksi.



# Tugas 2 : Analisis Koneksi TCP Menggunakan Wireshark

## Deskripsi Singkat

Pada tugas ini, saya melakukan analisis terhadap komunikasi TCP antara client dan server berdasarkan sample capture Wireshark yang diberikan, yaitu file **http.cap**. dari sample capture ini, analisis dilakukan untuk mengamati alur komunikasi mulai dari Connection establishment using three-way handshaking, Data Transfer dan Connection termination using three-way handshaking.

Dari **43 paket** yang tercatat dalam file capture **http.cap**,  hanya **34 paket** yang berhasil diproses dalam komunikasi TCP yang melibatkan client dan server.


## TCP Sequence Diagram

**1. Connection Establishment (Three-way handshaking)**

- **Client** mengirimkan paket **SYN** untuk memulai koneksi
- **Server** merespon dengan paket **SYN + ACK** untuk mengkonfirmasi penerimaan dan siap berkomunikasi
- **Client** kemudian mengirimkan **ACK** untuk menyelesaikan handshake dan membuka koneksi
- tahap ini digambarkan pada TCP Sequence diagram dimulai dari step 1-3.

**2. Data Transfer** 

- **Step 4: PSH + ACK**
   Seq = 1, Ack = 1. Client mengirimkan 479 byte data.

- **Step 5: ACK**
   Seq = 1, Ack = 480. Server mengonfirmasi penerimaan data yang dikirim oleh client, Ack = 480 menunjukkan bahwa server sudah menerima data hingga byte ke 479 dari client dan mengharapkan data selanjutnya dimulai dari byte 480.

- **Step 6: ACK**
   Seq = 1, Ack = 480. Server mengirimkan 1380 byte data dimulai dari Seq = 1, yang berarti data yang dikirimkan dimulai dari byte ke-1 hingga byte ke-1380.

- **Step 7: ACK**
   Seq = 480, Ack = 1381. Client mengkonfirmasi penerimaan data dari server dengan Ack = 1381, menunjukkan bahwa client sudah menerima semua data hinga byte ke 1380 dari server. Seq = 480 menunjukkan urutan data yang dikirimkan oleh client setelah menerima data dari server.

Proses Data Transfer terus berlanjut hingga Step 30. Data yang dikirimkan akan terus memiliki urutan nomor Sequence yang sesuai, dan Acknowledgment Number dari kedua pihak akan mengonfirmasi bahwa setiap paket diterima dengan benar. Setelah seluruh data terkirim, koneksi akan ditutup dengan paket FIN untuk mengakhiri sesi komunikasi.

**3. Connection termination (three-way handshaking)** 

- **Step 31 :** Server mengirimkan **FIN + ACK** yang menandakan bahwa server ingin menutup koneksi.
- **Step 32 :** Client mengkonfirmasi dengan **ACK**.
- **Step 33 :** Client mengirimkan **FIN + ACK** yang menandakan bahwa client juga ingin menutup koneksi.
- **Step 34 :** server mengkonfirmasi penutupan koneksi dengan **ACK**.











