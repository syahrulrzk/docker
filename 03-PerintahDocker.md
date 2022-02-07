<p align="center"><img src="https://drive.google.com/uc?export=view&id=1B2skhoyxRxEG60l5DMdkfjHKOCBFRllZ"></p>

# Perintah Dasar dan Cara Pengunaan nya!
### 1. Melihat Images.
<pre>$ docker images</code></pre>

### 2. Download Images.
<pre>$ docker pull debian (latest)
$ docker pull debian:9.8 (certain version)</code></pre>

### 3. Melihat Docker Container yang sedang running.
<pre class="wp-block-code"><code class="">$ docker cotainer ls</code></pre>

### 4. Melihat semua list Docker Container.</p>
<pre> $ docker container ls -a</code></pre>

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

<p>Jadi ada langkah tertentu untuk menjalankan Image tertentu. Seperti <strong><em>mysql/mysql-server</em></strong>, anda bisa melihat dokumentasi resminya. Container mysql dapat di jalankan dengan perintah<code>:</code></p>

<pre class="wp-block-code"><code class="">$ docker run -itd --name mysqlserver1 -p 1234:3306 mysql/mysql-server</code></pre>
<p>Ketika dilihat pada running Container, maka Container tersebut langsung berjalan. </p>
<p>Jadi perintah tersebut akan membuat container otomatis dari image <strong><em>mysql/mysql-server</em></strong>. Jika image <strong><em>mysql/mysql-server</em></strong> tidak ada di repository local, maka dia akan download image dari registry.</p>
<pre class="wp-block-code"><code class="">$ docker ps

atau 

$ docker container ls</code></pre>

<p>14. Membuat Volume</p>
<pre class="wp-block-code"><code class="">$ docker volume create data1
$ docker volume create data2</code></pre>
<p>Untuk melihat volume yang sudah dibuat pada docker, ketikkan perintah:</p>
<pre class="wp-block-code"><code class="">$ docker volume ls</code></pre>
<p>Untuk membuat container dengan mencantumkan volume yang ada dapat menggunakan opsi <strong>-v</strong>.</p>
<pre class="wp-block-code"><code class="">$ docker run -itd --name mysqlserver1 -v data1:/var/lib/mysql -p 1234:3306 mysql</code></pre>
<p>Perintah tersebut akan me-mount volume <strong>data1</strong> ke direktori <strong>/var/lib/mysql/</strong> pada container <strong>mysqlserver1</strong>.</p>

<p>15. Melakukan Commit Container</p>
<pre class="wp-block-code"><code class="">$ docker commit container1 image1</code></pre>

<p>Perintah tersebut akan membuat image dengan nama <strong>image1</strong> dari container yang sedang running yaitu <strong>container1</strong>. Jadi kondisi <strong>container1</strong> yang sekarang akan disimpan dalam <strong>image1</strong>.</p>

<p>Jika terjadi perubahan pada <strong>container1</strong>, maka ketika nanti membuat container baru dari <strong>image1</strong> maka perubahan tersebut akan tetap ada.</p>



## Setup Container Mongo

<p>1. Download image untuk mongo.</p>
<pre class="wp-block-code"><code class="">$ docker pull mongo</code></pre>

<p>2. Periksa apakah image sudah ter-download.</p>
<pre class="wp-block-code"><code class="">$ docker images</code></pre>

<p>3. Buat kontainer untuk mongo.</p>
<pre class="wp-block-code"><code class="">$ docker container create --name mongoserver1 -p 1000:27017 mongo</code></pre>

<p>4. Periksa apakah kontainer sudah terbuat.</p>
<pre class="wp-block-code"><code class="">$ docker container ls -a</code></pre>

<p>5. Jalankan kontainer mongo.</p>
<pre class="wp-block-code"><code class="">$ docker container start mongoserver1</code></pre>

<p>6. Periksa apakah kontainer mongo sudah jalan.</p>
<pre class="wp-block-code"><code class="">$ docker container ls</code></pre>

<p>7. Untuk masuk ke kontainer mongo dapat menggunakan perintah:</p>
<pre class="wp-block-code"><code class="">$ docker exec -it mongoserver1 bash
$ mongo</code></pre>

<p>8. Untuk mengakses mongo dari host:</p>
<pre class="wp-block-code"><code class="">$ mongo --port 2000</code></pre>




## Setup Container Mysql Server

<p>1. Download image untuk mysql-server.</p>
<pre class="wp-block-code"><code class="">$ docker pull mysql/mysql-server</code></pre>

<p>2. Periksa apakah image sudah ter-download.</p>
<pre class="wp-block-code"><code class="">$ docker images</code></pre>

<p>3. Buat kontainer untuk mysql-server dan langsung jalankan.</p>
<pre class="wp-block-code"><code class="">$ docker run -d --name mysqlserver1 -p 5000:3306 mysql/mysql-server</code></pre>

<p>4. Periksa apakah kontainer sudah jalan.</p>
<pre class="wp-block-code"><code class="">$ docker container ls</code></pre>

<p>5. Periksa log pada container mysql-server untuk melihat password yang di-generate.</p>
<pre class="wp-block-code"><code class="">$ docker logs mysqlserver1 | grep GENERATED</code></pre>

<p>6. Untuk masuk ke kontainer mysql dapat menggunakan perintah:</p>
<pre class="wp-block-code"><code class="">$ docker exec -it mysqlserver1 bash</code></pre>

<p>7. Masuk ke mysql.</p>
<pre class="wp-block-code"><code class="">$ mysql -u root -p (gunakan password yang di generate)</code></pre>

<p>8. Ganti password mysql.</p>
<pre class="wp-block-code"><code class="">$ ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpass';</code></pre>

<p>9. Buat user baru mysql.</p>
<pre class="wp-block-code"><code class="">$ CREATE USER 'newuser'@'%' IDENTIFIED BY 'newpass';</code></pre>

<p>10. Berikan akses pada user agar dapat diakses dari luar atau host.</p>
<pre class="wp-block-code"><code class="">GRANT ALL PRIVILEGES ON *.* TO 'newuser'@'%' WITH GRANT OPTION;</code></pre>

<p>11. Untuk mengakses mysql-server dari host:</p>
<pre class="wp-block-code"><code class="">$ mysql -h localhost -P 1234 --protocol=tcp -u root -p</code></pre>
