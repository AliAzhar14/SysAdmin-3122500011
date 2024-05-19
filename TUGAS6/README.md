## Perbedaan Web Server dan Web Browser

Server aplikasi dan server web memiliki peran yang mirip namun berbeda dalam beberapa aspek penting yang harus dipahami.

Server aplikasi tidak terbatas pada protokol HTTP saja. Mereka bisa bekerja dengan berbagai jenis program dan menyediakan fitur tambahan yang memperluas fungsionalitasnya. Server aplikasi juga mendukung transaksi, personalisasi, dan layanan pesan yang krusial bagi berbagai jenis situs web.

Sebaliknya, server web terutama berfungsi untuk menangani permintaan HTTP dan menampilkan halaman web. Meskipun server web juga dapat menyediakan fitur tambahan seperti caching dan pemrosesan permintaan dasar, fungsinya lebih terbatas dibandingkan server aplikasi.

Seringkali, situs web dan aplikasi memerlukan fitur yang tidak dapat disediakan oleh server web biasa. Oleh karena itu, kombinasi server web dan server aplikasi sering digunakan untuk memberikan hasil yang lebih baik. Server web menangani permintaan dasar dan menyediakan konten statis dengan efisien, sementara server aplikasi mengelola permintaan yang lebih kompleks dan dinamis.

Selain itu, server web sering menjadi bagian dari server aplikasi karena server web merupakan komponen penting dalam layanan yang disediakan oleh server aplikasi. Oleh karena itu, saat membicarakan server aplikasi, server web sering kali juga termasuk di dalamnya.

Saat pengguna mengetikkan URL di browser, server web menyajikan konten yang sama terlepas dari lokasi atau perangkat pengguna. Namun, halaman web dengan komponen adaptif biasanya didukung oleh teknologi lain selain server web.

Kesimpulannya, meskipun ada perbedaan signifikan antara server aplikasi dan server web, keduanya memainkan peran penting dalam menjaga situs web berjalan dengan lancar dan memberikan pengalaman pengguna yang optimal.


#### Containerized

Containerized adalah pendekatan dalam manajemen aplikasi dan lingkungan eksekusi yang memanfaatkan teknologi container untuk mengisolasi aplikasi dari lingkungan sekitarnya. Dalam konteks ini, aplikasi dan semua dependensinya, seperti perpustakaan dan konfigurasi sistem, dibungkus menjadi satu unit yang disebut container. Teknologi ini memungkinkan aplikasi untuk berjalan konsisten di berbagai lingkungan, dari pengembangan hingga produksi, tanpa perlu khawatir tentang perbedaan konfigurasi sistem atau ketergantungan yang hilang. Container biasanya lebih ringan dan lebih cepat dibandingkan dengan virtual machine karena mereka berbagi kernel sistem operasi host namun tetap memberikan isolasi yang kuat. Docker adalah salah satu platform paling populer untuk manajemen container, memungkinkan pengembang untuk membangun, mengirim, dan menjalankan aplikasi dalam container dengan mudah dan efisien. Dengan pendekatan containerized, proses pengembangan, pengujian, dan deployment menjadi lebih streamlined, portable, dan scalable.


## Containerized di Virtual Machine Box

Di praktik ini kami menggunakan Docker.

Docker adalah sebuah platform yang memfasilitasi pengembangan, pengiriman, dan menjalankan aplikasi dalam container. Container adalah unit yang membungkus aplikasi bersama dengan semua dependensinya, seperti library, runtime, dan konfigurasi, sehingga dapat berjalan secara konsisten di berbagai lingkungan. Docker menggunakan teknologi container untuk menyediakan isolasi yang ringan dan efisien dibandingkan dengan virtual machine (VM).

###### Pemasang Docker di Mesin Virtual Debian

1. Hapus Docker.io dan dependency bawaan dari debian.

        for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

2. Lakukan Update/Upgrade Repository dan tambahkan Docker Official GPG Keys

        sudo apt-get update
        sudo apt-get install ca-certificates curl
        sudo install -m 0755 -d /etc/apt/keyrings
        sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
        sudo chmod a+r /etc/apt/keyrings/docker.asc

3. Tambahkan Repository Apt Resources

        echo \
        "deb [arch=$(dpkg --print-architecture) signed-by=/etc apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
        $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
        sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
        sudo apt-get update

4. Install Docker

        sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

5. Jika Docker sudah terpasang, coba jalankan Hello World

        sudo docker run hello-world

    or

        sudo docker pull hello-world && docker run hello-world

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS6/assets/image-1.png)

    Sum

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS6/assets/image.png)    


###### Membuat Docker Image

1. Buat File dengan Konfigurasi Berikut Buat file bernama **Dockerfile**

    > Dockerfile

        from nginx:alpine

        COPY index.html /usr/share/nginx/html
        EXPOSE 80

        CMD ["nginx", "-g", "daemon off;"]

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS6/assets/image-2.png)

2. Build Ke dalam Docker **IMAGES**

            sudo docker build -t contoh .

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS6/assets/image-3.png)

    Jalankan Docker dengan Perintah

3. Jalankan **DOCKER IMAGES**

        sudo docker run -d -p 80:80 contoh


4. Berhasil!, akses port 80

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS6/assets/image-4.png)


## C. Apache2 + Dns Resolver + Docker Uptime Kuma Package

Sekarang kita akan coba buka salah satu running server dengan dns yang diresolve oleh named/bind9 kemudian kita gunakan apache2 untuk web servernya

1. Git Clone Uptime Kuma dahulu

        git clone https://github.com/louislam/uptime-kuma.git

        cd uptime-kuma

2. lalu Jalankan dengan cara berikut

        sudo docker compose up

    yang dimana akan melakukan eksekusi file compose.yaml

    cek running container

        sudo docker ps -a

    pastikan berjalan

3. kita cek pada port berjalan yaitu **3001**

    `localhost:3001`

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS6/assets/image-5.png)

###### Lalu Bagaimana jika menggunakan url `monitoring.kelompok2.local` ?

1. Konfigurasi file **/var/lib/bind/db.kelompok2.local**

    Tambahkan monitoring pada CNAME ns
    dan jangan lupa ubah version file + date

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS6/assets/image-6.png)

    `sudo sytemctl restart named`

2. Untuk melakukan pointing ke domain localhost kita, kita gunakan ReverseProxy pada Apache2 Kita ( a2enmod )

    Install Beberapa Package Berikut dengan menjalankan perintah berikut:

    `sudo a2enmod`

    Masukkan Package berikut
    `proxy proxy_ajp proxy_http rewrite deflate headers proxy_balancer proxy_connect proxy_html`

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS6/assets/ss.png)

3. Setelah itu kita lakukan Konfigurasi pada Apache2 Kita

    > /etc/apache2/sites-enabled/000-default.conf

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS6/assets/image-7.png)

    Tambahkan baris berikut untuk monitoring subdomain

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS6/assets/image-8.png)

    `sudo sytemctl restart apache2`

4. Cek pada web browser kita

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS6/assets/image-9.png)

    Berhasil

    ![hehe](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS6/assets/hehe.gif)