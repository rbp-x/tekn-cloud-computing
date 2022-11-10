# Latihan Praktikum Teknologi Cloud Computing - Minggu 8 
#### Rahadiyan Bondan Permadi
##### 215411119


## Materi

**Docker Network**

#### membuka menu docker network

    $ sudo docker network
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/1_docker_network_ls.jpg)

#### melihat daftar jaringan yang ada menggunakan perintah ls

    $ sudo docker network ls
![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/2_create_new_network.jpg)

#### menambahkan network baru

    $ sudo docker network create --subnet 192.176.60.56/24 tcc-rbp-pertemuan-ke8
![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/2_create_new_network.jpg)

#### cek kembali daftar jaringan setelah adanya penambahan

    $ sudo docker network ls
![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/2_create_new_network.jpg)

#### jika sukses selanjutnya ke tahap running kontainer dengan menggunakan image httpd seperti dibawah

    $ sudo docker run -d --network tcc-rbp-pertemuan-ke8 --ip 192.176.60.56 httpd
![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/3_running_container_dg_new_network_from_image_httpd.jpg)
![6.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/4_pulling_image_container_dg_new_network_httpd.jpg)

#### pastikan kontainer tidak ada error menggunakan perintah 

    $ sudo docker network ps
![7.jp](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/5_cek_kontainer.jpg)

#### pastikan status sudah UP dengan mengeceknya dg perintah 

    $ sudo docker network inspect tcc-rbp-pertemuan-ke8
![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/6_cek_address_kontainer.jpg)

#### Menghapus network 
    $ sudo docker network rm "nama network"
![9.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/7_hapus_network.jpg)

#### membuat Container dengan nama node1 dan node2 dari image engine stable-alpine yang udah tersedia 
    $ docker run -d --name node1 --network tcc-net nginx:stable-alpine
    $ docker run -d --name node2 --network tcc-net nginx:stable-alpine    
![10.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/8_membuat_container.jpg)

#### memeriksa network yang kita buat menggunakan perintah : 
    $ docker network inspect tcc-net
![11.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/9_inspect_network_node1_node2.jpg)

#### memeriksa koneksi container node1 dan node2 didalam network yang kita buat menggunakan perintah : 
    $ docker exec node1 ping node2 
![12.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/10_uji_ping_container_node1_node2.jpg)

#### memeriksa koneksi birdge sebagai default network menggunakan perintah : 
    $ docker network inspect bridge
![13.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/11_inspect_default_bridge.jpg)

#### membuat container nodeX untuk pengujian selanjutnya menggunakan perintah : 
    $ docker container create --name nodeX nginx:stable-alpine
![14.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/12_membuat_container_nodeX_blm_ada_ipNya.jpg)

#### Start container nodeX untuk pengujian selanjutnya menggunakan perintah : 
    $ docker start nodeX 
![15.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/13_docker_start_nodeX.jpg)
![16.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/14_docker_container_nodeX_started.jpg)

#### menghubungkan container nodeX ke network tcc-net dengan perintah : 
    $ docker network connect tcc-net nodeX 
![17.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/15_pindahkan_container_nodeX_ke_network_tcc-net.jpg)

#### uji konektivitas antar node / container nodeX dengan node1 dan node2 dengan perintah : 
    $ docker network connect tcc-net nodeX 
![18.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/16_nodeX_ping_node1_sukses.jpg)
![19.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/17_nodeX_ping_node2_sukses.jpg)

#### melihat masing - masing network dan container yang berhasil ditambahkan dan dijalankan : 
    $ docker network connect tcc-net nodeX 
![20.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Network/Pic/18_hasil_bertambah_masing_masing_container.jpg)

## Sekian untuk management Docker Network





