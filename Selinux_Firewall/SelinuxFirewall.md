# 📌 Security (SELinux & Firewall) (RHCSA)

## 1. Aktifkan `firewalld` dan Buka Port 80/TCP

Untuk mengaktifkan `firewalld` dan membuka port 80 (HTTP) agar bisa diakses, lakukan langkah-langkah berikut:

1. **Aktifkan `firewalld`**:

   ```bash
   sudo systemctl start firewalld
   ```

2. **Aktifkan `firewalld` agar berjalan otomatis saat boot**:

   ```bash
   sudo systemctl enable firewalld
   ```

3. **Buka port 80/tcp untuk HTTP**:

   ```bash
   sudo firewall-cmd --permanent --add-port=80/tcp
   ```

4. **Reload `firewalld` untuk menerapkan perubahan**:

   ```bash
   sudo firewall-cmd --reload
   ```

5. **Verifikasi apakah port 80/tcp sudah terbuka**:

   ```bash
   sudo firewall-cmd --list-all
   ```

---

## 2. Cek dan Ubah SELinux Context untuk File `index.html` Agar Bisa Diakses via `httpd`

Untuk memastikan bahwa file `index.html` dapat diakses melalui HTTP, Anda perlu memastikan bahwa SELinux context untuk file tersebut sudah benar.

1. **Cek SELinux context untuk file `index.html`**:

   ```bash
   ls -Z /var/www/html/index.html
   ```

   Jika SELinux context belum sesuai untuk diakses oleh `httpd`, maka Anda perlu mengubahnya.

2. **Ubah SELinux context file `index.html` agar sesuai untuk diakses oleh `httpd`**:

   ```bash
   sudo chcon -t httpd_sys_content_t /var/www/html/index.html
   ```

   **Penjelasan:**

   - `chcon`: Perintah untuk mengubah konteks SELinux file.
   - `-t httpd_sys_content_t`: Menetapkan konteks tipe konten HTTP agar file dapat diakses oleh server web.

3. **Verifikasi perubahan SELinux context**:

   ```bash
   ls -Z /var/www/html/index.html
   ```

   Pastikan konteks SELinux yang baru telah diterapkan.

---

## 3. Jalankan `getenforce` untuk Cek Mode SELinux, Lalu Set ke `Permissive`

Untuk memeriksa status mode SELinux dan mengubahnya ke mode `permissive`:

1. **Cek mode SELinux saat ini** dengan perintah:

   ```bash
   getenforce
   ```

   - Jika outputnya adalah `Enforcing`, berarti SELinux sedang mengaktifkan kebijakan akses yang ketat.
   - Jika outputnya adalah `Permissive`, berarti SELinux tidak memblokir tindakan, tetapi hanya mencatat pelanggaran.

2. **Set mode SELinux ke `Permissive`**:

   ```bash
   sudo setenforce 0
   ```

   **Penjelasan:**

   - `setenforce 0`: Mengubah mode SELinux menjadi `Permissive`, yang memungkinkan semua tindakan tetapi tetap mencatat pelanggaran.

3. **Verifikasi mode SELinux setelah perubahan**:

   ```bash
   getenforce
   ```

   Pastikan outputnya adalah `Permissive`.

---

## Kesimpulan

Langkah-langkah di atas mencakup:

- Mengaktifkan `firewalld` dan membuka port 80/tcp untuk HTTP.
- Memastikan file `index.html` dapat diakses oleh `httpd` dengan mengubah SELinux context.
- Memeriksa dan mengubah mode SELinux menjadi `Permissive`.

Proses ini adalah bagian dari **Red Hat Certified System Administrator (RHCSA)** yang berfokus pada konfigurasi keamanan melalui SELinux dan `firewalld`.
