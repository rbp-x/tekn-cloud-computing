# Laporan, Latihan dan Tugas Praktikum Teknologi Cloud Computing - Minggu 9 
#### Rahadiyan Bondan Permadi
##### 215411119


## Materi

**Docker for Beginners - Linux**

## Tujuan

1.  Mahasiswa mampu memahami perintah dasar Docker dan Alur Kerja Docker Build dan Run
2.  Mahasiswa mampu menjalankan, merubah/update beberapa container dan push file ke Docker Hub.
3.  Mahasiswa mampu menggunakan Dockerfile untuk pembuatan aplikasi atau website
4.  Mahasiswa mampu dan memahami penggunaan bind mount untuk memodifikasi container yang sedang berjalan.

## Pembahasan

Dalam praktikum ini ada beberapa tahapan diantaranya adalah :

## Task 0: Prerequisites

1. Prerequisites (kita melakukan clone linux_tweet_app ) terlebih dahulu.
   Persiapan DOCKERID jika belum memiliki akun docker wajib mendaftar dan membuat DOCKERID terlebih dahulu.
	Hasilnya 

    $ git clone https://github.com/dockersamples/linux_tweet_app
	
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/1.git_clone_dockersample_linux_tweet_app.jpg)

## Task 1: Run some simple Docker containers

2. Selanjut "Run some simple Docker containers" untuk menjalankan ini bisa berupa script shell atau aplikasi khusus, dan terkoneksi dengan container mirip seperti penggunaan remote SSH yang berguna untuk layanan jangka panjang seperti database dan website.

	Jalankan perintah di linux :
    $ docker container run alpine hostname
	
	![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/2.run_a_single_task_in_alpine_container.jpg)

3. Menampilkan list container dimana docker menjaga container tetap berjalan pada saat proses dalam container sedang berjalan.
	Jalankan perintah dibawah untuk melihat seluruh container yang sedang berjalan :
	
    $ docker container ls --all
	
	![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/3.menampilkan_detail_container.jpg)

4. Menjalankan container berdasarkan Versi Linux dari masing - masing Docker host, pada praktik ini menjalankan Container Linux diatas Host Alpine Ubuntu untuk tiap node nya. 
	Berikut perintahnya untuk menjalankan container Docker dan mengakses shellnya.
	
    $ docker container run --interactive --tty --rm ubuntu bash
	
	![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/4.run_ubuntu_container.jpg)

	Sedikit penjelasan script diatas : 
	--interactive untuk melakukan interkoneksi atau interaksi.
	--tty mengalokasi pseudo-tty.
	--rm perintah ini akan memberi informasi Docker untuk melanjutkan proses dan menghapus container setelah selesai dijalankan.

5. Kemudian menjalankan perintah dibawah didalam container :
    
    $ ls /
	menampilkan isi data root folder pada container
    $ ps aux
	menampilkan proses berjalan dalam container
    $ cat /etc/issue
	akan menampilkan distro linux apa yang dijalankan oleh container, dalam hal ini Ubuntu 22.04 LTS
	
	![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/5.ls_show_content_ps_aux_menampilkan_proses_berjalanan_cat_menampilkan_linux_container_berjalanan_dalam_hal_ini_ubuntu.jpg)

6. Perintah exit untuk keluar dari sesi shell dan menghentikan proses bash dan container keluar.
    
    $ exit

![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/6.exit_leave_session.jpg)

7. Kemudian untuk mengecek versi host virtual machine ketikan perintah :
   
   $ cat /etc/issue
	
	![7.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/7.cek_versi_vm_host.jpg)

8. Menjalankan MySql Container dengan perintah dibawah ini :
    
    $ docker container run \
 	--detach \
 	--name mydb \
 	-e MYSQL_ROOT_PASSWORD=my-secret-pw \
 	mysql:latest
	#### Penjelasan Script ####
	--detach untuk menjalankan 
 	--name mydb nama database ### mydb ###
 	-e untuk menetukan environment variabel password
	![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/8.run_background_mysql.jpg)

9. Menampilkan Container yang sedang berjalan dengan perintah :
    
    $ docker container ls
	
	![9.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/9.container_running_mysql.jpg)

10. Kita dapat mengecek apa saja yang terjadi di container menggunakan perintah :
    
    $ docker container logs mydb
	
	![10.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/10.docker_logs.jpg)
	atau 
    $ docker container top mydb
	 
	![10.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/11.docker_container_top_mydb.jpg)

11. Melihat versi MySql menggunakan perintah :
    
    $ docker exec -it mydb \
	mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version
	 
	![11.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/12.show_mysql_version.jpg)

12. Kita dapat menggunakan container exec untuk mengkoneksikan dan membuat proses baru di baris shell container yang sedang berjalan.
    
    $  docker exec -it mydb sh
	 
	![12.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/13.docker_container_exec_to_connect.jpg)

13. Selanjutnya kita cek MySql versi kemudian keluar dari proses menggunakan perintah :

    $ mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version
    $ exit
	
	![14.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/14.CEK_MYSQL_VERSION_ON_CONTAINER.jpg)

## Task 2: Package and run a custom app using Docker

14. Selanjutnya kita akan mencoba membuat dan menjalankan sebuah aplikasi menggunakan Dockerfile. 
Sebelumnya kita pastikan berada di dalam direktori linux_tweet_app dengan perintah :
    
    $  cd ~/linux_tweet_app
	Menampilkan isi dari Dockerfile 
    $ cat Dockerfile
	 
	![14.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/14.build_a_simple_website_images.jpg)
	
	## Penjelasan gambar
	
	FROM : sebagai titik awal data baru yang kita buat di mulai dari "nginx:latest"
	COPY : berguna untuk mengcopy file dari Host DOcker kedalam Container Image, dalam hal ini digunakan untuk menyalin dua file ke dalam gambar index.html yang akan di gunakan didalam web yang kita bangun.
	EXPOSE : Port yang digunakan oleh aplikasi
	CMD : menentukan perintah apa yang akan dijalankan saat container di jalankan.

15. Selanjutnya kita menggunakan docker image build untuk membuat Docker Image baru dalam Dockerfile :
    Sebelumnya kita lakukan langkah untuk mengexport DOCKERID kita, disini saya export DOCKERID=bondanproject/myrepo_9
    
    $ export DOCKERID=bondanproject/myrepo_9
    
    $  cat Dockerfile
    
    $  echo $DOCKERID
    
bondanproject/myrepo_9

    $ docker image build --tag $DOCKERID/linux_tweet_app:1.0 .
    
    Selengkapnya ada pada gambar dibawah ini :
    
![15.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/16.docker_myrepo_9_build_a_simple_website_images.jpg)

16. Selanjutnya kita menggunakan docker container run untuk memulai container baru dari image yang dibuat :

    $ docker container run \
	--detach \
 	--publish 80:80 \
 	--name linux_tweet_app \
 	$DOCKERID/linux_tweet_app:1.0
	Kemudian akses website :

![16.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/16.docker_container_run.jpg)

## Task 3: Modify a running website

17. Disini kita akan merubah dan sedikit memodifikasi tampilan web menggunakan mount :

    $ cp index-new.html index.html

![17.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/17.cp.jpg)

18. Selanjutnya mengcopy file index.html kedalam container 

Maka hasilnya akan seperti dibawah ini : 

![20.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/20.modify_web.jpg)
	
![21.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Pic/21.modify_web_index_html_cp.jpg)

	
## Software yang Diperlukan

Linux, Docker

```

