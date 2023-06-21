# Managing the Life Cycle of Containers

## Managing Containers
Docker menyediakan perintah berikut untuk mengelola container :
- docker ps : Perintah ini bertanggung jawab untuk membuat daftar container yang sedang berjalan.
- Cointainer ID : Setiap container, saat dibuat mendapatkan ID container, yang berupa angka heksadesimal dan terlihat seperti ID gambar, tetapi sebenarnya tidak terkait.
- IMAGE : Image Container yang digunakan untuk memulai container.
- COMMAND : Perintah yang dijalankan saat container dimulai.
- CREATED : Tanggal dan waktu penampung dimulai.
- STATUS : Total waktu aktif penampung, jika masih berjalan, atau waktu sejak dihentikan.
- PORT : Port yang diekspos oleh container atau port forward, jika dikonfigurasi.
- NAMES : Nama Container

Container yang dihentikan tidak langsung dibuang. Sistem file lokal mereka dan status lainnya dipertahankan sehingga dapat diperiksa untuk analisis post-mortem. Opsi -a mencantumkan semua container, termasuk Container yang belum dibuang.

- docker inspect : Perintah ini bertanggung jawab untuk mencantumkan metadata tentang container yang berjalan atau berhenti. Perintah menghasilkan keluaran JSON.


