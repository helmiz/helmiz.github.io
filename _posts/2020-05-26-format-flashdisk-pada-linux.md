---
layout: post
title: Format Flash Disk pada Linux
date: 2020-05-26 17:19:25 +0700
categories: [linux]
---
Berikut adalah cara format Flash Disk atau Flash Drive menggunakan command line di terminal Linux. Hal yang akan kita lakukan:
- Terminal linux karena pada aplikasi _GUI_ yang terinstall yaitu _Disk_ tidak bisa digunakan.
- Perintah fdisk untuk menghapus dan membuat partisi.
- Perintah mkfs untuk menyusun ulang (*format*) partisi.  

Petunjuk
--------
1.  Identifikasi letak USB Flash Disk yang terpasang pada sistem linux dengan cara:
	
	```bash
	lsblk
	```
	
	Maka akan tampil:
	
	```bash
	NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINT  
	sda    8:0   0 111,8G 0 disk  
	├─sda1 8:1   0 549M   0 part  
	├─sda2 8:2   0 56,3G  0 part  
	└─sda3 8:3   0 55G    0 part /  
	sdd    8:16  1 3,7G   0 disk  
	└─sdd1 8:17  1 3,7G   0 part /media/helmiz/HELMI  
	sr0    11:0  1 1024M  0 rom
	```
2. Melepas (Unmount) USB Flash Drive yang terbaca di sistem linux:
	```bash
	sudo umount /dev/sdd1
	```  
    
FDISK
------
1. Ketik perintah di bawah pada terminal linux:
	
	```bash
	sudo fdisk /dev/sdc
	```
	
	Ketik `p` untuk *print* ke layar. Maka akan muncul tampilan seperti ini (dalam hal ini partisi Flash Disk saya):
	
	```bash
	Disk /dev/sdd: 3,75 GiB, 4002910208 bytes, 7818184 sectors
	Disk model: DataTraveler G2 
	Units: sectors of 1 * 512 = 512 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disklabel type: dos
	Disk identifier: 0x15f006ae

	Device     Boot Start     End Sectors  Size Id Type
	/dev/sdd1        2048 7818183 7816136  3,7G  7 HPFS/NTFS/exFAT

    ```
    
2. Ketik `d` untuk menghapus (*delete*) setiap partisi.

3. Ketik `o` untuk membuat (*new*) DOS partisi baru.

4. Ketik `n` untuk membuat (*new*) partisi baru.

5. Selanjutnya akan muncul pilihan jenis partisi *Primary* (utama) atau *Extended* (tambahan), tekan `Enter` atau `p`.
	```bash
	Partition type
	p   primary (0 primary, 0 extended, 4 free)
	e   extended (container for logical partitions)
	Select (default p): 
	```
	
6. Lalu akan muncul pilihan tambahan, tekan `Enter` untuk memberikan nilai *default*.
	```bash
	Using default response p.
	Partition number (1-4, default 1): 
	First sector (2048-7818183, default 2048): 
	Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-7818183, default 7818183): 
	```

7. Secara *default* jenis partisi akan menjadi Linux. Untuk melihat daftar jenis partisi dapat mengetik `l`, pilih jenis partisi yang diinginkan seperti `7 HPFS/NTFS/exFAT` untuk partisi ***NTFS*** dan ***exFat*** serta `b W95 FAT32` untuk ***Fat32***. Mengganti jenis partisi dengan mengetik `t` dan masukan `id` jenis partisi.

8. Ketik `w` untuk menulis/mengaplikasikan proses yang kita lakukan ke dalam Flash Disk.

9. Ketik `q` untuk keluar (*quit*).  

MKFS
----
Langkah terakhir melakukan *format* Flash Disk dengan cara:
1. Format dengan Fat32
	```bash
	sudo mkfs.vfat -F32 -n NAMA /dev/sdd1
	```
	- -n NAMA: nama USB Flash Drive kita (menggunakan huruf kapital).
	- -F32: Membuat Fat32.  
    <br />

2. Format dengan NTFS
	```bash
	sudo mkfs.ntfs -f -L NAMA /dev/sdd1
	```
	- -f: pilihan untuk quick format
	- -L NAMA: nama USB Flash Drive kita (menggunakan huruf kapital).  
    <br />
    
3. Format dengan exFat
	Install beberapa paket tambahan (Ubuntu):
	```bash
	sudo apt install dosfstools exfat-fuse exfat-utils
	```
	Format:
	```bash
	sudo mkfs.exfat -n NAMA /dev/sdd1
	```
	- -n NAMA: nama USB Flash Drive kita (menggunakan huruf kapital).  
    
Terkadang USB Flash Drive yang kita format tidak terbaca padahal terbaca di Windows. Solusinya adalah:
1. Masuk ke Partition Manager.
    
2. Pilih dan klik kanan USB yang terbaca di bagian bawah.

3. Pilih Change letter….

4. Lalu kita pilih huruf yang digunakan sebagai penanda USB Flash Drive ke sistem.
<br />
<br />

**Sumber:**
- Kumar, Rahul. [How To Format USB Drive in Linux Command Line ](https://tecadmin.net/format-usb-in-linux/) (diakses tanggal 1 April 2020).
- Saive, Ravi. 2015. [10 fdisk Commands to Manage Linux Disk Partitions](https://www.tecmint.com/fdisk-commands-to-manage-linux-disk-partitions/) (diakses tanggal 26 Mei 2020).
- Bunic, Darko. 2020. [How to create FAT32 USB drive on Linux](https://www.redips.net/linux/create-fat32-usb-drive/) (diakses tanggal 26 Mei 2020).
- Gary Explains. 2019. [How to Partition and Format a Disk in Linux](https://www.youtube.com/watch?v=JCFlsslBvX8&list=WL&index=9&t=535s) diakses tanggal 26 Mei 2020).