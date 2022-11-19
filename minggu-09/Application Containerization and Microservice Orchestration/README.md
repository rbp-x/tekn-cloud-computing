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
   
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/1.cloning_repo.jpg)


# Step 0: Basic Link Extractor Script

cek isi data step0

    $ git checkout step0
   
    $ tree
   
![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/2.checkou_data_step0.jpg)


melihat isi dari file linkextractor.py

    $ cat linkextractor.py
   
![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/3.cat_link_py.jpg)

Kita coba menjalankan script diatas 

    $ ./linkextractor.py http://example.com/

![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/4.test_linkextractor_py_denied.jpg)

maka hasilnya error akses ditolak 

kita cek file linkextractor.py

    $ ls -l linkextractor.py

![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/5.permission_oke_after_chmod.jpg)

kita rubah permission menggunakan perintah 

    $ chmod a+x linkextractor.py
   
![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/5.permission_oke_after_chmod.jpg)

Run Python

    $ python3 linkextractor.py

![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/6.run_python_program.jpg)

# Step 1: Containerized Link Extractor Script

cek isi data step1

    $ git checkout step1

    $ tree

![7.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/7.step1_checkout.jpg)

Cat Dockerfile

    $ cat Dockerfile

![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/8.cat_Dockerfile.jpg)

kita perlu menambahkan dua paket install pip beautifulsoup4 dan requests agar skrip dalam dockerfile dapat berfungsi. Seblumnya pada mesin saya install py3_pip terlebih dahulu.

    $ sudo apt install python3-pip

![9.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/9.install_py_pip.jpg)

![9.2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/9.install2_py_pip.jpg)

![9.3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/9.install3_py_pip.jpg)

selanjutnya kita install beautifulsoup4

    $ pip install beautifulsoup4

![10.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/10.install_beatifulesoup4.jpg)

selanjutnya kita install pip requests (sudah tersedia di paket py3)

    $ pip install requests

![11.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/11.requests_already.jpg)

selanjutnya kita membangun Docker Image dengan perintah dibawah ini 

    $ docker image build -t linkextractor:step1 .

![12.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/12.build_docker_image.jpg)

menampilkan Docker Image dengan nama linsextractor:step1

    $ docker image ls

![13.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/13.showing_docker_image_ls.jpg)

selanjutnya menjalankan satu container linkextractor:step1

    $ docker container run -it --rm linkextractor:step1 http://example.com/

menghasilkan tautan seperti dibawah ini :

![14.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/14.sampel_web.jpg)

![14.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/14.web_sample.jpg)


selanjutnya mencoba lebih banyak link didalamnya dengan perintah 

    $ docker container run -it --rm linkextractor:step1 https://training.play-with-docker.com/

![15.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/15.links_on_web.jpg)

sebelum kita checkout step2 kita lakukan comit menggunakan perintah 

    $ git stash

# Step 2: Link Extractor Module with Full URL and Anchor Text

disini kita akan mencoba lebih banyak lagi, kita checkout step2

    $ git checkout step2
    $ tree
   
![16.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/16.step2_chechout_before_stash_step1.jpg)

selanjutnya kita melihat skirp yang sudah update dari step2 ini 

    $ cat linkextractor.py

![17.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/17.update_script_on_step2.jpg)

sekarang kita akan mencoba membangun docker image pada step2

    $ docker image build -t linkextractor:step2 .

![18.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/18.build_docker_image_on_step2.jpg)
   
    $ docker image ls

![19.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/19.docker_image_ls_step2.jpg)

selanjutnya kita mencoba menjalankan container pada image step2 dengan perintah dibawah 

    $ docker container run -it --rm linkextractor:step2 https://training.play-with-docker.com/

![20.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/20.docker_run_container_step2.jpg)

kita juga  mencoba untuk menjalankan container step1

    $ docker container run -it --rm linkextractor:step1 https://training.play-with-docker.com/
   
![21.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/21.docker_run_container_step1.jpg)

Sampai dengan langkah kedua ini kita telah belajar dan mempelajari pengemasan script menggunakan dependensi yang dibutuhkan dengan lebih fleksibel, kita mempelajari membuat perubahan dalam aplikasi dan membuat berbagai varian docker image yang berada dalam satu wadah.

# Step 3: Link Extractor API Service

Pada langkah ini kita akan mencoba membangun dan menjalankan layanan web menggunakan script ini dalam docker.

    $ git checkout step3
    $ tree

![22.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/22.checkout_step3.jpg)

Selanjutnya kita masuk dockerfile dengan perintah 

    $ cat Dockerfile

![23.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/23.cat_dockerfile_step3.jpg)

kita lihat isi main.py 

    $ cat main.py

![24.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/24.cat_main_py_step3.jpg)

selanjutnya kita build image dan jalankan docker container :

    $ docker image build -t linkextractor:step3 .
   
    $ docker container run -d -p 5000:5000 --name=linkextractor linkextractor:step3

    $ docker container ls

![25.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/25.docker_container_run_step3.jpg)

Selanjutnya membuat request HTTP dalam bentuk url

    $ curl -i http://localhost:5000/api/http://example.com/

![26.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/26request_http.jpg)

setelah servis API berjalan dan mendapatkan respon JSON berupa Link url seperti pada gambar.

kita dapat melihat log menggunakan perintah :

    $ docker container logs linkextractor

![27.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/27.logs_http.jpg)

kita mematikan dan menghapus container log setelah ditampilkan menggunakan perintah dibawah :

    $ docker container rm -f linkextractor

Step 4: Link Extractor API and Web Front End Services

Langkah selanjut membuat layanan GUI 

kita checkout dulu file step4

    $ git checkout step4
    $ tree

![28.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/28.checkou_step4.jpg)

selanjutnya kita lihat file docker-compose.yml

    $ cat docker-compose.yml

![29.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/29.cat_docker_compose_yml.jpg)

kita lihat isi file index.php

    $ cat www/index.php

![30.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/30.cat_index_php.jpg)

selanjut kita jalankan docker compose

    $ docker-compose up -d --build

![31.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/31.docker_compose_up.jpg)

pastikan bahwa keduanya layanan berjalan docker container 

    $ docker container ls

![32.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/32.docker_container_ls_step4.jpg)

selanjutnya kita test service API

reloading

    $ sed -i 's/Link Extractor/Super Link Extractor/g' www/index.php

    $ git reset --hard

    $ docker-compose down
   
   
![33.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/33.reloading.jpg)
   
![32.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/32.GUI%20Link%20Estractor.jpg)


Step 5: Redis Service for Caching

    $ git checkout step5
    $ tree
 
![34.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/34.checkout_step5.jpg)

kita tampilkan Dockerfile

    $ cat www/Dockerfile

![35.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/35.cat_dockerfile_step5.jpg)

kita tampilkan main.py

    $ cat api/main.py

![36.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/36.cat_api_json.jpg)


selanjutnya kita tampilkan docker-compose.yml

    $ cat docker-compose.yml

![37.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/37.cat_docker_compose_yml.jpg)


kita booting dan up service

    $ docker-compose up -d --build

![38.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/38.docker_compose_build_up.jpg)


    $ docker-compose exec redis redis-cli monitor

![39.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/39.redis.jpg)


    $ sed -i 's/Link Extractor/Super Link Extractor/g' www/index.php

    $ git reset --hard

    $ docker-compose down

![40.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/40..jpg)


# Step 6: Swap Python API Service with Ruby Conclusions

    $ git checkout step6
    
    $ tree
  
![41.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/41.checkout_step6.jpg)


    $ cat api/linkextractor.rb

![42.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/42.cat_api_linkextractor_rb.jpg)


    $ cat api/Dockerfile

![43.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/43.cat_api_dockerfile_step6.jpg)


    $ cat docker-compose.yml

![44.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/44.cat_docker_compose_yml.jpg)


dalam ervice ii kita build dan jalankan docker-compose 

    $ docker-compose up -d --build 

![45.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/45.docker_compose_up_and_build.jpg)

Akses API dengan port baru 

    $ curl -i http://localhost:4567/api/http://example.com/

![46.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/46.access_api_new_Port.jpg)

![46.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/46.interface_extractor.jpg)


Sekarang kita lakukan shut-down terhadap compose

    $ docker-compose down

![47.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/47.docker_compose_down.jpg)

cek apakah log masih ada setelah service di matikan 

    $ cat logs/extraction.log
   
![48.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/48.logs.jpg)

Sejauh ini, kita telah mempraktekan docker-compose untuk mengatur beberapa aplikasi berjalan dalam lingkup pengembangan.


## Software yang Diperlukan

Linux, Docker

```

