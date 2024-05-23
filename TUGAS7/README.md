# Tugas 7

Docker Labs 
https://labs.play-with-docker.com/

# Getting Started

install image

    docker run -d -p 80:80 dockersamples/101-tutorial

![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image.png)


# Our Application

1. Pertama-tama source code dapat diperoleh pada link berikut :
[DownloadZIP](http://ip172-18-0-94-cp0r4piim2rg00ao0lig-80.direct.labs.play-with-docker.com/assets/app.zip)
    or [Zip](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/app.zip)


    Setelah di download **Drag file zip tersebut** kedalam terminal lab docker. lakukan unzip file dan buat file `Dockerfile`

        unzip app.zip
        cd app
        touch Dockerfile
        vi Dockerfile


    Di dalam `Dockerfile` ketik konfigurasi basic berikut

        FROM node:10-alpine
        WORKDIR /app
        COPY . .
        RUN yarn install --production
        CMD ["node", "/app/src/index.js"]


1. Lakukan Build Images

        docker build -t docker-101 .

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-5.png)

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-1.png)

2. Run Images yang telah kita buat

        docker run -d -p 3000:3000 docker-101

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-2.png)

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-3.png)

    Kita cek pada link labs

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-4.png)
    

# Updating Our App

1. Buka /app/src/static/js/app.js gunakan editor dari labs

![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-6.png)

2. Build ulang Images karena kita melakukan perubahan pada source

        docker build -t docker-101 .

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-7.png)

3. Jalankan Images Lagi ( Akan Error karena terdapat instance dengan port yang sama sedang dijalankan )

        docker run -dp 3000:3000 docker-101

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-8.png)

4. Stop terlebih dahulu container dengan port `3000` kemudian hapus

        docker stop nama_container/id & docker rm nama_container/id

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-9.png)

5. jalankan ulang

        docker run -dp 3000:3000 docker-101

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-10.png)

    Sudah berubah

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-11.png)

    dan datanya hilang karena kita jalankan ulang! looks like factory mode

# Sharing our App


1. Buat Repository pada Hub Docker dengan nama repo `101-todo-app`

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-12.png)

2. Login Ke akun kita untuk push

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-17.png)

3. Push images dari Local ke dalam Docker HUB

        docker push aliazhar1234567/101-todo-app

4. Kita tag images tersebut ke aliazhar1234567/101-todo-app

        docker tag docker-101 aliazhar1234567/101-todo-app


5. Push tagged images

        docker push aliazhar1234567/101-todo-app

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-13.png)

6. Berhasil

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-19.png)



7. buat Instance baru dari Os labs

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-20.png)

    1. Run Images, ambil dari Hub karena tidak ada di lokal

            docker run -dp 3000:3000 aliazhar1234567/101-todo-app

        ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-23.png)



# Presisting Our DB

Kita buat 2 container

**Container Pertama**
1. buat sebuah Container dengan OS ubuntu dan buat sebuah file bernama file.txt yang melakukan generate random angka dari 1 hingga 10000

        docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"

    bash digunakan untuk melakukan eksekusi bash terminal didalam container.

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-25.png)

2. Ekseskusi perintah cat

        docker exec id cat /data.txt

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-26.png)


3. Run container lain

        docker run -it ubuntu ls /

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-27.png)

Secara default todo-app menyimpan pada sqlite database

kita lakukan mounting database ke app dengan membuat sebuah volume


1. Buat volume 

        docker volume create todo-db

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-29.png)

2. jalankan todo container dengan mounting volume yang kita buat

        docker run -dp 3000:3000 -v todo-db:/etc/todos docker-101

    disini saya pull dari hub saya

3. tambahakan beberapa data seblum di hapus container


4. Remove container


5. Start lagi! dan seharusnya data masih ada


6. setelah di hapus sebelumnya masih ada datanya

    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-34.png)

7. docker menyimpannya dalam sebuah directory



# Using Bind Mounts

presist data dapat disimpan kedalam volume, tetapi pada kasus tertentu kita harus tahu dimana letak dari data yang kita simpan, dengan `Bind Mounts` kita bisa mengatur letak dari data yang disimpan.

### Starting Dev-Mode Container

1. Hentikan semua docker-101 container
2. Run command berikut

        docker run -dp 3000:3000 \
        -w /app -v $PWD:/app \
        node:10-alpine \
        sh -c "yarn install && yarn run dev"


    penjelasan sama seperti contoh app diawal [here](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/#here)

3. kita lihat apa yang terjadi didalam container dengan melihat `logs` nya


4. Coba kita edit file didalamnya :D


    ![alt text](https://github.com/AliAzhar14/SysAdmin-3122500011/blob/main/TUGAS7/assets/image-39.png)

    sudah berubah


# Multi-Container Apps

Banyak perdebatan antara expert lebih baik `mysql database` di jadikan satu container atau dipisah, sebaiknya dipisah menjadi beda container. karena kita dapat melakukan scaling hanya pada app tertentu misal hanya databasenya!.

#### Starting Mysql

1. Buat Network 

        docker network create todo-app

2. Jalankan mysql server dengan beberapa setting untuk enviroment username dan password

        docker run -d \
            --network todo-app --network-alias mysql \
            -v todo-mysql-data:/var/lib/mysql \
            -e MYSQL_ROOT_PASSWORD=secret \
            -e MYSQL_DATABASE=todos \
            mysql:5.7

3. Mari kita coba mysql didalam containernya

        docker exec -it <mysql-container-id> mysql -p


#### Sambungkan Ke MYSQL

Pastinya mengakses sebuah database memerlukan IP, lalu apa IP dari Container tersebut?? mari gunakan container berikut.


1. install/pull `nicolaka/netshoot` container 

        docker run -it --network todo-app nicolaka/netshoot


2. kita cari tahu ipnya dengan perintah dig

3.  Simpan IP MYSQL

    172.18.0.2

    Apakah perlu kita menulis ip ini dalam env? tidak perlu! 
    Docker sudah otomatis melakukan resolve dns mysql sehingga kita cukup duduk santai :D


#### Running APP + Mysql

1. Run dengan command berikut tidak perlu ip spesifik

        docker run -dp 3000:3000 \
        -w /app -v $PWD:/app \
        --network todo-app \
        -e MYSQL_HOST=mysql \
        -e MYSQL_USER=root \
        -e MYSQL_PASSWORD=secret \
        -e MYSQL_DB=todos \
        node:10-alpine \
        sh -c "yarn install && yarn run dev"

2. cek log apakah berhasil dijalankan

    tambahkan item todo di web

3. Cek database

    Berhasil ditambahkan

# Using Docker Compose

Docker compose adalah sebuah alat berbentuk yml yang menyimpan configurasi dari sebuah container, bagusnya file ini menyimpan settingan install dengan single command.


1. cek compose version
    
        docker-compose version

2. Buat config sesuai isi berikut 

    disini tambahkan untuk webservernya

        version: "3.7"

        services:
          app:
            image: node:10-alpine
            command: sh -c "yarn install && yarn run dev"
            ports:
            - 3000:3000
            working_dir: /app
            volumes:
            - ./:/app
            environment:
            MYSQL_HOST: mysql
            MYSQL_USER: root
            MYSQL_PASSWORD: secret
            MYSQL_DB: todos

    `app` berisi `image`, `command` yang dijalankan  beserta running `ports` lalu `working directory` serta `volumes mount` yang dipakai
    `enviroment` tambahkan env dari mysql

3. tambahkan service Database untuk mysql

        mysql:
          image: mysql:5.7
        volumes:
          - todo-mysql-data:/var/lib/mysql
        environment: 
          MYSQL_ROOT_PASSWORD: secret
          MYSQL_DATABASE: todos

    `mysql` mendefiniskan nama service
    Tambahkan mysql s
    ebagai images yang akan digunakan pada bagian image
    `volumes`: berisi directory tempat menyimpan mysql
    `env`: pastikan sama dengan yang ada ada enviroment **app**


    tambahkan volumes

        volumes:
            todo-mysql-data:


4. Coba compose up
    pastikan app dan db sama dimatikan, lalu ketik

        docker compose up -d

5. cek logs


# Image Building Best Practices

#### Image Layering
Tahukah kita bahwa kita dapat melihat apa yang membentuk sebuah image? Dengan menggunakan perintah docker image history, kita dapat melihat perintah yang digunakan untuk membuat setiap lapisan dalam sebuah image.


1. Lihat history docker images

        docker image history <nama-image>

    full output


#### Layer Caching

Sekarang setelah kita melihat cara kerja pelapisan, ada pelajaran penting yang perlu dipelajari untuk membantu meningkatkan waktu pembuatan image container kita.


1. tambahkan config tambahan pada Dockerfile

        FROM node:10-alpine
        WORKDIR /app
        COPY package.json yarn.lock ./
        RUN yarn install --production
        COPY . .
        CMD ["node", "/app/src/index.js"]

2. Mari Kita build cek build log

3. edit satu file dan build lagi liat lognya

    disini karena kita hanya mengubah 1 file yang tidak banyak maka dia akan menggunakan **CACHE**  


#### Multi-Stage Builds

Pisahkan dependensi waktu build dari dependensi waktu proses
Kurangi ukuran Image secara keseluruhan dengan hanya mengirimkan apa yang diperlukan aplikasi Anda untuk berjalan

Maven/Tomcat Example

        FROM maven AS build
        WORKDIR /app
        COPY . .
        RUN mvn package

        FROM tomcat
        COPY --from=build /app/target/file.war /usr/local/tomcat/webapps 

React

        FROM node:10 AS build
        WORKDIR /app
        COPY package* yarn.lock ./
        RUN yarn install
        COPY public ./public
        COPY src ./src
        RUN yarn run build

        FROM nginx:alpine
        COPY --from=build /app/build /usr/share/nginx/html




