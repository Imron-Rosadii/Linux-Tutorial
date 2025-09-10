Berikut adalah file **Markdown** yang siap untuk Anda push ke Git:

````md
# 🧑‍💻 Exam Simulation (Full Practice)

Dalam ujian simulasi ini, Anda akan melakukan serangkaian tugas administratif di server Linux. Tugas-tugas yang akan dilakukan meliputi pembuatan **user & group**, pengaturan **LVM storage**, pemasangan **HTTP service** (`httpd`), pembuatan **script sederhana**, pengaturan **firewall & SELinux**, serta pembuatan **backup otomatis dengan cron**.

---

## 1. Membuat User dan Group

**Task:** Buat **user** dan **group** sesuai instruksi yang diberikan.

```bash
# Membuat group baru
sudo groupadd devgroup

# Membuat user baru dan menambahkan ke dalam group devgroup
sudo useradd -m -G devgroup user1

# Menetapkan password untuk user1
echo "password123" | sudo passwd --stdin user1
```
````

📌 **Penjelasan:**

- `groupadd devgroup` → membuat group `devgroup`.
- `useradd -m -G devgroup user1` → membuat user `user1` dan menambahkannya ke dalam group `devgroup`.
- `passwd --stdin user1` → menetapkan password untuk user `user1` secara otomatis.

---

## 2. Mengonfigurasi LVM dan Mount Storage ke Lokasi Tertentu

**Task:** Set up **LVM** untuk storage dan mount ke lokasi tertentu.

### 2.1. Membuat Partisi LVM

```bash
# Membuat physical volume (PV) di /dev/sdb
sudo pvcreate /dev/sdb

# Membuat volume group (VG) dengan nama vg_data
sudo vgcreate vg_data /dev/sdb

# Membuat logical volume (LV) dengan nama lv_data dan ukuran 10GB
sudo lvcreate -L 10G -n lv_data vg_data
```

### 2.2. Membuat Sistem Berkas dan Mount

```bash
# Membuat sistem berkas ext4 pada logical volume
sudo mkfs.ext4 /dev/vg_data/lv_data

# Membuat direktori mount point
sudo mkdir /mnt/data

# Mount logical volume ke direktori /mnt/data
sudo mount /dev/vg_data/lv_data /mnt/data
```

### 2.3. Membuat Mount Otomatis saat Boot

```bash
# Menambahkan entri di /etc/fstab agar mount otomatis saat boot
echo "/dev/vg_data/lv_data /mnt/data ext4 defaults 0 0" | sudo tee -a /etc/fstab
```

📌 **Penjelasan:**

- `pvcreate` → membuat physical volume di `/dev/sdb`.
- `vgcreate` → membuat volume group `vg_data` menggunakan `/dev/sdb`.
- `lvcreate` → membuat logical volume `lv_data` dengan ukuran 10GB.
- `mkfs.ext4` → membuat filesystem ext4 pada LV.
- `mount` → memasang logical volume pada direktori `/mnt/data`.

---

## 3. Menginstal HTTP Service dan Membuat Halaman Index Kustom

**Task:** Install **httpd** dan buat halaman index custom yang dapat diakses.

### 3.1. Menginstal HTTP Service

```bash
# Menginstal paket httpd
sudo yum install -y httpd
```

### 3.2. Membuat Halaman Index Kustom

```bash
# Membuat halaman index.html kustom
echo "<html><body><h1>Selamat datang di halaman index kustom!</h1></body></html>" | sudo tee /var/www/html/index.html
```

### 3.3. Menjalankan dan Mengaktifkan Layanan HTTPD

```bash
# Menjalankan layanan httpd
sudo systemctl start httpd

# Mengaktifkan agar httpd berjalan otomatis saat boot
sudo systemctl enable httpd
```

### 3.4. Verifikasi Akses HTTP

- Akses halaman index kustom melalui browser dengan menuju `http://<ip-server-anda>/`.

📌 **Penjelasan:**

- `yum install -y httpd` → menginstal paket `httpd` (Apache HTTP Server).
- `systemctl start httpd` → menjalankan layanan HTTPD.
- `systemctl enable httpd` → mengonfigurasi agar HTTPD otomatis berjalan saat boot.
- `tee /var/www/html/index.html` → membuat halaman `index.html` dengan konten kustom.

---

## 4. Membuat Script Sederhana

**Task:** Buat **script sederhana** yang mencetak tanggal saat ini ke dalam file.

```bash
# Membuat script sederhana
echo -e "#!/bin/bash\n\ndate > /tmp/current_date.txt" | sudo tee /usr/local/bin/print_date.sh

# Memberikan izin eksekusi pada script
sudo chmod +x /usr/local/bin/print_date.sh
```

📌 **Penjelasan:**

- `echo -e` → membuat script `print_date.sh` yang mencetak tanggal saat ini ke dalam file `/tmp/current_date.txt`.
- `chmod +x` → memberikan izin eksekusi pada file script.

---

## 5. Konfigurasi Firewall dan SELinux

**Task:** Konfigurasi **firewall** dan **SELinux** agar layanan HTTPD dapat berjalan.

### 5.1. Mengonfigurasi Firewall untuk HTTPD

```bash
# Menambahkan aturan firewall untuk HTTP
sudo firewall-cmd --permanent --add-service=http

# Memuat ulang konfigurasi firewall
sudo firewall-cmd --reload
```

### 5.2. Mengonfigurasi SELinux untuk HTTPD

```bash
# Memeriksa status SELinux
sestatus

# Jika SELinux aktif, jalankan perintah berikut untuk mengizinkan HTTPD
sudo setsebool -P httpd_can_network_connect on
```

📌 **Penjelasan:**

- `firewall-cmd --add-service=http` → menambahkan aturan untuk membuka port HTTP di firewall.
- `setsebool -P httpd_can_network_connect on` → mengizinkan HTTPD untuk mengakses jaringan dalam konfigurasi SELinux.

---

## 6. Membuat Backup Otomatis dengan Cron

**Task:** Buat **cron job** untuk melakukan backup otomatis setiap hari pada folder `/etc` ke folder `/backup`.

### 6.1. Membuat Direktori Backup

```bash
# Membuat direktori untuk backup
sudo mkdir -p /backup
```

### 6.2. Membuat Cron Job untuk Backup

```bash
# Edit crontab untuk user root
sudo crontab -e

# Menambahkan baris berikut ke crontab
0 2 * * * tar -czf /backup/etc_backup_$(date +\%F).tar.gz /etc
```

📌 **Penjelasan:**

- `tar -czf /backup/etc_backup_$(date +\%F).tar.gz /etc` → membuat file backup dari folder `/etc` setiap hari pada pukul 2 pagi dengan format nama file yang berisi tanggal.
- `cron` menjalankan perintah ini setiap hari pada pukul 2 pagi secara otomatis.

---

## 📌 Kesimpulan

1. **User & Group:** Membuat user `user1` dan group `devgroup`, serta menambahkan user ke dalam group.
2. **LVM Storage:** Mengonfigurasi LVM dengan membuat PV, VG, dan LV, serta melakukan mount ke `/mnt/data`.
3. **HTTPD Service:** Menginstal dan menjalankan HTTPD, serta membuat halaman index kustom.
4. **Script Sederhana:** Membuat script yang mencetak tanggal saat ini ke file.
5. **Firewall & SELinux:** Mengonfigurasi firewall untuk HTTPD dan mengubah pengaturan SELinux agar HTTPD dapat berfungsi.
6. **Backup Otomatis:** Membuat cron job untuk backup folder `/etc` setiap hari ke folder `/backup`.

Dengan menyelesaikan langkah-langkah ini, Anda telah menyelesaikan ujian simulasi yang mencakup tugas-tugas dasar dalam administrasi server Linux.

````

### Cara Mengunggah ke Git:
1. **Buat file `exam_simulation.md`** dengan menyalin konten di atas.
2. **Push ke Git**:
   - Pastikan Anda sudah menginisialisasi repository Git dan menambahkan file tersebut.
   - Gunakan perintah berikut untuk mengupload:
     ```bash
     git add exam_simulation.md
     git commit -m "Add exam simulation practice"
     git push origin main
     ```

Dokumentasi ini akan membantu Anda menyelesaikan ujian praktikum **RHCSA** atau tugas administratif serupa di server Linux.
````
