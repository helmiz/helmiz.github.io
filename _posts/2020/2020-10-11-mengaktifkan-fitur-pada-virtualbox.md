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
<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2020/mengaktifkan-fitur-pada-virtualbox/1-pengaturan-vbox.png"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/2020/mengaktifkan-fitur-pada-virtualbox/1-pengaturan-vbox.png" alt="Gambar bagian Settings pada VBox"></a>
    <figcaption>Gambar untuk langkah 3, 4, dan 5.</figcaption>
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
  <figcaption>Gambar untuk langkah 2, 3, 4, 5, dan 7.</figcaption>
</figure>

1. Jalankan Sistem Operasi pada VirtualBox.
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

## Daftar Pustaka
- Mingkul, Ji. 2019. [Virtualbox: Share A Folder in Ubuntu Host to Windows Guest](http://ubuntuhandbook.org/index.php/2019/06/virtualbox-share-a-folder-in-ubuntu-host-to-windows-guest/) (diakses tanggal 10 Oktober 2020).