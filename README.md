
<h1 align="center">Socket io & Node JS & Vue3 Composition Api & C# & MySql</h1>
<h1 align="center">Local ve WEB Tabanlı Socket-io Ağı</h1>


<h4 align="left">İÇERİK</h4>

- [Giriş](#Giriş)
- [Sistem Bileşenleri](#Sistem-Bileşenleri)
- [Çalışma Şekli](#Çalışma-Şekli)
- [Kullanılan Teknolojiler](#Kullanılan-Teknolojiler)
- [İletişim](#İletişim)

## Giriş

Bu çalışmada oyun alanlarında kullanılmak üzere basit bir ağ yapısı üzerinde çalışılmıştır. Bu yapıyla bir oyun alanında kullanılan temassız kartlara ait çeşitli bilgilerin oyun alanındaki bütün birimler tarafından ağ üzerinden paylaşılması ve oyun  alanındaki tüm birimler ile oyuncakların web den erişileibilir(IOT) olması amaçlanmıştır. Bu durumda hedeflerimiz şu şekilde ifade edebiliriz ;
<br><br>


- Oyun alanındaki tüm birimler tarafından temassız kart bilgilerinin paylaşılması.
- Temassız kartın müşteri bilgilerinin tüm birimler tarafından paylaşılması.
- Web üzerinden tüm birimlerdeki işlemlerin anlık takibi.
- Web üzerinden oyuncaklar ve üniteler ile ilgili çeşitli ayarların yapılması.
- Birimlere müşteri kaydının web ve mobil üzerinden yapılabilmesinin sağlanması.
- Web üzerinden oyuncakların uzaktan çalıştırılmasının sağlanması.

Bu sistem daha önce çalıştığımız ve şu anda piyasada kullanılmakta olan [Yoyuncak Oyun Alanı Yönetim Sistemi](#https://github.com/ilyas9461/yoy-yon-sistemi) (V2) üzerine inşa edilmiştir. 

Büyük bir oyun alanında bulunabilecek bazı oyun alanı yapılarını şu şekilde listeleyebiliriz:
- Soft Alanlar : Bunlar top havuzları ve kum havuzları olabilir
- Kiddy Rides oyuncaklar : Çocuklara hitap eden oyuncaklardır.
- Ekranlı Oyuncaklar : Bir PC üzeride çalışabilen oyuncaklardır.
- Peluş oyuncaklar
- Tırmanma duvarları.
- Akülü arabalar, çarpışan arabalar.
- ...

Bir oyun alanında bunlardan çok sayıda olabilir. Bu tür alanlarda genellikle müşteriler temassız karta yüklenen kontür ile bir oyuncağı çalıştırır veya bir oyun alanına giriş yaparlar. Geliştirmiş olduğumuz sistemimiz özetle bu oyun alanlarında farklı fiyat-süre seçeneklerini müşteriye sunarak müşterinin oyun alanında kalma süresini takip etmektedir. Aynı zamanda bütün ödemeleri temassız karta yüklenen kontürleden almaktadır. Dolayısıyla temassız kartlar sistemin en önemli bileşenidir. Bu alt yapıya entegre ettiğimiz yeni özelliklerle de sistem bileşenleri şu şeklide olmaktadır;

## Sockete-IO Ağı Sistem Bileşenleri :
### 1- Kartlı sistem jeton kanalı yükleme cihazı (PIC24F)
### 2- Kartlı sistem jeton kanalları (PIC24F) [Çalışma Videosu ...](https://www.youtube.com/watch?v=HQXXSq4kj5s)
### 3- Oyun alanı yönetim programı V3. (C#)
### 4- Node-JS local server ve socket-io. 
### 5- Server program (c#)
### 6- Web tarafında çalışan uzak server Node-JS ve Socket-io
### 7- VUE3 ile hazırlanmış Dashboard.
### 8- Wireless modüller (ESP8266)

## Çalışma Şekli
## Bölüm 1 : Kart Bilgilerinin Yerel ve Uzak Birimler Tarafından Paylaşılması:
Büyük bir oyun alanında ortalama haftalık ziyaretçi sayısı 1000-5000 arasında değişebilmektedir. Yoğun zamanlarda bir alana birden fazla PC konulabilmektedir. Örneğin iki veya daha fazla kart yükleme noktası oluşturduğunuz zaman kartların deposito durumları PC'ler arasında paylaşılmazsa PC'ler arasında birbirine karışmaktadır. Çok yoğun bir zamanda müşteriye ait bilgilerin her alanda tekrar takip programına girilmesi kuyrukların oluşmasına sebep olmaktadır. Kartlarda meydana gelen çeşitli arızaların (kontür silinmesi, oyuncağın kontürü çekip çalışmaması vb.) hangi alanda yada oyuncakta ne zaman meydana geldiğinin tespiti telafi yüklemelerinde işletmeci açısından önem arzetmektedir. Ayrıca işletmeci bir AVM ile anlaştı ise bu yerler AVM içersinde farklı noktalarda olabilmektedir. Bu durumda da kart bilgilerinin paylaşılabilir olması müşteri memnuniyeti ve sirkülasyonun artması için önemli hale gelmektedir. Bu sistemle kartlar için siyah liste oluşturulabilir ve kartın kullanımı sistemden kaldıralılabilir. Böylelikle kayıp-çalıntı kartın kullanımının da önüne geçilebilir.

Sistem mimarisi belirlenirken internet bağlantısının kopması gibi durumlarda düşünülmüş ve her birimdeki PC verilerini hem kendisine hem de yerelde server PC olarak belirlenen PC veri tabanına kaydetmektedir. Yerelde sistem modem aktif olduğu müddetçe internet bağlantısı olmasa bile kendi içersinde çalışabilmektedir. Birimlerde çalışan programlar web'e veri atarken bir takım gecikme sorunları yaşayablimektedir. Bu programların verileri sadece kendileri ve yerel server PC'deki veri tabanına atmalarının sağlanması ile de sistem çalışma hızı artmıştır. Server PC'de çalışan yerel server program yerel ağ ile web arasında köprü gibi çalışmaktadır. Her bir birimdeki program yapılan işleme bağlı olarak node-js ve socket-io ile yazılan server PC'de çalışan programa belirlenen port üzerinden olay tabanlı bildirimler göndermektedir. Server PC'de çalışan server programda bu bildirimlere abone durumdadır. Gelen olay-veriye göre gerekli işlemleri yapmaktadır. Olay-veriler socket-io yapısı üzerinden dolaşmaktadır. Web veri tabanına server program verileri göndermektedir. Böylelikle oluşabilecek birtakım güvenlik sorunlarının da önüne geçilmiştir.


<p  align="center">
<img src="img/iot_donanim.jpg" alt="pelus" width="400" style="margin-left:10px">
</p>

Server kısmında ;

- Node js Express
- Socket io versiyon 4

İstemci kısmında 

- Vue3 Composition Api

### Test Çalışmaları
Testler yerel server ve bir gsm firmasının superbox adı verilen wifi modemi ile yapılmıştır.
Farklı modem modellerinde özellikle mesafe ile ilgili sonuçlar benzer olmayabilir.

### 1- Bağlantı Mesafesi
Donanım 12V bir aküye bağlanarak yaklaşık 900 metre kare ve kare şeklinde iki katlı, alt ve üst katta duvarlarla bölünmüş alanların ve kolonların  bulunduğu bir üretim atölyesinde dip noktalar dahil her noktaya ve bahçeye gidilerek bağlantı durumu gözlenmiştir.

Bu alanda bağlantının kopmadığı görülmüştür.  

Sonrasında ise dışarıya çıkılarak binadan  uzaklşılmış yaklaşık 50m mesafede bağlantının koptuğu gözlenmiştir. 

Yapılan saha çalışmasında cep telefonunun kablosuz modemi gördüğü her noktada iletişimin sağlandığı sonucuna varılmıştır. 
(Dikkat, cep telefonu modeline göre de değişiklik olabilir.)

### 2- Veri Gönderme Hızı

Socket io bağlantısına gönderilecek verilerin minumum zaman aralığındaki durumu tespit edilmeye çalışılmıştır. Burada amacımız iki veri arasındaki minumum zaman  ve bu veriler veri tabanına kaydedilirken veya gönderilirken bir kayıp oluyor mu tespit etmektir.

Bunun için Node mcu içersindeki yazılım düzenlemiş ve TESTING isimli bir sabit oluşturularak sistem test aşamasına alınmıştır. Infrared yakınlık sensörü kod yapısı teste göre düzenlenerek sensörün tetiklenmmesi ile veriler gönderilmiştir.. Veri yapısı şu şekildedir ;

<p  align="center">
<img src="img/test_veri_yapisi.png" alt="pelus" width="300" style="margin-left:10px">
</p>

Zaman damgası ve örnek data sayısı da eklenerek kayıp veri kontrolü yapılması sağlanmıştır. Node mcu sensör tetiklendiğinde sadece bu veriyi json formatına çevirerek göndermektedir. Gecikmeler işlemleri gerçekleştiren  fonksiyonların gecikmesidir.

Cihaz resetlenerek 30 saniye süre ile sensör tetiklenmiştir. Elde edilen sonuçlar şu şekildedir :

<p  align="center">
<img src="img/test_db_ms1.png" alt="pelus" width="400" style="margin-left:10px">
<img src="img/test_db_ms2.png" alt="pelus" width="400" style="margin-left:10px">
</p>

- Veri tabanına yazılan satır sayısı :6162
- Son veri zaman damgası: 84961 mS
- ilk veri zaman damgası: 56434 mS

- Buna göre :(81063-49767)/6162  =4.629 mS 

Yapılan incelemede verilerin hepsinin sıra atlamadan veri tabanınada yazıldığı görülmüştür.

### Bazı Ekran Görüntüleri
<br>
<p  align="center">
<img src="img/istemci1.png" alt="pelus" width="425" style="margin-left:10px">
<img src="img/istemci.png" alt="pelus" width="400" style="margin-left:10px">
</p>
<br><br>
<p  align="center">
<img src="img/server_kod.png" alt="pelus" width="400" tyle="margin-left:10px">
<img src="img/vue3_kod.png" alt="pelus" width="400" style="margin-left:10px">
</p>

## Kullanılan Teknolojiler

```bash
- NOde MCU ESP-12E.
- Node js, Expres, socket io ...
- Vue3 Composition APi
- PostgreSQL

```

###  Örnek çalışma videosu :

<a href="https://youtu.be/AQEl6YUnvLM" target="_blank">
     <img src="https://camo.githubusercontent.com/241d4106ff5edca2ee25e04dcf4546fad9d20b626f7a10990307e8f83e95459f/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f796f75747562652d2532334646303030302e7376673f267374796c653d666f722d7468652d6261646765266c6f676f3d796f7574756265266c6f676f436f6c6f723d7768697465253232" alt="youtube">
</a>


## İletişim

- GitHub [@your-ilyas9461](https://github.com/ilyas9461)
- Linkedin [@your-linkedin](https://www.linkedin.com/in/ilyas-yagcioglu/)
