## Nginx Web Sunucusunun Kurulumu

**Nginx Nedir ?** : Web sayfalarını site ziyaretçilerine görüntülemek için kullanılan yüksek performanslı bir web sunucusudur.

**Kurulum Aşaması ;**

1. sudo apt update : Bu oturumu ilk kez kullanacağımız için apt sunucumuzun paket dizinini güncelleyerek başlıyoruz.

2. sudo apt install nginx : Nginx paketini yüklemek için.

3. sudo ufw allow 'Nginx HTTP' : Bağlantı noktasında normal HTTP trafiğine izin verebilmemiz için. 

4. sudo ufw status : Durumu kontrol ediyoruz.

5. Output : Bu çıktı,HTTP trafiğine artık izin verildiğini gösterir;

Status: active

To                         Action      From

OpenSSH                    ALLOW       Anywhere

Nginx HTTP                 ALLOW       Anywhere

OpenSSH (v6)               ALLOW       Anywhere (v6)

Nginx HTTP (v6)  

<img src="https://github.com/anilmahsun97/anilmahsun97/assets/98519922/d8170fb0-72da-4826-bbc6-5df887d2ee89." width="810" height="570">

Bu görüntüden sonra Nginx'i sistemimize başarılı şekilde kurmuş oluyoruz.


