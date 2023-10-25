# Data Persistent pada Docker Container
Seperti yang kita ketahui bahwa docker container bersifat sementara. Jadi ketika container dihapus, maka semua data atau perubahan yang telah terjadi akan ikut terhapus. Misalkan kita menjalankan container mysql dan kita memasukkan banyak data di dalamnya. Maka ketika container tersebut dihapus, maka data-data tersebut akan ikut hilang kecuali kita melakukan konfigurasi volume pada container tersebut.

Jika kita sudah melakukan konfigurasi volume pada docker, maka ketika kita membuat container dan kita ingin membawa perubahan ke dalam container yang lain atau kita nantinya akan membuat container baru, maka kita masih dapat membawa data-data dan perubahan lama. Mungkin kita juga mengenal docker commit, dimana perubahan konfigurasi pada container akan tetap disimpan dalam image baru. Tetapi untuk data-data pada path tertentu atau data pokok misalkan pada container mysql tidak akan tersimpan. Database pada mysql tidak akan tersimpan. Database mysql tersimpan pada /var/lib/mysql. Dan path tersebut akan selalu diperbarui ketika kita membuat container baru dari image yang baru ataupun image hasil commit.

Beda cerita jika kita melakukan perubahan pada sistem linux di dalam container. Misalkan pada container mysql, kita menambahkan user pada sistem linux nya (<b>$ adduser userbaru</b>) maka user tersebut akan tetap ada ketika kita melakukan commit pada container tersebut.

Saya akan memberikan sedikit gambaran bagaimana data dapat tersimpan di dalam container.
