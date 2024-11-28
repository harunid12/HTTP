# Web Server dengan HTTP
untuk menguji apakah suatu web server menggunakan HTTP/1.1, HTTP/2.0, dan HTTP/3.0, menganalisis menggunakan Chrome, dan menganalisis lalu lintas data dengan Wireshark, berikut merupakan hal-hal yang akan dilakukan:

---

## 1. Persiapan Aplikasi

-   **Docker**, Install Docker pada [link berikut](https://www.docker.com/). Pilih sesuai dengan Sistem Operasi masing-masing. Docker digunakan untuk menjalankan web server dalam container. hal ini memungkinkan pengujian berbagai versi protokol HTTP secara terisolasi tanpa menggangu antar entitas yang lain.
-   **Wireshark**, Install Wireshark pada [link berikut](https://www.wireshark.org/). wireshark digunakan untuk menganalisis lalu lintas jaringan secara real-time.
-   **Chrome**, pastikan aplikasi Chrome terinstall dengan versi terbaru.

## 2. Konfigurasi Docker

disini saya menggunakan web server **Nginx** karena mendukung pengunaan HTTP/1.1, HTTP/2.0, dan HTTP/3.0. Sebelum melakukan Konfigurasi, pastikan Docker Engine sudah running.

**a. Donwload Image**

download image Web Server **Nginx** dari [Docker Hub](https://hub.docker.com/_/nginx) dengan perintah `docker pull nginx:latest` 

**b. Generate SSL/TLS**

SSL (Secure Sockets Layer) merupakan protokol kriptografi yang digunakan untuk mengamankan komunikasi data antara client dan server di internet. SSL ini digunakan pada HTTP/2.0 dan HTTP/3.0 untuk memastikan data yang ditransfer terenkripsi dengan aman, serta melindungi data dari intersepsi dan manipulasi oleh pihak ketiga. Pada praktiknya, SSL digantikan oleh TLS (Transport Layer Security).

perintah untuk generate nya adalah `openssl req -x509 -newkey rsa:2048 -keyout nginx.key -out nginx.crt -days 365`

**c. Konfiguasi Nginx untuk HTTP/2.0 dan HTTP/3.0**

untuk HTTP/1.1 tidak diperlukan konfigurasi tambahan, karena Image Nginx yang sudah di pull sebelumnya secara default berjalan pada HTTP/1.1

buat file `http2.conf` dan `http3.conf` di dalam direktori root.

konfigurasi `http2.conf` sebagai berikut:

```
server {
    listen 443 ssl http2;
    server_name localhost;

    ssl_certificate /etc/nginx/certs/nginx.crt;
    ssl_certificate_key /etc/nginx/certs/nginx.key;

    location / {
        root /usr/share/nginx/html;
        index index.html;
    }
}
```


