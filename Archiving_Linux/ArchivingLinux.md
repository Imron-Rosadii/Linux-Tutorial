````md
# 🧑‍💻 Archiving & Backup: Cron Job untuk Backup /etc

Pada tutorial ini, kita akan membuat **cron job** untuk user `root` yang akan melakukan backup folder `/etc` setiap hari ke direktori `/backup`, dan memastikan bahwa file backup yang dihasilkan berupa file `tar` dengan timestamp.

---

## 1. Buat Direktori `/backup`

**Task:** Pastikan direktori `/backup` sudah ada untuk tempat penyimpanan hasil backup.

```bash
# Membuat direktori /backup jika belum ada
sudo mkdir -p /backup
```
````

📌 **Penjelasan:**

- `mkdir -p /backup` → membuat direktori `/backup` jika belum ada.

---

## 2. Menulis Cron Job untuk Backup

**Task:** Buat cron job untuk user `root` yang akan menjalankan backup setiap hari dan membuat file `tar` dengan timestamp.

```bash
# Edit crontab untuk user root
sudo crontab -e
```

📌 **Penjelasan:**

- `sudo crontab -e` → membuka file crontab untuk user `root` untuk mengedit cron job.

---

## 3. Menambahkan Cron Job untuk Backup

Tambahkan baris berikut ke dalam file crontab untuk menjalankan backup setiap hari pada pukul 2 pagi:

```bash
0 2 * * * tar -czf /backup/etc_backup_$(date +\%F).tar.gz /etc
```

📌 **Penjelasan:**

- `0 2 * * *` → Menjadwalkan cron job untuk berjalan setiap hari pada pukul 02:00 (2 pagi).
- `tar -czf /backup/etc_backup_$(date +\%F).tar.gz /etc` → perintah untuk membuat file backup dengan format `.tar.gz`:

  - `-c` → membuat arsip baru.
  - `-z` → mengompres arsip menggunakan gzip.
  - `-f` → menentukan nama file arsip.
  - `$(date +\%F)` → menambahkan timestamp ke dalam nama file backup (misalnya `etc_backup_2025-09-10.tar.gz`).
  - `/etc` → direktori yang akan di-backup.

---

## 4. Verifikasi Cron Job

**Task:** Setelah menyimpan perubahan, pastikan cron job sudah ditambahkan dengan benar.

```bash
# Cek daftar cron job untuk root
sudo crontab -l
```

📌 **Penjelasan:**

- `sudo crontab -l` → menampilkan daftar cron job yang telah diatur untuk user `root`. Anda harus melihat job yang baru ditambahkan di sini.

---

## 5. Verifikasi Backup

**Task:** Setelah cron job berjalan (misalnya pada pukul 2 pagi), periksa hasil backup di `/backup`.

```bash
# Cek hasil backup
ls /backup
```

📌 **Penjelasan:**

- Perintah `ls /backup` akan menampilkan file backup yang dihasilkan dengan timestamp pada nama file, seperti `etc_backup_2025-09-10.tar.gz`.

---

## 📌 Kesimpulan

1. Membuat direktori `/backup` untuk menyimpan file hasil backup.
2. Menambahkan cron job untuk user `root` yang akan melakukan backup folder `/etc` setiap hari pada pukul 2 pagi.
3. Menggunakan perintah `tar` untuk membuat file backup dengan format `.tar.gz` dan menambahkan timestamp pada nama file.
4. Memverifikasi apakah cron job sudah berjalan dengan benar dan memastikan hasil backup tersimpan di `/backup`.

```

Anda bisa langsung menyalin isi file ini dan mengunggahnya ke Git dalam format `.md` untuk dokumentasi **Archiving & Backup** menggunakan cron job.
```
