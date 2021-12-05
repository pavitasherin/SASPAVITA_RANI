# Laporan Praktikum 1

## Kelompok 3


### 1. Rename ubuntu_php5.6 menjadi ubuntu_landing, serta rubah IP mengikuti skema yang baru

1.1 Menampikan Container sebelum dirubah
```
sudo lxc-ls -f
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/1.1.jpeg">
</p>

1.2 Kode ini untuk menyalin daripada mengubah nama container dari ubuntu_php5.6 menjadi ubuntu_landing.
```
sudo lxc-copy -R -n ubuntu_php5.6 -N ubuntu_landing
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/1.2.PNG">
</p>

1.3 Menampikan Container setelah dirubah	
```
sudo lxc-ls -f
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/1.3.jpeg">
</p>

1.4 Start Ubuntu landing
```
sudo lxc-start ubuntu_landing
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/1.4.PNG">
</p>

1.5 Masuk ke root ubuntu_landing container
```
sudo lxc-attach ubuntu_landing
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/1.5.PNG">
</p>

1.6 Setting IP yang mengikuti skema baru
```
nano /etc/network/interfaces
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/1.6.PNG">
</p>

1.7 Restart container
```
shutdown now
sudo lxc-start ubuntu_landing
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/1.7.PNG">
</p>

1.8 Setelah Restart lalu check IP apakh sudah berubah
```
lxc-attach ubuntu_landing
ifconfig
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/1.8.PNG">
</p>
Dan IP sudah berubah menjadi 10.0.3.103

Inilah step bagaimana merename ubuntu_php5.6 menjadi ubuntu_landing, serta merubah IP mengikuti skema yang baru.



### 2. Install lxc debian 9 dengan nama debian_php5.6

2.1 Install lxc debian 9
```
sudo lxc-create -n debian_php5.6 -t download -- --dist debian --release stretch --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/2.1.PNG">
</p>

2.2 Cek container apakah sudah berhasil terinstall
```
sudo lxc-ls -f 
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/2.2.PNG">
</p>

2.3 Start debian_php 5.6
```
sudo lxc-start -n debian_php5.6 -d
sudo lxc-attach -n debian_php5.6
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/2.3.PNG">
</p>



### 3. Setup nginx pada debian_php5.6 untuk domain http://lxc_php5.dev , buat halaman index.html yang menerangkan informasi nama lxc

3.1 Pertama cek apakah ubuntu_php5.6 berjalan, setelah itu install nginx
```
sudo apt install nginx nginx-extras
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/3.1.PNG">
</p>

3.2 Setelah itu install net tools
```
apt install nano net-tools curl
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/3.2.PNG">
</p>

3.3 Lalu kita harus setting IP 
```
nano /etc/network/interfaces
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/3.3.PNG">
</p>

3.4 Lalu restart kontainer
Pertama reboot, setelah itu buka ifconfig untuk mengecek apakah IP telah berubah atau tidak.
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/3.4.PNG">
</p>

3.5 Setting nginx
Setelah itu setting nginx ikuti kode dibawah ini:
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/3.5.PNG">
</p>

3.6 Mulai nano untuk konfigurasi
```
nano lxc_php5.6.dev
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/3.6.PNG">
</p>

3.7 Setting hosts
```
nano /etc/hosts
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/3.7.1.PNG">
</p>

```
nano index.html
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/3.7.PNG">
</p>

3.8 Setelah itu, kita membutuhkan untuk mengecek code di index.html
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/3.8.PNG">
</p>

3.9 Setelah itu curl -i
```
curl -i http://lxc_php5.dev 
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/3.9.PNG">
</p>
Yang dapat kita simpulkan yaitu kita membutuhkan memasukkan cd lxc_php5.6 sebelum kita memasukkan nano index.html



### 4. Setup nginx pada ubuntu_landing untuk domain http://lxc_landing.dev , buat halaman index.html yang menerangkan informasi nama lxc

Langkahnya seperti nomer 3

4.1 Ikuti Langkah-langkah dibawah ini :

<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/4.1.1.PNG">
</p>

<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/4.1.2.PNG">
</p>

<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/4.1.3.PNG">
</p>

<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/4.1.4.PNG">
</p>

<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/4.1.5.PNG">
</p>

<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/4.1.6.PNG">
</p>

4. 2 Lalu kita membutuhkan untuk mengecek command curl
```
curl -i http://lxc_landing.dev
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/4.2.PNG">
</p>



### 5. LXC ubuntu_landing harus auto start ketika vm dinyalakan, hal ini digunakan untuk menjaga agar website company profile tidak mengalami *downtime*

5.1 Masuk ke Super User atau Sudo su untuk masuk halaman config
```
sudo su
cd /var/lib/lxc/ubuntu_landing
nano config
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/5.1.PNG">
</p>

5.2 Lalu tambahkan 
```
lxc.start.auto = 1
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/5.2.PNG">
</p>

5.3 Keluar dari super user lalu reboot
```
reboot
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/5.3.PNG">
</p>

5.4 Lalu cek ubuntu_landing autostart telah berjalan atau tidak. jika autostart telah berjalan, autostart akan berubah dari '0' ke '1'
```
sudo lxc-ls -f
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/5.4.PNG">
</p>



### 6. Setup nginx pada vm.local untuk mengatur *proxy_pass* dimana :

6.1 Masuk pada nano
```
sudo nano /etc/hosts
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/6.1.PNG">
</p>

6.2 Setelah itu kita harus install nginx, lalu mulai directory bagian yang available,lalu mulai nano vm.local dan edit nano vm.local
```
sudo apt install nginx nginx-extras
cd /etc/nginx/sites-available
sudo touch vm.local
sudo nano vm.local
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/6.2.PNG">
</p>

6.3 Setelah itu masuk pada directory bagian enabled, jika nginx gagal untuk di dimulai, jalankan sudo nginx-t untuk menemukannya jika ada kesalahan dengan konfigurasi file. Jika nginx error di beberapa konfigurasi file, ulangi dan tetap jalankan configurasi file sebelumnya.
```
cd ../sites-enabled
sudo nginx -t
sudo nginx -s reload
```

6.4 Mengakses [http://vm.local](http://vm.local/) akan diarahkan ke http://lxc_landing.dev
```
curl -i http://vm.local/blog
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/6.4.PNG">
</p>

6.5 Mengakses http://vm.local/blog akan diarahkan ke http://lxc_php7.dev
```
curl -i http://vm.local/
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/6.5.PNG">
</p>

6.6 Mengakses http://vm.local/app  akan diarahkan ke http://lxc_php5.dev
```
curl -i http://vm.local/app
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/6.6.PNG">
</p>



### 7. Untuk kebutuhan presentasi mereka, browser di laptop mereka harus dapat mengakses ketiga url tersebut.
```
http://vm.local/
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/7.1.PNG">
</p>
```
http://vm.local/app
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/7.2.PNG">
</p>

```
http://vm.local/blog
```
<p align="center">
      	<img src= "https://github.com/ranikusumawati/Sistem_Administrasi_Server/blob/main/asset/7.3.PNG">
</p>



### Analysis

1. Why we can't use ubuntu 16.04 for php5.6 needs, and we have to change the OS to debian 9?
2. Why we have to use LXC Virtualization for website scheme that will be developed?
3. What is a proxy server? Why we think of vm.local as a proxy server?

### Answer of the Analysis

1. Karena ubuntu 16.04 telah beralih ke PHP 7.0 dengan infrastruktur baru untuk paket PHP. Jadi, tidak, Anda tidak dapat menginstal php5 pada Ubuntu 16.04
2. LXC memberikan kemudahan dalam penerapan dan kinerja yang digunakan sangatlah ringan karena hanya memerlukan aplikasi pendukung yang diperlukan saja dalam pengoprasiannya
3. Server proxy adalah aplikasi server yang bertindak sebagai perantara antara klien yang meminta sumber daya dan server yang menyediakan sumber daya itu. Vm.local disebut sebagai server proxy karena vm local jembatan untuk menghubungkan internet
