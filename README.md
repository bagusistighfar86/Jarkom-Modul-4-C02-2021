# Jarkom-Modul-4-C02-2021

|         Nama        |       NRP      |
|        :----:       |     :----:     |
| Muhammad Bagus I    | 05111940000049 |
| Christoffer Ivano   | 05111940000091 |
| Bayu Adjie Sidharta | 05111940000172 |

## VLSM (CPT)

Tentukan pembagian jumlah subnet yang efektif berdasarkan topologi yang ada

[![TOPOLOGI-VLSM-01.png](https://i.postimg.cc/K8dNg2fp/TOPOLOGI-VLSM-01.png)](https://postimg.cc/Snf8wHwc)

Tentukan jumlah alamat IP yang dibutuhkan oleh tiap subnet dan lakukan labelling netmask berdasarkan jumlah IP yang dibutuhkan.

[![1638005326654.jpg](https://i.postimg.cc/TPz4GbBw/1638005326654.jpg)](https://postimg.cc/B8CgBjS9)

Hitung pembagian IP berdasarkan netmask tersebut menggunakan pohon pada gambar berikut, kemudian lakukan subnetting dengan menggunakan pohon tersebut untuk pembagian IP sesuai dengan kebutuhan masing-masing subnet yang ada :

[![VLSM.jpg](https://i.postimg.cc/6Qrd2GyT/VLSM.jpg)](https://postimg.cc/Ny0yZF8w)

Dari pohon dari pohon tersebut akan mendapat pembagian IP sebagai berikut :

[![1638005802304.jpg](https://i.postimg.cc/W3Kbs5TZ/1638005802304.jpg)](https://postimg.cc/Q9QrbkBN)










## CIDR (GNS3)
![test-Page-1 drawio](https://user-images.githubusercontent.com/31591861/143676227-7e8d4eba-9d68-44de-b4bd-ead5d29e9402.png)

### Perhitungan Subnet
#### Langkah 1
Pertama-tama jumlah alamat IP yang dibutuhkan ditentukan untuk tiap subnet dan dilakukan labelling netmask berdasarkan jumlah IP yang dibutuhkan.
```
| Subnet | Jumlah IP | Netmask |
| ------ | --------- | ------- |
| A1     | 101       | /25     |
| A2     | 2021      | /21     |
| A3     | 2         | /30     |
| A4     | 701       | /22     |
| A5     | 2         | /30     |
| A6     | 1001      | /22     |
| A7     | 2         | /30     |
| A8     | 521       | /22     |
| A9     | 2         | /30     |
| A10    | 502       | /23     |
| A11    | 13        | /28     |
| A12    | 252       | /24     |
| A13    | 721       | /22     |
| Total  | 5841      | /19     |
```
Berdasarkan total IP dan netmask yang dibutuhkan, maka kita dapat menggunakan netmask /19 untuk memberikan pengalamatan IP pada subnet.

#### Langkah 2
Gabunglah beberapa subnet kecil menjadi subnet yang lebih besar dengan berkala

#### Gabungan pertama 
```
| Subnet | Combination | Jumlah IP | Netmask |
| ------ | ----------- | --------- | ------- |
| B1     | A1          | 2122      | /20     |
|        | A2 
| B2     | A12         | 973       | /21     |
|        | A13
| B3     | A10         | 515       | /22     |
|        | A11 
```

#### Gabungan kedua 
```
| Subnet | Combination | Jumlah IP | Netmask |
|--------|-------------|-----------|---------|
| C1     | B1          | 2124      | /19     |
|        | A3          |           |         |
| C2     | B2          | 975       | /20     |
|        | A9          |           |         |
| C3     | B3          | 1036      | /21     |
|        | A8          |           |         |
```

#### Gabungan ketiga
```
| Subnet | Combination | Jumlah IP | Netmask |
|--------|-------------|-----------|---------|
| C1     | B1          | 2124      | /19     |
|        | A3          |           |         |
| C2     | B2          | 975       | /20     |
|        | A9          |           |         |
| C3     | B3          | 1036      | /21     |
|        | A8          |           |         |
```

#### Gabungan ke-empat
```
| Subnet | Combination | Jumlah IP | Netmask |
|--------|-------------|-----------|---------|
| D1     | C1          | 2825      | /18     |
|        | A4          |           |         |
| D2     | C2          | 1811      | /19     |
|        | C3          |           |         |

```
#### Gabungan ke-lima
```
| Subnet | Combination | Jumlah IP | Netmask |
|--------|-------------|-----------|---------|
| E1     | D1          | 2827      | /17     |
|        | A5          |           |         |
| E2     | D2          | 1813      | /18     |
|        | A7          |           |         |
```

#### Gabungan ke-enam
```
| Subnet | Combination | Jumlah IP | Netmask |
|--------|-------------|-----------|---------|
| F1     | E2          | 2814      | /17     |
|        | A6          |           |         |
```

#### Gabungan ketujuh
```
| Subnet | Combination | Jumlah IP | Netmask |
|--------|-------------|-----------|---------|
| G1     | G1          | 5841      | /16     |
|        | E1          |           |         |
```

Lalu dengan tabel yang sudah dibuat, buatlah pohon subnet
![test-Page-2 drawio (3)](https://user-images.githubusercontent.com/31591861/143676242-ae26d00f-e02d-4c6f-87c7-aaa27af30598.png)

Lalu buat ulang table baru dengan ip subnet yang didapatkan dari tree tersebut.
```
| Subnet | Type              | IP              | Binary                              |
|--------|-------------------|-----------------|-------------------------------------|
| A1     | Network ID        | 10.15.136.0     | 00001010.00001111.10001000.00000000 |
|        | Netmask           | 255.255.255.128 | 00000000.00000000.00000000.01111111 |
|        | Broadcast Address | 10.15.136.127   | 00001010.00001111.10001000.01111111 |
| A2     | Network ID        | 10.15.128.0     | 00001010.00001111.10000000.00000000 |
|        | Netmask           | 255.255.248.0   | 00000000.00000000.00000111.11111111 |
|        | Broadcast Address | 10.15.135.255   | 00001010.00001111.10000111.11111111 |
| A3     | Network ID        | 10.15.144.0     | 00001010.00001111.10010000.00000000 |
|        | Netmask           | 255.255.255.252 | 00000000.00000000.00000000.00000011 |
|        | Broadcast Address | 10.15.144.3     | 00001010.00001111.10010000.00000011 |
| A4     | Network ID        | 10.15.160.0     | 00001010.00001111.10100000.00000000 |
|        | Netmask           | 255.255.252.0   | 00000000.00000000.00000011.11111111 |
|        | Broadcast Address | 10.15.163.255   | 00001010.00001111.10100011.11111111 |
| A5     | Network ID        | 10.15.192.0     | 00001010.00001111.11000000.00000000 |
|        | Netmask           | 255.255.255.252 | 00000000.00000000.00000000.00000011 |
|        | Broadcast Address | 10.15.192.3     | 00001010.00001111.11000000.00000011 |
| A6     | Network ID        | 10.15.64.0      | 00001010.00001111.01000000.00000000 |
|        | Netmask           | 255.255.252.0   | 00000000.00000000.00000011.11111111 |
|        | Broadcast Address | 10.15.67.255    | 00001010.00001111.01000011.11111111 |
| A7     | Network ID        | 10.15.32.0      | 00001010.00001111.00100000.00000000 |
|        | Netmask           | 255.255.255.252 | 00000000.00000000.00000000.00000011 |
|        | Broadcast Address | 10.15.32.3      | 00001010.00001111.00100000.00000011 |
| A8     | Network ID        | 10.15.20.0      | 00001010.00001111.00010100.00000000 |
|        | Netmask           | 255.255.252.0   | 00000000.00000000.00000011.11111111 |
|        | Broadcast Address | 10.15.23.255    | 00001010.00001111.00010111.11111111 |
| A9     | Network ID        | 10.15.8.0       | 00001010.00001111.00001000.00000000 |
|        | Netmask           | 255.255.248.0   | 00000000.00000000.00000111.11111111 |
|        | Broadcast Address | 10.15.15.255    | 00001010.00001111.00001111.11111111 |
| A10    | Network ID        | 10.15.16.0      | 00001010.00001111.00010000.00000000 |
|        | Netmask           | 255.255.254.0   | 00000000.00000000.00000001.11111111 |
|        | Broadcast Address | 10.15.17.255    | 00001010.00001111.00010001.11111111 |
| A11    | Network ID        | 10.15.18.0      | 00001010.00001111.00010010.00000000 |
|        | Netmask           | 255.255.255.240 | 00000000.00000000.00000000.00001111 |
|        | Broadcast Address | 10.15.19.15     | 00001010.00001111.00010011.00001111 |
| A12    | Network ID        | 10.15.4.0       | 00001010.00001111.00000100.00000000 |
|        | Netmask           | 255.255.255.0   | 00000000.00000000.00000000.11111111 |
|        | Broadcast Address | 10.15.4.255     | 00001010.00001111.00000100.11111111 |
| A13    | Network ID        | 10.15.0.0       | 00001010.00001111.00000000.00000000 |
|        | Netmask           | 255.255.252.0   | 00000000.00000000.00000011.11111111 |
|        | Broadcast Address | 10.15.3.255     | 00001010.00001111.00000011.11111111 |
```

Lalu routing dapat dikerjakan.

### Routing

#### Subnetting

Pertama-tama, topologi dibuat dalam GNS3.
![image](https://user-images.githubusercontent.com/31591861/143676823-7479a333-c992-4938-a64a-db1b9c55e6e8.png)

alu setiap node dikonfigurasi dengan cara `Configure > Edit Network Configuration`. Berikut merupakan salah satu contoh, yaitu menggunakan node `Foosha`:

Pada Edit Network Configuration Foosha, isi konfigurasi masing-masing jalur berdasarkan subnetting yang sudah dibuat sebelumnya:

```
#Static config for eth0
auto eth0
iface eth0 inet static
	address 10.15.64.1
	netmask 255.255.252.0
  
auto eth1
iface eth1 inet static
	address 10.15.192.1
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.15.140.1
	netmask 255.255.255.252

auto eth3
iface eth3 inet static
	address 10.15.32.1
	netmask 255.255.255.252
  
auto eth4
iface eth4 inet static
	address 192.168.122.25
	netmask 255.255.255.0
	gateway 192.168.122.1
```

Misal, karena disini eth0 mengarah ke `Blueno (1000 Host)`, maka kita menggunakan subnet A6 dengan NID `10.15.64.0`. Pada konfigurasi `Foosha`, address untuk `eth0`-nya ditambahi 1 dari NID subnet A6 hingga menjadi `10.15.64.1`. Untuk kliennya, yaitu `Blueno (1000 Host)`, address untuk `eth0`-nya ditambahi 1 lagi dari IP Foosha sehingga menjadi `10.15.64.2`. Untuk netmasknya mengikuti tabel yang telah dibuat sebelumnya. Gateway hanya digunakan untuk klien dan server dan mengarah ke IP router terdekat, jadi gateway untuk klien Blueno (1000 Host) adalah `10.15.64.1`.

Hal ini dilakukan pada semua node dan subnetting pun selesai.

#### Routing
Terdapat 2 macam Routing yang dilakukan yaitu untuk antar router dan untuk router ke klien.  

##### Antar Router

Untuk antar router, dilakukan Default Routing pada setiap router yang bukan main router yang terconnect ke internet, pada kali ini foosha yang arahnya dari router yang lebih jauh dari Foosha ke yang lebih dekat ke `Foosha`. Misal, dari Pucci dilakukan Default Routing ke `Water7`, maka ditambahkan kode berikut pada `Pucci`:

route add -net 0.0.0.0 netmask 0.0.0.0 gateway 10.15.144.1

Karena merupakan default routing, maka NID dan Netmasknya 0.0.0.0, sedangkan gatewaynya merupakan IP dari `eth1`-nya `Water7`.

Hal ini dilakukan pada semua router yang bukan `Foosha`.

##### Router ke Klien

Untuk router ke klien, dilakukan routing dari router Foosha ke NID dan Netmask dari klien berdasarkan subnetting yang telah dilakukan. Misal dilakukan routing dari Foosha ke klien `Jipangu`, maka ditambahkan kode berikut pada `Foosha`:

route add -net 10.15.136.0 netmask 255.255.255.128 gateway 10.15.192.2

NID 10.15.136.0 dan Netmask 255.255.255.128 didapatkan berdasarkan tabel subnetting sedangkan gateway 10.15.192.2 merupakan IP `eth2`-nya dari `Water7`, dikarenakan untuk mencapai klien Jipangu perlu melalui router `Water7`.

Hal ini dilakukan untuk semua klien.

Routing dari semua router akan menjadi

#### Pucci
```
route add -net 0.0.0.0  netmask 0.0.0.0  gateway 10.15.144.1
```

#### Water7
```
route add -net 0.0.0.0 netmask 0.0.0.0 gateway 10.15.192.1
route add -net 10.15.136.0 netmask 255.255.255.128 gateway 10.15.144.2
route add -net 10.15.128.0 netmask 255.255.248.0 gateway 10.15.144.2
```

#### Foosha
```
route add -net 11.15.136.0 netmask 255.255.255.128 gateway 10.15.192.2
route add -net 10.15.144.0 netmask 255.255.255.252 gateway 10.15.192.2
route add -net 10.15.128.0 netmask 255.255.248.0 gateway 10.15.192.2
route add -net 10.15.20.0 netmask 255.255.252.0 gateway 10.15.32.2
route add -net 10.15.16.0 netmask 255.255.254.0 gateway 10.15.32.2
route add -net 10.15.18.0 netmask 255.255.255.240 gateway 10.15.32.2
route add -net 10.15.160.0 netmask 255.255.252.0 gateway 10.15.192.2
route add -net 10.15.4.0 netmask 255.255.255.0 gateway 10.15.32.2
route add -net 10.15.0.0 netmask 255.255.252.0 gateway 10.15.32.2
route add -net 10.15.8.0 netmask 255.255.255.252 gateway 10.15.32.2
route add -net 10.15.140.4 netmask 255.255.255.252 gateway 10.15.32.2
```

#### Guanhao
```
route add -net 0.0.0.0 netmask 0.0.0.0 gateway 10.15.32.1
route add -net 10.15.18.0 netmask 255.255.255.240 gateway 10.15.16.3
route add -net 10.15.4.0 netmask 255.255.255.0 gateway 10.15.8.2
route add -net 10.15.0.0 netmask 255.255.252.0 gateway 10.15.8.2
route add -net 10.15.140.4 netmask 255.255.255.252 gateway 10.15.8.2
```

#### Alabasta
```
route add -net 0.0.0.0 netmask 0.0.0.0 gateway 10.15.16.1
```

#### Oimo
```
route add -net 0.0.0.0 netmask 0.0.0.0 gateway 10.15.8.1
route add -net 10.15.0.0 netmask 255.255.252.0 gateway 10.15.4.3
```

#### Seastone
```
route add -net 0.0.0.0 netmask 0.0.0.0 gateway 10.15.4.1
```

#### Testing

Pertama-tama jangan lupa untuk menambahkan kode ini pada `Foosha`:

iptables -t nat -A POSTROUTING -o eth4 -j MASQUERADE -s 10.15.0.0/16

Selain itu jangan lupa untuk menambahkan kode ini juga pada setiap node agar dapat terhubung ke internet:

echo nameserver 192.168.122.1 > /etc/resolv.conf

Setup pun selesai dan kita bisa melakukan testing ping antar node, berikut merupakan beberapa contoh ping:

1. Cipher ke Doriki
![image](https://user-images.githubusercontent.com/31591861/143677237-808c908b-3622-458f-8f04-0887359b333f.png)

2. Cipher ke Google.com
![image](https://user-images.githubusercontent.com/31591861/143677257-2205341f-2dc1-44ff-b02d-e8677bb3cf5f.png)

3. Jipangu ke Elena
![image](https://user-images.githubusercontent.com/31591861/143677274-10e15db7-3635-41d4-bbf1-7bb3617c5bab.png)

4. Elena ke Fukurou
![image](https://user-images.githubusercontent.com/31591861/143677291-de4b9bf7-eafd-4fd4-8902-c8377211e194.png)

5. Elena ke google.com
![image](https://user-images.githubusercontent.com/31591861/143677303-32af437f-1a6f-4473-812a-06bf268484d0.png)

6. Elena ke Jipangu
![image](https://user-images.githubusercontent.com/31591861/143677315-412d9b9d-1c1c-4899-b298-1dedb929a386.png)



## Kendala
1. Bingung dibagian server apakah dibagi IP atau tidak
2. 
