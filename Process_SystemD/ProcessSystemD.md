# 📌 Process & Systemd (RHCSA)

## 1. Matikan Service `firewalld`

Untuk mematikan service `firewalld`, gunakan perintah berikut:

```bash
sudo systemctl stop firewalld
```

**Penjelasan:**

- `systemctl stop firewalld`: Mematikan service `firewalld` yang bertugas sebagai firewall di sistem.

Jika Anda juga ingin menonaktifkan service ini agar tidak berjalan saat boot, gunakan perintah:

```bash
sudo systemctl disable firewalld
```

---

## 2. Set Service `sshd` Agar Otomatis Jalan Saat Boot

Untuk memastikan bahwa service `sshd` (SSH Daemon) otomatis berjalan saat sistem boot, gunakan perintah:

```bash
sudo systemctl enable sshd
```

**Penjelasan:**

- `systemctl enable sshd`: Mengatur service `sshd` agar otomatis dijalankan saat boot.
- `sshd` adalah service yang digunakan untuk mengelola koneksi SSH ke sistem.

---

## 3. Cek Status Service `chronyd`

Untuk mengecek status service `chronyd` (service untuk sinkronisasi waktu), gunakan perintah:

```bash
sudo systemctl status chronyd
```

**Penjelasan:**

- `systemctl status chronyd`: Menampilkan status dari service `chronyd`, apakah sedang berjalan atau tidak.
- Service `chronyd` digunakan untuk menjaga sinkronisasi waktu sistem.

---

## 4. Buat Service Kustom Sederhana yang Menjalankan `ping 8.8.8.8`

Untuk membuat service kustom sederhana yang menjalankan perintah `ping 8.8.8.8`, lakukan langkah-langkah berikut:

1. **Buat file unit systemd** untuk service kustom. Misalnya, buat file dengan nama `ping8.service` di `/etc/systemd/system/`:

   ```bash
   sudo nano /etc/systemd/system/ping8.service
   ```

2. **Isi file unit dengan konfigurasi berikut**:

   ```ini
   [Unit]
   Description=Service to ping 8.8.8.8

   [Service]
   ExecStart=/bin/ping 8.8.8.8
   Restart=always

   [Install]
   WantedBy=multi-user.target
   ```

   **Penjelasan:**

   - `[Unit]`: Bagian ini berisi deskripsi tentang service.

     - `Description`: Menyediakan deskripsi singkat tentang apa yang dilakukan oleh service.

   - `[Service]`: Bagian ini mendefinisikan cara service dijalankan.

     - `ExecStart`: Perintah yang dijalankan ketika service dimulai. Di sini kita menggunakan perintah `/bin/ping 8.8.8.8`.
     - `Restart=always`: Service akan otomatis restart jika proses ping berhenti.

   - `[Install]`: Bagian ini mendefinisikan kapan service ini dijalankan.

     - `WantedBy=multi-user.target`: Menentukan bahwa service ini akan dijalankan pada saat sistem mencapai `multi-user.target` (target yang sesuai dengan keadaan normal sistem).

3. **Reload systemd untuk membaca file service baru**:

   ```bash
   sudo systemctl daemon-reload
   ```

4. **Aktifkan service agar dijalankan otomatis saat boot**:

   ```bash
   sudo systemctl enable ping8.service
   ```

5. **Mulai service**:

   ```bash
   sudo systemctl start ping8.service
   ```

6. **Cek status service kustom yang baru saja dibuat**:

   ```bash
   sudo systemctl status ping8.service
   ```

**Penjelasan:**

- Service kustom ini akan menjalankan perintah `ping 8.8.8.8` dan memastikan bahwa ping terus berjalan (karena `Restart=always`).
- `systemctl status ping8.service` akan menampilkan status service tersebut.

---

## Kesimpulan

Langkah-langkah di atas mencakup:

- Mematikan service `firewalld`.
- Mengatur agar service `sshd` otomatis berjalan saat boot.
- Mengecek status service `chronyd`.
- Membuat service kustom sederhana yang menjalankan `ping 8.8.8.8` secara terus-menerus.

Proses ini adalah bagian dari **Red Hat Certified System Administrator (RHCSA)** yang berfokus pada pengelolaan proses dan service menggunakan `systemd`.
