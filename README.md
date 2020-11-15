# Jarkom_Modul2_Lapres_C15
Lapres Modul 2 Jarkom

### Nama Anggota Kelompok :
### 1. Anggara Yuda Pratama (05111840000008)
### 2. Patrick (05111840000098)

![image](https://user-images.githubusercontent.com/61231385/98681112-e63fb980-2394-11eb-86fa-76895933d194.png)

Semeru adalah salah satu gunung yang terkenal di Jawa Timur. Bibah adalah salah satu juru kunci Semeru. Bibah ingin menyebarkan keindahan Semeru pada dunia sehingga dia membeli 3 buah server yang berada di **MALANG**, **MOJOKERTO** dan **PROBOLINGGO**. Server MALANG akan digunakan sebagai DNS Server Master, **MOJOKERTO** akan digunakan sebagai DNS Server Slave dan **PROBOLINGGO** akan digunakan sebagai Web Server. Selain 3 server terdapat 2 klien yang digunakan untuk testing oleh Bibah yaitu **GRESIK** dan **SIDOARJO**. Untuk menyambungkan semua jaringan tersebut Bibah memberi router di **SURABAYA**.

### Daftar Soal
* [No. 1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15#1-membuat-sebuah-website-utama-dengan-alamat-httpsemeruc15pw)
* [No. 2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15#2-alias-httpwwwsemeruc15pw)
* [No. 3](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15#3-subdomain-httppenanjakansemeruc15pw-yang-diatur-dns-nya-pada-malang-dan-mengarah-ke-ip-server-probolinggo)
* [No. 4](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15#4-dibuatkan-reverse-domain-untuk-domain-utama)
* [No. 5](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15#5-dibuatkan-dns-server-slave-pada-mojokerto-agar-tidak-terganggu-menikmati-keindahan-semeru-pada-website)
* [No. 6](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15#6-membuat-subdomain-dengan-alamat-httpgunungsemeruc15pw-yang-didelegasikan-pada-server-mojokerkto-dan-mengarah-ke-ip-server-probolinggo)
* [No. 7](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15#7-membuat-subdomain-dengan-nama-httpnaikgunungsemeruc15pw-domain-ini-diarahkan-ke-ip-server-probolinggo)
* [No. 8](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/README.md#8-mengatur-web-server-dengan-domain-semeruc15pw-dan-memiliki-document-root-pada-varwwwsemeruc15pw)
* [No. 9](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/README.md#9-mengubah-semeruc15pwindexphphome-menjadi-semeruc15pwhome)
* [No. 10](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/README.md#10-setting-penanjakansemeruc15pw-agar-bisa-diakses)
* [No. 11](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/README.md#11-pada-folder-public-dibolehkan-directory-listing-namun-untuk-folder-yang-berada-di-dalamnya-tidak-dibolehkan)
* [No. 12](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/README.md#12-untuk-mengatasi-http-error-code-404-disediakan-file-404html-pada-folder-errors-untuk-mengganti-error-default-404-dari-apache)
* [No. 13](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/README.md#13-untuk-mengakses-file-assets-javascript-awalnya-harus-menggunakan-url-httppenanjakansemeruyyypwpublicjavascripts-lalu-dibuatkan-konfigurasi-virtual-host-agar-ketika-mengakses-file-assets-menjadi-httppenanjakansemeruyyypwjs)
* [No. 14](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/README.md#14-setting-web-httpnaikgunungsemeruyyypw-yang-hanya-bisa-diakses-menggunakan-port-8888)
* [No. 15](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/README.md#15-bibah-meminta-kamu-membuat-web-httpnaikgunungsemeruyyypw-agar-diberi-autentikasi-password-dengan-username-semeru-dan-password-kuynaikgunung-supaya-aman-dan-tidak-sembarang-orang-bisa-mengaksesnya)
* [No. 16](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/README.md#16-mengarahkan-ip-probolinggo-ke-web-semeruc15pw)
* [No. 17](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/README.md#17-karena-pengunjung-pada-varwwwpenanjakansemeruyyypwpublicimages-sangat-banyak-maka-semua-request-gambar-yang-memiliki-substring-semeru-akan-diarahkan-menuju-semerujpg)

Keterangan :
- Terlebih dahulu mengisi file topologi.sh dengan cara : ```nano topologi.sh```

- Lalu isi topologi.sh dengan :
  ```
  # Switch
  uml_switch -unix switch1 > /dev/null < /dev/null &
  uml_switch -unix switch2 > /dev/null < /dev/null &

  # Router
  xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,'ip_tuntap_tiap_kelompok' eth1=daemon,,,switch2 eth2=daemon,,,switch1 mem=96M &

  # Server
  xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=128M &
  xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=160M &
  xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch2 mem=160M &

  # Klien
  xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch1 mem=96M &
  xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch1 mem=96M &
  ```

- Lalu masing-masing uml di-export proxy-nya agar bisa apt-get update. Kita membuat file dengan nama export.sh yang isinya :
  ```
  export http_proxy=”http://DPTSI-564318-23148:7b3c2@proxy.its.ac.id:8080”
  export https_proxy=”http://DPTSI-564318-23148:7b3c2@proxy.its.ac.id:8080”
  export ftp_proxy=”http://DPTSI-564318-23148:7b3c2@proxy.its.ac.id:8080”
  ```
 
 - Jangan lupa membuat file bye.sh dengan cara : ```nano bye.sh```, yang isinya :
 
   ```
   uml_mconsole SURABAYA halt
   uml_mconsole MALANG halt
   uml_mconsole MOJOKERTO halt
   uml_mconsole SIDOARJO halt
   uml_mconsole GRESIK halt
   uml_mconsole PROBOLINGGO halt
   ```

### 1. Membuat sebuah website utama dengan alamat http://semeruc15.pw

- Install bind9 pada uml MALANG dengan command : ``` apt-get install bind9 -y ```

- Pada uml MALANG membuat domain **http://semeruc15.pw** dengan mengedit file **named.conf.local** dengan syntax :

  ```
  nano /etc/bind/named.conf.local
  ```

  ![1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/1.jpg)

- Membuat folder **semeru** di **/etc/bind**. Lalu copykan file db.local pada path /etc/bind ke dalam folder **semeru** yang baru saja dibuat dan ubah namanya menjadi **semeruc15.pw**

  ```
  cp /etc/bind/db.local /etc/bind/semeru/semeruc15.pw
  ```

- Kemudian buka file **semeruc15.pw** dan edit seperti gambar berikut :

  ```
  nano /etc/bind/semeru/semeruc15.pw
  ```

  ![1.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/1.1.jpg)

- Jangan lupa buat restart bind

  ```
  service bind9 restart
  ```

- Pada client GRESIK arahkan nameserver menuju IP MALANG dengan mengedit file resolv.conf dengan mengetikkan perintah

  ```
  nano /etc/resolv.conf
  ```

  ![1.2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/1%20testing%20client%20ke%20server%20malang.jpg)

- Untuk mencoba koneksi DNS, lakukan ping domain **semeruc15.pw** dengan melakukan perintah berikut pada client GRESIK

  ```
  ping semeruc15.pw
  ```

  ![1.3](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/1%20testing%20ping%20domain.jpg)

### 2. Alias http://www.semeruc15.pw

Untuk membuat alias kita membuat record CNAME yang mengarah ke domain. 

- Mengubah isi dari file **semeruc15.pw** pada server MALANG dan menambahkan konfigurasi seperti berikut :

  ![2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/2.jpg)

- Jangan lupa buat restart bind

  ```
  service bind9 restart
  ```

- Lalu cek dengan **ping** www.semeruc15.pw pada client GRESIK

  ```
  ping www.semeruc15.pw
  ```

  ![2.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/2%20testing%20ping%20alias.jpg)

### 3. Subdomain http://penanjakan.semeruc15.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP server PROBOLINGGO

Subdomain umumnya mengacu ke suatu alamat fisik di sebuah situs. Kita membuat subdomain http://penanjakan.semeruc15.pw yang mengacu ke semeruc15.pw sebagai domain induknya.

- Edit file **/etc/bind/semeru/semeruc15.pw** lalu tambahkan subdomain untuk semeruc15.pw yang mengarah ke IP PROBOLINGGO.

  ```
  nano /etc/bind/semeru/semeruc15.pw
  ```

  ![3](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/3.jpg)

- Jangan lupa buat restart bind

  ```
  service bind9 restart
  ```

- Lalu cek dengan **ping** penanjakan.semeruc15.pw pada client GRESIK

  ```
  ping penanjakan.semeruc15.pw
  ```

  ![3.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/3%20testing%20subdomain%20penanjakan.jpg)

### 4. Dibuatkan reverse domain untuk domain utama.

Reverse domain digunakan untuk menerjemahkan alamat IP ke alamat domain yang sudah diterjemahkan sebelumnya.

- Mengubah isi dari file **/etc/bind/named.conf.local** pada server MALANG dan menambahkan konfigurasi seperti berikut :

  ```
  nano /etc/bind/named.conf.local
  ```

  ![4](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/4.jpg)

- Copykan file db.local pada path /etc/bind ke dalam folder **semeru** yang baru saja dibuat dan ubah namanya menjadi 77.151.10.in-addr.arpa

  ```
  cp /etc/bind/db.local /etc/bind/semeru/77.151.10.in-addr.arpa
  ```

- Edit file **77.151.10.in-addr.arpa** seperti berikut :

  ![4.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/4.1.jpg)
  
 - Jangan lupa buat restart bind

  ```
  service bind9 restart
  ```

- Testing host yang sudah dibuat di client GRESIK dengan : ``` host -t PTR 10.151.77.32```

  ![4.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/4%20testing%20host.jpg)

### 5. Dibuatkan DNS Server Slave pada MOJOKERTO agar tidak terganggu menikmati keindahan Semeru pada website

DNS Slave adalah DNS cadangan yang akan diakses jika server DNS utama mengalami kegagalan.

-- Konfigurasi pada server MALANG

  - Mengubah isi dari file **/etc/bind/named.conf.local** pada server MALANG dan menambahkan konfigurasi seperti berikut :

    ```
    zone "semeruc15.pw" {
      type master;
      notify yes;
      also-notify { 10.151.77.131; }; // IP MOJOKERTO
      allow-transfer { 10.151.77.131; }; // IP MOJOKERTO
      file "/etc/bind/semeru/semeruc15.pw";
    };
    ```

    ![5](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/5.jpg)

  - Jangan lupa buat restart bind

    ```
    service bind9 restart
    ```
  
-- Konfigurasi pada server MOJOKERTO

  - Install bind9 pada server MOJOKERTO dengan command : ``` apt-get install bind9 -y ```

  - Mengubah isi dari file **/etc/bind/named.conf.local** pada server MOJOKERTO dan menambahkan konfigurasi seperti berikut :

    ```
    zone "semeruc15.pw" {
      type slave;
      masters { 10.151.77.130; }; // IP MALANG
      file "/etc/bind/semeru/semeruc15.pw";
    };
    ```

    ![5.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/5.1.jpg)

  - Jangan lupa buat restart bind

    ```
    service bind9 restart
    ```
  
- Selanjutnya pada server MALANG silahkan matikan service bind9 dengan cara : ```service bind9 stop```

- Lalu testing pada client GRESIK.

  ![5.2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/5.2.jpg)

### 6. Membuat subdomain dengan alamat http://gunung.semeruc15.pw yang didelegasikan pada server MOJOKERKTO dan mengarah ke IP Server PROBOLINGGO.

Delegasi subdomain merupakan pemberian wewenaang atas sebuah subdomain kepada DNS baru.

-- Konfigurasi di server MALANG

 - Mengubah isi dari file **/etc/bind/semeru/semeruc15.pw** pada server MALANG seperti gambar berikut :
 
   ![6](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/6.png)
 
 - Lalu edit file **/etc/bind/named.conf.options** dengan comment **dnssec-validation auto;** dan tambahkan ```allow-query{any;};```. Lebih lengkapnya seperti gambar berikut :
 
   ![6.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/6.1.jpg)
 
 - Edit file **/etc/bind/named.conf.local** seperti gambar berikut :
 
   ![6.2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/6.2.jpg)
 
 - Jangan lupa buat restart bind

    ```
    service bind9 restart
    ```

-- Konfigurasi di server MOJOKERTO

 - Edit file **/etc/bind/named.conf.options** dengan comment **dnssec-validation auto;** dan tambahkan ```allow-query{any;};```. Lebih lengkapnya seperti gambar berikut :
 
   ![6.3](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/6.3.jpg)
   
 - Lalu edit file /etc/bind/named.conf.local menjadi seperti gambar berikut :
 
   ![6.4](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/6.4.jpg)

-- Testing 
  
  - Coba ping di server GRESIK ```ping gunung.semeruc15.pw```
    
    ![6.5](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/6%20testing%20ping.jpg)
  
### 7. Membuat subdomain dengan nama http://naik.gunung.semeruc15.pw, domain ini diarahkan ke IP Server PROBOLINGGO

-- Konfigurasi di server MOJOKERTO

 - Mengubah isi dari file **/etc/bind/delegasi/gunung.semeruc15.pw** seperti gambar berikut :
 
   ![7.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/6.5%20%26%207.jpg)
 
 - Lakukan restart service bind ```service bind9 restart```

-- Testing
  
  - Coba ping di server GRESIK ```ping naik.gunung.semeruc15.pw```
   
   ![7.2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/7%20testing%20ping.jpg)
   
### 8. Mengatur web server dengan domain semeruc15.pw dan memiliki document root pada /var/www/semeruc15.pw

-- Konfigurasi Server PROBOLINGGO
  
  - Install apache pada uml PROBOLINGGO dengan command : ``` apt-get install apache2 ```
  
  - Install php pada uml PROBOLINGGO dengan command : ``` apt-get install php ```
  
  - Pindah ke direktori **/etc/apache2/sites-available** dan copy file **000-default.conf** dan rename dengan nama **semeruc15.pw.conf**
    
    ```
    cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/semeruc15.pw.conf
    ```
  
  - Edit file **semeruc15.pw.conf**
    
    ![8.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/8.jpg)
  
  - Aktifkan site dengan command 
    
    ```
    a2ensite semeruc15.pw
    ```
    
    ![8.2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/8.2.jpg)
  
  - Pindah ke direktori **/var/www**
  
  - Download file website dengan cara ```wget 10.151.36.202/semeru.pw.zip```
  
  - Unzip file yang sudah didownload dan ganti nama file
    
    ![8.3](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/8%209%2014.jpg)
  
  - Restart apache : ```service apache2 restart```
  
  - Ketika **semeruc15.pw** diakses, akan menampilkan seperti di gambar berikut
    
    ![8.4](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/8.1.jpg)
    
### 9. Mengubah **semeruc15.pw/index.php/home** menjadi **semeruc15.pw/home**

-- Konfigurasi pada server PROBOLINGGO
  
  - Aktifkan module rewrite 
    ```
    a2enmod rewrite
    ```
  
  - Pindah ke direktori **/etc/apache2/sites-available** dan edit file **semeruc15.pw.conf**
    
    ![9.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/9%20di%20semeruc15pw.jpg)  
  
  - Pindah ke direktori **/var/www/semeruc15.pw** dan buat file **.htaccess** yang berisi
    
    ![9.2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/9%20di%20semeruc15pw.jpg)  
  
  - Restart apache : ```service apache2 restart```
  
  - Ketika **semeruc15.pw/home** diakses, akan menampilkan seperti di gambar berikut
    
    ![9.3](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/9.2.jpg)
 
 ### 10. Setting **penanjakan.semeruc15.pw** agar bisa diakses
 
 -- Konfigurasi pada server PROBOLINGO
  
  - Pindah ke direktori **/etc/apache2/sites-available** dan copy file **000-default.conf** dan rename dengan nama **penanjakan.semeruc15.pw.conf**
    
    ```
    cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/penanjakan.semeruc15.pw.conf
    ```
  
  - Edit file **penanjakan.semeruc15.pw.conf**
    
    ![10.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/10.jpg)
  
  - Aktifkan site dengan command 
    
    ```
    a2ensite penanjakan.semeruc15.pw
    ```
  
  - Pindah ke direktori **/var/www**
  
  - Download file website dengan cara ```wget 10.151.36.202/penanjakan.semeru.pw.zip```
  
  - Unzip file yang sudah didownload dan ganti nama file
    
    ![10.2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/8%209%2014.jpg)
  
  - Restart apache : ```service apache2 restart```
  
  - Ketika **penanjakan.semeruc15.pw** diakses, akan menampilkan seperti di gambar berikut
    
    ![10.3](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/10.1.jpg)
    
### 11. Pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan.

-- Konfigurasi pada Server PROBOLINGGO
  
  - Edit file **penanjakan.semeruc15.pw.conf**
    
    ![11.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/11.jpg)
  
  - Restart apache ```service apache2 restart```
  
  - Ketika dibuka, hasilnya akan seperti gambar dibawah ini
    
    ![11.2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/11.1.jpg)
    
    ![11.3](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/11.2.jpg)
    
    ![11.4](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/11.3.jpg)
    
    ![11.5](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/11.4.jpg)
    
### 12. Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada folder /errors untuk mengganti error default 404 dari Apache.

- Edit file penanjakan.semeruc15.pw.conf seperti berikut: 

  ```
  nano /etc/apache2/sites-available/penanjakan.semeruc15.pw.conf
  ```
  
  ![12](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/12.jpg)
  
- Jadi jika ketika membuka websitenya akan muncul seperti berikut yang mengganti error default 404 dari apache :

  ![12.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/12.1.jpg)

### 13. Untuk mengakses file assets javascript awalnya harus menggunakan url http://penanjakan.semeruyyy.pw/public/javascripts. Lalu dibuatkan konfigurasi virtual host agar ketika mengakses file assets menjadi http://penanjakan.semeruyyy.pw/js.

- Edit file penanjakan.semeruc15.pw.conf 

  ```
  nano /etc/apache2/sites-available/penanjakan.semeruc15.pw.conf
  ```
- Tambahkan :

  ```
  Alias "/js" "/var/www/penanajakan.semeruc15.pw/public/javascripts/"
  ```

  ![13](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/13.jpg)

- Jika kita buka **penanjakan.semeruc15.pw/js/** maka akan muncul seperti berikut :

  ![13.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/13.1.jpg)

### 14. Setting Web http://naik.gunung.semeruyyy.pw yang hanya bisa diakses menggunakan port 8888.

-- Konfigurasi pada Server PROBOLINGGO
  
  - Pindah ke direktori **/etc/apache2/sites-available** dan copy file **000-default.conf** dan rename dengan nama **naik.gunung.semeruc15.pw.conf**
    
    ```
    cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/naik.gunung.semeruc15.pw.conf
    ```
    
  - Edit file **naik.gunung.semeruc15.pw.conf**, ganti virtual host dari :80 menjadi :8888. Lalu tambahkan server name dan arahkan document root ke /var/www/naik.gunung.semeruc15.pw
    
    ![14.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/14.1.jpg)
  
  - Pindah ke direktori **/etc/apache2** dan edit file **ports.conf** agar bisa mengkases port 8888
    
    ![14.2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/14.2.jpg)
  
  - Aktifkan site dengan command
    
    ```
    a2ensite naik.gunung.semeruc15.pw
    ```
  
  - Pindah ke direktori **/var/www**
  
  - Download file website dengan cara ```wget 10.151.36.202/naik.gunung.semeru.pw.zip```
  
  - Unzip file yang sudah didownload dan ganti nama file
    
    ![14.3](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/8%209%2014.jpg)
  
  - Restart apache : ```service apache2 restart```
  
  - Hasilnya, web naik.gunung.semeruc15.pw hanya bisa diakses port 8888 dan akan menampilkan seperti gambar dibawah ini
    
    ![14.4](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/14.4.jpg)
    
### 15. Bibah meminta kamu membuat web http://naik.gunung.semeruyyy.pw agar diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung” supaya aman dan tidak sembarang orang bisa mengaksesnya.

- Kita harus membuat sebuah username dan password di server PROBOLINGGO dengan cara :

  ```
  htpasswd -c /etc/apache2/.htpasswd semeru
  ```

- Lalu isi passwordnya dengan ```kuynaikgunung```. Jika sudah membuat username, kita bisa mengeceknya di file .htpasswd :

  ![15](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/15.png)

- Kemudian jika kita membuka **naik.gunung.semeruc15.pw:8888**, maka tampilannya akan seperti berikut :

  ![15.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/15.1.jpg)

  ![15.2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/15.2.jpg)

### 16. Mengarahkan IP PROBOLINGGO ke web semeruc15.pw

-- Konfigurasi pada Server PROBOLINGGO
  
  - Pindah ke direktori **/etc/apache2/sites-available** dan buka file **000-default.conf**
  
  - Tambahkan perintah redirect seperti dibawah ini
    
    ```
    redirect permanent / http://semeruc15.pw
    ```
    
    ![16.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/16.1.jpg)
  
  - Restart apache : ```service apache2 restart```
  
  - Hasilnya, jika kita mencoba akses IP PROBOLINGGO, akan diredirect ke semeruc15.pw
    
    ![16.2](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/16.2.jpg)
    
    ![16.3](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/16.3.jpg)

### 17. Karena pengunjung pada /var/www/penanjakan.semeruyyy.pw/public/images sangat banyak maka semua request gambar yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg.

- Edit file .htaccess :

  ```
  nano /var/www/penanjakan.semeruc15.pw/.htaccess
  ```

- Edit dengan syntax :

  ```
  RewriteEngine On
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteRule ^/?(.*)semeru(.*)\.jpg$ /public/images/semeru.jpg [R=301,L]
  ```
  
  ![17](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/17%20var%20www%20penanjakan.jpg)
  
- Edit file penanjakan.semeruc15.pw.conf seperti berikut: 

  ```
  nano /etc/apache2/sites-available/penanjakan.semeruc15.pw.conf
  ```

  ![17.1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/17.1.jpg)
  
- Jika kita membuka url seperti ini :

  ![17.3](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/17.3.jpg)
  
  Maka akan keluar seperti ini :
  
  ![17.4](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/17.4.jpg)
