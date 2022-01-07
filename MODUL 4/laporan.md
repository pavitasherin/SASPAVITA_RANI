**Laporan Modul 4**

- Pavita Sherintama Giantoro (1202190051)
- Rani Kusumawati (1202192029)
#
1. Apply loadbalancer for /blog and /app with conditions
   
   i. /blog using least_conn
  
   ii. /app uses ip hash
   
   iii. it is recommended to use ansible for installation
   
2. Use apache Jmeter to analyze the difference between /, /app, /blog with loadbalancer and without loadbalancer on traffic of 50, 100 and 150 users. Analysis in terms of time only. Write testing and analysis steps in your own language.

---

- For each container, make 2 copies 

  ```
  lxc-ls -f
  lxc-copy -n ubuntu_php7.4 -N ubuntu_php7.4_2 -sKD
  lxc-copy -n ubuntu_php7.4 -N ubuntu_php7.4_3 -sKD
  lxc-ls -f
  ```
  

- Start each container
  ```
  lxc-ls -f
  lxc-start -n ubuntu_php7.4
  lxc-start -n ubuntu_php7.4_2
  lxc-start -n ubuntu_php7.4_3
  lxc-ls -f
  ```
  

- Change the IP address to 10.0.3.111 in ubuntu_php7.4_2 

  

  

- Go to etc/hosts to register lxc_php7_2.dev

  ```
  sudo nano /etc/hosts
  ```

  

- Change the server name

  ```
  sudo nano /etc/nginx/sites-available/lxc_php7.dev
  ```

  

- Restart nginx and make curl

  ```
  curl -i lxc_php7_2.dev
  ```

- Change the IP address to 10.0.3.121 in ubuntu_php7.4_3

  ```
  sudo nano /etc/netplan/10-lxc.yaml
  lxc-attach ubuntu_php7.4_3
  nano /etc/netplan/10-lxc.yaml
  ip r
  ```

  

- Go to etc/hosts to regidter lxc_php7_3.dev

  ```
  sudo nano /etc/hosts
  ```

  

- Change the server name

  ```
  sudo nano /etc/nginx/sites-available/lxc_php7.dev
  ```


  

- Restart nginx and make curl

  ```
  curl -i lxc_php7_3.dev
  ```
  

- Start all container

  ```
  lxc-ls -f
  ```

  

- Go to debian_php5.6_2 and change IP address to 10.0.3.112

  ```
  sudo nano /etc/network/interfaces
  ```
  

- Register lxc_php5_2 /etc/hosts

  ```
  nano /etc/hosts
  ```

- Change the name server

  ```
  sudo nano /etc/nginx/sites-available/lxc_php5.dev
  ```

- Restart nginx and curl it

  ```
  curl -i lxc_php5_2.dev
  ```

  

- Go to debian_php5.6_3 and change IP address to 10.0.3.122

  
  ```
  sudo nano /etc/network/interfaces
  ```

- Regist lxc_php5_2.dev /etc/hosts

  
  ```
  nano /etc/hosts
  ```

  

- Change the server name

   ```
  sudo nano /etc/nginx/sites-available/lxc_php5.dev
  ```

  

- Restart nginx and curl it

  ```
  curl -i lxc_php5_3.dev
  ```

  

- Regist all the container

  ```
  nano /etc/hosts
  ```

  

- Run the jmeter. Change the number from 50,100, 150

  ![23](https://user-images.githubusercontent.com/92453574/148266058-08ebd465-6b73-405c-b32e-884cf3f37999.png)

  ![24](https://user-images.githubusercontent.com/92453574/148266063-a629ddcb-b9b8-4794-aef2-d2ee161c18fb.png)

  ![25](https://user-images.githubusercontent.com/92453574/148266064-3108f728-c1e8-4bce-ab91-45ebe3f53b32.png)

  ![26](https://user-images.githubusercontent.com/92453574/148266067-3c5efdf5-aa06-4d22-8e7a-36a2294b40cb.png)

  ![27](https://user-images.githubusercontent.com/92453574/148266071-00fba6b7-abcc-4605-b3ed-511f6d053efc.png)

  ![28](https://user-images.githubusercontent.com/92453574/148266074-1871a9f3-1af4-4d93-9d82-929c149795a8.png)

  ![29](https://user-images.githubusercontent.com/92453574/148266076-054a71e3-8871-428c-9237-8b1d01f652c6.png)

  ![30](https://user-images.githubusercontent.com/92453574/148324939-c92623ff-8c32-4116-a549-f10a705a18d4.png)

  ![31](https://user-images.githubusercontent.com/92453574/148266080-a099b597-281e-4f9f-a9ba-8b35b93e0715.png)
  
  ![32](https://user-images.githubusercontent.com/92453574/148266082-069c8023-f7b5-4cd2-b471-364863a68ab9.png)

  ![33](https://user-images.githubusercontent.com/92453574/148266084-0fd3b98b-e315-4ce5-85d1-fe4626167994.png)

  ![34](https://user-images.githubusercontent.com/92453574/148266086-fd4e92e7-7003-4c25-bfa7-e56561a6f75a.png)

  

- Go back to VM and go to

  ```
  /etc/nginx/sites-available/vm.local
  ```

  

- Add upstream landing, php5, and php7

  ![35](https://user-images.githubusercontent.com/92453574/148266090-e27e64b6-9867-4b05-bae5-623f2092d1ec.PNG)

  

- Go back to jmeter and redo

  ![36](https://user-images.githubusercontent.com/92453574/148266091-da0ec16e-a9da-4ae9-a6f5-b6772d968936.png)

  ![37](https://user-images.githubusercontent.com/92453574/148266098-dee00661-12b6-43c9-a4c6-aa3b3f4977f1.png)

  ![38](https://user-images.githubusercontent.com/92453574/148266100-29947b49-bbad-47b6-9450-1cbb56e3a56f.png)

  ![39](https://user-images.githubusercontent.com/92453574/148266103-5e5331a5-1c41-4eaf-bb70-38705cf8a98f.png)

  ![40](https://user-images.githubusercontent.com/92453574/148266105-fd658891-4807-4b05-b149-c875d123c279.png)

  ![41](https://user-images.githubusercontent.com/92453574/148266112-11518da3-bc7b-4d56-b59a-b906770e3ff8.png)

  ![42](https://user-images.githubusercontent.com/92453574/148266117-f6861925-f66d-45b9-8cd8-696232ebff0e.png)

  ![43](https://user-images.githubusercontent.com/92453574/148266120-d040db1b-5baf-438f-802f-ea87c4c0952e.png)

  ![44](https://user-images.githubusercontent.com/92453574/148266125-02eff9bc-9810-40d2-b08d-22c7892f032e.png)

  ![45](https://user-images.githubusercontent.com/92453574/148266127-5a73d8cc-5664-4bdf-aea9-51890b0740b7.png)

  ![46](https://user-images.githubusercontent.com/92453574/148266134-fb6251fb-cc42-4ed7-aef2-16ec44276a0e.png)

  ![47](https://user-images.githubusercontent.com/92453574/148266138-7d44c886-26e3-4c53-9fb3-ba529c9f19c8.png)

  

Analysis

if we use load balancer, then the time is faster and the amount of users that accessing our web is much more then when we don't use load balancer
