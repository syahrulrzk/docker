<p align="center"><img src="https://drive.google.com/uc?export=view&id=1B2skhoyxRxEG60l5DMdkfjHKOCBFRllZ"></p>

# Perintah Dasar dan Cara Pengunaan nya!
### 1. Melihat Images.
<pre>$ docker images</pre>

### 2. Download Images.
<pre>$ docker pull debian (latest)
$ docker pull debian:9.8 (certain version)</code></pre>

### 3. Melihat Docker Container yang sedang running.
<pre> $ docker cotainer ls </pre>

### 4. Melihat semua list Docker Container.</p>
<pre> $ docker container ls -a</pre>

### 5. Membuat Docker Container.
<pre> $ docker container create --name mongodb1 mongo:4.0</code></pre>

### 6. Start Container.
<pre> $ docker container start mongodb1</code></pre>

### 7. Mencari Images.
<pre> $ docker search mysql</code></pre>

### 8. Stop Container.
<pre> $ docker container stop mongodb1</code></pre>

### 9. Menghapus Container.
<pre> $ docker container rm mongodb1</code></pre>

### 10. Membuat Container yang dapat diakses dari host. Dengan kata lain, membuka port pada Container sehingga service yang dijalankan dapat diakses dari luar.
<pre> $ docker container create --name mongodb2 -p 1234:27017 mongo</code></pre>

### 11. Menjalankan Images secara langsung. Sehingga, container akan otomatis terbentuk dari Image tersebut.
<pre class="wp-block-code"><code class="">$ docker run -itd mongo</code></pre>

### 12. Menjalankan Image secara langsung dan otomatis membuat container. 
<p>Dan juga membuka port untuk container tersebut. Contohnya pada Image mysql/mysql-server</p>
<pre> $ docker run -d --name mysqlserver1 -p 1234:3306 mysql/mysql-server</code></pre>

## 13. Masuk ke dalam Container.
<pre> $ docker exec -it mongodb2 bash</code></pre>
<p>Nanti mungkin anda akan menemui beberapa sedikit masalah, seperti Image yang tidak bisa di start dengan perintah<code>:</code></p>
<pre> $ docker container start namacontainer</code></pre>

<p>walaupun Container tersebut sudah dibuat sebelumnya. Tetapi Image tersebut akan jalan ketika langsung dijalankan dari Image-nya, contohnya seperti <strong><em>mysql</em></strong> atau <strong><em>mysql/mysql-server</em></strong>. </p>

<p>Jadi ada langkah tertentu untuk menjalankan Image tertentu. Seperti <strong><em>mysql/mysql-server</em></strong>, anda bisa melihat dokumentasi resminya. Container mysql dapat di jalankan dengan perintah : </p>

<pre> $ docker run -itd --name mysqlserver1 -p 1234:3306 mysql/mysql-server </pre>
<p>Ketika dilihat pada running Container, maka Container tersebut langsung berjalan. </p>
<p>Jadi perintah tersebut akan membuat container otomatis dari image <strong><em>mysql/mysql-server</em></strong>. Jika image <strong><em>mysql/mysql-server</em></strong> tidak ada di repository local, maka dia akan download image dari registry.</p>

<pre> 
$ docker ps
atau 
$ docker container ls</pre>

### 14. Membuat Volume
<pre> 
$ docker volume create data1
$ docker volume create data2 </pre>

<p>Untuk melihat volume yang sudah dibuat pada docker, ketikkan perintah:</p>
<pre> $ docker volume ls </pre>
<p>Untuk membuat container dengan mencantumkan volume yang ada dapat menggunakan opsi <strong>-v</strong>.</p>

<pre> $ docker run -itd --name mysqlserver1 -v data1:/var/lib/mysql -p 1234:3306 mysql </pre>
<p>Perintah tersebut akan me-mount volume <strong>data1</strong> ke direktori <strong>/var/lib/mysql/</strong> pada container <strong>mysqlserver1</strong>.</p>

### 15. Melakukan Commit Container
<pre> $ docker commit container1 image1 </pre>

<p>Perintah tersebut akan membuat image dengan nama <strong>image1</strong> dari container yang sedang running yaitu <strong>container1</strong>. Jadi kondisi <strong>container1</strong> yang sekarang akan disimpan dalam <strong>image1</strong>.</p>

<p>Jika terjadi perubahan pada <strong>container1</strong>, maka ketika nanti membuat container baru dari <strong>image1</strong> maka perubahan tersebut akan tetap ada.</p>



## Setup Container Mongo

### 1. Download image untuk mongo.
<pre> $ docker pull mongo </pre>

### 2. Periksa apakah image sudah ter-download.</p>
<pre> $ docker images</pre>

### 3. Buat kontainer untuk mongo.
<pre> $ docker container create --name mongoserver1 -p 1000:27017 mongo </pre>

### 4. Periksa apakah kontainer sudah terbuat.
<pre> $ docker container ls -a </pre>

### 5. Jalankan kontainer mongo.
<pre> $ docker container start mongoserver1 </pre>

### 6. Periksa apakah kontainer mongo sudah jalan.
<pre> $ docker container ls </pre>

### 7. Untuk masuk ke kontainer mongo dapat menggunakan perintah:
<pre> $ docker exec -it mongoserver1 bash
$ mongo</code></pre>

### 8. Untuk mengakses mongo dari host:
<pre> $ mongo --port 2000</pre>


## Setup Container Mysql Server

### 1. Download image untuk mysql-server.
<pre> $ docker pull mysql/mysql-server</pre>

### 2. Periksa apakah image sudah ter-download.
<pre>$ docker images</pre>

### 3. Buat kontainer untuk mysql-server dan langsung jalankan
<pre> $ docker run -d --name mysqlserver1 -p 5000:3306 mysql/mysql-server </pre>

### 4. Periksa apakah kontainer sudah jalan.
<pre> $ docker container ls </pre>

### 5. Periksa log pada container mysql-server untuk melihat password yang di-generate.
<pre> $ docker logs mysqlserver1 | grep GENERATED</pre>

### 6. Untuk masuk ke kontainer mysql dapat menggunakan perintah:
<pre> $ docker exec -it mysqlserver1 bash </pre>

### 7. Masuk ke mysql.
<pre> $ mysql -u root -p (gunakan password yang di generate)</pre>

### 8. Ganti password mysql.
<pre> $ ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpass';</pre>

### 9. Buat user baru mysql.
<pre> $ CREATE USER 'newuser'@'%' IDENTIFIED BY 'newpass';</pre>

### 10. Berikan akses pada user agar dapat diakses dari luar atau host.
<pre> GRANT ALL PRIVILEGES ON *.* TO 'newuser'@'%' WITH GRANT OPTION;</pre>

<p>11. Untuk mengakses mysql-server dari host:</p>
<pre class="wp-block-code"><code class="">$ mysql -h localhost -P 1234 --protocol=tcp -u root -p</code></pre>
