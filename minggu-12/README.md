# Laporan, Latihan dan Tugas Praktikum Teknologi Cloud Computing - Minggu 12 
#### Rahadiyan Bondan Permadi
##### 215411119

## Docker Orchestration Hands-on Lab


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
   
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/2.checkou_data_step0.jpg)


melihat info docker

    $ docker ps

#### docker ps
   
![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/3.cat_link_py.jpg)

#### Step 2.1 - Create a Manager node

#### Inisialisasi New Swarm

   $ docker swarm init --advertise-addr $(hostname -i)

![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/3.cat_link_py.jpg)

   $ docker info

![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/3.cat_link_py.jpg)

![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/3.cat_link_py.jpg)

#### Step 2.2 - Join Worker nodes to the Swarm

	Paste On Node 1 and Node 2

    $ docker swarm join --token SWMTKN-1-4jyeeeomwfddfbrhwib18kq08m7xisto1l0m3i5n8gpxbj1qy1-a6tizbli7zy4lm9nskm4ulhcw 192.168.0.18:2377

![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/6.run_python_program.jpg)

    $ docker node ls

![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/6.run_python_program.jpg)

#### Section 3: Deploy applications across multiple hosts
#### Step 3.1 - Deploy the application components as Docker services

    $ docker service create --name sleep-app ubuntu sleep infinity

![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/6.run_python_program.jpg)

    $ docker service ls

![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/6.run_python_program.jpg)

#### Section 4: Scale the application

    $ docker service update --replicas 7 sleep-app

![7.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/6.run_python_program.jpg)

    $ docker service ps sleep-app

![7.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/6.run_python_program.jpg)

    $ docker service update --replicas 4 sleep-app

![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/7.step1_checkout.jpg)

    $ docker service ps sleep-app

![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/7.step1_checkout.jpg)
 
#### Section 5: Drain a node and reschedule the containers

    $ cat Dockerfile

![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/8.cat_Dockerfile.jpg)

    $ docker node ls

![9.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/9.install_py_pip.jpg)

    $ docker node ls

![9.2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/9.install2_py_pip.jpg)

![9.3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/9.install3_py_pip.jpg)

![10.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-09/Application%20Containerization%20and%20Microservice%20Orchestration/Pict/9.install3_py_pip.jpg)



## Software yang Diperlukan

Linux, Docker

```

