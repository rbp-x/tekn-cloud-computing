# Tugas Praktikum Teknologi Cloud Computing - Minggu 8 
#### Rahadiyan Bondan Permadi
##### 215411119


## Materi

**Docker Network**

#### membuka menu docker network

    $ sudo docker network

#### melihat daftar jaringan yang ada menggunakan perintah ls

    $ sudo docker network ls

#### menambahkan network baru

    $ sudo docker network create --subnet 192.176.60.56/24 tcc-rbp-pertemuan-ke8

#### cek kembali daftar jaringan setelah adanya penambahan

    $ sudo docker network ls

#### jika sukses selanjutnya ke tahap running kontainer dengan menggunakan image httpd seperti dibawah

    $ sudo docker run -d --network tcc-rbp-pertemuan-ke8 --ip 192.176.60.56 httpd

#### pastikan kontainer tidak ada error menggunakan perintah 

    $ sudo docker network ps


#### pastikan status sudah UP dengan mengeceknya dg perintah 

    $ sudo docker network inspect tcc-rbp-pertemuan-ke8

