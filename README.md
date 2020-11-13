# Jarkom_Modul2_Lapres_C15
Lapres Modul 2 Jarkom

### Nama Anggota Kelompok :
### 1. Anggara Yuda Pratama (05111840000008)
### 2. Patrick (05111840000098)

![image](https://user-images.githubusercontent.com/61231385/98681112-e63fb980-2394-11eb-86fa-76895933d194.png)

Semeru adalah salah satu gunung yang terkenal di Jawa Timur. Bibah adalah salah satu juru kunci Semeru. Bibah ingin menyebarkan keindahan Semeru pada dunia sehingga dia membeli 3 buah server yang berada di **MALANG**, **MOJOKERTO** dan **PROBOLINGGO**. Server MALANG akan digunakan sebagai DNS Server Master, **MOJOKERTO** akan digunakan sebagai DNS Server Slave dan **PROBOLINGGO** akan digunakan sebagai Web Server. Selain 3 server terdapat 2 klien yang digunakan untuk testing oleh Bibah yaitu **GRESIK** dan **SIDOARJO**. Untuk menyambungkan semua jaringan tersebut Bibah memberi router di **SURABAYA**.

Keterangan :
- Terlebih dahulu mengisi file topologi.sh dengan cara :
```nano topologi.sh```

- Lalu isi topologi.sh dengan :
```
blablabla
```

- Lalu masing-masing uml di-export proxy-nya agar bisa apt-get update. Kita membuat file dengan nama export.sh yang isinya :
```
export http_proxy=”http://DPTSI-564318-23148:7b3c2@proxy.its.ac.id:8080”
export https_proxy=”http://DPTSI-564318-23148:7b3c2@proxy.its.ac.id:8080”
export ftp_proxy=”http://DPTSI-564318-23148:7b3c2@proxy.its.ac.id:8080”
```

**1. Membuat sebuah website utama dengan alamat http://semeruc15.pw**

- Install bind9 pada uml MALANG dengan command :
``` apt-get install bind9 -y ```

- Pada uml MALANG membuat domain **http://semeruc15.pw** dengan mengedit file ```named.conf.local``` dengan syntax :

```
nano /etc/bind/named.conf.local
```

![1](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/1.jpg)

- Membuat folder ```semeru``` di ```/etc/bind```. Lalu copykan file db.local pada path /etc/bind ke dalam folder ```semeru``` yang baru saja dibuat dan ubah namanya menjadi ```semeruc15.pw```

```
cp /etc/bind/db.local /etc/bind/semeru/semeruc15.pw
```

- Kemudian buka file ```semeruc15.pw``` dan edit seperti gambar berikut :

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

- Untuk mencoba koneksi DNS, lakukan ping domain ```semeruc15.pw``` dengan melakukan perintah berikut pada client GRESIK

```
ping semeruc15.pw
```

![1.3](https://github.com/anggarayp/Jarkom_Modul2_Lapres_C15/blob/main/Screenshots/1%20testing%20ping%20domain.jpg)

**2. Alias http://www.semeruc15.pw**

**3. Subdomain http://penanjakan.semeruc15.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP server PROBOLINGGO**

**4. Dibuatkan reverse domain untuk domain utama.**

**5. Dibuatkan DNS Server Slave pada MOJOKERTO agar tidak terganggu menikmati keindahan Semer pada website**

**6. Membuat subdomain dengan alamat http://gunung.semeruc15.pw yang didelegasikan pada server MOJOKERKTO dan mengarah ke IP Server PROBOLINGGO.**

**7. Membuat subdomain dengan nama http://naik.gunung.semeruc15.pw, domain ini diarahkan ke IP Server PROBOLINGGO**
