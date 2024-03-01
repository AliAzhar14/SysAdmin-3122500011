# DAFTAR TUGAS AKAN SAYA TAMPILKAN PADA BAGIAN INI
| TUGAS | FILE |
| ------| -----|
| [TUGAS 1](https://github.com/Reza1290/SysAdmin-3122500024/blob/main/TUGAS1.md) |  _[FILE](https://github.com/Reza1290/SysAdmin-3122500024/blob/main/TUGAS1.md)_ |
| [TUGAS 2](#tugas-2) | _[FILE](https://github.com/Reza1290/SysAdmin-3122500024/blob/main/TUGAS_2/README.md)_ , _[MARP CLICK](TUGAS_2/PPT_SYSADMIN.md)_, _[PDF MARP](TUGAS_2/PPT_SYSADMIN.pdf)_|

# KELOMPOK 2

| NAMA | NRP |
| ---- | --- |
| [MUHAMAD REZA MUKTASIB](https://github.com/Reza1290)| 3122500024 |
| [AWAL RAYA](https://github.com/abirey)| 3122500012 |
| [ALI AZHAR P.B](https://github.com/AliAzhar14)| 3122500011 |

-------

# TUGAS 2

**DAFTAR ISI**

- [SOAL 1](#1-linux-directory-structure)
- [SOAL 2](TUGAS_2/PPT_SYSADMIN.md)
- [SOAL 3](#3-setting-network)


## 1. Linux Directory Structure


Berdasarkan referensi https://www.debianadmin.com/linux-directory-structure-overview.html, struktur direktori di Linux berbeda dengan di Windows. Struktur Direktori mengikuti aturan **Filesystem Hierarchy Structure (FHS)** yang diatur oleh Free Standard Group meskipun saat pendistribusian terkadang cenderung menyimpang dari standar.

Direktori-direktori yang berbeda antara lain.

1. **`/root`**
   
    > Struktur direktori dimulai dari root file system yang menjadi root direktori untuk seluruh struktur. Partisi ini akan disimpan di UNIX atau Unix-compatible system.

2. **`/boot`**

    > Direktori ini mengandung file boot loader termasuk Grub atau Lilo, Kernel, initrd dan file konfigurasi system.map.

3. **`/sys`**
	
    >Direktori ini terdapat Kernel, Filmware dan file system lainnya yang terkait.

4. **`/sbin`**
	
    >Direktori ini mengandung sistem binari yang penting dan alat sistem administrasi yang penting untuk sistem operasi dan performa/kinerja.

5. **`/bin`**

	> Direktori ini mengandung binari-binari yang penting untuk pengguna dan utilitas tersebut dibutuhkan di mode user tunggal. Contohnya, termasuk cat, ls, cp, dan lainnya.

6. **`/lib`**

	> Direktori ini mengandung file library/pustaka untuk semua binari yang disimpan di direktori /bin dan /sbin.

7. **`/dev`**

	> Direktori ini mengandung sistem file dan driver yang penting.

8. **`/etc`**

	> Direktori ini mengandung file sistem konfigurasi yang penting termasuk /etc/hosts, /etc/resolv.conf, nsswicth.conf, default dan file konfigurasi network. Kebanyakan adalah sistem host spesifik dan file konfigurasi aplikasi.

9. **`/home`**

	> Semua pengguna direktori home disimpan di dalam direktori ini dengan pengecualian direktori root home yang disimpan di dalam /root. DIrektori ini terdapat file pengguna dan setting personal.

10. **`/media`**

	> Direktori umum yang diperuntukkan sebagai tempat media yang bisa dilepas seperti CD-ROM, USB, Floppies, dan lainnya.

11. **`/mnt`**

	> Direktori umum yang diperuntukkan untuk file sistem sementara. Hal ini sangat berguna ketika melakukan troubleshoot dari CD-ROM dan lainnyayang dimana mungkin dibutuhkan sistem file root dan mengedit konfigurasi.

12. **`/opt`**

	> Direktori yang jaarang digunakan untuk Optional Software Package. Ini secara ekstensif digunakan di sistem operasi UNIX seperti Sun Solaris di mana paket perangkat lunak diinstal.

13. **`/usr`**

	> Sub hierarki menuju file sistem root yang merupakan direktori data pengguna. Mengandung utilitas spesifik pengguna dan aplikasi. Terdapat juga banyak file sistem yang penting tetapi juga tidak sebegitu penting (important but not critical) yang dipasang. Akan ditemukan kembali direktori bin, sbin, dan lib yang mengandung pengguna non-critical dan binari sistem dan pustaka yang terkait dan direktori yang dibagikan. Terdapat juga direktori dengan file didalamnya.

14. **`/usr/sbin`**

	> Direktori ini mengandung sistem binari dan utilitas jaringan yang non-essential non-critical.

15. **`/usr/bin`**

	> Direktori ini mengandung binari command/perintah untuk pengguna yang non-essential non-critical.

16. **`/usr/lib`**

	> File pustaka untuk binari di direktori /usr/bin dan  /usr/sbin.

17. **`/usr/share`**

	> Platform independen untuk direktori data yang dibagi(shared).

18. **`/usr/local`**

	> Sub hierarki di bawah dari direktori /usr yang memiliki sistem lokal data spesifik termasuk pengguna dan sistem binari serta pustakanya.

19. **`/var`**

	> Direktori ini sebagian besar dipasang sebagai filesystem yang terpisah di bawah root di mana semua kandungan variabel sepeti logs, file spool untuk printer, crontab, ji jobs, mail, proses yang berjalan, mengunci file yang lainnya. Dibutuhkan pemeliharaan untuk perencanaan file sistem ini dan pemeliharaan seperti ini akan memenuhi dengan cepat dan ketika filesystem penuh akan mengakiban permasalahan operasional di sistem dan aplikasi.

20. **`/tmp`**

	> Sistem file sementara yang menyimpan file sementara yang dibersihkan di sistem reboot. Terdapat juga direktori /var/tmp yang menyimpan file sementara juga. Satu-satunya perbedaan keduanya yaitu di direktori /var/tmp menyimpan file yang diproteksi di sistem reboot. Dengan kata lain, direktori tersebut tidak terhapus/hilang saat reboot.

    
21. **`/proc`**
    > Kemudian terdapat vrtual file sistem /proc yang berada di memori dan dipasang di bawah root penahan kernel dan statistik proses di format file teks.


### LINUX DIRECTORY STRUCTURE Visual View

Berikut adalah gambar visual dalam bentuk tree dari directory root

![alt text](<TUGAS_2/assets/WhatsApp Image 2024-02-26 at 14.17.51_912ab718.jpg>)

![alt text](TUGAS_2/assets/linuk.png)


# 2. [MARP CLICK](TUGAS_2/PPT_SYSADMIN.md)
# 3. Setting Network

Ada 2 cara kita dapat melakukan setting network di debian yaitu dengan GUI ( NETWORK MANAGER ) dan CLI ( Menggunakan file /etc/network/interfaces)


Default Gateway :

![alt text](TUGAS_2/assets/image-jaringan5.png)

#### A. NETWORK MANAGER
- Buka Network Manager
- Buka setting pada interface terhubung/ sambungkan terlebih dahulu

![alt text](TUGAS_2/assets/image-jaringan.png)

- Pilih Menu IPV4 lalu klik manual, isi sesuai kolom

![alt text](TUGAS_2/assets/image-jaringan4.png)

- hasil

![alt text](TUGAS_2/assets/image-jaringan8.png)
#### B. Melalui interfaces File

- Jalankan Perintah

![alt text](TUGAS_2/assets/image-jaringan7.png)

- Setting seperti format berikut

![alt text](TUGAS_2/assets/image-jaringan6.png)

- lakukan ifdown ifup nama interface

![alt text](TUGAS_2/assets/image-jaringan9.png)

- hasil

![alt text](TUGAS_2/assets/image-jaringan10.png)

[sumber](https://wiki.debian.org/NetworkConfiguration#Starting_and_Stopping_Interfaces)