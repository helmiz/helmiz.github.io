---
title: "Mempercantik Tampilan Terminal Linux"
categories:
  - Sistem Operasi
tags:
  - Terminal
date: 2020-05-27 17:19:25 +0700
classes: wide
---
Mengatur atau modifikasi tema di Linux dan macOS menggunakan Gogh Color Schemes. Dengan syarat:
- Linux support: ***Gnome Terminal***, ***Pantheon Terminal***, ***Tilix*** dan ***XFCE4 Terminal***.
- MacOS support: ***iTerm***.

## Pemasangan
1. Pre-Install pada ubuntu:
```
sudo apt-get install dconf-cli uuid-runtime
```
2. Jalankan perintah berikut dengan cara copy dan paste ke terminal/konsole:
```
bash -c  "$(wget -qO- https://git.io/vQgMr)"
```
Pengguna Mac:
```
bash -c  "$(curl -sLo- https://git.io/vQgMr)"
```
3. Selanjutnya muncul tampilan di bawah. Pilih *Nomor* tampilan yang diinginkan dan tekan *ENTER*.
```
                                                                                
                    █████████                    █████                          
                   ███     ███                    ███                           
                  ███           ██████   ███████  ███████                       
                  ███          ███  ███ ███  ███  ███  ███                      
                  ███    █████ ███  ███ ███  ███  ███  ███                      
                   ███    ███  ███  ███ ███  ███  ███  ███                      
                    █████████   ██████   ███████ ████ █████                     
    ████████████████████████████████████████████████████████████████████████    
    ████████████████████████████████████████████████████████████████████████    
    ████████████████████████████████████████████████████████████████████████    
    ████████████████████████████████████████████████████████████████████████    
    ████████████████████████████████████████████████████████████████████████    
    ████████████████████████████████████████████████████████████████████████
Themes:
    ( 01 ) 3024 Day
    ( 02 ) 3024 Night
    ( 03 ) Aci
    ( 04 ) Aco
    ( 05 ) Adventuretime

    ...
    ...    
```

4. Semua tampilan bisa dilihat di [https://mayccoll.github.io/Gogh/](https://mayccoll.github.io/Gogh/).

## Permasalahan
Jika terdapat pesan *Error* seperti di bawah:
```bash
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
    ```bash
    dconf reset -f /org/gnome/terminal/legacy/profiles:/
    ```
2. Tutup Terminal dan Buka kembali.

3. Klik menu `Edit` pada terminal, pilih `Preferences` dan pilih `Profiles`.

4. Membuat *profile* baru dengan nama `Default`.

5. Tutup Terminal dan Buka kembali. Pastikan `Default` masih ada di dalam daftar *profiles* pada terminal.

6. Jalankan Script Gogh kembali.  

## Daftar Pustaka
- D, Miguel Quintero. 2020. [Gogh](https://github.com/Mayccoll/Gogh) (diakses tanggal 26 Mei 2020).
- Kogam22. 2019. [On type highlighting](https://github.com/Mayccoll/Gogh/issues/177) (diakses tanggal 26 Mei 2020).
