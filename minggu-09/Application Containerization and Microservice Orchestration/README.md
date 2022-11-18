# Laporan, Latihan dan Tugas Praktikum Teknologi Cloud Computing - Minggu 9 
#### Rahadiyan Bondan Permadi
##### 215411119


## Materi

**Application Containerization**
# Application Containerization and Microservice Orchestration

## Tujuan

1.  Mahasiswa mampu memahami perintah dasar Docker dan Alur Kerja Docker Build dan Run dan menjalankan berbagai komponen aplikasi sebagai layanan mikro.
2.  Mahasiswa mampu menggunakan docker compose dalam pengembangan.
3.  Mahasiswa mampu memahami JSON Cache Redis yang digunakan dalam API untuk menghindari penumpukan berulang.


## Pembahasan

Langkah - langkah 

Stage Setup

Kita mulai dengan meng-kloning demo kode dari repository git.

   $ git clone https://github.com/ibnesayeed/linkextractor.git
   $ cd linkextractor
   $ git checkout demo

Step 0: Basic Link Extractor Script

cek isi data step0

   $ git checkout step0
   $ tree

melihat isi dari file linkextractor.py

   $ cat linkextractor.py

gambar 4 

Kita coba menjalankan script diatas 

   $ ./linkextractor.py http://example.com/

maka hasilnya error akses ditolak 

gambar 4

kita cek file linkextractor.py

   $ ls -l linkextractor.py

gambar 5

kita rubah permission menggunakan perintah 

   $ chmod a+x linkextractor.py

gambar 5

Run Python

   $ python3 linkextractor.py

gambar 6

Step 1: Containerized Link Extractor Script

cek isi data step1

   $ git checkout step1

   $ tree

gambar 7

Cat Dockerfile

   $ cat Dockerfile

gambar 8

kita perlu menambahkan dua paket install pip beautifulsoup4 dan requests agar skrip dalam dockerfile dapat berfungsi. Seblumnya pada mesin saya install py3_pip terlebih dahulu.

   $ sudo apt install python3-pip

gambar 9
gambar 9.2
gambar 9.3

selanjutnya kita install beautifulsoup4

   $ pip install beautifulsoup4

gambar 10

selanjutnya kita install pip requests (sudah tersedia di paket py3)

   $ pip install requests

gambar 11





Step 2: Link Extractor Module with Full URI and Anchor Text
Step 3: Link Extractor API Service
Step 4: Link Extractor API and Web Front End Services
Step 5: Redis Service for Caching
Step 6: Swap Python API Service with Ruby
Conclusions

## Software yang Diperlukan

Linux, Docker

```

