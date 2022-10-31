# Latihan Praktikum Teknologi Cloud Computing - Minggu 8 
#### Rahadiyan Bondan Permadi
##### 215411119


## Materi

**Docker Compose**
Docker compose digunakan untuk otomisasi proses - proses manual sebelumnya yang sudah kita buat (multi container dijalankan). 
Pertama kita buat file - file terlebih dahulu sesuai dengan arahan.


#### Install docker compose

    $ sudo install docker-compose
![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/1_install_docker-compose_ub_server.jpg)

#### manualy install docker-compose

    $ DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
    $ mkdir -p $DOCKER_CONFIG/cli-plugins
    $ curl -SL https://github.com/docker/compose/releases/download/v2.12.2/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose
    $ chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose

![1.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/1_install_docker-compose_ub_server_manualy.jpg)

#### Membuat dirketori/folder project (composetest)

    $ mkdir composetest
    $ cd composetest
   
![2.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/2_create_a_directory_project.jpg)

#### Membuat file app.py yang akan di panggil

	import time

	import redis
	from flask import Flask

	app = Flask(__name__)
	cache = redis.Redis(host='redis', port=6379)

	def get_hit_count():
    	retries = 5
    	while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)

	@app.route('/')
	def hello():
    	count = get_hit_count()
    	return 'Hello World! I have been seen {} times.\n'.format(count)
	
![3.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/4_create_file_app_py.jpg)	
![4.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/3_create_file_app_py.jpg)


#### Membuat file lainnya yaitu requirements.txt yang akan di panggil
	
	$ nano requirments.txt

	flask
	redis

![5.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/5_create_file_requirements_txt.jpg)
![6.jpg](https://github.com/rbp-x/tekn-cloud-computing/blob/main/minggu-08/Latihan%20Docker%20Compose/pic/6_create_file_requirements_txt.jpg)

# Membuat file Docker / Dockerfile

#### Dockerfile berfungsi untuk membuild docker image dan bersii semua package/dependensi dari python bahkan python itu sendiri.
	$ nano Dockerfile (tanpa ekstensi apapun!)

![7.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/7_membuat_dockerfile.jpg)

di isi dengan code dibawah ini :

	# syntax=docker/dockerfile:1
	FROM python:3.7-alpine
	WORKDIR /code
	ENV FLASK_APP=app.py
	ENV FLASK_RUN_HOST=0.0.0.0
	RUN apk add --no-cache gcc musl-dev linux-headers
	COPY requirements.txt requirements.txt
	RUN pip install -r requirements.txt
	EXPOSE 5000
	COPY . .
	CMD ["flask", "run"]

# hasilnya
![8.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/8_membuat_dockerfile.jpg)

#### Membuat file docker-compose.yml

	version: "3.9"
	services:
 	 web:
 	   build: .
 	   ports:
 	     - "8000:5000"
	 redis:
    	   image: "redis:alpine"

![9.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/9_create_docker_compose_yml.jpg)

# Build and run app dengan docker compose

	$ docker compose up
![10.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/10_docker_compose_up.jpg)
![11.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/11_docker_compose_up.jpg)
![12.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/12_docker_compose_up.jpg)
![13.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/13_compose_pulls_redis_images.jpg)

#### Build on server remote windows :
![14.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/14_compose_up_pul_from_server_to_remote.jpg)
![14.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/14_w3m_http_localhost_8000.jpg)

#### refresh sesion 1 - 2

![15.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/15_w3m_http_localhost_8000_to_remote.jpg)
![15.jpg](https://github.com/rbp-x/tekn-cloud-computing/blob/main/minggu-08/Latihan%20Docker%20Compose/pic/15_w3m_http_localhost_8000_to_remote_1.jpg)

#### Docker image list
![16.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/16_docker_image_list.jpg)

#### stop docker compose yang sedang berjalan menggunakan Ctrl + C atau menggunakan perintah :

	$ docker compose down

![17.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/17_docker_compose_down.jpg)

# Edit Compose File menambahkan "bind mount" untuk web service untuk mempermudah pengelolaan volume pada container

	$ nano docker-compose.yml

	version: "3.9"
	services:
  	 web:
    	  build: .
    	  ports:
         - "8000:5000"
        volumes:
         - .:/code
        environment:
         FLASK_DEBUG: True
      redis:
        image: "redis:alpine" 
	
![18.jpg](https://raw.githubusercontent.com/rbp-x/tekn-cloud-computing/main/minggu-08/Latihan%20Docker%20Compose/pic/18_nano_composetest_yml_add_bind_mount_volume.jpg)

# Rebuild dan Run app with Compose
	$ docker compose up

(on proses maping volume)
