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
**1. Login Kedalam Server**

Disini kami menggunakan VM Instance dari Google Cloud dan connect ke SSH melalui console yang telah disediakan.

**2. Install LAMPP**

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

**3. Download file Moodle**
```
# pindah ke folder /var/www/html
cd /var/www/html

# clone file moodle
sudo apt install git
sudo git clone git://git.moodle.org/moodle.git
```

**4. Buat data direktori untuk Moodle**
```
sudo mkdir /var/www/html/moodledata

# berikan akses kepada folder
sudo chown -R www-data:www-data /var/www/html/moodle/ 
sudo chmod -R 755 /var/www/html/moodle/
sudo chown www-data /var/www/html/moodledata
```

**5. Sinkronisasi Domain dengan Konfigurasi Apache**
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

ServerName your-domain.com
ServerAlias www.your-domain.com
 
<Directory /var/www/html/moodle/>
 
Options +FollowSymlinks 
AllowOverride All
Require all granted

</Directory>
 

ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
 
</VirtualHost>
```
restart kembali apache
```
sudo systemctl restart apache2
```

**6. Membuat Database Moodle**

Akses phpMyAdmin dengan menulis ip_address/phpmyadmin pada web browser dan login menggunakan akun root. Kemudian klik tab menu database . Pada bagian `Create database`, silahkan buat database dengan nama yang diinginkan.
![image](https://user-images.githubusercontent.com/81523117/196926716-ac2f978c-a580-4c28-91f2-9bc75c3fcdc2.png)
![image](https://user-images.githubusercontent.com/81523117/196927476-fb56d28b-acad-4d58-a2ba-4f3e187e4c7d.png)


**7. Melakukan Instalasi Moodle**

Untuk melakukan instalasi Moodle, silahkan akses domain atau ip_addres di web browser. 
- Pilih bahasa yang akan digunakan
![image](https://user-images.githubusercontent.com/81523117/196928465-62741332-b648-43a1-95b9-515b4749a9e9.png)

- Sesuaikan web addres, direktori Moodle, dan direktori data Moodle
![image](https://user-images.githubusercontent.com/81523117/196928644-c5cd35e0-0cd9-41f2-8108-61d21dae28c4.png)

- Pilih tipe database yang digunakan, silahkan pilih `Improved MySQL`
![image](https://user-images.githubusercontent.com/81523117/196928772-a200f996-1659-41dd-a995-d8b278da98d8.png)

- Sesuaikan konfigurasi database
![image](https://user-images.githubusercontent.com/81523117/196929808-1a2fa626-c8d0-4a3b-aacd-101bd2d58aec.png)

- Persetujuan lisensi Moodle
![image](https://user-images.githubusercontent.com/81523117/196934746-160c51c7-a4fa-495b-bc0f-422480763587.png)

- Pengecekan persyaratan & Instalasi Moodle

Pastikan pada bagian plugin status sudah OK semua ya. Jika belum berstatus OK, maka dapat dipastikan proses instalasi gagal. Jika sudah OK, klik 'continue'
![image](https://user-images.githubusercontent.com/81523117/196935147-2923af04-c6c7-47da-a817-424cead275f1.png)

Tunggu hingga proses instalasi selesai dan klik 'continue'
![image](https://user-images.githubusercontent.com/81523117/196936068-d7191d3e-43be-4c8e-92bc-2eb784a63b8b.png)

8. Mengatur Username dan Password Admin
![image](https://user-images.githubusercontent.com/81523117/196936376-aec7c362-4f1d-41d1-8859-cb51b94cd143.png)

9. Mengatur tampilan kelas online
![image](https://user-images.githubusercontent.com/81523117/196937017-bb0bc103-3780-4c32-823a-cf3f25041ca3.png)

10. Akses website pada web browser

Untuk mengakses dapat menggunakan alamat ip atau domain yang digunakan untuk hosting Moodle. Akan muncul tampilan berikut yang merupakan halaman dashboard dari administrator.
![image](https://user-images.githubusercontent.com/81523117/196937319-797ec6b9-cd4e-455e-b63d-b268ce109b6d.png)


# Konfigurasi
[`^ kembali ke atas ^`](#)

Untuk konfigurasi aplikasi Moodle dapat dilakukan melalui bagian `site administration`
disitu kita dapat melakukan setting tambahan yang diperlukan untuk meningkatkan fungsi dan kinerja aplikasi, misalnya:
- batas upload file
![image](https://user-images.githubusercontent.com/81523117/196945644-83ee4cf6-1896-48d0-b89c-2edc48ab673d.png)

- batas memori
![image](https://user-images.githubusercontent.com/81523117/196945731-b6545b00-1fdc-4ae2-8db7-a424d2df0e25.png)

- install plugin
![image](https://user-images.githubusercontent.com/81523117/196945811-f51a44b3-9488-4327-99dc-e80ed40cdf50.png)

- atur tema
![image](https://user-images.githubusercontent.com/81523117/196945846-34cee2f4-8d4a-4e37-ab7a-d5dc3b8e98f6.png)

- dll

![image](https://user-images.githubusercontent.com/81523117/196942113-d9a26569-9c1d-4f0e-8351-1c3487742e6c.png)

untuk mempermudah mencari konfigurasi, kita dapat memanfaatkan tombol search yang telah disediakan


# Maintenance
[`^ kembali ke atas ^`](#)  

Ketika kita ingin memodifikasi aplikasi yang sudah terinstall, kita mungkin tidak ingin ada orang lain yang membuka aplikasi kita. Pada saat seperti itu, kita dapat mengkonfigurasi aplikasi kita untuk masuk ke dalam *maintenance mode*. Berikut ini adalah langkah-langkah yang harus kita lakukan :
1. Login ke dalam akun admin
2. Masuk ke submenu `Site administration` -> `server`
3. Pilih `maintenance mode` pada bagian maintenance
![image](https://user-images.githubusercontent.com/81523117/196943862-5a400edf-524f-40e2-b280-5c385f59161a.png)
5. Enable `maintenance mode` dan isi pesan yang ingin ditampilkan apabila ada yang mengakses aplikasi saat sedang maintenance. Lalu simpan perubahan 
![image](https://user-images.githubusercontent.com/81523117/196944027-79ff3775-45a8-4d3c-87e5-aaf26453b418.png)


Selanjutnya kita dapat melakukan setting tambahan untuk maintenance aplikasi secara periodik, misalnya:
- buat backup database tiap pekan
![image](https://user-images.githubusercontent.com/81523117/196945272-e1c890cd-504b-40b9-8cd0-21dec0cec1a3.png)
![image](https://user-images.githubusercontent.com/81523117/196945212-9fed073e-cc31-4d89-aaa6-eaaba1d4f2da.png)

- hapus direktori sampah tiap hari
![image](https://user-images.githubusercontent.com/81523117/196945339-872171ba-02da-48e6-9c93-3e91d738b3f3.png)
![image](https://user-images.githubusercontent.com/81523117/196945367-e1497fa0-4ff7-4443-9859-b675d7b68747.png)

- dll

# Otomatisasi
[`^ kembali ke atas ^`](#)

Jika kalian masih merasa kesulitan dalam meng-install **Moodle**, terdapat cara alternatif yang lebih mudah dengan menggunakan layanan yang tersedia pada web-hosting provider. Dengan layanan tersebut kita hanya perlu satu kali klik untuk meng-install **Moodle**. Berikut langkah-langkah untuk melakukannya installasi menggunakan web-hosting provider.
1. Kita perlu mengunjungi web-hosting provider yang menyediakan script instalasi **moodle** otomatis, seperti [softaculous.](http://www.softaculous.com/apps/educational/Moodle) melalui _web-hosting_ [infinityfree.](http://infinityfree.net/accounts)
2. Kunjungi link tersebut lalu buat akun _web-hosting_
![Screenshot (501)](https://user-images.githubusercontent.com/88269626/196848936-62a062a4-fc1a-490f-a07c-3d8922ee8beb.png)

3. Klik _web-hosting_ yang telah dibuat
![Screenshot (502)](https://user-images.githubusercontent.com/88269626/196849119-9b9835f2-3a4d-4126-977d-faa8c83d5e3e.png)

4. Kemudian masuk ke bagian control panel dan pilih softaculous
![Screenshot (503)](https://user-images.githubusercontent.com/88269626/196849136-eccb87e1-dda1-403e-bf54-34260a03981b.png) ![Screenshot (504)](https://user-images.githubusercontent.com/88269626/196849142-dcb87dbe-92d9-48d9-bed2-41870da9b532.png)

5. Selanjutnya cari software moodle dan install
![Screenshot (506)](https://user-images.githubusercontent.com/88269626/196849209-14977e45-def5-41af-98b2-88d85dcc5f51.png)

6. Lalu pilih versi moodle dan masukkan data admin
![Screenshot (507)](https://user-images.githubusercontent.com/88269626/196849229-a59b2c15-be78-4fa8-adb0-053fb91eecb1.png) ![Screenshot (521)](https://user-images.githubusercontent.com/88269626/196849448-29ecb241-9465-4e2e-9eb3-37c493af973f.png)

7. Klik install hingga selesai
![Screenshot (509)](https://user-images.githubusercontent.com/88269626/196849269-ffbf80a6-8986-4625-b540-0bec2b863e8c.png) ![Screenshot (522)](https://user-images.githubusercontent.com/88269626/196849506-bda89b89-c274-4e27-81bd-cbee4d4826cd.png) ![Screenshot (510)](https://user-images.githubusercontent.com/88269626/196849323-0578c12a-b232-4f95-a4a8-a3eea703b8b0.png)

8. Setelah terinstall silahkan klik link yang telah dibuat
![Screenshot (511)](https://user-images.githubusercontent.com/88269626/196849358-fca5fb6d-56c9-48c5-92ff-bfdd955b2e9a.png)

9. Apabila terjadi error, perlu diatur data root dengan file manager
![Screenshot (524)](https://user-images.githubusercontent.com/88269626/196849416-e83120d4-1dc0-42f9-80ce-393ed0d69e18.png)

10. Kembali ke control panel
![Screenshot (525)](https://user-images.githubusercontent.com/88269626/196849543-e473282e-1549-4813-9663-15e4842725cf.png)

11. Buka Online File Manager dan membuka folder htdocs kemudian folder moodle
![Screenshot (526)](https://user-images.githubusercontent.com/88269626/196849688-5a932360-d9fc-409e-a5a6-b1cec692170c.png)

12. Kemudian buat folder baru datanyamoodle dan atur CHMOD dengan write semua
![Screenshot (528)](https://user-images.githubusercontent.com/88269626/196849744-c4061b27-0f7f-45d7-9eb8-ce97cfb38747.png) ![Screenshot (529)](https://user-images.githubusercontent.com/88269626/196849745-e7ec6fc1-cc07-47a4-97be-402d5567755a.png)

13. Selanjutnya buka file config.php kemudian edit
![Screenshot (530)](https://user-images.githubusercontent.com/88269626/196849764-16e9c9c8-0e66-469f-9220-b95586e99b47.png)

14. Ubah data root yang mengarahkan ke folder datanyamoodle yang telah dibuat
![Screenshot (531)](https://user-images.githubusercontent.com/88269626/196849786-171eb1c5-30e2-40d0-a80d-560dfd5b8a44.png) ![Screenshot (532)](https://user-images.githubusercontent.com/88269626/196849798-f3a97297-9271-48c1-8350-655ddb4871db.png)

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
Moodle memberikan pengalaman bagi penggunanya untuk dapat merasakan pembelajaran jarak jauh melalui _online_. Moodle memiliki berbagai fitur yang dapat digunakan untuk mengakses ilmu pengetahuan, manajemen pembelajaran baik _knowledge material_, kuis, dan sebagainya. Sebagai admin dapat mendapatkan dampak dengan mudah menambahkan material yang akan dibagikan. Namun terdapat kekurangan berupa banyaknya data yang ingin dimasukkann namun tampilan muka perlu ditingkatkan untuk efisiensi pengguna. Apabila dibandingkan dengan Google Classroom sebagai aplikasi yang sejenis untuk pendidikan, tampilan muka yang lebih menarik dan efisien dalam menambahkan bahan ajar atau sejenisnya.

# Referensi
[`^ kembali ke atas ^`](#)

1. [About Moodle](https://en.wikipedia.org/wiki/Moodle) - Moodle
2. [Profile Moodle](https://moodle.com/about/) - Profile Moodle
3. [Install Moodle Otomatis](https://www.youtube.com/watch?v=gHNVFl37fRc&list=PL6-8zFijO6H-FkL_xWCFq3K7ueLoWEU82&index=4&ab_channel=BangSuprem) - Tutorial
4. [Dampak Menggunakan Moodle][https://www.indonesiana.id/read/150625/moodle-sebagai-media-interaktif-dalam-konteks-merdeka-belajar] - Dampak
