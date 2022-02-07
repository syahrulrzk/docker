		
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
