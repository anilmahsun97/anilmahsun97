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

# MANAGEIQ #

## MANAGEIQ NEDİR ? ##

ManageIQ, hibrit IT ortamlarını yönetebileceğimiz açık kaynak kodlu bir yazılımdır. Sanal Sistemler, bulut ortamları, konteyner yapılar gibi pek çok farklı ortamı destekler. ManageIQ ile ortamınızı sürekli olarak izleyebilir, son kullanıcılarınıza self-servis oluşturabilir, regülasyonların uygulanmasını sağlayabilir, ortamın performans ve kullanımını verimli hale getirebilirsiniz.

## MANAGEIQ KURULUMU ##

**1. sudo systemctl start docker :** Bu komut ile docker'ı çalıştırıyoruz.

**2. docker pull manageiq/manageiq:petrosian-1 :** Bu komut ile cihazı indiriyoruz ve dağıtıyoruz.

**3. docker run -d -p 8443:443 manageiq/manageiq:petrosian-1 :** Bu komut ile çalıştırıyoruz.

**Sonrasında Google Cloud'da hesap açıyoruz.**
  
<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/89dd3a08-2e47-419f-902d-7d8181fce21a" width="810" height="570">

**Buradan da Compute Engine -> Images -> Create Image deyip yeni bir görüntü oluşturuyoruz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/b744b83b-07d6-4655-8703-3990b42ccb72" width="810" height="570">
<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/5655b5f4-26df-40ad-9693-fa101abbf316" width="810" height="570">

**Sonra burada oluşturduğumuz örnekleri görebiliyoruz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/7ef5bdf2-7ad2-4321-a9c0-367c0fe77435" width="810" height="570">

**Artık ManageIQ arayüzüne giriş yapabiliriz.**

**Giriş : admin**

**Şifre : smartvm**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/05e7ee39-ae0a-46a4-818e-cec478ec51b2" width="810" height="570">

**Seçenekleri değiştiriyoruz. Bölge,saat dilimi,şirket adı vs...**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/ee7b0d7b-e7f9-4e3d-b5c5-0f1c06f913e5" width="810" height="570">

**Görsel seçenekleri ayarlıyoruz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/ccc7db1d-1677-417d-be16-3526762f2d67" width="810" height="570">

**E-posta sunucumuzu ManageIQ'ye bize e-posta gönderebilmesi için ekliyoruz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/f4bd055e-c730-4b17-874c-eacdadefd231" width="810" height="570">

**Buradan sonra Google Cloud'daki projemiz için JSON anahtarı oluşturuyoruz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/9c1f9dcd-94c6-48d9-a069-5cb6a47e4ca7" width="810" height="570">

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/10c7751c-dba8-4c11-b4c4-0b2f9eac113b" width="810" height="570">

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/92f47520-34ae-46cc-b9bf-bfb254474ac4" width="810" height="570">

**Sonrasında Google Cloud'u ManageIQ'ye ekliyoruz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/0239c61e-f4fd-4290-b5a8-334d268004f5" width="810" height="570">

**ManageIQ sağlayıcıyı yeniliyoruz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/c2ebbb42-0967-4a93-879e-9add3db0410f" width="810" height="570">

**Burada bulut sağlayıcılarımızı görebiliyoruz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/d060e65b-514a-4601-bef4-a868c6e6fbef" width="810" height="570">

**Burada doldurmamız gereken maddeler var: E-mail,isim,çevre,özellikler(Bulut sunucusu ve disk boyutu) gibi maddeleri dolduruyoruz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/c0b82c0e-33d2-40b0-a140-fbbb3fe0bae2" width="810" height="570">

**Burada aşamalardan geçip geçmediğini görebiliyoruz:**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/5e1a59e8-d996-47f1-9e5a-f119f6d4cc56" width="810" height="570">

**Buradaki oturumu kapatıp self servis arayüzüne bakalım. Burası daha basit bir tasarıma sahiptir.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/a10fad0b-64b2-4275-944e-d3f8d37d2dca" width="810" height="570">

## MANAGEIQ KULLANIMI ##

**MANAGEIQ'ye giriş yaptığımızda bizi "Overview Dashboard" sayfasına getirir. Bu sayfada ortamınızda gerçekleşen olayları,raporlarınızı ve konfigürasyonunu yaptığınız alarmlarınızı görebilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/88857bba-83c8-40d6-b0dc-5d2ddf4d0ba4" width="810" height="570">

**“Overview > Reports” sekmesinden kullanılabilir olan raporları görebilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/ed0eaf8a-a33b-4050-85f8-81d93e975211" width="810" height="570">

**"Services > My Services" sekmesinde servislerinizi görebilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/45117a1f-32eb-4903-bc82-8674ad6bd5f3" width="810" height="570">

**"Services > Catalog" sekmesinde kullanıcıların iş akışlarını tek bir tıklamayla sipariş etmelerine olanak sağlamak için self servis kataloglar oluşturabilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/a7240453-6fbd-455c-bbff-8389e6e826d0" width="810" height="570">

**"Services > Workloads" sekmesinden sanal makinelerinizi durdurabilir,baştabilir veya silebilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/fa43039d-617f-42a4-a9dc-0e5b904466d1" width="810" height="570">

**"Services > Request" sekmesinden istek oluşturabilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/014f87b5-335a-4350-a2a9-916821f9be25" width="810" height="570">

**"Compute > Clouds" sekmesinden sağlayıcılarımızı ekleyebilir ve onlar hakkında bir çok bilgiye (Erişilebilirlik alanları,bulut birimleri,bulut ağları...) erişebilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/55eaa069-1cd6-45c4-bf21-29d2281bc903" width="810" height="570">
<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/0fe547fb-3bba-44de-9de9-9a2df9840ccc" width="810" height="570">

**"Compute > İnsfrastrucre" sekmesinden yeni alt yapı sağlayıcıları ekleyebilir,sanal makineler ve şablonlarını görebilir,veri depoları indirebilir,anahtarlar indirebilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/f7447f8e-0f5e-4d38-a3e9-b639a7616d12" width="810" height="570">

**"Network" sekmesinden sağlayıcıların ağ özetlerini,alt ağları ve özelliklerini,ağ bağlantı noktalarını ve daha bir çok ağla alakalı bilgiye erişebilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/e1d959a9-8cf5-497c-b5cb-83e21d76fd16" width="810" height="570">
<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/53aab499-5ba8-49d7-8385-f8eaf759f00c" width="810" height="570">
<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/92739803-d1a0-42b9-ae58-2ddfc796734f" width="810" height="570">

**"Storage" sekmesinden yeni depolama yöneticisi ekleyebilir,bulut birimlerinin boyutlarını görebilir ve depolamayla alakalı bir çok bilgiye erişebilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/a911ef6a-5b64-4b42-8283-6964d5aac135" width="810" height="570">
<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/e681abae-b362-434b-a872-2ee5eb1146c1" width="810" height="570">

**"Automation" sekmesinden otomasyon yöneticilerini görebilir,otomasyonla alakalı tüm ayarlamaları buradan yapabilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/105f7ef4-74c2-4480-893b-85de0be389eb" width="810" height="570">
<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/e48118dc-8730-47e8-b009-216b32e2989b" width="810" height="570">

**"Control" sekmesinden politika profillerini görebilir,bilgilerini görebilirsiniz. Koşullar ekleyebilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/9856f810-0236-451a-b95b-499e07d44b35" width="810" height="570">
<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/48c8f76a-95f8-45b3-93be-8f69239a3c7f" width="810" height="570">

**"Settings" sekmesinden ayarlarla alakalı her şeyi yapabilirsiniz. Saat dilimi,rapor sayıları,şirket ismi... gibi. Dokümantasyon kısmına gidip bir çok bilgiye erişebilirsiniz.**

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/a3700e54-0dc0-49a0-af25-08d1547feb89" width="810" height="570">
<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/c01dc3d5-f910-4a50-91ef-ae94dd60d082" width="810" height="570">
<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/b09afa37-ffee-40cb-a803-17ee0cc2fe32" width="810" height="570">

# Kaynakça: 

https://www.manageiq.org/docs/get-started/index.html

https://github.com/orgs/ManageIQ/discussions

https://console.cloud.google.com/welcome/new?project=ancient-edition-419012

https://stackoverflow.com/questions/39100641/docker-service-start-failed

https://asiyeyigit.com/manageiq/

https://stackoverflow.com/questions/46068451/why-docker-cant-start-or-starting-forever

https://stackoverflow.com/questions/tagged/docker






