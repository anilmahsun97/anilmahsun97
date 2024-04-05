## LEMP KURULUMU ##

Linux Ubuntu 22.04 işletim sistemini kurduktan sonra kurulumlarımıza devam ediyoruz.

## Nginx Web Sunucusunun Kurulumu

**Nginx Nedir ?** : Web sayfalarını site ziyaretçilerine görüntülemek için kullanılan yüksek performanslı bir web sunucusudur.

**Kurulum Aşaması ;**

1. **sudo apt update :** Bu oturumu ilk kez kullanacağımız için apt sunucumuzun paket dizinini güncelleyerek başlıyoruz.

2. **sudo apt install nginx :** Nginx paketini yüklemek için.

3. **sudo ufw allow 'Nginx HTTP' :** Bağlantı noktasında normal HTTP trafiğine izin verebilmemiz için. 

4. **sudo ufw status :** Durumu kontrol ediyoruz.

5. **Output :** Bu çıktı,HTTP trafiğine artık izin verildiğini gösterir;

Status: active

To                         Action      From

OpenSSH                    ALLOW       Anywhere

Nginx HTTP                 ALLOW       Anywhere

OpenSSH (v6)               ALLOW       Anywhere (v6)

Nginx HTTP (v6)  

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/d8170fb0-72da-4826-bbc6-5df887d2ee89" width="810" height="570">

Bu görüntüden sonra Nginx'i sistemimize başarılı bir şekilde kurmuş oluyoruz.

## MySQL'in Kurulumu ##

**MySQL Nedir ?** : Artık çalışır durumda bir web sunucumuz olduğuna göre,sitemize ilişkin verileri depolamak ve yönetmek için veritabanı sistemini kurmamız gerekiyor.

**sudo apt install mysql-server :**  MySQL paketini yüklemek için.

**sudo mysql_secure_installation :** Bu komutla güvenli olmayan varsayılan ayarları kaldırıyoruz.

**"Press y|Y for Yes, any other key for No" :** Buna benzer çıktılar oluyor ve evet diyerek geçiyoruz.

**sudo mysql :** MySQL'e giriş yapıyoruz.

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/5c1f34e8-15f0-44a0-964d-700cbd32daf9" width="810" height="570">

Bu görüntüden sonra MySQL'i sistemimize başarılı bir şekilde kurmuş oluyoruz.

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/da20242d-85d4-4f72-bf50-f887aadb115b)" width="810" height="570">

Burada da veritabanı ayarlarımızı yapıyoruz.

## PHP'nin Kurulumu  ##

**sudo apt install php8.1-fpm php-mysql :** Bu kodla PHP'yi sistemimize kurmuş oluyoruz.

## Ubuntu'daki Nginx Web Sunucusuna Wordpress Kurulumu

**İlk önce wordpress dokümanını indiriyoruz.**

**Sonrasında ayarları yapıyoruz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/e85bdc6b-93c2-4610-81b5-80aa63a2f3a7" width="810" height="570">

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/10f319de-f98a-41c0-863a-904ea4e5a82c" width="810" height="570">

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/fed1964b-a2fd-49f8-9744-b8c1c3b5e257" width="810" height="570">

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/6bc7f421-2e76-4b87-9d8e-13ed0d84ae32" width="810" height="570">

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/b3b6b5ff-cafa-4c8c-991e-2ad6ab36453b" width="810" height="570">

Wordpress'i başarılı şekilde kurduktan sonra backup aşamasına geçiyoruz.

## Sitenin Backup'ını Alma

**sudo mkdir /var/backup/db :** İlk başta Backup diye bir klasör oluşturuyoruz.

**sudo crontab -e :** Crontab -e komutuyla da Cron'a giriş yapıyoruz. Peki Cron nedir ve nasıl kullanılır ?

**Cronjob Nedir Ve Nasıl Kullanılır ? :** Cron bir görevi ilerleyen bir zamanda tekrarlamak için kullanılan bir programdır.

**Kullanımı şu şekildedir :** * * * * * /bin/sh backup.sh

**30 18 * * * rm /home/sydtesting/tmp/*:** Örneğin bu komutta tmp dosyalarını /home/sydtesting/tmp konumundan her gün 18.30’da silecektir.

**53 21 * * * cd /home/anilmahsun/backup && tar -cpzf backup$(date +\%Y\%m\%d).tar.gz /var/www/html/ && mysqldump -u root -p 123456 --all-databases --master-data | gzip > backup$(date +\%Y\%m\%d).sql.gz :** Yazdığımız bu komut ile her gün 21:53'te sistem otomatik olarak Backup'ını almış oluyor.

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/a1c03da3-4b33-480a-a14b-6ba0fcf04dce" width="810" height="570">

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/1af28373-26d0-47c6-b099-e7a3cd2f2a4b" width="810" height="570">

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/a861750f-dd89-478b-b11b-d0813d39c023" width="810" height="570">

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/98a98f85-c0b8-4b59-85f3-7a135cfbb9b4" width="810" height="570">

Burada Backup'ımızı almış bulunuyoruz.

**sudo mysql -u root wordpress < backup20240322.sql :** Bu Komut ile de backup'ımıza geri dönüş sağlıyoruz.

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/d325127e-9bfe-40f6-b1fe-46fa5bf7a67f" width="810" height="570">

# Kaynakça: 

https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-22-04

https://www.linuxbabe.com/backup/backup-and-restore-wordpress-site-without-a-plugin

https://medium.com/@satriajanaka09/how-to-setup-a-scheduler-for-mysql-database-backup-with-crontab-63917e594bbb

https://folio3.com/5-easy-steps-on-scheduling-mysql-database-backup-using-cron  

https://github.com/kaymal/Markdown

https://medium.com/@edanur.yanik.mhnds/cron-job-nedir-f3cc57d3ee02

https://www.youtube.com/watch?v=z35ZPELo5_Y

https://www.youtube.com/watch?v=vZjAhjqLakU

---
---
---

## PERFORMANS TESTİNİ ARTIRMAK İÇİN YAPILAN ADIMLAR ##

**1.**  İlk önce sistemi güncelliyoruz.

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/6d0fe895-6ac1-4060-a476-fdcacd94157c" width="810" height="570">

**2.**  Nginx'te statik içerik önbelleğe alma süresini değiştiriyoruz.

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/a7dd36a1-9307-473d-9369-0a11ed68b786" width="810" height="570">

**3.**  Arabellek boyutunu ayarlıyoruz.

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/1d2bc0c0-a6fa-480c-bda2-0b0b1fe02b83" width="810" height="570">

**4.**  Zaman aşımlarını azaltıyoruz. Zaman aşımları Nginx performansını önemli ölçüde artırır.

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/5a2f65be-e6a7-4207-a9d5-2542d227389e" width="810" height="570">

**5.**  systcl.conf dosyasında değerleri artırıyoruz.

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/76d6c7cc-5c82-467c-926d-ce0ae17aefdb" width="810" height="570">

### Performans testini çalıştırıyoruz.

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/c503fb84-4778-403b-865a-6360640432ab" width="810" height="570">

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/21a28eca-3733-41dc-a478-beb0e3b6a0cb" width="810" height="570">

# Kaynakça: 

https://sysopstechnix.com/7-tips-for-nginx-performance-tuning/

https://github.com/hugapi/hug/issues/625

https://www.baeldung.com/linux/error-too-many-open-files

https://cs.uwaterloo.ca/~brecht/servers/openfiles.html

https://gist.github.com/denji/8359866

https://wordpress.org/plugins/redis-cache/

https://medium.com/@khushalbisht/improving-wordpress-performance-with-nginx-b1535bc9e2b7

---
---
---

## MANAGEIQ ##

# MANAGEIQ KURULUMU #

**1.** sudo systemctl start docker : Bu komut ile docker'ı çalıştırıyoruz.

**2.** docker pull manageiq/manageiq:petrosian-1 : Bu komut ile cihazı indiriyoruz ve dağıtıyoruz.

**3.** docker run -d -p 8443:443 manageiq/manageiq:petrosian-1 : Bu komut ile çalıştırıyoruz.

Sonrasında **Google Cloud**'da hesap açıyoruz. (1)

Buradan da Compute Engine -> Images -> Create Image diyip yeni bir görüntü oluşturuyoruz. (2-3)

Sonra burada oluşturduğumuz örnekleri görebiliyoruz. (4)

Artık ManageIQ arayüzüne giriş yapabiliriz. (5)

Giriş : admin
Şifre: smartvm

Seçenekleri değiştiriyoruz. Bölge,saat dilimi,şirket adı vs... (6)

Görsel seçenekleri ayarlıyoruz. (7)

E-posta sunucumuzu ManageIQ'ye bize e-posta gönderebilmesi için ekliyoruz. (8)

Buradan sonra Google Cloud'daki projemiz için JSON anahtarı oluşturuyoruz. (9-10-11)

Sonrasında Google Cloud'u ManageIQ'ye ekliyoruz. (12)

ManageIQ sağlayıcıyı yeniliyoruz. (13)

Burada bulut sağlayıcılarımızı görebiliyoruz. (14)
