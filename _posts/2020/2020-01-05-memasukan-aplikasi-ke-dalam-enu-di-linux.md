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
  Catatan:
  * `nama_aplikasi` dapat diganti dengan nama aplikasi yang ingin kita munculkan ke dalam Menu Aplikasi.
  * `gedit` adalah aplikasi text editor yang saya gunakan. Bisa diganti dengan `vi` atau `nano`.

2. Salin dan tempelkan kode berikut ke dalam aplikasi text editor:
```
[Desktop Entry]
Encoding=UTF-8
Exec=/home/helmiz/tools/eclipse/eclipse
Icon=/home/helmiz/tools/eclipse/icon.xpm
Type=Application
Terminal=false
Comment=Eclipse Integrated Development Environment
Name=Eclipse 2019
GenericName=eclipse-2019-12-R
StartupNotify=false
Categories=Development;IDE;Java;
```
Catatan:
* `Exec` adalah path dimana kita menyimpan nama aplikasi. Penulisan path harus jelas dan benar jika tidak maka aplikasi tidak akan muncul pada Menu Aplikasi.
* `Icon` adalah path dimana kita menyimpan icon untuk aplikasi. Penulisan path harus jelas dan benar jika tidak maka gambar aplikasi tidak akan muncul pada Menu Aplikasi.
* `Name` adalah nama untuk aplikasi. Disini kita bisa ganti nama sesuai dengan keinginan kita.
* `GenericName` adalah nama aplikasi beserta versinya. Disini kita bisa ganti nama sesuai dengan keinginan kita.
* `Comment` adalah deskripsi aplikasi.
* `Categories` adalah kategori aplikasi yang ingin kita munculkan.

3. Simpan dan keluar dari aplikasi teks editor yang kita gunakan untuk membuat file `.desktop`.

4. Lakukan pengecekan pada pencarian Menu Aplikasi. Jika tidak muncul kemungkinan salah pada saat memasukan path.

{% capture notice-2 %}
#### Tambahan

* Untuk menentukan `categories` dapat mengunjungi tautan ini <a href="https://askubuntu.com/questions/674403/when-creating-a-desktop-file-what-are-valid-categories">https://askubuntu.com</a>.
* Ada beberapa aplikasi yang tidak menyertakan gambar seperti aplikasi dari .Appimage. maka kita dapat mengunduhnya di google dan menyimpan satu folder dengan aplikasi tersebut.
{% endcapture %}

<div class="notice">{{ notice-2 | markdownify }}</div>

## Daftar Pustaka
- jahid_0903014. 2014. [Install latest eclipse in linux mint](https://community.linuxmint.com/tutorial/view/1503) (diakses tanggal 5 Januari 2020).