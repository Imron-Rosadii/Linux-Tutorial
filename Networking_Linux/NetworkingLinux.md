Berikut adalah tutorial lengkap dengan langkah-langkah untuk mengonfigurasi IP statis di `ens33`, menambahkan DNS, memastikan koneksi ke google.com, dan mengganti hostname menjadi `server1.example.com`:

````md
# 🧑‍💻 Networking Configuration (Set IP, DNS, Hostname)

Dalam tutorial ini, kita akan mengonfigurasi IP statis di interface `ens33`, menambahkan DNS, memastikan koneksi internet dengan `ping` ke `google.com`, dan mengganti hostname menjadi `server1.example.com`.

---

## 1. Set IP Address Statis di Interface `ens33`

**Task:** Atur IP address statis di interface `ens33` dengan alamat `192.168.100.10/24` dan gateway `192.168.100.1`.

```bash
# Edit file konfigurasi jaringan untuk interface ens33
sudo nano /etc/sysconfig/network-scripts/ifcfg-ens33
```
````

📌 **Konfigurasi yang perlu ditambahkan**:

```bash
BOOTPROTO=static
ONBOOT=yes
IPADDR=192.168.100.10
NETMASK=255.255.255.0
GATEWAY=192.168.100.1
```

📌 **Penjelasan:**

- `BOOTPROTO=static` → mengatur IP statis.
- `IPADDR=192.168.100.10` → alamat IP yang akan digunakan.
- `NETMASK=255.255.255.0` → subnet mask.
- `GATEWAY=192.168.100.1` → alamat gateway.

Setelah selesai, simpan dan keluar dari editor (tekan `CTRL + X`, lalu `Y`, dan tekan `Enter`).

---

## 2. Tambahkan DNS Server

**Task:** Tambahkan DNS server `8.8.8.8`.

```bash
# Edit file resolv.conf untuk menambahkan DNS
sudo nano /etc/resolv.conf
```

📌 **Tambahkan baris berikut**:

```bash
nameserver 8.8.8.8
```

📌 **Penjelasan:**

- `nameserver 8.8.8.8` → menggunakan DNS Google (8.8.8.8).

Setelah selesai, simpan dan keluar dari editor.

---

## 3. Restart Jaringan

Untuk menerapkan konfigurasi IP dan DNS baru, restart jaringan:

```bash
# Restart jaringan untuk menerapkan perubahan
sudo systemctl restart network
```

---

## 4. Pastikan Koneksi Internet (Ping ke google.com)

**Task:** Verifikasi koneksi dengan melakukan `ping` ke `google.com`.

```bash
ping google.com
```

📌 **Penjelasan:**

- Jika ping berhasil, artinya koneksi internet berfungsi dengan baik.

---

## 5. Ganti Hostname Menjadi `server1.example.com`

**Task:** Ganti hostname mesin menjadi `server1.example.com`.

```bash
# Set hostname
sudo hostnamectl set-hostname server1.example.com
```

📌 **Penjelasan:**

- `hostnamectl set-hostname server1.example.com` → mengubah hostname mesin.

---

## 6. Verifikasi Hostname

**Task:** Verifikasi perubahan hostname.

```bash
hostname
```

📌 **Penjelasan:**

- Perintah ini akan menampilkan hostname mesin yang baru. Seharusnya keluar `server1.example.com`.

---

## 📌 Kesimpulan

1. Mengonfigurasi IP statis di interface `ens33` dengan alamat `192.168.100.10/24` dan gateway `192.168.100.1`.
2. Menambahkan DNS server `8.8.8.8` untuk resolusi nama.
3. Melakukan restart jaringan agar perubahan diterapkan.
4. Memastikan koneksi internet dengan `ping google.com`.
5. Mengganti hostname menjadi `server1.example.com`.
