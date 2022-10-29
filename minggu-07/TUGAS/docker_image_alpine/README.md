# Tugas
## Container Docker Repository Alpine

[DockerHub](https://hub.docker.com/)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Tutorial Cara Install Docker dan membuat Container Docker di Ubuntu Server 22.04 Lts
Docker adalah Perangkat (PAaS) -Platform As a Service- Virtulasisasi Tingkat OS untuk mengirimkan perangkat lunak dalam bentuk container. Pertama - tama kita lakukan :

#### Install docker

    $ sudo apt install docker
    ![1_install_docker_ub_server.jpg]( {https://github.com/rbp-x/tekn-cloud-computing/blob/main/minggu-07/TUGAS/docker_image_alpine/1_install_docker_ub_server.jpg} )

#### Install docker-compose 

    $ sudo apt install docker-compose
     ![2_install_docker-compose_ub_server.jpg]( {https://github.com/rbp-x/tekn-cloud-computing/blob/main/minggu-07/TUGAS/docker_image_alpine/2_install_docker-compose_ub_server.jpg} )
    
#### Cek status running docker 

    $ sudo service docker status
    ![3_active_install_docker_ub_server.jpg]( {https://github.com/rbp-x/tekn-cloud-computing/blob/main/minggu-07/TUGAS/docker_image_alpine/3_active_install_docker_ub_server.jpg} )

#### Mencari Citra dari Alpine

    $ sudo docker search apline
    ![4_docker_search_alpine.jpg]( {https://github.com/rbp-x/tekn-cloud-computing/blob/main/minggu-07/TUGAS/docker_image_alpine/4_docker_search_alpine.jpg} )
    
#### Pull atau menambahkan/download docker container dari dockerhub repository Alpine

    $ sudo docker pull alpine
    ![5_docker_pull_alpine.jpg]( {https://github.com/rbp-x/tekn-cloud-computing/blob/main/minggu-07/TUGAS/docker_image_alpine/5_docker_pull_alpine.jpg} )
    
#### Menampilkan image alpine yang sudah di download 

    $ sudo docker images
    ![6_melihat_docker_image_yg_kita_buat_pull_dari_repo_alpine.jpg]( {https://github.com/rbp-x/tekn-cloud-computing/blob/main/minggu-07/TUGAS/docker_image_alpine/6_melihat_docker_image_yg_kita_buat_pull_dari_repo_alpine.jpg} )
    
#### Untuk menjalankan container alpine

    $ sudo docker run -it alpine 
    ![7_sukses_masuk_alpine_container.jpg.jpg]( {https://github.com/rbp-x/tekn-cloud-computing/blob/main/minggu-07/TUGAS/docker_image_alpine/7_sukses_masuk_alpine_container.jpg} )
    
    
# -- DONE -- #
