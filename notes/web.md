############################

############################
# WEB
############################

############################

# Web browser User Agent

user agent header'da otomatik platform tarafından gönderilir. sadece browser değil, her client user-agent atmalıdır.

formatı incelersek; Çoğu "mozilla/" ile başlar. ilk olarak bu isim verilmişti. daha sonra herkes devam ettirdi. yanındaki ilk numara format sürümüdür.

User agent içerisinde aşağıdakiler sürüm bilgileri ile yazar:

- tarayıcıda bazı kurulu eklentilerin listesini

- layout engine ismi

- tarayıcı ismi

- işletim sistemi ismi

- işletim sistmi çekirdek ismi

- windows için kurulu .net ve service pack sürümleri

User agent dışında javascript tarafında alınan bilgiler:

ekran çözünürlüğü, tarayıcı pencere boyutu, local saat, cookie ve jascriptin açık olmadığı bilgisi.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Ajax (or Asynchronous JavaScript and XML)

web sayfasında reloading yapmadan sunucuya xml istekleri yaparak sayfayı yenileme tekniğidir.

# XMLHttpRequest (or XHR)

Core Javascript'te ajax yollamaya yarayan objenin ismidir.

# origin
kelime anlamı: menşei, köken

web dünyasında origin protokol, domain, host (subdomain olarakta adlandırılır), port dörtlüsünün bir arada temsil etmektedir. örneğin; iki URL değerimiz olsun. ikisi aynı origin olabilmesi için bu 4 bilgininde aynı olması şarttır.

path değeri önemsizdir.

Sadece Microsoft internet explorer'da:

- "Trust Zones" olarak tanımlı domain'lere
- port bilgisi farklı olan URL'lere

istisna tanınıp aynı origin'de oldukları varsayılır. bu her sürümde varmı bilmiyorum. kaynak: (source-id: 193)

# Cross origin domain policy

Web tarayıcılarının başka domainlere istek yapılmasını güvenlik için engellemektedirler. Cross origin domain policy bu kıstası kapsamaktadır. web sitesinin bunu aşmasının birkaç yolu vardır:
- jsonP
- Adobe flash gibi eklentiler
- CORS

# Cross-Origin Resource Sharing (or CORS)

Modern tarayıcılar tarafından cross site scriptin desteklenmesi standartlarıdır. Farklı bir domain'e istek yapılacağı zaman tarayıcı anında (artık - cors destekleyen tarayıcılar) bloklama yapmaz. bunun yerine eğer;

- istek "basit istek" değil ise preflight isteği yapılıyor.

- istek "basit istek" ise isteğe direk izin veriliyor.

tarayıcı arkaplanda; web sayfasının istek yapmak istedikleri adrese, istek tipini ve web sayfasının o andaki adresi gibi bilgileri gönderir. bu istek "option" metodu tipinde bir XHR'dır ve ismi "Preflight"'tır. sunucu bu isteğe cevap olarak tarayıcıya asıl isteği gönderip gönderemeyeceği bilgisini verir. eğer sunucu izin verirse web sayfasının ajax işlemi gerçekleştirilir. burada bir nebzede olsa güvenlik sağlanmış olmaktadır. çünkü Preflight request'i web sayfası değil, tarayıcı tarafından hazırlanmaktadır. standartlar web sayfalarını tamamiyle serbest bırakmak yerine, bir nebze daha güvenli olacağı düşünülmüş bu taktiği uygulamaktadır. JSONP yönteminden daha modern bir yöntemdir.

CORS isteği hata verirse detaylarını JS tarafından programatik olarak alamayız. Bu güvenlik sebebiyle engellenmiştir.

# Basit istek (or simple request)

Beğer bir XHR isteği;

- GET veya HEAD veya POST ise

- Tarayıcıların default olarak kendi eklediği header'lar (örnek user-agent) dışında saadece bazı header'lar kabul edilir.

- İzin verilen header'ların bazılarında sadece bazı alanların olmasına izin verilir. örnek:

  Content-type header'ında sadece şu 3'ü kabul edilir:
  - application/x-www-form-urlencoded
  - multipart/form-data
  - text/plain

- Ek bazı kurallar daha vardır. kaynak: (source-id: 194) "Simple requests" başlığı.

# json vs jsonp
ajax isteği ile ancak aynı domain'e istek yapıp cevap alabiliriz. farklı domainlere yapılan istekler tarayıcılar tarafından güvenlik sebebi ile engellenir.

jsonp formatı; json formatındaki bir değerin bir metod içerisinde çağrılacak şekilde formatlanmış halidir.

örneğin;

json:
> { isim: ahmet }

jsonp:
> metodName ( { isim: ahmet } )

HTML sayfasında include edilen kütüphanelerin (script, css vs) taglerindeki url'lerde cross domain'e izin verilir. İşte bu noktada jsonp ie bir açıktan yararlanılır:

JSonp ile istek yaparken HTTPRequest isteği isteği yapılmaz. Sayfaya script include edilir. Bu include edilecek değer ise sunucudan gelecek olan response'tur.

```js
var elm = document.createElement("script");

elm.setAttribute("type", "text/javascript");

elm.src = "http://example.com/jsonp";

document.body.appendChild(elm);
```

Burada dönen cevap bir metodu çağırır. Metod bizişm javascript tarafında tanımlı olduğundan ona veri olarak parametre gönderir. İşte tüm bunları simüle eden bir fonksiyon yapıp HTTPRequest-Ajax işlemi yaparmış gibi cross domain kuralını aşarak işlem yapabilir.

# jsonP vs cors
Cors web tarayıcıları tarafından önerilen bir yöntemdir.

jsonp'nin dezavantajları:

(tüm dezavantajlar \<src\> eklenip yapılmasından kaynaklıdır.)

- sadece get isteği yapılabilir
- excepiton handling mekanizması ajax request yönetimine göre daha kötüdür. sadece request'te hata olup olmadığını görebiliriz.
- headerları seçip yollayamayız yada gelene header'ları göremeyiz

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Do Not Track (or DNT)

web siteleri kullanıcılardan istatistik toplar. web tarayıcıları http header'larına, kullanıcın bilgi toplanmasını istemediğini yada istediğine dair bir metadata ekler. sitede buna göre davranır. yasal süreçlerin getirmiş olduğu bir zorunluluktur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# google chrome os vs chromium os

- embeeded adobe flash

- auto updater

- donanıma özgü performans paketleri içerir

- resmi destek google ve/veya donanım üreticisi tarafından verilir. chromium için topluluklar ile temasta olmak gerekir.

- chromium browser (look at: chromium browser vs google chrome browser )

- Name and logo tradememarks and licence

- ve daha fazlası

# chromium browser vs google chrome browser

- default installed extensions

- embeeded auto updater

- embeeded adobe flash (linux paketinde de geliyor)

- Media codecs to support H.264, AAC and MP3 formats

- Name and logo tradememarks and licence

- isteğe bağlı olarak birçok bilginin istatistik olarak google'a gönderilmesi seçeneği (chromium üzerinde bulunan diğer hizmetlerde de bilgi gönderiliyor. detaylar farklı başlıkta yazıyor)

- resmi destek google tarafından verilir. chromium için topluluklar ile temasta olmak gerekir.

- ve daha fazlası

# notlar

- "built-in PDF viewer" and "print preview" future added both browsers after chromium 47 version.

- chromium has no release tags inside code review system. there is no way to find stable versions. açık kaynağı destekleyen topluluklar, kodun stabil olduğunu düşündükleri bir noktadan, debian tabanlı sistemler için paket çıkmaktadırlar. şimdilik en stabil versiyonu bu.

- html ve javascript derleyicilerinde bir farklılık yok. fakat buna rağmen chromium ile teknik bir kaşrılaştırma yapmak mümkün diil, çünkü chromium için aynı noktadan paket çıkılmış versiyon bulmak pratikte neredeyse imkansız.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# URL Safety
Below functions are embeeded to all browsers as default.

```js
// Replace unsafe URL characters with %01 or %02...
// It accepts full URL, therefor it does not convert / ? characters.
var urlSafe = encodeURI("http://www.google.com");
decodeURI(urlSafe); // returns real URL which includes unsafe characters.

// encodeURIComponent function replace all unsafe characters with %01 or %02...
// It is different from encodeURI. Because encodeURIComponent also converts / ? characters. We can use this function to make safe a part/component of URL. For example: query param, query value, path...
var safeStr = encodeURIComponent("This string has unsafe characters");
decodeURIComponent(safeStr);
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# WebAssembly (or Wasm)
web tarayıcılarında sunucudan gönderilen c/c++ gibi native code'lar çalıştırılıyor. bu kod güvenlik amaçlı sandbox'ta çalıştırılıyor ve yetkileri çok kısıtlı. js gibi sadece belli kaynaklara erişebiliyor (cookies, DOM...).

örnek kod:

```java
var wasmModule = new WebAssembly.Module(wasmCode);
var wasmInstance = new WebAssembly.Instance(wasmModule, wasmImports);
wasmInstance.exports.factorial(10); //native taraftaki faktoriel alan fonksiyonumuzu çağırdık.
```

örneğin; client tarafta video editleme uygulaması yaptık. bu gibi durumlarda bu teknoloji performans'ı çok etkiliyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# postback

web sayfasında forma tıklanıp, aynı sayfaya istek yapılan istek postback işlemidir. "POSTed back" to same page teriminden gelir. genelde jsp, jsf, asp gibi platformlarda karşımıza çıkar, fakat teknolojiden bağımsızdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# REST Resource Naming
- URL bir identifier olduğu unutulmamalıdır
  
bu sebeple fiil içermemelidir. fiil içermemelidir.
örnek: 

> /api/message/3/delete/

yerine

> /api/message/3

  DELETE metodu desteği olmalıdır

- tekil kaynak çağırma
  
  /user-management/users/{id}
  /user-management/users/admin

- çoğul kaynak çağırma
  
  /device-management/managed-devices
  /user-management/users
  /user-management/users/{id}/accounts

  Tekil ve çoğul kaynaklarda "users" yada "user" yazılıp yazılmayacağı önemsizdir. fakat tüm servislerimizde ya çoğul yada tekil olan kelimeleri kullanmalıyız.

- fiil içerme durumları
  
  yapılacak işlem bir prosedürü başlatacak ise; fiil kullanılmak zorundayız. örnek:
  /cart-management/users/{id}/cart/checkout

- geçerli olmayan standartlar
  
  Google, facebook, dropbox, instagram gibi büyük servislerin api'leri aşağıdaki standartlar konusunda farklı yol izlemektedirler. Hatta aynı şirketin farklı servisleri farklı yöntemler kullanmaktadır.

  - okunabilirlik
    - userManagement
    - user-management
    - user-management
    - usermanagement

  - büyük küçük harf standartları

    rfc2616 standartlarına göre ( w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.2.3 ) büyük küçük harf hostname'e kadar önemsiz iken, path kısmında önemlidir.

  - versioning
    
    - With a timestamp, a release number
    - In the path, at the beginning or at the end of the URI
    - As a parameter of the request's body
    - In a HTTP Header
    - With an optional (example: /api/users/1?v=2 )

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# placeholder
türkçe kelime anlamı: yer tutucu
bazı html form elemenleri için bir attribute'dir. bu attribute ile son kullanıcı text girmemiş ise, placeholder value'sinde yazan string değeri ekranda gösterilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# carousel
Türkçede kelime anlamı: atlıkarınca

HTML'de sağ ve sola doğru oklar aracılığı ile resim galerisi gezintisi sağlayan component'e verilen özel isimdir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Favicon
Favorites icon'un kısaltmasıdır. bu resim dosyası, sitenin sık kullanılanlara eklendiğinde, veya siteye gidildiğinde görünecek ufak simgesidir. html kodları içerisinde yer alır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# access inside html popup with pure (core) js

```js
var myWindow = window.open("", "myWindow", "width=200, height=100");
myWindow.document.write("hello I'm popup");

//or get the opener object
var opener = window.opener;

if(opener) {
    var oDom = opener.document;
    var elem = oDom.getElementById("elementId");
    if (elem) {
        var val = elem.value;
    }
}
```

html, aynı anda birden fazla popup desteklemektedir. fakat çoğu tarayıcı varsayılan olarak ikinci açılan popup'ları engellemektedir. bu sebeple açılması tavsiye edilmez.

# Backlink
Backlink, bir web sayfasından başka bir web sitesine giden köprü bağlantıya verilen isimdir. Bir web sitesine, diğer sitelerden verilen backlink ne kadar fazla olursa, bu web sitesi arama motorları açısından o denli popüler olur. burada önemli kriter: X sitesi, Y sitesine link veriyorsa, X'teki sayfanın içeriğinin Y'deki ile bağlantılı/alakalı olmasıdır. ilgisiz konulardaki linkler verimsiz olacağından arama motorlarındaki puanı olumsuz etkiler.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# tampermonkey vs greasemonkey vs Violentmonkey

web tarayıcıları için birbirlerine alternatif eklentilerdir.eklentiler sayesinde son kullanıcı javascriptleri, istediği event (sadece standart javascript eventleri değil, ekstra eventler de kullanılabiliyor) sonrası çalıştırabiliyor. internette birçok hazır script paylaşılıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# chart.js
web teknolojilernii kullanarak ekrana sadece chart çizmek için kullanılan js kütüphanesi.

# d3
web teknolojileri ile ekrana her türlü görüntü oluşturmak için kullanılan js kütüphanesi.

# jqplot
jQuery eklentisi. sadece chart oluşturmaya yarıyor.

# çizge (or graph or grafik or tr:graf or çizit)
elle yada araçla çizilen her türlü görüntüye grafik adı veriliyor.

"Graph" kelimesi tek başına bilişimde; bir veri yapısı çeşidini temsil eder (başka başlıkta anlatılıyor).

# chart
grafiğin bir alt kümesidir. sadece değişkenler arasındaki ilişkiyi göstermeye yarayan çizgisel anlatım şekli.

çok kullanılan bazı chart çeşitleri:

- Line chart (or Çizelge): x-y ekseni üzerinde bir fonksiyonun gösterilmesidir.

- bar chart: birden fazla kalın çubukların yanyan dizilerek x-y ekseni üzerinde gösterilmesi. 

- pie chart (or a circle chart): pasta üzerinde oranların paylaştırıldığı grafik

- histogram: gruplandırılarak gösterilen bir "Bar chart" çeşididir. örnek olarak aşağıdaki datayı bar chart'ta gösterdiğimizi düşünelim:

| BOY (CM) GRUPLAR | KİŞİ SAYISI |
|------------------|-------------|
| 161-165          | 5           |
| 166-170          | 10          |
| 171-175          | 9           |

# diagram (or tr:diyagram)
grafiğin bir alt kümesidir. sadece herhangi bir olayın değişimini gösteren grafik. UML diyagramları buna örnektir.

# Cartogram (or kartogram)
grafiğin bir alt kümesidir. istatistiki bilgilerin harita üzerinde gösterildiği grafiktir.

# indicator (or indikatör)
gösterge anlamına gelmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Web Debugging Proxy Application

Yaızlımlar network üzerinden ajax işlemi yaparlar. bu ajaxları intercept edip devam ettirmek ve manipüle etmek için aracı programlardan yararlanılır. bu progrmalara genelde "Web Debugging Proxy Application" uygulamaları denir.

tüm network trafiğini intercep eden uygulamalar:
- Fiddler
- Charles
- mitmproxy (açık kaynaklı): ismi man-in-middle-proxy kısaltmasından gelmektedir.
- tamperchrome: Chrome için google'nin geliştirdiği eklenti. sadece google chrome üzerinden çıkan ajax işlemlerini intercept edebiliyor.

# Temel çalışma mantığı

"Web Debugging Proxy Application" aslında bir proxy uygulaması. bu sebeple örneğin; firefox uygulamasınından gidecek ajax istekleri incelenecek ise; firefox'un proxy ayarlarına "Web Debugging Proxy Application" proxy sunucusunun açtığı ip:port bilgisi veriliyor. artık firefox'un yaptığı istekler "Web Debugging Proxy Application" GUI ekranında listelenmeye başlıyor.

# localhost problemi
localde development yaparken "Web Debugging Proxy Application" uygulamaları localhost'a yada 127.0.0.1'e yapılan istekleri yakalayamayabilir. bu gibi durumlarda localhost yerine makine-name'mizi kullanabiliriz. çünkü localhost direk loopback interface'sine yönlendirilirken, makine-name'mimiz network üzerinden sorgulamaya çalışılıyor.

# Web Debugging Proxy Application'lerin SSL bağlantılarını izlemesi
normal koşullarda ssl bağlantısını kimse takip edemez. fakat, Proxy uygulamamız kendi "certificate Authority" sertifikasını işletim sistemine yada takip edeceğimiz client'a (java app, web browser...) kurdurduyor. Client isteği proxy'ye atıyor. proxy o anda, sisteme tanıtılmış olan certificate Authority'ye uygun bir sertifika üretiyor. proxy, isteği sunucuya kendi atıyor(yönlendirmiyor). dönen cevabı da kendi sertifikası ile imzalayıp döndürüyor. yani proxy, gerçek isteği yönlendirilmiyor. proxy arada sahtecilik yapıyor.

burada bazı sorular/sıkıntılar var. çözümleri ile birlikte açıklamak gerekirse:

- web tarayıcı DNS sorgusu sonrası sunucuya ip ile gidiyor. dolayısı ile http isteği ip ile bağlantı kurulup yapılıyor. yani proxy hangi domaine gitmek istediğini bilemiyor. bu sebeple nasıl o domaine uygun sertifikayı o anda üretiyor?

  Proxy ip'ye aynı anda bir request atıp handshake işlemi yapıyor. proxy o ip'li sunucunun sertifikasına bakıyor. sertifikasında olan "Common Name" bilgisi zaten domain bilgisini vermektedir.

- bazı sertifikalar birden fazla domain bilgisi içerebiliyor. bu gibi durumda, client'ın hangi domaine gitmek istediğini proxy nereden bilebilir?

  Proxy sunucudan indirdiği ssl sertifikasındaki "Subject Alternative Name" değerine bakıyor. burada birden fazla domain ismi oluyor. proxy o anda tüm bu domainlere uygun bir sertifika üretiyor ve client ile bununla haberleşiyor.

şirketler çalışanlarının https bağlantıları bu yöntemle takip etmektedirler. her işletim sistemine certificate Authority tanıtmaktadırlar.

eğer bir kullanıcının tcp ile iletişim kurulacak yazılımına "certificate Authority" kurulmamış ise; tüm network trafiği izlensede kullanının dataları görünemez. çünkü client taraf, daha ilk mesajından itibaren sunucunun private key'i ile şifreli şekilde data'ları yolluyor. şirketler "certificate Authority" sertifikasını tüm web tarayıcılarına ve işletim sistemine baştan root yetkisi ile kuruyor ve kimseye sildirtmiyor. bu sahte "certificate Authority" sayesinde şirket aradaki tüm bağlantıları açık şekilde izleyebiliyor.

peki biz portable bir firefox kurup, işletim sisteminden sertifikaları algılamamasına göre konfigüre edersek ne olacak? bu sefer bağlantıyı şirket takip edemeyecek fakat bağlantıda giden gelen data'lar anlamsızlaşacak ve iletişim kurulamayacak.

# mitmproxy modes
mitmproxy birden fazla mode ile çalışabilir. bazıları:

- socks proxy

  SOCKS bir çeşit proxy türüdür. Birçok sürümü vardır: 4, 4a, 5...

  'HTTP proxy'ler sadece HTTP isteklerini karşılarken, SOCKS proxy daha alt seviyeli birçok bağlantı çeşidini destekliyor: örnek TCP.

- Reverse proxy

  sunucu tarafta (datacenter'ında) olan proxy'dir. target sunucularının önünde durur.

  reverse proxy'lere bazı kaynaklarda "gateway" de denir. kaynak: (source-id: 195) "Forward Proxies and Reverse Proxies/Gateways" başlığı, 1inci paragraf.

- regular proxy

  default mode. "__forward proxy__" olarak davranır.

  forward proxy'ler, client tarafın ortamında olan proxy'lerdir. client proxy olarak bunu kullanacağını belirtmelidir/bilmelidir.

- Transparent proxy

  önce router'a giden client, daha sonra router tarafından mitmproxy'ye yönlendirilir. daha sonra mitmproxy default mode'daki gibi gelen istekleri yönlendirir. (aşağıdaki başlıkta daha detaylı anlatılıyor)

- Upstream: birden fazla proxy zinciri varsa, mitmproxy bu zincirdeki bir proxy olarak çalışabilir.

# Transparent Proxying (or intercepting proxy or inline proxy or forced proxy)
Transparent: saydam, şeffaf, transparan

2 farklı anlamı vardır:

- network katmanında kullanıcı hiçbir ayar yapmasına gerek kalmadan yapılan proxy işlemidir.

- rfc2616 (source-id: 214) standardında belirtildiği gibi request ve response'u hiç değiştirmeyen proxy'lere denir. __non-transparent proxy__ ise request veya response üzerinde bazen yada her zaman değişiklik yapan proxy'lerdir.

Mitmproxy Transparent mode'a ayarlandığında aşağıdakilerden sadece bir tanesi yapılmalıdır;
- spoof edilecek cihaz'ın network ayalarında gateway olarak mitmproxy'nin çalıştığı bilgisayarın ip'si verilmelidir. yani gateway = mitmproxy olacaktır. (bu durumda rooter'ın ayar yapmasına gerek kalmaz)
- router'ımızda mitmproxy konfigürasyonu yapılmalıdır. bu ayar ile client, önce router'a gitmekte, router istekleri ise mitmproxy'nin olduğu sunuya yönlendirmektedir. (bu durumda client'ın ayar yapmasına gerek kalmaz) (kaynak: (source-id: 440) "Transparent Proxy" başlığı, 1inci cümle.)

yukarıda 2 farklı çözüm ile Transparent modun çalışabileceği için kaynak: (source-id: 440) "Common Configurations" başlığı.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# bookmarklet

web tarayıcıları url'den javascript çalıştırılmasına izin verir. bu sebeple birçok hazır js sık kullanılanlara eklenerek tarayıcıya ek işlevler kazandırılır. bu uygulamacıklara bookmarklet denir. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# DOM Events
asagida bazı event ve bu eventlerin bazı grupları listelenmiştir.

- #### mouse events:

  - oncontextmenu : user right clicks to an object

  - ondblclick : on double click

  - onmousemove :bir obje üzerinde fare hareket ettiği zaman

  - onmouseenter : fare elementin üzerine geldiğinde

  - onmouseover : onmouseenter ilgili obje içerisindeki diğer objeleri kapsamazken, onmouseover altobjeleri de kapsıyor.

  - onmouseleave : fare objenin dışında çıktığında

  - onmouseout : onmouseleave'in altobjeleri de kapsadığı durum

- #### key events

  klavyeden bir tuşa basıldığında sırası ile bu eventler çağrılıyor: keydown, (bu sırada text ekranda yazılmış görünüyor), keypress, keyup

  keypress metodu CTRL+V gibi işlemleri yakalamazken,  keydown bu işlemleri de yakalayabliyor.

- #### Frame/Object Events

  asagidakiler her element'te geçerli olan eventler değil. çoğu sadece body tag'inde çalışıyor.

  - onabort: The event occurs when the loading of a resource has been aborted

  - onbeforeunload: The event occurs before the document is about to be unloaded

  - onerror: The event occurs when an error occurs while loading an external file

  - onhashchange: The event occurs when there has been changes to the anchor part of a URL

  - onload: The event occurs when an object has loaded

  - onpageshow: The event occurs when the user navigates to a webpage

  - onpagehide: The event occurs when the user navigates away from a webpage

  - onresize: The event occurs when the document view is resized

  - onscroll: The event occurs when an element's scrollbar is being scrolled

  - onunload: once a page has unloaded

- #### Form Object events

  - onblur: object loses focus

  - onchange: the selection, or the checked state have changed (for input, keygen, select, and textarea)

  - onfocus: The event occurs when an element gets focus

  - oninput: keypress gib fakat CTRL+V ile yazılanları da algılıyor.

  - oninvalid: örneğin; textbox'un boş olması

  - onreset: form reset button clicked

  - onselect: the user selects some text (for input and textarea)

  - onsubmit: a valid form's submit button clicked

- #### drag events

- #### clipboard events
  - oncopy 
  - oncut
  - onpaste

- #### print events
  - onafterprint
  - onbeforeprint

- #### Media Events

- #### Animation Events

# event object
javascript'te event callback metoduna geçilen event nesnesinin bazı property'leri ve metodları asagidadir.

asagidakilere ek olarak her event (örneğin click-event) kendi property'sini eklemektedir.

- #### property'ler

- bubbles: Returns whether or not a specific event is a bubbling event.

- cancelable: Returns whether or not an event can have its default action prevented

- currentTarget: Returns the element whose event listeners triggered the event

- defaultPrevented: Returns whether or not the preventDefault() method was called for the event

- eventPhase: Returns which phase of the event flow is currently being evaluated

- isTrusted: if user call the action or not.

- target: Returns the element that triggered the event

- timeStamp: Returns the time (in milliseconds relative to the epoch) at which the event was created

- type: Returns the name of the event

- view: Returns a reference to the Window object where the event occured

- #### metod'lar

- event.preventDefault()

```html
<script>
function engelle(e){
    e.preventDefault();
}
</script>

<a href="http://www.mylink.org" onclick="engelle(event)">Tıkla</a>
```

a tag'ine tıklandığında sayfa başka yere gitmesi gerekirken gitmeyecektir. preventDefault bunu engelliyor. örneğin; keypress eventine şu metodu yazarsak rakam haricindeki kullanıcı girişlleri bir input'a yapılamayacaktır:

```js
if(e.keyCode>=58 || e.keyCode<=47)

   e.preventDefault();
```

- event.stopPropagation();
DOM'da Div içinde p, onunda içinde psan elementi olsun. asagidaki tanımlamalar yapılmış olsun. spana fare ile tıkladığımızda, stopPropagation diğer metodların çalışmasını engelleyecektir.

```js
$("span").click(function(event){

   event.stopPropagation();

   alert("The span element was clicked.");
});

$("p").click(function(event){

   alert("The p element was clicked.");
});

$("div").click(function(){

   alert("The div element was clicked.");
});
```

- stopImmediatePropagation()
aynı objenin click event'ine 2 tane metod atılmış olsun. diğer metodların çalışmasını engellemek için bu metod kullanılır.

- return of callback method

event metodu return false yapınca da belli anlama geliyor. aşağıdaki tabloda net görülmektedir.

|                          | stop bubbling | prevent default action | prevent event handlers        |
|--------------------------|---------------|------------------------|-------------------------------|
|                          |               |                        | Same Element / Parent Element |
| return false             | Yes           | Yes                    | No      /     No              |
| preventDefault           | No            | Yes                    | No      /     No              |
| stopPropagation          | Yes           | No                     | No      /     Yes             |
| stopImmediatePropagation | Yes           | No                     | Yes     /     ?               |

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# upload file 

tarayıcılardan sunucuya dosya yükleme işlemleri var. bu işlemler http standartları altında yapılmaktadır. upload işlemi POST tipindedir.

"contenttype" header'ı "multipart/form-data" olmalıdır. bu işlemde html form içindeki elemanlar yollanırmış gibi data yollanır.  

Header'da aşağıdaki bilgi olmalı:

```
contentType = part/form-data; boundary=--BURAYA_ISTEDIGIMIZ_BIR_STRING_GIRERIZ
```

tarayıcılar otomatik olarak bir form'daki bilgileri request'e uygun şekilde dolduruyor. Yukarıdaki header'daki string'imizi body kısmında kullanıyoruz. her form elemanını ayrı ayrı aynı body'de yolluyoruz. body kısmı:

```
--BURAYA_ISTEDIGIMIZ_BIR_STRING_GIRERIZ

Content-Disposition: form-data; name="username"



Ahmet

--BURAYA_ISTEDIGIMIZ_BIR_STRING_GIRERIZ

Content-Disposition: form-data; name="Filedata"; filename="profile_photo.png"

Content-Type: application/octet-stream



PHOTO_FILE_AS_BINARY_IS_HERE

--BURAYA_ISTEDIGIMIZ_BIR_STRING_GIRERIZ

Content-Disposition: form-data; name="country"



England

--BURAYA_ISTEDIGIMIZ_BIR_STRING_GIRERIZ
```

yukarıdaki işlem tek bir tcp soketi üzerinden yollanır. stream'ing yaparak yollar. ve yukarıdaki tek bir request'tir. tarayıcılarda tek işlem olarak algılanır. 

java rest sunucusu üzerinde metod çok genel olarak şu şekilde olacaktır:

```java
@post
fileUpload(inputstream) {

   while( inputstream.hasnext() ){

        inputstream.read();
   }
   return http.status.ok;
}
```

Alt seviyeli bakıldığında; herhangi kısa bir http isteği de steraming yaparak yollanır. fakat büyük bir data olmadığı için inputStream'ler işin içine katılmaz. bu sebeple upload işlemlerinde inputStream'ler işin içine girer.

# download file
tarayıcılar bir dosya download edilmesi gerektiğinde, GET isteği ile download yapar. get'in response'u data'nın direk kendisidir (binary data). get işleminde hiçbir header eklemeye gerek yok. işlem tek bir request'tir. sadece response'un alınması uzundur. java sunucu tarafı psudo olarak aşağıdaki gibidir:

```java
@RequestMapping(path = "/download", method = RequestMethod.GET)

public ResponseEntity<Resource> download(String param) throws IOException {

  InputStreamResource resource = new InputStreamResource(new FileInputStream(file));

  return ResponseEntity.ok()

          .contentLength(file.length())

          .contentType(MediaType.parseMediaType("application/octet-stream"))

          .body(resource);
}
```

# multipart/alternative vs multipart/mixed
bu isteklerin standartları mail sunucuları tarafından kullanılmaktadır. normal web sayfalarında kullanılmazlar. bunun gibi birçok mimetype mevcuttur.

# chunked http request
chunk türkçe kelime anlamı: yığın

http 1.1 ile gelen bir özelliktir. http 2.0 ile bu özellik artık kullanılamamaktadır. çünkü http 2 daha farklı stream'ing özellikleri sunmaktadır.

"Content-Length" header'ı body'nin byte boyutunu belirtmektedir. eğer bu değer yoksa "Transfer-Encoding: chunked" header'ı elle yada server tarafından otomatik eklenmektedir. eğer işlem chunked ise sürekli olarak payload/body karşı taraftan çekilmektedir.

chunked işlemini hem sunucu hem client atabilir.

her chunk satır sonu karakteri ile sonlanmaktadır.

Her tarayıcı ve web browser (default ayarları ile, ek ayar yapılmamışsa) giden body'nin boyutu hesaplar ve belli bir limiti geçmişse chunked olarak karşıya atarlar.

"Content-Encoding: gzip" header'ı sıkıştırılmış chunked data atabilmemizi sağlamaktadır.

# chunked vs multipart

chunked alt seviyeli ve (HTTP API'yi geliştirmiyorsa) yazılımcı tarafından farkedilmemektedir. fakat multi-part daha üst seviyeli bir işlemdir.

# http version history

http versiyonları HTTP/1.1, HTTP/2 şeklinde gösterilmektedir.

- 0.9 (1991)
- 1.0 (1996)
- 1.1 (1999)
- 2 (2015)

Her sürüm arası köklü değişiklikler yapılmıştır.

# HTTP 1.1 vs HTTP 2

- http2 de her request frame'lere bölünmüştür. bir request/response birçok frame'den oluşabilir. en ufak birim framedir.

- eskiden her istek birer tcp bağlantısından gider gelirdi. yani birçok istek paralel yapılmak istendiğinde birçok tcp bağlantısı açılırdı. artık tek tcp üzerinden birçok frame karşı tarafa yollanabilir. bu sebeple hangi frame hangi request'e ait olduğunu anlayabilmek için her frame içinde stream-id kullanılır. aynı anda response geliyor olabilir ve biz data yolluyor olabiliriz. aynı stream'den giden ve gelen olamaz fakat diğer stream'lerden dönüş alınıyor olabilir. bu özelliğe "Multiplexing" deniyor.

- her origin için tek tcp bağlantısı olması daha basit bir yapıya kavuşturmuş oldu. eskiden bir tarayıcı her domain için ortalama 6 soket açıyordu. bu ölçümlere göre daha çok performans kaybına (cpu, ram) sebep oluyor ve komplekliği arttırıyordu.

- http dünyasında "message" terimi bir response yada request'i temsil etmek için kullanılır. bu terim http2'ye özgü değildir.

- header compress özelliği gelmiştir.

- priority: client birçok istek yapsın, bunların dönüşünde hangilerine öncelik verilmesi gerektiğinin bilgiside karşıya yollanıyor. bu özellik ile http-api'leri kendi içinde öncelik veriyor. bunun için yazılımcının ek bir ayar yada bilgiye ihtiyaç duymuyor. burada örneğin; web tarayıcıları önce css dosyalarının, ardından da resimlerin çekilmesini sağlayabilecek. çünkü resimlerin daha geç yüklenmesi, sayfanın hiç yüklenmemesinden daha verimli olacaktır..

- "HTTP/2 push" özelliği: sunucuya index.html'i döndürsün diye istrek yaptık. bize index.css, main.css gibi değerleri de dönebiliyor ekstradan. bu requestleri zaten %99 yapacağını bildiği için sunucu request beklemeden atıyor. web tarayıcısıda bunları cache'leyebiliyor (isterse).

  http2 anlatan birçok makalede bu madde için "server push" terimi kullanılmış. fakat tam olarak bu maddeye uymuyor. "server push" başka başlıkta anlatılıyor.

- binary data: eski sürümlerde satır sonu karakterlerinin bir önemli vardı. dolayısı ile satır sonu karakterine denk gelecek bir encoidng kullanmak zorundaydık. oysa artık byte seviyesindeki sinyaller kullanıldığından, byte seviyesinden bilgi alımı için ekstra parse/kontrol yapmaya gerek yoktur.

- http1.1 client, http2 sunucusunun döndüreceği cevabı algılayamaz. yani http2 geriye uyumlu diildir.

# SPDY

bir kısalmta değildir. özel isimdir. google'ın http alternatifi geliştirdiği ptotokoldür. fakat http2 çıkışı ile artık geliştirilmemektedir.

# http request methods

- get

  return details of given data.

- post

  - HTML üzerinden bilgi göndermek için kullanılır (form bilgileri gibi)
  - daha karmaşık işlemler gerektiğinde bu yöntem tercih edilmelidir:
    - birden fazla kaynak (aynı/tek bir istekte) gönderirken
    - içiçe kaynak güncellemelerinde

- patch

  kaynağı güncellemek için kullanılır

- put

  override (or create if not exist) the given data.

  put ile yepyeni bir kaynak oluşturulup yollanabilirken, patch ile mutlaka sadece varolan kaynak güncellenebilir. 

- options

  returns all methods of the given url.

- CONNECT

  http standartları üzerinde (ssh a benzer şekilde) daha düşük seviyede (tcp socket) tünel açıp artık yapılacak isteklerin oradan yapılması sağlanır. örneğin chrome tarayıcısında connect ile bir http isteği yapılır, onay alındıysa, artık yapılacak istekler o tünel üzerinden, connect isteği yaptığımız sunucuya gidecektir. connect isteği yaptığımız sunucu ile aramızda bir proxy var ise; o proxy artık yaptığımız işlemleri göremeyecektir. dolayısı ile aalında connect işlemi ile gerçek sunucu ile direk iletişimde olmaktayız. bu güvenlik açıkları da meydana getirmektedir. bu sebeple canlı sistemlerde CONNECT metodu devre dışı bırakılmaktadır.

- trace

  requestte gönderilen bilgiyi aynı şekilde döndürmektedir. test amaçlı kullanılmaktadır.

- DELETE

  delete given data

- HEAD

  get metodu ile aynıdır. sadece reposneta body yoktur. response header'da, LastModified/ContentLength gibi değerler mevcuttur. bu bigliler kullanarak tekrar get ile datayı çekmeye gerek varmı diye kontrol edilebilir. (başka başlıkta anlatılıyor)

(source-id: 196)'de her işlemde hangi status codun dönmesi gerektiği ve hangi dataların hangi durumlarda dönmesi gerektiği belirtilmiştir. örneğin; "4.3.3.  POST" başlığında POST işlemi ile bir kaynak oluşturulduğunda, response olarak 201 dönülmeli ve header'da "Location" dönülmesi ve bu değerde (location değerinde), oluşturduğumuz yeni kaynağa erişebilmek için gerekli "get" isteği url'sinin olması gerektiği belirtilmektedir.

rfc7231, (source-id: 197) gibi sayfalardan referans olarak kullanılmaktadır.

# Safe method vs Idempotent method
Idempotent kelime anlamı: etkisiz.

GET, HEAD, OPTIONS, TRACE "safe" metodlardır. çünkü sunucudaki state'i değiştirmezler. RFC'de "safe metod" olması imkansız yazmaktadır, çünkü suncu tarafta gerlen istekler'de log basılması bile sunucudaki statüyü değiştirmektedir, yani side effect yaratmaktadır.

Aynı istek birden fazla kere atılması veya sadece 1 kere atılması hiçbir farklılık yaratmayacak ise, bu istekler Idempotent method'lardır. RFC'de bunların Idempotent olduğu belirtilmiştir: GET, HEAD, OPTIONS, TRACE, PUT and DELETE.

Idempotent istek birden fazla defa sunucuya yollnadığında, sunucu aynı cevabı dönmek zorunda diildir. örneğin PUT ettik, "ok" döndü, tekrar PUT ettik bu sefer "already exist" döndü. ama bu "Idempotent" olmasını engellemiyor.

# conditional requests
Herhangi bir requestimiz'e cache header'larını ekleyerek duruma göre işlem yapmasını bekleyebiliriz. örneğin; get'e header ekleyebiliriz. eğer veri değişmişse bize yeni data döndürülür. put'a header ekleriz. eğer data şimdiki yollayacağımız data ile aynı ise, sunucuda put yapmaya gerek kalmaz. bu tarz request'lere conditional request denir. http standartlarında HEAD metodu bu iş için tasarlanmıştır. head'de body atılmaz sadece header'lar atılır. HEAD değişiklik var mı yok mu onun bilgisini döner. fakat body dönmez. standartlarda yoktur. bu sebeple herkes genelde; HEAD kullanmıyor. onun yerine diğer get veya put'a header eklemeyi tercih ediyor. çünkü head kullanılırsa tekrardan put ve get metodunu tekrar sunucuya atmak gerekebilir. fakat direk put ve get'e header ekleyince, sunucu conditiona'ı sağlarsa işlemi yapacaktır (get ise yeni datayı  döndürücek, put ise datayı update edecektir).

HEAD metodu header'da "ETag" veya/ve "Last-Modified" tagini barındırıyor. buna cevap olarak sunucu; aynı (istek) path'e "get" isteği yapılsaydı en son atılan response'takine göre değişiklik varmı yok mu onun bilgisini döner.

HEAD yerine get ve put kullanılacaksa hem "ETag" veya/ve "Last-Modified" hemde aşağıda anlatılan "if-match" gibi metodlarda kullanılabilir. 

apache http server static dosyaları dışarıya açarken bu özelliği otomatik sunar. yazılımcının ek bir configürasyon/kod girmesine gerek kalmaz.

javaee yada spring'de controllerlarda head isteniyor ise; bu metod elle hazırlanmalıdır. örnek bir wrapper yazılabilir:

```java
protected void doHead(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    doGet(req, response);
}
```

yukarıdaki metod filter'a eklenip eğer request HEAD ise çağrılabilir. bu şekilde her metod için ayrı HEAD yazmak zorunda kalmayabiliriz.

web tarayıcıları web standartlarını varsayılan olarak uygular ve static dosyalar için (örnek css, <img> ...) conditional request kullanıyor fakat head ile değil. bir elemanı çekmek için en son tarayıcnın çektiği tarihi "get" metoduna "If-Modified-Since" olarak ekliyor. sunucu eğer hala değişiklik yoksa cevap olarak bunu bildiriyor. eğer değişiklik var ise; direk cevap olarak yeni datayı gönderiyor. bu control web tarayıcı tarafından cache disable edilmedikçe otomatik yapılır.

"spring-data-rest" modülü databasedeki değerleri direk önyüze sunucucak kontrollerları da otomatik hazırlıyor. bikaç annotation kolayca entitylerimizi önyüe hazırlıyor ve head kontrollerini de standartlara bağlı olarak dışarıya açıyor. spring-data-rest pek tavsiye edilmez. çünkü database nesneleri genelde direk tümü ile önyüze açılmazlar. bazıları static parameter servislerini spirng-data-rest ile dışarıya açıyor. spring-data-rest modülü her nentity için put, get gibi tüm metodları dışarıya hazırlıyor ve Richardson Maturity Model Level-3'ü de hazırlıyor.

database'lerde otomatik olarak bir satır değiştiğinde, o satırda belirlediğimiz bir sutnuna otomatik tarih atılabiliyor. bu özellik için javada da entity içinde o sutun için özel bir annotation bulunmaktadır. bu şekilde önyüze HEAD metodlarımızı hazırlarken bu sutundan yararlanabiliriz.

# strong ve weak validator

W/ karakterlerini hash'lerin önüne atarsak sunucunun weak kontrol yapmasını istemiş oluruz. atmazsak strong istemiş oluruz.

strong ve weak'in anlamı yazılım geliştiricinin tanımına kalmıştır. örneğin bazı mimarilerde strong kontrol, header'ları dahi kontrol eder. bazı mimarilerde ise; strong iligli kaynağın çok önemli verilerinin değişip değişmediği anlamına gelir.

# cache ile ilgili header'lar

(cache harici diğer header'lar başka başlıkta anlatılıyor)

- #### Cache-Control (eski sürüm http'lerde "Pragma"):

alabildiği değeler: (multiple değerler alabiliyor)

- no-cache: data must be re-validated on each requeest

- no-store: never cache

- public: can be cached by the browser and any intermediate (proxy) caches

- private: only browser should cache it

- max-age: max age of cached content as second. on new http versions replaced by "Expires" header.

- s-maxage: max-age ile aynı görevi görüyor fakat bu client haricindeki aracılar (proxy) için geçeri bir değerdir.

- #### ETag

Cache verisinini değişip değişmediğini kontrol etmek için kullanılan değer.

- #### If-Match

örnek kullanım:

If-Match: "34242"

sağ taraf kaynağın hash'idir. eğer değişiklik var ise sunucu kaynağı dönmeyecek. eğer değişiklik yok ise kaynağı dönecek.

if-match içine birden fazla değer atanabilir. örnek:

If-Match: "34242", "34666"

- #### If-None-Match

If-Match'in tersidir. eğer kaynak'ın hash'i bu değil ise tüm kaynak döndürülecektir.

- #### If-Modified-Since

burada bir tarih değeri sunucuya yollanıyor. eğer bu tarihten sonra ilgili kaynak güncellenmiş ise tüm kaynak cevap olarak dönecektir.

içine birden fazla tarih değeri atabiliriz.

- #### If-Unmodified-Since

If-Modified-Since'in tersi.

- #### IF-Range

içine tarih yada hash degerini alabiliyor. bu header ile beraber farklı bir header'da "Range" değerini yollamak şart.

içine sadece bir tane değer alabiliyor.

if the entity (only the part of range) is unchanged, send me the part(s) that I am missing; otherwise, send me the entire new entity.

- #### Last-Modified

sunucu tarafından client'a gönderilen bir header'dır. ilgili kaynağın en son ne zaman güncellendiğini belirtir.

- #### 304 Not Modified

bu status sunucu tarafından client'a eğer değişiklik yok ise gönderiliyor. eğer kaynakta değişiklik var ise sunucu 200 OK döndürüyor. fakat her request için aynı cevap dönmeyebiliyor. istisnai durumlar çok fazla.

# payload

türkçe kelime anlamı: yük.

iletişim protokollerinde metada'lar dışında kalan mesaj bloğudur. asıl gönderilmek istenen mesaj kısmıdır. doğal olarak; sadece ajax işlemlerinde kullanılan bir terim değildir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Viewport
Sayfa yapısı ile ilgili kararları vermemize yarayan meta etiketidir. HTML HEAD tag'larının içerisinde olmalıdır.

örnek;

sayfa ilk yüklendiğinde %100 zoomlanmış olmalıdır:

<meta name="viewport" content="initial-scale=1" />

genişliğin 360 pixel olduğunu belirtiyoruz. tarayıcı buna göre sayfayı fit edebilir.

<meta name="viewport" content="width=360" />

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Document Object Model
DOM, bir programlama lisanı veya sadece JavaScript için tasarlanmış bir olgu değildir. DOM, HTML ve XML dokümanları için API'dir. genelde DOM denilince HTMK dökümanları için olan API akla gelir fakat sadece bu değildir.

# xhtml (or Extensible HyperText Markup Language)
html standartları katı kurallara sahip değildir. örneğin xml teglaeri büyük harf yazılabilir. oysa xhtml bu kuralları daha katı standartlara baglamıştır. xhtml tarayıcılar tarafından desteklenir çünkü yine xml yapısındadır. sadece kurallar daha katı tututlur. temiz kod sağlanır.

# DHTML (or Dynamic HTML)
CSS Javascript ve HTML çalışan yapılara verilen isimdir.

# HTML DOM Levels
HTML DOM'ün sürümleridir. DOM'un çalışma prensiplerinin kurallarıdır (spesifikasyonlarıdır). DOM 1, DOM 2, DOM 3, DOM 4...

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# cookie security policy
cookie'ler:

- port: aynı domain'inin tüm port'larındaki sercisler tarafından kullanılabilir. port önemsizdir.
- subdomain: subdomain'ler cookie spesific programatic olarak belirtilebilmektedir.
- path: path bilgisi önemsizdir.

# cookies properties

- secure: sadece https üzerinden giden ajax isteklerine eklenir. http ise gönderilmez.

- httpOnly: javascript tarafından bu cookieler okunamaz. fakat her ajax isteğinde sunucuya gönderilir.

- Expires (or Max-Age): son kullanma tarihi

- Path: o domain için kimlerin bu cookie'ye erişebileceği yetkisidir. path'in prefix'idir. tüm bu prefix'e ait subdirectorie'ler (sub-url'ler) bu cookie'ye erişebilir.

- same-site: 
  
  3 farklı değer alabilir:

  - Strict

    ilgili cookie sadece kendi path'ine bağlı yere yollanabilir.

  - Lax

    ilgili cookie; third-party sitelere sadece GET isteği ile yollanır veya top-level domainde sadece cookie'nin path'indeki sunuculara yollanır.

  - none

    same-site alanı için default değerdir. eğer same-site boş bırakılırsa none olarak set edilir. fakat güncel tarayıcılarda artık default değer Lax'tir.

    tüm ajax isteklerinde bu değer request'e ekleniyor.

- domain: hangi domainlerin buna erişicek yetkisi olup olmadığıdır. normalde tarayıcılar başka domainden cookie okumaya veya yazmaya izin vermez fakat bu kısım 2 sebepten ötürü yapılmıştır:
  - third party cookie'lere izin veriliyor (başka başlıkta anlatılıyor)
  - sub-domain'ler belirtilebilir: her subdomain (a.google.com, b.google.com gibi) sadece kendi yada o domaine bağlı tüm subdomain'ler tarafından erişilebilir cookie set edebilir.

# third party cookie vs first party cookie
- a.com'a gittik.
- r.com içerisinden bir js yüklendi
- r.com kendi içerisinde cokkie set etti (javascript'te cookie set ederken domain de belirtilebilir). bu senaryoda r.js kendi domainine cookie set ediyor.
- Daha sonra b.com'a gidildi ve yine r.com'un bir js'i yüklendi. r.com b.com'a gidildiğinde, bu kullanıcının a.com'a da gittiğini görebiliyor. çünkü kendi cookie'leri third party.

son kullanıcı tarayıcıların ayarlarından basit bir şekilde bunu disable edebiliyor.

# supercookie
sadece ".co.uk" ".com" gibi domain barındıran cookie'lerdir. çok tehlikelidirler. ".co.uk" olan her domain bu cookie'leri görebilir.

supercookie terim, bazı kaynaklarda cookie dışında başka anlamda kullanılmaktadır. web standartlarında olan fingerprinting açıklarına da bu supercookie denilebilmektedir.

# media file transfer cookies
media dosyaları web tarayıcı tarafından otomatik sunucudan çekilirken, varolan cookie'ler sunucuya yollanmaktadır. nihayetinde resimlerde çekilirken, http isteği yapılmaktadır.

# firefox and chrome cookie management
- chrome ile bir sayfada inspect element yapıldığında, cookie kısmında www.a.com grubu altındaki cookie'ler listelendiğinde, domain sutununda bazen www.a.com'dan farklı domain'lerin olduğunu görebiliriz. bunun sebebi a.com'da (inspect ettiğimiz sayfada)  farklı iframe'ler olmasıdır. farklı domain grupları ise, javascript tarafında gidilen sayfanın (a.com'un), farklı domainler için set ettiği cookie'lerdir. oysa firefoxta cookie'ler listelenirken sadece domaine göre gruplandırılmaktadır.

- firefox ve chrome private mod'larda cookie'ler ile ilgili hiçbir farklı politika izlemiyor.

- cookie'ler güvenlik sebebi ile varsayılan olarak tarayıcılar ile editlenemiyorlar. bunun için eklenti kullanmak şart.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Diğer sitelere login olup olmadığı bilgisini edinme

Örneğin facebook'a login olunca, instagram ayrı sekmede facebook'a login olduğumuzu anlayabiliyor. Bunu ufak bir hack yöntemi ile gerçekleştiriyorlar. Bu açık bir CSRF tipi bir saldırıdır. Bir siteye giderken yönlendirmeler kullanılabilmektedir. Örneğin; https://www.facebook.com/login.php?next=www.facebook.com/bookmarks/Fpages  bu sayfa ğer kullanıcı login olmuşsa bizi "next" parametresinde yazan yere yönlendirecektir. Eğer login olmamışsak login sayfasına yönlendirecektir. İşte bu isteği  bir sekmeden yaptığımızda, login syafasına gidilmiyorsa, facebook'a login olunmuştur demektir. Fakat farklı sekemede farklı domainden request yapmamız güvenlik gereği engellenmiştir. İşte JSONP de olduğu gibi benzer bir trik uygulanıyor. <IMG> elementi sayfaya (DOM'a) include edilirmiş gibi bir kod yazılıyor:

```html
<img onload="alert('logged in to fb')" onerror="alert('not logged in to fb')" src="https://www.facebook.com/login.php?favicon.ico">
```

Bu resim dosyasına web tarayıcıları her zaman farklı domaine izin veriyor. çünkü siteler normalde CDN kullanmaktadır video ve resimler için. Yukarıdaki örnekte https://www.facebook.com/login.php?next=www.facebook.com/myprofile/photo.jpg olduğunda dosya eğer login olmuşsa kullanıcı çekilmektedir. Dolayısı ile kullanıcının login olup olunmadığı, hatta bazen profil fotosu da çekilebilmektedir.

Bazı siteler tüm resimleri CDN'e yüklediklerinden işler daha da karışmaktadır ve bu tehlikeyi engellemektedirler. Fakat bazı sitelerin en çok kullanılan standart dosyası olan favico.ico resim dosyası çekilmektedir.

# Content Blocking (or tracking protection)

- bu özellik başka bir çok tarayıcı eklentisinde de mevcuttur.

- başka domaine istek yapmamızı engellemektedir. Bu listeler firefox içerisine gömülmüştür (blacklist). Örneğin; facebook.com/next=facebook.com/# firefoxta, facebook haricindeki tüm sitelerden resim objesi içerisinden dahi engellenmektedir. böylece başka sitelere login olup olmadığımızı kimse takip edemeyecektir.

- firefox private mode'da Content Blocking'i açık tutuyor yada basit GUI seçeneklerinde normalde açılabilmesini sağlıyor.

# mixed content

https başlatılan bir sitede daha sonra http yüklenen bir dosya var ise bu duruma denir.

2 ye bölünür:

- active: css, html, js, iframe, flash gibi sayfanın yapısını değiştirebilecek tehlikeli dosyalar. bu dosyalar tarayıcılar tarafından engellenmektedir ve developer consola çıktısı kırmızı ile uyarı şeklinde verilmektedir.

- pasif: video, ses, resim gibi sayfanın sadece görünümünü değiştirebilecek dosyalar. bu dosyalar tarayıcılar tarafından engellenmiyor fakat developer console'a warning veriliyor.

# XSS (or Cross Site Scripting)

Cascading Style Sheets (CSS) ile aynı kısaltmaya sahip olduğu için XSS olarak kısaltılır.

HTML formalarında, yada url'den giden parametreler manuel olarak değiştirilerek, sunucu tarafta SQL injection , yada HTML tarafında değişikliklere yol açan script'lerdir.

XSS saldırılarını engellemenin en temel ve köklü yöntemi HTML'de her karaktere gelen entity'leri kullanmaktır.

çeşitleri: (kaynak: (source-id: 198) )

- # Stored XSS (AKA Persistent or Type I)

  kötü amaçlı kodların web sunucusunda veritabanında kayıt edildiği durumları temsil eder. "commentler" buna en iyi örnektir. buradaki datalar başka user'lar tarafından görüntülendiğinde kötü amaçlı kodlar çalışacaktır.

- # Reflected XSS (AKA Non-Persistent or Type II)

  bu tarz xss'ler sadece o andaki user için çalışır. yani genelde input veya url alanlarına yapılan girişler sonucunda, kotü amaçlı kodlar kendisine yansır. tabi saldırılar diğer kullanıcılara yapılacağı için, genelde başkasının bir yerlere tıklamasını sağlamak gerekir. örneğin sahte bir email atıp, kötü amaçlı kodların user'ın kendisi tarafından tetiklenmesi beklenir.

- # DOM Based XSS (AKA Type-0)

  DOM Manipülasyonu yapan XSS'lerdir.

# XSS in react framework
reactjs yapısı gereği XSS ataklarının baıları engelliyor. View katmanında (render'dan dönen view) dinamik variable varsa onu string olarak escape karakterlerini ekliyor. en basit örnek üzerinden gidelim:

```jsx
var htmlString = '<img src="javascript:alert('XSS!')" />';

render() {
    return (
        <div>{htmlString}</div>
    );
}
```

result:

```html
<span>"<img src="javascript:alert('XSS!')" />"</span>
```

Fakat bu tüm XSS açıklarının kapatıldığı anlamına gelmiyor. kaynak: (source-id: 199) "CyberPanda Consulting" answer at Aug 15 2018 at 3:33.

# HTML character entities

  Bir string'in her karakteri (or sadece özel karakterleri) html referansına çevirirsek ekranda her zaman bu metin gösterilecektir. fakat ekranda HTML olarak gösterilmesi gerekiyorsa işte o zamana riskler artmaktadır. buna örnek bir durum: gmail web arayüzünün bize html formatında atılan bir emaili, web browser'ımızda bir divin içerisinde göstermesi örnek verilebilir. işte bu gibi durumlarda verilen HTML string'ini safe hale getiren (eventlerini silen), bilinen XSS saldırılarını temizleyen kütüphaneler kullanılmaktadır. örnek kütüphane: htmlpurifier (source-id: 432)

  burada firefox html 4.0 için tüm character entity listesi vardır:

  (source-id: 200)

  Birçok karakterin hem name hemde code olarak gösterimi vardır. örnek:

  | Result | Description                        | Entity Name | Entity Number |
  |--------|------------------------------------|-------------|---------------|
  |        | non-breaking space                 | &nbsp;      | &#160;        |
  | <      | less than                          | &lt;        | &#60;         |
  | >      | greater than                       | &gt;        | &#62;         |
  | &      | ampersand                          | &amp;       | &#38;         |
  | "      | double quotation mark              | &quot;      | &#34;         |
  | '      | single quotation mark (apostrophe) | &apos;      | &#39;         |
  | ¢      | cent                               | &cent;      | &#162;        |
  | £      | pound                              | &pound;     | &#163;        |
  | ¥      | yen                                | &yen;       | &#165;        |
  | €      | euro                               | &euro;      | &#8364;       |
  | ©      | copyright                          | &copy;      | &#169;        |
  | ®      | registered trademark               | &reg;       | &#174;        |

  Bazı karakterleri bir önceki karakterlerin üzerine ekleme de yapabiliyor:

  | Mark | Character | Construct | Result |
  |------|-----------|-----------|--------|
  | ̀     | a         | a&#768;   | à      |
  | ́     | a         | a&#769;   | á      |
  | ̂     | a         | a&#770;   | â      |
  | ̃     | a         | a&#771;   | ã      |
  | ̀     | O         | O&#768;   | Ò      |
  | ́     | O         | O&#769;   | Ó      |
  | ̂     | O         | O&#770;   | Ô      |
  | ̃     | O         | O&#771;   | Õ      |

  html 5'te birçok karakter daha destekleniyor:

  (source-id: 201)

  HTML ile artık karakterler unicode code point'i ile referans ediliyor. tüm unicode desteklenmemektedir. sadece belli bir kısmı destekleniyor.

  Fakat XHTML ile HMTL arasında bir ortak çözüm olmadığndan ve HTML geriye uyumluluğu için &amp;, &lt;, &gt;, &quot; and &apos; haricindeki karakterler normal yazılması önerilir. kaynak: (source-id: 202)

# CSRF (or Cross-Site Request Forgery or XSRF)
Forgery kelime anlamı: sahtecilik

resmi olmayan kullanımları:
- one-click attack
- session riding
- CSRF'in "sea-surf" olarak okunduğunu sıkça duyabiliriz.

yetkisi olmadan istek yapan http istek çeşitleridir. örneğin; yetkisi olmadan şifre değiştirmeye çalışan, yada yetkisi olmadan mesaj silen her HTTP isteği CSRF grubu altındadır. 

CSRF case'ine şöyle yakalanabiliriz: bir bankaya login olduk. Yan sekmede mailimize bakıyoruz. Kötü niuetli bir email açtık. Mailin içinde banka domainine yapılan bir request oldu. bu request birçok şekilde tetiklenebilir:
- event click sonrası (son kullanıcı hatası)- ki bazen bazı yerler link diilmiş gibi CSS yazılıyor, oysa orda bir link oluyor...
- tarayıcılarda medya dosyaları oto yüklenir. GET isteği atılması sağlanabilir. Oysa karşı tarafta bir medya yoktur. CSRF engellemek için REST servislerimizi (en azından önemli request'leri) GET değil, POST yapmamız gerekiyor. En azından, web tarayıcısı user-click yapmadan hiç POST yapmıyor.

Burada önemli olan nokta şu: isteği atarsınız ama dönen cevapta o domainin cookie'sine vs yazamazsınız.

CSRF'i engllemenin en önemli çözümü, her response'ta client'a sadece memory'de tutması gereken bir random geçici token atmaktır. Her request'te bu token o client'tan mı gelmiş anlarız.

# CSRF vs XSS

xss sadece client side koşulan kötü amaçlı scriptleri kapsar. XSS'te yetki yada HTTP-istek konusu olmak zorunda değildir. xss, CSRF kümesini ve daha fazlasını kapsar.

# chrome guest mode vs private mode
- her iki modda da pencereler kapatıldığında bilgiler saklanmaz.

- private mode sık kullanılanlarda değişiklik yapabilir ve eklentileri kullanmaya devam edebilir. oysa guest mode, anında (gues isimli)  bir profil açar ve pencere kapatılınca o profili siler.

- google chrome'un gizli moduna "incognito mode" ismi verilmiştir. Incognito tütkçe anlamı: kılık değiştirmek, sahte ad.

# firefox vs chrome private mode
Private mode seçeneklerinin ilk çıkış amacı, sadece private mode penceresi kapatıldığında history'nin saklanmamasıydı. Dha sonrasında farklı ek özelliklerde eklenmeye başladı. Bu sebeple bir web sayfası, private mode'da aynı şekilde açılmayabilir. Örneğin; firefox (aksi tanımlanmadıkça) private mode'da Content Blocking'i açık tutuyor. Normal browsing'de bunu açmıyor. Normal browsing'de ancak özel tanımlama yapılırsa açılıyor.

Bir problemde firefox ve chrome'un private mode'ları farklı yönetmesidir. Bir tarayıcıda private mode'da bir özellik aktif iken, diğerinde olmayabilir.

# firefox profiles
firefox -p parametresi ile profile manager açılır. chrome'da olduğu gibi farklı profiller mevcuttur.

# Multi-Account Containers
firefox'un bir eklentisidir. bu eklenti ile aynı profile içerisinde her sekmenin birbirinin cookie'leri ve diğer storageleri hiç görmemesi sağlanabilir. örneğin 2 facebook hesabı farklı sekmelerde açılabilir.

# adblock vs adblock plus
sadece reklamları engellemek amaçlı yapılan tarayıcı eklentileridir. 2 farklı proje.

# uBlock Origin (or uBlock₀ or old-name:μBlock) vs uMatrix
bu eklentiler tarayıcıdan content engellemesi için yapılmıştır. herhangi bir javascript'i yada nesneleri filtreler hazırlayarak engelleyebilmemizi sağlar. adblock ve adblock plus'a göre çok daha gelişmişlerdir. kullandıkları filtreler, diğer add-block eklentilerindeki filtreleri de desteklemektedir(uyumludur).

# noscript
web sayfasındaki elementleri parçalı/tamamiyle engelleyerek güvenliği sağlamakta. örneğin sadece script tag'lerini, sadece font'ları, sadece webgl'i, sadece media'ları engelleyebiliyor.

# ghostery
analitic firmalarının istek yapmasını engelliyor. fakat bu sonuçları kendi sunucularında topluyor ve yine engellediği firmalara satıyor.

# WOT (or Web of Trust or myWOT)
bu eklenti kullanıcılardan site güvenliği hakındaki oylamalarını toplamaktadır. ve bu oyları sürekli tarayıcının tepesinden göstermektedir.

# addblocker web sitemizdeki bir kaynağı engellerse ne yapmalıyız?
- "addblocker plus" eklentisi firefox developer menüsünde özel sekme ekliyor. buradan bir web sitesine gidildiğinde hangi objelerin engellendiğini görebiliyoruz.
- önce hangi filtrenin sitemizdeki kaynağı engellediğini bulmalıyız. bunun için addblocker eklentimizdeki listeleri tek tek disable edip her disable işleminden sonra web sayfamızı reload etmeliyiz. hangi filtrenin engellediğini tespit edersek, o filtrenin resmi sitesine gidip geliştiricileri ile iletişime geçmemiz gerekir.
- filtreler addblock eklentileri/uygulamalarından bağımsız olarak başkaları tarafından geliştirilir.
- eğer engellenen objeler reklam ise, geliştiriciler olumsuz dönüş yapacaktır.

# add blocker'a yakalanmamak için ne yapılmalıdır
- html veya kaynakların url'lerinde "add, addvertise, banner" veya bunları içeren string'ler var ise bu kaynakalrımız mutlaka engellenecektir.
- bazı reklamların tasarımı uygun ise, bazı filtreler bunları kaldırmıyor. uygunluğun birçok standardı var. bunlardan bazıları:
  - browser'da bellek tüketimine sebep olmaması
  - video olmaması
  - resim ise resim formatının düşük kalitede olması
  - resim ise ufak boyutta olması
  - ekranda son kullanıcıyı rahatsız etmeyecek pozisyonda olması
  - bazı filtreler resimleri de engelliyor. sadece text reklamları kabul ediyor (hafif olduğu için)
  - arkada çalıştırdğı js'in kullanıcı gizliliğine saygı duyuyor olması
  - ekranda ufak boyutta olması

Bazı filtreler +18 içerikleri de engelliyor. bu filtreler genelde iş yerlerinde aktif ediliyor.

# add blocker'ı algılamak
browser'da addblocker olup olmadığı kolaylıkla algılanabilir. hatta kullanıcının hangi filtreleri devreye almış olduğu bile tespit edilebiliyor (çünkü bilinen sık kullanılan filtreler var - açık kaynaklı). bunlar için birçok farklı yöntemler var. fakat bu yöntemler sürekli olarak değiştiriliyor, çünkü her tespit eden koda karşılık, addblocker'lar tarafından bunları engelleyen kodlar tasarlanıyor.

add blocker'ı algılamak için çok basit ve temel bir örneği ele alalım:
- /ads.js'e bir istek yaparız. eğer isteğimiz engelleniyor ise, kullanıcı addblocker kullanıyor demektir.
- sitemizde id'si "addvertising" olan bir div yaratırız. sayfa yüklendikten sonra bir js ile bu div'in içindekilerin yada div'in manüpüle edilip edilmediğine bakarız. eğer manüpilasyona uğramışsa, son kullanıcı addblocker kullanıyor demektir.

adblock, adblock plus, ublock origin, uMatrix varsayılan olarak kendilerinin çalıştığını karşı tarafa gizleme gibi bir dertleri yok (zorunlu kalınmadığı takdirde). fakat bu eklentilerin bazı forkları kendilerinin çalıştığını ilgili web sayfasına engellemektedirler.

# adblocker'lar nasıl çalışır
 ABP-compatible filters'larda 2 tip engelleme var:
- network filters

  network isteği direk engellenir

- Cosmetic filters (ublock origin cosmetic diye isimlendiriyor. adblock ve adblock plus "element hiding" olarak isimlendiriyor.)

  netwokr isteğinden dönen cevap engellenmez, fakat sayfadaki content, HTML DOM içerisinden silinir veya hide edilir.

# filtreler
ublock origin eklentisinin ayarlarındaki "filtre" sekmesine girildiğinde birçok farklı kategoride filtre görünecektir. Bunların bazıları:

- built-in
  
  karışık (diğer tüm kategorilerden filtreler burada var).

  default'ta ublock origin community'si tarafından yönetilen ve aktif edilmiş durumda olanlar.

- ads

  sadece reklamları engelleyen filtreler

- privacy

  takip edilmek için yüklenen contentleri engelleyen listeler.

- malware domains

  malware olduğu belirlenen domainleri/contentleri engelliyor.

- annoyaces

  önemsiz bildirimleri/contentleri (gereksiz popup'ları: bun en güzel örnek: "cookie koşullarımızı kabul etmektesiniz" popup'ları) engelliyor.

- regios, languages

  ülke/dil bazlı sitelerin filtreleri.

# Canonical Name record (or CNAME record)
DNS server'lar bir DNS kaydını farklı bir DNS'e referans ettirebilir. örneğin mail.domain1.com'u, domain1.com gibi gösterebiliriz. Bunu DNS sunucuları destekliyor. Bu tarz DNS kayıtlarına CNAME record denir.

Web tarayıcıları veya eklentileri 3üncü party siteleri engellemeye başladığından, bazı internet siteleri kendi sub domain'lere istek yaptırarak diğer 3üncü parti sitelere ulaştırmaktadırlar.

Bunu engellemek için ublock origin eklentisi ilk adımı atmıştır. first party'de olsa ilgili request'leri engelleyebilmektedir. fakat eklenti altyapısı gereği bu özellik sadece firefox'ta desteklenebilmektedir. kaynak: (source-id: 203)

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# HTML icin "Object" ve "embed" tag'leri
iki tag'de aynı görevi görmektedir. örnek kullanım:

```html
<object type="application/pdf" data="filename.pdf" width="100%" height="100%">
</object>
```

bu şekilde tarayıcının eklentileri çağrılabilir durumda olmaktadır. örneğil pdf, wsf (flash) gibi. tarayıcı "data" da belirtilen dosya uzantısına göre yada "type" ile belirtilen mime-type'a göre eklentiyi devreye sokar. son kullanıcı bu dosyaların neyle açılacağını tarayıcının özelliklerinden set etmiş olmalıdır. örneğin bir video açılacakken tarayıcının embed video görüntüleyiciside açılabilir, vlc'nin tarayıcıya kurduğu eklentide açılabilir.

HMTL5'te embeed tagı ile açılan video player'ın teması neredeyse tümüyle değiştirilebilir durumdadır. böylece herkes kendi player'ını tasarlayabilmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Browsers and their engines

# internet explorer version history
Burada birçok versiyon için minimum gereksinimler ve hangi işletim sistemine kurulabileceği detaylı şekilde yazmaktadır: (source-id: 204)

Burada ise daha eski versiyonlar için detaylı bir tablo mevcut: (source-id: 205) "Release history for desktop Windows OS version" başlığı ikinci tablo.

# Edge version history
Detalı bir tablo burada mevcut: (source-id: 206) "Release history" başlığındaki tablo (wikipedia sayfasındaki bu tabloyu görüntülemek için tabloda [show] seçeneğini seçmek gerekiyor).

Edge Windows'ta default yüklü gelmeyen OS'lara da kurulabiliyor. kaynak: (source-id: 207)

Birkaç versiyon:

| version  | engine            | public release date | comment                              |
|----------|-------------------|---------------------|--------------------------------------|
| 20.10240 | EdgeHTML 12.10240 | July 15, 2015       | first public release                 |
| 44.19041 | EdgeHTML 18.19041 | 2020                | latest version before blink engine   |
| 79.0.309 | Blink 79          | January 15, 2020    | first public release of blink engine |
| 81.0.416 | Blink 81          | April 13, 2020      |                                      |

# browser and engines

| NAME                                                                                         | JS ENGINE         | BROWSER ENGINE     |
|----------------------------------------------------------------------------------------------|-------------------|--------------------|
| internet explorer (11. sürümde geliştirmesi durduruldu. Artık Edge tarayıcısı kullanılıyor.) | ?                 | Trident(or MSHTML) |
| Microsoft Edge (or Spartan) (2018'in sonlarına kadarki sürümler)                             | chakra            | EdgeHTML           |
| Microsoft edge (or Spartan) (2020'den sonraki sürümler) (2)                                  | v8                | Blink              |
| firefox                                                                                      | SpiderMonkey      | gecko              |
| safari                                                                                       | Nitro*(1)         | WebKit             |
| google chrome                                                                                | v8 (or Chrome V8) | Blink              |
| opera (14. sürüme kadar)                                                                     | Carakan           | Presto             |
| opera (14. sürümden sonra)                                                                   | v8                | Blink              |
| yandex browser                                                                               | v8                | Blink              |

- (1) Safari Js Engine
  - WebKit, JavaScriptCore ve webcore olarak 2 temel projeden oluşuyor.
  - JavaScriptCore, WebKit projesinin bir alt projesidir.
  - JavaScriptCore tekrardan birçok kere optimize edildi. Sırası ile yeni isimleri: SquirrelFish --> SquirrelFish Extreme (or SFX or Nitro)

- (2) chromium tabanlı tarayıcı 2019'un başlarında developer kanallarından sunulmaya başladı. ilk public release 2020'nin başlarında çıktı.

# NodeJS
V8 tabanlıdır.

# SunSpider
benchmark(kıyaslama) tool that measure JavaScript performance.

# Netscape
Netscape firması tarafından geliştirilen tarayıcı. daha sonra açık kaynaklı oldu ve mozilla kurumu ile geliştirilmeye devam edildi. fakat mozilla daha sonra sıfırdan tarayıcı yazdı.

# Aurora
Firefox'un beta ile nightly version arasındaki sürümü.

# Firefox focus
firefox'un sürekli gizli modda açılan ve gömülü adblocker içeren versiyonu. lisans sorunları sebebi ile; almanca sürümlerinde "firefox klar" olarak adlandırılmaktadır.

# Firebug
Firefox'un içinde gelen default developer tool'un alternatifi açık kaynaklı bir eklentidir. artık geliştirilmiyor.

# Fennec
firefox'un tüm mobile versiyonları için kullanılan resmi bir takma isimdir.

# IceCat (or old-name:IceWeasel)
gnu projesi kapsamında firefox'un  içindeki lisanslı paketlerin çıkarılarak yaratılan forkudur. içerisinde varsayılan olarak eklentiler barındırıyor.

# Fennec F-Droid
Firefox f-droid gibi marketlerde yer almamaktadır ve public ftp indirme sunucusu sunmamaktadır. bu sebeple community, firefox'un kodunu sürekli derleyerek f-droid mağzasında bu isimde dağıtmaktadır.

# Waterfox
düzenli olarak firefox'tan fork olan proje. telemetrilerin disable edildiği, çok temel isteklerin yapıldığı proje.

# Palemoon
firefox tabanlı fakat firefox'u düzenli olarak fork etmeyen bir proje.

# GeckoView
mozilla'nın resmi olarak geliştirdiği android için webview'dır. 

- Firefox Preview (stabil sürüme çıktığında, normal "firefox" olarak kullanılıyor)
- Firefox Reality
- Firefox Focus

uygulamaları bunu kullanarak geliştirilmektedir.

# Firefox Preview
mozilla firması android için firefox'u sıfırdan tasarlamaktadır. proje varolan firefox'un android versiyonuna paralel yapılmaktadır.

projenin kod adı: fenix

bu paket stabil versiyonuna ulaştığı için kaldırıldı. artık google play store'dan firefox'un stabil sürümü indirildiğinde bu güncelleme zaten geliyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# submit request vs Ajax
Bu konu başlığı da okunması faydalı olacaktır: [java.md "JSP ile single page application"](https://github.com/yusufd89/notes/blob/master/java.md)

sunucu taraf isteğin submit mi yoksa sadece js ile yollanmış ajax isteği mi bilmiyor.

Sunucu, client'ın yapacağı bir javascript-AJAX isteğinde sayfayı yönlendiremez. javascript tarafında, ajax sonrası programatik olarak sayfa URL'sini değiştirmek gerekir. Oysa submit işleminde buna gerek yok. sunucu, submit işlemi sonrası html döner. bu HTML direk olarak web tarayıcısında gösterilir. tabi web tarayıcısında artık istek yapılan URL vardır. Eğer son kullanıcı bu son durumda sayfayı refresh etmek isterse, aynı submit isteği aynı sekmede tekrarlanır. Submit işleminde kritik bilgi barınabileceğinden, web tarayıcısı güvenlik gereği popup'ta soru sorar.

```html
<form method="post" action="/login">

  <input type="text" name="name">
  <input type="text" name="surname">

  <input type="submit">Submit</input>
</form>
```

- HTML standartlarında form içinde form olmaması gerektiği belirtilmektedir. kaynak: "Example of a form" başlığında (source-id: 208)

- form submit default'ta GET'tir. eğer method="post" yazarsak POST olur.

- örnekteki "surname" ve "name" attribut'leri submission method GET ise URL'de sona eklenir (query param olarak eklenir). örnek:

  ```
  www.currentdomainofwebpage.com/login?name=Ahmet&surname=Kemal
  ```

  eğer method POST ise o zaman body'ye eklenir.

- Birçok web tarayıcı veya postman gibi http-GUI-client'lar form POST işlemlerini, "Form Data" diye özel bir kısımda gösterir. Bu tamamane GUI'nin verdiği bir isimlendirmedir.

- form element can take "enctype":
  - __application/x-www-form-urlencoded__
  
    URL encoded form. This is the default value.

  - __multipart/form-data__
   
    when the user wants to upload files

  - __text/plain__
    
    A new form type introduced in HTML5. simply sends the data without any encoding.

- URL standartlarında boşluk karakteri yerine + karakterini koymanın tanımı yoktur. Boşluk karakteri yerine farklı bir karakter kullanmak gerektiği belirtilmiştir. kaynak: (source-id: 209).

  Fakat web standartlarında URL'de boşluk yerine, + koyulmalıdır. kaynak: (source-id: 210) "application/x-www-form-urlencoded" başlığı.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

- hash mark (or #)

- hash-bang (or #!)

- ! (or bang or ünlem işareti or Exclamation Mark)

- Fragment
kelime anlamı: parça

- URL'lerde sadece hash işareti ile linkler sayfadaki  bir yere yönlendirmek için (sunucuya istek olmadan) kullanılır. # ile yönlendirilen sayfalar "fragment identifier" aracılığı ile sayfanın hangi kısmına gideceğini bilirler.


- _escaped_fragment_=
Bu string google (ve diğer) arama robotları tarafından html sayfalarını gezerken kullanılmaktadır. Arama için indexlenecek sayfa url'sinde hash-bank var ise; ! işareti kısmını bu string ile değiştiriyor. Bu şekilde gidilen sayfa bu keyword'ü okuyor ve eğer bu keyword var ise static (içerde ajax işlemi yapmayan, robotlar javascript çalıştırır) bir html sayfası döndürüyor. Çünkü arama motorları dinamik sayfaları çalıştıramaz.

- \<meta name="fragment" content="!"> etiketi Ajax içeren sayfalara koyulur. Eğer robot bu syafaya gelirse bu etiketi görünce aynı url'ye _escaped_fragment_= ekleyip yeni url'ye gider.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# html 5 yenilikler

- table footer gibi div yerine kullanılacak hazır tasarım şablonları

- video ve audio elemenleri geldi. bunlarla flash yada eklenti ihtiyacı kalktı.

- bazı elementler ve attribute'ler çıkarıldı, ve yenileri eklendi.

- form elementler için tipler geldi.

- canvas

- offline web app (web-cache or app-cache): cache mekanizması. artık manifest dosyaları ile hangi dosyaların tamamen offline hangilerinin ise kesinlikle internetten çekilebileceği belirtilebiliyor. \<html manifest="cache.appcache"> ile dosya verilmelidir. web cache daha sonra standartlardan kaldırıldı. html5 öncesi tarayıcılarda hiçbir şekilde cache mekanizması yoktu. ya özel javascript kütüphaneleri ile kendi cache mekanizmaları yazılıyordu, yada web tarayıcıları hiçbir standarta bağlı olmadan kendilerince cache mekanizması uyguluyorlardı. bu sebeple bazı yazılımcılar web geliştirmesi yaparken bilinçsizce cache temizliği yaparlar.

- drag and drop

- history api: artık url'lerde hash # tag'i kullanımı yerine direk oralarak html 5in getirdiği history kullanılmaktadır. HTML 5 ile artık URL değişmeden sayfanın yenilenmesi de sağlanabiliyor.

  html5 öncesi sayfa iki şekilde değişebiliyordu: 1-hastag vs 2-url ile gidilen yeni sayfa.

  html5 ile gelen history mekanizmasında hashtag ihtiyacı kalkmıştır.

  ```js
  // state objesi 640 bin karakterlik limiti var. çok büyük data'lar geçilmemelidir.
  let stateObj = {
    foo: "bar",
  }

  window.history.pushState(stateObj, "page 2", "bar.html");
  ```
  
  Yeni sayfa aynı url olmak zorunda değil. Aynı url olmadığında da sayfanın state'i yenilendiği için hastag'lere gerek kalmamıştır. parametreler:
  
  - stateobj: yenilenen sayfadan event listener ile bu parametre okunabilmektedir.
  - "page 2": title. bu deger ignore ediliyor. boş gönderilmesi öneriliyor.
  - "bar.html": relative path olmalıdır. çünkü ancak; aynı domainde history olabilir. eğer boş yollanırsa, URL hiç dğeişmez fakat sayfa değişmiş olarak algılanır.

  pushState fonksiyonu çağrılınca server tarafa HTTP GET isteği yollanmıyor. Hastag'lerde de böyleydi. Sadece snal bir history yaratılıyor. Eğer sunucuya istek atmak istiyorsak; şöyle yapabiliriz:

  ```js
  window.onpopstate = function(event) {    
      if(event && event.state) {
          location.reload(); 
      }
  }
  ```

- web mesaging: iframe içerisinde event listenlerlarla (message event'i ile) data dönderimi ve alımı yapılıyor.

- Web Worker: js thread mekanizması. aksi durumlarda tarayıcı son kullanıcıya "not repsoding" mesajı verebiliyor.

- websocket (başka başlıkta anlatılıyor)

- webrtc: tarayıcı ile tarayıcı arasında direk iletişim protokolü.

- geolocation: lokasyon tespiti için API.

  Her istek için şu bilgileri döndürüyor:

  - coords.latitude - enlem. decimal number 
  - coords.longitude - boylam. decimal number 
  - coords.accuracy - sadece enlem ve boylam için doğruluk oranı.
  - coords.altitude - rakım. (deniz seviyesinden yükseklik).
  - coords.altitudeAccuracy - rakım için doğruluk oranı.
  - coords.heading - rota (eğer cihaz hareket halinde ise). as degrees clockwise from North.
  - coords.speed - The speed in meters per second 
  - timestamp - The date/time of the response

- web sql database: sorgu yapmayı sağlayan database. bu artık deprecated oldu.

- indexedDB: nosql gibi düşünülebilir. LocalStorage küçük data'lar, indexedDB büyük data'lar için tercih edilmelidir (zorunluluk diil).

- web storage (local storage + session storage): bazı kaynaklarda "__DOM storage__" olarakta geçer. anahtar - value mantığı ile çalışır.

# cookie vs web storage
- Web storage API'si çok daha temzidir. cookie'lerde metadatalar eklenince string merge işlemine girmek durumundasınız.
- web storage'ın boyutu cookie'lere göre çok daha fazladır.
- cookie'lerin oto-destroy özelliği vardır (time-to-live). web storage'de böyle bir özellik yoktur.
- cookieler header'a otomatik eklenebilir. web storage'da böyle bir feature yoktur. Asıl olan bu maddedir. Bu maddeye göre hangi storage'yi kullanacağımıza karar vermeliyiz (çok nadir durumlarda bunun istisnası olabilir tabi).

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# websocket

socket'lere bağlanamazlar. Karşı tarafında websocket kullanması şart. tcp üzerine kurulu http alternatifidir.

browser to browser haberleşme mümkün diil, çünkü browserda server-web-socket açılamaz. 

server taraf istediği port'ta ve path'te web socket'i sunucu modunda açabilir.

Firefox developer tool içinde websocket'leri takip edebilmek için bir özellik mevcut değil. Chrome'da bu mevcut (yıl 2018). CHrome'da network sekmesinde ilgili soket işleminin içinde "Frame" sekmesinden görülmektedir.

protocol: http alternatifi olduğu için http yerine 'ws' kullanılıyor. wss ise secure (ssl) kullanan versiyonudur.

websocket tam iki taraflı iletişimi sağlar. bir request'e karşılık response olmak zorunda değildir. iki tarafta istediği kadar ve istediği zaman mesaj atabilir. bu tarz iletişimlere duplex (or tr:dubleks, türkçe kelime anlamı: çift(dual) ) iletişim protokolü denir. 

websocket bağlantısı kurulduğunda client sunucya önce bir http isteği gönderir (80 portu diil. direk websocket'in bağlanacağı port'a yollar bu isteği):

örnek:

```
GET ws://websocket.example.com/ HTTP/1.1

Origin: http://example.com

Connection: Upgrade

Host: websocket.example.com

Upgrade: websocket
```

Burada websocket'e geçiş yapmalarını söyler. sunucda bunu kabul eder:

```
HTTP/1.1 101 WebSocket Protocol Handshake

Date: Wed, 16 Oct 2013 10:07:34 GMT

Connection: Upgrade

Upgrade: WebSocket
```

Bu istekten sonra artık aynı tcp bağlantı üzerinden sürekli stream'in yapılır.


# Message vs fragment

fragment türkçe kelime anlamı: parça

API'lerin sunduğu onMessage eventlerimiz her message geldiğinde tetiklenir. her message arkaplanda en az bir adet frame denilen parçalardan oluşur. frame'ler şu akışta daha basit anlaşılabilir:

```
Client: FIN=1, opcode=0x1, msg="hi"

Server: bir mesaj geldi: Hi

Client: FIN=0, opcode=0x1, msg="ben"

Server: mesaj dinlenmeye devam ediyor...

Client: FIN=0, opcode=0x0, msg="ahmet"

Server: mesaj dinlenmeye devam ediyor...

Client: FIN=1, opcode=0x0, msg="doganoglu'yum."

Server: bir mesaj geldi: ben ahmet doganoglu'yum.
```

- FIN=1 ve FUN=0 mesajın devam edip etmeyeceği bilgisini yolluyor.

- opcode=0x1 text mesajı atıldığını, opcode=0x2 binary mesaj atıldığını, opcode=0x0'ın ise bir anlamı yok. opcode=0x0 zaten önceden belirlenmiş mesaj tipinin devamında gelen frame'ler tarafından kullanılıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# web 1.0 vs web 2.0 vs web 3.0
web dünyasını belirleyen standartlardır. web 1.0 sadece html'in olduğu fakat ajax işleminin dahi gerçekleşmediği web standartlarını temsil eder. 2.0 ise 2003'ten itibaren olan tüm standartların tümünü temsil eder. 3.0 ise ethereum gibi smart-contract'larla çalışan web sayfalarıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# canvas (or Tuval) vs svg (or Scalable Vector Graphics)
svg her çözünürlüğe uygundur.

# svg örneği:
```xml
<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" stroke="green" stroke-width="4" fill="yellow" />
</svg>
```

# canvas örneği:

```js
<canvas id="myCanvas" width="200" height="100" style="border:1px solid #000000;"></canvas>

var c = document.getElementById("myCanvas");

var ctx = c.getContext("2d");

ctx.fillStyle = "red";

ctx.fillRect(0,0,150,75);
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# SASS
Sass, CSS'i bir programlama diline benzer yapıyla geliştirmemizi sağlayan, sürekli ihtiyaç duyduğumuz ve CSS'te bulunmayan birçok özelliği kullanarak, daha pratik ve okunaklı kod yazmamıza olanak verir.

Sass ile CSS yazarken; değişkenler (variables), döngüler (for, each, while), karar yapıları (if, else), fonksiyonlar kullanılabilir.

SCSS ve SASS iki farklı syntax sunan formata sahiptir. bu kodlar bir tool aracılığı ile derlenerek css formatı oluşturulur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Mustache vs underscore vs lodash

bu iki javascript kütüphanesi de hazırlanan template dosyalarını verilen model ile html'e render etmeye yaramaktadır.

underscore ek olarak jquery gibi fonksiyonel fakat dom'dan bağımsız metodlar içerir. kolay döngüler kurar, array içerisinde koşulları kontrol etme metodları gibi.

lodash; underscore'a alternatif açık kaynaklı kütüphane. underscore'dan daha fazla özellik içeriyor. underscore daha core çok metodlar içeriyor.

ecmascript'in 6'ıncı versiynu ile artık underscore veya lodash ile yapılan %80 özellik default olarak sağlanabiliyor. underscore ve lodash'in kullanılmasının sebebi eski tarayıcılarda da aynı metodların desteklenmesi ve %20'luk ecmascirptte olmayan fonksiyonların kulanılmasıdır.

# jquery vs jquery mobile vs jquery ui
jquery, javascript için temel metodları içeren kütüphanedir.

jquery ui ise date-picker, drag-drop gibi görsel bölgelerde düzenlemeler sağlayan kütüphanedir.

jquery mobile ise, mobile platformlarına uygun davranışlar sergilemesi için gerekli metodları içerir. örneğin mobile'de farklı eventt'ler varken, desktopta farklıdır. jquery html elementlerine verilen attribute'ler ile sayfada nasıl duracağına vs karar verebilir. bu durumlar için mobile'e daha uygun bir kütüphane gerekir. bu sebeple jquery-mobile kullanılmalıdır.

jquery eklenti altyapısına sahiptir.

# knockout js
javascript mvc kütüphanesidir.

# önyüz için MVC karşılaştırması
Burada birçok önyüz framework'leri için basit TODO uygulaması mevcut: (source-id: 211)

# backbone js
javascript mvc kütüphanesidir.. fakat angular ve knockout'a göre core bir framework'tür. herşeyi kendi başınıza tasarlamanız gerekir.

Backbone contoller isminde bir sınıf içermez. bu sebeple bazı yerlerde MV bazlı bir kütüphane olduğu yazar. fakat backbone MVC'dir. çünkü backbone-View objesi aslında, mvc'deki contoller'ın görevini karşılamaktadır. MVC'deki, View'ı ise; backbone-template'ler denk gelmektedir. Template'ler backbone-View içerisinde oluşturululduğundan yanlış algılamaya sebep olabilmektedir.

View'daki event'ler takip edilir, her event sonrasi metodlar çalıştırılır model'ler update edilir. modeller update edilince view'lar update edilir. Burada ek olarak modeller update olduğunda, otomatik olarak web servislerine istek gider. bu şekilde sunucudaki model ile sync olmamızı sağlar. Buradaki (source-id: 212) "Models and Views" başlığındaki ilk şekil bu durumu iyi açıklamaktadır.

Buradaki örnek çok temel ve basit: (source-id: 213)

Çok basit bir örnek:

```html
<!DOCTYPE html>
<html>

    <head>
        <meta charset="utf-8" />
        <title>Your first Backbone.js App | Tutorialzine </title>

        <!-- Google web fonts -->
        <link href="http://fonts.googleapis.com/css?family=PT+Sans:400,700" rel='stylesheet' />

        <!-- The main CSS file -->
        <link href="assets/css/style.css" rel="stylesheet" />

    </head>

    <body>

        <form id="main" method="post" action="submit.php">
            <h1>My Services</h1>

            <ul id="services">
                <!-- The services will be inserted here -->
            </ul>

            <p id="total">total: <span>$0</span></p>

            <input type="submit" id="order" value="Order" />

        </form>

        <!-- JavaScript Includes -->
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
        <script src="//cdnjs.cloudflare.com/ajax/libs/underscore.js/1.4.4/underscore-min.js"></script>
        <script src="//cdnjs.cloudflare.com/ajax/libs/backbone.js/1.0.0/backbone-min.js"></script>

        <script src="assets/js/script.js"></script>

    </body>
</html>
```

Yukarıdaki sayfa ile birlikte bu js dosyasını çalıştırdığımıza sayfa içerisindeki html dolacaktır.

```js
$(function(){

    var Service = Backbone.Model.extend({

        defaults:{
            title: 'My service',
            price: 100,
            checked: false
        },

        toggle: function(){
            this.set('checked', !this.get('checked'));
        }
    });

    var ServiceList = Backbone.Collection.extend({

        model: Service,

        getChecked: function(){
            // where backbone'un özel bir metodudur. bunun gbi birçok metod sunar.
            return this.where({checked:true});
        }
    });

    var services = new ServiceList([
        new Service({ title: 'web development', price: 200}),
        new Service({ title: 'web design', price: 250}),
        new Service({ title: 'photography', price: 100}),
        new Service({ title: 'coffee drinking', price: 10})
    ]);

    var ServiceView = Backbone.View.extend({
        tagName: 'li',

        events:{
            'click': 'toggleService'
        },

        initialize: function(){
            this.listenTo(this.model, 'change', this.render);
        },

        render: function(){

            // Create the HTML

            this.$el.html('<input type="checkbox" value="1" name="' + this.model.get('title') + '" /> ' + this.model.get('title') + '<span>$' + this.model.get('price') + '</span>');
            this.$('input').prop('checked', this.model.get('checked'));

            return this;
        },

        toggleService: function(){
            this.model.toggle();
        }
    });

    // The main view of the application
    var App = Backbone.View.extend({

        // already  existing element on html
        el: $('#main'),

        initialize: function(){

            // Cache these selectors
            this.total = $('#total span');
            this.list = $('#services');

            this.listenTo(services, 'change', this.render);

            services.each(function(service){

                var view = new ServiceView({ model: service });
                this.list.append(view.render().el);

            }, this); // "this" is the context in the callback
        },

        render: function(){

            // Calculate the total order amount by agregating
            // the prices of only the checked elements

            var total = 0;

            _.each(services.getChecked(), function(elem){
                total += elem.get('price');
            });

            // Update the total price
            this.total.text('$'+total);

            return this;
        }
    });

    new App();

});
```

# bootstrap
bootstrap, UI objeleri yaratmaya yarayan bir kütüphanedir.

"boostrap ui" ise, angular modülüdür. birçok bootsrap nesnesi angular ile yazılmıştır. bu şekilde angular ile daha uyumlu çalışılabilir. bootstrap jquery'ye depend ederi. oysa bootstrap modülü etmez. bu sebeple projeye jquery include etme zorunluluğu ortadan kalkar.

# bootstrap css vs bootstrap js
Bootstrap gösrselleştirme kütüphanesi. Fakat js dosyası bazı ek özellikler (genelde animasyon işlemleri) sunmak için isteğe bağlı kullanılabilir. bootstrap js, jquery'ye depend eder.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# jquery version history

| version | release date       | latest version and its release date | note                                                                          |
|---------|--------------------|-------------------------------------|-------------------------------------------------------------------------------|
| 1.0     | August 26, 2006    |                                     | First stable release                                                          |
| 1.1     | January 14, 2007   |                                     |                                                                               |
| 1.2     | September 10, 2007 | 1.2.6                               |                                                                               |
| 1.3     | January 14, 2009   | 1.3.2                               |                                                                               |
| 1.4     | January 14, 2010   | 1.4.4                               |                                                                               |
| 1.5     | January 31, 2011   | 1.5.2                               |                                                                               |
| 1.6     | May 3, 2011        | 1.6.4                               |                                                                               |
| 1.7     | November 3, 2011   | 1.7.2 (March 21, 2012)              | New Event APIs: .on() and .off(), while the old APIs are still supported.     |
| 1.8     | August 9, 2012     | 1.8.3 (November 13, 2012)           |                                                                               |
| 1.9     | January 15, 2013   | 1.9.1 (February 4, 2013)            |                                                                               |
| 1.10    | May 24, 2013       | 1.10.2 (July 3, 2013)               |                                                                               |
| 1.11    | January 24, 2014   | 1.11.3 (April 28, 2015)             |                                                                               |
| 1.12    | January 8, 2016    | 1.12.4 (May 20, 2016)               |                                                                               |
| 2.0     | April 18, 2013     | 2.0.3 (July 3, 2013)                | Dropped IE 6–8 support for performance improvements and reduction in filesize |
| 2.1     | January 24, 2014   | 2.1.4 (April 28, 2015)              |                                                                               |
| 2.2     | January 8, 2016    | 2.2.4 (May 20, 2016)                |                                                                               |
| 3.0     | June 9, 2016       | 3.0.0 (June 9, 2016)                |                                                                               |
| 3.1     | July 7, 2016       | 3.1.1 (September 23, 2016)          |                                                                               |
| 3.2     | March 16, 2017     | 3.2.1 (March 20, 2017)              |                                                                               |
| 3.3     | January 19, 2018   | 3.3.1 (January 20, 2018)            |                                                                               |
| 3.4     | April 10, 2019     | 3.4.1 (May 1, 2019)                 |                                                                               |

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# angular js
DOM manipülasyonları jquery gibi kütüphanelerle yapılıyor. Fakat MVC kavramını client tarafta uygulamak için angular gibi kütüphaneler kullanılmaktadır. angular mvc yapısı ile çalışır.

- #### sürüm

angularjs, 2inci sürümü ile sıfırdan yazıldı ve yeni bir siteye taşındı (angular.io). angular geriye uyumlu yazılmadı.

3üncü sürüm, isim çakışması sebebi ile atlandı. 2'den sonra direk 4 üncü sürüme çıkıldı.

| sürüm no | çıktığı yıl |
|----------|-------------|
| 2        | 2016        |
| 4        | 2017        |
| 5        | 2017        |
| 6        | 2018        |
| 7        | 2018        |
| 8        | 2019        |

Asagidaki tüm bilgiler angular 1.6 baz alınarak yazılmıştır.

- #### jquery

  - angular js, jquery'ye ye depend etmez. kendi içinde jQuery Lite'ı (jqLite) bulundurur. eğer jQuery var ise, angular jqLite yerine jQuery kullanır. jqLite sadece angular ihtiyacı metodları ve en temel jquery metodlarını sunar.

  - fonksiyonlara geçilen "element" objeleri her zaman jquery objesine wrap edilmiş olarak geçilir. örneğin;


  ```js
  angular.module('myModule', [])

    .directive('failswithoutjquery', function() {

      return {

        restrict : 'A',

        link : function(scope, element, attrs) {

                 element.hide(4000);
               }
      }
  });
  ```

  Yukarıdaki örnekte element objesi jquery objesi. hide elementi ise jquery lite'ta yok. bu sebeple eğer jquery inject edilmemişse bu kod bloğu hata verecektir.

  angular.element DOM objesinin element (jquery ile wrap edilmiş) olarak dönmektedir.

- #### modülerlik

  angular js eklenti desteği mevcut değil. çünkü her şey bir angular modülü olarak tanımlanabiliyor ve başka modüller tarafından çağrılabiliyor. örneğin routing ayrı bir modüldür ve ayrı inject edilir.

  yazılım geliştirici yeni modüller ekler. bir sayfada birden fazla modül olabilir. her modülün altında birden fazla component, directive ve controller olabilir.

- #### Component

kullanımı:

```xml
<w3-test-directive></w3-test-directive>
```

yada

```xml
<div w3-test-directive></div>
```

yada

```xml
<div class="w3-test-directive"></div>
```

yada

```xml
<!-- directive: w3-test-directive -->
```

tanımlanması:

```js
var app = angular.module("myApp", []);

app.directive("w3TestDirective", function() {

    return {

        template : "<h1>Made by a directive!</h1>"

 };
});
```

- #### watch variables

two-way binding olduğundan; herhangi bir dinamic değer değiştirdiğinde onu referans eden tüm değerlerde anında değişmektedir. fakat javascript'te bir değer console'danda değiştirilebilir. bunu angular nasıl anlıyor?

angular bunları  anlayamıyor. bu sebeple click metodu yerine ng-click gibi alternatifler mevcut. çünkü her angular stanardındaki metodların çağrılması sonrası tüm değerler manuel kontrol ediliyor. yani console'dan, daya on-click eventi üzerinden bir değer değiştirildiğinde angular bunu göremiyor.

bu sebeple şöyle bir sorun da ortaya çıkıyor:

contoller içinde async bir thread üzerinden (timeout, ajax call, cordova pugin'in return callback'leri gibi) bir dinamic değer değiştirildiğinde, contoller'ın main thred'inden sonra çalışırsa controller'ın haberi olmuyor. bu sebeple $scope.apply() metodu geliştirilmiştir. bu metodu çağrıldığında tüm dinamic değerler angular tarafından tekrar kontrol edilmektedir. örneğin; ajax-callback thred'in sonunda apply() methodu çağrılabilir.

angular $http modülü ajax işlemlerini yapmak için geliştirilmiştir. bu metdun callbakclerinde otomatik olarak apply metodu çağrılır. bu sebeple yaızlımcının bu metodu çağırmasına gerek yoktur. fakat jquery.ajax yada javascript core ajax işlemi yapıyorsa apply metodu şarttır.

apply() metodu isteğe bağlı bir metod parametresi de alabilir. bu metod parametresi içindeki fonksiyon çalışmasını bitirdiğinde apply işlemini gerçekleştirir.

- #### watch metodu

```js
$scope.myVar= "estVar";

$scope.$watch('myVar', function() { 

      alert('hey, myVar has changed!');

});
```

$watch metodunda apply() işlemi sırasında değişen variable'ler için event yaratabilmemizi sağlıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# HTTP Basic Authentication
http ile istek yaparken auth mekanizmasının en kolay ve standartlaşmış şeklidir. sadece requestin headırınına base64 tipinde username ve password bilgisi girilir. yapılan http isteğine eger bilgiler dogru ise cevap dönülür. standrat bir güvenlik şekli olduğundan, bazı web tarayıcıları bunu destekler ve popupta şifre ve kulanıcı adı sorar.

Basic auth işlemi her HTTP requestte yapılır. yani headera sadece ekleme yapılır. web tarayıcıları localde bir site için cookie olarak saklar request ile giden değeri. bu sebeple her defasında sormaz username ve passwordü. aynı şekilde örneği javada client objesi ile birçok istek yapabiliyoruz. aynı obje ile bir kere istek authantike olunduktan sonra cookieleri client objesi tutuyor ise bir daha request gerekmeyebilir.

# HTTP Digest authentication
Diggest auth'ta, önce, client sunucuya güvenlik sorgusundan geçeceğini belirten bir istek yapar. Bu isteğe cevap olarak sunucu, tek kullanımlık bir anahtar değer döndürür. Client tarafı hem bu değeri hemde MD5 algortimasını kullanarak şifreleyip sunucuya gönderir (ek olarak; client tarafı da bir tek kullanımlık anahtar kullarnı + URL adresi de şifrelemede kullanır …). Sunucu kullanıcı adı ve şifre ile aynı algoritmayı kendi uygular ve sonucun aynı olup olmadığına bakarak onay verir.

MD5 geri çevrilemez bir algoritma olduğu için güvenlik olarak basit auth'tan daha başarılır.

standart bir güvenlik şekli olduğundan, bazı web tarayıcıları bunu destekler ve popupta şifre ve kullanıcı adı sorar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# WebGL
Tarayıcılarda plugin gerektirmeden 3d ve 2d oyunlar, nesneler yaratılmasını sağlayan javascript API'sidir. OpenGL ES altyapısını kullanmaktadır.

# OpenGL
AÇık kaynaklı DirectX alternatifidir.

# OpenGL ES (or OpenGL for Embedded Systems)
OpenGL'nin cep telefonu gibi gömülü sistemler için tasarlanmış versiyonudur.

# NativeClient (or NaCl)
AÇık kaynaklı geliştirilen API. Bu API ile eklentiye gereksinim olmadan WebGL gibi 3d ve 2d modeller hazırlanabiliyor. Tek farkı herhangi bir proramlama dili ile yazılıp derlenmiş olan dosyanın tarayıcı tarayından (derlenmeye gerek kalmadan) direk olrsaka execute edilebilmesidir.Performans ve basitlik (javascript ile yazmak yerine diğer dillerle de yazabilme) açısından WebGL'den çok daha başarılıdır. NaCl, PPAPI destekli bir eklentidir.

# Plugin Application Programming Interface (or PAPI)
Tarayıcıların native işletim sisteminden yararlanması için tarayıcı tarafındaki API.

# Netscape Plugin Application Programming Interface (or NPAPI)
Birçok tarayıcı desteklemektedir, ilk Netscape çıkardığı için ismi böyle kalmıştır. Artık NPAPI özelliği çoğu tarayıcıdan kaldırılmaktadır.

# Pepper Plugin API (PPAPI)
Google'ın geliştirdiği, NPAPI'nin türevidir. Daha çok portabilite ve  işletim sistemi processinde çalışmaya yönelik geliştirmeler içermektedir.

chromium based browser's built-in PDF viewer is a plug-in which based on PPAPI.

# ActiveX
Microsoftun Internet explorer tarayıcısı için geliştirdiği PAPI. Microsoft Edge (windows 10 ile gelen yeni tarayıcı), ActiveX'i desteklememektedir.

# Silverlight
Adobe Flash alternatifi açık kaynaklı Microsoft'un geliştirdiği yazılım. Lisans sebeple ile silverlight kullanmayanlar projeyi forklayarak Moonlight projesini oluşturmuştur. fakat bu 2 projeninde geliştirilmesi durdurulmuştur.

# WebExtensions
Firefox 57inci sürümü ile zorunlu kıldığı yeni eklenti API'sinin ismidir. BU API chromium tabanlı tüm tarayıcılarda (örnek: Opera) da kullanıldığı için cross-browser eklenti yazılmasını sağlamaktadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# rest (or Representational state transfer) vs restful
Representational kelime anlamı: temsili.

"Representational" kelimesi suncu tarafta manipüle ettiğimiz resource'ları (state'leri) temsili değerlerle (genelde bir çeşit ID ile) yönetmemizden gelir.

__rest__ yazılım haberleşme tekniği/mimarisidir. "__restful__" ise, REST'i kullanan sistemler (uygulamalar) için kullanılır.

REST, 200 yılında "Roy Thomas Fielding" tarafından bir doktora tezinde ortaya atılmıştır.

rest bir protokol değildir. rest bir protokol mimarisidir. temelde şu kuralların olmasına dayanır:

- client-server

  sistem, client'ın herhangi bir platformda çalışabilecek şekilde tasarlanmış olmalıdır.

- stateless server

  request'lerde sadece client taraf state(context) ve session bilgisi tutmalıdır. sunucuda tutulmaz.

- Uniform interface

  her resource için CRUD (Create, update, delete...) metodları hazır olmalıdır.

- cacheable

  client veya aradaki proxy'ler cacheleme yapabilmelidir. her isteğin cacheable olup olmadığı her daim net bir şekilde belirtilmelidir.

- layered system

  sunucularımız birçok katmandan meydana geliyor olabilir. load balancer, proxy, cache, ayrı microservisler... bunlar client tarafından bilinmemesi gereklidir. client tek bir endpoint'den tüm ihtiyaçlarını giderebilmelidir.

- Code-On-Demand (optional)

  server, client'a execute etmesi için kod yollayabilir. örnekler: Javascript kodu yada java-applet'leri yollayabilir.

Eğer request/response'larımız bu kurallara uymuyorsa, sistem __restless__'dır.

Rest yapısı HTTP ile ortaya atılmıştır ve HTTP ile çok uyumludur. bu sebeple piyasada Rest kelimesi denilince herkesin aklına sadece HTTP gelmektedir. oysa bu doğru değildir.

REST mimarisinde geçen terimler ve buna denk gelen karşılıkları:

| Data Element            | Modern Web Examples                                     |
|-------------------------|---------------------------------------------------------|
| resource                | the intended conceptual target of a hypertext reference |
| resource identifier     | URL, URN                                                |
| representation          | HTML document, JPEG image                               |
| representation metadata | media type, last-modified time                          |
| resource metadata       | source link, alternates, vary                           |
| control data            | if-modified-since, cache-control                        |

# REST vs SOAP (or Simple Object Access Protocol)

SOAP xml tabanlı bir istek atıyormuş gibi görünebilir, fakat aslında bir HTTP POST isteğidir. Gönderilen XML post isteğinin data bloğunda göderilir. SOAP bir protokoldür oysa REST protokollerde kullanılan bir tekniktir. Bu sebeple karşılaştırılması doru değildir. Fakat piyasada REST, sadece HTTP olarak algılandığı için bunun karşılaştırılması yapılıyor.

İstenirse JWT'nin tuttuğu bilgiler SOAP isteğinde tutulur ve SOAP mimarisi ile Restful bir sistem yapılır. Fakat piyasada kimse bunu tercih etmez çünkü best bractice olarak zaten Resful sisteme HTTP requstleri çok uygundur.

SOAP mesajı POST Http'dir. payload bloğunda xml vardır. bu xml'in root'undaki element "Envelope"'tur. içinde "header" ve "body" vardır.

# SOA (or Service-oriented architecture) vs web service
SOA kabaca bir mimarisel paradigmadır. Bu paradigma; birden fazla/farklı web servisini entegre ederek (veya gruplayarak) tek bir sistem gibi işlemesini sağlamaya dayanır.

web servis ise, web teknolojileri kullanarak, dışarıya API açarak, hizmet veren servislere verilen genel bir terimdir.

SOA paradigmasını birçok teknoloji ile gerçekleyebilir (implemente edebiliriz):
- web servisler
- CORBA
- REST
- gRPC
- EJB
- SOAP

# raw of http request
bir http isteği TCP katmanında incelendiğinde şu şekilde görünmektedir:

```
GET /wx/in/kanpur/wx.php HTTP/1.0
Host: cdn.sstatic.net
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: text/html
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

```

Görüldüğü gibi özel bir formatı yoktur. Her bilgi farklı satırda yollanır. En sonda bilginin bittiğine dair fazladan bir satır sonu da olmalıdır.

örneğin nc (netcat) komutu ile tcp üzerinden raw isteği yollayabilir:

> nc www.google.com 80

komut satırı input bekleyecektir. aşağıdakiler girildiğinde karşı tarafa bilgi yollanacaktır:

```
GET /index HTTP/1.0
Accept: text/html
```

İki kez enter tuşuna basılıp satır sonu eklendiğinde; response komut satırında ekrana basılacaktır:

```
HTTP/1.0 404 Not Found
Content-Type: text/html; charset=UTF-8
Referrer-Policy: no-referrer
Content-Length: 1566
Date: Sat, 23 Mar 2019 10:11:18 GMT

<!DOCTYPE html>
<html lang=en>
  <meta charset=utf-8>
  <meta name=viewport content="initial-scale=1, minimum-scale=1, width=device-width">
  <title>Error 404 (Not Found)!!1</title>
  <style>
```

Telnet komut satırı ile de aynı durum söz konusudur. örnek:

> telnet httpbin.org 80

```
POST /post HTTP/1.1
Host: httpbin.org
Connection: close
Content-type: application/json
Content-length: 11

{"test":true}

```

header'lar ile body arasında bir satır boş olmalı. o satır boşluk dahi içermemeli. eğer boşluk içerirse headermış gibi algılanır. Spring ile test edildiğinde, eğer log'ları debug'a çekersek her gelen istek detaylı şekilde basılır:

```
logging:
  level:
    root: DEBUG
```

Telnetten alınan response direk terminal output'a yansıyacaktır. Eğer tcp connection'ı kapanırsa telnet komutu sonlacaktır. fakat tcp sonlanmaz, terminal yeni input beklemeye devam eder.

(source-id: 214) burada belrtildiği gibi client "Connection: close" atarsa sunucunun response sonrası tcp'yi kapatması beklenir. Eğer client atmaz sunucu atarsa connection'ı client kapatır.

Chunked request'lerde (body'nin parça parça yollandığı isteklerde), her chunk size'ı body'den önce ve sonra yollanır. Dolayısı ile telnet output'undan her body öncesi ve sonrası anlamsız kısa text'ler görebiliriz. bu anlamsız tex'ler yollanacak body chunk'ının size'ıdır.

# Telnet vs raw TCP socket
- telnet RFC'si olan, TCP/IP model'inde en üst katmanında (Application level'da) olan bir protokoldür.

- telnet'in default server portu 23'tür.

- telnet'in detayları için birçok RFC var. Fakat asıl RFC 854'tür. kaynak: (source-id: 215) title: "Related RFCs".

- Telnet protokolü basittir. Bazı karakterlerin bazı anlamları vadır. sunucu veya client onları okursa ona göre tepki yapar (bir fonksiyon çalıştırır ve return olarak soketten karşıya döner).

- Telnet'te en ufak birim 8-bit'tir. kaynak: (source-id: 216) title: "INTRODUCTION".

- Telnet server olmayan bir TCP sunucuya (örnek http server) telnet client aracılığı ile (http request'ine denk gelen) bir byte-array atarsak, karşılığında hata almayız. Normal server soket response'umuzu (yani http response'u) alırız. Çünkü telnet client, istediğimiz her bilgiyi karşı tarafa direk yollar. Ekstra yaptığı bir şey yoktur. Karşı tarafta telnet server olmadığı için normal/saf TCP haberleşmesi gerçekleşmiş olur.

  Fakat burada bazı istisnalar var. örneğin;
  
  - eğer serverdan gelen bir karakteri (veya karakter setlerini) bir telnet komutu olarak algılarsa, o zaman telnet clienmt farklı bir tepki verebilir. çünkü ilgili komutun gereksinimini yerine getirmelidir.

  - telnet LF satır sonlarını CR+LF convert eder.

  - Ctrl+] karakterlerini escape karakteri olarak algılar

  - gibi farklı durumlarda çıkabilir...

  Aynı durum telnet-server içinde geçerli. telnet server açarsak client telnet diilse sorun yaşayabiliriz. bu sorunlar yukarıdaki maddelerle aynı sebeplerden kaynaklanacaktır.

  Telnet connection initialize olunca bazı bilgileri karşıya atar. örneğin "terminal GUI size" gibi.. Aslında bu bilgi bile bizim HTTP server'la raw sokcetten haberleşememizi sağlayacaktır, çünkü http server bize excepiton atacaktır. Fakat pratikte http server'a telnet client ile istek atabiliyoruz. Bunun sebebi şu: telnet komut satrırı uygulamaları initialize olunca karşı tarafa environment bilgilerini atmıyor (her komut satırı farklı davranabiliyor). kaynak: (source-id: 217) asnwer of Mew, at Jan 26 2011, 14:02.

  Netcat (nc) komutu ise direk tcp soket seviyesinde işlem yapar ve hiçbir data'da oynama yapmaz veya anlamlandırmaya çalışmaz. görevi farklıdır. bu sebeple telnet olmayan sunculara telnet komutu ile bağlanmamalıyız. insanlar alışığı için böyle yapıyor fakat bu yanlış.

# Richardson Maturity Model

tam anlamıyla restful bir servis yazıyorsak 3 no'lu level'dayızdır. rest mimarisini kötü kurguladıysak 0 nolu durumdayızdır.

- Level-0 - Swamp of POX

  swamp kelime anlamı: bataklık.

  POX ise; "Plain Old XML" in kısaltmasıdır.

  rest'i sadece data taşımak için kullanıyoruz. genelde SOAP, RPC benzeri altyapılar kullanıyoruz.

- Level-1 - Resources

  istek yaptığım endpoint'ler resource bazlı değişiyor ise bu leveldayızdır.

- Level-2 - HTTP Verbs

  resourcelerime erişirken post, get, delete gibi  istekleri aynı endpoint için kullanabiliyorsam bu leveldayızdır.

- Level-3 - HyperMedia Controls

  servisin dönüş değerleri; client'ın tekrardan yapacağı isteklerin URL'lerini içeriyor ise son level'dayızdır. buradaki amaç client tarafta daha az bilgi tutmaktır. örnek: doktor randevu boş saatleri servisten çekildi. dönüş değerinin içinde dolu saatlerin randevu almak için gerekli URL'si de olmalıdır.

  # Hypermedia As The Engine Of Application State (or HATEOAS)

  bu "Richardson Maturity Model" level-3 için kullanılan bir terimdir. client, dinamik olarak sayfanın state'ini (kısmen yada tamamını) network'ten gelen cevaplara/datalara göre oluşturmaktadır. bu da level-3 gibi bir sistemde en optimum yapılabilecektir.

  level-3 response örneği:

```json
{
    "name": "Alice",
    "links": [ 
          {
            "rel": "self",

            "href": "http://localhost:8080/customer/1"
          }, {
            "rel": "customer.search",

            "href": "http://localhost:8080/customer/search"
          } ]
}
```

- "rel" relation kelimesinin kısaltmasıdır.
- "self" dönen bu response için hangi kaynağın çağrılması (request) gerektiğini belirtir.
- bu tarz response veren sistemlere "hypermedia-driven system" da adlandırılır.
- farklı bir örnek:
  mesaj'ı döndüren bir servisimiz olsun. X id'li mesajı çektik bize şöyle bir cevap dönebilir:

```json
{
    "text": "how are you",
    "links": [ 
          {
            "rel": "self",

            "href": "http://localhost:8080/message/x"
          }, {
            "rel": "delete",

            "href": "http://localhost:8080/message/delete/x"
          } , {
            "rel": "favorites",

            "href": "http://localhost:8080/message/favorites/x"
            "methods": ["put", "delete"]
          } ]
}
```

HATEOS için birçok implementasyon mevcut. Bu implementasyonlar bu dosyadaki birçok standardı belileyebiliyor. örnek:
- links, href, rel yerine ne yazılması gerektiği
- links, href, rel değerlerinin ne ve hangi formatta olacağı
- links, href, rel gibi hangi değerlerin olacağı

Yukarıdaki örnekte mesajımızı silme butonunu, yada favorilere ekleyip ekleme seçeneklerini sunup sunmayacağımıza client tarafta dinamik olarak karar veririz.

# Spring org.springframework.http.ResponseEntity

HATEOS'u programatik olarak tanımlaybiliyoruz. örnek:

```java
import static org.springframework.web.servlet.mvc.method.annotation.MvcUriComponentsBuilder.fromMethodCall;
import static org.springframework.web.servlet.mvc.method.annotation.MvcUriComponentsBuilder.on;

@PostMapping(value = "/createUser")
public ResponseEntity<Void> createUser(int userId) {

    boolean result = repository.createUser(userId);
    if(result = success){
      
      URI location = fromMethodCall(on(UsersApiController.class).getUser(userId)).build().toUri();
      return ResponseEntity.created(location).build();
    
    } else {
       throw exception(); // or another logic
    }
}

```

Yukarıda createUser'ı 3 id'si ile çağrırsak (yani yeni user yarat ve id'si 3 olsun istersek) cevaba olarak spring otomatik olarak bu header'ı ekler:

- Header Name: "Location"
- Header Value: "http://localhost:8080/users/3"

localhost yerine o anda çalışan spring sunucusunun ip'si dönecektir.

spring yukarıdaki örnekte getUser() metodunu run etmez. sadece onun path'ini alır.
