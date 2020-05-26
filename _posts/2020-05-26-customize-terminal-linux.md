---
layout: post
title:  Customize Terminal Linux 
date: 2020-05-26 19:50:25 +0700
categories: [linux]
---
Mengatur atau modifikasi tema di Linux dan macOS menggunakan Gogh Color Schemes. Dengan syarat:
- Linux support: ***Gnome Terminal***, ***Pantheon Terminal***, ***Tilix*** dan ***XFCE4 Terminal***.
- MacOS support: ***iTerm***.

Pemasangan
----------
1. Pre-Install
    ```
    sudo apt-get install dconf-cli uuid-runtime
    ```
2. Copy dan Paste kode berikut pada Command Line:
    ```
    bash -c  "$(wget -qO- https://git.io/vQgMr)"
    ```
    Pengguna Mac:
    ```
    bash -c  "$(curl -sLo- https://git.io/vQgMr)"
    ```
3. Tema bisa dilihat di [https://mayccoll.github.io/Gogh/](https://mayccoll.github.io/Gogh/).

4. Masukan `Nomor` tema yang diinginkan.



Problem-Solved
--------------
Jika terdapat pesan *Error* seperti di bawah:
```
bash: line 655: read: `/apps/gnome-terminal/profiles/default_profile': not a valid identifier
environment: line 402: --get: command not found
environment: line 411: --get: command not found
environment: line 222: : command not found
environment: line 222: : command not found
environment: line 205: : command not found
environment: line 205: : command not found
environment: line 205: : command not found
environment: line 205: : command not found
environment: line 205: : command not found
environment: line 205: : command not found
environment: line 205: : command not found
environment: line 205: : command not found
environment: line 205: : command not found
```  
Solusi:  

1. Reset profiles dengan mengetik:
    ```
    dconf reset -f /org/gnome/terminal/legacy/profiles:/
    ```
2. Tutup Terminal dan Buka kembali.

3. Klik menu `Edit` pada terminal, pilih `Preferences` dan pilih `Profiles`.

4. Membuat *profile* baru dengan nama `Default`.

5. Tutup Terminal dan Buka kembali. Pastikan `Default` masih ada di dalam daftar *profiles* pada terminal.

6. Jalankan Script Gogh kembali.  
<br />
<br />

***Sumber***:
- D, Miguel Quintero. 2020. [Gogh](https://github.com/Mayccoll/Gogh) (diakses tanggal 26 Mei 2020).
- Kogam22. 2019. [On type highlighting](https://github.com/Mayccoll/Gogh/issues/177) (diakses tanggal 26 Mei 2020).