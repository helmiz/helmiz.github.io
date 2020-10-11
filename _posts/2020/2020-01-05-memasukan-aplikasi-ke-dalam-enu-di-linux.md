---
title: "Memasukan Aplikasi ke dalam Menu di Linux"
categories:
  - Sistem Operasi
tags:
  - Aplikasi
date: 2020-01-05 18:27:25 +0700
classes: wide
---
Pastikan aplikasi sudah diekstrak karena biasanya aplikasi dibundle dengan tar atau zip. Kalau aplikasi dibundle dengan deb untuk Ubuntu/debian atau rpm untuk Fedora maka aplikasi langsung terinstall dan muncul di Menu Aplikasi sehingga tidak perlu melanjutkan cara ini.
1. Buka Terminal atau Console dan ketik kode berikut:
```
sudo gedit /usr/share/applications/nama_aplikasi.desktop
```
{% capture notice-2 %}
#### Catatan

* `nama_aplikasi` dapat diganti dengan nama aplikasi yang ingin kita munculkan ke dalam Menu Aplikasi.
* gedit adalah aplikasi text editor yang saya gunakan. Bisa diganti dengan `vi` atau `nano`.
{% endcapture %}

<div class="notice">{{ notice-2 | markdownify }}</div>


## I. Pengecekan
Memastikan apakah Disk kita memakai MBR atau tidak, dengan cara buka `Disk Management` di pencarian Windows. Setelah itu klik kanan pada `Hard Disk` kita (biasanya Hard Disk 0). Pilih `Properties` dan klik Tab bagian `Volumes`. Mari kita perhatikan gambar di bawah ini:
<figure class="half">
    <a href="/assets/images/2020/menghapus-linux-dualboot/01-disk_management.png"><img src="/assets/images/2020/menghapus-linux-dualboot/01-disk_management.png"></a>
    <a href="/assets/images/2020/menghapus-linux-dualboot/02-properties.png"><img src="/assets/images/2020/menghapus-linux-dualboot/02-properties.png"></a>
    <figcaption>Gambar pada Disk Management dan Tab Volumes pada Properties.</figcaption>
</figure>

## II. Download
Download Mini Tool Partition Wizard (Free) pada link berikut: [https://www.partitionwizard.com/free-partition-manager.html](https://www.partitionwizard.com/free-partition-manager.html)

## III. Melakukan Partisi
Pada program Mini Tool Partition Wizard, pilih `Disk & Partition Management`. Ikuti gambar dan penjelasan berikut sebagai petunjuk:
<figure>
    <a href="/assets/images/2020/menghapus-linux-dualboot/03-mini_tool_partition.png"><img src="/assets/images/2020/menghapus-linux-dualboot/03-mini_tool_partition.png"></a>
    <figcaption>Gambar Disk & Partition Management.</figcaption>
</figure>
1. Pilih partisi yang mengandung linux (punya saya partisi 3). Klik kanan dan pilih Delete.
2. Pilih Disk yang partisinya di Delete tadi (punya saya disk 1). Klik kanan dan pilih Rebuild MBR.
3. Operations Pending yang berisi Informasi alur yang sudah kita lakukan yaitu Delete partisi dan rebuild MBR, tetapi masih bisa kita Undo atau tidak jadi.
4. Apply jika sudah yakin.