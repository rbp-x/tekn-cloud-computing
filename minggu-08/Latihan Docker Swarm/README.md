# Latihan Praktikum Teknologi Cloud Computing - Minggu 8 
#### Rahadiyan Bondan Permadi
##### 215411119


## Materi

**Docker Swarm**


#### inisialisasi docker swarm

    $ docker swarm init

#### status docker swarm 

    $ docker info | grep -i swarm

#### status docker node yang sudah join ke swarm dengan perintah 

    $ docker node ls

#### add node to swarm, memerlukan join token dari token yang kita dapatkan ketika inisialisasi swarm pada gambar pertama diatas :

    $ docker swarm join-token worker

	docker swarm join --token 	SWMTKN-1-5w2527mejpqx0tg52pkv74w037eopa0yu9q3zw5foou09eod0x-7r3sfk4kbfea9z67hza7ir0ix 192.176.60.56:2377