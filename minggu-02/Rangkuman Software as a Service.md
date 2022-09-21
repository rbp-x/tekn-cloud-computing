# Rangkuman Software as a Service
## Perbedaan antara IaaS, SaaS dan PaaS

**IaaS (Infrastructure as a Service)** 
<br>Adalah model *cloud service*  dimana sumber daya komputasinya disediakan secara virtual sehingga penggunanya memiliki kendali penuh terhadap infrastruktur yang digunakan, mulai dari server, jaringan, sistem operasi, storage dan ruang data center. Pengguna juga dapat membuat `pusat data virtual` di cloud dan memiliki akses ke seluruh data tanpa harus memiliki hardware atau perangkat sendiri. 
Beberapa contoh dari SaaS yaitu Digital Ocean, Amazon Web Services (AWS), Linode, Rackspace, Google Compute Engine (GCE), Microsoft Azure, Cisco Metapod, dll.

**SaaS (Software as a Service)**
<br>Adalah suatu lisensi perangkat lunak dan *delivery* model berbasis *cloud*, sehingga memungkinkan penggunanya untuk tetap mengakses suatu software dimanapun, kapanpun dan dengan device apapun asalkan terkoneksi dengan internet. Dalam SaaS, pengguna tidak perlu lagi melakukan install, update, atau menangani masalah pada software yang digunakan karena semua hal tersebut telah dikelola oleh vendor karena pengguna hanya perlu menggunakan service yang disediakan. 
Beberapa contoh dari SaaS yaitu Google Apps, Salesforce, Hubspot, Zendesk, Slack, Ahrefs, Semrush, Majestic SEO, Drop Box, Mailchimp, dll.

**Platform as a Service (PaaS)**
<br>Adalah model *cloud service* berupa framework yang dapat digunakan oleh pengguna (developer) untuk membangun/membuat sebuah perangkat lunak (aplikasi). Sistem operasi, server dan segala kebutuhan yang diperlukan oleh pengguna telah disediakan oleh vendor, sehingga memungkinkan bagi pengguna untuk lebih fokus dalam pengembangan perangkat lunak.
Beberapa contoh PaaS yaitu Google App Engine, Windows Azure, AWS Elastic Beanstalk, dll.

## SaaS (Software as a Service)

Dengan model SaaS, sebuah aplikasi dengan satu konfigurasi dapat digunakan untuk semua pelanggan. Hal itu dikarenakan aplikasi tersebut diinstal pada beberapa mesin untuk mendukung skalabilitas atau disebut dengan penskalaan horizontal.

![1](SaaSArchitecture.jpeg)

Terdapat 2 jenis utama dari SaaS, yaitu.

**SaaS Vertical** adalah sebuah perangkat lunak yang digunakan untuk kebutuhan sebuah industri tertentu, sehingga cenderung lebih terfokus pada satu bidang industri saja. Misalnya perangkat lunak untuk kebutuhan industri kesehatan, pertanian, real estate, keuangan, dll.

**SaaS Horizontal** adalah sebuah perangkat lunak yang berfokus pada sebuah produk, sehingga cakupan bisnis dan industrinya lebih luas dibanding SaaS Vertical. Misalnya perangkat lunak untuk kebutuhan pemasaran, penjualan, alat pengembang, SDM, dll.

Manfaat SaaS yaitu pengguna dapat secara langsung menggunakan layanan tanpa harus atau menginstall atau membuat sendiri (in-house development). Pengguna tidak perlu khawatir tentang ketersediaan dan reliabilitas aplikasi, karena telah dijamin oleh penyedia layanan sehingga pengguna hanya perlu fokus pada data yang dimiliki saja.

## Kelebihan & Kekurangan SaaS (Software as a Service)

Kelebihan:
- Keamanan
- Kesesuaian
- Sederhana
- Ekonomis

Kekurangan:
- Performa
- Permasalahan data
- Kurang dalam hal akses kontrol
- Ekosistem terbatas

## Cara Membangun Aplikasi SaaS berbasis Cloud

1. Pilih bahasa pemograman yang tepat (Contohnya Python karena lebih fleksibel dalam banyak kasus)

2. Pilih database yang tepat (Database Document Oriented seperti MongoDB)

3. Pilih sistem antrian yang tepat (Yaitu sebuah protokol komunikasi asinkron yang memungkinkan pengirim dan penerima berinteraksi disaat yang sama atau dikenal dengan MSMQ, seperti RabbitMq)

Dengan Python, MongoDB dan RabbitMQ kiranya telah mencukupi dalam dasar pembangunan SaaS. Mungkin akan ada penambahan lain seperti kebutuhan software pemantauan dan analitik yang tepat.

### Referensi:
1. [What is the difference between IaaS, SaaS, and PaaS?](https://www.quora.com/What-is-the-difference-between-IaaS-SaaS-and-Paas). 
2. [SaaS Platform Architecture](https://hackernoon.com/saas-software-as-a-service-platform-architecture-757a432270f5).
3. [SaaS (Software as a Service) Platform  itecture](https://www.devteam.space/blog/saas-software-as-a-service-platform-architecture/).
4. [How to build a cloud-based SaaS Application](https://usersnap.com/blog/cloud-based-saas-architecture-fundamentals/).