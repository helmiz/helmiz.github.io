---
layout: post
title: Menampilkan Aplikasi Pada Menu di Linux
date:   2020-05-08 16:26:25 +0700
categories: linux

---
Saya ingin berbagi bagaimana cara agar aplikasi yang kita download dapat tampil pada menu di Linux karena ada beberapa aplikasi untuk linux yang tidak langsung menginstall (biasanya dibundle dengan tar atau zip). Aplikasi yang saya contohkan adalah **Eclipse IDE**. Sebenarnya aplikasi linux yang kita download sudah bisa diigunakan secara langsung dengan klik dua kali pada aplikasi tersebut tanpa harus menambahkannya ke dalam Menu Aplikasi. Berikut adalah caranya:  
  
1.  Pastikan aplikasi sudah diekstrak karena biasanya aplikasi dibundle dengan tar atau zip. Kalau aplikasi dibundle dengan deb untuk Ubuntu/debian atau rpm untuk Fedora maka aplikasi langsung terinstall dan muncul di Menu Aplikasi sehingga tidak perlu melanjutkan cara ini.

2. Buka Terminal atau Console dan ketik kode berikut:  
    ```
    sudo gedit /usr/share/applications/nama_aplikasi.desktop
    ```
    Catatan:
    -   `nama_aplikasi` dapat diganti dengan nama aplikasi yang ingin kita munculkan pada Menu Aplikasi.
	-   `gedit` adalah aplikasi text editor yang saya gunakan. Bisa diganti dengan `vim` atau `nano`.

3. Salin dan tempelkan kode berikut ke dalam aplikasi text editor:  
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
-   `Exec` adalah path dimana kita menyimpan nama aplikasi. Penulisan path harus jelas dan benar jika tidak maka aplikasi tidak akan muncul pada Menu Aplikasi.
-   `Icon` adalah path dimana kita menyimpan icon untuk aplikasi. Penulisan path harus jelas dan benar jika tidak maka gambar aplikasi tidak akan muncul pada Menu Aplikasi.
-   `Name` adalah nama untuk aplikasi. Disini kita bisa ganti nama sesuai dengan keinginan kita.
-   `GenericName` adalah nama umum aplikasi atau nama jenis aplikasinya, contohnya "Web Browser".
-   `Comment` adalah deskripsi aplikasi, contohnya "Untuk melihat website di Internet".
-   `Categories` adalah tempat dimana aplikasi ditampilkan pada menu. Lihat bagian tambahan di bawah.
- `Type` adalah spesifikasi pada aplikasi desktop yang memiliki tiga jenis, yaitu `Application`, `Link`, dan`Directory`.

4. Simpan dan keluar dari aplikasi teks editor yang kita gunakan untuk membuat file `.desktop`.

5. Lakukan pengecekan pada pencarian pada Menu Aplikasi. Jika tidak muncul kemungkinan salah pada saat memasukan path pada bagian `Exec`.

**Tambahan**:
-   Untuk menentukan `categories` dapat mengunjungi tautan [https://askubuntu.com](https://askubuntu.com/questions/674403/when-creating-a-desktop-file-what-are-valid-categories) atau [freedesktop.org](https://specifications.freedesktop.org/menu-spec/menu-spec-1.0.html) pada bagian Registered Categories.
- Untuk mengetahui isi dan penjelasan lebih lengkap pada Desktop Entry dapat mengunjungi tautan [freedesktop.org](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html)
-  Ada beberapa aplikasi yang tidak menyertakan gambar seperti aplikasi dari .Appimage. maka kita dapat mengunduhnya di google dan menyimpan satu folder dengan aplikasi tersebut.

_**Sumber**_:  
- jahid_0903014. 2014. [install latest eclipse in linux mint](https://community.linuxmint.com/tutorial/view/1503). (diakses tanggal 8 Mei 2020).
- Bastian, Waldo, dkk. [Desktop Menu Specification](https://specifications.freedesktop.org/menu-spec/menu-spec-1.0.html). (diakses tanggal 8 Mei 2020).
- Brown, Preston, dkk. [Desktop Entry Specification](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html). (diakses tanggal 8 Mei 2020).
