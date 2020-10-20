---
title: "Mengaktifkan Fitur Shared Folder, Shared Clipboard dan Drag and Drop pada VirtualBox"
categories:
  - Konfigurasi
tags:
  - VirtualBox
date: 2020-10-11 18:23:25 +0700
classes: wide
---
Pada konfigurasi ini kita menggunakan sistem operasi:
- Windows 7
- Ubuntu
- CentOS

## Pengaturan VirtualBox
Pastikan kita sudah menginstall sistem operasi yang akan dikonfigurasi. 
<figure class="align-center">
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2020/mengaktifkan-fitur-pada-virtualbox/1-pengaturan-vbox.png"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/2020/mengaktifkan-fitur-pada-virtualbox/1-pengaturan-vbox.png" alt="Gambar bagian Settings pada VBox"></a>
    <figcaption>Gambar A untuk langkah 3, 4, dan 5.</figcaption>
</figure>

1. Pilih sistem operasi pada VirtualBox.
2. Tekan menu ***Settings***.
3. Pilih tab ***Shared Folders***.
4. Klik icon ***Adds new shared folder*** pada bagian kanan.
5. Akan muncul Pop-up *Add Share*.
6. Pada ***Folder Path***, pilih direktori yang digunakan sebagai tempat berbagi.
7. ***Folder Name*** akan terisi otomatis setelah memilih direktori.
8. Ceklis ***Auto Mount*** agar pada guest selalu ada direktori tempat berbaginya.
9. Hiraukan ***Read-only*** karena hanya digunakan agar file di dalam direktori tidak bisa dirubah atau ditambah di dalam VirtualBox.
10. Hiraukan ***Mount point*** juga.
11. Jika Sudah Pilih Ok.

## Pengaturan Sistem Operasi Windows Pada VirtualBox
<figure class="third">
  <a href="/assets/images/2020/mengaktifkan-fitur-pada-virtualbox/2-pengaturan-windows.png"><img src="/assets/images/2020/mengaktifkan-fitur-pada-virtualbox/2-pengaturan-windows.png" alt="Gambar bagian Device"></a>
  <a href="/assets/images/2020/mengaktifkan-fitur-pada-virtualbox/3-pengaturan-windows.png"><img src="/assets/images/2020/mengaktifkan-fitur-pada-virtualbox/3-pengaturan-windows.png" alt="Gambar bagian Installasi Direktori VBox"></a>
  <a href="/assets/images/2020/mengaktifkan-fitur-pada-virtualbox/4-pengaturan-windows.png"><img src="/assets/images/2020/mengaktifkan-fitur-pada-virtualbox/4-pengaturan-windows.png" alt="Gambar Muncu direktori Shared Files"></a>
  <figcaption>Gambar B untuk langkah 2, 3, 4, 5, dan 7.</figcaption>
</figure>

1. Jalankan Sistem Operasi Windows yang sudah diatur pada Pengaturan VirtualBox di bagian atas.
2. Pilih menu ***Device*** -> Pilih ***Insert Guest Additions CD image*** seperti pada gambar di atas.
3. Aktifkan Copy paste dengan pilih menu ***Device*** -> Pilih ***Shared Clipboard*** -> Pilih ***Biderectional***.
4. Aktifkan Drag and drop dengan pilih menu ***Device*** -> Pilih ***Drag and Drop*** -> Pilih ***Biderectional***.
5. Buka ***File Explorer -> Pilih ***Computer*** -> Klik dua kali pada ***VirtualBox Guest Additions***.
6. Melakukan instalasi dengan mengklik dua kali pada file ***VBoxWindowsAdditions***.
7. Terakhir *restart* VM (reboot), maka *Copy Paste*, *Drag and Drop*, dan direktori *share* yang sudah diatur tadi akan muncul pada *File Explorer* seperti gambar di atas.

<div class="notice">
  <h4>Error: The Specified path does not exist</h4>
        <ol>
            <li>Pilih file yang ada di direktori sharing file.</li>
            <li>Copy dan paste ke direktori yang ada di Windows, seperti direktori Downloads.</li>
        </ol>
</div>

## Pengaturan Sistem Operasi CentOS Pada VirtualBox
1. Jalankan Sistem Operasi CentOS yang sudah diatur pada Pengaturan VirtualBox di bagian atas.
2. Buka terminal, install Repository ***EPEL*** atau ***Extra Packages for Enterprise Linux*** yang menyediakan perangkat lunak tambahan pada keluarga RedHat dengan cara:
```bash
sudo dnf install epel-release
```
Untuk memeriksa installasi:
```
rpm -q epel-release
```
3. Install Kernel Headers dan Build Tools:
```bash
sudo dnf install gcc make perl kernel-devel kernel-headers bzip2 dkms
```
4. Memeriksa versi `kernel-devel` dan `kernel-linux` yang kita gunakan dengan:
```bash
rpm -q kernel-devel
```
```bash
uname -r
```
5. Jika versi kernel berbeda maka kita harus update `kernel-linux` agar tidak terjadi konflik dengan cara:
```
sudo dnf update kernel-*
```
6. Restart Virtualbox
7. Saat Booting pilih versi `kernel` paling pertama.
8. Memeriksa kembali versi `kernel-devel` dan `kernel-linux` yang kita gunakan apakah sudah sama atau tidak dengan:
```bash
rpm -q kernel-devel
```
```bash
uname -r
```
9. Pilih menu ***Device*** -> Pilih ***Insert Guest Additions CD image*** seperti pengaturan pada Windows pada langkah kedua.

10. Akan muncul *pop up* pemberitahuan untuk menjalankan via *GUI*. Tetapi kita dapat menggunakan terminal dengan cara masuk ke direktori mount VirtualBox:
```bash
cd /media/userName/VBox_Direktori/
```
***Catatan***:
  - `userName`: Ganti dengan nama user kita.
  - `VBox_direktori`: Ganti dengan nama VBox kita tergantung versi.
11. Jalankan Virtualbox dengan cara:
```bash
sudo ./VBoxLinuxAdditions.run 
```
12. Jalankan perintah berikut agar User dapat mengakses share folder (ganti userName dengan user yang kita buat):
```bash
sudo usermod -aG vboxsf userName
```
13. Aktifkan Copy paste dengan pilih menu ***Device*** -> Pilih ***Shared Clipboard*** -> Pilih ***Biderectional*** sama seperti pengaturan pada Windows pada langkah ketiga.
14. Aktifkan Drag and drop dengan pilih menu ***Device*** -> Pilih ***Drag and Drop*** -> Pilih ***Biderectional*** sama seperti pengaturan pada Windows pada langkah keempat.
15. Restart VM (Reboot).

## Pengaturan Sistem Operasi Ubuntu Pada VirtualBox
1. Jalankan Sistem Operasi Ubuntu yang sudah diatur pada Pengaturan VirtualBox di bagian atas.
2. Buka terminal, Lakukan update sistem:
```bash
sudo apt update
sudo apt upgrade
```
3. Restart VM (Reboot).
4. Install paket aplikasi yang dibutuhkan:
```bash
sudo apt install build-essential dkms linux-headers-$(uname -r)
```
5. Pilih menu ***Device*** -> Pilih ***Insert Guest Additions CD image*** seperti pengaturan pada Windows pada langkah kedua.

6. Akan muncul *pop up* pemberitahuan untuk menjalankan via *GUI*. Tetapi kita dapat menggunakan terminal dengan cara masuk ke direktori mount VirtualBox:
```bash
cd /media/userName/VBox_Direktori/
```
***Catatan***:
  - `userName`: Ganti dengan nama user kita.
  - `VBox_direktori`: Ganti dengan nama VBox kita tergantung versi.
7. Jalankan Virtualbox dengan cara:
```bash
sudo ./VBoxLinuxAdditions.run 
```
8. Jalankan perintah berikut agar User dapat mengakses share folder (ganti userName dengan user yang kita buat):
```bash
sudo usermod -aG vboxsf userName
```
9. Aktifkan Copy paste dengan pilih menu ***Device*** -> Pilih ***Shared Clipboard*** -> Pilih ***Biderectional*** sama seperti pengaturan pada Windows pada langkah ketiga.
10. Aktifkan Drag and drop dengan pilih menu ***Device*** -> Pilih ***Drag and Drop*** -> Pilih ***Biderectional*** sama seperti pengaturan pada Windows pada langkah keempat.
11. Restart VM (Reboot).

## Daftar Pustaka
- Mingkul, Ji. 2019. [Virtualbox: Share A Folder in Ubuntu Host to Windows Guest](http://ubuntuhandbook.org/index.php/2019/06/virtualbox-share-a-folder-in-ubuntu-host-to-windows-guest/). (diakses tanggal 10 Oktober 2020).

- Kiarie, James. 2020. [How to Install VirtualBox Guest Additions on CentOS 8](https://www.tecmint.com/install-virtualbox-guest-additions-on-centos-8/). (diakses tanggal 10 Oktober 2020).

- Kili, Aaron. 2020. [How to Install VirtualBox Guest Additions in Ubuntu](https://www.tecmint.com/install-virtualbox-guest-additions-in-ubuntu/). (diakses tanggal 10 Oktober 2020).

- Average Linux User. 2019. [How to enable a Virtualbox shared folder for Linux guest systems](https://averagelinuxuser.com/virtualbox-shared-folder/). (diakses tanggal 10 Oktober 2020).