# Install Docker on Ubuntu 22.04

## Latihan

1.  Install Docker sesuai petunjuk pada `Materi dan Pembahasan` di atas, sesuaikan dengan OS yang anda gunakan.
2.  Kerjakan no 4 pada `Materi dan Penjelasan` di atas.

**Teknologi Virtualisasi dan *Container* - Docker**

1.  Pengertian *container* dan keterkaitannya dengan Docker
2.  Instalasi Docker

## Download Software yang Diperlukan

* [Docker](https://docs.docker.com/get-docker/).

## Latihan Install

2.  [Artikel tentang Docker di Wikipedia](https://en.wikipedia.org/wiki/Docker_(software))
3.  [Instalasi Docker](https://docs.docker.com/install/)
4.  [Get Started - Docker](https://docs.docker.com/get-started/)
5.  [Dokumentasi DockerHub](https://docs.docker.com/docker-hub/)


## Download dan Install Docker

Donwload [Docker](https://docs.docker.com/get-docker/). 

## Install using the repository

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

## Set up the repository

    1. Update the apt package index and install packages to allow apt to use a repository over HTTPS:

    sudo apt-get update

    sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
    
    2. Add Docker’s official GPG key:
    $ sudo mkdir -p /etc/apt/keyrings
    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    
    3. Use the following command to set up the repository:
    $ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
  ## Install Docker Engine
  1. Install Docker Engine
  $ sudo apt-get update
  2. Install Docker Engine, containerd, and Docker Compose.
  $ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
  3. Verify that the Docker Engine installation is successful by running the hello-world image:
  $ sudo docker run hello-world
  
  


  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  