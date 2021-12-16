**Laporan Modul 3**

- Pavita Sherintama Giantoro (1202190051)
- Rani Kusumawati (1202192029)
#
Soal praktikum dapat diakses disini [Klik disini.](https://github.com/aldonesia/Sistem-Administrasi-Server-2021/blob/master/modul-3/silabus.md)
#
- Masuk ke ~/ansible/laravel , kemudian membuat file dengan nama sublaravel.yml
```
cd ~/ansible/laravel
nano sublaravel.yml
```
![image](https://user-images.githubusercontent.com/92929042/146447764-39f3bacb-1b25-419b-9ab9-9c57b35f3648.png)
```
---
- hosts: all
  become : yes
  tasks:
    - name: install bind9 dan dnsutils
      apt:
       pkg:
         - bind9
         - dnsutils
```
- Langkah selanjutnya adalah menginstal paket dengan ansible
![image](https://user-images.githubusercontent.com/92929042/146448663-639109a7-c2ed-4bda-bc60-b736efc17869.png)
- Buat file config1.yml
![image](https://user-images.githubusercontent.com/92929042/146448686-53e2efd2-f771-43be-baf9-06697ec57f9b.png)
```
---
- hosts: all
  become : yes
  tasks:
   - name: membuat direktori
     file:
      path: /var/www/html/dev/landing
      state: directory
   - name: copy file vm.local
     copy:
      src: /etc/bind/vm/vm.local
      dest: /var/www/html/dev/landing
   - name: mengganti konfigurasi
     replace:
      path: /var/www/html/dev/landing/vm.local
      regexp: 'www'
      replace: 'dev'
   - name: copy file named.conf.local
     copy:
      src: /etc/bind/named.conf.local
      dest: /etc/bind/named.conf.local
   - name: mengganti konfigurasi conf local
     replace:
      path: /etc/bind/named.conf.local
      regexp: '/etc/bind/vm/vm.local'
      replace: '/var/www/html/dev/landing/vm.local'
   - name: mengganti konfigurasi conf local part2
     replace:
      path: /etc/bind/named.conf.local
      regexp: '/etc/bind/vm/115.168.192.in-addr.arpa'
      replace: '/var/www/html/dev/landing/115.168.192.in-addr.arpa'
   - name: copy file 115.168.192.in-addr.arpa
     copy:
      src: /etc/bind/vm/115.168.192.in-addr.arpa
      dest: /var/www/html/dev/landing
   - name: copy file resolv.conf
     copy:
      src: /etc/resolv.conf
      dest: /etc/resolv.conf
   - name: copy file named.conf.options
     copy:
      src: /etc/bind/named.conf.options
      dest: /etc/bind/named.conf.options
   - name: restart nginx
     service:
      name: nginx
      state: restarted
   - name: restart bind9
     action: service name=bind9 state=restarted
```
- Lakukan instalasi
![image](https://user-images.githubusercontent.com/92929042/146448936-78bfb1a5-83da-4119-8725-be5f396bd974.png)
- Menambahkan subdomain ke /etc/host
![image](https://user-images.githubusercontent.com/92929042/146449010-dbd74258-128d-4e04-a510-b0cff16eb45e.png)
- Buka vm.local file
![image](https://user-images.githubusercontent.com/92929042/146449068-7f15be52-89f3-4726-aee5-774a299efb6a.png)
- Tambahkan baris www. Setelah itu keluar lxc
![image](https://user-images.githubusercontent.com/92929042/146449492-d0f8115e-05ef-49bb-979a-72c68b83ebf2.png)
- Membuka dan mengedit vm.local di direktori /etc/nginx/sites-enabled/
![image](https://user-images.githubusercontent.com/92929042/146449305-d3be82b1-837b-465b-b383-9c072ba27693.png)
![image](https://user-images.githubusercontent.com/92929042/146449330-3bda7d92-e566-4990-b9d2-ee87d4764138.png)
- Membuka dan mengedit vm.local di direktori /etc/bind/vm/
![image](https://user-images.githubusercontent.com/92929042/146449532-cef2b041-d857-43f3-83b4-8b32ec5d77e5.png)
- Mulai ulang semua paket
![image](https://user-images.githubusercontent.com/92929042/146449597-ecd1dc31-ea81-41b1-8a85-b38ad9074b2b.png)
- Buka Pengaturan Wifi, tambahkan server dns
![image](https://user-images.githubusercontent.com/92929042/146449743-2cf7bf50-1e6c-4dad-a5ea-5da2de5c92a8.png)
- Hasil
![22](https://user-images.githubusercontent.com/92929042/146450118-79f0763d-f382-4fef-a216-cf8ef913f2be.jpg)
