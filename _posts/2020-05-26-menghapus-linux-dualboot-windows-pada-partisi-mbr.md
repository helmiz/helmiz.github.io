---
title: "Menghapus Linux Dualboot Windows Pada Partisi MBR"
categories:
  - Sistem Operasi
tags:
  - Partisi
date: 2020-05-26 18:27:25 +0700
classes: wide
---
Pada kesempatan ini saya ingin berbagi sekaligus catatan bagi saya jika sewaktu-waktu lupa. Cara ini sudah saya praktikan di laptop saya sendiri. Berikut adalah langkah-langkahnya:

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