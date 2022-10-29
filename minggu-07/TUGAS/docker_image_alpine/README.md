# Tugas
## Container Docker Repository Alpine

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

#### Mencari Citra dari Alpine

    $ sudo docker search apline
    
#### Pull atau menambahkan/download docker container dari dockerhub repository Alpine

    $ sudo docker pull alpine
    
#### Menampilkan image alpine yang sudah di download 

    $ sudo docker images
    
#### Untuk menjalankan container alpine

    $ sudo docker run -it alpine 
    
    
# -- DONE -- #