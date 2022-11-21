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

![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/1.docker_network.jpg)

Daftar docker network

      $ docker network ls

![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/2.docker_network_ls.jpg)

Inspect a network

      $ docker network inspect bridge

![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/3.inspect_docker_network.jpg)

Docker info

      $ docker info

![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/4.docker_info.jpg)


Section #2 - Bridge Networking

daftar docker network 

      $ docker network ls

![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/5.docker_network_ls.jpg)


Selanjutnya kita mulai install dulu brctl dengan perintah 

      $ sudo apt-get install bridge-utils

![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/6.install_bridge_utils.jpg)

      $ brctl show

![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/6.brctl_show.jpg)

menampilkan detail dari docker0

      $ ip a

![7.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/7.ip_a.jpg)

Membuat container baru dengan menjalankan perintah :

      $ docker run -dt ubuntu sleep infinity

![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/8.create_container.jpg)

![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/8.create_container_2.jpg)

Memverivikasi container

      $ docker ps

![9.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/9.docker_ps.jpg)

Kembali kita tampilkan bridge-utils menggunakan 

      $ brctl show

![10.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/10.brctl_show.jpg)

kita inspect kembali menggunakan perintah 

      $ docker network inspect bridge

![11.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/11.inspect_bridge.jpg)

Lakukan ping dengan 172.17.0.2

      $ ping -c5 172.17.0.2

![12.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/12.ping.jpg)

Docker ps

      $ docker ps

![13.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/13.docker_ps.jpg)

sekarang kita coba menjalankan didalam shell container ubuntu dengan perintah :

      $ docker exec -it fa39e102f0a4 /bin/bash

![14.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/14.docker_exec.jpg)

Selanjutnya kita install program ping dengan menjalankan perintah dibawah ini :

      $ apt-get update && apt-get install -y iputils-ping

![15.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/15.install_program_ping.jpg)

selanjutnya kita coba koneksi dengan ping ke github

      $ ping -c5 www.github.com

![16.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/16.ping_docker_com.jpg)

Konfigurasi NAT untuk koneksi luar dengan memulai membuat container baru nginx

      $ docker run --name web1 -d -p 8080:80 nginx

![17.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/17.nginx.jpg)

      $ docker ps

![18.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/18.docker_ps.jpg)

kita buka web dengan durl 

      $ curl 127.0.0.1:8080

![19.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/19.curl.jpg)


Section #3 - Overlay Networking
Cleaning Up

Pada langkah ini kita akan menginisialisasi swarm baru konek dengan node dan memverivikasinya.

Jalankan perintah berikut ini :

      $ docker swarm init --advertise-addr $(hostname -i)

gambar 20

Jalankan docker-swarm-join

      $ docker swarm join --token SWMTKN-1-28egcsrt15whmx4a5i9n6u3d7blnhip4bik468xm95l9kuuaxr-68l5e9lr62nyscynu9ui3ewym 192.168.0.27:2377

	$ docker node ls

gambar 21

Membuat jaringan overlay

	$ docker network create -d overlay overnet
	$ docker network ls

gambar 22
gambar 23
	
Jalankan juga di terminal kedua 
	
	$ docker network ls

gambar 24

Kita inspect overnet

	$ docker network inspect overnet

gambar 25

# Step 3 Saatnya membuat layanan menggunakan jaringan yang sudah terinisialisasi

	$ docker service create --name myservice \
	--network overnet \
	--replicas 2 \
	ubuntu sleep infinity
	
	$ docker service ls

gambar 26
gambar 26

Memverifikasi single task (replika)

	$ docker service ps myservice

gambar 27

	$ docker network ls

gambar 28

	$ docker network inspect overnet

gambar 29

Test jaringan 

	$ docker network inspect overnet

gambar 30

	$ docker ps

gambar 31

install 
	
	$ docker exec -it e345aed47cba /bin/bash

GAMBAR 32

	$ apt-get update && apt-get install -y iputils-ping

gambar 33
	
test ping 10.0.0.3

	$ ping 10.0.0.3 

gambar 34

	$ cat /etc/resolv.conf

gambar 35

ping myservice
	
	$ ping -c5 myservice

gambar 36

docker inspect myservice

	$ docker service inspect myservice

gambar 37

# cleaning up

	$ docker service rm myservice

gambar 38

	$ docker ps

gambar 39

	$ docker kill 3ae8a2ac8297

gambar 40

	$ docker swarm leave --force

gambar 41

	
## Software yang Diperlukan

Linux, Docker

```

containerid

node1 3ae8a2ac8297
node2 ff36aa7e91e7

# Selesai
