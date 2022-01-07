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

  ![1](https://user-images.githubusercontent.com/92453574/148256371-b51204b9-7971-4edb-8ab8-dbe6c0223c64.PNG)

  

- Start each container

  ![2](https://user-images.githubusercontent.com/92453574/148256379-4f6de51e-b8e0-43ed-93e1-86dbcbd78b00.PNG)

  

- Change the IP address to 10.0.3.111 in ubuntu_php7.4_2 

  ![3](https://user-images.githubusercontent.com/92453574/148256383-4ed9f83c-0fd2-4235-a3d9-1739226f733e.PNG)

  

- Go to etc/hosts to register lxc_php7_2.dev

  ![5](https://user-images.githubusercontent.com/92453574/148256391-1554aac7-2abd-47ab-a30b-8d7e6ddf69f4.PNG)

  

- Change the server name

  ![6](https://user-images.githubusercontent.com/92453574/148256397-fa168430-5032-47b6-a671-f739e4d6aebd.PNG)

  

- Restart nginx and make curl

  ![7](https://user-images.githubusercontent.com/92453574/148256400-9df0671d-a2a4-4c2b-8719-622fed31ced4.PNG)

- Change the IP address to 10.0.3.121 in ubuntu_php7.4_3

  ![8](https://user-images.githubusercontent.com/92453574/148256403-b388e3a0-9ae9-420e-a865-d1c2f473dd5e.PNG)

  ![9](https://user-images.githubusercontent.com/92453574/148256409-95b80c9a-1a20-4d16-82b3-9a5c59382c6f.PNG)

  

- Go to etc/hosts to regidter lxc_php7_3.dev

  ![10](https://user-images.githubusercontent.com/92453574/148256412-6d256292-a0d7-44a3-bf4c-fc175755819e.PNG)

  

- Change the server name

  ![11](https://user-images.githubusercontent.com/92453574/148256415-c00fb359-ac6d-4042-a509-3e4156855f83.PNG)


  

- Restart nginx and make curl

  ![12](https://user-images.githubusercontent.com/92453574/148256359-e59c1ebe-169b-49ba-8016-e17a749a383a.PNG)

  

- Start all container

  ![13](https://user-images.githubusercontent.com/92453574/148256810-6cae00d2-ea9b-4caf-9242-d71ec1ee2fbf.PNG)

  

- Go to debian_php5.6_2 and change IP address to 10.0.3.112

  ![14](https://user-images.githubusercontent.com/92453574/148256822-77a227de-0164-4d5e-908f-b5651a668afe.PNG)
  

- Register lxc_php5_2 /etc/hosts

  ![15](https://user-images.githubusercontent.com/92453574/148256825-10a0e105-bf04-4ee2-8026-ab67388d45dc.PNG)

  

- Change the name server

  ![16](https://user-images.githubusercontent.com/92453574/148256828-52569a85-0e0a-43ae-9e14-bce121e627d8.PNG)

  

- Restart nginx and curl it

  ![17](https://user-images.githubusercontent.com/92453574/148256833-4af698d8-996b-4fd1-b6ed-116dbab2cd5c.PNG)

  

- Go to debian_php5.6_3 and change IP address to 10.0.3.122

  ![18](https://user-images.githubusercontent.com/92453574/148256837-e85f69e8-e415-4906-a562-1e26f0ed93c5.PNG)

  

- Regist lxc_php5_2.dev /etc/hosts

  ![19](https://user-images.githubusercontent.com/92453574/148256846-284c1f4c-3f91-4484-80e8-94212fb98aef.PNG)

  

- Change the server name

  ![20](https://user-images.githubusercontent.com/92453574/148256850-733dae1e-3e21-419e-9d77-232cf2968a5a.PNG)

  

- Restart nginx and curl it

  ![21](https://user-images.githubusercontent.com/92453574/148256855-5ae882e0-e81d-4c4f-ae3f-6a03db1fe894.PNG)

  

- Regist all the container

  ![22](https://user-images.githubusercontent.com/92453574/148256866-cd4aaf10-5ff2-460b-9e51-13c4d9798aa9.PNG)

  

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
