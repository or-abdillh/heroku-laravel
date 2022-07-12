# Heroku Laravel

## _Deploy Your Laravel With Heroku_ 🙌🏻

### About Heroku 
[Heroku](https://heroku.com)  adalah sebuah Platform As Service yang memungkinkan untuk melakukan build and run application di lingkungan cloud.

### Persiapan Lingkungan Pengembang
Pastikan telah memiliki akun heroku aktif, jika belum memiliki akun bisa daftar melalui tautan [berikut](http://heroku.com/login).

#### Install Node JS
Node js digunakan untuk melakukan instalasi package heroku melalui command line. Pengguna linux bisa menggunakan perintah ```$ sudo apt install nodejs-lts```
Khusus pengguna Windows dapat menggunakan file installer Node JS melalui tautan [berikut](https://nodejs.org/en/download/)

Instalasi git pada komputer akan secara otomatis menambahkan *NPM / Node Package Manager* pada komputer.

#### Instalasi Git
Git adalah sebuah version control system yang populer dan gratis yang digunakan untuk melakukan remote pada repository project pada platform heroku. Untuk pengguna linux dapat menggunakan perintah ```$ sudo apt install git```

Khusus penggunan Windows dapat menggunakan file installer pada tautan [berikut](https://git-scm.com/downloads)

Setelah terinstall pada komputer, lakukan konfigurasi awal pada git melalui beberapa perintah berikut :
```$ git config --global user.mail "yout@email"```
```$ git config --global user.name "your name"```

Instalasi git pada komputer akan secara otomatis menambahkan *Git Bash* pada komputer.

#### Instalasi Heroku CLI
Heroku memiliki tool berbasis CLI yang dapat digunakan dalam melakukan tahap deployment apkikasi ke dalam layanan Heroku dengan cepat dan mudah. Instalasi dapat digunakan melalui *NPM* dan *git bash* yang telah terinstall pada komputer.

Akses Git bash bisa melalui : _klik kanan home screen > Git Bash Here_
Gunakan perintah ```$ npm install -g heroku```

### Menggunakan Layanan Heroku
Layanan heroku memiliki limit 5 buah applikasi pada satu akun aktif. Untuk menggunakan layanan heroku pastikan memiliki akun aktif dan lakukan login terlebih dahulu ke website resmi heroku

Pada tampilan awal dashboard akun gunakan menu _new > crete app > fill your app name_

#### Tahap 1 : Deploy Application
Setelah applikasi baru telah dibuat pada Heroku , maka selanjutnya adalah melakukan deploy aplikasi local ke dalam layanan cloud heroku melalui Heroku CLI yang telah terinstall 

##### Login Heroku
Heroku CLI memerlukan akses autentikasi pada akun heroku aktif sebelum terhubung dengan layanan heroku. Akses Git Bash lalu gunakan perintah ```$ heroku login``` tunggu hingga browser otomatis terbuka dengan mencoba mengetikkan apa saja pada keyboard. Silahkan login menggunakan akun anda pada browser
##### 1.1 Navigasi Project
Pada langkah ini silahkan masuk ke dalam direktori project aplikasi laravel yang ingin di deploy ke layanan heroku
##### 1.2 Membuat fle konfigurasi
Sebelumnya pastikan bahwa window git bash sebelumnya tidak tertutup, lalu pada direktori project _klik kanan > git bash here_ lalu gunakan perintah ```$ echo web: vendor/bin/heroku-php-apache2 public/ > Procfile```
#### 1.3 Menggunakan git dalam tahap deployment
Setelah file konfigurasi selesai dibuat, lakukan beberapa perintah berikut ini :
```bash
$ git init
$ heroku git:remote -a nama-aplikasi-heroku
$ git add .
$ git commit -am "Push"
$ git push heroku master 
````
Tunggu beberapa saat hingga aplikasi berhasil di deploy dan secara otomatis aplikasi dapat diakses melalui ```http://nama-aplikasi-heroku.herokuapp.com```

#### Tahap 2 : Persiapan Koneksi Database
Sebelum lanjut pada tahap ini pastikan project di lokal komputer telah berjalan dengan baik dan memiliki file migration dan seeder untuk melakukan dumping data pada database
##### 2.1 Install Heroku Postgres
Pada tahap ini silahkan _klik icon persegi pada pojok kanan atas > elements > Heroku Postgress > Install Heroku Postgress > Fill Your App Name > Submit Order Form__
##### 2.2 Melihat Postgress Credentials
Setelah langkah 2.1 selesai maka selanjutnya _klik Heroku Postgress pada bagian bawah hingga terbuka tab baru > settings > view credentials__
Pada tahap ini akan diperlihatkan informasi mengenai konfigurasi koneksi database yang telah tersedia, mulai dari Hostname, Username, hingga password.
##### 2.4 Setup Environment Variable
Pada tahap ini melakukan konfigurasi pada environment variable pada server aplikasi. 
Kembali pada tab browser sebelum langkah 2.3 lalu pergi ke _settings > reveal config vars_
Pada halaman ini pada bagian bawah akan ditampilkan dua input text yaitu KEY dan VALUE yang harus diisi satu - satu.
###### Mengisi variable
key diisi _DB_CONNECTION_ dan value diisi _pgsql_  lalu klik _add_
Lakukan hal sama mulai dari DB_DATABASE, DB_USERNAME, DB_PASSWORD, DB_PORT yang mana untuk value pada masing - masing key harus menyesuaikan pada langkah 2.2

#### Tahap 3 : Dumping database
Pada direktori project akses git bash melalui cara yang sama pada point 1.2 lalu login ke dalam server aplikasi heroku menggunakan perintah ```$ heroku run bash``` tunggu proses hingga selesai lalu lakukan beberapa perintah berikut pada server :
```bash
$ php artisan migrate
$ php artisan db:seed
```
Jika file migration dan seeder tidak bermasalah maka dumping data pada database telah selesai dilakukan, namun jika terdapat error pada proses silahkan cek kemabali file miigration dan seeder pada project lokal di komputer.

#### Tahap 4 : Melakukan perubahan pada aplikasi
Heroku menggunakan layanan cloud dalam menyimpan project aplikasi, jadi pastikan antara project di local komputer dengan server heroku benar - benar saling sinkrron

Setiap kali melakukan perubahan pada project di local komputer maka lakukan beberapa perintah berikut : 
```bash
$ git add .
$ git commit -m "Update"
$ git push heroku master
```
Perintah diatas untuk melakukan sinkronisasi project lokal dengan server heroku

Last Edited on 12/07/2022
Created by [or.abdillh](http://github.com/or-abdillh)
