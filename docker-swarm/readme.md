# Docker Swarm
Docker Swarm adalah fitur clustering dan orchestration bawaan dari Docker yang memungkinkan pengelolaan dan pengaturan kontainer di beberapa host (server) sebagai satu kesatuan kluster. Dengan Docker Swarm, kamu bisa menjalankan aplikasi berbasis kontainer secara terdistribusi di banyak mesin, sambil tetap mengelolanya seperti sebuah sistem tunggal.

## 🔧 Komponen Utama Docker Swarm

1. Nodes (Node)
    - Manager Node : Bertugas mengelola kluster, menjadwalkan tugas, dan menyimpan status kluster.
    - Worker Node : Menjalankan layanan (services) atau kontainer sesuai instruksi dari manager node.

3. Services
    - Merupakan definisi tentang bagaimana kontainer harus dijalankan di dalam kluster.
    - Contoh: "Saya ingin 3 replika dari kontainer web saya selalu berjalan."

3. Tasks
    - Setiap unit kerja yang diberikan ke worker node untuk menjalankan kontainer sesuai spesifikasi service.

4. Stacks
    - Kumpulan layanan yang saling terkait dan didefinisikan dalam file `docker-compose.yml`.
    - Digunakan untuk mendeploy aplikasi lengkap dengan dependensinya.


## 🚀 Cara Kerja Docker Swarm

1. Inisialisasi kluster Swarm:
```shell
docker swarm init
```
Ini akan membuat satu manager node.

2. Menambahkan worker nodes:
```shell
docker swarm join --token <token> <manager-ip>:<port>
```

3. Membuat service:
```shell
docker service create --replicas 3 -p 80:80 nginx
```
Ini akan membuat 3 replika kontainer Nginx yang tersebar di node-node dalam kluster.

4. Mengelola service:
