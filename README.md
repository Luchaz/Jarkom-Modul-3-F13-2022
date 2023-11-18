# Jarkom-Modul-3-F13-2022

| **No** | **Nama**                         | **NRP**    |
| ------ | -------------------------------- | ---------- |
| 1      | Helmi Abiyu Mahendra             | 5025211061 |
| 2      | Muhammad Naufal Fawwaz Ramadhan  | 5025211223 |


--------------------------------
## Topologi

![topologi](Images/topologi.png)

### Netwok Configuration

Router:
* Aura (Router/DHCP Relay):
    ```sh

    ```

Switch 1
* Himmel (DHCP Server):
    ```sh
   
    ```

* Heiter (DNS Server):
    ```sh
   
    ```

Switch2
* Denken (Database Server):
    ```sh
 
    ```

* Eisen (Load Balancer):
    ```sh
  
    ```

Switch3
* Revolte (Client):
    ```sh
    
    ```

* Richter (Client):
    ```sh
   
    ```

* Lawine (Laravel Worker):
    ```sh
 
    ```

* Linie (Laravel Worker):
    ```sh

    ```

* Lugner (Laravel Worker):
    ```sh

    ```

Switch4
* Sein (Client):
    ```sh

    ```

* Stark (Client):
    ```sh

    ```

* Frieren (PHP Worker):
    ```sh

    ```

* Flamme (PHP Worker):
    ```sh
 
    ```

* Fern (PHP Worker):
    ```sh
  
    ```

## Setup DHCP

### Setup DHCP Relay on `Aura`

1. install `isc-dhcp-relay`
2. configure `/etc/default/isc-dhcp-relay`
3. configure `/etc/sysctl.conf`
4. run `service isc-dhcp-relay restart`

* `/etc/default/isc-dhcp-relay`:
    ```sh
  
    ```
* `/etc/sysctl.conf`:
    ```sh
  
    ```

### Setup DHCP Server on `Himmel`

1. install `isc-dhcp-server`
2. konfigurasi `/etc/default/isc-dhcp-server`
3. konfigurasi `/etc/dhcp/dhcpd.conf`
4. jalankan `service isc-dhcp-server restart`

* `/etc/default/isc-dhcp-server`:
    ```sh
   
    ```

* `/etc/dhcp/dhcpd.conf`:
    ```sh

    ```

## Soal 1

> Setelah mengalahkan Demon King, perjalanan berlanjut. Kali ini, kalian diminta untuk melakukan register domain berupa `riegel.canyon.f04.com` untuk worker Laravel dan `granz.channel.f04.com` untuk worker PHP (0) mengarah pada worker yang memiliki IP `192.223.x.1`.


1. tambakan `nameserver` pada `/etc/resolv.conf`
...

* `/etc/resolv.conf`:
    ```sh
 
    ```

* `/etc/bind/named.conf.local`:
    ```sh

    ```

* `/etc/bind/named.conf.options`:
    ```sh

    ```

* `/etc/bind/granz/granz.channel.f04.com`:
    ```sh

    ```

* `/etc/bind/riegel/riegel.canyon.f04.com`:
    ```sh

    ```

## Soal 2
 > Client yang melalui Switch3 mendapatkan range IP dari 192.223.3.16 - 192.223.3.32 dan 192.223.3.64 - 192.223.3.80



1. tambahkan konfigurasi range ip pada `/etc/default/isc-dhcp-server` on `Himmel`

* `/etc/default/isc-dhcp-server`:
    ```sh
    ...
   
    ...
    ```

## Soal 3

> Client yang melalui Switch4 mendapatkan range IP dari 192.223.4.12 - 192.223.4.20 dan 192.223.4.160 - 192.223.4.168


1. add ip range configuration in `/etc/default/isc-dhcp-server` on `Himmel`

* `/etc/default/isc-dhcp-server`:
    ```sh
    ...
  
    ...
    ```

## Soal 4

> Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut


1. tambahkan konfigurasi DNS pada `/etc/default/isc-dhcp-server` di `Himmel` menuju `Heiter`

* `/etc/default/isc-dhcp-server`:
    ```sh
    ...
 
    ...
    ```
    
## Soal 5

> Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit


1. add lease time configuration in `/etc/default/isc-dhcp-server` on `Himmel`

* `/etc/default/isc-dhcp-server`:
    ```sh
    ...
   
    ...
    ```
    
    
## Soal 6

> Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.


Pada tiap PHP worker:

1. install `nginx php php-fpm`
...

* download dan unzip file dengan command berikut:
    ```sh
   
    ```
* `/etc/nginx/sites-available/granz.channel.f04`:
    ```sh

    ```
    
## Soal 7

> Kepala suku dari Bredt Region memberikan resource server sebagai berikut: <br>
> a. Lawine, 4GB, 2vCPU, dan 80 GB SSD. <br>
> b. Linie, 2GB, 2vCPU, dan 50 GB SSD. <br>
> c. Lugner 1GB, 1vCPU, dan 25 GB SSD. <br>
> aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.


Untuk melakukan testing, kita dapat menggunakan `ApacheBench`. berikut adalah langkah-langkahnya:

Pada salah satu client:

1. install `apache2-utils`

#### hasil:


    
## Soal 8

> Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut: <br>
> a. Nama Algoritma Load Balancer <br>
> b. Report hasil testing pada Apache Benchmark <br>
> c. Grafik request per second untuk masing masing algoritma. <br>
> d. Analisis 


Sebelum melakukan testing algoritma load balancing, kita perlu meng-setup load balancer terlebih dahulu:

Pada `Eisen`:

1. install `nginx`



Untuk melakukan testing, kita dapat menggunakan `ApacheBench`. berikut adalah langkah-langkahnya:

Pada salah satu client:

1. install `apache2-utils`


#### Hasil: 
    
## Soal 9

> Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.
 

Untuk melakukan testing, kita dapat menggunakan `ApacheBench`. berikut adalah langkah-langkahnya:

Pada salah satu client:

1. install `apache2-utils`


#### Hasil: 

    
## Soal 10

> Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: `netics` dan password: `ajkf04`, dengan yyy merupakan kode kelompok. Terakhir simpan file `htpasswd` nya di `/etc/nginx/rahasisakita/` .
 

Pada Eisen:

1. buat directory baru `/etc/nginx/rahasiakita/`


* `/etc/nginx/sites-available/lb-jarkom`:
    ```sh
   
    ```

#### Hasil: 


    
## Soal 11

> Lalu buat untuk setiap request yang mengandung `/its` akan di proxy passing menuju halaman `https://www.its.ac.id`.
 

Pada Eisen:

1. konfigurasi `/etc/nginx/sites-available/lb-jarkom` 

* `/etc/nginx/sites-available/lb-jarkom`:
    ```sh

    ```

#### Hasil: 



## Soal 12

> Selanjutnya LB ini hanya boleh diakses oleh client dengan IP `192.223.3.69`, `192.223.3.70`, `192.223.4.167`, dan `192.223.4.168`.
 

Pada Eisen:

1. konfigurasi `/etc/nginx/sites-available/lb-jarkom` 

* `/etc/nginx/sites-available/lb-jarkom`:
    ```sh

    
    ```

#### Hasil: 



## Soal 13 & 14

> Karena para petualang kehabisan uang, mereka kembali bekerja untuk mengatur `riegel.canyon.f04.com`.
> 1. Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh `Lawine`, `Linie`, dan `Lugner`. (13)
> 2. `Lawine`, `Linie`, dan `Lugner` memiliki Riegel Canyon sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi `PHP8.0` dan `Composer` (14)

Pada `Danken`

1. tambakan `nameserver 192.223.1.3 # IP Heiter` pada `/etc/resolv.conf`


* `queries.sql`:
    ```sql
   
    ```

* `/etc/mysql/my.cnf`:
    ```sh

    ```

Pada `Lawine`, `Linie`, dan `Lugner`:

Untuk setup Laravel:

1. install `mariadb-client`, `php8.0`, `git`, dan `composer`


* `.env`:
    ```sh
    ...

    ...
    ```

Untuk setup deploy Laravel menggunakan Nginx:

1. install `nginx`


* `/etc/nginx/sites-available/riegel.canyon.f04`:
    ```sh
  
    
    ```

#### Hasil: 



## Soal 15

> 3. Riegel Canyon memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.<br>
> a. POST /auth/register


Pada salah satu client:

1. buat `register.json` yang memuat akun yang ingin diregister


* `register.json`:
    ```js
   
    ```

#### Hasil:


## Soal 16

> 3. Riegel Canyon request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.<br>
> b. POST /auth/login


Pada salah satu client:

1. buat `register.json` yang memuat akun yang ingin diregister
...

#### Hasil:



## Soal 17

> 3. Riegel Canyon memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.<br>
> c. GET /me



#### Hasil:


## Soal 18

> 4. Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Canyon maka implementasikan Proxy Bind pada `Eisen` untuk mengaitkan IP dari `Lawine`, `Linie`, dan `Lugner`.



## Soal 19

> Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada `Lawine`, `Linie`, dan `Lugner`. Untuk testing kinerja naikkan 
>
> * pm.max_children
> * pm.start_servers
> * pm.min_spare_servers
> * pm.max_spare_servers
> 
> sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire.


Pada `Lawine`, `Linie`, dan `Lugner`:

1. konfigurasi `/etc/php/8.0/fpm/pool.d/www.conf`


#### Hasil:


## Soal 20

> Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second



#### Hasil:

