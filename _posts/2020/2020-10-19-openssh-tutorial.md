---
title: "OpenSSH Tutorial"
categories:
  - Tutorial
tags:
  - Jaringan
date: 2020-10-19 15:45:25 +0700
toc: true
toc_sticky: true
---
OpenSSH adalah software yang biasanya digunakan untuk mengelola Server Linux jarak jauh dari laptop kita. Tutorial ini menggunakan:
- Linux sebagai Client
- Linux sebagai Server pada VirtualBox
- Perangkat lunak Openssh-client untuk client
- Perangkat lunak Openssh-server untuk server
- Perangkat lunak Netstat yang digunakan untuk monitoring network connections yang masuk dan keluar serta dapat digunakan untuk melihat routing tables, interface statistics dsb.
- Secure Copy Protocol (SCP) digunakan untuk transfer files menggunakan SSH.
- SSH File System (SSHFS) digunakan untuk *mount* direktori server ke lokal. SSH tetap berjalan pada background.

## Installasi OpenSSH
- Install pada Linux Ubuntu untuk client:
```bash
sudo apt install openssh-client
```
- Install OpenSSH untuk server pada VirtualBox:
```bash
sudo apt install openssh-server
```
- Untuk mengecek OpenSSH pada linux yang menggunakan systemd:
```bash
# Gunakan sshd untuk keluarga redhat
sudo systemctl start ssh # Menjalankan OpenSSH
sudo systemctl stop ssh # Memberhentikan OpenSSH
sudo systemctl restart ssh # Menjalankan ulang OpenSSH
sudo systemctl status ssh # Memeriksa OpenSSH
```
- Untuk mengecek OpenSSH pada linux yang menggunakan init:
```bash
sudo /etc/init.d/ssh start
sudo /etc/init.d/ssh restart
sudo /etc/init.d/ssh stop
```

## Memeriksa OpenSSH
- Install Netstat dengan:
```bash
sudo apt install net-tools
```

- Jalankan kode berikut untuk menampilkan port apa saja yang sedang terkoneksi pada server kita:
```
sudo netstat -tulpn
```
Contoh hasil pada Openssh akan listening pada port 22:
```bash
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp     0      0    0.0.0.0:22              0.0.0.0:*               LISTEN      901/sshd
tcp6    0      0    :::22                   :::*                    LISTEN      901/sshd
```

- Melihat openssh yang berjalan pada background service:
```bash
sudo systemctl status sshd
```
Contoh hasil tampilan:
```bash
● sshd.service - OpenSSH server daemon
     Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2020-10-17 12:19:22 EDT; 12min ago
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 901 (cups-browsed)
      Tasks: 1 (limit: 5029)
     Memory: 388.0K
     CGroup: /system.slice/sshd.service
             └─901 /usr/sbin/sshd -D

Okt 17 12:19:22 centos-server1 systemd[1]: Starting OpenSSH server daemon..
Okt 17 12:19:22 centos-server1 sshd[901]: Server Listening on 0.0.0.0 port 22
Okt 17 12:19:22 centos-server1 sshd[901]: Server Listening on :: port 22
Okt 17 12:19:22 centos-server1 systemd[1]: Started OpenSSH server daemon..
```

## Menjalankan Koneksi Menggunakan OpenSSH
- Kita harus mencaritahu IP address mesin server yang ingin kita koneksikan dengan cara:
```bash
ip a
```
Contoh hasil tampilan:
```bash
...
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:bb:05:6f brd ff:ff:ff:ff:ff:ff
    inet 192.168.100.43/24 brd 192.168.100.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86381sec preferred_lft 86381sec
    inet6 fe80::cbbb:ec2:218b:2b99/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
...
```

- Koneksikan dengan mengetik perintah berikut pada client :
```bash
    ssh user@ipaddress

```
Contoh hasil tampilan:
```bash
ssh person1@192.168.100.43
person1@192.168.100.43's password: 
Activate the web console with: systemctl enable --now cockpit.socket

Last login: Sun Oct 18 01:46:31 2020
[person1@centos-server1 ~]$
```
***Catatan***:
    - `user` adalah username yang sudah dibuat pada server (biasanya pada saat installasi linux kita sudah membuat satu user).
    - Kita dapat menuliskan `ssh ipaddress` saja tanpa `user` jika username pada client dan server sama atau pada server sudah dibuatkan user dengan nama yang sama dengan username pada client.
    - `ipaddress` adalah IP address server di atas.
    - Sampai sini kita sudah dapat masuk ke server. Kita dapat mengeceknya dengan membuat file dengan `touch testfile` dan lihat pada server apakah file tersebuat ada atau tidak.
    - Kita juga dapat menggunakan `hostname` untuk masuk dengan SSH jika sudah disetting.

- Jika kita ingin melakukan koneksi dan melihat informasi **debug** jika pada suatu saat kita tidak bisa koneksi dengan SSH ke server dengan cara:
```bash
ssh -v ipaddress
```
Contoh beberapa baris output:
```bash
...
debug1: Authentications that can continue: publickey,gssapi-keyex,gssapi-with-mic,password
debug1: Trying private key: /home/helmiz/.ssh/id_dsa
debug1: Trying private key: /home/helmiz/.ssh/id_ecdsa
debug1: Trying private key: /home/helmiz/.ssh/id_ecdsa_sk
debug1: Trying private key: /home/helmiz/.ssh/id_ed25519
debug1: Trying private key: /home/helmiz/.ssh/id_ed25519_sk
debug1: Trying private key: /home/helmiz/.ssh/id_xmss
debug1: Next authentication method: password
...
```
***Catatan***:
    - Dapat dilihat bahwa server diakses dengan mengecek `publickey` terlebih dahulu sampai ke `password`

- Kita dapat mengkoneksi dengan port yang berbeda jika pada server portnya diganti (default 22) dengan cara:
```bash
ssh ipaddress -p portNumber
```

## Konfigurasi Sederhana
- Tempat menyimpan konfigurasi client berada pada direktori `.ssh`. Direktori tsb dibuat saat client mengkoneksi server.
```bash
ls -la
```
Contoh hasil:
```bash
drwx------  2 helmiz helmiz 4096 Okt 17 12:53  .ssh
```
***Catatan***:
    - Di dalam direktori tsb akan ada file `known_host` yang digunakan untuk menyimpan fingerprint mesin yang kita koneksikan. Sehingga jika kita melakukan koneksi ke mesin server yang sama kita tidak ditanya *Confirm the Fingerprint* lagi.

- Tempat konfigurasi server berada pada direktori `/etc/ssh/sshd_config`:
```bash
sudo nano /etc/ssh/sshd_config
```
***Catatan***:
    - `Port`: Mengganti port number dapat meningkatkan keamanan dari BOTS otomatis dari Internet.
    - `PermitRootLogin`: Root login akses jadikan `no` agar orang lain tidak dapat masuk sebagai Root. Pengecualian jika kita mengakses ke VPS atau Cloud Server yang memberikan Root Login.
    - `PasswordAuthentication`: Penggunaan password untuk masuk ke server yang akan kita ganti jadi `no` nanti. Jadi akses hanya boleh menggunakan *public key authentication*.
    - `AllowUsers`: Users siapa saja yang hanya boleh mengakses server. Contoh `AllowUsers azam21 rahmah93 nindi11` berarti hanya tiga orang itu yang boleh mengakses server.
    - `AllowGroups`: Cara mudah daripada `AllowUsers` karena kita menuliskan berdasarkan group user. Contoh `AllowGroups sshusers admin`.

-   Jangan lupa untuk restart SSH setelah melakukan konfigurasi:
```bash
sudo systemctl restart sshd
```

## Mendeteksi Permasalahan pada SSH
- Client tidak dapat mengkoneksi server maka kita dapat menggunakan perintah:
```bash
ssh -v user@ipaddress
```

- Cara di atas kurang memberikan informasi rinci. Alternatif lain kita dapat mengecek *logs* pada server dengan cara:
```bash
# Keluarga Ubuntu
cat /var/log/auth.log
# atau secara follow realtime
tail -f /var/log/auth.log

# Keluarga Redhat
cat /var/log/secure
# atau secara follow realtime
tail -f /var/log/secure
```

## Public Key Authentication
- Kita dapat membuat Public key yang digunakan sebagai metode authentication supaya keamanan lebih terjamin. Kita dapat *generete key* dengan:
```bash
ssh-keygen
```
***Catatan***:
    - `Passphrase`: Encrypt key pada local machine.
    - Terdapat dua file pada direktori `.ssh` yaitu `id_rsa` adalah private key yang harus disembunyikan dan `id_rsa.pub` adalah public key untuk di *broadcast* ke mesin lain.
    
- Kita dapat memberikan public key kita ke server untuk membuat *relationship* antara server dan client dengan:
```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub user@ipaddress
```
***Catatan***:
    - Dengan membuat menghubungkan *public key* kita tidak perlu lagi menuliskan password secara berulang-ulang.
    
- Jika kita ingin membuat key baru ke server, maka kita harus menghapus key lama pada file `authorized_keys` di server. File tersebut berisi semua *public key* yang tersimpan pada server:
```bash
nano .ssh/authorized_keys
```

- Kita dapat tidak mengizinkan user untuk masuk ke server menggunakan authentication dengan password sehingga meningkatkan keamanan:
```bash
# File
sudo nano /etc/ssh/sshd_config
# Baris
PasswordAuthentication no
```

## Secure Copy Protocol (SCP)
- Installasi:
```bash
scp nameFile ipaddress:/home/dir -P 22
```
Contoh:
```bash
$ scp wallpaper.jpg person1@192.168.100.44:/home/person1/
  person1@192.168.100.44's password: 
  wallpaper.jpg                                           100% 2251KB  22.0MB/s   00:00    
```

- Transfer direktori
```bash
scp -r dirName ipaddress:
```
Contoh:
```bash
$ scp -r mydir person1@192.168.100.44:
  person1@192.168.100.44's password: 
  wallpaper.jpg                                           100% 2251KB  19.7MB/s   00:00    
```
***Catatan***:
- Jika tanpa path maka default pathnya adalah user home direktori

- Jika kita ingin mengambil file yang ada di server (pull), maka:
```bash
scp -r ipaddress:dir .
```
Contoh:
```bash
$ scp -r person1@192.168.100.44:mydir .
  person1@192.168.100.44's password: 
  wallpaper.jpg                                           100% 2251KB  34.6MB/s   00:00    
```
***Catatan***:
- `.` adalah copy ke path dimana kita berada.

## SSH File System (SSHFS)
- Installasi:
```bash
sudo apt install sshfs
```

- Selanjutnya buat direktori di lokal yang akan ditempenkan pada direktori server dan lakukan *mount* dengan cara:
```bash
sshfs ipaddress:/server-direktori client-direktori/
```
Contoh:
```bash
sshfs person1@192.168.100.44:/home/person1/mydir-server mydir-client/
```

- Jika langkah di atas berhasil maka direktori server (`mydir-server`) sudah ditempel ke direktori lokal dengan nama `mydir-client`. Kita dapat mengecek isi pada direktori server setiap dua detik dengan perintah:
```bash
watch ls dirName/
```

- Buat file `test-file1`, `test-file2`dan `test-file3` pada direktori client sehingga output perintah watch sebagai berikut:
```bash
Every 2.0s: ls mydir-server/                                                                                  centos-server1: Sun Oct 18 21:17:50 2020
test-file1
test-file2
test-file3
```

- Kita dapat menonaktifkan *mount* dengan cara :You can disconnect with this command:
```bash
fusermount -u /home/dirName
```

## Meningkatkan Keamanan OpenSSH pada Cloud Instance
Bagian ini menggunakan Ubuntu Server.

### Disable Root Login
Pada saat berlangganan Cloud Instance maka kita akan mendapatkan Root Login. Kita dapat mematikannya dengan cara:
1. Masuk ke dalam Cloud Instance dan buat dua tab untuk mengakses untuk berjaga-jaga jika terjadi kesalahan kita punya *session* di tab satunya.
```bash
ssh root@ipAddress
```

2. Membuat User baru di dalam Cloud Instance isikan `username` dan `password`.
```bash
adduser userName

# Menambahkan sudo pada userName hanya pada Ubuntu 
usermod -aG sudo userName
```

3. Disable Root Login:
```bash
sudo nano /etc/ssh/sshd_config

# Cari dan ganti
PermitRootLogin no

# Restart SSH
sudo systemctl restart ssh
```

### Disable Password Authentication
1. Membuat Public key dan Private key pada local:
```bash
ssh-keygen

# Masukan Passphrase
```

2. Copy public key ke server:
```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub userName@ipAddress
```

3. Mematikan Password Authentication
```bash
sudo nano /etc/ssh/sshd_config

# Ganti
PasswordAuthentication no
```

4. Restart SSH
```bash
sudo systemctl restart ssh
```

### Change SSH Port
1. Masuk ke server dan ganti nomor port berapapun dengan perintah:
```bash
sudo nano /etc/ssh/sshd_config

# Ganti default Port bagian:
Port 22
```

2. Masuk ke server dengan:
```bash
ssh -p portNumber userName@ipAddress

# Jika menggunakan SCP
scp -P portNumber
```

3. Restart SSH
```bash
sudo systemctl restart ssh
```

### Restrict User
1. Masuk ke server dan tambahkan kode berikut:
```bash
sudo nano /etc/ssh/sshd_config

# Tambahkan
AllowUsers userName
```

2. Restart SSH
```bash
sudo systemctl restart ssh
```

### Restrict IP
Jika IP kita tidak berubah-ubah (static) tergantung provider maka sangat direkomendasikan untuk membatasi IP yang masuk ke server dengan SSH.

### Deteksi Permasalahan
Untuk melihat permasalahan yang terjadi pada SSH, dapat mengecek log pada server dengan:
```bash
sudo cat /var/log/auth.log
```

## Daftar Pustaka
- LaCroix, Jeremy. 2019. [Getting started with OpenSSH](https://www.youtube.com/playlist?list=PLT98CRl2KxKHtOhMYulS43hayRsGXLzmx). (diakses tanggal 19 Oktober 2020).