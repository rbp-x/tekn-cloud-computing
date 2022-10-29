# Latihan Praktikum Teknologi Cloud Computing - Minggu 8 
#### Rahadiyan Bondan Permadi
##### 215411119


## Materi

**Docker Network**

#### membuka menu docker network

    $ sudo docker network
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan/1_docker_network_ls.jpg)

#### melihat daftar jaringan yang ada menggunakan perintah ls

    $ sudo docker network ls
![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan/2_create_new_network.jpg)

#### menambahkan network baru

    $ sudo docker network create --subnet 192.176.60.56/24 tcc-rbp-pertemuan-ke8
![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan/2_create_new_network.jpg)

#### cek kembali daftar jaringan setelah adanya penambahan

    $ sudo docker network ls
![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan/2_create_new_network.jpg)

#### jika sukses selanjutnya ke tahap running kontainer dengan menggunakan image httpd seperti dibawah

    $ sudo docker run -d --network tcc-rbp-pertemuan-ke8 --ip 192.176.60.56 httpd
![5.jp](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan/3_running_container_dg_new_network_from_image_httpd.jpg)
![6.jppg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan/4_pulling_image_container_dg_new_network_httpd.jpg)

#### pastikan kontainer tidak ada error menggunakan perintah 

    $ sudo docker network ps
![7.jp](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan/5_cek_kontainer.jpg)

#### pastikan status sudah UP dengan mengeceknya dg perintah 

    $ sudo docker network inspect tcc-rbp-pertemuan-ke8
![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan/6_cek_address_kontainer.jpg)

