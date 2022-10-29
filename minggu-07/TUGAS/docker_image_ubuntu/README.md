# Tugas
## Container Docker Repository Ubuntu

[DockerHub](https://hub.docker.com/)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Tutorial Cara Install Docker dan membuat Container Docker di Ubuntu Server 22.04 Lts
Docker adalah Perangkat (PaAS) -Platform as A Service- Virtulasisasi Tingkat OS untuk mengirimkan perangkat lunak dalam bentuk container. Pertama - tama kita lakukan :

#### Install docker

    $ sudo apt install docker
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-07/TUGAS/docker_image_alpine/1_install_docker_ub_server.jpg)

#### Install docker-compose 

    $ sudo apt install docker-compose
![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-07/TUGAS/docker_image_alpine/2_install_docker-compose_ub_server.jpg)

#### Cek status running docker 

    $ sudo service docker status
![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-07/TUGAS/docker_image_alpine/3_active_install_docker_ub_server.jpg)

#### Mencari Citra dari Ubuntu

    $ sudo docker search ubuntu
![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-07/TUGAS/docker_image_ubuntu/1_docker_image_ubuntu.jpg)
    
#### Pull atau menambahkan/download docker container dari dockerhub repository Ubuntu

    $ sudo docker pull ubuntu
![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-07/TUGAS/docker_image_ubuntu/2_docker_pull_ubuntu_image.jpg)

#### Menampilkan image ubuntu yang sudah di download 

    $ sudo docker images
![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-07/TUGAS/docker_image_ubuntu/3_docker_images.jpg) 

#### Untuk menjalankan container ubuntu

    $ sudo docker run -it ubuntu 
![7.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-07/TUGAS/docker_image_ubuntu/5_updated_docker_image_ubuntu.jpg)
    
    
#### Kita coba install apache2

    $ apt install apache2
![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-07/TUGAS/docker_image_ubuntu/6_install_apache2_on_ubuntu_container.jpg)

![9.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-07/TUGAS/docker_image_ubuntu/7_install_apache2_on_ubuntu_container.jpg)
    
    
#### Untuk cek status running paket apache2 container ubuntu

    $ service apache2 status
![10.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-07/TUGAS/docker_image_ubuntu/8_apache2_running_ubuntu_container.jpg)
    
   
    
# -- DONE -- #
