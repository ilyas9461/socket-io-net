
<h1 align="center">Local ve WEB Tabanlı Socket-io Ağı</h1>
<h2 align="center">Node JS & Socket io & C# & MySql & Vue3 Composition Api </h1>

<h4 align="left">İÇERİK</h4>

- [Giriş](#Giriş)
- [Sistem Bileşenleri](#Sistem-Bileşenleri)
- [Çalışma Şekli](#Çalışma-Şekli)
- [Kullanılan Teknolojiler](#Kullanılan-Teknolojiler)
- [İletişim](#İletişim)

## Giriş

Bu çalışmada oyun alanlarında kullanılmak üzere basit bir socket-io ağ yapısı üzerinde durulmuştur. Bu yapıyla bir oyun alanında kullanılan temassız kartlara ait çeşitli bilgilerin oyun alanındaki bütün birimler tarafından ağ üzerinden paylaşılması ve oyun  alanındaki tüm birimler ile oyuncakların web den erişileibilir (IOT) olması amaçlanmıştır. Büyük bir oyun alanında iki ana eğlence alanından bahsedebiliriz:
- Oyuncaklar, bireysel olarak kulanılan ve temassız kart okuyucu ile aktif edilebilen çok çeşitli gruplardır. 
- Birimler olarak tanımladığımız kısım ise, genel olarak soft alanlar olarak adlandırılır ve birden fazla kişinin aynı anda yararlandığı eğlenme yerleridir. Her birimde bir PC bulunur ve üzerinde çalışan program vasıtasıyla birimlere müşteriler temassız kart, nakit ve kredi kartı ödeme seçenekleri ile kabul edilirler. Bu program ayrıca müşterilerin birimde kalma sürelerini de takip ederek çeşitli seçenekler sunar. Günsonunda günlük ciro, masraflar, misafir sayıları vb. konularda raporlama sunarken yaptığı bütün işlemleri web veri tabanına da kaydeder. Böylece web tarafından anlık ciro vb bilgiler görüntülenebilir. Ayrıntılı bilgi için; [Yoyuncak Oyun Alanı Yönetim Sistemi](https://github.com/ilyas9461/yoy-yon-sistemi) 

Bu durumda genel olarak hedeflerimizi şu şekilde ifade edebiliriz:<br>

- Oyun alanındaki tüm birimler ve oyuncaklar tarafından temassız kart bilgilerinin paylaşılması.
- Temassız kartın müşteri bilgilerinin tüm birimler tarafından paylaşılması.
- Tüm birimlerde yapılan işlemlerin ağ üzerinde anlık olarak gözlenebilmesi.
- Web üzerinden tüm birimlerdeki işlemlerin anlık takibi.
- Web-yerel üzerinden oyuncaklar ve üniteler ile ilgili çeşitli ayarların uzaktan yapılması.
- Birimlere müşteri kaydının web ve mobil üzerinden yapılabilmesinin sağlanması.
- Web-yerel üzerinden oyuncakların uzaktan çalıştırılmasının sağlanması.

Bu sistem daha önce çalıştığımız ve şu anda piyasada çeşitli yerlerdeki (11 farklı oyun alanı ve yaklaşık 25 PC'de) oyun alanlarında kullanılmakta olan [Yoyuncak Oyun Alanı Yönetim Sistemi](https://github.com/ilyas9461/yoy-yon-sistemi) (V2) üzerine inşa edilmiştir. 

Büyük bir oyun alanında bulunabilecek bazı oyun alanı eğelence merkezlerini şu şekilde listeleyebiliriz:
- Soft Alanlar : Bunlar çeşitli büyüklükteki top havuzları ve kum havuzları olabilir
- Kiddy Rides oyuncaklar : Çocuklara hitap eden oyuncaklardır.
- Ekranlı Oyuncaklar : Bir PC üzeride çalışabilen oyuncaklardır.
- Peluş oyuncaklar.
- Tırmanma duvarları.
- Akülü arabalar, çarpışan arabalar.
- ...

Bir oyun alanında bunlardan çok sayıda olabilir. Bu tür alanlarda genellikle müşteriler temassız karta yüklenen kontür ile bir oyuncağı çalıştırır veya bir oyun alanına giriş yaparlar. Geliştirmiş olduğumuz sistemimiz özetle bu oyun alanlarında farklı fiyat-süre seçeneklerini müşteriye sunarak müşterinin oyun alanında kalma süresini takip etmektedir. Aynı zamanda bütün ödemeleri temassız karta yüklenen kontürleden veya nakit-kredi kartı üzerinden alabilmektedir. Genel olarak bir veya daha fazla kart yükleme noktsından temassız kartlar kontur yüklenmekte ve diğer yerlerde bu temassız kartlar kullanılmaktadır. Dolayısıyla temassız kartlar sistemin en önemli bileşenidir. Bu alt yapıya entegre ettiğimiz yeni özelliklerle de sistem bileşenleri şu şeklide olmaktadır;

<p  align="center">
<img src="img/system-structure.png" alt="pelus" width="100%" style="margin-left:10px">
</p>

## Sockete-IO Ağı Sistem Bileşenleri :
### 1- Kartlı sistem jeton kanalı yükleme cihazı (PIC24F)
### 2- Kartlı sistem jeton kanalları (PIC24F) [Video ...](https://www.youtube.com/watch?v=HQXXSq4kj5s)
### 3- Oyun alanı yönetim programı V3. (C#)
### 4- Node-JS local server ve socket-io. [yoy-io-server-local](https://github.com/ilyas9461/yoy-io-server-local)
### 5- Server program (c#)[YOY-Socket-ServerV1](https://github.com/ilyas9461/YOY-Socket-ServerV1)
### 6- Web tarafında çalışan uzak server Node-JS ve Socket-io [yoy-io-server-cloud ](https://github.com/ilyas9461/yoy-io-server-cloud)
### 7- VUE3 ile hazırlanmış Dashboard.
### 8- Wireless modüller (ESP8266) [socket-io-study](https://github.com/ilyas9461/iot-study)

## Çalışma Şekli
## Bölüm 1 : Kart Bilgilerinin Yerel ve Uzak Birimler Tarafından Paylaşılması:
Büyük bir oyun alanında ortalama haftalık ziyaretçi sayısı 1000-5000 arasında değişebilmektedir. Yoğun zamanlarda bir alana birden fazla PC konulabilmektedir. Örneğin iki veya daha fazla kart yükleme noktası oluşturduğunuz zaman kartların deposito durumları PC'ler arasında paylaşılmazsa PC'ler arasında kartlar birbirine karışmaktadır. Çok yoğun bir zamanda müşteriye ait bilgilerin her alanda tekrar takip programına girilmesi kuyrukların oluşmasına sebep olmaktadır. Kartlarda meydana gelen çeşitli arızaların (kontür silinmesi, oyuncağın kontürü çekip çalışmaması vb.) hangi alanda yada oyuncakta ne zaman meydana geldiğinin tespiti telafi yüklemelerinde işletmeci açısından önem arzetmektedir. Ayrıca işletmeci bir AVM ile anlaştı ise AVM işletmeciye farklı noktalarda yerler verebilmektedir. Bu durumda da kart bilgilerinin paylaşılabilir olması müşteri memnuniyeti ve artması için önemli hale gelmektedir. Bu sistemle kartlar için siyah liste oluşturulabilir ve kartın kullanımı sistemden kaldıralılabilir. Böylelikle kayıp-çalıntı kartın kullanımının da önüne geçilebilir.

Sistem mimarisi belirlenirken internet bağlantısının kopması gibi durumlarda düşünülmüştür. Her birimdeki PC verilerini hem kendisine hem de yerelde server PC olarak belirlenen PC'deki veri tabanına kaydetmektedir. Yerelde sistem modem aktif olduğu müddetçe internet bağlantısı olmasa bile kendi içersinde çalışabilmektedir. Birimlerde çalışan programlar web'e veri atarken bir takım gecikme sorunları olabilmekteyken,  programların verileri sadece kendilerine ve yerel server PC'deki veri tabanına atmalarının sağlanması ile de sistem çalışma hızı artmıştır. Server PC'de çalışan yerel server program yerel ağ ile web arasında köprü gibi çalışmaktadır. Her bir birimdeki program yapılan işleme bağlı olarak server PC'de çalışan node-js socket-io server'a belirlenen port üzerinden olay tabanlı bildirimler göndermektedir. Server PC'de çalışan server programda bu bildirimlere abone durumdadır. Gelen olay ve verisine göre gerekli işlemleri yapmaktadır. Olay-veriler socket-io yapısı üzerinden dolaşmaktadır. Web veri tabanına server program verileri göndermektedir. Böylelikle oluşabilecek birtakım güvenlik sorunlarının da önüne geçilmiştir. Başka bir internet bağlantısı üzerinden sisteme dahil olan birimler ise olay-verilerini web de çalışan node-js socket-io server'a göndermektedir. Bu programlar aynı zamanda direkt olarak web veri tabanına veri gönderebilmektedirler. Yerel de çalışan server program web de bulunan socket-io server bildirimlerine de üye durumdadır. Köprü görevini işte bu şekilde görür. Yerel deki olayları aynı zaman da web'e, web'deki olayları da yerele yayınlar. Bu şekilde verilerin iki yönlü paylaşımı sağlanmış olur.


## Kullanılan Teknolojiler

```bash
- C#, SocketIOClient
- Node js, Expres, socket-io 4.x
- MySql
- PICC, PIC24F
- ESP8266

```

###  Örnek çalışma videosu :

<a href="https://youtu.be/RWEq8n_fpZ4" target="_blank">
     <img src="https://camo.githubusercontent.com/241d4106ff5edca2ee25e04dcf4546fad9d20b626f7a10990307e8f83e95459f/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f796f75747562652d2532334646303030302e7376673f267374796c653d666f722d7468652d6261646765266c6f676f3d796f7574756265266c6f676f436f6c6f723d7768697465253232" alt="youtube">
</a>


## İletişim

- GitHub [@your-ilyas9461](https://github.com/ilyas9461)
- Linkedin [@your-linkedin](https://www.linkedin.com/in/ilyas-yagcioglu/)
