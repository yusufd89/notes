############################

############################
# SECURITY OAUTH
############################

############################

# Single sign-on (or SSO)
Artık kullanıcılar birçok farklı sisteme ayrı ayrı giriş yapmakta ve ayrı ayrı şifre tutmaktadırlar. BU şifreleri tek bir merkezi yerden yönetilebiliyor olması durumunda;

avantaj:
- son kullanıcı için daha rahat, tek şifre çünkü

dezavantaj:

- çalınması durumunda bir tehlike oluşturmaktadır çünkü tüm sistemler için şifre aynı. buradaki çalınma şifrenin diğer sistemlerin herhangi biri tarafından çalınmasıdır.ss

dezavantajı gidermek için SSO çözümü uygulnabilir. Yine şifre yönetimi tek bir yerden olacaktır. Fakat kullanıcıya token gönderilecektir. Şifre giriş ekranı domain adresi; ortak şifre yönetim sisteminin olmalıdır. SOn kullanıcı bu şekilde şifresini diğer sistemlere girmemiş oluyor. Dİğer sistemler hack'lendiği zaman, kullanıcının sadece token'ını kullabilecektir.

# authentication (or kimlik doğrulama)
sadece kullanıcıyı doğrulama mekanizmasıdır.

# authorization (or yetkilendirme)
Sadece ilgili kullanıcının nelere yetkili olup olmadığı yönetimidir. Yetki kontrolü yapan sistemde, kimlik doğrulama olmak zorunda değildir. Bunun en bilinen örneği Oauth'dır.

# authentication vs authorization
authentication authN, authorization authZ olarak kısaltılır.

sadece login bilgilerini client'a paylaşan bir süreç "authentication", login bilglleri ile ilgilenmeyip resource'larsa erişim için token ile çalışan süreçlere "authorization" denir.

bazı protokoller hem authentication hem de authorization işlevini kapsar. örnek "openId connect".

# OpenId 1.0 ve 2.0

- Kimlik doğrulama protokolüdür.

- açık kaynaklıdır.

- örneğin twitter gibi bir siteyi provider(kimlik doğrulayıcı) olarak kullanıp, başka yere login olmak isterseniz, login olacağınız sitenin, twitter'dan anahtar(onay) almış olması şart değildir.

- openid protokolünü destekleyen herhangi bir provider ile, openid login'i destekleyen herhangi bir siteye login olunabilir.

- herkes birer openid provider'ı olabilir. 

- openid provider ile login olunmaya çalışılan site arasındaki haberleşme protokolüdür.

süreç:

- kullanıcı, login olanacağı web siteye girer (muhtemelen "login with Twitter" gibi bir butona tıklar)

- web sitesi openID-provider'a (örnek: tiwtter'a) yönlendirme yapar

- kullanıcı twitter'a login olur (nasıl login olacağına openID hiç karışmaz)

- kullanıcı başarılı yada başarısız olursa login olmaya çalıştığı web sitesine yönlendiririlir.

- twitter, web sitesine yönlendirilirme yaparken (success url'ye yönlendirirken), web sitesine kullanıcı için kontakt bilgilerini de gönderir. burada bir çok farklı bilgi olabilir.

# Oauth 1.0, 1.1, 2.0

- Yetkilendirme protokolüdür. HTTP üzerinden çalışır.

- açık kaynaklıdır.

- örneğin twitter gibi bir siteyi provider olarak kullanıp, başka yere login olmak isterseniz, login olacağınız sitenin, tiwtter'dan anahtar(onay) almış olması şarttır.

- 2.0, geriye uyumlu değildir.

- openid'dekine benzer bir süreç vardır. fakat web sitesi twitter'dan login bilgilerini almaz. aldığı token ile birlikte sürekli olarak arkaplanda twitter'ın kaynaklarına user adına erişip işlem yapabilir. bu sebeple; oauth bir yetkilendirme protokolüdür.

# openid connect (or OIDC)
- openid 2.0'dan sonra çıkan sürümü. isim değişikliği sonrası 1.0 sürümünden devam edilmektedir. 

- Openid connect, oauth 2.0 üzerine kurulu bir yapıdır.

- "Openid connect" ile oauth 2.0'a kimlik doğrulama özelliği de getirmiştir.

# scope
scope'lar client uygulamasının role'leri olarak düşünülmelidir. login olan son kullanıcının google'daki role'ü google drive dosyalarına erişmek olabilir, fakat sadece "email" scope'una sahip bir uygulama sadece gmail'e erişebilir. yani "scope" uygulamanın role'üdür.

## predifined scopes

- "openid connect 1.0"'da scope'larda "openid" olmak zorundadır.

- "openid connect 1.0"'da scope'larda istenirse "offline_access" olabilir. "offline_access" scope'u varsa, son kullanıcı web tarayıcısını/uygulamasını kapatsa dahi, arkaplanda access token ile user-info bilgilerine erişebileceği anlamına gelir.

  Tam olarak hangi bilgilerin user-info olduğu standartlarda yazmamaktadır. fakat önceden ayrılmış field'lar vardır. kaynak: (source-id: 319) title: "5.1. Standard Claims".

# Facebook Connect
Facebook'un diğer sitelere login olabilmemizi sağlayan kendi protokolü.

# token
SSO'larda token sadece yetkilendirme için kullanılır. sadece kimlik doğrulama için token kullanımına gerek yoktur. yetkisine göre cevap dönülmesi gereken yerlerde token kullanılmaktadır.

rest sessionlarda kullanılan token'lar farklı amaçtadır. onlar her defasında sunucuya gönderilir, bu şekilde kullanıcı login mi değilmi diye anlaşılır.


# oauth 2.0

- ## roller

  - ### Resource owner
    kullanıcının kendisi. end-user.

  - ### Resource server
    API. user'ın kişisel bilgilerini barındırır. dışarıdan gelen isteklere cevap verip vermeyeceğini bilmelidir. işte bunu anlaması için oauth 2.0 protokolünden yararlanacaktır. bu sunucuya client istek yapacaktır.

  - ### Authorization server
    bu kısım istenirse API ile aynı uygulama içerisinde de olabilir.

  - ### Client
    third-party app

yukarıdaki rollere bazı örnekler:

- banka uygulamamız var. sunucu tarafta birçok microservisimiz var. bir mikro servisimiz sadece auth_server görevi görsün. diğer tüm micro servisler API olacaktır. mobil veya ATM ise birer client rolünde olacaktır.

- amazon.com'a login olucaz. amazona hızlı login olabilmek için facebook profilimizle login olduk. facebook hangi bilgileri vereceğini bize sorar. biz onayı verdiğimizde amazon bu bilgilere erişir. amazon burada client, facebook ise API ve auth server birliktedir. Yani; facebook'taki user bilgilerimiz resource olmaktadır.

- ## süreç

client taraf prod ortamına çıkmadan önce __auth_server__'dan (provider'dan) bir __client_id__ ve __client_secret__ alması şarttır.

aynı zamanda client taraf provider'a redirectURL'ler de vermesi gerekir. bu url'ler success ve error durumunda kullanıcının client tarafa yönlendirilmesi için şarttır. client'ın test ve prod ortamı için provider'dan iki anahtar almak uygun olacaktır.

request'lerin isimleri bu şekilde kullanılmaktadır:

```
+--------+                               +---------------+
|        |--(A)- Authorization Request ->|   Resource    |
|        |                               |     Owner     |
|        |<-(B)-- Authorization Grant ---|               |
|        |                               +---------------+
|        |
|        |                               +---------------+
|        |--(C)-- Authorization Grant -->| Authorization |
| Client |                               |     Server    |
|        |<-(D)----- Access Token -------|               |
|        |                               +---------------+
|        |
|        |                               +---------------+
|        |--(E)----- Access Token ------>|    Resource   |
|        |                               |     Server    |
|        |<-(F)--- Protected Resource ---|               |
+--------+                               +---------------+
```

Yukarıdaki şekildeki resource owner, Authorization server'da olabilir. Yukarıdaki şekil abstract olarak tanımlanmıştır. Aslında son kullanıcın (resource owner) onayı alınıyor. Yukarıdaki şekil soyut bir gösterimdir. 

- ## state

user oauth2 sunucusuna yönlendirildiğinde state parametresi isteğe bağlı atılır. bu parametreyi alan provider bu degeri redirect url ile tekrar client'e geri yollar.

- ## login flow çeşitleri (access token'ı elde etme yöntemleri)

Oauth 2'de 3 şekilde access token'ı client elde edebiliyor:

- ## 1 - Authorization Code

provider'dan onay alındığında kullanıcı client'a redirect ediliyor. client tarafa, bu success redirection sırasında __authorization_code__ da gönderiliyor. Fakat bu kod ile, client taraf, artık resource-API'ye istek yapamaz. çünkü redirect sırasında araya biri girmiş olabilir. burada 2 çözüm var:
- oauth 2.0 RFC'sinde (rfc6749) yazan: __authorization_code__ ile auth-server'a istek yaparız ve __access_token__'ı alırız. __access_token__ ile artık resource-API'ye istek atabiliriz. Burada sorun şu: auth-server'a __authorization_code__ yanında client-secret-key'i de yollarız. Fkat bu secret key'i özellikle native-mobile ve JS-client'larda saklamak imkansız. De-compile işlemi ile mobile uygulamalaraki string'leri çok kolay şekilde hacker'lar bulabiliyor.
- oauth 2.0 RFC'sinde (rfc6749) yazmayan ek uzantı çözüm: __Proof Key for Code Exchange (PKCE)__. (source-id: 320) Bu çözüm oauth 2.0 RFC'sinde yazan çözüm patlak verebileceğinden sunulmuş durumda.

  PKCE, oauth 2.0 RFC'sinde (rfc6749) yazan __authorization_code__ süreci ile aynı. Sadece istekler bazı ek parametreler içeriyor:

  - the client first creates what is known as a "__code verifier__". This is a cryptographically random string using the characters A-Z, a-z, 0-9, and the punctuation characters -._~ (hyphen, period, underscore, and tilde), between 43 and 128 characters long.
  - Client hash256 alabiliyor; __code verifier__'i, "BASE64-URL-encoded string of the SHA256" olarak çevirmelidir. Yoksa direk code verifier ile devam edebilir. hash alınsın alınmasın, artık (bu adımda), bu değere artık "__code challenge__" deniliyor.
  
  Artık __Authorization Request__'e aşağıdakiler ek olarak eklenmelidir:

  - __code_challenge__
  - __code_challenge_method__ --> "plain" (eğer hash alınmadıysa) veya "S256" (hash alındıysa)

  Daha sonra "Authorization Code Exchange" adımında ise tekrar "__code_verifier__"'ı yolluyoruz. Burada artık __code_challenge_method__ yollamıyoruz.

  Auth-server her 2 istekte attığımız code_challenge değerlerini kendi tarafında valide ediyor. Bu da güvenliği arttırıyor.

- ## 2 - implicit flow
Fakat bazı uygulamalar sadece client-side'da çalışıyor. Bu durumda "implicit grant" süreci işletiliyor. Yani client-secret'a htiyaç olmuyor. Tabi bu da güvenlik açıklarına sebep oluyor. acces token direk client'a veriliyor. oysa implicit olmazsa 2 aşama var. Implicit sürecinde __Authorization endpoint__'e client-secret olmadan istek atılıyor ve auth server direk acess token  dönüyor. kaynak: (source-id: 321) title: "4.2. Implicit Grant", subtitle: "4.2.1. Authorization Request".

- ## 3 - username password
Bazı uygulamalar direk son kullancının şifre ve username'si ile acces token'ı elde edebiliyor. En güvensiz yöntemdir. Bu çok özel/istisna durumlarda kullanılmalıdır. "İmplicit" gibi tek istekte access token elde ediliyor. kaynak: (source-id: 321) title: "4.3. Resource Owner Password Credentials Grant".

- ## Authorization Code ile süreç - Adım 1

bu kısım "__Authorization Request__" olarak adlandırılıyor. bunu sağlayan server endpoint'ine "__Authorization endpoint__" deniliyor.

web browser'dan user'ı provider'ın sitesine yönlendirirken şu parametrelerle yönlendirmek gerekli:

- __client_id__

- __reponse_type__: bu istekte spesifik olarak "code" değerini vermek gerekli. "code", response'ta __authorization_code__ istediğinizi belirten bir value'dur.

- __redirect_url__: opsiyonel. provider'a kaydolurkende bu url veriliyor. isterse bu adımda o değer override edilebilir. redirect url http:// diilde app:// gibi de olabilir. bu şekilde native uygulamadan web view açarak login ettiğimiz kullanıcı tekrar uygulamamıza yönlendirilebilir.

- __scope__: provider'ın belirlediği stringlerdir. bu stringler hangi yetkileri istediğinizi belirtiyor. arada boşluk olucak şekilde formatlı olmalılar

  scope application'ın kullanacağı permission'lar olarak düşünülebilir. bu scope 

- __state__: (yukarıda açıklandı.) buraya verilen stringler, aynen geri client'a yollanıyor. burada ek güvenlik sağlamak amaçlı, her istekte her seferinde random data yollamak şiddetle önerilir.

yukarıdaki istek provider'ın authorization url'sine yapılmalıdır.

Bu request'in dönüşünde __authorization_code__ ve __state__ dönmektedir.

- ## Authorization Code ile süreç - Adım 2 (Authorization Code Exchange step)

authorization_code'u access_token'a çevirme isteğidir/aşamasıdır.

istek attığımız API'ye, "__token endpoint__" deniliyor.

login olma aşaması bittiğinde, client tarafa __authorization_code__ gönderildi. bu kodu __access_token__'a çevirmek için provider'ın token url'sine post isteği aşağıdaki parametrelerle yapılmalıdır:

- __grant_type__: bu istekte spesifik olarak "authorization_code" vermek gerekli.

- __code__: bize bir önceki response'ta gelen __authorization_code__.

- __redirect_uri__: success olma durumunda buraya bir istek yapılacak

- __client_id__:

- ## api calls

__access_token__'ı alan client/app, artık API'ye istek yapabilir. oauth2 bu istek hakkında standart içermiyor. fakat genelde header'daki "Authorization" değerine "Barear 345345234234234" şeklinde yollanıyor. resource server gelen istekteki __access_token__'ı alıyor ve __auth_server__ server'a gönderiyor. __acees_token__'ın geçerli olup olmadığının cevabını __auth_server__'dan alıyor. her istekte bu işlem tekrarlanıyor. eğer gelen istekteki access_token bir jwt ise; o zaman auth server'a gitmeye gerek kalmaz. çünkü jwt'de, resource server'ın kendisi, token'ı private key ile açıp kontrol edebilir.

- ## refresh token vs access token

refresh token jwt'deki aynı mantıkta kullanılmaktadır. AŞağıdaki şekilden de akış görülebilir:

```
+--------+                                           +---------------+
|        |--(A)------- Authorization Grant --------->|               |
|        |                                           |               |
|        |<-(B)----------- Access Token -------------|               |
|        |               & Refresh Token             |               |
|        |                                           |               |
|        |                            +----------+   |               |
|        |--(C)---- Access Token ---->|          |   |               |
|        |                            |          |   |               |
|        |<-(D)- Protected Resource --| Resource |   | Authorization |
| Client |                            |  Server  |   |     Server    |
|        |--(E)---- Access Token ---->|          |   |               |
|        |                            |          |   |               |
|        |<-(F)- Invalid Token Error -|          |   |               |
|        |                            +----------+   |               |
|        |                                           |               |
|        |--(G)----------- Refresh Token ----------->|               |
|        |                                           |               |
|        |<-(H)----------- Access Token -------------|               |
+--------+           & Optional Refresh Token        +---------------+
```
