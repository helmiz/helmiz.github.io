---
layout: post
title: Menghapus Linux Dualboot Windows Pada Partisi MBR
date: 2020-05-26 18:27:25 +0700
categories: [windows]
---
Pada kesempatan ini saya ingin berbagi sekaligus catatan bagi saya jika sewaktu-waktu lupa. Cara ini sudah saya praktikan di laptop saya sendiri. Berikut adalah langkah-langkahnya:

1. Memastikan apakah Disk kita memakai MBR atau tidak, dengan cara buka `Disk Management` di pencarian Windows. Setelah itu klik kanan pada `Hard Disk` kita (biasanya Hard Disk 0). Pilih `Properties` dan klik Tab bagian `Volumes`. Perhatikan gambar di bawah.
    [![Disk Management]({{site.url}}/images/2020/menghapus-linux-dualboot/01-disk_management.png)]({{site.url}}/images/2020/menghapus-linux-dualboot/01-disk_management.png)

    [![Properties]({{site.url}}/images/2020/menghapus-linux-dualboot/02-properties.png)]({{site.url}}/images/2020/menghapus-linux-dualboot/02-properties.png)


2. Download Mini Tool Partition Wizard (Free) pada link berikut: [https://www.partitionwizard.com/free-partition-manager.html](https://www.partitionwizard.com/free-partition-manager.html)

3. Pada program Mini Tool Partition Wizard, pilih `Disk & Partition Management`. Ikuti gambar dan penjelasan berikut sebagai petunjuk:
    [![Mini Tool Partition]({{site.url}}/images/2020/menghapus-linux-dualboot/03-mini_tool_partition.png)]({{site.url}}/images/2020/menghapus-linux-dualboot/03-mini_tool_partition.png)

    - 3.1 Pilih partisi yang mengandung linux (punya saya partisi 3). Klik kanan dan pilih Delete.

    - 3.2 Pilih Disk yang partisinya di Delete tadi (punya saya disk 1). Klik kanan dan pilih Rebuild MBR.

    - 3.3 Operations Pending yang berisi Informasi alur yang sudah kita lakukan yaitu Delete partisi dan rebuild MBR, tetapi masih bisa kita Undo atau tidak jadi.

    - 3.4 Apply jika sudah yakin