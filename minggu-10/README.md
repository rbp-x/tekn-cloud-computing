# Laporan, Latihan dan Tugas Praktikum Teknologi Cloud Computing - Minggu 10 
#### Rahadiyan Bondan Permadi
##### 215411119


## Materi

** Docker Networking Hands-on Lab **

## Tujuan

Pada pertemuan ini, kita akan mempelajari konsep utama Docker Networking dan beberapa contoh konsep jaringan dasar, bridge danyang terakhir jaringan overlay.

## Pembahasan

Dalam praktikum ini ada beberapa tahapan diantaranya adalah :

Section #1 - Networking Basics

Docker Network Command

      $ docker network

gambar 1

Daftar docker network

      $ docker network ls

gambar 2

Inspect a network

      $ docker network inspect bridge

gambar 3

Docker info

      $ docker info

gambar 4


Section #2 - Bridge Networking

daftar docker network 

      $ docker network ls

gambar 5


Selanjutnya kita mulai install dulu brctl dengan perintah 

      $ sudo apt-get install bridge-utils

gambar 6

      $ brctl show

gambar 6

menampilkan detail dari docker0

      $ ip a

gambar 7

Membuat container baru dengan menjalankan perintah :

      $ docker run -dt ubuntu sleep infinity

gambar 8

gambar 8

Memverivikasi container

      $ docker ps

gambar 9

Kembali kita tampilkan bridge-utils menggunakan 

      $ brctl show

gambar 10

kita inspect kembali menggunakan perintah 

      $ docker network inspect bridge

gambar 11

Lakukan ping dengan 172.17.0.2

      $ ping -c5 172.17.0.2

gambar 12

Docker ps

      $ docker ps

gambar 13

sekarang kita coba menjalankan didalam shell container ubuntu dengan perintah :

      $ docker exec -it fa39e102f0a4 /bin/bash

gambar 14

Selanjutnya kita install program ping dengan menjalankan perintah dibawah ini :

      $ apt-get update && apt-get install -y iputils-ping

gambar 15

selanjutnya kita coba koneksi dengan ping ke github

      $ ping -c5 www.github.com

gambar 16

Konfigurasi NAT untuk koneksi luar dengan memulai membuat container baru nginx

      $ docker run --name web1 -d -p 8080:80 nginx

gambar 17

      $ docker ps

gambar 18

kita buka web dengan durl 

      $ curl 127.0.0.1:8080

gambar 19


Section #3 - Overlay Networking
Cleaning Up

Pada langkah ini kita akan menginisialisasi swarm baru konek dengan node dan memverivikasinya.

Jalankan perintah berikut ini :

     $ docker swarm init --advertise-addr $(hostname -i)
	
## Software yang Diperlukan

Linux, Docker

```

