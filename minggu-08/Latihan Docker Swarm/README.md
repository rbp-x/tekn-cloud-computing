# Latihan Praktikum Teknologi Cloud Computing - Minggu 8 
#### Rahadiyan Bondan Permadi
##### 215411119


## Materi

**Docker Swarm**


#### inisialisasi docker swarm

    $ docker swarm init
    
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Swarm/Pic/1_docker_swarm_init.jpg)

#### status docker swarm 

    $ docker info | grep -i swarm

![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Swarm/Pic/2_docker_swarm_info_active.jpg)


#### status docker node yang sudah join ke swarm dengan perintah 

    $ docker node ls

![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Swarm/Pic/3_docker_node_ls_menampilkan_node_join_ke_swarm.jpg)

#### add node to swarm, memerlukan join token dari token yang kita dapatkan ketika inisialisasi swarm pada gambar pertama diatas :

    $ docker swarm join-token worker

![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Swarm/Pic/4_join_node_worker_to_swarm.jpg)


