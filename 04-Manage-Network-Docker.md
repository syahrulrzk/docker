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

Menampilkan informasi detail container.
<pre>docker inspect node1    </pre>

Informasi network dari container terdapat pada bagian Networks. Container menggunakan network driver bridge. 12 karakter pertama (1652fc7934a6) NetworkID sama dengan NETWORK ID yang ditampilkan sebelumnya pada hasil perintah docker network ls dengan NAME dan DRIVER bridge.

<pre>
...
"Networks": {
    "bridge": {
        "IPAMConfig": null,
        "Links": null,
        "Aliases": null,
        "NetworkID": "1652fc7934a653e3852e24f289219ea1255292133d625563bf5905947a313d98",
        "EndpointID": "ce80598649bf6500e4fb6799f76801908bc9e69a7535fb8241a64a6cb7418b04",
        "Gateway": "172.17.0.1",
        "IPAddress": "172.17.0.2",
...
</pre>

IP address 172.17.0.2 dan Gateway 172.17.0.1. Gateway menggunakan network interface dan IP dari Docker0 di host.

<pre>
ifconfig docker0

docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:b0ff:fe4b:4ff9  prefixlen 64  scopeid 0x20<link>
        ether 02:42:b0:4b:4f:f9  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 5  bytes 526 (526.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
</pre>

Menampilkan informasi network dengan nama bridge.

<pre>
docker network inspect bridge    
</pre>

<pre>
...
"Containers": {
    "aba5c5373c2dc5cf0c416d4c9a64334f060d05a84695dbcfbb3866bb7722d036": {
        "Name": "node1",
        "EndpointID": "ce80598649bf6500e4fb6799f76801908bc9e69a7535fb8241a64a6cb7418b04",
        "MacAddress": "02:42:ac:11:00:02",
        "IPv4Address": "172.17.0.2/16",
        "IPv6Address": ""
    },
    "f0667f59710ee4a62299f6943a38f0b40bbe09ee950b6e62d8b35fc6bdb71b2f": {
        "Name": "node2",
        "EndpointID": "d272a549bdb743c4206eb4ef17fc10981c9cbb3a51c38e2fad22afd55175f374",
        "MacAddress": "02:42:ac:11:00:03",
        "IPv4Address": "172.17.0.3/16",
        "IPv6Address": ""
    }
},
...   
</pre>

Container yang menggunakan bridge network dapat dilihat informasinya pada bagian Containers. Terdapat dua container yaitu node1 dengan IP address 172.17.0.2 dan node2 dengan IP address 172.17.0.3.

Uji ping dari container node1 ke node2.

<pre>docker exec node1 ping 172.17.0.3</pre>

Hasil perintah di atas.

<pre>
PING 172.17.0.3 (172.17.0.3): 56 data bytes
64 bytes from 172.17.0.3: seq=0 ttl=64 time=0.119 ms
64 bytes from 172.17.0.3: seq=1 ttl=64 time=0.134 ms
64 bytes from 172.17.0.3: seq=2 ttl=64 time=0.107 ms
</pre>

## Membuat Bridge Network

Container yang menggunakan default bridge network tidak dapat secara otomatis berkomunikasi menggunakan hostname dari container, hanya dapat menggunakan IP address. Misalnya tidak bisa ping node2 hanya bisa ping 172.17.0.3.

Untuk dapat berkomunikasi dengan menggunakan hostname, definisikan IP-host di file /etc/hosts container secara manual. Cara lainnya, container menggunakan bridge network yang dibuat sendiri (user-defined bridge).

Membuat bridge network dengan nama net-web.
<pre>docker network create net-web    </pre>

Menampilkan network.

<pre>
docker network ls

NETWORK ID     NAME      DRIVER    SCOPE
1652fc7934a6   bridge    bridge    local
547776771fe2   host      host      local
2aa8cf07ab2e   net-web   bridge    local
a4d149a845ae   none      null      local
</pre>

### Membuat Container Dengan Opsi Network

Pada saat membuat container dapat sekaligus menghubungkannya ke network.

Membuat container dan menghubungkannya ke network dengan nama net-web.

<pre>
docker run -d --name node1 --network net-web nginx:stable-alpine
docker run -d --name node2 --network net-web nginx:stable-alpine
</pre>

Uji ping dari container node1 ke node2.

<pre>
docker exec node1 ping node2

PING node2 (172.19.0.3): 56 data bytes
64 bytes from 172.19.0.3: seq=0 ttl=64 time=0.145 ms
64 bytes from 172.19.0.3: seq=1 ttl=64 time=0.100 ms
64 bytes from 172.19.0.3: seq=2 ttl=64 time=0.117 ms
</pre>

### Menghubungkan Container yang Sudah Ada

Container yang sudah ada sebelumnya dapat dihubungkan ke network.

Menghubungkan container node1 dan node2 ke network net-web.

<pre>
docker network connect net-web node1
docker network connect net-web node2    
</pre>

Melepaskan container node1 dari network net-web.

<pre>docker network disconnect net-web node1</pre>

## Perintah Docker Network

Menampilakn semua network <pre>docker network ls</pre>
Membuat Network <pre>docker network create nama-network</pre>
Menghubungakan Container Ke Network <pre>docker network connect nama-network nama-container</pre>
Melepaskan Container dari Network <pre>docker network disconnect nama-network nama-container</pre>
Menampilakan Informasi Detail Network <pre>docker network inspect nama-network</pre>
Menghapus Network<pre>docker network rm nama-network</pre>
Menghapus Semua Network Yang tidak Di Pakai<pre>docker network prune</pre>




























