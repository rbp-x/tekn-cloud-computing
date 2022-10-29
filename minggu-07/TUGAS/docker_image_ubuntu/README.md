# Tugas
## Container Docker Repository Ubuntu

[DockerHub](https://hub.docker.com/)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Tutorial Cara Install Docker dan membuat Container Docker di Ubuntu Server 22.04 Lts
Docker adalah Perangkat (PAaS) -Platform As a Service- Virtulasisasi Tingkat OS untuk mengirimkan perangkat lunak dalam bentuk container. Pertama - tama kita lakukan :

#### Install docker

    $ sudo apt install docker

#### Install docker-compose 

    $ sudo apt install docker-compose
    
#### Cek status running docker 

    $ sudo service docker status

#### Mencari Citra dari Ubuntu

    $ sudo docker search ubuntu
    
#### Pull atau menambahkan/download docker container dari dockerhub repository Ubuntu

    $ sudo docker pull ubuntu
    
#### Menampilkan image ubuntu yang sudah di download 

    $ sudo docker images
    
#### Untuk menjalankan container ubuntu

    $ sudo docker run -it ubuntu 
    
    
# -- DONE -- #