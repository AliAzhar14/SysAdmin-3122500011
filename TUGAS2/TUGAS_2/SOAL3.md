# 3. Setting Network

Ada 2 cara kita dapat melakukan setting network di debian yaitu dengan GUI ( NETWORK MANAGER ) dan CLI ( Menggunakan file /etc/network/interfaces)


Default Gateway :

![alt text](assets/image-jaringan5.png)

#### A. NETWORK MANAGER
- Buka Network Manager
- Buka setting pada interface terhubung/ sambungkan terlebih dahulu

![alt text](assets/image-jaringan.png)

- Pilih Menu IPV4 lalu klik manual, isi sesuai kolom

![alt text](assets/image-jaringan4.png)

- hasil

![alt text](assets/image-jaringan8.png)
#### B. Melalui interfaces File

- Jalankan Perintah

![alt text](assets/image-jaringan7.png)

- Setting seperti format berikut

![alt text](assets/image-jaringan6.png)

- lakukan ifdown ifup nama interface

![alt text](assets/image-jaringan9.png)

- hasil

![alt text](assets/image-jaringan10.png)

[sumber](https://wiki.debian.org/NetworkConfiguration#Starting_and_Stopping_Interfaces)