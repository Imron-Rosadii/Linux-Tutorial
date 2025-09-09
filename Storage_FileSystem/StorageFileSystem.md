# 📌 Storage & Filesystem (RHCSA)

## 1. Membuat Partisi Baru dengan `fdisk` atau `parted`

Untuk membuat partisi baru (misalnya `/dev/sdb1`) menggunakan `fdisk`:

1. **Jalankan perintah `fdisk` untuk memilih disk** yang akan dipartisi:

   ```bash
   sudo fdisk /dev/sdb
   ```

2. **Buat partisi baru** dengan mengikuti langkah-langkah di `fdisk`:

   - Tekan `n` untuk membuat partisi baru.
   - Pilih `p` untuk partisi primer.
   - Pilih nomor partisi (misalnya, 1).
   - Tentukan ukuran partisi (misalnya, pilih ukuran default atau tentukan ukuran manual).
   - Tekan `w` untuk menulis perubahan dan keluar dari `fdisk`.

   Setelah itu, partisi baru `/dev/sdb1` akan tersedia.

---

## 2. Format dengan `ext4` dan Mount ke `/mnt/data`

Untuk memformat partisi `/dev/sdb1` dengan filesystem `ext4` dan mount ke direktori `/mnt/data`:

1. **Format partisi dengan `ext4`**:

   ```bash
   sudo mkfs.ext4 /dev/sdb1
   ```

2. **Buat direktori mount point** (jika belum ada):

   ```bash
   sudo mkdir -p /mnt/data
   ```

3. **Mount partisi ke `/mnt/data`**:

   ```bash
   sudo mount /dev/sdb1 /mnt/data
   ```

4. **Verifikasi apakah partisi sudah ter-mount**:

   ```bash
   df -h
   ```

---

## 3. Menambahkan ke `/etc/fstab` Agar Otomatis Mount Saat Boot

Untuk memastikan partisi `/dev/sdb1` otomatis ter-mount saat boot, tambahkan entri ke file `/etc/fstab`.

1. **Edit file `/etc/fstab`**:

   ```bash
   sudo nano /etc/fstab
   ```

2. **Tambahkan baris berikut di akhir file**:

   ```ini
   /dev/sdb1  /mnt/data  ext4  defaults  0  2
   ```

   **Penjelasan:**

   - `/dev/sdb1`: Partisi yang akan di-mount.
   - `/mnt/data`: Lokasi mount point.
   - `ext4`: Tipe filesystem.
   - `defaults`: Opsi mount default.
   - `0 2`: Nilai untuk opsi `dump` dan `fsck` (untuk pemeliharaan filesystem).

3. **Simpan dan keluar** dari editor.

4. **Verifikasi entri dengan menjalankan**:

   ```bash
   sudo mount -a
   ```

   Pastikan tidak ada error, dan partisi sudah ter-mount secara otomatis.

---

## 4. Membuat Volume Group `vgdata` dengan LVM

Untuk membuat Volume Group (VG) dengan nama `vgdata` menggunakan LVM:

1. **Persiapkan partisi untuk LVM**:

   Sebelumnya, pastikan partisi `/dev/sdb1` digunakan untuk LVM. Jika belum, gunakan perintah berikut untuk menyiapkannya:

   ```bash
   sudo pvcreate /dev/sdb1
   ```

2. **Buat Volume Group `vgdata`**:

   ```bash
   sudo vgcreate vgdata /dev/sdb1
   ```

3. **Verifikasi Volume Group**:

   ```bash
   sudo vgs
   ```

---

## 5. Membuat Logical Volume `lvdata` Ukuran 1GB di `vgdata`

Untuk membuat Logical Volume (LV) `lvdata` dengan ukuran 1GB di dalam Volume Group `vgdata`:

1. **Buat Logical Volume `lvdata`**:

   ```bash
   sudo lvcreate -L 1G -n lvdata vgdata
   ```

2. **Verifikasi Logical Volume**:

   ```bash
   sudo lvs
   ```

---

## 6. Format `lvdata` dengan `xfs` dan Mount ke `/data`

Untuk memformat Logical Volume `lvdata` dengan filesystem `xfs` dan mount ke direktori `/data`:

1. **Format Logical Volume `lvdata` dengan filesystem `xfs`**:

   ```bash
   sudo mkfs.xfs /dev/vgdata/lvdata
   ```

2. **Buat direktori mount point** (jika belum ada):

   ```bash
   sudo mkdir -p /data
   ```

3. **Mount Logical Volume `lvdata` ke `/data`**:

   ```bash
   sudo mount /dev/vgdata/lvdata /data
   ```

4. **Verifikasi apakah Logical Volume sudah ter-mount**:

   ```bash
   df -h
   ```

---

## Kesimpulan

Langkah-langkah di atas mencakup:

- Membuat partisi baru dengan `fdisk` atau `parted`.
- Memformat partisi dengan `ext4` dan mount ke `/mnt/data`.
- Menambahkan entri di `/etc/fstab` agar partisi otomatis mount saat boot.
- Membuat Volume Group `vgdata` dengan LVM.
- Membuat Logical Volume `lvdata` ukuran 1GB di dalam `vgdata`.
- Memformat Logical Volume dengan `xfs` dan mount ke `/data`.

Proses ini adalah bagian dari **Red Hat Certified System Administrator (RHCSA)** yang berfokus pada manajemen storage dan filesystem menggunakan LVM.
