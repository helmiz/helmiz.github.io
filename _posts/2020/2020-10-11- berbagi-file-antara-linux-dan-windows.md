---
title: "Berbagi File Antara Linux Host dan Windows Guest Pada VirtualBox"
categories:
  - Sistem Operasi
tags:
  - VirtualBox
date: 2020-10-11 18:23:25 +0700
classes: wide
---
## Konfigurasi VirtualBox
<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/2020/berbagi-file-antara-linux-dan-windows/1-Virtualbox-Settings.png"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/2020/berbagi-file-antara-linux-dan-windows/1-Virtualbox-Settings.png" alt="Gambar bagian Settings pada Windows"></a>
</figure>



1. Pilih Windows yang sudah dijadikan VM pada VirtualBox.
2. Tekan menu ***Settings***.
3. Pilih tab ***Shared Folders***.
4. Klik icon ***Adds new shared folder*** pada bagian kanan.
5. Akan muncul Pop-up *Add Share*.
6. Pada ***Folder Path***, pilih direktori yang digunakan sebagai tempat berbagi.
7. ***Folder Name*** akan terisi otomatis setelah memilih direktori.
8. Ceklis ***Auto Mount*** agar pada guest selalu ada direktori tempat berbaginya.
9. Hiraukan ***Read-only*** karena hanya digunakan agar file di dalam direktori tidak bisa dirubah atau ditambah.
10. Hiraukan ***Mount point*** juga.
11. Jika Sudah Pilih Ok.

## Pengaturan Sistem Operasi Guest (Windows)
<figure class="third">
  <a href="/assets/images/2020/berbagi-file-antara-linux-dan-windows/2-Virtualbox-Device-Menu.png"><img src="/assets/images/2020/berbagi-file-antara-linux-dan-windows/2-Virtualbox-Device-Menu.png"></a>
  <a href="/assets/images/2020/berbagi-file-antara-linux-dan-windows/3-file-explorer.png"><img src="/assets/images/2020/berbagi-file-antara-linux-dan-windows/3-file-explorer.png"></a>
  <a href="/assets/images/2020/berbagi-file-antara-linux-dan-windows/4-share-directory.png"><img src="/assets/images/2020/berbagi-file-antara-linux-dan-windows/4-share-directory.png"></a>
</figure>

1. Jalankan Sistem Operasi yang sudah dikonfigurasi dalam hal ini Windows 10.
2. Pilih menu ***Device*** -> Pilih ***Insert Guest Additions CD image*** seperti pada gambar di atas.
3. Buka ***File Explorer -> Pilih ***This PC*** -> Klik dua kali pada ***CD Drive (D:) VirtualBox Guest Additions***.
4. Melakukan instalasi dengan mengklik dua kali pada ***VBoxWindowsAdditions***.
5. Setelah restart VM (reboot), maka direktori *share* yang sudah dikonfigurasi tadi akan muncul pada *File Explorer* seperti gambar di atas.

<div class="notice">
  <h4>Error: The Specified path does not exist</h4>
        <ol>
            <li>Pilih file yang ada di direktori sharing file.</li>
            <li>Copy dan paste ke direktori yang ada di Windows, seperti direktori Downloads.</li>
        </ol>
</div>

## Daftar Pustaka
- Mingkul, Ji. 2019. D, Miguel Quintero. 2020. [Virtualbox: Share A Folder in Ubuntu Host to Windows Guest](http://ubuntuhandbook.org/index.php/2019/06/virtualbox-share-a-folder-in-ubuntu-host-to-windows-guest/) (diakses tanggal 10 Oktober 2020).