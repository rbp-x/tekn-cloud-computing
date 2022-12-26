# Laporan Praktikum Teknologi Cloud Computing - Minggu 13
#### Rahadiyan Bondan Permadi
##### 215411119

## Learn Kubertentes Basics


## Materi
 
# Di lab ini, kita akan bermain-main dengan container orchestration pada Docker. Kita akan menerapkan aplikasi sederhana ke satu host dan mempelajari cara kerjanya. Kemudian, kita mengonfigurasi Docker Swarm, dan belajar menerapkan aplikasi sederhana yang sama di beberapa host. Kemudian kita akan melihat cara menskalakan aplikasi dan memindahkan beban kerja ke berbagai host dengan mudah.

## Tujuan

1.  Mahasiswa mampu menerapkan dan memahami aplikasi sederhana ke satu host dan mempelajari cara kerjanya.
2.  Mahasiswa mampu mengkonfigurasikan Docker Swarm dan menerapkan beberapa aplikasi yang sama dalam beberapa host.
3.  Mahasiswa mampu menskalakan aplikasi dan memindahkan beban kerja ke berbagai host dengan mudah.


## Pembahasan

Langkah - langkah Praktikum

Section 2

### Configure Swarm Mode

#### Step 2. Menjalankan berbagai hal secara manual pada satu host dan membuat wadah baru di node1 dengan menjalankan

Login Docker : run

    $ docker run -dt ubuntu sleep infinity
   
#### Node 1
   
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/1.%20Node%201.jpg)


melihat info docker

    $ docker ps

#### docker ps
   
![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/2.%20docker-ps.jpg)

#### Step 2.1 - Create a Manager node

#### Inisialisasi New Swarm

   $ docker swarm init --advertise-addr $(hostname -i)

![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/3.%20docker%20swarm.jpg)

   $ docker info

![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/4.%20docker%20info%202.jpg)

![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/4.%20docker%20info.jpg)

#### Step 2.2 - Join Worker nodes to the Swarm

	Paste On Node 1 and Node 2

    $ docker swarm join --token SWMTKN-1-4jyeeeomwfddfbrhwib18kq08m7xisto1l0m3i5n8gpxbj1qy1-a6tizbli7zy4lm9nskm4ulhcw 192.168.0.18:2377

![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/5.join%20node-2-3.jpg)

    $ docker node ls

![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/5.joined%20node-2-3.jpg)

#### Section 3: Deploy applications across multiple hosts
#### Step 3.1 - Deploy the application components as Docker services

    $ docker service create --name sleep-app ubuntu sleep infinity

![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/6.docker%20service%20ls.jpg)

    $ docker service ls

![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/6.docker%20sleep.jpg)

#### Section 4: Scale the application

    $ docker service update --replicas 7 sleep-app

![7.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/7.docker%20sleep.jpg)

    $ docker service ps sleep-app

![7.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/7.docker%20sleep2.jpg)

    $ docker service update --replicas 4 sleep-app

![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/8.docker%20slepp.jpg)

    $ docker service ps sleep-app

![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/8.docker%20slepp2.jpg)
 
#### Section 5: Drain a node and reschedule the containers

    $ cat Dockerfile

![9.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/9.docker%20node%20ls.jpg)

    $ docker node ls

![10.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-12/Pict/10.docker%20node%20.jpg)


## Software yang Diperlukan

Linux, Docker

```

