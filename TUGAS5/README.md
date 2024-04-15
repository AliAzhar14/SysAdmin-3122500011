# Mail Server dan Local Domain

### Daftar Isi
- [Mail Server dan Local Domain](#mail-server-dan-local-domain)
    - [Daftar Isi](#daftar-isi)
    - [A. Persiapan](#a-persiapan)
    - [B. Setup NTP ( Network Time Protocol )](#b-setup-ntp--network-time-protocol-)
    - [C. Install Web Server ( APACHE2 + PHP-FM )](#c-install-web-server--apache2--php-fm-)
      - [+  Install Apache2](#--install-apache2)
      - [+ Install PHP 8.2](#-install-php-82)
      - [+ Install PHP FM](#-install-php-fm)
    - [D. Install Database server ( Mariadb-Server )](#d-install-database-server--mariadb-server-)
      - [E. Install POSTFIX mailserver (SMTP Server)](#e-install-postfix-mailserver-smtp-server)
    - [F. Install DOVECOT (IMAP POP3)](#f-install-dovecot-imap-pop3)
    - [G. DEBIAN EVOLUTION](#g-debian-evolution)
    - [H. ROUNDCUBE](#h-roundcube)

### A. Persiapan

1. Setup terlebih dahulu mail server pada konfigurasi zone sehingga dapat di resolve ```mail.kelompok2.local```

    > ![alt text](assets/image-1.png)
    > forward

    >![alt text](assets/image-2.png)
    > inverse

2. nslookup

    > ![alt text](assets/image-3.png)


### B. Setup NTP ( Network Time Protocol )

1. Installasi Paket dengan command ``sudo apt install systemd-timesyncd``

2. Ubah TimeZone ke Asia/Jakarta

3. Buat RTC menjadi sama dengan UTC

4. Aktifkan NTP supaya waktu Sinkron

    > ![alt text](<assets/Screenshot 2024-04-14 024813.png>)

5. Ubah config file ``timesync.d``, buat pool ke terdekat supaya delay jadi pendek.

    > ![alt text](assets/image-4.png)

    > List NTP Indonesia https://www.ntppool.org/zone/id

6. Restart Service yang berjalan dan cek statusnya

    > ![alt text](<assets/Screenshot 2024-04-14 025009.png>)

7. Cek Tanggal

    > ![alt text](<assets/Screenshot 2024-04-14 025028.png>)

### C. Install Web Server ( APACHE2 + PHP-FM )

#### +  Install Apache2
1. Install paket dengan command berikut ``sudo apt -y install apache2``



2. Ubah ServerToken Menjadi Prod gunakan Text Editor seperti Nano

    > ![alt text](<assets/Screenshot 2024-04-14 030245.png>)
    > sudo nano /etc/apache2/conf-enabled/security.conf

3. Tambahkan Directory yang dapat diakses

    > ![alt text](<assets/Screenshot 2024-04-14 030341.png>)
    > sudo nano /etc/apache2/mods-enabled/dir.conf

4. Tambahkan ServerName

    > ![alt text](<assets/Screenshot 2024-04-14 030838.png>)
    > sudo nano /etc/apache2/apache2.conf

5. Webmaster email

    > ![alt text](<assets/Screenshot 2024-04-14 031039.png>)
    > sudo nano /etc/apache2/sites-enabled/000-default.conf

6. Reload service apache2


7. Cek apakah webserver berjalan pada browser kita

    > ![alt text](<assets/Screenshot 2024-04-14 032124.png>)

#### + Install PHP 8.2

1. Install dengan perintah berikut


    > sudo apt -y install php8.2 php8.2-mbstring php-pear

2. Cek apakah sudah terinstall
   > php -v


3. Buat sebuah file php untuk memeriksa apakah PHP Berjalan/Fungsi

    > ![alt text](<assets/Screenshot 2024-04-14 032957.png>)

4. Jalankan

    > ![alt text](<assets/Screenshot 2024-04-14 033008.png>)


#### + Install PHP FM

1. Install dengan perintah berikut

    > sudo apt -y install php-fpm

2. Lakukan Konfigurasi pada file apache untuk PHP-FM

    > ![alt text](<assets/Screenshot 2024-04-14 033350.png>)
    > sudo nano /etc/apache2/sites-available/default-ssl.conf

3. setenvif pada ae2enmod proxy_fcgi
4. load config

    > ![alt text](<assets/Screenshot 2024-04-14 033509.png>)

5. Jalankan ulang Servicenya 

    > ![alt text](<assets/Screenshot 2024-04-14 033534.png>)

6. Test kedalam webserver, buat file info.php

    > ![alt text](<assets/Screenshot 2024-04-14 033722.png>)
    > sudo echo '<?php phpinfo(); ?>' > /var/www/html/info.php

7. cek pada web

    > ![alt text](<assets/Screenshot (1669).png>)
    > berhasil


### D. Install Database server ( Mariadb-Server )

1. Install paket dengan perintah berikut


    > sudo apt -y install mariadb-server

2. Pastikan atau ubah charset ke utf8mb4, lalu restart service mariadb

    > ![alt text](<assets/Screenshot 2024-04-14 034101.png>)
    > sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf

3. Lakukan installasi dengan perintah ``sudo mysql_secure_installation``



    Installasi pattern

    
       Enter current password for root (enter for none): Tekan Enter

       Switch to unix_socket authentication [Y/n] n

       Change the root password? [Y/n] n

       Remove anonymous users? [Y/n] y

       Disallow root login remotely? [Y/n] y

       Remove test database and access to it? [Y/n] y

       Reload privilege tables now? [Y/n] y

    Pastikan sama sehingga langkah tetap sama.

4. Masuk kedalam mysql perintah    `mysql`

    > ![alt text](<assets/Screenshot 2024-04-14 034429.png>)

5. Cek akses user root

    > ![alt text](<assets/Screenshot 2024-04-14 034505.png>)

6. Cek daftar user pada database user

    > ![alt text](<assets/Screenshot 2024-04-14 034530.png>)

7. Lihat semua database

    > ![alt text](<assets/Screenshot 2024-04-14 034555.png>)

8. Berarti mysql sudah terinstall, coba buat sebuah dummy database dan table untuk menjalankan beberapa query crud

    > ![alt text](<assets/Screenshot 2024-04-14 034806.png>)

9. Berhasil dan Database mariadb sudah terinstall.



#### E. Install POSTFIX mailserver (SMTP Server)

1. Install dengan perintah ``sudo nano apt -y install postfix sasl2-bin``
2. Pilih yang No Configuration ( kita config manual )
    > ![alt text](<assets/Screenshot (1650).png>)

3. Copy file config /usr/share/postfix/main.cf.dist ke /etc/postfix/main.cf



4. Ubah beberapa Konfigurasi pada file postfix main.cf

    > ![alt text](<assets/Screenshot (1651).png>)
    > ![alt text](<assets/Screenshot (1652).png>)
    > ![alt text](<assets/Screenshot (1653).png>)
    > ![alt text](<assets/Screenshot (1654).png>)
    > ![alt text](<assets/Screenshot (1655).png>)
    > ![alt text](<assets/Screenshot (1656).png>)
    > ![alt text](<assets/Screenshot (1657).png>)
    > ![alt text](<assets/Screenshot (1658).png>)
    > ![alt text](<assets/Screenshot (1659).png>)
    > ![alt text](<assets/Screenshot (1660).png>)
    > ![alt text](<assets/Screenshot (1661).png>)

5. Tambahkan config anti spam
    > ![alt text](<assets/Screenshot (1662).png>)


### F. Install DOVECOT (IMAP POP3)

1. Gunakan Perintah berikut untuk installasi `sudo  apt -y install dovecot-core dovecot-pop3d dovecot-imapd`

    > ![alt text](<assets/Screenshot 2024-04-14 040547.png>)


2. Ubah listen IP
    > ![alt text](<assets/Screenshot (1664).png>)

3. Setting file auth   

    > ![alt text](<assets/Screenshot (1663).png>)

4. Konfigurasi file mail

    > ![alt text](<assets/Screenshot (1665).png>)

5. Terakhir tambahkan mode 0666, dan user,group postfix pada file master

    > ![alt text](<assets/Screenshot (1666).png>)

6. Restart service, dan cek di netstat

    > ![alt text](<assets/Screenshot (1668).png>)




### G. DEBIAN EVOLUTION

1. Buat User Terlebih dahulu disini kita buat user default kita di saya yaitu
``user``

    > Identitiy : username@mail.kelompok2.local

    > Recieve ( Port 993 )

    > Sending ( Port 25 )

1. user telah dibuat sekarang buat user lagi (dummy) untuk saya, ``ali`` dengan langkah yang sama. adduser terlebih dahulu
    > ![alt text](<assets/Screenshot (1672).png>)

2. Mengirim pesan

    > ![alt text](assets/image-9.png)

3. cek Inbox user `ali`





### H. ROUNDCUBE

1. Sebelum itu kita perlu melakukan Konfigurasi untuk user roundcube, tambahkan pada tabel db user

    > ![alt text](assets/image-12.png)

2. Berikan full access

    > ![alt text](assets/image-13.png)
    
    Load
    > ![alt text](assets/image-14.png)

3. Install Roundcube paket dengan perintah berikut

    > ![alt text](assets/image-15.png)

4. Pilih Yes
    > ![alt text](assets/image-16.png)

5. Masukkan password tadi ( 123 )

    > ![alt text](assets/image-17.png)

6. Lakukan config pada file `/etc/roundcube/config.inc.php`

7. Samakan dengan config berikut
    > ![alt text](assets/image-19.png)
8. Kemudian konfigurasi file apache pada roundcube, uncomment line 3 dan hapus public_html path

    > ![alt text](assets/image-20.png)

9. pada apache2 default conf tambahkan Servername untuk mail dan document root menjadi roundcube ``sudo nano /etc/apache2/sites-available/000-default.conf``, Servername mail.kelompok2.local DocumentRoot /var/lib/roundcube/
    
    > ![alt text](assets/image-21.png)

10. jalankan rekonfigurasi seperti berikut

    > ![alt text](assets/image-22.png)
    
    Ok

    > ![alt text](assets/image-24.png)

    en_Us

    > ![alt text](assets/image-25.png)

    Pilih Install ulang ( YES 
    
    > ![alt text](assets/image-26.png)

    Pilih TCP IP

    > ![alt text](assets/image-27.png)

    Pilih localhost

    > ![alt text](assets/image-28.png)

    Port 3306

    > ![alt text](assets/image-29.png)

    Pilih native password

    > ![alt text](assets/image-30.png)

    Database name default

    > ![alt text](assets/image-31.png)

    Username default

    > ![alt text](assets/image-32.png)

    Password 123

    > ![alt text](assets/image-33.png)

    Admin root

    > ![alt text](assets/image-34.png)

    Pilih webserver apache2

    > ![alt text](assets/image-35.png)

    Restart dan keep curently installed

11. Roundcube terinstall

    > ![alt text](assets/image-36.png)
