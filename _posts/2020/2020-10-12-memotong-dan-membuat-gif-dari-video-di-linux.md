---
title: "Memotong dan Membuat Gif di Linux"
categories:
  - Konfigurasi
tags:
  - Aplikasi
date: 2020-10-12 18:22:25 +0700
classes: wide
---
## Pengertian
FFmpeg adalah perangkat lunak free dan open source tersusun dari banyak libraries program untuk menangani video, audio, file multimedia dan stream.

## Installasi
```
sudo apt-get install ffmpeg
```

## Penggunaan Cara 1
Cara ini video dipotong dan dikonversi menjadi gif.

### Pemotongan video menjadi video pendek
```
ffmpeg -i original.mp4 -ss 00:03:20 -c copy -t 00:00:30 output.mp4
```
***Catatan***:
- `-i`: Input file.
- `original.mp4`: Nama video yang ingin dipotong.
- `-ss`: Membuat video baru dimulai dari menit 30 dan detik 20.
- `-t`: Durasi video baru yaitu 30 detik.
- `output.mp4`: Nama video baru.

### Pembuatan video pendek to gif
```
ffmpeg -i original.mp4 -r 15 -vf scale=512:-1 -loop 0 Switch.gif
```
***Catatan***:
- `-r 15`: Jumlah FPS yang digunakan, semakin tinggi nilainya maka akan semakin jelas akan tetapi ukuran file gif menjadi besar. Nilai rekomendasinya 5, 10, dan 15.
- `vf scale=512:-1`: Membuat gif dengan tinggi 512 px dan lebarnya mengikuti rasionya. Nilai rekomendasinya 512, dan 320.
- `-loop 0`: Membuat Infinite Loop, atau berulang.

## Penggunaan Cara 2 (Alternatif)
Cara ini video tidak dipotong, dikonversi menjadi kumpulan png/jpg dalam satu direktori dan dikonversi menjadi gif serta harus install imagemagick terlebih dahulu:
```
sudo apt-get install imagemagick
```

### Pembuatan video menjadi png/jpg
```
mkdif frames
ffmpeg -i video.mp4  -r 5 'frames/frame-%03d.png'
```
***Catatan***:
- `%03d`: Membuat nomor pada penamaan secara berurutan.

### Pembuatan png/jpg menjadi gif
```
cd frames
convert -resize 20% -delay 20 -loop 0 *.png myimage.gif
```
***Catatan***:
- `-resize 20%`: Untuk mengatur ulang ukuran gif dapat diganti juga dengan 768x576. 

## Daftar Pustaka
- Santilli,Ciro. 2016. [How to create an animated GIF from MP4 video via command line?](https://askubuntu.com/questions/648603/how-to-create-an-animated-gif-from-mp4-video-via-command-line). (diakses tanggal 12 Oktober 2020).

- Maythux. 2015. [How to create an animated GIF from MP4 video via command line?](https://askubuntu.com/questions/648603/how-to-create-an-animated-gif-from-mp4-video-via-command-line). (diakses tanggal 12 Oktober 2020).

- Peiris, Eranda. 2018. [Application for trimming a video mp4 of ubuntu 16.04 LTS](https://askubuntu.com/questions/1025271/application-for-trimming-a-video-mp4-of-ubuntu-16-04-lts). (diakses tanggal 12 Oktober 2020).