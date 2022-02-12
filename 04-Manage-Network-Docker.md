# Cara Menage Network Di Docker
Secara default container menggunakan network driver tipe bridge dengan nama bridge. Network driver lain yang tersedia yaitu host, overlay, dan macvlan.

## Network Driver
<ul>
  <li>bridge: menghubungkan container yang memakai nama bridge yang sama</li>
  <li>host: menghapus network isolation antara container dan Docker host, secara langsung menggunakan network milik host</li>
  <li>overlay: menghubungkan beberapa Docker daemon bersama-sama dan memungkinkan swarm service berkomunikasi satu sama lain</li>
  <li>macvlan: memungkinkan menetapkan MAC address ke container, membuatnya muncul sebagai perangkat fisik di network</li>
  <li>none: menonaktifkan semua network. Biasanya digunakan bersama dengan custom network driver</li>
  <li>Network plugins: menginstall dan menggunakan third-party network plugin yang tersedia di Docker Hub atau dari third-party vendor</li>
</ul>

## Bridge Network

Menampilkan network yang tersedia di Docker.
<pre>
 docker network ls    
</pre>

Contoh hasil perintah di atas, menampilkan network default, belum ada network yang ditambahkan sendiri.

<pre>
NETWORK ID     NAME      DRIVER    SCOPE
1652fc7934a6   bridge    bridge    local
547776771fe2   host      host      local
a4d149a845ae   none      null      local
</pre>

## Default Brigde Network

Membuat dua container dengan nama container node1 dan node2, image nginx:stable-alpine, dan tanpa mendefinisikan opsi network.
<pre> 
docker run -d --name node1 nginx:stable-alpine    
docker run -d --name node2 nginx:stable-alpine    
</pre>
