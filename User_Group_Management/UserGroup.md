# 🧑‍💻 User & Group Management (RHCSA)

Manajemen **user** dan **group** merupakan salah satu topik penting dalam ujian **RHCSA (Red Hat Certified System Administrator)**. Berikut langkah-langkah dasar yang sering muncul, lengkap dengan contoh perintah.

---

## 1. Membuat User Baru

**Task:** Buat user bernama `student` dengan password `Redhat123`.

```bash
# Membuat user baru
useradd student

# Set password untuk user student
echo "Redhat123" | passwd --stdin student
```

📌 **Penjelasan:**

- `useradd student` → membuat user baru bernama `student`.
- `passwd --stdin` → membaca password dari input standar (`echo`) agar bisa otomatis.

---

## 2. Membuat Group Baru

**Task:** Buat group bernama `developers` lalu tambahkan user `student` ke dalamnya.

```bash
# Membuat group developers
groupadd developers

# Menambahkan user student ke dalam group developers
usermod -aG developers student
```

📌 **Penjelasan:**

- `groupadd developers` → membuat group baru bernama `developers`.
- `usermod -aG developers student` → menambahkan (`-a`) user `student` ke dalam group tambahan (`-G`).

---

## 3. Mengatur Expiry Date (Kadaluarsa User)

**Task:** Atur agar akun `student` kadaluarsa dalam **30 hari ke depan**.

```bash
# Hitung tanggal kadaluarsa (30 hari ke depan)
date -d "+30 days"

# Atur tanggal expiry user
chage -E $(date -d "+30 days" +%Y-%m-%d) student
```

📌 **Penjelasan:**

- `date -d "+30 days"` → menampilkan tanggal 30 hari ke depan.
- `chage -E YYYY-MM-DD student` → menetapkan tanggal expiry user.

---

## 4. Mengecek UID dan GID User

**Task:** Cek UID (User ID) dan GID (Group ID) dari user `student`.

```bash
# Menampilkan informasi user student
id student

# Atau cek detail di file /etc/passwd
grep student /etc/passwd
```

📌 **Penjelasan:**

- `id student` → menampilkan UID, GID, dan group user.
- `grep student /etc/passwd` → melihat entri detail user di file konfigurasi sistem.

---

## 5. Verifikasi

Setelah semua langkah dijalankan, pastikan:

```bash
# Cek user di sistem
getent passwd student

# Cek group developers
getent group developers

# Cek expiry date
chage -l student
```

---

## 📌 Kesimpulan

1. Kita membuat user `student` dan password `Redhat123`.
2. Membuat group `developers` dan menambahkan user ke group tersebut.
3. Mengatur **expiry date** user agar aktif hanya 30 hari.
4. Mengecek UID dan GID user `student` dengan perintah `id`.
5. Melakukan verifikasi dengan `getent` dan `chage`.
