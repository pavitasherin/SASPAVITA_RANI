# Modul 4 - Web Server, Load Balancing dan uji performansi
- Pavita Sherintama Giantoro (1202190051)
- Rani Kusumawati (1202192029)
---
## Soal Praktikum
1. Terapkan loadbalancer untuk /blog dan /app dengan ketentuan
	1. /blog menggunakan least_conn
	2. /app menggunakan ip hash
	3. disarakan menggunakan ansible untuk instalasi
2. Gunakan apache Jmeter untuk menganalisa perbedaan antara /, /app, /blog dengan loadbalancer dan tanpa loadbalancer pada traffic 50, 100 dan 150 users. Analisa dari segi waktu saja. Tulis langkah testing dan analisa dengan bahasa sendiri.

---

## Soal Modul 4
- Pada latihan kita sudah melakukan konfigurasi pada ubuntu_landing
- Maka Step berikutnya yaitu melakukan konfigurasi yang sama terhadap ubuntu php7.4 dan debian_php5.6 yang akan dilaporkan sebagai berikut :

### Load Balancing
1. Siapkan LXC untuk ubuntu7.4
	* Clone LXC ubuntu_php7.4 menjadi ubuntu_php7.4_2 dan ubuntu_php7.4_3
	
		```sh
		sudo lxc-stop -n ubuntu_php7.4
		sudo lxc-copy -n ubuntu_php7.4 -N ubuntu_php7.4_2 -sKD
		sudo lxc-copy -n ubuntu_php7.4 -N ubuntu_php7.4_3 -sKD
		```
		
		![1](https://user-images.githubusercontent.com/78127403/148645617-6e0ea461-2302-4a26-bb89-4b085947ba17.jpg)

	* Start LXC 
	
		```sh
		sudo lxc-start -n ubuntu_php7.4
		sudo lxc-start -n ubuntu_php7.4_2
		sudo lxc-start -n ubuntu_php7.4_3
		```
		![2](https://user-images.githubusercontent.com/78127403/148645632-d4c6f777-b6ec-41b6-89e8-5762b79c635e.jpg)

	* Masuk ke lxc ubuntu_php7.4_2
	
		```sh
		sudo lxc-attach -n ubuntu_php7.4_2
		```
		
	* Configurasi IP dan nginx ubuntu_php7.4_2
	
		```sh
		nano /etc/netplan/10-lxc.yaml
		```
		
		ganti ip menjadi 10.0.3.111
		
		![3](https://user-images.githubusercontent.com/78127403/148645855-42eaa357-3435-4f64-b60f-fdc9a6ebb5fe.jpg)

		
		terapkan konfigurasi netplan baru
		
		```sh
		netplan apply
		```
		
		check ip
		
		```sh
		ip addr show eth0
		```
		![4](https://user-images.githubusercontent.com/78127403/148645837-670e384d-ec3b-42b3-9cde-acbc46ebf496.jpg)

		
		Daftarkan domain lxc_php7_2.dev di hosts file
		
		```sh
		nano /etc/hosts
		```
		
		![5](https://user-images.githubusercontent.com/78127403/148645868-edf4209e-2a9d-48f0-8508-2bf5bbb18fe0.jpg)

		
		Konfigurasi nginx untuk lxc_php7.4_2.dev
		
		```sh
		nano /etc/nginx/sites-available/lxc_php7.dev
		```
		
		![6](https://user-images.githubusercontent.com/78127403/148645879-7702a263-3cb7-4eb2-bb15-8a7b2218084e.jpg)

		
		Check configurasi nginx dan start nginx
		
		```sh
		nginx -t
		service nginx restart
		```
		
		Coba akses lxc_php7
		
		```sh
		curl -i http://lxc_php7_2.dev
		```
		
		![7](https://user-images.githubusercontent.com/78127403/148645938-7f086b8f-2168-4e84-a50f-c80da5e8852e.jpg)

		
		keluar dari ubuntu_php7.4_2
		
		```sh
		exit
		```
		
	* Masuk ke lxc ubuntu_php7.4_3
	
		```sh
		sudo lxc-attach -n ubuntu_php7.4_3
		```
		
	* Configurasi IP dan nginx ubuntu_php7.4_3
	
		```sh
		nano /etc/netplan/10-lxc.yaml
		```
		
		ganti ip menjadi 10.0.3.121
		
		![8](https://user-images.githubusercontent.com/78127403/148645994-cbe35721-3b1b-44e3-9d59-ef2fa65f19be.jpg)

		
		terapkan konfigurasi netplan baru
		
		```sh
		netplan apply
		```
		
		check ip
		
		```sh
		ip addr show eth0
		```
		
		![9](https://user-images.githubusercontent.com/78127403/148646013-9b2be218-d26d-433c-97dc-2b1e5064e039.jpg)

		
		Daftarkan domain lxc_php7_3.dev di hosts file
		
		```sh
		nano /etc/hosts
		```
		
		![10](https://user-images.githubusercontent.com/78127403/148646027-0ad30199-2dc1-4a1f-876e-94267c71f65b.jpg)

		
		Konfigurasi nginx untuk lxc_php7_3.dev
		
		```sh
		nano /etc/nginx/sites-available/lxc_php7.dev
		```
		![11](https://user-images.githubusercontent.com/78127403/148646043-7c254c1f-0f58-4bd9-954a-67b4a2b4e81a.jpg)
		
		Check configurasi nginx dan start nginx
		
		```sh
		nginx -t
		service nginx restart
		```
		
		Coba akses lxc_php7
		
		```sh
		curl -i http://lxc_php7_3.dev
		```
		
		![12](https://user-images.githubusercontent.com/78127403/148646062-af25c604-fea9-4207-8811-6f25fed4719f.jpg)

		
		exit dari ubuntu_php7.4_3
		
		```sh
		exit
		```
		
2. Siapkan LXC untuk debian_php5.6
	* Clone LXC debian_php5.6 menjadi debian_php5.6_2 dan debian_php5.6_3
	
		```sh
		sudo lxc-stop -n debian_php5.6
		sudo lxc-copy -n debian_php5.6 -N debian_php5.6_2 -sKD
		sudo lxc-copy -n debian_php5.6 -N debian_php5.6_3 -sKD
		```
		![13](https://user-images.githubusercontent.com/78127403/148646164-f221526a-86e9-4586-bc51-284a6b053f7c.jpg)
		
	* Start LXC 
	
		```sh
		sudo lxc-start -n debian_php5.6
		sudo lxc-start -n debian_php5.6_2
		sudo lxc-start -n debian_php5.6_3
		```
		
		![14](https://user-images.githubusercontent.com/78127403/148646174-d98e8fcf-cce1-4fb4-91f8-dd35204bdf02.jpg)

		
	* Masuk ke lxc debian_php5.6_2
	
		```sh
		sudo lxc-attach -n debian_php5.6_2
		```
		
	* Configurasi IP dan nginx debian_php5.6_2
	
		```sh
		nano /etc/network/interfaces
		```
		
		ganti ip menjadi 10.0.3.112
		
		![15](https://user-images.githubusercontent.com/78127403/148646179-235d2f56-8a73-4d33-9a6e-06fda3337624.jpg)
		
		
		Daftarkan domain lxc_php5_2.dev di hosts file
		
		```sh
		nano /etc/hosts
		```
		
		![16](https://user-images.githubusercontent.com/78127403/148646204-e0fbcafb-41ec-4d15-ac02-85ef0930aa5f.jpg)

		
		Konfigurasi nginx untuk lxc_php5.6_2.dev
		
		```sh
		nano /etc/nginx/sites-available/lxc_php5.dev
		```
		
		![17](https://user-images.githubusercontent.com/78127403/148646211-2e80c493-0868-4d31-9c3c-f32a9a0430f9.jpg)

				
		keluar dari debian_php5.6_2
		
		```sh
		exit
		```
		
	* Masuk ke lxc debian_php5.6_3
	
		```sh
		sudo lxc-attach -n debian_php5.6_3
		```
		
	* Configurasi IP dan nginx debian_php5.6_3
	
		```sh
		nano /etc/network/interfaces
		```
		
		ganti ip menjadi 10.0.3.122
		
		
		![18](https://user-images.githubusercontent.com/78127403/148646239-7a0aee84-42f0-4047-8168-9d59cd3a4f06.jpg)

			
		Daftarkan domain lxc_php5_3.dev di hosts file
		
		```sh
		nano /etc/hosts
		```
		
		![19](https://user-images.githubusercontent.com/78127403/148646243-1deb6948-808e-42cd-aeac-54c3cf4beb39.jpg)

		
		Konfigurasi nginx untuk lxc_php5.6_3.dev
		
		```sh
		nano /etc/nginx/sites-available/lxc_php5.dev
		```
		
		![20](https://user-images.githubusercontent.com/78127403/148646252-4bf4e974-a76c-4203-ad05-708007a2ce2d.jpg)

		
		exit dari debian_php5.6_3
		
		```sh
		exit
		```

3. Daftarkan semua kontainer ke dalam `etc host` pada VM

	![21](https://user-images.githubusercontent.com/78127403/148646304-e10e0d97-cf3c-40b8-b999-27f1e2621b59.jpg)

	
	* Jalankan jmeter. Ganti angka pada box (number of threads) dari menu `user access` menjadi `50, 100, 150` . 

	* number of threads `50`
	
	![22](https://user-images.githubusercontent.com/78127403/148646362-02db8cdc-5d28-447d-9a6c-44cd973dd719.jpg)
	![23](https://user-images.githubusercontent.com/78127403/148646365-cbf66e47-4fa9-41ab-b4c5-8a78820e926c.jpg)
	![24](https://user-images.githubusercontent.com/78127403/148646383-ab7728e0-9656-44e6-9c3a-929fe98c628b.jpg)
	![25](https://user-images.githubusercontent.com/78127403/148646385-c9ac2115-3d78-44d8-947c-fbb4a9b93a97.jpg)
	![26](https://user-images.githubusercontent.com/78127403/148646387-0e23b63c-c517-43a2-8a1b-2515b7b2edbf.jpg)

	* number of threads `100`

	![27](https://user-images.githubusercontent.com/78127403/148646397-d6c5416c-757e-467d-b736-7d121b460204.jpg)
	![28](https://user-images.githubusercontent.com/78127403/148646399-fee629dd-e1e8-4781-bb5a-5a4bd3fbef70.jpg)
	![29](https://user-images.githubusercontent.com/78127403/148646403-d3abc493-c18f-454e-9c96-9ad9fd2babe4.jpg)
	![30](https://user-images.githubusercontent.com/78127403/148646410-33772266-652f-405e-96ba-fa81e82fb98c.jpg)
	![31](https://user-images.githubusercontent.com/78127403/148646415-638bb977-0723-457d-99be-dbed159ce876.jpg)

	
	* number of threads `150`

	![32](https://user-images.githubusercontent.com/78127403/148646434-2f166b7f-e04d-4c53-a4b2-5a4a4c09ba7c.jpg)
	![33](https://user-images.githubusercontent.com/78127403/148646439-258e6e70-2545-468b-8307-9d8f6724ae73.jpg)
	![34](https://user-images.githubusercontent.com/78127403/148646440-8517beab-889b-4a38-907a-233d371db102.jpg)
	![35](https://user-images.githubusercontent.com/78127403/148646441-7113bf27-7bf5-4a26-b562-22fbd45266d2.jpg)
	![36](https://user-images.githubusercontent.com/78127403/148646443-63060402-d354-4ddb-937b-4c903a576d89.jpg)


	* Konfigurasi load balancer menggunakan round robin (upstream) untuk halaman landing, php5, dan php7 `vm.local` pada nginx
	
		```sh
		sudo nano /etc/nginx/sites-available/vm.local
		```
		![37](https://user-images.githubusercontent.com/78127403/148646459-6a0387d4-ba07-46c1-abe8-bcc6b81674be.jpg)
		
		Ganti proxy_pass
		
		![38](https://user-images.githubusercontent.com/78127403/148646484-3ed06333-c57c-4df5-bf6d-d2f4a4084c39.jpg)

		
	* Jalankan kembali jmeter dan ulangi kembali untuk Ganti angka pada box (number of threads) dari menu `user access` menjadi `50, 100, 150` . 
	
	* number of threads `50`
	
	![39](https://user-images.githubusercontent.com/78127403/148646517-42de8609-e4e0-410c-a29b-069cbfe1b68b.jpg)
	![40](https://user-images.githubusercontent.com/78127403/148646519-d4219d13-d060-4363-aef4-c8c848d43659.jpg)
	![41](https://user-images.githubusercontent.com/78127403/148646522-27041751-6ce4-4ed4-945d-81e1000239ab.jpg)
	![42](https://user-images.githubusercontent.com/78127403/148646523-51200e7b-bf32-4d55-a184-ab12567085a0.jpg)
	![43](https://user-images.githubusercontent.com/78127403/148646527-53c2ff6f-956c-4826-af4d-b8ee3012dae4.jpg)
	
	* number of threads `100`
	![44](https://user-images.githubusercontent.com/78127403/148646532-e41443cb-2569-4ade-b3ea-3dfed894c3bb.jpg)
	![45](https://user-images.githubusercontent.com/78127403/148646536-311922e8-6416-4cdd-9a39-da371950d16d.jpg)
	![46](https://user-images.githubusercontent.com/78127403/148646544-a00c021f-e541-4b54-852c-e6e3260b35dd.jpg)
	![47](https://user-images.githubusercontent.com/78127403/148646547-dee230f1-4b7e-4dc1-8308-12da030a6056.jpg)
	![48](https://user-images.githubusercontent.com/78127403/148646554-d2be503f-bd23-4627-9218-cb123cdba11b.jpg)
	
	* number of threads `150`

	![49](https://user-images.githubusercontent.com/78127403/148646563-b30a7e79-fd9a-4a8b-84c5-bd81fe3fd1c6.jpg)
	![50](https://user-images.githubusercontent.com/78127403/148646578-a49bf7b3-a5b7-4042-b243-a496a719f32d.jpg)
	![51](https://user-images.githubusercontent.com/78127403/148646588-db7e9e80-63b1-4294-8f38-a1038181528c.jpg)
	![52](https://user-images.githubusercontent.com/78127403/148646599-57aea911-0918-43ac-9c3f-64df496d7dc3.jpg)
	![53](https://user-images.githubusercontent.com/78127403/148646605-2b1b099d-034c-4aa5-b352-a234f7813988.jpg)

		
## Analisys

Berikut perbandingan antara penggunaan load balancer dan tidak
![](assets/analisis2.PNG)

Dari tabel perbandingan di atas dapat disimpulkan bahwa perbedaan antara /, /app, /blog dengan loadbalancer dan tanpa loadbalancer pada traffic 50, 100 dan 150 users dari segi waktu :
- terdapat kestabilan pada traffic yang semakin tinggi dengan menggunakan loadbalancer maka semakin banyak pengguna yang mengakses website yaitu terjadi pada saat jmeter (setelah konfigurasi loadbalancer menggunakan round robin (upstream) dan setting proxy pass pada vm.local) -> pada tabel terdapat pada bagian Average2 dan Troughput2 dengan traffic 150 users dimana akses web lebih cepat dan lebih banyak pengguna. 
- Sedangkan pada percobaan jmeter yang pertama terdapat ketidakstabilan dimana yang tanpa loadbalancer lebih banyak pengguna yang mengakses dilihat dari segi troughputnya yaitu pada traffic 50 user

Keterangan warna di tabel (berkaitan dengan pengguna yang mengakses persekon) :

- Warna merah : Sedikit
- Warna kuning : Sedang
- Warna hijau : Banyak
