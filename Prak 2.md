**Laporan Modul 2**

- Pavita Sherintama Giantoro (1202190051)
- Rani Kusumawati (1202192029)

---

1. **Rubah LXC landing dengan ubuntu focal (destroy n create, same ip, same name)**

   - Menghapus container ubuntu_landing sebelum membuat container baru dengan nama yang sama 
     ```
     lxc-destroy ubuntu_landing
     ```
     ![1](https://user-images.githubusercontent.com/78127403/144471046-fbe09e50-430b-4fc8-a128-a7caa77c2a72.jpg) 

     ![2](https://user-images.githubusercontent.com/78127403/144471674-fb0bbc80-d473-406a-ae6e-90472838087d.jpg)

     ![4](https://user-images.githubusercontent.com/78127403/144471859-3825b7b3-35f3-4d74-a677-06bea2a69c5e.jpg)  


   - Buat container lxc ubuntu versi focal baru 
     ```
     lxc-create -n ubuntu_landing -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
     lxc-start ubuntu_landing
     lxc-attach ubuntu_landing
     ```

     ![5](https://user-images.githubusercontent.com/78127403/144472116-c910974b-af64-4c42-ac19-2c9dcb720cd2.jpg)
     

   - Konfigurasi IP static di dalam nano
     ```
     nano /etc/netplan/00-installer-config.yaml
     ```

     ![6](https://user-images.githubusercontent.com/78127403/144472667-97d37a95-cb31-4760-8c8f-b52df6fdd823.jpg)


     ```
     netplan apply
     ```
     ![7](https://user-images.githubusercontent.com/78127403/144473058-6f4c51e3-f91e-4d79-b65f-43ce22d126a0.jpg)

     

     

   - Kemudian install open ssh server 
     ```
     apt-get install openssh-server -y
     ```
     ![8](https://user-images.githubusercontent.com/78127403/144473064-97dad895-d08d-44cb-930f-7c6e52e283e5.jpg)

     
   
   - Lalu lakukan konfigurasi ssh
     ```
     nano /etc/ssh/sshd_config
     ```
     
     ![9](https://user-images.githubusercontent.com/78127403/144473295-7019f43f-1750-4e2f-9685-2acaa6b43a61.jpg)

     
     
   - Buat password baru
     ```
     service sshd restart
     passwd
     ```
     ![10](https://user-images.githubusercontent.com/78127403/144473432-b485cc2c-2b1c-4e7e-99d2-e95fc78e383e.jpg)

     
     
     
   - Cek ssh 
     ```
     ssh root@10.0.3.103
     ```
     ![11](https://user-images.githubusercontent.com/78127403/144473477-e5ba51df-7b31-4075-bcd4-8b988d0bfe0d.jpg)

     
     





2. **Rubah LXC php7 dengan ubuntu focal (destroy n create, same ip, same name)**

   - menghapus container ubuntu php 7.4
     ```
     lxc-destroy ubuntu_php7.4 -f
     ```
     ![1](https://user-images.githubusercontent.com/78127403/144475789-d66aee25-992b-487d-80a9-91074618056f.jpg)


     

   - buat container lxc ubuntu versi focal 

     ```
     lxc-create -n ubuntu_php7.4 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
     ```

     

     ```
     lxc-start ubuntu_php7.4
     lxc-attach ubuntu_php7.4
     apt-get install nano net-tools curl
     ```

     ![2](https://user-images.githubusercontent.com/78127403/144476232-de9cc625-b4df-4677-a701-f1d48f9ce88c.jpg)


   - konfigurasi menjadi IP statik 
     ```
     nano /etc/netplan/10-lxc.yaml
     ```
     ![3](https://user-images.githubusercontent.com/78127403/144476410-81027bca-d7ae-4ffb-9a76-7a079e7e5edd.jpg)



     ```
     netplan apply
     ```
     ![4](https://user-images.githubusercontent.com/78127403/144476482-6074d40d-0ee5-4fab-8b6c-83048d9e685f.jpg)


     

   - kemudian install open ssh server 
     ```
     lxc-start ubuntu_php7.4
     lxc-attach ubuntu_php7.4
     apt-get install openssh-server -y
     ```
     ![5](https://user-images.githubusercontent.com/78127403/144476786-d60d0afb-c8dc-4f6b-bdd1-b9b695e1b12e.jpg)


   - lalu lakukan konfigurasi ssh
     ```
     nano /etc/ssh/sshd_config
     ```
   
     ![6](https://user-images.githubusercontent.com/78127403/144476922-6cab201e-616f-4408-ab22-3dc141c6a891.jpg)

   
    - buat password baru
      ```
      service sshd restart
      passwd
      ```

      ![7](https://user-images.githubusercontent.com/78127403/144477113-aff507be-dbf5-4a08-befd-2c2876eafd73.jpg)

     
    - cek ssh      
      ```
      ssh root@10.0.3.103
      ```
     
      ![8](https://user-images.githubusercontent.com/78127403/144477196-91d7540c-b93c-4a4a-a9fa-e0467ba2be93.jpg)

     
     

3. **vm.local/**

   - Install laravel dengan ansible
   
     1.Pertama kita membutuhkan untuk memasukkan pada `cd ~/ansible/modul2-ansible` lalu kita membutuhkan untuk membuat file dengan nama install-laravel.yml
      
       ![1](https://user-images.githubusercontent.com/78127403/144529896-c20a7eb0-8e35-43aa-a859-3179f10a8f6c.jpg)

       ![2](https://user-images.githubusercontent.com/78127403/144529901-664d1d24-fe02-4eb0-9c69-444ee1f109d8.jpg)

       ![3](https://user-images.githubusercontent.com/78127403/144529904-f10f25fe-d047-4cc6-8ac7-7ed955b8e26c.jpg)
       
       ```
       nano install-laravel.yml
       #Inside install-laravel.yml
       ---
       - hosts: ubuntu_landing
         vars:
             username: 'admin'
             password: 'SysAdminSas0102' #DON'T FORGET TO CHANGE
             domain: 'lxc_landing.dev'
         roles:
             - php
             - lv
       ```

     2.Setelah itu membuat direktori untuk tasks dan handlers di folder php,lalu masukkan tasks main.yml untuk install packages
       
       ![4](https://user-images.githubusercontent.com/78127403/144486023-d1faa200-c864-469a-9c6b-535dacc53b1f.jpg)

       ![5](https://user-images.githubusercontent.com/78127403/144486029-42bb946e-d0a8-44e5-afa7-bc87c6a8e512.jpg)
       
     3.Lalu masukkan handlers main.yml untuk restart php

       ![6](https://user-images.githubusercontent.com/78127403/144593373-25b07335-6b7e-42a8-8a87-188b90064b0a.jpg)

       ![7](https://user-images.githubusercontent.com/78127403/144593378-eb289f9a-c310-413f-931c-25f7989fe6f0.jpg)
       
     4.Setelah itu kita membuat direktori untuk tasks, templates, dan handlers di folder lv, lalu masukkan tasks main.yml untuk install package laravel dan composer
       ```
       mkdir -p roles/php/tasks
       mkdir -p roles/php/handlers
       cd roles/php/tasks
       nano main.yml
       ```
       ![8](https://user-images.githubusercontent.com/78127403/144593804-9fdc25b5-814c-4222-9be6-f01dc7a8e584.jpg)

       ![9](https://user-images.githubusercontent.com/78127403/144593812-15c7273e-36e5-4da4-8385-89d7b8d9052b.jpg)

       ![10](https://user-images.githubusercontent.com/78127403/144593815-16356f6e-0adc-4346-a42f-e9d8fec6cdf6.jpg)

       ![11](https://user-images.githubusercontent.com/78127403/144593820-eabaa27c-e5e0-4433-af3a-c78e43332bb5.jpg)

       Tidak ada interaksi yang digunakan karena itu sistem tidak melakukan pertanyaan interactive 
       
       ![12](https://user-images.githubusercontent.com/78127403/144593922-61511a0d-e4ab-4216-9c7f-6a1280bafeef.jpg)
       
     5.Lalu masukkan templete env.template (Ini adalah laravel konfigurasi)
     
       ```
       cd roles/lv/templates
       nano env.template
       ```
       ![13](https://user-images.githubusercontent.com/78127403/144594715-b66736f8-29f8-472a-972e-0a5c1e76f2eb.jpg)

       ![14](https://user-images.githubusercontent.com/78127403/144594726-40107d0e-e968-4a85-ab52-11c65d5c2533.jpg)

       ![15](https://user-images.githubusercontent.com/78127403/144594732-7ff56b53-9cff-4014-a504-1cd60660747e.jpg)

     6.Setelah itu kita masukkan templates lv.conf untuk nginx configuration
     
       ```
       nano lv.conf
       ```
       ![16](https://user-images.githubusercontent.com/78127403/144594915-db77f685-4253-4483-9427-6f75fb38d92e.jpg)

       ![17](https://user-images.githubusercontent.com/78127403/144594920-5a4d7c8c-7fa7-4f21-b82a-7ea9033a3e2a.jpg)
       
     7.Lalu kita memasukkan handlers main.yml untuk restart php dan nginx
      
       ```
       cd roles/lv/handlers
       nano main.yml
       ```
       ![18](https://user-images.githubusercontent.com/78127403/144595183-19c5f28f-fa66-4aad-84ed-e9b1d4d3fb93.jpg)

       ![19](https://user-images.githubusercontent.com/78127403/144595190-fb228894-8944-46ab-af1a-3540950b9512.jpg)

     8.Setelah itu kita jalankan ansible playbook
     
       ```
       ansible-playbook -i hosts install-laravel -k
       ```
       ![20](https://user-images.githubusercontent.com/78127403/144595332-7f5d9c93-f53e-47fa-8d7a-feea619d2cf8.jpg)

       ![21](https://user-images.githubusercontent.com/78127403/144595324-044f33ac-9e0e-4d0b-b250-456256d21a77.jpg)
       
     9.Sudah selesai terinstal. Tetapi kikta belum selesai, kita membutuhkan untuk mengeceknya. Buka http://vm.local/ di web browser

       ![22](https://user-images.githubusercontent.com/78127403/144595410-dd9fe3a2-4795-4f0c-9e80-7cb1196f9ab7.jpg)


4. **vm.local/blog**
   - Edit deploy-wp
     ```
     cd ~/ansible/modul2-ansible
     nano deploy-wp.yml
     ```

     ![1](https://user-images.githubusercontent.com/78127403/144533283-05315c93-29cb-4f40-a428-1689c346ef4f.jpg)
  
     ![2](https://user-images.githubusercontent.com/78127403/144533289-00ebd68c-b46d-4b2e-a2d8-8a7325afa793.jpg)

   - Buat roles wp
     ```
     mkdir -p roles/wp
     mkdir -p roles/wp/handlers
     mkdir -p roles/wp/tasks
     mkdir -p roles/wp/templates
     ```
     ![3](https://user-images.githubusercontent.com/78127403/144533474-fd5056ef-3b92-4ffc-9046-4d857cf46051.jpg)

     ![4](https://user-images.githubusercontent.com/78127403/144533482-688b3ba1-ca31-47cf-9e93-b2d6823d6092.jpg)
     
     ![5](https://user-images.githubusercontent.com/78127403/144533485-56062ec5-35e4-42b5-b487-7e991fec0a3e.jpg)

     ![6](https://user-images.githubusercontent.com/78127403/144533486-2dcb7c91-c7ea-41b7-9e0d-70a0b04df54f.jpg)

   - Isi pada /tasks/main.yml
     ```
     ---
     - name: delete apt chache
       become: yes
       become_user: root
       become_method: su
       command: rm -vf /var/lib/apt/lists/*
  
     - name: install requirement dpkg to install php7.4
       become: yes
       become_user: root
       become_method: su
       apt: name={{ item }} state=latest update_cache=true
       with_items:
         - ca-certificates
         - apt-transport-https
         - curl
         - python-apt
         - software-properties-common
    
     - name: Add Php Repository 7.4
       apt_repository:
       repo: "ppa:ondrej/php"
       state: present
       filename: php.list
       update_cache: true
     
     - name: install nginx php7.4
       become: yes
       become_user: root
       become_method: su
       apt: name={{ item }} state=latest update_cache=true
       with_items:
           - nginx
           - nginx-extras
           - curl
           - wget
           - php7.4
           - php7.4-fpm
           - php7.4-curl
           - php7.4-gd
           - php7.4-opcache
           - php7.4-mbstring
           - php7.4-zip
           - php7.4-json
           - php7.4-cli
           - php7.4-mysqlnd
           - php7.4-xmlrpc
      
     - name: wget wordpress
       shell: wget -c http://wordpress.org/latest.tar.gz
      
     - name: tar latest.tar.gz
       shell: tar -xvzf latest.tar.gz
    
     - name: copy folder wordpress
       shell: cp -R wordpress /var/www/html/blog
    
     - name: chmod
       become: yes
       become_user: root
       become_method: su
       command: chmod 775 -R /var/www/html/blog/
    
     - name: copy .wp-config.conf
       template:
         src=templates/wp.conf
         dest=/var/www/html/blog/wp-config.php
      
     - name: copy wp.local
       template:
         src=templates/wp.local
         dest=/etc/nginx/sites-available/{{ domain }}
       vars:
         servername: '{{ domain }}'

     - name: Delete another nginx config

       become: yes
       become_user: root
       become_method: su
       command: rm -f /etc/nginx/sites-enabled/*
    
     - name: Symlink sites-available wordpress
       command: ln -sfn /etc/nginx/sites-available/{{ domain }} /etc/nginx/sites-enabled/{{ domain }}
       notify:
           - restart nginx

     - name: Write {{ domain }} to /etc/hosts
       lineinfile:
         dest: /etc/hosts
         regexp: '.*{{ domain }}$'
         line: "127.0.0.1   {{ domain }}"
         state: present

     - name: enable module php mbstring
       command: phpenmod mbstring
       notify:
         -restart php
     ```

   - Isi pada /templates/wp.conf
     ```
     <?php
     /**
     * The base configuration for WordPress
     *
     * The wp-config.php creation script uses this file during the installation.
     * You don't have to use the web site, you can copy this file to "wp-config.php"
     * and fill in the values.
     *
     * This file contains the following configurations:
     *
      * * MySQL settings
      * * Secret keys
      * * Database table prefix
      * * ABSPATH
      *
      * @link https://wordpress.org/support/article/editing-wp-config-php/
      *
      * @package WordPress
       */

      define( 'WP_HOME', 'http://vm.local/blog' );
      define( 'WP_SITEURL', 'http://vm.local/blog' );

      // ** MySQL settings - You can get this info from your web host ** //
      /** The name of the database for WordPress */
      define( 'DB_NAME', 'blog' );

      /** MySQL database username */
      define( 'DB_USER', 'admin' );

      /** MySQL database password */
      define( 'DB_PASSWORD', 'chintya' );

      /** MySQL hostname */
      define( 'DB_HOST', '10.0.3.200:3306' );

      /** Database charset to use in creating database tables. */
      define( 'DB_CHARSET', 'utf8' );

      /** The database collate type. Don't change this if in doubt. */
      define( 'DB_COLLATE', '' );

      /**#@+
      * Authentication unique keys and salts.
      *
      * Change these to different unique phrases! You can generate these using
      * the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}.
      *
      * You can change these at any point in time to invalidate all existing cookies.
      * This will force all users to have to log in again.
      *
      * @since 2.6.0
      */
      define( 'AUTH_KEY',         'put your unique phrase here' );
      define( 'SECURE_AUTH_KEY',  'put your unique phrase here' );
      define( 'LOGGED_IN_KEY',    'put your unique phrase here' );
      define( 'NONCE_KEY',        'put your unique phrase here' );
      define( 'AUTH_SALT',        'put your unique phrase here' );
      define( 'SECURE_AUTH_SALT', 'put your unique phrase here' );
      define( 'LOGGED_IN_SALT',   'put your unique phrase here' );
      define( 'NONCE_SALT',       'put your unique phrase here' );

      /**#@-*/

      /**
      * WordPress database table prefix.
      *
      * You can have multiple installations in one database if you give each
      * a unique prefix. Only numbers, letters, and underscores please!
      */
      $table_prefix = 'wp_';

      /**
      * For developers: WordPress debugging mode.
      *
      * Change this to true to enable the display of notices during development.
      * It is strongly recommended that plugin and theme developers use WP_DEBUG
      * in their development environments.
      *
      * For information on other constants that can be used for debugging,
      * visit the documentation.
      *
      * @link https://wordpress.org/support/article/debugging-in-wordpress/
      */
      define( 'WP_DEBUG', false );

      /* Add any custom values between this line and the "stop editing" line. */



      /* That's all, stop editing! Happy publishing. */

      /** Absolute path to the WordPress directory. */
      if ( ! defined( 'ABSPATH' ) ) {
            define( 'ABSPATH', __DIR__ . '/' );
      }

      /** Sets up WordPress vars and included files. */
      require_once ABSPATH . 'wp-settings.php';
      ```

    - Isi pada /templates/wp.local
      ```
      server {

          listen 80;

          server_name {{ domain }};

          root /var/www/html/blog;
          index index.php;

          charset utf-8;

          location / {
              try_files $uri $uri/ /index.php?$query_string;
          }

          location ~ \.php$ {
              try_files $uri =404;
              fastcgi_split_path_info ^(.+\.php)(/.+)$;
              fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
              fastcgi_index index.php;
              fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
              include fastcgi_params;
          }
      }

      ```
      ![7](https://user-images.githubusercontent.com/78127403/144533924-a2583cea-ce2f-4cf2-a3bc-79bdc98edddf.jpg)

      ![8](https://user-images.githubusercontent.com/78127403/144533926-042874c8-650d-40df-b851-3e18b5f95717.jpg)

      ![9](https://user-images.githubusercontent.com/78127403/144533928-b9380665-9932-4f7b-9eed-fa32777f95a1.jpg)
   
      ![10](https://user-images.githubusercontent.com/78127403/144533930-fe2da0d3-64ef-4d13-8818-3dbe21ff91d6.jpg)
   
      ![11](https://user-images.githubusercontent.com/78127403/144533932-20450a29-a551-4656-896f-48e816c9dcda.jpg)
      
    - Isi /handlers/main.yml
      ```
      ---
      - name: restart nginx
        become: yes
        become_user: root
        become_method: su
        action: service name=nginx state=restarted
        
      ![12](https://user-images.githubusercontent.com/78127403/144534036-f8a9cf33-414b-49bd-975e-e7148d97c863.jpg)

      - name: restart php
        become: yes
        become_user: root
        become_method: su
        action: service name=php7.4-fpm state=restarted
      ```
  
    - Jalankan
      ```
      cd ~/ansible/modul2-ansible
      ansible-playbook -i hosts deploy-wp.yml -k
      ```
      ![13](https://user-images.githubusercontent.com/78127403/144590936-b37ce412-eb59-4f16-b272-b9ba73171e34.jpg)

      ![14](https://user-images.githubusercontent.com/78127403/144590944-897e5133-c33c-471f-99de-b8ff05888dab.jpg)

    - Hasil

      ![15](https://user-images.githubusercontent.com/78127403/144534082-507b443d-df88-4b31-a7d2-9299ba72283b.jpg)

      ![16](https://user-images.githubusercontent.com/78127403/144534086-3b74f634-298e-4d05-a7fe-24ca75268791.jpg)

      ![17](https://user-images.githubusercontent.com/78127403/144534089-e3db5d7c-531e-408a-a6f2-d2842da98aa1.jpg)

      ![18](https://user-images.githubusercontent.com/78127403/144534092-a379200b-311a-4f5a-91e5-405ae569954f.jpg)

   

**Soal Tambahan**

1. Laravel

   - masuk pada konfigurasi file lxc_landing

     ```
     cd ~/ansible/laravel/
     nano lxc_landing.dev
     ```

    ![1](https://user-images.githubusercontent.com/92453574/144454260-0268c6ab-f8f9-4176-89b1-57637a28e1b3.PNG)

   

   - akan tertampil seperti dibawah ini

     ![2 sebelum](https://user-images.githubusercontent.com/92453574/144454266-874e97d1-d13c-49f7-9367-8e61778d9f3a.PNG)

     

   - kemudian rubah menjadi seperti gambar di bawah

     ![2 sesudah](https://user-images.githubusercontent.com/92453574/144454268-ca06dc8c-579c-44aa-801a-e698c6d010df.PNG)

     

   - buat ansible dengan nama "tambahan.yml"

     ```
     nano tambahan.yml
     ```

     ![3](https://user-images.githubusercontent.com/92453574/144454272-f729e4a7-a77a-45ac-86ae-bd98ba089344.PNG)

     

   - jalankan ansible "tambahan.yml"

     ```
     ---
     - hosts: all
       become : yes
       tasks:
        - name: mengganti php sock
          lineinfile:
           path: /etc/php/7.4/fpm/pool.d/www.conf
           regexp: '^(.*)listen =(.*)$'
           line: 'listen = 127.0.0.1:9001'
           backrefs: yes
        - name: copy the nginx config file 
          copy:
           src: ~/ansible/laravel/lxc_landing.dev
           dest: /etc/nginx/sites-available/lxc_landing.dev
        - name: Symlink lxc_landing.dev
          command: ln -sfn /etc/nginx/sites-available/lxc_landing.dev /etc/nginx/sites-enabled/lxc_landing.dev
          args:
           warn: false
        - name: restart nginx
          service:
           name: nginx
           state: restarted
        - name: restart php7
          service:
           name: php7.4-fpm
           state: restarted
        - name: curl web
          command: curl -i http://lxc_landing.dev
          args:
           warn: false
     ```

     ![4](https://user-images.githubusercontent.com/92453574/144454275-8616d722-c706-4fad-bd27-15c44609cd8e.PNG)
     ![5](https://user-images.githubusercontent.com/92453574/144454276-051793f1-3ba1-4322-bdca-9d98dbc61b11.PNG)

     

   - buka vm.local untuk mengecek apakah berhasil.

     ![6](https://user-images.githubusercontent.com/92453574/144454280-1c81ba96-6679-49be-a7a7-12ed236446f3.PNG)

   - berhasil

     

   

2. Wordpress

   - masuk pada konfigurasi file wordpress.conf

     ```
     cd wordpress/
     nano wordpress.conf
     ```

     ![1](https://user-images.githubusercontent.com/92453574/144454321-5a9855df-ca3f-4fe2-b0b8-e8ae7f056832.PNG)

     

   - akan tertampil seperti dibawah ini

     ![2 sebelum](https://user-images.githubusercontent.com/92453574/144454324-5234b081-781a-47aa-9ce5-30c6cc711bbf.PNG)

     

   - kemudian ubah menjadi seperti di bawah ini

     ![2 sesudah](https://user-images.githubusercontent.com/92453574/144454326-574058ef-2528-4226-bdd3-651c3a95a1d8.PNG)

     

   - buat ansible dengan nama "tambahan.yml"

     ```
     nano tambahan.yml
     ```

     ![3](https://user-images.githubusercontent.com/92453574/144454329-829ab04f-284e-47f8-8005-72e9201bcaa9.PNG)

     

   - jalankan ansible "tambahan.yml"

     ```
     ---
     - hosts: all
       become : yes
       tasks:
        - name: mengganti php sock
          lineinfile:
           path: /etc/php/7.4/fpm/pool.d/www.conf
           regexp: '^(.*)listen =(.*)$'
           line: 'listen = 127.0.0.1:9001'
           backrefs: yes
        - name: copy the nginx config file 
          copy:
           src: ~/ansible/wordpress/wordpress.conf
           dest: /etc/nginx/sites-available/lxc_php7.dev
        - name: Symlink lxc_php7.dev
          command: ln -sfn /etc/nginx/sites-available/lxc_php7.dev /etc/nginx/sites-enabled/lxc_php7.dev
          args:
           warn: false
        - name: restart nginx
          service:
           name: nginx
           state: restarted
        - name: restart php7
          service:
           name: php7.4-fpm
           state: restarted
        - name: curl web
          command: curl -i http://lxc_php7.dev
          args:
           warn: false
     ```

     ![4](https://user-images.githubusercontent.com/92453574/144454333-f5781906-e330-4880-a0b8-b85cee85da88.PNG)

     ![5](https://user-images.githubusercontent.com/92453574/144454337-8c341508-c2a4-4052-afba-250a0a616143.PNG)

     

   - buka vm.local/blog untuk mengecek apakah berhasil

     ![6](https://user-images.githubusercontent.com/92453574/144454342-e37f8022-b5b6-48f4-a60f-08cbba37f956.PNG)

   - berhasil




















