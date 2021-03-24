<h1 align="center">
  <img src="https://user-images.githubusercontent.com/60166802/111296442-14087800-867f-11eb-85c0-6422e8fa8999.png" >
  <br>Ampache</br>
</h1>

# Sekilas Tentang

**Ampache** adalah Aplikasi streaming audio atau video berbasis web dan pengelolaan file yang memungkinkan penggunanya mengakses musik dan video dari mana saja. **Ampache** dapat digunakan oleh hampir semua perangkat yang terhubung jaringan internet.

# Instalasi
#### Kebutuhan Sistem :
- Unix, Linux atau Windows.
- Apache
- PHP7.40
- MySQL 5.x
- Composer

#### Proses Instalasi :

1. Pastikan seluruh paket sistem kita ter-*update*, dan install seluruh kebutuhan dasar sistem seperti `Apache`, `PHP`, dan `MySQL`. Kemudian install tools bantuan lainnya, yaitu `git` dan `composer` yang berguna dalam proses instalasi **Ampache**.
    ```
    $ sudo apt-get update
    $ sudo apt-get install apache2
    $ sudo apt-get install mysql-server
    $ sudo apt-get install php
    $ sudo apt-get install libapache2-mod-php
    $ sudo apt-get install php-mysql
    $ sudo apt-get install php-gd
    $ sudo apt-get install php-mcrypt
    $ sudo apt-get install php-mbstring
    $ sudo apt-get install php-xml
    $ sudo apt-get install php-ssh2
    $ sudo apt-get install php-curl
    $ sudo apt-get install php-zip
    $ sudo apt-get install php-intl
    $ sudo apt install git
    $ sudo apt install composer
    $ sudo service apache2 restart
    ```
2. Clone **Ampache** dengan Git ke dalam direktori `var/ww/html/` .
    ```
    $ sudo git clone https://github.com/ampache/ampache.git
    ```
3.  Masuk ke dalam direktori `var/www/html/ampache`yang merupakan hasil dari  clone, lalu ubah permission dari folder `config` menjadi 777 (semua *user* dapat mengakses, menulis dan menjalankan) agar composer dan ampache dapat mengakses serta merubah isi file yang terdapat di dalam folder tersebut
	```
	$ sudo chmod 777 -R config
	```



 4. Kembali ke root folder ampache kemudian lakukan instalasi *dependency* yang diperlukan oleh  **ampache** agar dapat berjalan di server dengan bantuan composer
	```
	$ sudo composer install
	```

 5. Ubah otorisasi kepemilikan ke webserver yang berjalan (Apache2).
    ```
    //lakukan pada direktori /var/www/http untuk mengurangi resiko error
    $ sudo chown -R www-data:www-data ampache
    ```



6. Konfigurasi web server Apache agar **Ampache** dapat berjalan .
    ```
    $ sudo a2enmod rewrite
    $ sudo nano /etc/apache2/apache2.conf
	```
	Pada file `/etc/apache2/apache2.conf`, ubah `AllowOverride none` menjadi `AllowOverrie All`  pada bagian
	```
	<Directory /var/www/>
	        Options Indexes FollowSymLinks
	        AllowOverride None
	        Require all granted
	</Directory>
    ```
    Menjadi
    ```
	<Directory /var/www/>
	        Options Indexes FollowSymLinks
	        AllowOverride All
	        Require all granted
	</Directory>
    ```
	Kemudian lakukan restart Apache
	```
	sudo service apache2 restart
	```

7. Mengubah maksimal ukuran file yang bisa di upload oleh apache.
  Edit file `etc/php/7.0/apache2/php.ini` dan ubah baris kode yang bersesuaian menjadi baris kode berikut :
    ```
    upload_max_filesize = 300M
    post_max_size = 300M
    ```

8. Restart kembali Apache web server.
    ```
    $ sudo service apache2 restart
    ```

9. Buka halaman IP web server yang kita gunakan di browser dan akses folder dimana kita melakukan instalasi **Ampache** .
	(Misal jika menggunakan IP localhost) : ``http://localhost/ampache/public/install.php``

    - Pilih bahasa yang akan digunakan selama penginstallan
      ![1](https://raw.githubusercontent.com/wiki/ampache/ampache/images/ampache_installation_01.png)

    - Kemudian akan muncul halaman untuk melakukan pengecekan apakah seluruh *requirements* sudah terpenuhi

      ![2](https://i.pinimg.com/originals/7c/a8/e8/7ca8e8ccb01f01a561241e8e09f16eed.png)

    - Jika *requirements* sudah terpenuhi, maka seluruh status akan mengembalikan Nilai **OK**

      ![3](https://i.pinimg.com/originals/ce/64/91/ce64917e2617e8623d6176943a4f65dc.png)

    - Konfigurasi database yang akan digunakan oleh **Ampache**

      ![4](https://i.pinimg.com/originals/65/94/91/659491e8b7cca85cb44eff7cb46910c4.png)

    - Konfigurasi pembuatan *config file*

      ![5](https://i.pinimg.com/originals/94/e1/56/94e156de32e99c67bc92657649d3c577.png)

![6](https://i.pinimg.com/originals/9e/58/67/9e58676b4fbf301012a569c167de99ea.png)

![7](https://i.pinimg.com/originals/37/91/7d/37917dffa04b701c2a6c2d37c47e69bc.png)

Pada tabs *file insight*, dapat dilihat error-error seperti di gambar di bawah. Jika semua instalasi telah dilakukan dengan benar, ketika tombol *create config* diklik, maka file konfigurasi akan langsung tersimpan dan semua error tersebut akan teratasi.
![8](https://user-images.githubusercontent.com/60166802/111440967-6f973c00-8739-11eb-82bd-9787da5f00bb.jpeg)

  10. Membuat *user account* untuk *administrator*

   ![9](https://i.pinimg.com/originals/f0/f2/6a/f0f26a01c4efdb156f52fa6874e7cf52.png)

11. Setelah proses instalasi selesai, akan tampil halaman informasi versi dari Ampache, dan informasi update. Apabila ampache yang terinstall adalah versi terbaru dari github, maka tidak perlu dilakukan update.
    ![10](https://i.pinimg.com/originals/d3/f5/19/d3f519f844e2e1b444f742c7e883154b.png)
	Tombol update now hanya akan menampilkan bahwa ampache telah berada dalam versi yang terbaru.
12. Login ke dalam **Ampache** dengan menggunakan akun administrator yang telah dibuat sebelumnya.
	![11](https://i.pinimg.com/originals/93/59/f9/9359f99e0d8b61054df058761485aa02.png)

	**Ampache** telah berhasil terinstall
	![12](https://i.pinimg.com/originals/d0/a1/09/d0a109b5572d4715fb93b4de9d299934.png)

# Cara Pemakaian

1. Sebelum menggunakan Ampache, pertama lakukanlah Login pada halaman awal dengan menggunakan akun yang sudah tersedia:
![11](https://user-images.githubusercontent.com/60166802/111445921-73798d00-873e-11eb-965b-7b9bdc7b3f3f.PNG)
Hubungi Admin jika anda belum terdaftar dan ingin mendaftar ke ampache.
2. Pada halaman awal kita akan ditampilkan menu pilihan seperti gambar di bawah ini.
![](https://user-images.githubusercontent.com/60166802/111448642-35319d00-8741-11eb-9d42-4f3c80484cb0.PNG)
3. Pada deretan tombol menu, di bawah menu Music terdapat pemilihan kategori file musik berdasarkan artist, genre, album, year dan lainnya. Sebagai contoh, klik pilihan *Song titles*. ![](https://user-images.githubusercontent.com/60166802/111446001-84c29980-873e-11eb-8ee0-7b055568e705.PNG)
Akan ditampilkan lagu yang telah terdapat di dalam katalog di yang berada di server. Untuk memutar lagu hanya perlu klik tombol play yang terdapat di sebelah kiri dari judul lagu setelah kita *hover* mouse kita ke lagu tersebut.
4. Untuk Video dan Juga Stream Radio, bisa dilakukan dengan klik pada pilihan yang tersedia, namun layanan radio harus didaftarkan terlebih dahulu oleh admin atau pihak  berwenang yang lain.
5. Jika anda adalah seorang administrator (atau pihak lain yang diberikan akses untuk menambah katalog), anda dapat menambah katalog yang berisi direktori dimana anda menyimpan lagu di server anda pada  tab admin, lalu dibawah menu katalog, add a catalog seperti pada gambar di bawah ini.![enter image description here](https://user-images.githubusercontent.com/60166802/111446050-91df8880-873e-11eb-9e45-3d882a4a733f.PNG)
Masukan nama katalog, jenis katalog apakah local atau remote, setelah anda memilih, misalkan local akan tampil form untuk mengisi *path* dari tempat anda menyimpan lagu atau file lainnya di dalam server anda.
![enter image description here](https://user-images.githubusercontent.com/60166802/111446084-9ad05a00-873e-11eb-8f6a-c935932e8791.PNG)
Jika telah selesai memasukkan direktori di path, klik **Add catalog** untuk menyelesaikan proses penambahan katalog.
6. Lagu atau file media yang anda simpan kemudian akan di scan oleh **Ampache** lalu akan tampil ke dalam daftar musik atau media yang ada di ampache. Kemudian file tersebut langsung dapat diputar oleh user lain.

# Pembahasan
**Ampache** dalam kemampuan untuk mengakses seluruh perpustakaan musik dari jarak jauh dan digunakan menggunakan PHP,HTML5 dan MySQL.  <br>

Kelebihan: <br/>
- Mendukung untuk dimainkan secara lokal untuk VLC
- Multidevice di satu akun, dapat digunakan di banyak device berbeda dengan akun yang sama secara bersamaan.


Kekurangan: <br>
- Interfacenya kurang menarik
- Tidak memiliki pemutaran cepat
- Tidak ada fitur bookmark yang memungkinkan Anda melanjutkan dari tempat Anda tinggalkan.


# Referensi

1. [Github Official Installation Guide](https://github.com/ampache/ampache/wiki/Installation) - Ampache
