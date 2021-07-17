############################

############################
# WEB HTTP HEADERS
############################

############################

# http headers

> Age

proxy üzerinde kaç defa cache'den bu değerin kullanıldığıdır. otomaik proxy tarafından her defasından 1 arttırılır.

> Connection

keep-alive, close gidi değerler alır. Bir sonraki isteğin bu istekte kullaılan tc soket üzerindn gitmesini sağlar. bir sonraki istekler gönderileceği kesin ise; performans artışı sağlar. bu header'dan da anlaşıladığı gibi ssl bağlantıları her istekte eğer keep-alive gidiyorsa yeni soket üzerinden yapılmaz.

> Authorization

Standart auth işlemleri için kullanılan header

> Proxy-Authorization

Authorization ile aynı görevde fakat proxy'nin önemsediği değerdir.

> Accept

requestin kabul edeceği mimetype

> Accept-Charset, Accept-Encoding, Accept-Language

requestin kabul edeceği tipler

> Content-MD5

sadece body kısmının md5'i.

> Content-Type

sadece body kısmımının mimetype'si.

> TE

Transfer encoding'dir. Body kısmındaki verinin nasıl tutulduğunu belirtir. örneğin compress yapılmış ise; gzip gibi.

> Date

requestin oluşturulduğu tarih

> Max-Forwards

bu isteğin en fazla kaç tane proxy (aracı) üzerinden gidebileceğini liitler.

> DNT

do not track. 1 veya 0 değerini alır.

> Origin

CORS çin gereklidir. O anda URL barda bulunan domain adresidir. Bunu ajaxı yapan javascript değil, tarayıcının kendisi doldurmaktadır.

> Range

Büyük body kısmı olduğunda sürekli olarak arkaplanda tekrar işlem gönderiliyor. Böyle durumlarda bu header'a bod'nin hangi byte'larının (byte aralığı) gönderldiği belirtilmektedir.

> Forwarded

X-Forwarded-For yerine kullanılan standartlaşmış bir header'dır.

client proxy'ye istek yaptığında bu değer boştur. daha sonra ilk proxy 2'inci proxy'ye istek atarken bunu doldurur. 1. proxy 2.inci proxy'ye istek yaparken bu header bu şekildedir:

Forwarded: for=CLIENT_IP

Daha sonra 2. proxy gerçek sunucuya isteği yönlendirdiğinde bu header şöyledir:

Forwarded: for=CLIENT_IP, for=PROXY1_IP; by=PROXY3_IP; proto=http; host=example.com

> Via

forwarded ile aynı bilgileri içerir aynı zamanda kullanıla protokollerin sürümlerini de içerir.

> Host

istek yapılan url'nin adresi ve portu. path buna dahil değildir.

> Referer

Kelime olarak yanlış yazılmıştır fakat artık herkes bu şekilde kullanmaktadır.

Bir başka isteye yönlendirmelerde referer kısmı doldurulur. kullanıcının hangi siteden yönlendiğini anlamak için kullanılır.

> X-Forwarded-For

standart olmayan bir header'dır. Forwarded'dan önce vardı. fakat standart olarak referer sonradan belirlendi.  Fakat hala x-forwared-for'u kullanan yazılım/donanımlar var.

X-Forwarded-For IP bilgilerini tutar. bir proxy bir isteği başka yere yönlendirdiği zaman bu bilgide orjinal isteği yapan sunucunun ip'sini barındırır. örnek:

X-Forwarded-For: client, proxy1, proxy2

> X-Forwarded-Host

X-Forwarded-For ile aynı bilgiler içerir. sadece IP yerine domain bilgisi tutar.

> X-Forwarded-Proto

X-Forwarded-For varken protokollerin yazlması için ayrı bir header belirlenmişti. her aracı bir sonraki aracıya isteği yaparken hangi protokol kullandıysa (örnek https) onu buraya yazar.

> X-Forwarded-IP

standart değildir. mail sunucularına istek yaparken kullanılan bir değerdir.

> Access-Control-Request-Method

CORS için gerekli. "Preflight" isteklerinde kullanılır. Preflight onayı alınırsa gönderilecek asıl isteğin metodudur (örnek : "put").

sunucu asıl request'e izin verip vermeyeceğine karar verebilmek için preflight'ta bu tarz detayları ister.

> Access-Control-Request-Headers

CORS için gerekli. "Preflight" isteklerinde kullanılır. Preflight onayı alınırsa gönderilecek asıl isteğin header'ını barındırır.

sunucu asıl request'e izin verip vermeyeceğine karar verebilmek için preflight'ta bu tarz detayları ister.

> Access-Control-Expose-Headers

CORS isteklerinde sunucu bu header'ı client'a döndürür. web tarayıcı JS tarafında sadece:

- burada belirtilecek olan header'ların
- default olarak web standartlarında belirtilmiş header'ların

okunmasına izin verecektir.

> Access-Control-Allow-Origin

Response'ta bulunur. Preflight ‘a cevapta bulunur. Server'ın izin verdiği tüm domain'leri içerir. bu domainler url bar'daki domainler oluyor.

> Access-Control-Allow-Methods, Access-Control-Allow-Headers

Response'ta bulunur. Preflight'a cevapta bulunur. Server'ın izin verdiği bilgilerdir.

> Access-Control-Allow-Credentials

Response'ta bulunur. Preflight ‘a cevapta bulunur. Server'ın izin verdiği güvenlik bilgilerini içerir. örneğin; asıl atılacak istekte cookie olup olmayağını belirtir.

> Access-Control-Max-Age

Preflight responsunda bulunur. Bu o isteğin ne kadar süre gereli olduğunu belirtir.

> X-Requested-With: 

Bu header her zaman XMLHttpRequest değerini alır. Bunun yollanma sebebi isteğin CORS olup olmadığını ayırt edebilmektir. Çünkü CORS standatlarında yollanan isteklerde sadece bazı header'lar yer alabiliyordu. Bu header listede olmadığından CORS standartları çerçevesinde atılmadığını anlamak için kullanılır.

> User-agent

tarayıcı yada isteği yapan client'ın bilgisi

> Upgrade

istek yapılan yere http sürümünü güncelemesi isteğidir.

> Status

HTTP status code

- 1xx Informational responses: payload gönderilmeye devam ediliği zaman, protokol sürümü değiştirileceği zaman...
- 2xx Success
- 3xx Redirection
- 4xx Client errors: url too long, bad request, method not found, auth failed...
- 5xx Server error: internal problems on server…

Status code'lar spring'de bu şekilde döndürülüyor:

```java
import org.springframework.http.ResponseEntity;

@RequestMapping(value = "/controller", method = RequestMethod.GET)
@ResponseBody
public ResponseEntity sendViaResponseEntity() {
    return new ResponseEntity(HttpStatus.NOT_ACCEPTABLE); // ilgili hata code'unu HTTP responsu'nun status'unda dönüyor
}
```

Diğer durumlarda spring yine gerçek hataları atıyor. örneğin filterlarda olmadık bir exception olursa, internal server error hata kodu dönüyor. standart http kodları dönüyor.

ResponseEntity objesi body'yi wrap etmez yada response output'unu değiştirmez. ResponseEntity response'u daha detaylı değiştirebilmemize yarar. ResponseEntity'siz sadece body'yi değiştirebiliriz. fakat ResponseEntity ile header'ları, status code'ları da değiştirebilir.

Yukarıdaki header'lara ek olarak cache için kullanılan header'lar da vardır. bu header'lar başka başlıkta anlatılıyor.

Hata kodlarının listesi: (aşağıda birçok farklı kaynaktan buraya kopyalandı. Bazıları daha detaylı bilgi içeriyor çünkü.)

- [web_http_status_codes_iana.md](https://github.com/yusufd89/notes/blob/master/web_http_status_codes_iana.md)
- [web_http_status_codes_microsoft.md](https://github.com/yusufd89/notes/blob/master/web_http_status_codes_microsoft.md)

# header isimlendirmesi

Eskiden x- ile başlayanlar standart olmayan header için kullanılıyordu. fakat bazı header'lar sık kullanılmaya başlandığından, artık standart hale geldiler. bu sebeple artık custom header'lara farklı bir prefix yazılması önerilir.

# relative quality factor
q parametresi "accept" keyword'ünü içeren header'ların (Accept-Charset, Accept-Encoding...) value kısmında kullanılmaktadır. bu değer 0 ile 1 arasında bir sayı değeri almaktadır. örnek:

```
Accept: text/plain; q=0.5, text/html, text/x-dvi; q=0.8, text/x-c
```

Yukarıdaki header şu analam geliyor: __html__ ve __x-c__ en öncelikli (q=1 default), eğer bu tipleri sunucu desteklemiyorsa, __dvi__ olarak cevap version. eğer onu da desteklemiyorsa, __plain__ cevap version.

# header'lar cookieleri barındırır

header'lar arasında cookie diye bir değer bulunur. bu degerde cookieler taşınır. formatı şu şekildedir:


- client sunucuya atarken Header içerisinde şu satırlar yer alır:

Cookie: name=value; name2=value2
Cookie: name3=value3

Yukarıda expire secure gibi nitelikler isteğe bağlıdır.

- Suncudan client'a repsonse içerisinde dönen heraderlar

Yukarıdaki ile aynı formattadır. tek farkı "Cookie:" yerine "Set-Cookie:" yazmasıdır. Aynı zamanda expire, secure gibi özellikler burada isteğe bağlı belirtilmelidir.

Set-Cookie: name=value; name2=value2; Expires=12.04.2018; Secure
Set-Cookie: name3=value3

her tarayıcı isteğin yapıldığı domaine bağlı tüm cookie'leri sunucuya otomatik gönderir. her defasında yollanması istenmeyen cookie'ler, cookie olarak değilde, farklı storage'lere atılmalıdır.
