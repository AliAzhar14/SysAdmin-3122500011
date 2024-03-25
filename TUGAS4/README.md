# TUGAS 4

**Daftar Isi**
- [TUGAS 4](#tugas-4)
 [](#)
  - [1. Ekosistem Internet](#1-ekosistem-internet)
 [](#-1)
  - [2. Instalasi DNS Server dengan BIND9](#2-instalasi-dns-server-dengan-bind9)
#
## 1. Ekosistem Internet     
Rangkuman:

Internet telah berkembang pesat di seluruh dunia berkat beberapa faktor kunci:

1. **Kepemilikan Global Bersama**: Internet merupakan hasil dari kerja sama global yang melibatkan berbagai pihak dari seluruh dunia, tanpa adanya satu entitas tunggal yang mengendalikan seluruh infrastruktur.

2. **Pengembangan Standar Terbuka**: Adopsi standar terbuka memungkinkan berbagai perangkat dan sistem berkomunikasi satu sama lain secara efisien, memungkinkan interoperabilitas yang luas di seluruh ekosistem Internet.

3. **Proses Pengembangan Teknologi dan Kebijakan yang Dapat Diakses secara Bebas**: Proses pengembangan teknologi dan kebijakan yang terbuka dan dapat diakses oleh masyarakat memungkinkan partisipasi luas dan beragam dalam mengatur dan memperbaiki Internet.

Internet memiliki aspek teknis yang meliputi sistem routing, sistem penamaan (DNS), arsitektur, standar, penyedia layanan, dan registri Internet. Sistem routing memastikan transfer data yang efisien melalui jaringan yang terdiri dari berbagai penyedia layanan dan penyedia akses, dengan prinsip-prinsip seperti hot potato routing dan cold potato routing.

Sistem penamaan, terutama melalui Domain Name System (DNS), memungkinkan pengguna untuk mengakses situs web dengan menggunakan nama domain yang mudah diingat, dengan alamat IP yang tersembunyi di baliknya. DNS menggunakan hierarki dan mekanisme resolusi untuk menghubungkan nama domain dengan alamat IP yang sesuai.

Standarisasi dalam pengembangan teknologi Internet dipimpin oleh organisasi seperti Internet Engineering Task Force (IETF), yang bertujuan untuk meningkatkan kinerja dan interoperabilitas Internet melalui pembuatan dan pemeliharaan standar yang relevan.

Layanan Internet disediakan oleh berbagai penyedia, termasuk penyedia konten, penyedia akses, penyedia transit, dan titik pertukaran Internet (IXPs). Masing-masing memiliki peran yang berbeda dalam menyediakan infrastruktur dan konektivitas yang diperlukan untuk menjalankan Internet.

Registri Internet, seperti Regional Internet Registries (RIRs) untuk alamat IP dan Domain Name Registries untuk domain, mengatur dan mengalokasikan sumber daya kunci Internet seperti blok alamat IP dan nama domain.

Selain itu, terdapat juga entitas seperti Clearing Houses dan Internet Route Registries yang membantu dalam pertukaran informasi dan koordinasi antara operator jaringan.

Keterlibatan dan dukungan dari berbagai pihak melalui organisasi dan inisiatif seperti Internet Society sangat penting dalam menjaga dan meningkatkan keberlangsungan serta aksesibilitas Internet bagi semua orang di seluruh dunia.
#
## 2. Instalasi DNS Server dengan BIND9

Link Tutorial Youtube : https://youtu.be/I1Y9bcQ3zY8
1. lakukan instalasi bind9
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/1.png)
2. cek instalasi di /etc/bind
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/2.png)
3. cek konfigurasi utama bind di named.conf.
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/3.png)
4. Menambahkan ACL (access list), control, dan include 3 file.
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/4.png)
5. Buka named.conf.deafult-zones.
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/5.png)
6. Buka named.conf.option, mengisi provider dan listen-on. Listen ditambahkan sesuai kelompok masing-masing
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/6.png)
7. Buka named.conf.local, untuk mengset atau konfigurasi zone file. Melakukan pengubahan zone sesuai nama kelompok.
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/7.png)
8. Lakukan sudo named-checkconf untuk mengeck pesan error. jika tidak ada pesan error yang keluar itu berarti konfigurasi yang dilakukan telah benar.
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/11.png)
9. Pergi ke arah configuration zone file. 
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/9.png)
10. Masuk ke zone file pertama dan mengubah data di dalamnya.
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/10.png)
11. Masuk ke zone file kedua (.inv) untuk mengubah data seperti file sebelumnya.
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/12.png)
12. Jalankan sudo systemctl restart named untuk menjalankan sistem bind.
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/13.png)
13. Cek status bind apakah running atau tidak.
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/17.png)
14. Cek apakah port terbuka atau tidak.

15. Gunakan perintah dig.
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/16.png)
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/14.png)
16. Gunakan perintah nslookup.
#
![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS4/assets/15.png)
