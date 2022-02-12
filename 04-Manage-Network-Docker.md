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
