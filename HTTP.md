# Web Server dengan HTTP
untuk menguji apakah suatu web server menggunakan HTTP/1.1, HTTP/2.0, dan HTTP/3.0, menganalisis menggunakan Chrome, dan menganalisis lalu lintas data dengan Wireshark, berikut merupakan hal-hal yang akan dilakukan:

---

## 1. Persiapan Aplikasi

-   **Docker**, Install Docker pada [link berikut](https://www.docker.com/). Pilih sesuai dengan Sistem Operasi masing-masing. Docker digunakan untuk menjalankan web server dalam container. hal ini memungkinkan pengujian berbagai versi protokol HTTP secara terisolasi tanpa menggangu antar entitas yang lain.
-   **Wireshark**, Install Wireshark pada [link berikut](https://www.wireshark.org/). wireshark digunakan untuk menganalisis lalu lintas jaringan secara real-time.
-   **Chrome**, pastikan aplikasi Chrome terinstall dengan versi terbaru.

## 2. Konfigurasi Docker

disini saya menggunakan web server **NGINX** karena mendukung pengunaan HTTP/1.1, HTTP/2.0, dan HTTP/3.0. Sebelum melakukan Konfigurasi, pastikan Docker Engine sudah running.

**a. Donwload Image**

download image Web Server **NGINX** dari [Docker Hub](https://hub.docker.com/_/nginx) dengan perintah `docker pull nginx:latest` 

**b. Create Container**


