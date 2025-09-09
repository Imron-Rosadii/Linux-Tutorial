# 📌 Software & Package Management (RHCSA) - Menggunakan DNF

## 1. Menambahkan Repository Lokal ke `/etc/yum.repos.d/local.repo`

Untuk menambahkan repository lokal, lakukan langkah-langkah berikut:

1. **Buat file repository baru** di dalam direktori `/etc/yum.repos.d/` dengan nama `local.repo`:

   ```bash
   sudo mkdir -p /etc/yum.repos.d/
   ```

   ```bash
   sudo nano /etc/yum.repos.d/local.repo
   ```

2. **Isi file tersebut dengan informasi repository** Anda. Misalnya:

   ```ini
   [local-repo]
   name=Local Repository
   baseurl=file:///path/to/your/repo/directory
   enabled=1
   gpgcheck=0
   ```

   **Penjelasan:**

   - `[local-repo]`: Nama repository.
   - `name`: Deskripsi dari repo tersebut.
   - `baseurl`: Lokasi repo, gunakan `file:///` untuk repositori lokal.
   - `enabled=1`: Menandakan repository ini aktif.
   - `gpgcheck=0`: Menonaktifkan pemeriksaan GPG untuk paket.

   Jika repo berada di server lain, gunakan URL FTP atau HTTP sebagai `baseurl` seperti:

   ```ini
   baseurl=http://your-server-address/path/to/repo/
   ```

---

## 2. Instal Paket `httpd` dari Repository yang Ditambahkan

Setelah menambahkan repository lokal, instal paket `httpd` dengan perintah:

```bash
sudo dnf install httpd
```

**Penjelasan:**

- Perintah ini akan menginstal paket `httpd` (web server) dari repository lokal yang telah Anda tambahkan di file `local.repo`.

---

## 3. Menghapus Paket `httpd` dan Reinstall Lagi

### Menghapus Paket `httpd`:

```bash
sudo dnf remove httpd
```

**Penjelasan:**

- Perintah ini menghapus paket `httpd` beserta dependensinya.

### Menginstal Ulang Paket `httpd`:

```bash
sudo dnf install httpd
```

**Penjelasan:**

- Setelah menghapus paket, perintah ini akan menginstal kembali paket `httpd`.

---

## 4. Mencari Informasi tentang Paket `bash`

Untuk mencari informasi lebih lanjut mengenai paket `bash`, gunakan perintah:

```bash
dnf info bash
```

5. Cek Status dan Akses Apache

Setelah menginstal Apache, Anda bisa memastikan bahwa service httpd berjalan dengan baik:

Cek status Apache:

```bash
sudo systemctl status httpd
```

Pastikan statusnya menunjukkan active (running).

Cek Apache mendengarkan di port 80:

```bash
sudo ss -tuln | grep :80
```

Jika Apache mendengarkan pada port 80, Anda akan melihat output yang menunjukkan port tersebut terbuka.

Akses melalui browser: Cobalah mengakses http://localhost atau http://<IP_Server> di browser untuk memastikan bahwa Apache dapat diakses dengan benar.

**Penjelasan:**

- `dnf info bash` akan menampilkan informasi detail tentang paket `bash`, termasuk versi, deskripsi, repository tempat paket tersebut berasal, dan ukuran paket.

---

## Kesimpulan

Langkah-langkah ini mencakup:

- Menambahkan repository lokal.
- Menginstal dan menghapus paket menggunakan DNF.
- Mencari informasi tentang paket yang terpasang pada sistem.

Proses ini adalah bagian dari **Red Hat Certified System Administrator (RHCSA)** yang menguji kemampuan dasar dalam manajemen paket dan repositori pada sistem berbasis RHEL, CentOS 8, atau Fedora yang menggunakan DNF.
