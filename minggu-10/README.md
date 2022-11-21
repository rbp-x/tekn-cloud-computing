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

![20.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/20.docker_swarm_init.jpg)

Jalankan docker-swarm-join

      $ docker swarm join --token SWMTKN-1-28egcsrt15whmx4a5i9n6u3d7blnhip4bik468xm95l9kuuaxr-68l5e9lr62nyscynu9ui3ewym 192.168.0.27:2377

	$ docker node ls

![21.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/21.docker_swarm_join.jpg)

Membuat jaringan overlay

	$ docker network create -d overlay overnet
	$ docker network ls

![22.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/22.create_overlay_network.jpg)
![23.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/23.docker_network_ls.jpg)
	
Jalankan juga di terminal kedua 
	
	$ docker network ls

![24.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/24.docker_network_ls_on_second_console.jpg)

Kita inspect overnet

	$ docker network inspect overnet

![25.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/25.docker_network_overnet.jpg)

# Step 3 Saatnya membuat layanan menggunakan jaringan yang sudah terinisialisasi

	$ docker service create --name myservice \
	--network overnet \
	--replicas 2 \
	ubuntu sleep infinity	
	
![26.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/26.create_service.jpg)
	
	$ docker service ls

![26.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/26.create_service_ls.jpg)

Memverifikasi single task (replika)

	$ docker service ps myservice

![27.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/27.docker_service_ps.jpg)

	$ docker network ls

![28.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/28.docker_network_ls.jpg)

	$ docker network inspect overnet

![29.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/29.docker_network_ls_inspect.jpg)

Test jaringan 

	$ docker network inspect overnet

![30.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/30.docker_network_inspect_overnet.jpg)

	$ docker ps

![31.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/31.%20docker_ps.jpg)

install 
	
	$ docker exec -it e345aed47cba /bin/bash

![32.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/32.docker_exec.jpg)

	$ apt-get update && apt-get install -y iputils-ping

![33.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/33.install.jpg)
	
test ping 10.0.0.3

	$ ping 10.0.0.3 

![34.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/34.test_ping.jpg)

	$ cat /etc/resolv.conf

![35.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/35.cat.jpg)

ping myservice
	
	$ ping -c5 myservice

![36.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/36.ping_myservice.jpg)

docker inspect myservice

	$ docker service inspect myservice

![37.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/37.docker_inspect.jpg)

# cleaning up

	$ docker service rm myservice

![38.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/38.cleaningup.jpg)

	$ docker ps

![39.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/39.docker_ps.jpg)

	$ docker kill 3ae8a2ac8297

![40.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/40.docker_kill.jpg)

	$ docker swarm leave --force

![41.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-10/Pict/41.docker_leave.jpg)

	
## Software yang Diperlukan

Linux, Docker, Docker Network, Docker Swarm

```

containerid

node1 3ae8a2ac8297
node2 ff36aa7e91e7

# Selesai
