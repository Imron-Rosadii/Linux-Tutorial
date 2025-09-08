# 📌 Rangkuman & Langkah Belajar File Management (RHCSA)

## 1. Membuat Direktori & Pindah

```bash
mkdir -p /lab/files
cd /lab/files
```

* `mkdir -p` → membuat folder `/lab/files` (otomatis buat parent folder jika belum ada).
* `cd` → pindah ke folder kerja.

---

## 2. Membuat File

```bash
echo "ini adalah catatan pertama saya di Linux." > notes.txt
```

* `echo` → menampilkan teks.
* `>` → redirect output ke file (`notes.txt`).
* Hasil: file baru berisi teks.

Cek isi:

```bash
cat notes.txt
```

---

## 3. Redirect Output ke File

```bash
ls -l /etc > list.txt
```

* Menyimpan daftar isi folder `/etc` ke file `list.txt`.

---

## 4. Mencari Teks dengan grep

```bash
grep root /etc/passwd
```

* Menampilkan baris yang mengandung kata *root*.

```bash
grep "^root" /etc/passwd
```

* Menampilkan baris yang diawali kata *root* (`^` = anchor awal baris).

---

## 5. Membuat Hardlink & Softlink

```bash
ln notes.txt notes_hardlink.txt
ln -s notes.txt notes_softlink.txt
ls -l
```

* **Hardlink** (`ln`) → file kembar dengan inode sama. Jika isi diubah/hapus salah satunya, yang lain tetap sama.
* **Softlink** (`ln -s`) → shortcut yang menunjuk ke file asli. Jika file asli dihapus, softlink jadi rusak.

---

## 6. Arsipkan File dengan tar

```bash
tar -cvf backup.tar /etc/hosts /etc/passwd
```

* `c` → create arsip
* `v` → tampilkan proses
* `f` → nama file output
* Hasil: file arsip `backup.tar` berisi dua file `/etc/hosts` dan `/etc/passwd`.

---

## 7. Kompres Arsip dengan gzip

```bash
gzip backup.tar
```

* Mengompres `backup.tar` → menjadi `backup.tar.gz`.
* Atau bisa langsung arsip + kompres:

```bash
tar -czvf backup.tar.gz /etc/hosts /etc/passwd
```

---

## 8. Cek Isi Arsip Tanpa Ekstrak

```bash
tar -tzf backup.tar.gz
```

* `t` → tampilkan isi arsip.
* `z` → file dikompres gzip.
* `f` → nama file arsip.

Output contoh:

```
etc/hosts
etc/passwd
```

