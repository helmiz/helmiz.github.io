---
title: "Download Video Youtube dengan Youtube-dl"
categories:
  - Konfigurasi
tags:
  - youtube-dl
date: 2020-10-12 12:20:25 +0700
classes: wide
---
## Pengertian
Youtube-dl adalah program *command-line* untuk mengunduh video dari Youtube dan beberapa [website lain](http://ytdl-org.github.io/youtube-dl/supportedsites.html). Program ini membutuhkan Python Interpreter dan dapat berjalan di sistem operasi Linux, Windows dan Mac OS X.

## Installasi
- Pastikan kita sudah menginstall (Python)[https://www.python.org/downloads/] kecuali pada Windows.

- Windows membutuhkan [Microsoft Visual C++ 2010 Redistributable Package (x86)](https://www.microsoft.com/en-US/download/details.aspx?id=5555).

- Installasi untuk pengguna UNIX (Linux, MacOS, dsb):
```
sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl
sudo chmod a+rx /usr/local/bin/youtube-dl
```
Jika kita tidak punya Curl, alternatifnya menggunakan Wget:
```
sudo wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl
sudo chmod a+rx /usr/local/bin/youtube-dl
```

- Untuk pengguna Windows dapat mengunduh di [youtube.dl](https://yt-dl.org/latest/youtube-dl.exe) dan disimpan di path direktori manapun kecuali di `C:\Windows\System32`.

- Installasi menggunakan Pip:
```
sudo -H pip install --upgrade youtube-dl
```

- Installasi menggunakan Homebrew untuk MacOS:
```
brew install youtube-dl
```

## Penggunaan
Disini saya hanya mendemokan beberapa perintah yang sering saya gunakan, jika ingin tahu lebih dalam maka dapat mengunungi website [dokumentasi youtube-dl](https://github.com/ytdl-org/youtube-dl/blob/master/README.md#description) atau dengan menuliskan perintah `youtube-dl -h` pada terminal atau konsole. Berikut adalah penulisan perintahnya:
```
Usage: youtube-dl [OPTIONS] [URL...]
```
<div class="notice">
  <h4>Catatan:</h4>
      <ol>
          <li>[OPTIONS] adalah jenis perintah yang dapat digunakan yang ada pada dokumentasi.</li>
          <li>[URL...] adalah link video youtube.</li>
      </ol>
</div>

### Download Video
1. Pastikan kita sudah memilih video youtube dan copy link video tersebut.

2. Check daftar video format yang akn kita download:
```
youtube-dl -F [URL....]
```
Contoh output:
```
[info] Available formats for 2lAe1cqCOXo:
format code  extension  resolution note
249          webm       audio only tiny   60k , opus @ 50k (48000Hz), 2.02MiB
250          webm       audio only tiny   78k , opus @ 70k (48000Hz), 2.66MiB
140          m4a        audio only tiny  130k , m4a_dash container, mp4a.40.2@128k (44100Hz), 5.20MiB
251          webm       audio only tiny  147k , opus @160k (48000Hz), 5.27MiB
394          mp4        256x144    144p   78k , av01.0.00M.08, 24fps, video only, 2.74MiB
278          webm       256x144    144p   98k , webm container, vp9, 24fps, video only, 3.51MiB
160          mp4        256x144    144p  118k , avc1.4d400c, 24fps, video only, 4.43MiB
395          mp4        426x240    240p  169k , av01.0.00M.08, 24fps, video only, 5.73MiB
242          webm       426x240    240p  237k , vp9, 24fps, video only, 7.66MiB
133          mp4        426x240    240p  253k , avc1.4d4015, 24fps, video only, 9.77MiB
396          mp4        640x360    360p  371k , av01.0.01M.08, 24fps, video only, 11.87MiB
243          webm       640x360    360p  416k , vp9, 24fps, video only, 13.52MiB
134          mp4        640x360    360p  635k , avc1.4d401e, 24fps, video only, 22.12MiB
397          mp4        854x480    480p  663k , av01.0.04M.08, 24fps, video only, 21.10MiB
244          webm       854x480    480p  771k , vp9, 24fps, video only, 22.26MiB
135          mp4        854x480    480p 1164k , avc1.4d401e, 24fps, video only, 40.81MiB
398          mp4        1280x720   720p 1237k , av01.0.05M.08, 24fps, video only, 38.26MiB
247          webm       1280x720   720p 1501k , vp9, 24fps, video only, 39.15MiB
399          mp4        1920x1080  1080p 2287k , av01.0.08M.08, 24fps, video only, 65.88MiB
136          mp4        1280x720   720p 2323k , avc1.4d401f, 24fps, video only, 78.74MiB
248          webm       1920x1080  1080p 2696k , vp9, 24fps, video only, 85.91MiB
137          mp4        1920x1080  1080p 4417k , avc1.640028, 24fps, video only, 145.25MiB
18           mp4        640x360    360p  672k , avc1.42001E, 24fps, mp4a.40.2@ 96k (44100Hz), 26.97MiB
22           mp4        1280x720   720p 2090k , avc1.64001F, 24fps, mp4a.40.2@192k (44100Hz) (best)
```
Catatan: 
- Perhatikan keterangan video. Ada yang hanya *Video Only* dan *Audio Only*.
- Biasanya format video paling bagus di bagian paling bawah.

3. Download video dengan cara:
```
youtube-dl -f [FORMAT CODE] [URL....]
```

4. Download Video dengan Subtitle (jika ada):
Untuk mengecek subtitle dapat dilihat pada video youtube itu sendiri atau dengan cara:
```
youtube-dl --list-subs [URL....]
```
Perintah untuk mengunduh:
```
youtube-dl -f [FORMAT CODE] --write-sub/--write-auto-sub/--all-subs [URL....]
```
<div class="notice">
  <h4>Catatan:</h4>
      <ol>
          <li>--write-sub: Mengunduh subtitle default biasanya English.</li>
          <li>--write-auto-sub: Mengunduh subtitle auto generated English.</li>
          <li>--all-subs: Mengunduh semua subtitle yang tersedia.</li>
      </ol>
</div>

5. Download semua video yang ada di dalam *Playlist* dengan nomor indeksnya:
```
youtube-dl -o "%(playlist_index)s-%(title)s.%(ext)s" [URL Playlist]
```

## Daftar Pustaka
- youtube-dl. [Youtube-dl Github](https://github.com/ytdl-org/youtube-dl) (diakses tanggal 12 Oktober 2020).

- Mohamadi, Iman. 2015. [How to download a youtube playlist with numbered prefix via youtube-dl?](https://askubuntu.com/questions/694848/how-to-download-a-youtube-playlist-with-numbered-prefix-via-youtube-dl) (diakses tanggal 12 Oktober 2020).
