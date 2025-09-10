Berikut adalah versi yang lebih lengkap dan jelas dari tutorial **Podman/Buildah** untuk menarik image, menjalankan container `httpd` di port 8080, serta mengonfigurasi agar container otomatis start saat boot.

# 🧑‍💻 Containers Management with Podman/Buildah

Tutorial ini menjelaskan cara untuk:

1. Menarik image `ubi8/ubi` dari registry Red Hat.
2. Menjalankan container dari image tersebut.
3. Menjalankan container `httpd` di port 8080.
4. Mengonfigurasi agar container otomatis dimulai saat boot.

## 1. Menarik Image `ubi8/ubi` dari Registry

**Task:** Menarik image `ubi8/ubi` dari registry Red Hat untuk digunakan dalam container.

```bash
podman pull registry.access.redhat.com/ubi8/ubi
```

📌 **Penjelasan:**

- `podman pull` → perintah untuk menarik (download) image dari registry.
- `registry.access.redhat.com/ubi8/ubi` → alamat image yang ingin Anda tarik (image `ubi8/ubi` dari Red Hat).

**Output yang diharapkan:**

Setelah perintah berhasil, Anda akan melihat hasilnya seperti ini:

```bash
Trying to pull registry.access.redhat.com/ubi8/ubi:latest...
Getting image source signatures
Copying blob sha256:abcdef...
Copying config sha256:123456...
Writing manifest...
...
```

---

## 2. Menjalankan Container dari Image `ubi8/ubi`

**Task:** Menjalankan container dari image `ubi8/ubi` yang telah ditarik sebelumnya.

```bash
podman run -it --name mycontainer registry.access.redhat.com/ubi8/ubi
```

📌 **Penjelasan:**

- `podman run` → perintah untuk menjalankan container.
- `-it` → menjalankan container secara interaktif dengan terminal (untuk memudahkan pengelolaan).
- `--name mycontainer` → memberi nama container `mycontainer` agar mudah dikenali.
- `registry.access.redhat.com/ubi8/ubi` → image yang digunakan untuk menjalankan container.

**Output yang diharapkan:**

Container akan dijalankan dengan prompt interaktif, sehingga Anda bisa bekerja di dalam container. Jika Anda melihat prompt seperti `#`, itu berarti container sedang berjalan.

---

## 3. Menjalankan Container `httpd` di Port 8080

**Task:** Menjalankan container `httpd` pada port 8080 di sistem host.

```bash
podman run -d --name httpd-container -p 8080:80 httpd
```

📌 **Penjelasan:**

- `podman run -d` → menjalankan container dalam mode detached (background).
- `--name httpd-container` → memberi nama container sebagai `httpd-container`.
- `-p 8080:80` → memetakan port 8080 di host ke port 80 di container (akses HTTP akan tersedia di port 8080).
- `httpd` → image yang digunakan untuk menjalankan container web server Apache HTTP.

**Output yang diharapkan:**

Container akan berjalan di background dan Anda dapat mengecek statusnya menggunakan perintah berikut.

```bash
podman ps
```

Perintah ini akan menampilkan semua container yang sedang berjalan, dan Anda akan melihat container `httpd-container` terdaftar di sana.

---

## 4. Mengonfigurasi Container Agar Otomatis Start Saat Boot

**Task:** Mengonfigurasi container `httpd-container` agar otomatis mulai saat sistem boot.

```bash
podman run -d --name httpd-container -p 8080:80 --restart=always httpd
```

📌 **Penjelasan:**

- `--restart=always` → memastikan container akan otomatis dimulai kembali jika container dihentikan atau saat sistem reboot.
- Parameter lainnya tetap sama seperti yang digunakan sebelumnya untuk menjalankan container `httpd` pada port 8080.

**Output yang diharapkan:**

Setelah menjalankan perintah ini, container `httpd-container` akan otomatis dimulai setiap kali sistem di-boot ulang.

---

## 5. Verifikasi

**Task:** Verifikasi bahwa container berjalan dengan benar dan dapat diakses di port 8080.

### 5.1. Verifikasi Status Container

Periksa apakah container sedang berjalan:

```bash
podman ps
```

📌 **Penjelasan:**

- `podman ps` → perintah ini menampilkan semua container yang sedang berjalan. Pastikan `httpd-container` terdaftar.

### 5.2. Verifikasi Akses HTTP

Untuk memastikan bahwa container web server dapat diakses melalui port 8080, gunakan `curl` atau akses dari browser.

```bash
curl http://localhost:8080
```

📌 **Penjelasan:**

- `curl http://localhost:8080` → perintah ini akan mengirimkan permintaan HTTP ke port 8080 di host. Anda harus melihat halaman default Apache HTTP server jika semuanya berjalan dengan baik.

---

## 6. Menonaktifkan dan Menghapus Container (Opsional)

Jika Anda ingin menghentikan dan menghapus container yang telah dibuat, Anda dapat menjalankan perintah berikut:

### 6.1. Menonaktifkan Container

```bash
podman stop httpd-container
```

### 6.2. Menghapus Container

```bash
podman rm httpd-container
```

📌 **Penjelasan:**

- `podman stop` → menghentikan container yang sedang berjalan.
- `podman rm` → menghapus container dari sistem.

---

## 📌 Kesimpulan

1. **Menarik Image:** Menarik image `ubi8/ubi` dari registry Red Hat menggunakan `podman pull`.
2. **Menjalankan Container:** Menjalankan container dari image `ubi8/ubi` dengan menggunakan perintah `podman run`.
3. **Menjalankan HTTP Server:** Menjalankan container `httpd` pada port 8080 dengan perintah `podman run -p 8080:80`.
4. **Autostart pada Boot:** Mengonfigurasi container `httpd-container` untuk otomatis dimulai saat boot dengan opsi `--restart=always`.
5. **Verifikasi:** Memverifikasi status container dengan `podman ps` dan memastikan akses HTTP pada port 8080 menggunakan `curl`.
6. **Opsional:** Menonaktifkan dan menghapus container jika diperlukan.

Dengan mengikuti langkah-langkah di atas, Anda telah berhasil menarik image, menjalankan container HTTP, dan mengonfigurasi agar container tersebut dimulai otomatis saat booting menggunakan **Podman**. Anda juga telah memastikan container dapat diakses melalui port 8080.

```

### Penjelasan untuk Penggunaan:
- **Podman** adalah alat pengelolaan container yang digunakan untuk menjalankan dan mengelola container di Linux.
- Tutorial ini mencakup semua langkah dari menarik image hingga mengonfigurasi container agar start otomatis saat boot.
```
