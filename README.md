# 📌 Daftar Task Latihan RHCSA (Lengkap)

## 1. **Essential Tools & File Management**

- [ ] Buat direktori `/lab/files` dan masuk ke dalamnya.
- [ ] Buat file `notes.txt`, isi dengan teks bebas.
- [ ] Redirect output `ls -l /etc` ke file `list.txt`.
- [ ] Gunakan `grep` untuk mencari kata `root` di file `/etc/passwd`.
- [ ] Buat hardlink dan softlink dari `notes.txt`.
- [ ] Arsipkan `/etc/hosts` dan `/etc/passwd` ke `backup.tar`.
- [ ] Kompres `backup.tar` menjadi `backup.tar.gz`.

---

## 2. **User & Group Management**

- [ ] Buat user `student` dengan password `Redhat123`.
- [ ] Buat group `developers` lalu tambahkan user `student` ke dalamnya.
- [ ] Atur expiry date user `student` (misalnya +30 hari dari sekarang).
- [ ] Cek UID dan GID dari user `student`.

---

## 3. **File Permissions & ACL**

- [ ] Buat direktori `/project` dimiliki oleh user `student` dan group `developers`.
- [ ] Beri permission `770` ke direktori tersebut.
- [ ] Buat file `doc.txt` dalam `/project` dan berikan ACL agar user `student` punya `rw-`.
- [ ] Pastikan user lain tidak bisa mengakses file itu.

---

## 4. **Software & Package Management**

- [ ] Tambahkan repo lokal ke `/etc/yum.repos.d/local.repo`.
- [ ] Install paket `httpd` dari repo tersebut.
- [ ] Hapus paket `httpd` lalu reinstall lagi.
- [ ] Cari informasi tentang paket `bash`.

---

## 5. **Process & Systemd**

- [ ] Matikan service `firewalld`.
- [ ] Set service `sshd` agar otomatis jalan saat boot.
- [ ] Cek status service `chronyd`.
- [ ] Buat service kustom sederhana yang menjalankan `ping 8.8.8.8`.

---

## 6. **Shell Scripting**

- [ ] Buat script `/usr/local/bin/hello.sh` yang menampilkan `Hello RHCSA`.
- [ ] Buat script untuk cek apakah `/etc/passwd` ada, kalau ada tampilkan `OK`, kalau tidak tampilkan `Not Found`.
- [ ] Buat script looping untuk mencetak angka 1–10.
- [ ] Buat script menerima argumen (contoh: `$1`) dan menampilkan `Welcome $1`.

---

## 7. **Storage & Filesystem**

- [ ] Buat partisi baru (misalnya `/dev/sdb1`) dengan `fdisk` atau `parted`.
- [ ] Format dengan `ext4` dan mount ke `/mnt/data`.
- [ ] Tambahkan ke `/etc/fstab` agar otomatis mount saat boot.
- [ ] Buat volume group `vgdata` dengan LVM.
- [ ] Buat logical volume `lvdata` ukuran 1GB di `vgdata`.
- [ ] Format `lvdata` dengan `xfs` dan mount ke `/data`.

---

## 8. **Security (SELinux & Firewall)**

- [ ] Aktifkan `firewalld` dan buka port 80/tcp.
- [ ] Cek dan ubah SELinux context untuk file `index.html` agar bisa diakses via httpd.
- [ ] Jalankan `getenforce` untuk cek mode SELinux, lalu set ke `permissive`.

---

## 9. **Networking**

- [ ] Set IP address statis di `ens33`: `192.168.100.10/24` dengan gateway `192.168.100.1`.
- [ ] Tambahkan DNS `8.8.8.8`.
- [ ] Pastikan bisa `ping` ke `google.com`.
- [ ] Buat hostname menjadi `server1.example.com`.

---

## 10. **Archiving & Backup**

- [ ] Buat cron job user `root` untuk backup `/etc` setiap hari ke `/backup`.
- [ ] Pastikan hasil backup berupa file tar dengan timestamp.

---

## 11. **Containers (Podman/Buildah)**

- [ ] Pull image `registry.access.redhat.com/ubi8/ubi`.
- [ ] Jalankan container dari image tersebut.
- [ ] Jalankan container httpd di port 8080.
- [ ] Buat container agar otomatis start saat boot.

---

## 12. **Exam Simulation (Full Practice)**

- [ ] Buat user & group sesuai instruksi.
- [ ] Set storage dengan LVM dan mount ke lokasi tertentu.
- [ ] Install service `httpd`, buat halaman index custom, dan pastikan bisa diakses.
- [ ] Buat script sederhana sesuai requirement.
- [ ] Konfigurasi firewall dan SELinux agar service berjalan.
- [ ] Buat backup otomatis dengan cron.

---

⚡ Semua task di atas meniru **kompetensi resmi RHCSA**. Kalau kamu bisa selesaikan ini semua tanpa melihat catatan, berarti sudah siap ujian 💯.

Mau saya bikinkan juga **jawaban (step-by-step command)** untuk tiap task ini, biar kamu bisa langsung praktek dan cek hasilnya?
