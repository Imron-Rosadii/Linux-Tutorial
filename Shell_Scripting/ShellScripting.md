# 📌 Shell Scripting (RHCSA)

## 1. Script `/usr/local/bin/hello.sh` yang Menampilkan "Hello RHCSA"

Buat file script `hello.sh` yang menampilkan pesan "Hello RHCSA".

1. **Buat file script** dengan perintah:

   ```bash
   sudo nano /usr/local/bin/hello.sh
   ```

2. **Isi file tersebut dengan script berikut**:

   ```bash
   #!/bin/bash
   echo "Hello RHCSA"
   ```

   **Penjelasan:**

   - `#!/bin/bash`: Menentukan bahwa script ini dijalankan menggunakan interpreter `bash`.
   - `echo "Hello RHCSA"`: Menampilkan pesan "Hello RHCSA" ke layar.

3. **Beri izin eksekusi pada file**:

   ```bash
   sudo chmod +x /usr/local/bin/hello.sh
   ```

4. **Jalankan script**:

   ```bash
   hello.sh
   ```

---

## 2. Script untuk Mengecek Apakah `/etc/passwd` Ada

Buat script untuk mengecek apakah file `/etc/passwd` ada. Jika ada, tampilkan "OK", jika tidak, tampilkan "Not Found".

1. **Buat file script** dengan perintah:

   ```bash
   sudo nano /usr/local/bin/check_passwd.sh
   ```

2. **Isi file tersebut dengan script berikut**:

   ```bash
   #!/bin/bash

   if [ -f /etc/passwd ]; then
       echo "OK"
   else
       echo "Not Found"
   fi
   ```

   **Penjelasan:**

   - `if [ -f /etc/passwd ]`: Mengecek apakah file `/etc/passwd` ada dengan menggunakan operator `-f`.
   - `echo "OK"`: Jika file ada, tampilkan "OK".
   - `echo "Not Found"`: Jika file tidak ada, tampilkan "Not Found".

3. **Beri izin eksekusi pada file**:

   ```bash
   sudo chmod +x /usr/local/bin/check_passwd.sh
   ```

4. **Jalankan script**:

   ```bash
   check_passwd.sh
   ```

---

## 3. Script Looping untuk Mencetak Angka 1–10

Buat script yang mencetak angka 1 hingga 10 menggunakan looping `for`.

1. **Buat file script** dengan perintah:

   ```bash
   sudo nano /usr/local/bin/loop_numbers.sh
   ```

2. **Isi file tersebut dengan script berikut**:

   ```bash
   #!/bin/bash

   for i in {1..10}
   do
       echo $i
   done
   ```

   **Penjelasan:**

   - `for i in {1..10}`: Membuat loop untuk mencetak angka dari 1 hingga 10.
   - `echo $i`: Menampilkan angka yang sedang diproses dalam loop.

3. **Beri izin eksekusi pada file**:

   ```bash
   sudo chmod +x /usr/local/bin/loop_numbers.sh
   ```

4. **Jalankan script**:

   ```bash
   loop_numbers.sh
   ```

---

## 4. Script yang Menerima Argumen dan Menampilkan "Welcome $1"

Buat script yang menerima argumen (misalnya nama) dan menampilkan pesan "Welcome $1".

1. **Buat file script** dengan perintah:

   ```bash
   sudo nano /usr/local/bin/welcome.sh
   ```

2. **Isi file tersebut dengan script berikut**:

   ```bash
   #!/bin/bash

   echo "Welcome $1"
   ```

   **Penjelasan:**

   - `$1`: Ini adalah parameter pertama yang diterima oleh script (misalnya, nama yang dimasukkan saat menjalankan script).
   - `echo "Welcome $1"`: Menampilkan pesan "Welcome" diikuti dengan argumen yang diberikan.

3. **Beri izin eksekusi pada file**:

   ```bash
   sudo chmod +x /usr/local/bin/welcome.sh
   ```

4. **Jalankan script dengan argumen**:

   ```bash
   welcome.sh John
   ```

   Hasilnya:

   ```
   Welcome John
   ```

---

## Kesimpulan

Langkah-langkah di atas mencakup:

- **hello.sh**: Menampilkan pesan statis "Hello RHCSA".
- **check_passwd.sh**: Mengecek apakah file `/etc/passwd` ada dan menampilkan "OK" atau "Not Found".
- **loop_numbers.sh**: Mencetak angka 1 hingga 10 menggunakan looping.
- **welcome.sh**: Menerima argumen dan menampilkan pesan "Welcome $1".

Proses ini adalah bagian dari **Red Hat Certified System Administrator (RHCSA)** yang menguji kemampuan dasar dalam pembuatan dan eksekusi shell script untuk automasi di sistem Linux.
