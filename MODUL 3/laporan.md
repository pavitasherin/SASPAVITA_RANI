**Laporan Modul 3**

- Pavita Sherintama Giantoro (1202190051)
- Rani Kusumawati (1202192029)

---
Paktikum dilaksanakan berdasarkan keadaan yang tertera pada soal dan soal dapat diakses [Klik disini.](https://github.com/aldonesia/Sistem-Administrasi-Server-2021/blob/master/modul-3/silabus.md)
---
Masuk ke ~/ansible/laravel , kemudian membuat file dengan nama sublaravel.yml
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
