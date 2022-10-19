<h1 align="center"><img src="https://i.ibb.co/1Z3NRzz/kisspng-moodle-logo-learning-management-system-5b648cf3b74b53-8737104215333163397508.png"></h1>

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:|:---:

# Sekilas Tentang
[`^ kembali ke atas ^`](#)

**MOODLE** (singkatan dari ***Modular Object-Oriented Dynamic Learning Environment***) adalah paket perangkat lunak yang diproduksi untuk kegiatan belajar berbasis internet dan situs web yang menggunakan prinsip ***social constructionist pedagogy***. MOODLE merupakan salah satu aplikasi dari konsep dan mekanisme belajar mengajar yang memanfaatkan teknologi informasi, yang dikenal dengan konsep pembelajaran elektronik atau e-learning. **MOODLE** dirancang untuk memberikan pendidik, administrator, dan siswa dengan satu sistem yang kuat, aman dan terintegrasi untuk menciptakan lingkungan belajar yang dipersonalisasi.

**MOODLE** dapat digunakan secara bebas sebagai produk sumber terbuka (*open source*) di bawah lisensi GNU. Moodle dapat diinstal di komputer dan sistem operasi apapun yang bisa menjalankan `PHP` dan mendukung database `SQL`. **MOODLE** awalnya dikembangkan oleh **Martin Dougiamas** dengan tujuan membantu pendidik membuat kursus online dan fokus pada interaksi dan konstruksi kolaboratif konten yang dirilis pada 20 Agustus 2002 menjadi versi pertama. Hingga saat ini, ratusan juta orang di ribuan institusi dan organisasi pendidikan di seluruh dunia menggunakan **MOODLE** sebagai kotak peralatan untuk mengelola pembelajaran online mereka.

# Instalasi
[`^ kembali ke atas ^`](#)

#### Kebutuhan Sistem :
- **Sistem operasi Cloud VPS:** Unix, Linux atau Windows.
- **Web Server:** Apache.
- **Database:** MySQL 5.7+.
- **Bahasa Pemrograman Web:** PHP 7.3.

#### Proses Instalasi :
1. Login Kedalam Server 
Disini kami menggunakan VM Instance dari Google Cloud dan connect ke SSH melalui console yang telah disediakan.

2. Install LAMPP
LAMPP adalah singkatan dari Linux, Apache, MySQL, PHP & phpMyAdmin. Untuk membangun sebuah website diperlukan sistem operasi server, web server, database dan bahasa pemrograman web (PHP).
```
# update repository
sudo apt update
# instalasi Apache
sudo apt install apache2
# instalasi MySQL
sudo apt install mysql-server
# instalasi PHP
sudo apt install php php-intl php-soap php-xmlrpc
# instalasi phpMyAdmin (untuk mempermudah pengelolaan database)
sudo apt install phpmyadmin
``` 

3. Download file Moodle
```
# pindah ke folder /var/www/html
cd /var/www/html

# clone file moodle
sudo apt install git
sudo git clone git://git.moodle.org/moodle.git
```

4. Buat data direktori untuk Moodle
```
sudo mkdir /var/www/html/moodledata

# berikan akses kepada folder
sudo chown -R www-data:www-data /var/www/html/moodle/ 
sudo chmod -R 755 /var/www/html/moodle/
sudo chown www-data /var/www/html/moodledata
```

5. Sinkronisasi Domain dengan Konfigurasi Apache
```
# membuat konfigurasi baru
sudo touch /etc/apache2/sites-available/moodle.conf
# membuat link untuk file konfigurasi di folder sites-enable
sudo ln -s /etc/apache2/sites-available/moodle.conf /etc/apache2/sites-enabled/moodle.conf
# edit file konfigurasi
sudo nano /etc/apache2/sites-available/moodle.conf
```

Masukan kode berikut pada file konfigurasi
```
<VirtualHost *:80>

DocumentRoot /var/www/html/moodle/ 

ServerName kelasonline.websitesaya.net
ServerAlias www.kelasonline.websitesaya.net
 
<Directory /var/www/html/moodle/>
 
Options +FollowSymlinks 
AllowOverride All
Require all granted

</Directory>
 

ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
 
</VirtualHost>
```

# Konfigurasi
[`^ kembali ke atas ^`](#)

Setting server tambahan yang diperlukan untuk meningkatkan fungsi dan kinerja aplikasi, misalnya:
- batas upload file
- batas memori
- dll

Plugin untuk fungsi tambahan
- login dengan Google/Facebook
- editor Markdown
- dll

# Maintenance
[`^ kembali ke atas ^`](#)  

Setting tambahan untuk maintenance secara periodik, misalnya:
- buat backup database tiap pekan
- hapus direktori sampah tiap hari
- dll

# Otomatisasi
[`^ kembali ke atas ^`](#)

Skrip shell untuk otomatisasi instalasi, konfigurasi, dan maintenance.

# Cara Pemakaian
[`^ kembali ke atas ^`](#)

- Tampilan aplikasi web
- Fungsi-fungsi utama
- Isi dengan data real/dummy (jangan kosongan) dan sertakan beberapa screenshot

# Pembahasan
[`^ kembali ke atas ^`](#)

- Pendapat anda tentang aplikasi web ini
    - kelebihan
    - kekurangan
- Bandingkan dengan aplikasi web lain yang sejenis

# Referensi
[`^ kembali ke atas ^`](#)

1. [About Moodle](https://en.wikipedia.org/wiki/Moodle) - Moodle
2. [Profile Moodle](https://moodle.com/about/) - Profile Moodle
