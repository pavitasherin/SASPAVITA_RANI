## UAS 
- Pavita Sherintama Giantoro (1202190051)
- Rani Kusumawati (1202192029)
---

- Buat LXC yang terdiri dari 6 LXC ubuntu, 2 LXC debian PHP, dan 1 LXC debian mariadb. Setting autostart dan IP setiap LXC
  <p align="center">
        	<img src= "UAS/1.jpeg">
  </p>
- Setting hosts ansible
  <p align="center">
        	<img src= "UAS/2.jpeg">
  </p>
- Buat folder tubes pada ~/ansible
  <p align="center">
        	<img src= "UAS/3.jpeg">
  </p>
  <p align="center">
        	<img src= "UAS/4.jpeg">
  </p>
- Buat beberapa file pada folder ~/ansible/tubes
  <p align="center">
        	<img src= "UAS/5.jpeg">
  </p>
  <p align="center">
        	<img src= "UAS/6.jpeg">
  </p>
  <p align="center">
        	<img src= "UAS/7.jpeg">
  </p>
  <p align="center">
        	<img src= "UAS/9.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/laravel/tasks
  ```
  ---
  - name: delete apt chache
    become: yes
    become_user: root
    become_method: su
    command: rm -vf /var/lib/apt/lists/*
  
  - name: Download and install Composer
    shell: curl -sS https://getcomposer.org/installer | php
    args:
      chdir: /usr/src/
      creates: /usr/local/bin/composer
      warn: false
    become: yes
  
  - name: Add Composer to global path
    copy:
      dest: /usr/local/bin/composer
      group: root
      mode: '0755'
      owner: root
      src: /usr/src/composer.phar
      remote_src: yes
    become: yes
  
  - name: Ansible delete file create-project
    file:
      path: /var/www/html/laravel
      state: absent
  
  - name: composer create-project
    shell: /usr/local/bin/composer create-project laravel/laravel /var/www/html/laravel --prefer-dist --no-interaction
  
  - name: Copy .env.template
    template:
      src=templates/env.template
      dest=/var/www/html/laravel/.env
  
  - name: composer
    shell: cd /var/www/html/laravel; /usr/local/bin/composer install  --no-interaction
  
  - name: key
    shell: /usr/bin/php7.4 /var/www/html/laravel/artisan key:generate
  
  - name: chmod
    become: yes
    become_user: root
    become_method: su
    command: chmod 777 -R /var/www/html/laravel/storage
  
  - name: Copy lv.conf
    template:
      src=templates/lv.conf
      dest=/etc/nginx/sites-available/{{ domain }}
    vars:
      servername: '{{ domain }}'
  
  - name: copy php7.conf
    template:
      src=templates/php7.conf
      dest=/etc/php/7.4/fpm/pool.d/www.conf
  
  - name: Symlink lv.conf
    command: ln -sfn /etc/nginx/sites-available/{{ domain }} /etc/nginx/sites-enabled/{{ domain }}
    notify:
      - restart nginx
  
  - name: Write {{ domain }} to /etc/hosts
    lineinfile:
      dest: /etc/hosts
      regexp: '.*{{ domain }}$'
      line: "127.0.0.1 {{ domain }}"
      state: present
  ```
  <p align="center">
        	<img src= "UAS/10.jpeg">
  </p>
- Buat beberapa file pada ~/ansible/tubes/roles/laravel/templates
  <p align="center">
        	<img src= "UAS/11.jpeg">
  </p>
  <p align="center">
        	<img src= "UAS/12.jpeg">
  </p>
  <p align="center">
        	<img src= "UAS/13.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/php/tasks
  <p align="center">
        	<img src= "UAS/14.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/php/handlers
  <p align="center">
        	<img src= "UAS/15.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/codeigniter/tasks
  <p align="center">
        	<img src= "UAS/16.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/codeigniter/handlers
  <p align="center">
        	<img src= "UAS/17.jpeg">
  </p>
- Buat file app.conf pada ~/ansible/tubes/roles/codeigniter/templates
  <p align="center">
        	<img src= "UAS/18.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/db/tasks
  <p align="center">
        	<img src= "UAS/19.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/db/handlers
  <p align="center">
        	<img src= "UAS/20.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/db/templates
  <p align="center">
        	<img src= "UAS/21.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/pma/tasks
  <p align="center">
        	<img src= "UAS/22.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/pma/handlers
  <p align="center">
        	<img src= "UAS/23.jpeg">
  </p>
- Buat file pma.local pada ~/ansible/tubes/roles/pma/templates
  <p align="center">
        	<img src= "UAS/24.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/wp/tasks
  <p align="center">
        	<img src= "UAS/25.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/wp/handlers
  <p align="center">
        	<img src= "UAS/26.jpeg">
  </p>
- Buat file wp.local pada ~/ansible/tubes/roles/wp/templates
  <p align="center">
        	<img src= "UAS/27.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/yii/tasks
  <p align="center">
        	<img src= "UAS/28.jpeg">
  </p>
- Buat file main.yml pada ~/ansible/tubes/roles/yii/handlers
  <p align="center">
        	<img src= "UAS/29.jpeg">
  </p>
- Buat file yii.conf pada ~/ansible/tubes/roles/yii/templates
  <p align="center">
        	<img src= "UAS/30.jpeg">
  </p>
- Buat file dengan nama kelompok3.fpsas, lalu masukkan script dibawah ini
  ```
  upstream laravel {
          least_conn;
          server lxc_php7_1L.dev;
          server lxc_php7_2L.dev;
          server lxc_php7_4L.dev;
          server lxc_php7_6L.dev;
  }
  
  upstream wordpress {
          ip_hash;
          server lxc_php7_2W.dev;
          server lxc_php7_3W.dev;
          server lxc_php7_4W.dev;
          server lxc_php7_5W.dev;
  }
  
  upstream yii {
          server lxc_php7_1Y.dev weight=3;
          server lxc_php7_2Y.dev weight=2;
          server lxc_php7_4Y.dev weight=4;
          server lxc_php7_5Y.dev weight=1;
          server lxc_php7_6Y.dev weight=6;
  }
  
  upstream codeigniter {
          server lxc_php5_1.dev;
          server lxc_php5_2.dev;
  }
  
  server {
          listen 80;
          listen [::]:80;
  
          server_name kelompok3.fpsas;
  
          root /var/www/html;
          index index.html;
  
          location /product {
                  rewrite /product/?(.*)$ /$1 break;
                  proxy_pass http://yii;
          }
  
          location /app {
                  rewrite /app/?(.*)$ /$1 break;
                  proxy_pass http://codeigniter;
          }
  
          location /phpmyadmin{
                  rewrite /phpmyadmin/?(.*)$ /$1 break;
                  proxy_pass http://lxc_mariadb.dev;
          }
  
          location / {
                  #rewrite /?(.*)$ /$1 break;
                  proxy_pass http://laravel;
          }
  }
  
  server {
          listen 80;
          listen [::]:80;
  
          server_name news.kelompok3.fpsas;
  
          root /var/www/html;
          index index.html;
  
          location / {
                  #rewrite /?(.*)$ /$1 break;
                  proxy_pass http://wordpress;
          }
  }
  ```
  <p align="center">
        	<img src= "UAS/32.jpeg">
  </p>


- cek konfigurasi pada web https://kelompok3.fpsas

---
