		
<p>1. Melihat Images.</p>
<pre class="wp-block-code"><code class="">$ docker images</code></pre>

<p>2. Download Images.</p>
<pre class="wp-block-code"><code class="">$ docker pull debian (latest)
$ docker pull debian:9.8 (certain version)</code></pre>

<p>3. Melihat Docker Container yang sedang running.</p>
<pre class="wp-block-code"><code class="">$ docker cotainer ls</code></pre>

<p>4. Melihat semua list Docker Container.</p>
<pre class="wp-block-code"><code class="">$ docker container ls -a</code></pre>

<p>5. Membuat Docker Container.</p>
<pre class="wp-block-code"><code class="">$ docker container create --name mongodb1 mongo:4.0</code></pre>

<p>6. Start Container.</p>
<pre class="wp-block-code"><code class="">$ docker container start mongodb1</code></pre>

<p>7. Mencari Images.</p>
<pre class="wp-block-code"><code class="">$ docker search mysql</code></pre>

<p>8. Stop Container.</p>
<pre class="wp-block-code"><code class="">$ docker container stop mongodb1</code></pre>

<p>9. Menghapus Container.</p>
<pre class="wp-block-code"><code class="">$ docker container rm mongodb1</code></pre>

<p>10. Membuat Container yang dapat diakses dari host. Dengan kata lain, membuka port pada Container sehingga service yang dijalankan dapat diakses dari luar.</p>
<pre class="wp-block-code"><code class="">$ docker container create --name mongodb2 -p 1234:27017 mongo</code></pre>

<p>11. Menjalankan Images secara langsung. Sehingga, container akan otomatis terbentuk dari Image tersebut.</p>
<pre class="wp-block-code"><code class="">$ docker run -itd mongo</code></pre>

<p>12. Menjalankan Image secara langsung dan otomatis membuat container. Dan juga membuka port untuk container tersebut. Contohnya pada Image mysql/mysql-server.</p>
<pre class="wp-block-code"><code class="">$ docker run -d --name mysqlserver1 -p 1234:3306 mysql/mysql-server</code></pre>

<p>13. Masuk ke dalam Container.</p>
<pre class="wp-block-code"><code class="">$ docker exec -it mongodb2 bash</code></pre>

<p>Nanti mungkin anda akan menemui beberapa sedikit masalah, seperti Image yang tidak bisa di start dengan perintah<code>:</code></p>
