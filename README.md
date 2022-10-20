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

Jika kalian masih merasa kesulitan dalam meng-install **Moodle**, terdapat cara alternatif yang lebih mudah dengan menggunakan layanan yang tersedia pada web-hosting provider. Dengan layanan tersebut kita hanya perlu satu kali klik untuk meng-install **Moodle**. Berikut langkah-langkah untuk melakukannya installasi menggunakan web-hosting provider.
1. Kita perlu mengunjungi web-hosting provider yang menyediakan script instalasi **moodle** otomatis, seperti [softaculous.](http://www.softaculous.com/apps/educational/Moodle) melalui _web-hosting _[infinityfree.](http://infinityfree.net/accounts)
2. Kunjungi link tersebut lalu buat akun _web-hosting_
![Screenshot (501)](https://user-images.githubusercontent.com/88269626/196848936-62a062a4-fc1a-490f-a07c-3d8922ee8beb.png)

3. Klik _web-hosting _yang telah dibuat
![Screenshot (502)](https://user-images.githubusercontent.com/88269626/196849119-9b9835f2-3a4d-4126-977d-faa8c83d5e3e.png)

4. Kemudian masuk ke bagian control panel dan pilih softaculous
![Screenshot (503)](https://user-images.githubusercontent.com/88269626/196849136-eccb87e1-dda1-403e-bf54-34260a03981b.png)

![Screenshot (504)](https://user-images.githubusercontent.com/88269626/196849142-dcb87dbe-92d9-48d9-bed2-41870da9b532.png)

5. Selanjutnya cari software moodle dan install
![Screenshot (506)](https://user-images.githubusercontent.com/88269626/196849209-14977e45-def5-41af-98b2-88d85dcc5f51.png)

6. Lalu pilih versi moodle dan masukkan data admin
![Screenshot (507)](https://user-images.githubusercontent.com/88269626/196849229-a59b2c15-be78-4fa8-adb0-053fb91eecb1.png)

![Screenshot (521)](https://user-images.githubusercontent.com/88269626/196849448-29ecb241-9465-4e2e-9eb3-37c493af973f.png)

7. Klik install hingga selesai
![Screenshot (509)](https://user-images.githubusercontent.com/88269626/196849269-ffbf80a6-8986-4625-b540-0bec2b863e8c.png)

![Screenshot (522)](https://user-images.githubusercontent.com/88269626/196849506-bda89b89-c274-4e27-81bd-cbee4d4826cd.png)

![Screenshot (510)](https://user-images.githubusercontent.com/88269626/196849323-0578c12a-b232-4f95-a4a8-a3eea703b8b0.png)

8. Setelah terinstall silahkan klik link yang telah dibuat
![Screenshot (511)](https://user-images.githubusercontent.com/88269626/196849358-fca5fb6d-56c9-48c5-92ff-bfdd955b2e9a.png)

9. Apabila terjadi error, perlu diatur data root dengan file manager
![Screenshot (524)](https://user-images.githubusercontent.com/88269626/196849416-e83120d4-1dc0-42f9-80ce-393ed0d69e18.png)

10. Kembali ke control panel
![Screenshot (525)](https://user-images.githubusercontent.com/88269626/196849543-e473282e-1549-4813-9663-15e4842725cf.png)

11. Buka Online File Manager dan membuka folder htdocs kemudian folder moodle
![Screenshot (526)](https://user-images.githubusercontent.com/88269626/196849688-5a932360-d9fc-409e-a5a6-b1cec692170c.png)

12. Kemudian buat folder baru datanyamoodle dan atur CHMOD dengan write semua

![Screenshot (528)](https://user-images.githubusercontent.com/88269626/196849744-c4061b27-0f7f-45d7-9eb8-ce97cfb38747.png)

![Screenshot (529)](https://user-images.githubusercontent.com/88269626/196849745-e7ec6fc1-cc07-47a4-97be-402d5567755a.png)

13. Selanjutnya buka file config.php kemudian edit
![Screenshot (530)](https://user-images.githubusercontent.com/88269626/196849764-16e9c9c8-0e66-469f-9220-b95586e99b47.png)

14. Ubah data root yang mengarahkan ke folder datanyamoodle yang telah dibuat
![Screenshot (531)](https://user-images.githubusercontent.com/88269626/196849786-171eb1c5-30e2-40d0-a80d-560dfd5b8a44.png)

![Screenshot (532)](https://user-images.githubusercontent.com/88269626/196849798-f3a97297-9271-48c1-8350-655ddb4871db.png)

15. Silahkan buka kembali link moodle yang telah dibuat
![Screenshot (533)](https://user-images.githubusercontent.com/88269626/196849806-8f23d6e5-2d7d-44f5-b650-222d839da30b.png)

# Cara Pemakaian
[`^ kembali ke atas ^`](#)

1. Buka link yang telah dibuat http://moodle-komdat-5.rf.gd/moodle/ atau http://34.128.93.120/
2. Klik log in dan masukkan data admin 
![Screenshot (538)](https://user-images.githubusercontent.com/88269626/196849850-3222ae6b-1116-4115-a68e-7843b68510ea.png)

3. Masuk ke bagian site home yang berfungsi untuk mengatur course yang digunakan
![Screenshot (540)](https://user-images.githubusercontent.com/88269626/196849896-760b36bb-faf9-4471-a816-e675a385f1a6.png)

4. Kemudian admin dapat menambahkan course baru 
![Screenshot (541)](https://user-images.githubusercontent.com/88269626/196849910-23dcb33d-87b4-4cae-bc7e-40fd693a2666.png)

5. Kemudian admin dapat memasukkan data course yang ingin ditambahkan berupa nama course, summary, gambar, dan sebagainya
![Screenshot (543)](https://user-images.githubusercontent.com/88269626/196849957-0a9bbdd2-2971-49d0-b845-3868c6786090.png)

6. Kemudian admin dapat membuka course yang telah dibuat 
![Screenshot (544)](https://user-images.githubusercontent.com/88269626/196849981-786d4dd9-14f6-43e0-ba36-5c0867c423a1.png)

7. Admin dapat menambahkan berkas pendukung course dengan menekan tombol Add an activity or resource
![Screenshot (545)](https://user-images.githubusercontent.com/88269626/196850000-776c5359-8b47-4c40-acbc-b49560678254.png)

8. Admin dapat memasukkan data dan berkas pendukung course
![Screenshot (546)](https://user-images.githubusercontent.com/88269626/196850028-aba5e7b8-e0a6-4a4a-8198-bf814ee72437.png)

9. Peserta/admin dapat mengakses berkas pendukung
![Screenshot (547)](https://user-images.githubusercontent.com/88269626/196850044-ff9b0495-c6cf-4641-a8c9-fb4e46442b7d.png)

10. Selain itu juga, peserta/admin dapat melihat perkembangan belajar melalui dashboard
![Screenshot (548)](https://user-images.githubusercontent.com/88269626/196850065-eb4d4c04-a2fc-46e7-bcd7-90e53e92388a.png)

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
