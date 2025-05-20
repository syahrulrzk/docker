# Docker Swarm
Docker Swarm adalah fitur clustering dan orchestration bawaan dari Docker yang memungkinkan pengelolaan dan pengaturan kontainer di beberapa host (server) sebagai satu kesatuan kluster. Dengan Docker Swarm, kamu bisa menjalankan aplikasi berbasis kontainer secara terdistribusi di banyak mesin, sambil tetap mengelolanya seperti sebuah sistem tunggal.

## 🔧 Komponen Utama Docker Swarm

### 1. Nodes (Node)

    - Manager Node : Bertugas mengelola kluster, menjadwalkan tugas, dan menyimpan status kluster.
    - Worker Node : Menjalankan layanan (services) atau kontainer sesuai instruksi dari manager node.

### 3. Services

    - Merupakan definisi tentang bagaimana kontainer harus dijalankan di dalam kluster.
    - Contoh: "Saya ingin 3 replika dari kontainer web saya selalu berjalan."

### 3. Tasks

    - Setiap unit kerja yang diberikan ke worker node untuk menjalankan kontainer sesuai spesifikasi service.

### 4. Stacks

    - Kumpulan layanan yang saling terkait dan didefinisikan dalam file `docker-compose.yml`.
    - Digunakan untuk mendeploy aplikasi lengkap dengan dependensinya.


## 🚀 Cara Kerja Docker Swarm

### 1. Inisialisasi kluster Swarm:
   
```shell
docker swarm init
```
Ini akan membuat satu manager node.

### 2. Menambahkan worker nodes:
```shell
docker swarm join --token <token> <manager-ip>:<port>
```

### 3. Membuat service:
```shell
docker service create --replicas 3 -p 80:80 nginx
```
Ini akan membuat 3 replika kontainer Nginx yang tersebar di node-node dalam kluster.

### 4. Mengelola service:
- Lihat daftar service :
```shell
docker service ls
```

- Update jumlah replika
```shell
docker service scale <service-name>=5
```


# Exampeles
 
 Run on Master/Leader
 ```shell
╭────[ reborn@linux ] [~] 
╰────[ ~ docker node ls
ID                            HOSTNAME   STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
34jf5sxl5wqcgd05vuh7vq1sj     DietPi     Ready     Active                          28.1.1
qn0o6dvohxppviod2do0ptnav     DietPi     Ready     Active                          28.1.1
rsuf6zkz0epz9lg0dk0x4wn6i *   ubuntu     Ready     Active         Leader           28.1.1
╭────[ reborn@linux ] [~] 
╰────[ ~ docker service create --name web --replicas 3 -p 80:80 nginx
5d1t6yp6y2y4zbmncw5hj8mnt
overall progress: 3 out of 3 tasks 
1/3: running   [==================================================>] 
2/3: running   [==================================================>] 
3/3: running   [==================================================>] 
verify: Service 5d1t6yp6y2y4zbmncw5hj8mnt converged 
╭────[ reborn@linux ] [~] 
╰────[ ~ docker service ls
ID             NAME      MODE         REPLICAS   IMAGE          PORTS
5d1t6yp6y2y4   web       replicated   3/3        nginx:latest   *:80->80/tcp
╭────[ reborn@linux ] [~] 
╰────[ ~ docker service ps web
ID             NAME      IMAGE          NODE      DESIRED STATE   CURRENT STATE           ERROR     PORTS
w40qt6743rrp   web.1     nginx:latest   ubuntu    Running         Running 6 minutes ago             
g8t5kfg87asz   web.2     nginx:latest   DietPi    Running         Running 5 minutes ago             
04a9kgel31t5   web.3     nginx:latest   DietPi    Running         Running 5 minutes ago             
╭────[ reborn@linux ] [~] 
╰────[ ~ 

```

