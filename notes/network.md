
############################

############################
# NETWORK
############################

############################

# network metrics
- __Bandwidth (or bant genişliği)__: maximum amount of data can be transferred in a unit of tme.
- __Throughput__: actual amount of data that is transferred.
- __latency (or gecikme)__: how long it takes data transferred fron end to other one.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Captive Portal (or Kısıtlama Portalı)
portal hem türkçe hem ingilizce kelimedir. "ana giriş kapısı" anlamına gelir. webportal gibi terimler bundan türemiştir.

Captive portal tekniği HTTP istemcisini interneti normal olarak kullanmadan önce ağ üzerinde özel bir Web sayfasını görmeye zorlar. Kısıtlama Portalı Web tarayıcısını kimlik denetleme cihazına çevirir. Bu, kullanıcı bir tarayıcı açıp İnternete erişmeye çalışana kadar porttan veya adresten bağımsız olarak bütün paketleri engelleyerek olur. Bu sırada tarayıcı kimlik denetleme ve/veya ödeme, ya da basitçe uygun kullanım poliçesini görüntüleyip kullanıcının onaylamasını sağlayacak Web sayfasına yönlendirilir. Kısıtlama Portalı uygulamaları en çok Wi-Fi erişim noktalarında kullanılır. Ayrıca kablolu kullanımı kontrol etmek için de kullanılabilir. (Otel odaları, iş merkezleri, vs.).

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# DNS over TLS (DoT) vs DNS over HTTPS (DoH)
Standart DNS client'lar, DoT ve DoH sunucularına istek yapamazlar. çünkü farklı protokollerdir. satndart dns'te isteğin çoğu açık gider/gelir. oysa DoT ve DoH 'ta istek tamamen şifrelenmiştir.

DoT soket bağlantısı açıp, o soketi üzerinden TLS ile dns sorgusu atar.  DoH ise http protokolünden yararlanarak DNS isteği atar.

Bu iki ptotokolün amacı ISP'lerden gizlenmek değildir. çünkü ISP, dns sorgusundan sonra, gideceğimiz IP adresini zaten görecektir. buradaki amaç;

- man-in-the-middle-attack'ı önlemek
- dns sorgusu yapılıp, cevabı şifreli bir bağlantıda kullanılacak ise güvenliği sağlamış oluruz
- ISP'lerin DNS sunucularındaki yaptığı engellemeleri ortadan kaldırmak

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# network interface

wifi, kablolu, loopback, sanal network interfaceleri aynı makinada olabilir.

java ile bunların listesi şu metod'dan geliyor: NetworkInterface.getNetworkInterfaces();

istediğimiz network interfacesinden soket açabiliriz. bir soketi o network adresine bind etmemiz yeterli olacaktır.

bazı interfaceler:

- eno1 yada em1 onboard or embedded network card (genelde anakart içinde olan kartlar)

- eth# genelde anakart dışında ekstra bir kart olduğunda

- w# wireles

- lo loopback

- vbox# virtualbox'un kendi içinde yarattığı networkler

- virbr# libvirt (kvm için sanal makine kütüphanesi) için kendi içinde kullandığı networkler

- docker# dockerın kendi içinde kullandığı networkler

bu isimleri driver'ın kendisi belirliyor. donanım değil. örneğin aynı donanımı, üçüncü parti geliştirilen açık kaynaklı ve daha sonra kendi resmi sitesindeki driver ile kullandığımızı varsayalım. ikisinde de farklı isim olabilir. eğer driver'dan bu isim algılanamaz ise; işletim sistemi kendi standartlarını kullanıyor. bu sebeple isimlendirmede kesinlik söz konusu değildir. birçok çeşit mevcut: fiberoptikler ayrı, kartın modeline göre yada bir özelliğine göre isimlendiren driver'ler de mevcut.

bir ağdayken her bilgisayarın değil, her network kartının bir ip'si vardır. işletim sisteminde bir yazılım uzak makineye bağlantı açsın. bu bağlantı sadece bir interface üzerinden sağlanabilir. eğer birden fazla NI varsa, destination ip'mize göre işletim sisteminde tanımlı olan routing table'lar aracılığı ile yazılım ilgili NI'a yönlendirilecektir. NI yollanacak datayı yollanacak yere ulaştıracaktır. fakat isterse yazılımlar diğer interfaceleri kullanabilir. NetworkInterface.getNetworkInterfaces() kodu ile interface listesi döndüğünde, listeden istediğimiz elemanı alabiliriz. array döndüğü için interface name'i önceden bilmek zorunda değiliz.

```java
Socket socket = new Socket();
socket.connect(new InetSocketAddress(remote_ip, port));
```

Yukarıdaki yerine aşağıdakini yapabilirsak, hangi interfaceden dışarıya datayı ileteceğimize biz karar vermiş oluruz:

```java
NetworkInterface nif = NetworkInterface.getByName("wlo0"); // interfacemizi önceden bildiğimiz varsaydık (yoksa ilk elemanı alabilirdik)
Enumeration<InetAddress> nifAddresses = nif.getInetAddresses(); // NI'ın IPv4, IPv6 adresleri array olarak dönmektedir.

Socket socket = new Socket(); //bu satır değişmedi
socket.bind(new InetSocketAddress(nifAddresses.nextElement(), 0)); // ipv4 adresi ile soketimizi bu NI'a bind etmiş oluruz. bu kısım olmazsa OS routing table'lara bakarak bizi uygun NI'ye attach edecekti.
socket.connect(new InetSocketAddress(remote_ip, port)); //bu satır değişmedi
```

# network interface card (or NIC or network interface controller)

network interface'ine denk gelen fiziksel kart.

# Loopback interface

ipconfig komutu ile görelebilen bu interface, tamamen sanal bir ağ bağdaştırıcıdır. bir donanımmış gibi davranır. Local makinanın DNS kayıtlarında ip adresi: 127.0.0.1'dir. Bu IP'nin hostname'i localhost'tur. bilgisayarın kendi içinde haberleşmesi için (örneğin local sunucuya istek yapmak için) kullanılır. cihazda hiç network kartı olmasa bile loopback vardır.
# multiple ip address to one interface

```java
NetworkInterface ni = NetworkInterface.getByName("wlp4s0");

ni.getInetAddresses(); //bu metod bize bir liste döner. bu listede ipv4 ve ipv6 adresleri vardır. bazen network manager sadece ipv4 yada ipv6'yı atamış olabilir.

ni.getInterfaceAddresses(); //getInetAddresses() ile aynıdır. ekstra olarak ip bilgisi yerine network class bilgisini de döner.
```

# virtual interface vs subinterface

örnek: A interface'inin sub-interface'leri olabilir. A'ya gelen istekler, hem A hemde onun sub'larına klonlanarak dağıtılır.

her subinterface, bir virtual interface'dir. oysa tersi her zaman doğru değildir.

# server socket vs client socket

```java
//sunucu taraftaki kod

ServerSocket serverSocket = new ServerSocket(8089); 

Socket clientSocket = serverSocket.accept(); //bu metod sürekli bekliyor

clientSocket.getPort(); // returns random port number (X no'lu port olsun)

clientSocket.getLocalPort(); // returns 8089

//client taraftaki kod:

Socket socket = new Socket(IP_OF_SERVER, 8089);

socket.getPort(); // returns 8089

socket.getLocalPort(); // returns random port - yukarıdaki ile aynı port numarası (X)

yukarıda görüldüğü gibi; accept işlemi sonrası hala haberleşme server-soket portu (8089) üzerinden devam ediyor. fakat paralelden server-soket o porttan dinlemeye devam ediyor. 
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# DNS (or Domain Name System)
internet adres resolving sistemini temsil eden genel bir terimdir. 

__DNS Server (or Name Server)__ ise IP'leri resolving yapmakla yükümlü yazılımdır. Bazen __Domain Name Server__ denir fakat yanlış bir kullanımdır.

# International Corporation for Assigned Names and Numbers (or ICANN)
2019 yılı itibariyle en yetkili kuruluştur. Amerika'ya bağlıdır. __registrar (or kaydedici)__ firmalar (örnek: godaddy) ICANN'dan lisans alıyorlar.

# IANA (or Internet Assigned Numbers Authority)
ICANN için gerekli bazı teknik konuları tamamlayan kuruluştur.

# RIR (yad Regional Internet Registry)
ICANN ve IANA, dünyanın 5 farklı bölgesinde yetkilendirilmiş kuruluşlar vardır. Bu kuruluşlar kendi bölgelerinden sorumludur.

- AfriNIC
African Region Internet Registry: Afrika

- APNIC
Asia Pacific Network Information Centre: Asya ve Pasifik

- ARIN
American Registry for Internet Numbers: Kuzey Amerika

- LACNIC
Latin America and Caribbean Internet Addresses Registry: Latin Amerika ve Karaibler bölgesi

- RIPE NCC
Réseaux IP Européens Network Coordination Centre: Avrupa bölgesi.

RIR alanları yukarıda yazıldığı kadar keskin çizgilerle ayrılmaz. Örneğin, ARIN bölgesi esas olarak Kuzey Amerika olmakla beraber Güney Amerika ve Afrikaya da servis verir. RIPE bölgesi esas olarak avrupa olmakla beraber ortadoğu ve orta-asya içlerine kadar servis vermektedir. Türkiye RIPE NCC bölgesindedir. RIPE NCC'nin merkezi Hollanda’dadır.

# LIR (or Local Internet Registry)
kullanıcıya IP veren kuruluşlardır. ISP (or Internet Sevice Provider)'lere denk gelir. Yasal anlamda şirketi olan herkes bu görevi alabilir.

# root servers
DNS sunucuları tüm domain bilgilerini saklayamaz. local cache'inde yok ise, root server'lara sorar. root server dünor 12 adettir (yıl 2019). bunlar ICANN tarafından belirlenmiştir. fakat sadece 1 tanesi ICANN kuruluşa direk bağlı bir sunucudur. bu sunucuya __ICANN Managed Root Server (or IMRS)__ deniyor. diğerlerinin ICANN'a bağlı olmamasının sebebi, merkezi yönetimden kaçınmaktır.

ICANN'ın resmi sayfası olan www.dns.icann.org sitesinde root-servers.org'a referans verilmiştir. buradan 12 server'ı görebiliriz.

12 root-server'ın bilgileri DNS server yazılımlarında 'Root Hints File'a kaydedilir.

# whois server
registrar'a yeni bir domain eklendiğinde, registrar bu bilgiyi o domainin uzantısının sorumlusu olan "whois server"'a yollar. örneğin .com ve .net alan isimleri için verisign şirketinin whois sunucusu merkezi sunucudur. daha sonra bu bilgi diğer üçüncü parti whois server'lar tarafından klonlanır.

Dolayısı ile; root server'lar dahi .com ve .net için gerekli tüm domain'leri local'lerinde tutmazlar.

Versign firması ICANN'a bağlıdır ve ICANN tarafından yetkilendirilmiştir.

ICANN'dan her firma godaddy gibi kolayca yetki alamaz. fakat godaddy'ye kolayca aracılık edebilir, yani godaddy'nin bayisi olabilir.

# hostname vs domain name
domain name bir bilgisayara DNS sunucusu tarafından atanmış string'dir. oysa hostname local bir network'te her makinanın kendisini dışarıya tanıttığı isimdir. network içinde hostname kullanılırken, dışarıya gidişlerde domain kullanılır. dışardaki bir yere giderken, oradaki networkteki bir alt makineye erişmek istediğimizde hostname.domainname.com gibi bir adresten yararlanılır. hostname ve domain name aynı görevi görür. www internet tarayıcıları için gerekli varsayılan makinanın hostname'idir.

# subdomain
mail.google.com, map.google.com'deki mail ve map birer subdomain'dir. ayrı IP'leri vardır. fakat istenirse aynı IP'ye de yönlendirilebilir.

# domain'i hosting'e bağlama
wix.com bizim sayfamızı barındırıyor (sunucu hosting firmamız) olsun. godaddy.com'dan da domainimizi almış olalım.

- wix.com'a domain-name'imizi bildiriyoruz.
- wix.com bize wix'in kendi dns'lerini veriyor. bunlar genelde ns1.wix-dns.com tarzında URL'ler oluyor. 
- godaddy'de o domaine ait nameserver'larımızı tanımlıyoruz. bunun için godaddy'ye login oluyor, ilgili domainimizi seçiyor, ayarlarına giriyor ve nameserver alanlarımızı dolduruyoruz. burada birden fazla nameserver olabilir. çünkü yedek nameserver olabiliyor.

Artık domanimize istek yapıldığında, godaddy dns sorgusunu yapanı ns1.wix-dns.com'a yönlendiriyor. ns1.wix-dns.com gelen sorguyu görüyor ve onu sunucu bilgisayarın IP'sini dönüyor.

Bu örnekte godaddy'ye veridğimiz dns sunucuları bizim kendi kişisel sunucularımız olabilir. Genelde büyük firmalar kendi dns suncuularını kullanıyor.

# fully qualified domain name (or FQDN)
hostname + domain name birarada olduğunda verilen isimdir. örnek: tr.wikipedia.com, www.wikipedia.com...

# top-level domain (or TLD)
.com, .org, tr gibi terimlere verilen isimdir. TLD'nin çeşitleri vardır:

- # country code top-level domain (ccTLD)
  .tr, .fr, .de, .us gibi ülke bazlı gruplma için gerekli domain bilgisini ifade eder.

- # generic top-level domains (or gTLD)
  .com, .org gibi kurumların tipini belli eden domain ifadeleridir.

# domain levels
example: mail.google.com

- 1st level domain (or first-level domain)
  
  com

- 2nd level domain (or second-Level domain)

  google

- 3rd level domain (or third-level domain)

  mail

# DNS sorgu tipleri

  - # Özyinelemeli (or Recursive) Sorgu
    dns sunucusuna yapılan sorgu isteğidir. örneğin browser'ın ISP sunucusuna yaptığı sorgu isteği.

  - # Tekrarlamalı (or Iterative) Sorgu
    DNS sunucuları kendi local'lerinde dns bilgisini bulamaz ise diğer dns sunucularına sorabilir. işte bu sorgular (dns'lerin kendi aralarında kullandığı sorgular) Tekrarlamalı Sorgu olarak adlandırılır.

# Ters DNS Çözümlemesi (or Reverse DNS lookup or reverse DNS resolution or rDNS)
  IP'den dns bulma işlemidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# CCNA (or Cisco Certified Network Associate)
- Cisco kurumumun verdiği network sertifikaları grubudur. altında birçok çeşit sertifika barındırır: güvenlik, data center teknolojileri, bulut bilişim gibi...
- en çok bilinen sertifika "CCNA Routing and Switching"'dır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# imap (or Internet Access Message Protocol) vs pop3 (or Post Office Protocol version 3)

ikiside birer mail sunucu ile haberleşme protokolleridir. imap, pop3'ten daha gelişmiştir.

# smtp (or Simple Mail Transfer Protocol)
imap ve pop3 gibi client-sunucu arasındaki mail protokolüdür. ek olarak smtp; sunucular arası mailleşmek içinde kullanılabilmektedir.

# mail sunucusu
mail suncusu diğer emaillerle haberleşen yazılımdır. tabi client'lar ile de haberleşir. mailleri clientlardan alır ve kaşı tarafa email atar. bunları backupunu da tanımlı veritabanında saklar. fakat saklmak zorunda değildir.

# mail client
mail client'lar mail suncusu tarafından sağlanmak zorunda değildir. web client, mail sunucusuna mail suncunun açmış olduğu API ile erişir.

# Microsoft Exchange
sunucu yazılımının ismidir. herkes kendi local networküne kurabilir. mail sunucusu görevinin yanında birçok ek işlev de sağlamaktadır.

# Messaging API (MAPI)
Microsoft tarafından kullanılan IMAP gelişmişi protokoldür. temel amacı email olsada birçok ek işleve destek vermektedir.

# CC (or carbon copy)
Carbon türkçe kelime anlamı: kopya kağıdı

carbon copy türkçe kelime anlamı: kopya, tıpatıp benzeri

# BCC (blind carbon copy)
diğerinin göremediği alıcı.

# Multipurpose Internet Mail Extensions (MIME)
SMTP mail ptokolü ile birlikte artık emaillerde text yerine farklı tiplerde datalar kullanılabilmektedir. MIME bu standartın ismidir.

# MIME Type
MIME desteği ile gönderilen emaillerde, gönderilen data tipidir. Bu tipi yazmak için belirli bir standart format vardır: formatın-ailesi / format-uzantısı. örneğin: application/pdf, text/html, image/png

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# DMZ (or demilitarized zone or perimeter network)
Örnek üzerinden gidilirse; bir şirket ağında tüm iç networkün önünde bir güvenlik duvarı vardır. Dışarıdan içeriye giriş yoktur yada kısıtlıdır. Fakat bazı müşterilerin erişebileceği, yada tüm halka açık bir alt ağ olmasını isteyebilirsiniz. Bu alt ağa verilen özel isim DMZ'dir.

DMZ için modem ayarlarından bir ip verilir. bu ip; bir makineye yada alt ağa erişimi sağlayan bir router'a ait olabilir. artık modeme gelen tüm istekler aynı şekilde o ip'ye iletilir. bu durumda dmz dışında kalan cihazlar ne yapacaktır? dmz ip'si, sürekli olarak tüm portları kullanmadığından diğer portlardan boş olanlar diğer makinelere tahsis edilecektir. ama her zaman öncelik dmz makinasında olmalıdır. dmz aarları ile diğer makineler için yapılan port forwardingler çok karışık/conflict bir durum yaratabilir. 

# local area network (or LAN or yerel alan ağı)
kısıtlı bir alandaki network'e verilen genel isimdir.

# wide area network (or WAN or Geniş alan ağı)
büyük coğrafik alanlardaki üst ağa verilen genel isimdir. WAN, LAN gibi terimlerin uygulama bazında kesin bir karşılığı yoktur. WAN genelde piyasada; internet servis sağlayıcıları (or internet service provider or ISP) 'nın networkü için kullanılır. çünkü en geniş coğrafya'ya onlar hizmt vermektedirler.

# metropolitan area network (or MAN or Metropol alan ağı)
wan ve lan arasındaki büyüklükteki network'lere verilen genel isimdir. WAN ile ülkeler ve ehirler birbirine bağlanırlar. Fakat şehirler veya ilçeler kendi içlerinde MAN diye  bir altağda olurlar.

# intranet
şirket içi (yada özel bir amaç için) networke verilen takma isim.

# Ekstranet (or extended intranet or extranet)
intranete ek olarak organizasyona bağımlı tedarikçiler, müşteriler için genişletilen ağdır. internet ağı buranın dışında kalır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# iptables
netfilter projesi altında geliştirilen, linux üzerinde çalışan bir komut satırı uygulamasıdır. ip/port filtrelemesi yapar. güvenlik duvarı görevi görür.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Samba
windows harici sistemler için yazılmış, açık kaynaklı dosya paylaşım yazılımıdır. gene olarak dosya paylaşım mekanizmalarında; bir dosya paylaşım yazılımı hem sunucu hem client görevi görebilmektedir. dosya paylaşımı yapıldığında sunucu kısmı, başka makineden dosya okuma işlemleri client modülleri ile gerçekleşir. samba her iksini birlikte yapabilmektedir.

# SMB
windowsun dosya paylaşım protokolüdür. samba yazılımıda bunu desteklemektedir. smb protokolünün birçok türevi ve sürümü vardır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# DHCP (or Dynamic Host Configuration Protocol)
Network'e IP atayan uygulamadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# broadcast (or yayın)
network üzerinde bir paket yollandığında bir IP belirtilerek yollanır. Fakat her alt ağda bir broadcast Ip'si vardır. bu ip'ye atılan paketler, tüm alt ağa komple gönderilir.

# Multicast
network üzerinde belirli bir IP uzayına yapılan yayındır.

# Unicast
Network üzerinde sadece 1 adet IP ye iletilen yayındır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Subnet (or Alt ağ or subnetwork)
IP blokları gruplanarak; alt ağlar meydana getirilir. Bu şekilde hem gruplama yapılmış olur, yönetimi daha kolay olur ve broadcasting işlemleri networku daha az yorar (çünkü sadece ilgili alt ağa broadcast yapılacaktır).

bir network'ü subnetwork'lere ayırma işlemine __subnetting__ denir.

# subnet altındaki özel IP'ler
192.168.1.0/24 --> 24'ten bu çıkıyor: submask = 255.255.255.0 --> 256 tane ip olabilir bu ortamda (bu subnet'te). 192.168.1.0-192.168.1.255 ip aralığıdır.

- network-id -> 192.168.1.0 (bunu kullanamazsın ve bir cihaza atanmaz. bu sadece bir göstergedir.)
- broadcast ip --> 192.168.1.255

# default gateway (or varsayılan ağ geçici)
subnet'te network'te bulamadığımız ip'leri default gateway'a yollarız. bu şekilde ilgili yönlendirmeleri artık ona bırakmış oluruz.

genelde subnet'teki ilk kullanılabilen IP yada son IP veriliyor. fakat istenilen herhangi bir IP'de gateway olarak verilebilir.

# Subnet Mask (or IP Mask or altağ maskesi or IP maskesi)
İki makine birbiri ile aynı ağda olup olmadığını IP ve "IP Mask" değerlerini kullanarak anlayabilirler. "IP Mask" değeri bir altağda herkeste aynıdır.

Örneğin; Aynı networkte, IP maskesi 255.255.255.0 ise, tüm makinelerin IP'lerini ilk 3 sekizliği (yani ilk 24 biti) diğer karşılaştırılan IP ile aynı olmak zorundadır.

# Classless Inter-Domain Routing (or CIDR or Sınıfsız alanlar arası yönlendirme)
Classful network'e alternatif olarak sonradan çıkmıştır.

255.255.255.224 bit bazında yazıldığında: 11111111 11111111 11111111 11100000, 27 tane "1" bit olduğundan, "/27" class network olarak sınıflandırılır. Burtadaki 1 bit sadece gösterim amaçlıdır. Fakat kastedilen şudur: "1" yazan basamaklar, o subnetteki IP'ler tarafından değiştirilemiyor. Yani o kısımlar gerçekten "1" olmak zorunda değil. 

# subnetting örnek değerler
örnek 128'lik bloklar halinde subnetler oluştursak bu değerler olacaktır:

192.168.1.0/25 --> 25'ten bu sonuç çıkıyor: submask = 255.255.255.128  --> 128 tane ip olabilir.

192.168.1.128/25 --> 25'ten bu sonuç çıkıyor: submask = 255.255.255.128  --> 128 tane ip olabilir.

192.168.2.0/25 --> 25'ten bu sonuç çıkıyor: submask = 255.255.255.128  --> 128 tane ip olabilir.

192.168.2.128/25 --> 25'ten bu sonuç çıkıyor: submask = 255.255.255.128  --> 128 tane ip olabilir.

192.168.3.0/25 --> 25'ten bu sonuç çıkıyor: submask = 255.255.255.128  --> 128 tane ip olabilir.

64'lük subnetwork'lere bölseydik:

192.168.1.0/26 --> 26'ten bu çıkıyor: submask = 255.255.255.192  --> 64 tane ip olabilir.

192.168.1.64/26 --> 26'ten bu çıkıyor: submask = 255.255.255.192  --> 64 tane ip olabilir. (örnek bu ortamda 64 ile 128 arasındaki ip'ler tanımlanabilir)

# Classful network

Aşağıdaki tabloda her "A" (bit değeri), ilgili subnet için değiştirilemez değerdir. Yani ilgili subnet'te hangi IP'yi kullanırsak kullanalım, ancak "x" olanları kullanabiliriz. "A" olanları kullanamayız. A olanlar o subnet için sabittir.

| Class   | IP (bit bazında)                | sub id (CIDR terminologisindeki id'si) |
|---------|---------------------------------|----------------------------------------|
| Class A | AAAAAAA.xxxxxxx.xxxxxxx.xxxxxxx | /8                                     |
| Class B | AAAAAAA.AAAAAAA.xxxxxxx.xxxxxxx | /16                                    |
| Class C | AAAAAAA.AAAAAAA.AAAAAAA.xxxxxxx | /24                                    |
| Class D | AAAAAAA.AAAAAAA.AAAAAAA.AAAAAAA | /32                                    |
| Class E | özel durumlar için ayrılmış     |                                        |

Sub-id "/12" gibi farklı bir değer olursa, ona özel isim verilmemiş. Bu tarz sınıflara "classless subnet" deniliyor.

# subnetting example
Subnetting örneği yapalım: 2 pc var. 2 router. 2 pc farklı subnetlerde. bunun ağ yapısnı ip'leri ile gösterek çizelim.

Her subnet'te total 4 ip'ye ihtiyaç var: 1 PC + network ID + 1 default gateway (router) + 1 brodcast

bu durumda subnet'ler 4'lü olarak bölünecek.

255.255.255.252 = 11111111.11111111.11111111.11111100 --> subnet mask (Burada 4 IP yok. 3 IP var. fakat subnetmask'larda hespalama hep 1 fazlası olacak şekilde yapılır.)

subnet mask'te 30 adet "1" var.

192.168.1.0 / 30 --> CIDR gösterimi

Network-1:
- network-id         192.168.1.0
- PC-1               192.168.1.1
- router-1           192.168.1.2 (this is network-1's gateway)
- broadcast ip       192.168.1.3

Network-2
- network-id         192.168.2.0
- PC-2               192.168.2.1
- router-2           192.168.2.2 (this is network-2's gateway)
- broadcast ip       192.168.2.3

Network-3
- network-id         192.168.3.0
- router-1           192.168.3.1
- router-2           192.168.3.2
- broadcast ip       192.168.3.3

çizim:

```
                (network-3)
############                      ############
# router-1 # ******************** # router-2 #
############                      ############
   *                                  *
   *                                  *
   *(network-1)                       *(network-2)
   *                                  *
   *                                  *
########                            ########
# PC-1 #                            # PC-2 #
########                            ########
```

Tek bir subnet'i bizim için oluşturan hesaplayıcıdan da buna benzer hesaplamaları basitçe görebiliriz: http://jodies.de/ipcalc?host=192.168.1.0&mask1=30&mask2=

Yukarıdaki network örneğinde PC-1, PC-2'ye direk istek atmak istediğinde atamayacaktır. Bunu yapabilmek için aşağıdakilerdne en az 1 tanesini yapmak gerekiyor:
- router-1 ve router-2'ye özel tanımlama yapmak
- network-3'ün gateway'ına ve router-2'ye özel tanımlama yapmak

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# TCP Socket states

- LISTEN - sunucu - soket gelebilecek bağlantıları bekliyor

- SYN_SENT - client - soket bağlantı kurmak için karşıya istek yapıyor durumda

- SYN_RECV - server - client server-sokete bağlanma isteği yolladı, server kabul etti, ve son onayı tekrar client'tan bekliyor durumda

- ESTABLISHED - sunucu ve istemci - soket bağlantı kurmuş durumda

Buradan aşağıdaki tüm durumlar kapatılma ile ilgili:

- FIN_WAIT1 - sunucu ve istemci - bağlantı sonlandırma bildirisi yollandı. cevap bekleniyor.

- FIN_WAIT2 - sunucu ve istemci - FIN_WAIT1 ile gönderilen bağlantı sonlandırma isteğine, uzak soket onay döndü. artık uzağın bağlantısını kapattığına dair son onayı yollaması bekleniyor. bu bekleniyorken karşıya hiçbir şey atılmıyor. yani; paket alındı, tekrar yeni paket bekleniyor.

- TIME_WAIT - sunucu ve istemci - Uzak soket bağlantıyı kapattığına dair son onayı yolladı. soket closed duruma geçiş için son procesi yürütüyor.

- CLOSED - sunucu ve istemci - bağlantı sonlandırıldı.

- CLOSE_WAIT - sunucu ve istemci - karşı taraf, katapma bildirisini bize gönderdi. Karşı tarafa bildiri alındığına dair onay yollanır ve soketi kapatma işlemine geçilir. soketi kapatma işlemi için yazılımın onay vermesi gerekir. bu yüzden bu statüde takılan birçok soket oluyor.

- LAST_ACK - sunucu ve istemci - CLOSE_WAIT sonrası Soket kapatıldığında, son olarak kapatıldı bilgisi karşı tarafa gönderilir. gönderildiğinde bu soket CLOSED olur.

# acknowledgement (or acknowledgment or ack)
protokol içerisindeki onay mesajıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Quality of Service (QoS)
Genel bir ismi var fakat özel olarak; internet ağı içinde network'te giden gelen paketlere öncelik vermek için gerekli yapılandırma ve ayarlar bütünüdür. Örneğin modem, voip ve http üzerinden isteklere, download edilen bir dosyadan daha fazla öncelik verir. Bu sadece bir parametredir. bunun gibi bir çok önlem alınabilmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# VPN (or Virtual Private Network)

B bilgisayarı ve N networku var. B'nin N networkü üzerinde çalışması isteniyor fakat ayrı networkteler. bu durumda vpn kullanılıyor. b bilgisayarına ve N network'unden bir X bilgisayara vpn yazılımı kuruluyor. X üzerindeki yazılım, kendi işletim sistemi üzerinde bir sanal network kartı oluşturuyor (ipconfig ile görülebilir). X bu sanal kart ile, N'in DHCP'sinden ikinci bir IP'yi alıyor. İkinci IP'yi B bilgisayarı için ayırıyor. B üzerindeki yazılım ve X üzerindeki yazılım artık direk birbirleri arasında bağlantı içerisinde işlemleri yapmaya başlıyorlar.

Bu senaryoda X bilgisayarı 24 saat açık kalmalı ki B isteği zaman bağlanabilsin. BUnun yerine modem'ler vpn destekli olursa, vpn konfigurasyonları modeme yapılıyor, modem aracılığı ile B bilgisayarına DHCP'den ip atanıyor ve aynı işlemler gerçekleştiriliyor.

Bu 2 senaryoda da, modemin içindeki yazılım veya X bilgisayarına kurulan yazılım sunucu uygulaması oluyor.

VPN yazılım katmanında olduğu için bir çok özellik sunabilir. Örneğin; vpn yazılımı belirli IP'ler dışındaki isteklere çıkışınızı engelleyebilir, şifreleme yöntemlerini değiştirebilir, güvenlik için paketleri inceleyebilir, log sistemi olabilir, GUI sunabilir, bir yazılımın VPN üzerinden gitmesine ayarlarken, diğer yazılımların istedikleri yerden çıkmaları sağlanabilir.

Android 5 ile bir uygulama root yetkisi istemeden, diğer uygulamarı vpn üzerinden iletişimini sağlayabilir.

VPN bu yapının genel ismidir. Altında bir çok protokol, bu protokollerden yararlanarak bağlantı kurmamızı sağlayan birçok bulut hizmet, ve bu bağlantıları sağlayan yazılımlar mevcuttur.

# OpenVPN
Açık kaynaklı VPN uygulaması ve protokolüdür. Aynı zamanda yazılımı geliştiren firma, openvpn protokolü ve yazılımları ile bulut vpn hizmeti de sunmaktadır.

# Proxy server (or Vekil sunucu or yetkili sunucu)
A bilgisayarı istekleri önce P bilgisayarına gönderir. P bilgisayarı bir proxy'dir. bu istekleri dışarıya aktarır ve dönen değerleri direk A bilgisayarına gönderir. P bilgisayarı burada bir proxy'dir. Amacı aracılık yapmaktır. Bunun bir çok sebebi olabilir:

- aynı proxy'den çıkanlar için cache mekanizması yapmak.
- yasaklı internet sitelerine erişmek.
- gidilen yere yavaş gidiliyor ise proxy hızı ile bu süreyi kısaltmak.
- siteleri yasaklamak
- proxy ile istekleri filtreleyip/inceleyip güvenliği sağlamak gibi.
- istekleri log'lama yapmak

# vpn vs proxy
consept olarak farklı olsalarda teknik altyapı incelendiğinde birbirinin görevlerini tamamlayabildikleri görülür. fakat ikisinin amacı farklı olduğundan çok farklı özellikleri vardır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Network Address Translation (or NAT or Ağ Adresi Dönüştürme)
Router'ın bir IP adresi olsun. Bu router'ın arkasında birden fazla cihaz olabilir. Yani bir (çıkış) IP'yi birçok cihaz kullanmaktadır. Yönlendirici kendi içinde haritalama yaparak kimin hangi IP'yi kullandığını belirleme mekanizmasıdır. Bu mekanizmanın birden fazla yöntemi vardır:

  - # Static NAT
    Routerlarda çıkış IP'si tek olmayabilir. Bize bir çıkış IP aralığı verilmiş olabilir. Böyle durumlarda içerideki her cihazı, sabit olarak bir çıkış IP'sine haritaladığımızda bu yöntemi kullanmış oluruz.

  - # Dynamic NAT
    Static ile aynı mantıkta çalışır. Tek farkı hangi IP'nin hangi çıkış ile gideceğine router o sıra karar verir (önceden belirlenmez).

# Port Adres Çevirimi (Port Address Translation or PAT or NAPT or Network PAT)
Overloading (aşırı yüklenme) olduğu zamanlar tercih edilen NAT yöntemidir. Örneğin; bir çıkıp IP'miz var. İçerde ise on tane makinamız. Bu durumda router, içerdeki her IP'nin her IP:PORT'u çıkıştaki bir IP:PORT'a bağlar. çıkışta bir adet IP'miz olduğundan maximum TCP soket portu sayısı kadar farklı bağlantı kurbiliriz. Bu durumda localde 2 makina olsun, 2 makina birde 65bin adet portunu aynı anda kullanamayacaktır.

# Port yönlendirme (or port mapping or port redirection)
Router ayarında olan bir özelliktir. Dışarıdan X portuna gelen bağlantılar, local tarafta A IP'li bilgisayarın Z portuna yönlendirilmesi sağlanabiliyor.

# Port Triggering (or Port tetikleme)
ort yönlendirme ile aynı şeydir. sadece ek olarak; yönlendirilen port kullanılmadığında kapalı kalır. bu şekilde ek güvenlik sağlanır.

# virtual servers
port forwarding ile aynı şeydir. fakat bu terim sadece external port ve internal port aynı olduğu zaman kullanılır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# fiziksel network aygıtları
- ## Hub
  Yerel ağ oluşturmak için gerekli cihaz. Sadece veriyi alıp dağıtmak için kullanılır. Bir özelliği yoktur. Gelen veri-paketlerini bağlı olan tüm kablolarına dağıtır.

- ## Switch (or switching hub or bridging hub or MAC bridge or dağıtıcı or ağ anahtarı)
  Hub ile aynı görevi görür. Fakat hub'dan daha zekidir. Gelen paketi inceleler ve hangi port'a (kablo girişine) o bilgi gönderilecekse, sadece oraya aktarır. Gereksiz ağ trafiğini de engellemiş olur. Bu işlemi yaparken MAC adreslerine bakıp yapar. IP'ye göre dağıtım yapmaz.

- ## Router (or Yönlendirici)
  Router'lar switch'lere benzer mantıkta çalışırlar fakat bağlı olan bilgisayarları değil, network'leri birbirine bağlarlar. Bu yüzden genelde az portu olan bir cihazdır. 
  
  son kullanıcıya satılan router'lar içerilerinde switch teknolojisi ile entegre gelirler. bu şekilde router sonrası switch alma gereksinimini ortadan kaldırır. bu yüzden piyasada, çok porta sahip router'lar görebiliriz.
  
  switch, LAN içerisinde MAC adreslerini bilir ve ona göre paketleri filtreler. Oysa router, IP adreslerini bilir. network'leri birbirine bağlar.
  
  router bir firewall modülü de içerebilir.

- ## Modem
  Dijital-analog sinyal çevirimini yaparak verilerin kablo üzerinden iletilmesini sağlar. Bu yüzden ismini modulator-demodulator kelimelerinden almaktdır. Son kullanıcıya sunulan modem'lrde çoğunda router modülü entegre gelir. bu şekilde router almaya gerek kalmaz.

# Ağların fizisel iletişim çeşitleri

- # Dial-up Internet access (or Çevirmeli ağ)
  telefon standartlarını (kablolarını) kullanarak erişimin sağlandığı fiziksel yöntemdir. Max hız 56 kbit/s'dir.

- # digital subscriber line (DSL)
  bakır kablo ile iletişim sağlanan iletişim yapısıdır. xDSL olarak adlandırılırlar. x yerine kullanılan teknolojinin harfi gelir: aDSL, vDSL gibi.

- ## Fiberoptik
  Metal kablolar yerine fiber kablolar kullanılır. fiber kablolar cam veya plastik'ten meydana gelmektedir. ışık ile veri iletimini sağlar. metal kalbolara göre temel avantajları: manyetik alandan hiç etkilenmemeleri ve daha diğer gürültü çeşitlerinden daha az etkilenmeleridir.

- ## uydu

- ## kablo (or cable)
  Kablo kelime anlamı olarak tüm kablo çeşitlerini kapsamaktadır. Fakat local ağlarda iletişim için kullanılmak üzere geliştirilmiş özel network kabloları vardır.

# Sinyal çeşitleri

- ## Dijital Sinyal (or sayısal signal)
  Bu sinyalde iki değer vardır. Bu iki değer 1 ve 0 dır. Bu iki değer farklı şekillerde adlandırılabilir. Açık ve kapalı,doğru ve yanlış,yüksek ve düşük gibi.

- ## Analog sinyal (or analog signal)
  Yönü ve şiddeti zamanla değişen sinyallere denir. Analog sinyale en güzel örnek ses sinyalidir. Digital sinyallerde max 1, min 0 olarak temsil edilirken, analog'da bu değer herhangi bir sayı aralığı olabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Access Point
bilgisayarın ilgili iletişim ağından erişilen ilk noktadır. Örneğin bir bilgisayar bir wifiye erişiyorsa, wifi cihazı bir access point olur. aynı şekilde wifi haricindeki örneklerde verilebilir. fakat günlük hayatta halk arasında genelde sadece wifi için bu terim kullanılmaktadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Ethernet
Sadece kablo aracılığı ile cihazlar ararsı iletişim kurulması için gerekli standratlardır. Wi-Fi ise radyo dalgaları (radyo: elektrik dalgalarının özelliğinden yararlanarak seslerin iletilmesi sistemi) ile iletişim kurma standardıdır.

# IEEE 802
Tüm network iletişim standratlarının tanımlandığı standartlar ailesidir. ALtında birçok standart vardır. Bu standartlar yanında numara ve karakterlerle temsil edilirler. Örneğin; IEEE 802.11 kablosuz ağ standartlarıdır. 802.11g kablosuz ağ starndartlarının bir sürümüdür. IEEE 802.3 ethernet standartlarıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# fiziksel telefon ağ yapıları

- ## Plain old telephone service (or POTS or plain ordinary telephone service)
  Bazı kaynaklarda "classic telephone system (or klasik telefon sistemi)" olarakta isimlendirilmektedir.

  eski usul analog telefon iletişim protokolüdür.

- ## ISDN (or Integrated Services Digital Network or Tümleşik Hizmetler Sayısal Şebekesi)
  en eski usul telefonlardan sonra çıkan ilk dijital telefon altyapısıdır. internet ağı üzerinden haberleşmez. Kendi özel bir ağdır. Fakat ISDN, video ve görüntü aktarımı da yapabilmektedir.

# internet telefonu
internet bağlantısı kullanılarak haberleşmeyi sağlayan altyapılara verilen genel isimdir. internet telefonları direk internet kablosuna bağlıdır. içerisinde yazılım gömülü gelir ve internetten (skype, whatsapp'ın yaptığı gibi) sesli veya görüntülü konuşmayı sağlar. (Not: Görüntülü konuşmaya imkan veren her telefon, "internet telefonu" olmak zorunda değil. "ISDN" hatları da görüntülü konuşmayı desteklemektedir.)

# VoIP (or voice over ip)
yazılım protokolüdür. genel bir isimdir. cihazlar aracılığı ile paketler diğer telefon altyapılarına çevrilecek şekilde kolay tasarlanmıştır. bu şekilde internet üzerinden, normal telefonlar ile konuşulabilmektedir. normal telefonlardan daha ucuz olabilirler. çünkü normal telefon hatları mesafeler uzadıkça daha maliyetli olmaktadır. fakat voip hizmeti sunan sunucular, bizi internet ağı üzerinden ulaşacağımız telefona en yakın yere yönlendirip, yönlendirdiği endpoint üzerinden paketleri çevirerek normal telefon hattı olan bir yere bağlamaktadır. bu da maliyeti ucuzlatmaktadır.

# SIP (or Session Initiation Protocol)
özel bir voip protokolüdür.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# UPnP (or Universal Plug&Play or Evrensel Tak&Çalıştır)
Elektronik cihazların internet ağı üzerinde biribirini otomatik algılaması için geliştirilen bir protokoldür. Ağ'ı yöneten router'ın UPnP desteği olması ve çalışan yazılımın (elektronik cihaz içerisindeki) UPnP supportu olması şarttır.

örneğin UPnP destekli modemler, modeme bağlı client'lardan aldığı komutlar doğrultusunda port yönlendirme yapabiliyor. böylece örneğin vnc içerisindeki bir seçenek ile port yönlendirme yapılmış oluyor ve teamviewer gibi merkezi sunucuya ihtiyaç kalmıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Delik Açma (or Hole Punching)
Teamviewer gibi port yönlendirmenin yapılmaması istenen sistemlerde birbiri ile haberleşmesi gereken makinalar söz konusudur. böyle durumlarda merkezi bir sunucu ihtiyacı vardır. bu sunucu "S", "A"  ve "B" makinelerinin haberleşmesini sağlar. Öncelikle A  ve B, S'e bağlanır. S, A'ya b'nin, b'ye de a'nın bilgilerini verir. artık a yada b programın ihtiyacına göre sunucu gibi davranır ve yeni bir soketten dinleme yapmaya başlar. örneğin; a dinleme yapmaya başladı. b ise anın portunu biliyor. bu yöntem ile artık b a ile soket üzerinden haberleşebilir. bu yöntem'e delik açma yöntemi denir.

bu yöntem her zaman %100 temiz çalışmayabiliyor. zira router'ların nat sistemi her zaman beklenilen gibi işlemeyebiliyor. örneğin; dışarıdan  bağlantı gelince router bunu tehlike olarak görüp portu kapatabilir. yada local-external port arada değişebilir vs... bu sebeple son kullanıcı uygulamalarında bu teknik kullanılmaz. teamviewer gibi uygulamalarda teamviewer'ın sunucusu a'dan b'ye ekran görüntülerini kendi üzerinden aktarır. yani tüm transfer edilen veriler teamviewer sunucuları üzerinden geçer. teamviewer sunucusu yazılımsal aracı görevi görür.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Encapsulation
OSI TCP layer'daki gibi bir protokolün, alt protokole data yerleştirmesidir. tersi (__decapsulation__) ise alt protokoldeki dataların üst protokollere taşınmasıdır/yerleştirilmesidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# routing table (or routing information base or RIB)
router içinde yada bilgisayarda (OS'ta) tanımlı olan bir tablodur. bu tabloda hangi ip'ye gidildiğinde bizi nereye yönlendireceği belirtilir. normalde; bir bilgisayar bir ip'ye gitmek istediğinde network'te bağlı olduğu router'a paketi atar ve paket router tarafından gerekli yere yollanır. fakat bazen;

- uzak networkteki iç bilgisayarlara özel bir yönlendirme yapmak zorunda kalabiliriz

- hızlı routing olması amaçlı bildiğimiz makinelere routing yaptırabiliriz

- farklı network kartlarından (sanal yada fiziksel kartlardan) hangisinden çıkacağımızı belirlememiz gerekir

gibi...

örnek routing table listeyen komut:

```sh
route -n
# or "ip route"
# or "netstat -rn"
```

çıktısı:

```
Destination   Gateway      Genmask        Flags Metric Ref   Use Iface
172.16.55.0   0.0.0.0      255.255.255.0  U     0      0       0 eth0
172.16.50.0   172.16.55.36 255.255.255.0  UG    0      0       0 eth0
127.0.0.0     0.0.0.0      255.0.0.0      U     0      0       0 lo
0.0.0.0       172.16.55.1  0.0.0.0        UG    0      0       0 eth0
```

Yukarıdaki çıktıda:
- Iface --> Interface anlamına geliyor
- Genmask - ilgili interface'ye bağlı network'ün subnetmask değeri
- gateway sutununda yıldızlı bir satır var ise, ilgili network/interface için gateway'a ihtiyaç yok/kullanılmıyor demektir. (bu değeri override edebiliriz. network'e yanlış paket gereksiz/yanlış oluruz.)
- 0.0.0.0 satırı (son satır) eğer farklı bir routing satırına uymayan istek için default algılanacak interface'dir.
- Genelde internete (dış dünyaya) açılan kartımız default olan olmalı. eğer böyle bir durum yok ise, bunu yine "route" komutu ile default'u değiştirebiliriz. routing table user tarafından editlenebilir.
- flag'lerin anlamları:
  - U - routing is enabled
  - H - bu routing satırının spesific bir hosta yönlendirdiğini belirtiyor (örneğin bir IP'yi spesific bir host'a yönlendirebiliriz). Bu flag yoksa, ilgili request network'e yönlendirilir.

Yukarıdaki routing table olan bir makinede bir IP'ye request yapalım. OS önce routing table'dan eşleştirme yapmaya çalışıyor. eğer bulamazsa default olan Network card'ına yönlendirecek. Eşleştirme yaparken destination ve genmask'a bakıyor. genmask, bağlı olan network kartındaki diğer IP'lerin bilgisini alabilmemiz sağlıyor. Destination ise network-ID olarak düşünülmelidir. Dolayısı ile eğer ilgili request bu network'teki bir cihaza gidecek ise iligli network kartına yönlendiriyor.

# komut satırı uygulamaları ile takip etme
traceroute posix'lerde, tracert ise windows sistemlerde komut satırı uygulamalarıdır. bu uygulamalar bir ip'ye gidilmesi için gerekli tüm aradaki node'ların(router'ların) iplerini gösterir. bu işlemi gerçektende karşıya paket atarak yapar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# DigitalOcean
Amazon'un bulut hizmetleri gibi sanal sunucular sunan bir firma.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Skype Wi-Fi
Microsoft'un skype-wifi için anlaştığı wifi olan bir mekanda skype hesabınız ile wifiye login oluyorsunuz. bu skype hesabınızda önceden kredi yüklü olmalıdır. wifi'ye login olunduğunda skype-wifi uygulaması başlatılmalıdır. Skype wifi artık dakika üzerinden ücret tarifesi başlatmakta ve interneti sınırsız olarak kullandırtmaktadır. skype-wifi, Skype uygulamasından tamamen bağımsız bir uygulamadır.

# Hot spot firmaları
Skype Wi-Fi gibi bir çok firma anlaşmalı olarak bu işi yapabilmektedir. tek bir modemden hotspot yaparak birçok ağ yaratılıp birçok markanın ağına bağlanabiliyoruz. bunnu yapan hizmet sağlayıcılar mevcut.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# instant messaging (IM)
anlık mesjalaşma teknolojilerine verilen genel isim.

# Extensible Messaging and Presence Protocol (XMPP)
mesajlaşma protokolüdür. merkezi bir sunucusu yoktur. herkes bir sunucu kurup bu hizmeti bağımsızca kullanabilmeyi sağlar. eskiden google ve facebook chat protokollerinden XMPP tabanlı sistemlerden yararlanıyordu fakat artık bu teknolojiyi bıraktılar. şu anda XMPP android ve ios için push notification'larda kısmen kullanılmaktadır.

# Jabber
XMPP'nin eski ismidir. Şu anda Jabber.org sitesinden XMPP protokolü kullanan bir chat mesajlaşma sunucusu hizmet vermektedir.

# Xabber
android XMPP client app.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# TCP/IP protocol suite


# protocol suite vs protocol stack
iki terim piyasada birbiri yerine kullanılmaktadır. Oysa bu iki terim net bir şekilde ayrılmıştır.

  - # protocol suite (or Internet Protocol suite)
      Protocol stack implementasyonundaki herhangi bir katmanı (veya katmanları) yürütebilmemiz için gerekli tüm protokollerin kümesidir. 

      - # TCP/IP protocol suite
        TCP/IP model'indeki trasnport ve internet katmanlarını yürütebilmemiz için gerekli bir protokol kümesidir.

  - # protocol stack (or Internet Protocol Stack)

    tüm ağ iletişim yapısını temsilen modelleyen katmanlı mimaridir.

    - # Open Systems Interconnection (or OSI or Open System Interconnection Reference Model or OSI/RM)
      ISO tarafından belirlenmiş ağ katmanlarının belirlendiği modelidir.

    - # TCP/IP
      OSI'ye alternatif bir ağ katman modelidir. Bu model'de sadece 5 katman vardır. TCP IP adlandırılmasının sebebi, en çok bu protokollerin kullanılmasıdır.

# TCP/IP vs OSI
aşağıdaki tablo için kaynak: (source-id: 336) "Table 4-2 TCP/IP Protocol Stack"

| OSI Ref. Layer No. | OSI Layer Equivalent               | TCP/IP Layer     | TCP/IP Protocol Examples                                                    |
|--------------------|------------------------------------|------------------|-----------------------------------------------------------------------------|
| 5,6,7              | Application, Session, Presentation | Application      | NFS, NIS+, DNS, telnet, ftp, rlogin, rsh, rcp, RIP, RDISC, SNMP, and others |
| 4                  | Transport                          | Transport        | TCP, UDP                                                                    |
| 3                  | Network                            | Internet         | IP, ARP, ICMP                                                               |
| 2                  | Data Link                          | Data Link        | PPP, IEEE 802.2                                                             |
| 1                  | Physical                           | Physical Network | Ethernet (IEEE 802.3) Token Ring, RS-232, others                            |

TCP/IP protokolü birçok makalede farklı seviye isimleri ve hatta farklı seviye sayıları ile tanıtılmıştır. kaynak: (source-id: 337) "Layer names and number of layers in the literature". wikipedia'daki belirtilen bu tabloda her sutun için kaynak belirtilmiştir.

# OSI Model
Üst seviyeden aşağıya doğru detaylar aşağıda yazmaktadır:

- isim
  - ilgilendiği birim
  - açıklama
  - örnek protokoller

- Application
  - Data
  - High-level APIs
  - HTTP, FTP, Telnet, SMTP, SSH

- Presentation (Sunum)
  - Data
  - ensures that data is in usable format (like character encoding, data compression, encryption/decryption)
  - SSL/TLS

- Session (Oturum)
  - Data
  - Managing communication sessions

- Transport
  - Segment (when using TCP) / Datagram (when using UDP)
  - Reliable transmission of data segments between points on a network
  - TCP, UDP

- Network
  - Packet
  - trasnport katmanından gelen verilere destination ip, source ip gibi data'larla çerçeveler.
  - IPv4, IPv6

- Data link
  - Frame
  - verinin frame'lere bölünmesini sağlar. Services provided by the Data Link Layer to the Network Layer include data link connection, sequencing, error notification, flow control, and data unit transfer. kaynak: (source-id: 338) "DATAPRO" report. "ISO Reference Model for Open Systems Interconnection (OSI)".
  - ATM, Ethernet. kaynak: (source-id: 339)

- Physical
  - Bit
  - bit bazında işlemlerin fiziksel olarak trasnfer olmasından sorumludur. tamamı donanım kısmında yapılır.
  - Ethernet, USB, Bluetooth

# tcp soket header
header kısmı en aşağıdaki data haricindeki kısmı kapsar.

Aşağıdaki büyük grafik bir tcp paketini göstermektedir. Birçok tcp paketi birleşerek bir segment'i oluşturur.

```
    0                   1                   2                   3   

    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 

   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

   |          Source Port          |       Destination Port        |

   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

   |                        Sequence Number                        |

   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

   |                    Acknowledgment Number                      |

   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

   |  Data |           |U|A|P|R|S|F|                               |

   | Offset| Reserved  |R|C|S|S|Y|I|            Window             |

   |       |           |G|K|H|T|N|N|                               |

   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

   |           Checksum            |         Urgent Pointer        |

   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

   |                    Options                    |    Padding    |

   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

   |                             data                              |

   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

- #### Sequence Number vs Acknowledgment
ikiside datanın başlangıç byte numarasıdır. karşı tarafa paket attığımızda bizim aynı pakette yolladığımız data'nın tüm sgement'teki kaçıncı bayt olduğu bilgisi sequence'de yollanıyor. oysa ACK'da karşı taraftan kaçıncı sıradaki datayı istediğimizi bilgisini yolluyoruz. örnek; yolladığımız pakette SEQ=5, ACK=90 olsun. bu şu demek oluyor: yolladığım paket tüm segment için 5'inci byte'tan başlayan bir data içeriyor. ve ben buna karşılık karşıdan 90inci bayttan başlayan datayı istiyorum. karşı taraftan ne kadar büyüklükte bayt geleceği ve benim ne kadar büyüklükte bayt yolladığım blgisi SEQ ve ACK'da belirtilmemektedir.

- #### data offset
options kısmının uzunluğu değişebiliyor. bu sebeple sadece tüm header'ın uzunluğu burada belirtilmektedir. bu şekilde data'nın nereden başladığını bilebiliriz.

- #### Reserved
hiçbir işe yaramaz. ilerde  tcp sürümü çıktığında kullanılması için rezerve edilmiştir.

- #### Control Bits (or Flags)
bazı sinyalleri içerir.

- #### window
tcp protokolünde her paket sırası ile yollanır fakat cevap gelmeden diğerleri de yollanır. bunun yapılmasının sebebi kuyruk mekanizması yerine pararlel mekanizma ile zamandan kazanılmasıdır.

  window kısmı byte biriminde bir uzunluk belirtir. bu kısımda bu paketi yollayan kişinin kaç adet paket daha almaya hazır olduğunu belirtir. bu şekilde karşı taraf paralel olarak buradaki boyu kadar byte yollayabilir. böylece karşılıklı denge ile paralel data yollanır. eğer bu window sayısı olmasaydı, herkes birbirine aynı anda tüm bandwith kadar paket yollardı. rşı tarafın müsaitlik durumunu buradaki sayı ile anlayabiliriz.

- #### Checksum
destination ip + source ip + protocol bilgisi (bizim senaryomuzda "TCP") + tcp header ve body length --> bu 3 adet bilgi daha alt seviyeli bir katmanda yollanıyor. bu 3 adet bilgiyinin hash'i checksum'a atılıyor.

- #### urgent point
"URG" control bit'i set edilmişse bu kısımda öncelik numrası verilmektedir. paketin önceliği için gerekli sıra numarası vardır.

- #### options
opsiyonel bir alandır. ekstra bilgiler içerir. örnek: timestamp.

- #### padding
tcp header'ın belli bir sayının katı olması beklenir. yani örneğin; 29 bit olamaz, onun yerine 32 olabilir. dolayısı ile 32'ye tamamlamak için padding kısmına boş data atılır.

# heartbeat
tcp soketi herşeyin sorunsuz olduğu koşullarda data yollanmazsa bile kapanmaz. sürekli açık bekler. fakat arada proxy varsa, firewall varsa gibi sebeplerden tcp soketleri aracılar tarafından kapatılabilir. bu sebeple tcp soketimizi açık kalmasını istiyorsak düzenli olarak karşı tarafa yaşadığımızı belli eden sinyal atmalıyız. protokol dünyasında bu tarz sinyallere yazılımcılar arasında heartbeat deniyor.

tcp standartlarında özel bir sinyal yok. fakat herkes tarafından kullanılan bir tcp sinyali var: "keep-alive". bu data kısmı boş olan bir tcp paketidir. hangi aralıklarla atılacağı tamamen yazılımcının kendisine kalmıştır.

# broken pipe
karşı taraf bağlantıyı kapatmış ise ve biz hala data yollamaya çalıştığımızda alacağımız hatadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# mac adres (or media access control address)
mac adres donanımın içinden sürücüler aracılığı ile yazılım tarafından okunur. fakat mac adres bilgisi (en azından network cihazları için) network-internet ağı iletişimlerinde yazılım katmanında taşındığı için kolaylıkla sahte bilgi kullanılabilmektedir.

'mac' birçok terimin kısaltmasına denk gelmektedir: (source-id: 451). bazıları:
- modified, access, creation times on filesystem
- 'message authentication code' kriptografide kullanılan, mesajın hash değeridir. bu şekilde mesjaın değişip değişmediği doğrulanabilir. mac değeri key ile imzalandığı için aynı zamanda, mesajın istenilen alıcıdan geldiği de doğrulanmış olur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# ssh (secure shell)
ağ üzerinde gücenli veri iletimi sağlamak için geliştirilmiş protokol.

shh uygulaması login işlemini doğrularken, o anda sunucu tarafta run edilen işletim sistemi user'ının şifresini istemez. onun yerne ssh sunucusunun config dosyasında belirtilen şifreyi yada public key'i ister.

ssh tamamen işletim sisteminden bağımsız olan bir uygulamadır. ssh'a bağlandığımızda ssh üzerinden verdiğimiz komutlar, ssh server uygulamasına TCP üzerinden yollanır. server uygulama bu komutları direk uzak işletim sistemine yollar. eğer admin gerektiren bir işlem yaparsak işlemtim sisteminin user admin şifresini girmemiz gerekir. 

ssh ekrtra olarak ("-X" parametresi verilmiş ise), kurduğu TCP bağlantısı üzerinden uzak masaüstündeki X server'a bağlanabilmemizi de sağlar.

# openssh
açık kaynaklı ssh sunucu ve client uygulamasıdır.

# openssl
açık kaynaklı ssl işlemleri yapan komtu satırı uygulaması ve kütüphanesidir.

# Heartbleed
openssl'in 2014'te çıkan meşhur güvenlik açığı.

# GnuPG (or GNU Privacy Guard)
__OpenPGP__ implementasyonudur.

OpenPGP ise __PGP yada Pretty Good Privacy)__'nin forkudur.

hem OpenPGP hemde GnuPG kendi komut satırı uygulamalarını sunar. bu uygulama ile dosya, disk (herhangi bir data) şifrelenip decript edilebilir. şifreleme metodu ve diğer parametreler dışarıdan verilebilir.

OpenPGP, "pgp", GnuPG "gpg" komut satırı uygulamasını sunar.

opengpg ve diğer tüm implementasyonlar sadece şifrelme ile değil aynı zamanda sıkıştırma, digital imza gibi ek özellikler de sunar.

# FTP
dosya transferi için kullanılan protokol.

# FTPS (or FTPES or FTP-SSL or S-FTP or FTP Secure or FTP over SSL)
FTP prokolünün SSL ve TSL ile birlikte kullanımı için geliştirilen protokol.

# SFTP (or SSH file transfer protocol)
ssh yapısı ile tamamiyle bütünleşik ftp protokolüdür.

# FTP over SSH (or SSH üzerinde FTP kullanımı)
SFTP ile karıştırılmamalıdır. SSH bağlantısı açıp, bağımsız olarak o bağlantı üzerinden FTP ile dosya yollama işlemleridir.

# scp (or secure copy)
özel bir dosya transferi protokolüdür.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Request for Comments (RFC)
is a type of publication from the Internet Engineering Task Force (or IETF) and the Internet Society (or ISOC) which includes contents about Internet.

RFC dökümanları güncellenebilir veya ilgili dökümana ekleme yapılabilir. Eğer yeni RFC eskisini update ediyor yada güncelleme sunuyorsa, yeni RFC eskisini "update" ediyordur. Eğer eski döküman geçersiz olmuşsa, yeni döküman eskisini "absolute" ediyordur. kaynak: (source-id: 340) "12. Relation to other RFCs" ilk paragraf.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Lightweight Directory Access Protocol (or LDAP)
Uzak ve birbirine direk bağlı ağlarda bilgisayarlar arası paylaşım/izin gibi yetkilerin sorgulanmasını sağlayan açık kaynaklı protokoldür. Protokolün kullanılabilmesi için sunucu ve her bilgisayarda client yazılımı olması gereklidir. Bu protokolü destekleyen sunucular:

- Microsoft Active Directory
- OpenLDAP
- Apache Directory Server
- Red Hat Directory Service
- ve daha birçoğu...

LDAP sadece client ve sorver arasındaki haberleşme protokolüdür. Client veya serveR'ı çalışma mantığı hakkında hiçbir standart içermez.

Client sunucuya query atıp yetkisi dahilindeki user'ları, grupları, user detaylarını, hangi resource'lara erişebildiğini sorgulayabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Surface web (or Visible Web or Indexed Web or Indexable Web or Lightnet)
Internette arama motorlarına kayıtlı siteler.

# Derin ağ (or derin internet or deep web or invisible web or hidden web)
Arama motorlarının indexlenmediği bir web sitesi, derin internet'teki bir site olmuş oluyor. bunun için özel ek bir işlem yapmaya gerek yok. site yetkilileri arama motorlarına indexlemeleri için başvuru yapmazlarsa indexlenmezler. bu tarz siteler genelde özel amaçlar yada herkes tarafından görünmemek için tercih ediliyor. url'yi bilen adrese girebiliyor. 

# dark web
Ancak özel programlarla erişilebilen derin ağ sitelerine verilen isimdir. 

# dark net
Dark web'e erişim için geliştirilmiş network sistemidir. Örneğin "tor" bir darknet türüdür.

# Tor (The Onion Router)
Anonim iletişim için gerekli ağ ve bu ağa bağlanmak için ilgili yazılımları geliştiren proje adıdır. Ağın ayakta kalabilmesi için sunucu kaynakları gerekli. burada tor yazılımları kuran kullanıcılar, isterse birer tor ağı olabiliyor. tor ağı protokolleri log takibini zorlaştıracak şekilde tasarlanmaktadır. mutlak gizliliği sağlamamaktadır. proje açık kaynaklıdır. Ağ'a bağlanmak için gerekli tool'lar ve protokoller OSI network katmanında en üst seviyede (Application layer) çalışmaktadır. tor network routing'leri ile gidilebilecek siteler mevcut. bu sitelere erişmek için sadece tor kullanmak gereklidir. .onion uzantılı siteler mevcuttur.

# Tor Browser
Tor project'in resmi masaüstü tarayıcısı. firefox türevi. tüm masaüstü işletim sistemlerinde çalışan açık kaynaklı portable versiyonları mevcut.

# Orbot
android için uygulamaların tor networkuna bağlanmasını sağlayan uygulama. androidin yeni gelen vpn özelliği sayesinde, her uygulamanın ayrı ayrı tor'dan çıkıp çıkmayacağı ayarlanabiliyor.

# Orweb
Tor project'in resmi android tarayıcısı. varsayılan android stock tarayıcı türevi. fakat orfox'un stabilleşmesi üzerine artık marketten kaldırılmıştır.

# Orfox
Tor project'in resmi android tarayıcı versiyonu. firefox türevi.
