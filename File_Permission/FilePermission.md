# 📂 File Permissions & ACL (RHCSA)

Manajemen **permission** dan **Access Control List (ACL)** sangat penting dalam keamanan Linux.
Berikut studi kasus sesuai task:

---

## 1. Buat Direktori `/project`

**Task:** Buat direktori `/project` yang dimiliki oleh user `student` dan group `developers`.

```bash
# Membuat direktori /project
mkdir /project

# Mengubah kepemilikan direktori
chown student:developers /project
```

📌 **Penjelasan:**

- `mkdir /project` → membuat direktori baru.
- `chown student:developers /project` → mengatur owner ke `student` dan group ke `developers`.

---

## 2. Atur Permission Direktori

**Task:** Beri permission `770` pada `/project`.

```bash
chmod 770 /project
```

📌 **Penjelasan:**

- `770` = **rwxrwx---**

  - `rwx` → owner (student) full akses.
  - `rwx` → group (developers) full akses.
  - `---` → user lain tidak bisa akses.

---

## 3. Buat File `doc.txt` di Dalam `/project`

**Task:** Buat file `doc.txt` lalu berikan ACL agar user `student` punya `rw-`.

```bash
# Membuat file
touch /project/doc.txt

# Memberikan ACL agar user student punya rw-
setfacl -m u:student:rw /project/doc.txt
```

📌 **Penjelasan:**

- `touch` → membuat file kosong.
- `setfacl -m u:student:rw` → memberi ACL (modify, -m) untuk user `student` dengan permission **read & write**.

---

## 4. Pastikan User Lain Tidak Bisa Akses

**Task:** Cek ACL dan coba akses dengan user lain.

```bash
# Lihat permission dan ACL
ls -l /project/doc.txt
getfacl /project/doc.txt

# Misalnya coba dengan user lain (contoh: testuser)
su - testuser
cat /project/doc.txt   # harusnya "Permission denied"
```

📌 **Penjelasan:**

- `ls -l` → melihat permission dasar.
- `getfacl` → melihat ACL detail.
- User lain yang bukan `student` atau anggota `developers` tidak bisa membuka file.

---

## 5. Verifikasi

```bash
# Cek kepemilikan direktori
ls -ld /project

# Cek ACL file
getfacl /project/doc.txt
```

Contoh hasil `getfacl`:

```
# file: project/doc.txt
# owner: student
# group: developers
user::rw-
user:student:rw-
group::r--
mask::rw-
other::---
```

---

## 📌 Kesimpulan

1. Direktori `/project` dibuat dan dimiliki oleh user `student` dan group `developers`.
2. Permission `770` → hanya `student` dan `developers` yang bisa akses.
3. File `doc.txt` diberi ACL agar `student` punya akses **rw-**.
4. User lain (di luar group) **tidak bisa mengakses** file tersebut.

---
