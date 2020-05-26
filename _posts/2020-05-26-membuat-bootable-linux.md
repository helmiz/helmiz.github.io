---
layout: post
title:  Membuat Bootable Linux pada Sistem Operasi Linux 
date: 2020-05-26 19:50:25 +0700
categories: [linux]
---
Pada kesempatan kali ini, saya akan memasang linux ke dalam Flash Disk di sistem operasi Linux. Saya menggunakan command ***dd*** pada bash di terminal linux. Berikut adalah langkahnya:  

1.  Mengecek dimana Flash Disk kita terbaca oleh sistem linux kita dengan cara:
    ```
    lsblk
    ```
    Contoh tampilan:
    Dapat dilihat bahwa Flash Disk saya terbaca di sdb1.
    ```
    NAME MAJ:MIN RM SIZE   RO TYPE MOUNTPOINT
    sda    8:0   0  111,8G 0  disk
    ├─sda1 8:1   0  549M   0  part
    ├─sda2 8:2   0  56,3G  0  part
    └─sda3 8:3   0  55G    0  part  /
    sdb    8:16  1  3,7G   0  disk
    ├─sdb1 8:17  1  1,9G   0  part  /media/username/usb volume name
    └─sdb2 8:18  1  2,4M   0  part
    ```  

2.  Melepaskan pembacaan (*unmount*) Flash disk dengan sistem linux kita dengan cara:
    ```
    sudo umount /dev/sdXX
    ```
    Catatan:
    - X pertama adalah huruf dimana Flash Disk kita terbaca.
    - X kedua adalah angka dimana Flash Disk kita terbaca.
    - Dalam hal ini, command yang saya gunakan adalah:
    ```
    sudo umount /dev/sdb1
    ```  

3. Langkah terakhir, Proses penghapusan isi dari Flash Disk dan pemasangan linux dengan cara:
    ```
    sudo dd bs=4M if=path/to/input.iso of=/dev/sdX status=progress
    ```
    Catatan:
    - if adalah path atau tempat dimana input file berada.
    - of adalah path Flash disk terbaca oleh sistem linux.
    - X adalah huruf Flash disk terbaca pada langkah pertama tanpa diikuti angka.
    - Dalam hal ini, saya mengeksekusi:
    ```
    sudo dd bs=4M if=~/Downloads/ubuntu-mate-18.04.2-desktop-amd64.iso of=/dev/sdb status=progress
    ```
    Contoh proses:
    ```
    2051014656 bytes (2,1 GB, 1,9 GiB) copied, 217 s, 9,4 MB/s
    489+1 records in
    489+1 records out
    2053521408 bytes (2,1 GB, 1,9 GiB) copied, 521,076 s, 3,9 MB/s
    ```  
<br />
<br />

***Sumber***:
- Marc dan rogerdpack. 2019. [How to create a bootable Ubuntu USB flash drive from terminal?](https://askubuntu.com/a/377561) (diakses tanggal 26 Mei 2020).  

