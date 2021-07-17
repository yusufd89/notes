############################

############################
# SECURITY
############################

############################

# impersonation
türkçe kelime anlamı: kimliğe bürünme

impersonate --> taklit etme

bir user ile başka bir user'ın şifresini bilmeden onun yerine giriş yapmak isteyebilir. bu genelde admin'ler tarafından yapılmaktadır. bu işleme impersonation denir.

Fakat yazılımın arkaplanda impersonation'dan haberi olup olmayacağı standartlarda esnek bırakılmıştır. kaynak: (source-id: 286) title: "1.1.  Delegation vs. Impersonation Semantics". Şu şekilde belirtilmiştir: "It is true that some members of the identity system might have awareness that impersonation is going on, but it is not a requirement.".

# delegation
impersonation'dan farklıdır. delegation'da; A user'ı, B'user'ını delegate ediyor ise, "merheba $userName" basan bir sayfada "merhaba A" görecektir. Yani, A kendi kimliğini taşımaya devam etmektedir. A user'ı, B'nin rollerini (önceden delege edilen (konfigüre edilen) rollerini) taşımaktadır (tümünü taşımak zorunda diil).   

# keycloak ile impersonation
keycloak token impersonation ile Oauth 2.0'a ek uzantı olan "OAuth 2.0 Token Exchange" özelliğini kullanmaktadır. (source-id: 286). Fakat süreç tamamen aynı diildir ve production-ready değildir (2021 mart).

- Production-ready destek olmadığı için keycloak'u şu şekilde başlatmak gerekiyor:

/keycloak-12.0.4/bin/standalone.sh -Dkeycloak.profile.feature.token_exchange=enabled -Dkeycloak.profile.admin_fine_grained_authz=enabled

- impersonation yapacak olan user'a, "realm-management" altındaki "impersonator" rol'ü atanmalıdır.

- User normal login sürecini tamamlar ve kendi access_token'ını alır.

- keycloak'a şu istek atılır:

```yml
POST http://localhost:8080/auth/realms/realm1/protocol/openid-connect/token

grant_type: urn:ietf:params:oauth:grant-type:token-exchange
client_id: $client-id
requested_subject: 1ab7cfd4-5401-4985-b264-145c25aa6c19 (taklit edilecek user'ın keyclok-id'si)
subject_token: $current(impersonator)-access-token
client_secret: $client-secret
```

Response olarak bize access ve refresh token dönecektir. Bu dönen jwt'leri decode edersek içerisinde taklit edilen user'ın bilgilerinin (role, isim...) olduğunu göreceğiz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# vault
hashicorp firması tarafından geliştirilen açık kaynaklı key management yazılımı.

config dosyaları hcl (HashiCorp Configuration Language kısaltmasıdır) formatındadır. hcl, json, yml'ye alternatif olarak geliştirilmiştir. örnek syntax:

```hcl
service {
    key = "value"
}

service2 {
    key2 = "value2"
}

// comment-1

# comment-2

/* multi-line
   comment */

root1 "child1" {
    prop1 = "value1"
}
// equivalent to yaml:
// root1.child1.prop1: value1
```

# initialization
vault sunucusu başladığında sadece 1 kere init etmek gerekli. init output'u olarak şunlar basılıyor:
- 5 adet unseal-key'lerı

  unseal-key'lerden en az 3 tanesi ile vault ancak unseal edilebiliyor. Unsealing süreci her sunucu restartında gerektiği için bu key'lere ihtiyacımız olacak. kaynak: (source-id: 288) title: "Initializing the Vault", kod bloğunun içindeki outputtaki metinler.

- 1 adet root token
  
  bu token ile client her işlemi yapabiliyor.

# secret engine
vault'ta herşeyi gruplamak amaçlı her "secret" belli 1 adet "secret engine" altında olmalıdır. bu şekilde bir secret engine'i komple disable edebiliriz yada enbale edebiliriz.

# authantication
client'ın vault'tan data çekmesi veya manipülasyon yapabilmesi için her uygulamada olduğu gibi önce login olmalıdır. "token" ile authantication'da buna bir örnektir. kaynak: (source-id: 289) title: "14.2. Token authentication".

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# subresource integrity
web tarayıcıları indirdikleri dosyanın hash'ine bakarak validasyon yapar. eğer valid diilse o dosyayı html'e import etmez. developer console'da da hata verir. örnek:

```html
<script src="https://example.com/example-framework.js"
        integrity="sha384-oqVuAfXRKap7fdgcCY5uykM6+R9GqQ8K/uxy9rx7HNQlGYl1kPzQho1wx4JwY8wC"
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Trust on first use (or TOFU or trust upon first use or TUFU)
2 makinenin haberleşmesinde ilk aşamada birbirlerine bir identifier üzerinden güvenmeleri tekniğidir. TOFU kullanan birkaç örnek üzerinden gidelim:

- ssh

  ssh client sunucuya bğalndığında, eğer bu sunucuya giderken (eğer bu sunucu için daha önce son kullanıcıdan onay alınmamış ise), son kullanıcıya sunucunun identifier'ini gösterir. eğer son kullanıcı onaylar ise artık bu bilgiyi shh client $HME dizinine kaydeder ve bir daha son kullanıcıya sormaz.

- HTTP Public Key Pinning

  browser sunucuya erişip sertifikasını aldığında onu valide ederse doğru olarak kabul eder ve bu bilgiyi db'ye kaydeder. ilerdeki zamanlarda tekrar aynı sunucuya gidildiğinde, db'de bulunan key'lere göre sunucyu valide eder.

- Signal messenger

  sinal karşı tarafın identifier'ini son kullanıcıya sadece gösterir ve karşı taraf ile iletişimi son kullanıcının onayı olmadan başlatır. yani TOFU'yu direk(onaysız) uygular. Son kullanıcı eğer isterse identifier'ı karşıdaki kişiden manuel barcode aracılığı ile kontrol edebilir.

  Eğer karşıdakinin identifier'i değişirse, signal bizi uyarır. fakat yine iletişime devam eder.

  eğer biz karşı tarafın identifier'ini signal uygulaması içerisinden "verified" olarak işaretlersek ve karşıdakinin identifier'i değişirse, signal sadece uyarmakla kalmaz aynı zamanda iletişimi block'lar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Crypto-shredding
shredding kelime anlamı: parçalama

şifrelenmiş data'ları kullanılamaz hale getirmek için tüm şifrelenmiş data'ları tek tek override etmek veya silmek yerine, sadece decryption key'i silme çözümüdür.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# 3 state of data in computer science

- __Data at rest__

  data'nın, kalıcı storage'de durma durumudur.

- __Data in transit (or data in motion or data in flight)__

  data'nın, network üzerinde taşındığı durumlardır. interprocess-communication gibi durumlar bu gruba dahil diildir.

- __Data in use__

  data'nın, RAM, "cpu cache" gibi kalıcı olmayan bellekte olma durumudur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# confused deputy problem
deputy kelime anlamı: vekil

client olarak; bir servise bir istek yaptık, bu servis işlemi yapabilmek için diğer servislere de istek yapıyor. dolayısı ile diğer servisler ilgili isteğin nerden geldiğini bilebilmeli. security'yi buna göre implemente etmeliyiz. çünkü diğer servislere dışarıdan da istek gelebiliyor. bu istek internal'dan mı geliyor yoksa client'tan mı, her servis bunu ayırt edebilmeli. Aynı zamanda client yaptığı bu istek ile diğer servislere istek tetikleyebilmiş oluyor. burada farklı zaafiyetler söz konusu olabiliyor. bu durum confused deputy problem olarak adlandırlılıyor. çünkü her aracı servis client adına istek atmış oluyor. bu aracı servisler, bu problem kapsamında vekil olarak adlandırlılıyor.

bir servisimiz olsun. parametre olarak dosya adı ve dosya içeriği alsın. eğer securi-ty implementasyonumuzda güvenlik açığı var ise; client sunucudaki /etc/hosts dosyasını dahai güncellebilecektir. oysa buna normalde yetkisi yoktur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# secret zero problem (or secret-zero problem)
güvenlik birçok katmandan oluşur. tüm sistem diilde sadece bir katman hacklenebilir. dolaysı ile birçok katman vardır. "x" katmanı hacklenir ,"y" katmanı hacklenir, en sonda ise tek bir katman kalır. işte bu katman hacklendiğinde tüm sistem hacklenmiş olur. bu en son katmandaki "secret key"'in hacklenme durumuna "secret zero" problemi denir.

yani bir data'yı şifrelemek için yeni şifre kullanırsınız. bu yeni şifre'yi de şifrelemk için bir şifre kullanırsınız. bu şekilde 100 adım dahi yapabiliriz. fakat her zaman mutlaka bir şifreyi koruma gereği duyacağız. bu şifre'ye "secret zero" denir. "secret-zero problemi" ise; bu şifreyi nasıl koruyacağımızdır.

"secret zero" problemine çözüm bulmak teorikte imkansız. çünkü hacklenecek her zaman son bir sistem/şifre olmalıdır. fakat bazı sistemler son katmanı parçalara bölerek "secret zero" problemini kısmen de olsa çözmektedirler. örneğin, bir "master key"'imiz (secret zero) olsun. bu master'i 2 ye bölersek o zaman bu master key ile işlem yapmak istediğimizde bu 2 kişiye de ulaşmamız gerekecek. yani; "secret zero" tek bir yere bağımlı diil. her kişide multi-factor authantication sistemleri ile korunur. bu şekilde secret-zero'yu korumak için farklı bağımlılıklarda eklenmiş olur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# SQL injection (or SQLi)

- SQL injection'dan kaçmak için ORM framework sürümümüzün güncel olmasına dikkat etmeliyiz. çünkü orm'nin aşağıda örneklendirilen bind işleminde kontroller gerçekleştiriyor.

- Dışardan alınan parametreleri bind ederek tanımlamalıyız:

  ```java
  Query query = createQuery("from LoginUsers where userName=:userName");

  query.setParameter("username", userName); //ORM burada userName'in tipini biliyor ve kontrolleri kendisi yapıyor. 
  ```

  Bind etmeyi sadece SQL komutları için değil, JPQL için dahi yapmalıyız. SQL ile JPQL farksızdır. JPQL; ancak bind edilirse güvenliği sağlar.

- Dinamik querry yapılacak ise Criteria API'den faydalanılmalı

- # tipleri

  - # In-band SQLi (or Classic SQLi)
      
      - # Error-based SQLi
        Exception detayları uygulamadan denüyor ise, bunlardan yola çıkarak sunucudan bilgi toplanır.

      - # Union-based SQLi
        "select * from X where ' $VAR '" gibi sql'lerde VAR inputunu değiştirerek sunucudan bilgi toplanırız. VAR yerine bir şey eklememiz ancak ve ancak UNION sorguları ile mümkündür. bu sebeple bu ataklara Union-based denir.

  - # Inferential SQLi (or Blind SQLi)

      - # Boolean-based (or content-based) Blind SQLi
          Suncuda bu şekilde bir http controler olsun:

          ```java

          @HTTTP_GET
          isExist(String input){

              boolean exist = doSQL("SOME SQL" + input);

              if(exist){
                return "true";
              } else {
                return "false";
              }
          }
          ```

          Bu kontrollerdan bilgi almak için şöyle bir yöntem geliştirilebiliriz:

          input'taki sql'imiz önce tüm tabloları çeken sql'i çalıştıracak. sonra bu tablo listesindeki ilk elemanın (ilk tablo adının) ilk karakeri A mı diye bakılacak. eğer A ise "boolean exist = true" olacak şekilde dönüş yapılmalı. eğer true olursa demekki ilk karakter A. 

          Aynı işlemi ilk tablonun ikinci elemanı içinde yapmalıyız ve tüm alfabe ve özel karakterler için yapmalıyız. Her tablo adı 100 karakter olsa, 100 tablo olsa, 50 karakter kombinasyonu olsa, 100\*100*50 adet HTTP isteğinde tüm tablo listesini almış oluruz.

          Bu işlemi daha hızlandırmak için farklı yöntemler mevcut. Örneğin; Tablo isminin ilk karakterinin ASCII karşılığı alınır. Örneğin bu değer 50 olsun. Biz sql sorgumuzda bu değer 50'den küçükse "boolean exist = true" dönecek şekilde ayarlarız. Eğer true dönerse; ASCII 50'nin üzerindeki hiçbir karakter için HTTP denemesi yapmamıza gerek kalmayacak. Bu tarz trick'lerle deneme sayımızı çok azaltabiliriz. 

      - # Time-based Blind SQLi

          controller'ımız boolean dahi dönmüyor olsun:

          ```java
          @HTTTP_GET
          isExist(String input){

              boolean exist = doSQL("SOME SQL" + input);

              if(exist){
                return "true";
              } else {
                return "false";
              }
          }
          ```

          Buradan bilgi alabilmek için Boolean-based ile aynı SQL'leri çalıştıracağız. Fakat dönüşümüzde true false alamadığımızdan, dönüş değerimiz yerine zaman aralığından faydalanacağız. SQL'lerimiz true durumunda sleep(7) gibi bir SQL fonksiyonu çalıştıracak. eğer 7 saniye içinde cevap gelmezse o SQL sonucunu true olarak varsayacağız.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Insecure Direct Object References (or IDOR)
Objelere erişmke için kullandığımız ID'ler, eğer uygulamamızın arkaplanında kullandığımız referanslar ise, o zaman bu referansları kullanarak kötü niyetli kullamnıcılar güvenlik açıklarından yararlanabilir. bu tarz ID'lere (referanslara) IDOR denir.

örnek:
Account objemizin ID'si 1001 olsun. eğer bu ID diğer tüm metodlarda (isil, update) kullanılan sabit bir ID ise, bu ID, IDOR'dur. çünkü aynı ID sil metoduna yollandığında o hesap silinecektir.

bu durumu önlemek için;
- önyüze dönülen her referansa sadece o işlem için geçici farklı bir referans atanır
- her işlemde kullanıcının bu işlemi yapmaya yetkisi var mı diye detaylı kontrol edilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# PIN (or Personal Identification Number)
geçici olarak kullanılan şifredir.

# Multi-factor authentication (or MFA)
factor türkçe kelime anlamı: faktör, etken

işlem yapabilmek için birden fazla onay adımının olması ve her onay adımında farklı kanallardan güvenlik doğrulamalarının yapılmasıdır. örneğin; ilk adımda şifre giriliyorsa, ikinci adımda sms'in girilmesi bambaşka bağımsız bir kanal üzerinden sağlandığı için MFA olur. fakat şifre + CAPTCHA girişi yapmak MFA'yı karşılamaz.

# Two-factor authentication (or 2FA)
MFA'nın 2 adımlı olan türevidir.

# Two-step verification (or two-step authentication)
MFA diildir. MFA örneğinde verildiği gibi farklı kanallardan sağlanmayan güvenlik adımlarını temsil eden gruptur.

# TOTP (or Time-Based One-Time Password)
Bir OTP çeşididir. Offline olarak OTP üretir. Bu OTP sadece belirli bir süre geçerlidir. Bu sebeple Time based'dir.

# Google authenticator
TOTP kullanımını sağlayan bir GUI uygulamasıdır. Kullanıcı parametre olarak OTP'nin yenileneceği döngü süresi (varsayılan 30 saniye) ve secret-key'i google'den alır. Bu parametreler ile 30 saniyede bir yeni bir OTP üretir. Bu OTP'nin algoritması bellidir. Bu sebeple offline olarak OTP üretilebilir.

Google authanticator açık kaynaklı bir algoritmaya dayanır. bu sebeple alternatifi birçok client ve programlama dili API'si mevcuttur. 

# otp hakkında
otp süresi algoritmaa göre değil, kullandılığı hizmetin kendisine göre değşir. yani; google'ın kullandığı algoitma 30 saniyeliktir. fakat aynı algoritmayı 40 saniye olacak şekilde de ayarlayabiliriz.

otp şifresi T zamanında üretilmiş olsun. artık bu T zamanında üretilen otp google için 30 saniye süresinde kabul görecektir. T+1 zamanında aynı secret key ile bir OTP üretelim. Bu password'de artık 30 saniye geçerli olacaktır. dolayısı ile T+1 de oluşturduğumuz key daha farklıdır. Fakat T+2 anında her 2 key'imizde geçerlidir.

Örneğin; https://github.com/bilelmoussaoui/Authenticator uygulaması ile masaüstünde aynı secret key ile iki şifre oluşturduğumuzda, iki şifre farklı zamanlarda oluşturulacağı için farklı key göstreceklerdir. her 30 saniyede bir yeni key oluşturacaklar ve her ikisinin döngüsünün sona erdiği an farklı olduğundna hep farklı key üretecekler.

Bazı servisler her 2 anahtarı da kabul etmektedir. Fakat google bunu kabul etmiyor. "Google authenticator" uygulaması bu durumu şu şekilde çözüyor. "Google authenticator" kendi içinde belli zaman aralıkları belirlemiş. Her 30 saniye bir zaman aralığı içinde, yani 00:00:00 - 00:00:30 ilk zaman aralığı.  00:00:30 - 00:00:60 ikinci zaman aralığı. Eğer 00:00:35 anında bir key üretirsek; bizi ikinci zaman aralığına otomatik alıyor ve 00:00:30 anında şifreyi üretmişiz gibi varsayıyor ve buna göre hesaplamaları yapıyor. Dolayısı ile her 30 saniye için en fazla 1 farklı key üretebiliyoruz. Bu tamamen "Google authenticator"'ın önyüzde uyguladığı bir mantıktır. anahtar üretim algoritması ile bağlantılı bir durum diildir.

Aynı durum https://github.com/bilelmoussaoui/Authenticator için geçerli değildir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Post-quantum cryptography (or quantum-proof or quantum-safe or quantum-resistant)
Kuantum hesaplamaları fizik kuralları gereği her türlü hesaplamayı verimli şekilde yapamamaktadır. Bu sepeble kuantum teknolojisinin hızlı hesaplamaya tabi tutamayacağı algortimalar ortaya atılmıştır. Bu önlemleri üretebilmek için matematik ve fizik bilgisi de gerekmektedir.

One-time-password, n deneme sonrası hesabın devre dışı bırakılması gibi önlemlerde de terminolojik olarak bakıldığında "quantum resistant security"'yi sağlamaktadır.

2019 yılı itibari ile çoğu asimetrik şifreleme (private/public key'e dayanan şifreleme) algoritmaları kuantum bilgisyaralarına karşı dirençsiz. Simetrik algoritmalar ise dirençli. Fakat simetrik algoritmalar'ın keyleri yarıya düşürülmüş kadar daha hızlı çözülebiliyor. örneğin 512'lik bir anahtara sahip bir şifreleme algoritması, eğer kuantum bilgisayarı ile kırılırsa, 256'lık hızında kırılabiliyor.

2019 yılı itibari ile özgür lisanslı ve ticari anlamda tümüyle kullanılabilecek quantum resisdent algoritması yoktur. Olanlar ya lisanslı, yada key'leri büyük olması gibi önemli dezavantajları mevcut. 

# quantum algorithms
kuantum bilgisayarların verimli çözdüğü algoritmalardır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# HTTP Public Key Pinning (or HPKP)
Ssl işlemlerine ek güvenlik yapmak için kullanılan bir yöntemdir. Sunucu cevaplarının header'ına şunu ekler:

```json
Public-Key-Pins: 
         pin-sha256="cUPcTAZWKaASuYWhhneDttWpY3oBAkE3h2+soZS7sWs=";

         pin-sha256="M8HztCzM3elUxkcjR2S5P4hhyBNf6lHkmjAHKhpGPWE=";

         max-age=5184000
```

Tarayıcı bu değerleri tüm yaşamı boyunca (en fazla max-age e göre) saklar. Pin-sha değeri sunucunun public key sha'dır. Eğer ilerde bir hacker sunucunun döndürdüğü public key'i değiştirirse; tarayıcı eski sha'ları da kontrol edeceği için bir sorun olduğunu anlayacak ve kullanıcıyı uyaracaktır.

2 tane pin olmasının sebebi max-age süresince sunucunun gerçektende public key'ini değiştirmesi durumunda kullanılacak backup'tır. Sunucu dilediği kadar pin-sha yollayabilir.

Bir siteye bir tarayıcıdan ilk defa gidiliyorsa; bu güvenlik önlemi bir işe yaramaz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# browser fingerprint
internet siteleri kullanıcılardan kısıtlı bilgi alabilmektedir. fakat bu bilgilerin kombinasyonları ile yine makinanın uniqu'liğini tespit edebilmektedirler.

- cookie'nin açıp olup olmadığı bilgisi
- hangi fontların yüklü olduğu listesi
- user agent
- cpu tipi
- timezone
- index db olup olmadığı
- do not track yollanıp yollanmadığı
- screen resolution
- dil

gibi daha bir çok parametre ile tarayıcının uniqu'liği ortaya koyulabilmektedir. hatta bazı özellikler tek başlarına %100 unique'liği sağlayabilmekte, bazı özellikler yine tek başlarına %99 oranında unique'liği sağlayabilmektedirler.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Biyometri (or biometry)
yaşayan organizmaların ölçümlerine verilen genel isimdir. tüm niteliklerin sayısal ortama aktarılmış halidir.

# biyometrik authentication yöntemleri (or biometric verification methods)
- parmak izi (or fingerprint) (parmaklara gözle detaylı bakıldığında bu şekiller görülebilir)
- yüz tanıma (or face recognition)
- damar izi (or vein scar)
  - parmak damar izi (opr finger vein print)
  - avuç içi damar izi (or palm vein print)
- göz tarama
  - retina taraması (or retinal scan)
  - iris tanıma (or iris recognition)
- ses tanıma (or voice recognition)
- (elyazılı) imza

yukarıdaki biyometrik bilgiler genişleyebilir/büyüyebilir fakat şekilleri değişmez. bu sebeple ömür boyu aynı kalırlar.

engelli kişiler, bazı biyometrik bilgileri veremediği unutulmamalıdır.

her veri, teorik olarak replice edilebilir. fakat başka başlıkta anlatıldığı gibi; kimlik doğrulama amaçlı yukarıdaki her biyometrik veri kullanılabilir. çünkü kimlik doğrulama yapılırken, %100 aynı olan replica'lar kabul edilememektedir.

hatalar genelde şunlardan kaynaklanmaktadır:
- yazılımsal/algoritmik hatalar
- kontrol edilen biyometrik cihazların ucuz olmasından kaynaklı hassas data toplanamaması (örneğin; kameranın kalitesiz olması durumunda, görüntü detaylı pixellere sahip diildir. bu da hatalara sebebiyet verebilir. çünkü hassas ölçümler yapılamaz.)

Tüm biyometrik sistemler aşağıda açıklanmış olan beş özelliğe sahip olmalıdır:
- Evrensellik: Tüm bireyler biyometrik özelliklere sahip olmalıdır.
- Eşsiz olma: Biyometrik karakteristiğin her insanda farklı bir şekilde yer alması.
- Süreklilik: Karakteristiğin zamanla değişmemesi.
- Elde edilebilirlik: Biyometrik özelliklerin bazı pratik cihazlarla ölçülebilir olması.
- Kabul edilebilirlik: Bireylerin biyometriğin ölçüm ve toplanmasında itirazları olmamalı

Karakteristiklere göre karşılaştırma tablosu: Kaynak: (source-id: 290) "Yüz tanıma sistemlerinde canlılık analizi", Yazar: TUGAY BOZİK,  Yüksek Lisans tezi, yayım yılı: 2019

| Biyometrik Karakteristik | Evrensellik | Eşsizlik | Süreklilik | Elde Edilebilirlik | Performans | kabul Edilebilirlik | Yaygınlık |
|--------------------------|-------------|----------|------------|--------------------|------------|---------------------|-----------|
| DNA                      | Y           | Y        | Y          | D                  | Y          | D                   | D         |
| Kulak                    | O           | O        | Y          | O                  | O          | Y                   | O         |
| Yüz                      | Y           | D        | O          | Y                  | D          | Y                   | Y         |
| Yüz Termogramı           | Y           | Y        | D          | Y                  | O          | Y                   | D         |
| Parmak İzi               | O           | Y        | Y          | O                  | Y          | O                   | O         |
| El Geometrisi            | O           | O        | O          | Y                  | O          | O                   | O         |
| İris                     | Y           | Y        | Y          | O                  | Y          | D                   | D         |
| Retina                   | Y           | Y        | O          | D                  | Y          | D                   | D         |
| İmza                     | D           | D        | D          | Y                  | D          | Y                   | Y         |
| Ses                      | O           | D        | D          | O                  | D          | Y                   | Y         |

Y:Yüksek O:Orta D:Düşük

# parmak izi (or fingerprint)
parmak izi en sık kullanılan, en basit ve ucuz yöntemlerle tespit edilen ve karşılaştırılabilen metodlardandır. bu sebeple sık kullanılır.

parmak izinin %100 benzersiz olduğuna dair bir tez yoktur. fakat şu ana dek aynı parmak izi olduğu görülmemiştir. bu sebeple herkes eşsiz olarak varsayar. bazı kurumlar, bu sebepten ötürü sadece 1 parmağın değil, garantilemek amacı ile birden fazla parmak izini birden saklamaktadır. Bunun ayrı bir sebebi de, kötü niyetli kişinin, fiziksel olarak başkasının parmağını kullanabilme ihtimalidir. Bu durumda kötü niyetli kişinin birden fazla parmağı ele geçirmiş olması gerekecektir.

parmak izi benzerliğini kontrol etmek için kullanılan birçok algoritma mevcut. 

alınan parmak izinin ne kadar detaylı alındığı da önemlidir. çok kalitesiz alınan parmak izi kaydı, yanlış sonuçlara yol açabilir.

# biyometrik doğrulama için kulanılan cihazlar
siemens bir cihaz üretsin. bu cihazı XX firması hastanelerde kullansın.

- bazı cihazlarda siemens, hangi bilgiyi (örneğin parmaklardan; parmaklarda milyar çeşit bilgi mevcut) son kullanıcıdan (buradaki senaryoda hastalardan) aldığını paylaşmaz. bu şekilde XX firmasının veritabanı hacklenirse; insanların hangi bilgilerinin çalındığı bilinmemiş olacaktır. ancak siemens'in içinden de, cihazla ilgili gizli bilgilerede erişmeleri gerekecektir.

- aynı zamanda son kullanıcıdan (buradaki senaryoda hastalardan) çekilen bilgiyi şifreler ve bu datayı cihazın output'undan şifrelemiş şekilde paylaşır. şifrenin private key'i de XX firması ile paylaşılmaz. bu şekilde XX'in veritabanı hacklenirse; hacker'lar ancak siemens'in içinden de, cihazla ilgili gizli bilgilerede erişmeleri gerekecektir. siemens'in ürettiği key, her cihaz(model) için de farklıdır.

XX firması zaten kişinin ilgisi önemli değildir. XX firması için önemli olan, kişinin o kişi olup olmadığını anlamak. yani; eşleştirme yapmak. datanın içeriği önemli değildir. cihazın nasıl karşılaştırma yaptığı, XX firması için önemli değildir. bir diğer değişle; parmak izi cihazı gömülü olarak kendi içinde şifrelenerek dışarı bilgi veriyor, fakat XX firması karşılaştırma yapmak istediğinde, cihaz kendi içinde private key'i ile bu bilgiyi açıyor ve karşılaştırma yapıyor. dışarıya sadece true yada false dönüyor. cihaz kendisine gelen bilgi %100 eskisi ile aynı ise false dönüyor (eşit diil). çünkü biyometrik değerler (örnek: parmak damar izi); o anda odanın sıcaklığı, kişinin o gün yediği yemeklerden dahi çok az da olsa etkileniyor. %100 eş bilgi ise; bu kişi databaseden veriyi kopyalamış anlamına geliyor. bu sebeple örneğin ancak %93-%99.999 eşleşen bilgiler onaylanıyor.

peki; hacker %100 benzetilmiş data yerine, %99 oranla benzer data'yı cihaza gönderebilir. dolayısı ile; max eşlemşem oranını %99.999 yerine, %98 yapmak daha mantıklı diil mi? yani; en üst aralık %98 olması daha mantıklı diil mi?

değil. çünkü cihaza input veren hacker, ya %100 benzer veri verebilir, yada hiç alakasız bir veri verebilir. çünkü cihaza giren input şifrelenmiş olmalı. bu şifrelenecek private key'i kimse bilmiyor. dolayısı ile şifrelenmiş data üzerinde deişiklik yapılınca, zaten şifre private key ile açıldığında saçmalanmış bir veri otaya çıkacaktır. yani hacker'ın %99 benzer bir veri oluşturması imkansız. bu sebeple %99 benzer veriler cihaz tarafından onaylanıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# hijack attack
hijack türkçede hırsızlık anlamına gelmektedir. güvenlik saldırısı hijack genel anlamı ile bilginin çalınması anlamına gelir. kelime anlamı gereği çok genel bir tabirdir. fakat hijak saldırıları genelde; iletişimde olan iki makine arasında olan hacker'ın, iletişim sırasında paketleri kendi üzerinden geçirmesi ile olan saldırılar için kullanılır. bu tarz saldırılara aynı zamanda "man-in-the-middle attack" denir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# pentest (or penetration)
penetration türkçe anlamı nufuz etmek, delmek, içine girmektir.

sisteme sızma testleridir. bu testler ile güvenlik açıkları tespit edilir.

# Whitebox vs blackbox vs greybox
pentest tipleridir. pentesti yapacak ekibe sistem hakkında hiçbir bilgi verilmiyor ise blackbox testidir. kodlar, network bilgileri gibi tüm sistem bilgileri veriliyor ise Whitebox testidir. kısmen bazı bilgileri veriliyor ise greybox tipinden test yapılıyor demektir.

# blackbox
kelime anlamı: mat (parlak olmayan, ışık geçirmeyen).

blackbox bilişim dünyasında sadece input ve output'ları gözlenebilen fakat içi görünmeyen herşeye denir.

# Vulnerability Assessment (or zaafiyet tarama)
bu çalışmalar, çoğu zaman pentest'lere benzediklerinden dolayı pentest ile karıştırılmaktadırlar. zaafiyet taramaları; sistemde direk güvenlik açığı oluşturmasada, güvenliği arttırıcı etkenleri tespit etme çalışmasıdır. örneğin; sunucuda kullanılan java sürümü eski olduğunu varsayalım. bu durum pentestler'den dönmesede, zaafiyet taramasından dönmelidir. eğer java eski olduğundan; kullanıcıların bilgilerine erişiliyorsa o zaman pentest sonuçlarında raporlanmalıdır.

# Alpha Testing Vs Beta Testing
junit integration ve sistem testleri koşulduktan sonra yapılan testlerdir. buradan sonra yapılan testler "user acceptence test" olduğu için alpha ve beta da user acceptence testi olarak geçer.

alpha testleri genelde bu işin uzmanı kişilerin yaptığı testlerdir. beta testleri ise public fakat sadece belli kişilerin test etmesi sürecidir.

# functional requirement
- yazılım/sistem ihtiyaç analizleri için kullanılan terimdir. 
- spesifik bir fonksiyonalite/özellik için yazılmış olması gereken ihtiyaca verilen sıfattır. örnek:
  - son kullanıcı formu yolla tuşuna ancak şifresini girdikten sonra basabilecektir.
  - ikinci sayfadan sonra direk dördüncü sayafaya geçiş mümkün olmalıdır.

# Non-functional requirement
bu ihtiyaçlar spesifik özellikler için belirtilmez. genel sisteme hitap eder. örnek:

- sistem 10.000 kişiyi destekleyecektir.
- yazılım güncel linux sistemlerini destekleyecektir.

Bazı kaynaklarda __cross-functional requirement__ olarak geçmektedir. Kaynak: "Sam Newman" "Building microservices" kitabının 151'inci sayfasında "cross-functional testing" başlığı, 2inci paragpaf.

# Functional Testing vs Non-Functional Testing
fonksiyonel test sadece belirli bir özelliğe istinaden koşulan testlerdir. oysa Non-Functional performans gibi kriterleri ölçmek için yapılan testlerdir.

# regresyon testleri
yazılıma eklenen yeni bir özelliğin, sistemde zaten varolan diğer özellikleri etkileyip etkilemediğinin testleridir. bu durumda aslında tüm sistem baştan sona test edilmesi gerekir fakat bu yükske maliyet olacaktır. bu sebeple; sadece etkisi olabilecek potansiyel modüller test edilmelidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# BackTrack
pentest yapabilmek için gerekli tool'ların bir arada sunan, linux tabanlı, canlı cd ile çalışan işletim sistemidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# IPSec
Internet Protokol katmaninda gizlilik ve dogruluk saglamaya yönelik güvenlik standartlari grubudur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# rootkit
sistemin admin kullanıcı haklarını ele geçirip işlem yapmaya çalışan malware'dir. genelde algılanmaları zordur, çünkü zaten en yüksek seviyede yetkiye sahiptirler ve bu sebeple kendilerini gizlemeleri kolaydır.

# IP spoofing (or IP sahteciliği)
IP adresini farklı gösterip request gönderme işlemdir. Tabi cevap bizim isteği yolladığımız makinaya eğil, IP sahibi makinaya gidecektir. Fakat IP sahteciliğinde dönüş cevabı önemsenmez. Yapılmasının amaçları farklıdır. Örneğin; sunucunun bant kaynaklarını tüketmek.

# DoS attack (or Denial of Service attack)
sistemin kaynaklarını (örneğin bant genişliği, cpu) tüketip, hizmetin kullanıcılara uaşmasını engellemeye çalışan saldırı tipidir.

Denial-of-service terimi "servisin reddi" anlamına gelir. yani; ilgili kullanıcıları saldırı altında olan servis reddetmek zorunda kalır.

# DDoS attack (or Distributed DoS attack)
birçok makineden paralel DoS atağı yapma saldırısıdır. DDoS saldırıları bazen botnet ağından, target'a yapılmaktadır.

# Malware (or malicious software)
category of all dangerous softwares.

# Spyware
kullanıcıdan habersiz arkaplanda bilgi toplamak amaçlı yazılmış zararlı uygulamadır. örnek: keylogger.

# Phishing
Password'ün ilk karakteri ve fishing'in (balık avlama, oltalama) birleşiminden oluşan bir terimdir.

şifre gibi bilgileri çalmak için, gerçek bir kurumdan geliyormuş gibi e-posta yada benzeri sayfalar ile hazırlanan tuzaklara verilen isimdir.

# Social enginnering
Sosyal mühendislik, internette insanların zaafiyetlerinden faydalanarak çeşitli ikna ve kandırma yöntemleriyle istenilen bilgileri elde etmeye çalışmaktır.

# Adware
reklam gösteren uygulamalardır.

# Ransomware
Ransom türkçe kelime anlamı: fidye

fidye isteğen yazılımlar. genelde sistemde belli şeyleri şifrelerler, para karşılığında karşılığında bilgisayarı tekrar virüsten arındıracağını idda eder.

# Scareware
Scare kelime anlamı: korkmak

farklı bir yazılım yükleme vaadiyle (gerçekten o yazılım yüklenir) kurulup, arkaplanda kötü amaçlı farklı yazılımlar çalıştıran uygulamalardır.

# Botnet (or zombi ağı)
her bilgisayara botnet dediğimiz bu zararlı yazılım yüklenir. bu zararlı yazılım, kurulduğu makineye uzaktan erişim için güvenlik açığı sağlar. bu şekilde tek bir noktadan tüm uzak bilgisayarlar yönetilebilir olur. bu kurulan network ağına "zombi ağı" denir. her bilgisayara ise "zombi (or zombie)" denir.

# backdoor
bilgisayarın uzaktan yönetilebilmesi için açılan güvenlik açığına verilen isimdir.

# trojen (or Truva atı)
Scareware ile farkı genel olarak yoktur.

# virüs
otomatik yada kullanıcı tıklamalarıyla farklı makinelere yayılma özelliği olan malware'lerdir.

# Worm (or solucan)
başka makinelere otomatik yayılır.

# Brute-force attack (or kaba kuvvet atağı)
Sadece deneme yanılma ile sürekli olarak farklı girdilerle doğru çıktıları elde etmeye çalışma işlemidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# TLS (or Transport Layer Security)
TLS ve SSL mesajlaşma sırasında şifreleme yöntemlerini belrleyen alternatif protokollerdir. fakat TLS, SSL 3.0'a baz alınarak geliştirilmiştir. Aslında bir nevi yeni bir sürümdür fakat lisans sebepleri yüzünden yeni bir isim kullanılması uygun görülmüştür.

TLS, SSL'e göre daha genişlenitlmiş bir protokoldür. TLS, SSL protokolünü işler fakat iletişim başlangıcında direk olarak güvenli bağlantı üzerinden haberleşmez. Daha sonra güvenli bağlantıyı kurar. Oysa SSL de direk güvenli bağlantı işletilmelidir.

# ssl version history

| version | publish date |
|---------|--------------|
| SSL 1.0 | Unpublished  |
| SSL 2.0 | 1995         |
| SSL 3.0 | 1996         |
| TLS 1.0 | 1999         |
| TLS 1.1 | 2006         |
| TLS 1.2 | 2008         |
| TLS 1.3 | 2018         |

Artık SSL 2.0 ve 3.0 bulunan güvenlik açıkları sebebi ile güvensiz olduğu belgelerle resmileştirilmiştir.

# sunucunun sertifika detaylarını görme
Birçok farklı työntem kullanılabilir:

- (source-id: 291) gibi birçok site girdiğimiz domain name adresine istek yaparak detayarı web tarayıcıda bize raporluyor. hangi client'ların (web tarayıcı, java) sürümleri ile bu sertifikada sorun çıkarıp çıkarmayacağını da raporluyor.

- (source-id: 292) birçok farklı sertifika içeren sayfaya linkler içeriyor. bu şekilde web tarayıcımızın her sertifika için nasıl uyarı verdiğini veya diğer davranışlarını inceleyebiliyoruz. Badssl projesi burada geliştirilmektedir: (source-id: 293)

- komut satırı uygulamaları ile sertifika ve handshare işlemlerinin detaylarını print edebiliriz:
  - openssl s_client -showcerts -connect ma.ttias.be:443
  - curl -vvI https://gnupg.org

# Simetrik Şifreleme Algoritması (or gizli anahtarlı şifreleme or secret key encryption or symmetric-key algorithm)
bazı yerlerde eş anlamlı olarak bu terimlerde kullanılıyor: __single-key yada shared-key yada one-key__

Veriyi şifrelemek ve şifreli veriyi çözmek için her iki tarafında bildiği ortak-tek bir anahtar kullanılır.

# Asimetrik şifreleme Algoritmasi (or asymmetric algorithm or açık anahtarlı şifreleme Algoritmasi)
public-private anahtar yapısına dayanır. public key ile şifrelenmiş bir data'yı, ancak o private key ile birlikte oluşturulan public key ile düzgün şekilde açabiliriz. (aynı şey tersi için de geçerli - public ile şifrelenen sadece private ile açılabilir)

# anahtar (or key) ve şifrelerin çözülme hızı
- public ve private key'ler birer şifredir. dosya olmalarının sebebi büyük boyutta olmalarıdır. örnek 512 karakterli şifre.

- anahtar ile şifrelenmiş bir verinin çözülmesi uzun sürmektedir. örnek: ortalama değerler üzerinden konuşursak; 2017'de ortalama bir bilgisayar, 128'lik bir sha ile şifrelenmiş bir veriyi 2 trilyon yılda çözebiliyor.

- Aynı anahtar uzunluığuna sahip simetrik algoritma, asimetriklere göre daha uzun sürede çözülebiliyor. örnek değeler:
  - 1024-bit RSA keys are equivalent in strength to 80-bit symmetric keys
  - 2048-bit RSA keys to 112-bit symmetric keys
  - 3072-bit RSA keys to 128-bit symmetric keys
  - 15360-bit RSA keys to 256-bit symmetric keys
  
  Yukarıdaki değerler için kaynak: (source-id: 294) "Series/Number: NIST Special Publication 800-57 Part 1 Revision 4". "Ttile: Recommendation for Key Management, Part 1: General". 

# passphrase
pass (geçiş) ve pharese (ifade) kelimelerinin birleşimidir. parola anlamında kullanılır.

ssh-keygen gibi komut satırı uygulamaları ile private-public key oluşturulmaktadır. bu private key'ler oluşturulduğunda bizden passphrase istenebilir. bu opsiyoneldir. eğer passphrase istenirse oluturduğumuz key bu passphrase ile şifrelenir. aynı şekilde public key'de buna istinaden oluşturulur. dolasyısı ile private key dosyamıza ulaşan hacker, şifreli dosyamıza ulaşmış olur.

# sayısal imza (or e-imza or elektronik imza or sayısal imza or electronic signature or e-signature)
bu kavram bir şifrelereme algoritması değildir. sadece data'yı şifreleyen tarafın, kendi imzasınıda dataya eklemesi ve bu şekilde açan tarafın bu mesajın sadece o alıcıdan geldiğine emin olmasını sağlamasıdır + verinin bütünlüğünün (değiştirilmemiş olduğunun) sağlanmış olmasıdır.

# RSA
Ron Rivest, Adi Shamir, ve Leonard Adleman tarafından geliştirilmiştir. RSA ismi bu kişilerin soyisimlerinin başharflerinden gelir.

Bir çeşit asimetrik şifreleme algoritmasıdır.

# Shamir's Secret Sharing
Adi Shamir tarafından geliştirilen yöntemdir.

Bir çeşit __Secret sharing (or secret splitting)__'dir. Bir anahtar birden fazla anahtar olarak parçalanır. Ancak bu parçalar biraraya getirilerek master key oluşturulur. Bu şekilde "secret zero" problemine (kısmen) çözüm getirilir.

Sahmir algoritmasında tüm parçaların bir araya gelmesine gerek yoktur. Minimum sayı var, o sayıda anahtarlar birleştirilmesi master key'inm oluşturulması için yeterlidir.

# DES (or Data Encryption Standart)
simetrik bir şifreleme algoritmasıdır.

# AES (or Advanced Encryption Standard or Gelişmiş Şifreleme Standardı)
Rijndael tarafından geliştirilmiştir. AES, Rijndael'ın proposal'ından ayrı olarak farklı isimde (AES ismi ile) resmileştirilmiştir.

DES artık eski kaldığı için pek tercih edilmemektedir. bu algoritma onun yerini alması için geliştirilmiştir. simetriktir.

"Key size (or key length)" genelde kripto dünyasında bit bazında birime sahiptir. Bu sebeple AES-128 (or AES128), 128 bitlik anahtar istemektedir (başka boyutta anahtar kesinlikle olmaz).

Wikipedia sayfasında bu şekilde notlar düşülmüş (fakat buna karşılık resmi bir kaynak bulamadım):

- Key sizes of 128, 160, 192, 224, and 256 bits are supported by the Rijndael algorithm, but only the 128, 192, and 256-bit key sizes are specified in the AES standard.
- Block sizes of 128, 160, 192, 224, and 256 bits are supported by the Rijndael algorithm for each key size, but only the 128-bit block size is specified in the AES standard.

# cipher (or cypher)
şifrelemek için kullanılan algoritmadır.

__ciphertext__ terimi "şifreli" anlamına gelmektedir. bunun tersi ise "__plaintext__"'tir ve türkçe'de "__açık metin yada düzmetin__" olarak çevrilir.

# encrypting vs coding (or encoding) | decrypting vs decoding
coding ve decoding bir girdiyi farklı bir formata çevirmek anlamına gelir. çevirirken public olan bir şema/formata çevrilmesi gerekir. yani şifreli bir işlem yapılmamaktadır. eğer şifreli bir işlem olursa o zaman encrypting/decrypting olurlar.

# base64
çift yönlü bir algoritmadır. anahtarsız geri çevrilme işlemi yapılabilir. bu sebeple şifreleme algoritması değildir. çıktı kümesindeki karakterler, ASCII'nin sadece belirli elemanlarını içermektedir. çıktıda limitli bir karakter kümesi olabileceğinden terslik yapabilecek karakterler ortadan kaldırılmış olur. genelde işaret kararkerleri olmadığından; dosya sistemindenki dosya isimleri, xml, json içerisindeki degerler gibi kullanım alanları vardır.

input olarak verilen binary data; 6 bit olarak okunur. 2^6=64 olduğundan; 64 farklı karakter çıktı kümesi vardır. çıktı kümesine "Base64 Alphabet" deniliyor. çıktılar şu şekilde: 

- 000000 --> A
- 000001 --> B
- 000002 --> C
- ...
- 000025 --> Z
- 000026 --> a
- 000027 --> b
- ...
- 000051 --> z
- 000052 --> 0
- 000053 --> 1
- ...
- 000061 --> 9
- 000062 --> +
- 000063 --> /

base64'ün birçok implementasyonu var:

- RFC 3548 or RFC 4648 -> standart base64. Bu genel kabul gören ve özel bir amaç için tasarlanmayan base64.

- RFC 2045 -> MIME BASE64

- ve daha birçoğu: (source-id: 433) "Variants summary table" başlığı.

= (eşitlik) işareti bazı implementasyonlarda padding kartakteri olarak kullanılmaktadır.

# java'da base64
javada birçok base64 encode/decode kütüphanesi var.

- java 6 ile

```java
javax.xml.bind.DatatypeConverter.printBase64Binary("hello".getBytes());

DatatypeConverter.parseBase64Binary("aGVsbG8gd29ybGQ=");
```

- Java 8'de

daha esnekleştirilerek birçok base64 destekleyecek şekilde yeni embeded kütüphane gelmiştir. direk örnek üzerinden incelersek:

```java
Base64.Encoder enc = java.util.Base64.getEncoder(); // standart base64

Base64.Encoder encURL = Base64.getUrlEncoder(); // url safe base64. RFC4648 ile aynıdır. Ek olarak url safe karakterler yapar. Bunun resmi bir RFC standardını bulamadım. Java kendi içinde böyle bir implementasyon yapmış. standart base64 ile aynı çıktıyı üretir. tek farkı şudur '+' yerine '-', '/' yerine '_' kullanır.

Base64.Encoder mimeEncoder = Base64.getMimeEncoder(); // mime base64

enc.encode(data.getBytes()); //ile encoding yapılıyor.
```

# hash algoritmaları (or özet fonksiyonları)
hash türkçe anlamı: bir malzemenin işlemden geçirilerek yeniden sunulan malzeme anlamına gelir. örneğin; kıyılan etin tekrar sunulması gibi.

- çıktı ile, girdiyi bulmak mümkün diildir. yani algoritma tek yönlü çalışır. şifreleme algoritmalarında ise bunun tersi şeklinde; çıktıdan girdiyi (bir anahtar aracılığı ile) elde edebilirsiniz.

- tüm hash algoritmaları gibi; birden fazla girdi, aynı çıktıyı üretebilir. aynı büyüklükteki string'ler bile, aynı hash sonucunu verebilir. çünkü her 1 girdi'ye karşılık, 1 çıktı olması şart olduğundan, birden fazla girdi aynı çıktıyı vermek zorunda kalacaktır. bu duruma __collision (or çatışma or çarpışma)__ denir.

# non-cryptographic hash function
hash'leme işlemleri genelde geriye çözülememesi amacı ile yapılır. Örneğin şifreler hash'lenir. Fakat bazı hash'ler vardır ki, geriye dönülememesi amaçlanmaz. farklı amaçları vardır. örneğin hash çıktısının boyutu sabit olsun, bizde bir string'in referansını bir yerde primary key olarak kullanmak isteyelim. o zaman primary key2in size'ını hash boyutuna fix'leriz ve primary key'i hash olarak tutarız. bu tarz hash algoritmalarına "non-cryptographic hash" denir.

geriye dönülememezlik özelliğinden feragat ettiğimiz için başka özelliklerden kazanırız. örneğin; performans gibi...

örnek; cassandra arkaplanda primary key'leri non-cryptographic hash kullanarak saklar.

"__Murmur__"; non-cryptographic hash algoritma ailesidir. birçok farklı türevi ve versiyonu vardır.

# cryptographic hash functions
- elektronik cihazlar güçlendikçe ve maliyeti düştükçe brute force attak yapmanın maliyeti ve hızıda düşmektedir.
- son kullanıcılar genelde belli keleimleri birleştirerek şifre oluşturabilmektedirler. bu durumlara karşı sözlüklerdeki kelimleer üzerinden kombinasyonlar ile hash'leri deneyen brute force yazılımları mevcut.
- her string'in hash karşılığının tutulduğu veritabanları mevcut. bu veritabanlarından baist bir sql sorugu ile hash karşılığı bulunabilir.

yukarıdaki sebeplerden şifreler mutlaka güçlü hash metodları ile hash'lenmelidir.

örnek: SHA256, SHA512, RipeMD, WHIRLPOOL

# Salt
kelime anlamı: tuz

- hash'leme algoritmaları ne kadar güçlü olsa da güvenliği arttırma amaçlı hash'lemeden önce her şifrenin sonuna bir string eklemeliyiz. bu string'e salt denir. bu şekilde veritabanımızın ele geçirilmesi durumunda şifreler açık şekilde bulunamamış olacak.
- md5 ve sha1 salt olsa bile güvensiz olarak kabul edilmektedir.
- Salt'ın çok gizli tutulmasına çok takılmamak gerekli. 
- Salt her şifre için ayrı üretilmelidir ve salt üretimi için "Cryptographically Secure Pseudo-Random Number Generator"lar kullanılmalıdır.

şifrelerin bunlarla üretilmesi önerilir: Argon2, bcrypt, scrypt, PBKDF2

# Kerckhoffs's principle (or Kerckhoffs ilkesi)
"principle" in title can be refered also as: desideratum, assumption, axiom, doctrine, law

başlıktaki "ilke" bunlarla da kullanılmaktadır: sanı, aksiyom, yasa

Kerckhoffs ilkesi şunu der: bir kriptosistem, anahtar hariç, sistemle ilgili her şey bilinse bile güvenli olmalıdır.

# key stretching (or anahtar germe)
anahtar üretimin zamanını arttırarak brute-force atakların önüne geçilebilir.

bunun için ideal algoritmalar: PBKDF2, bcrypt

Bu konu sanal paralardaki ASIC olayı ile benzerdir ("Equihash" başlığı). bu kaynakta: (source-id: 295) bu tarz algoritmalar "CPU-intensive hash function" olarak nitelendirilmiş. Bu URL, "Sam Newman" "Building microservices" kitabında 180inmci sayafdaki "Go with the Well Known" başlığında, 3üncü paragrafta önerilmiştir.

# hash table (or hash map)
bir çeşit veri yapısıdır. bir tablo düşünelim. her satırı bir dizi'de tutmak yerine, her satırın primary değerleri ile hash'ini alıp, hash'ini index olarak kullanabliriz.

Java'da "java.util.Hashtable" sınıfı thread-safe'dir, "java.util.HashMap" ise diildir.

hash table'larda arama işlemi çok hızlıdır. listeye bir data eklemek array'e göre daha uzundur çünkü hash alma işlemi gerektirir. işte bu durumlarda non-cryptographic hash kullanmakta yarar var. çünü performanstan kazanç sağlayabiliriz. zira burada key gizli bir bilgi değildir.

Hash table'larda iki değerin hash'i aynı olduğunda (çarpışma or collision), hash değeri artık index/key gibi kullanılamiyor. bu noktada çözüm için birçok farklı yöntem mevcut. bazı hash-table implementasyonları hash'e denk gelen "Value" değerini linked-List yapıp, komple bu linkedlist'i hash'in value'su olarak set ediyor. okurkende bunları parse ediyor. 

# hash kodları (or hash toplamları (or hash sums) or Hash digest (or hash özeti))
hash fonksiyonlarından dönen değerlere (çıktı değerine) denir.

# merkle tree (or Hash tree)
özel bir tree veri yapısıdır. ağacın her yaprağı altındaki ona bağlı yaprakların hash'ini tutmaktadır. en üstteki ağacın kök yaprağına da "hash sum" adı verilir.

# kontrol toplamları (or checksums)
dosyaların doğrulunu kontrol etmek istediğimizde yine "hash sums" değerine bakarız. fakat son kullanıcı açısından "hash sums" ile checksums farklı isimlendirilmiştir. oysa teknik anlamda aynı şeydir. 

# Blok Şifreleme (or Block Cipher)
blok şifreleme kullanan algoritmalarda, şifrelenecek tüm mesaj 'block size' kadar bölünür. her bölünen parça ayrı ayrı şifrelenerek şifrelenmiş halleri birleştirilir.

Blok şifreleme kullanan birçok algortima vardır. Fakat her blok şifrelemeninde birçok türevi/uzantısı vardır. Bunlar "__çalışma kipi (or mode of operation)__" olarak ta adlandırılırlar. örnek çalışma kipleri:

- # Elektronik kod defteri (or Electronic Codebook or ECB)
  blok şifrelemenin en basitidir. Her blok bağımsızca şifrelenir ve sonrada yanyana dizilerek birleştirilir.

- # Şifre Blok Zincirlemesi (or Cipher Block Chaining or CBC)
  her blok bağımsız şifrelenir fakat ek olarak her blok; bir önceki blokun şifrelenmiş halini ile XOR'lanır ve daha sonra şifrelenir.
  
  İlk bloğun öncesinde hiçbir blok olmadığı için, ilk blok manuel olarak verilecek "Initialization Vector" ile işleme tabi tutulur.

  bu modun dezavantajı cpu'nun paralele şekilde çözümleme yapamaması ve bu sebeple yavaş çalışmasıdır.

- # Yayılımlı Şifre Blok Zincirlemesi (or Propagating Cipher Block Chaining or PCBC or plaintext cipher-block chaining)
  CBC ile aynı mantıktadır. CBC; sadece bir önceki bloğun şifreli halini kullanırken, PCBC buna ek olarak; bir önceki bloğun açık halinden (şifrelenmemiş halinden) de yararlanır.

- # Şifre Geri Beslemeli (or Cipher FeedBack or CFB)
- # Çıktı Geri Beslemeli (or Output FeedBack or OFB)
- # Sayıcı Şekli Şifreleme (or Counter Mode Encryption or CTR)
  Bazı kaynaklarda sadece 'CTR mode'un kısaltması olduğundan "__CM__" olarak da kullanılmaktadır. Bazı kaynaklarda ise; "__integer counter mode (or ICM) and segmented integer counter (or SIC)__" olarak kullanılır.

# ilklendirme vektörü (or starting variable or SV or Initialization Vector or IV or İV or ilklendirme değişkeni)
Eğer her şifreleme işleminde IV kullanılmazsa, CBC tabanlı algoritmalarının yapısı gereği, aynı veri şifrelendiğinde, şifrelenmiş verinin ilk bloğu aynı çıktıyı verir. kaynak: (source-id: 296) "IV – the bit twister" başlığı.

örnek:

openssl komutu ile bir mesajı şifreleyelim:

```sh
$ openssl enc -aes128 -k secretpassword -a -p -nosalt -iv 00
key=2034F6E32958647FDFF75D265B455EBF
Hello Mr Warrender, I have some terrible news

VVklkPrL5fczxmu4vZ93BnfBBpU8BWK1IQhHF6JRKSNZJ7PvpcaE8K/Mkbx1xgHa
```

```sh
openssl enc -aes128 -k secretpassword -a -p -nosalt -iv 00
key=2034F6E32958647FDFF75D265B455EBF
Hello Mr Warrender, This is good news

VVklkPrL5fczxmu4vZ93BkAsVA64MLd5uah+zTVzr0XlOONVgDEd7ZunyIIzhpAo
```

Farklı bir IV kullanırsam, ilk bloğu farklı bir çıktı alırım:

```sh
openssl enc -aes256 -k secretpassword -a -p -nosalt
key=2034F6E32958647FDFF75D265B455EBF40C80E6D597092B3A802B3E5863F878C
iv =AD0ACC568C88C116D57B273D98FB92C0
Hello Mr Warrender, This is good news 
 
9/0FGE21YYBl8NvlCp1Ft8j1V7BiIpCIlNa/zbYwL5LWyemd/7QEu0tkVz9/f0JG
```

CBC tabanlı algoritmalarının yapısı gereği IV elimizde yok ise, key ile sadece ilk bloğu (mesajın ilk kısmını açamayız). Diğer kısımları açabiliriz. kaynak: kaynak: (source-id: 296) "Wait… The IV is not a key!" başlığı.

# MD (Message-Digest)
bir çeşit hash algoritmasıdır.

- md2
- md4
- md5: 128 bitlik bir çıktı verir. piyasada en sık kullanılandır.
- md6

# SHA (or Secure Hash Algorithm)
bir çeşit hash algoritmasıdır.

- sha (or sha-0) - 160 bit (40 karakter) lik hash (çıktı) üretir.

- sha-1 - 160 bit (40 karakter) lik hash (çıktı) üretir.

- sha-2 - altında bir çok şifreleme barındırır. her şifreleme ürettiği hash'in boyutuna göre isimlendirirlir. örnek:

   - 256'lık çıktı veren algoritma birçok isimde gösterilir: SHA-256 (or SHA 256 or SHA256 or SHA-256 bit or SHA2 256 or SHA-2 256 bit)

   - SHA-224, SHA-384, SHA-512 gibi birçok örnek verilebilir.

   - Sayı ne kadar yüksekse o kadar güvenlik arttırılmış olur, çünkü kırılması o kadar zordur. çünkü; kombinasyonlar çok daha fazla olmaktadır.

- sha-3

  sha2 gibi altında birçok şifreleme barındırır. sh2 gibi aynı şekilde; her şifreleme ürettiği hash'in boyutuna göre isimlendirirlir.

  sha3, sha2 ile aynı boyutta hash çıktı boyutlarını destekler. sha3, sh2'den daha sonra çıktığından bu şekilde isimlendirmeler mevcuttur:

  - SHA-224 --> sha-2 224 bit
  - SHA3-224 ---> sha-3 224 bit

# Neden hala SHA-512 yerine SHA-256 kullanılması öneriliyor?
Teorikte SHA-512 kullanılması önerilir. fakat pratikte 256'yı çözecek bir kudret olmadığından, 256 şu sebeplerden tercih ediliyor:

- 512'nin daha çok networkte bandwidth (or bant genişliği), memory, cpu vb harcıyor olması

- 256'nın yazılımlar tarafından daha çok desteklendiği için (eski olduğu için) daha az bug'lı olması

# çığ etkisi (or avalanche effect)
X string'in hash'i Y olsun. X stringinin bir karakterini değiştirdiğimizde ve tekrar hash aldığımızda Y ye benzer bir sonuc bekleriz, fakat çok farklı bir sonuc alırız. hash algoritmaları bunu bilerek yaparlar ki, değişiklikler daha belirgin olsun. buna çığ etkisi ismi verilmiştir.

# end-to-end encryption (or E2EE)
arada farklı aracı makineler olsada şifrelenmiş data taşındığından ve sadece gönderen ve alıcının çözebildiği şifreleme sistemleridir.

# ssl sertifikları ile web sayfaları ilişkisi

- ## sertifika (or certificate)
public key + ilgili kurum bilgileri

- ## ssl (secure socket layer)
soket üzerinden sertifika ile şifreleyerek data alışverişi yapan sanal katmandır.

tarayıcı üzerinden bir internet sitesine gittiğimiz zaman, public key'i site bize gönderir. artık yaptığımız her işlem (ajax işlemi) bu public key ile şifrelenerek gönderilir. artık bu bilgileri sadece private anahtara sahip internet sitesi açabilecektir.

- ## CA (or Certification Authority or sertifika otoritesi)
Sertifika vermeye yetkisi olan kurum. bu kurumun kendi sertifikasına "root" (kök) sertifikası denir. Pazarı yüksek olan bazı firmalar: IdenTrust, Sectigo, DigiCert, GoDaddy, Globalsign, Verisign. 

internet siteleri ssl sertifikalarını aracı kurumlara onaylatırlar. süreç bu şekildedir:
- web sunucu kendi public key (__SITE_PUB__) + private key'ini (__SITE_PRV__) localde oluşturur.
- public key'i CA'ya yollar.
- CA kendi private key'i (__CA_PRV__) ile __SITE_PUB__'nin hash'ini şifreyip yeni anahtar oluşturur (__X__).
- CA, __X__'i web sunucusu yetkililerine yollar.

Kullanıcı bir web sitesini ziyaret ettiğinde;
- web tarayıcısında CA'in public key'leri (__CA_PUB__) zaten yüklü olmalıdır.
- browser web sunucusundan ziyaret ettiği sitenin public key'ini (__X__) indirir.
- browser __CA_PUB__ ile __X__'i açar. __X__ kendi içinde domain ve ip bilgisi tutmaktadır. bu sebeple tarayıcı gittiği sitenin doğru olup olmadığını anlar.
- browser o anda simetrik şifreleme için bir anahtar yaratır (__S__). __S__ i tarayıcı sunucuya public key (__SITE_PUB__) ile şifreleyip yollar.
- Artık browser sunucuya bir istek yolladığında sadece __S__ şifrelenecektir. yani artık public/private keylere ihtiyaç yoktur. 

Web tarayıcıları __S__ değerini son kullanıcıya dahi vermiyor. Handhsake sırasında yaratılan ve simetrik haberleşmede kullanılacak olan __S__ public key (__SITE_PUB__) ile şifrelendiğinden ve sadece sunucu tarafından açıldığı için, bir hacker tüm akışı baştan sona takip edebilse bile, hiçbir şey yapamayacaktır.

__S__, değeri olmadan public key üzerinden de haberleşilebilir. fakat bu şekilde "kusursuz ileri güvenlik" sağlanmış oluyor (bu konu başka başlıkta alatılıyor).

TLS 1.2 için yukarıdaki adımları daha detaylı inceleyecek olursak:

  - client "__client hello__" (tam olarak bu string kullanılıyor) tipindeki mesajı ile handshake isteği yollar. bu mesajda:
    - client'ın kabul ettiği cipher'lerin listesi de mevcuttur.
    - session id: önceden varsa bu değer doludur. eğer bu değeri sunucuda onaylarsa tekrar handshake yapılmasına gerek kalmaz.
    - tls version
    - random bytes
    - extensions: extra değerler burada yollanır. örneğin opsiyonel kullnılan "session ticket" özelliği bilgileri burada yollanır.

  - server ise response olarak "__server hello__" tipinde mesaj döner.

  - buradan sonra server sertifikasını yollar ve client sunucu sertifikasını kendi içinde valide eder.

  - daha sonra "__Key Exchange__" adımına gelinir. burada kullanılabilecek bazı yöntemler şunlardır:
    - TLS_RSA
    - Diffie-Hellman (TLS_DH)
    - ephemeral Diffie-Hellman (TLS_DHE) (Ephemeral kelime anlamı: fani, kısa ömürlü)
    - Elliptic Curve Diffie-Hellman (TLS_ECDH)
    - ephemeral Elliptic Curve Diffie-Hellman (TLS_ECDHE)
    - anonymous Diffie-Hellman (TLS_DH_anon)

    Not: Diffie-Hellman algoritması başka başlıkta anlatılmaktadır.

    Bu adımda __S__ anahtarı oluşturulur. Nasıl oluşturulacağı burada belirtilen algoritmaya bağlıdır.

    Bu akışta kullanılan bazı terimler:

    - ## pre master key
        web tarayıcısnın kendi içinde oluşturduğu random key (__BS__)

    - ## master secret
        Web tarayıcısı handshake sırasında bir random bilgi, sunucuda dönüşünde bir random key yollar. bu 2 data ve __BS__ kullanılarak "master secret" (__S__) oluşturulur.

  - daha sonra "Server Hello Done" mesajı sunucudan client'a iletilir.

https ile haberleşildiğinde tüm http mesajı şifrelenir. header yada farklı bir bilgi açık bırakılmaz. url path'leri ve query variable'ları dahi şifrelenir. fakat neredeyse tüm web servisleri şifrelenmesi gereken datalar olduğunda hiçbir zaman GET isteği ile query parametrelerinde o datalar yollanmaz. onun yerine POST payloadında yollanır. aslında ikiside aynı kapıya çıkar. fakat GET isteği ile atılan istekler, hem web tarayıcısınının history'sinde, hemde server tarafının access log'larında görülür. bu sebeple post tercih edilir.

web sitenin anlaştığı sertifika firmasının web tarayıcılarla anlaşmış olması gerekmektedir. aksi durumda sertifika kırmızı uyarı verir. kırmızı uyarı sertifika var, fakat CA'lara tanıtılmamış anlamına gelir.

Bazı çakışmalar/uyuşmazlıklar:
- farklı web tarayıcıları farklı sertifika sağlayıcılarla anlaşabilir.
- aynı web tarayıcısı mobil versiyonu ile masaüstü versiyonunda aynı sertifika firmalarının bilgilerini bulundurmayabilir.
- aynı tarayıcı farklı versiyonlarında farklı sertifika sağlayacıyıcılarının bilgilerini bulundurabilir. 
- aynı tarayıcı farklı versiyonlarda aynı CA'leri bulundurur fakat farklı sertifikalarını  (farklı sürümlerini) bulundurabilir

bu tarz durumlar yaşamamak için her zaman globalsign, Verisign gibi gibi çok terhcih edilen firmalardan sertifika almakta fayda vardır.

sertifika çeşitlerine göre; web tarayıcısında logo, firma ismi vs gösterilme durumları vardır.

- ## Session ID
web sunucuna ilk istek atılacağı zaman client varsa eski Session ID'lerden devam edebilir. eğer önceden açılmış bir Session ID yoksa bu bilgi null gönderilir. session id var oldukça handshake'e gerek kalmaz.

- ## SessionTicket
session id'den farklı bir özelliktir. TLS extension olarak kullanılır. yani ekstra bir özelliktir. RFC buradadır: (source-id: 447)

- ## self sign key

public ve private key herhangi bir tool ile anında oluşturulabilir. bu anahtarlarda siteye gömülüp kulanılabilir. fakat web tarayıcısı kırmızı uyarı verecektir.

self sign aracılığı ile yapılan bağlantıların dışarıdan çözümlenme gibi bir durum söz konusu olamaz. aynı durum CA'e onaylatılan sertifikalar içinde geçerlidir.

self sign imza kullanırken şifre anahtarlarının boyutu arttırılarak güvenlik seviyesi çok rahat şekilde arttırılabilir. fakat dosya paylaşımı gibi uzun data işlemi gerektiren işlemlerde, anahtar boyutu sebebi ile şifreleme ve açma işlemleri cpu'ya yük bindirebilir.

- ## Intermediate CA
CA'lere 3üncü parti kuruluşlarda aracılık yapabilir. bu sebeple web tarayıcılarımızın "certificates" sekemlerinde içiçe sertifikalar görürüz.

- ## End Entity Certificate
son kullanıcıya ziyaret ettiği site aracılığı ile yollanan public key'dir.

- ## Certificate Signing Request (or CSR)
CA'ya müşterisinin (yani web sunucusunun sahibinin) yaptığı sertifika imzalatma isteğidir.

- ## Subject Alternative Name
firefox sayfa ayarlarında web sitenin sertifika özelliklerini incelendiğimizde bu alanı görürürüz. bazı sertifikalar birden fazla domain için kullanılabiliyor. bu gibi durumlarda izin verilen domain listesi bu değerin içerisinde yazmaktadır.

- ## sayısal imza
Gönderici ---> Mesajı gönderen kişi, mesajı kendi private key'i ile şifreler. Mesajın yanına public key'ini de yerleştirir. alıcı taraf public key'i kullanarak private ile şifrelenmiş mesajı çözer. bu şekilde 2 şey kanıtlanmış olur:

  - verinin nereden geldiği kesinleşmiş olur. public key ile açtığımız veri ancak private ile şifrelenmiş olabilir. dolayısı ile private'ye sahip olan kişi, bizim iletişimde olduğumuz kişidir.

  - verinin bütünlüğü korunmuş olur. çünkü asıl mesaj şifrelenmeden önce hash değeri hesaplanıp, hash değeri şifrelenmeden önce mesajın sonuna koyuluyor. asıl mesajı açan alıcı, tekrar bir hash işlemi gerçekleştiriyor. hash sonucu çıkan sonuç mesajın sonunda olan hash değeri ile aynı olup olmadığına bakıyor.

- ## "servers" tab on firefox certificate manager
self-sign imzalı bir web sitesine firefox üzerinden gittiğimizde firefox exception fırlatır. eğer son kullanıcı add exception'a tıklarsa o sertifika bu listeye eklenir. 

- ## wildcard certificate
wildcard türkçe kelime anlamı: joker

her subdomain (a.google.com, b.google.com gibi) için ayrı sertifika alınması gerekir. fakat wildcard sertifikalar tüm subdomain'leri desteklemektedir.

## Java KeyStore (or JKS) 
private ve public key'lerin, sertifikaların bir arada tutulabildiği dosyaya Java dünyasında verilen isimdir. keystore bir format değildir, bir java sınıfıdır:

> KeyStore store = KeyStore.getInstance("PKCS12");

__keytool__ komut satırı uygulaması keystore dosyaları üzerinde değişiklik yapmamıza olanak sağlıyor. tabi tüm keystore dosya formatları bu uygulama tarafından desteklenmiyor.

JKS gibi içinde certifika, key saklanan dosyalara yazılım dünyasında __keyring__ denir.

# TrustStore
içerisinde CA'ların sertifikaları bulunduran doayalara java dünyasında verilen isimdir. TrustStore bu dosyayı temsil eden sınıfın ismidir.

# Keychain
macOS'larda yüklü gelen GUI desteği olan key manager uygulamasıdır.

# X.509
Standartlaşmış digital bir sertifika formatıdır. Sertifika formatı dahilinde; sertifika imzalama algoritması, sertifika public key'i, versiyon, algoritma ID, seri numarası, konu, geçerlilik süresi gibi bilgiler barındırır.

# X.509 kullanan sertifika uzantıları

.pem

.cer, .crt, .der

.p7b, .p7c (PKCS#7)

.p12 (PKCS#12)

.pfx

# PKCS 
"RSA Security" kuruluşu tarafından yayımlanan "public-key cryptography standards"'ın kısaltmasıdır. yayımlanan bu güvenlik standartları ailesidir. 

15 adet standart içerir (yıl 2019). her sürüm farklı bir dosya formatı tanımlamaktadır.

```
ismi       version
PKCS #1    2.2
PKCS #3    1.4
PKCS #7    1.5
```

Tüm sürümler farklı zamanlarda çıkarılmıştır. Fakat sırası ile çıkmamıştır. Bu sebeple yeni sürümler daha iyi olarak düşünülmemelidir. dikkat edilirse PKCS sürümü ile isminde bulunan numara aynı değil.

# http'den https'e yönlendirme
http ile gidilen site dönüş değerinde https'e yönlendirme isteğinda bulunur. web tarayıcıda kullanıcyı https'e yönlendirir. eğer arada trafiğimizi izleyip manipüle eden birileri varsa, bu isteğin cevabında https'e yönlendirme yapmaz. normal http sitenin get isteğinin cevabını döndürür. artık son kullanıcı http ile iletişime devam edeceği için tüm iletişim baştan sona izlenebilir.

# "https everywhere" vs "smart https"
Web tarayıcı eklentileridir. Smart; her url'yi sorgulamadan https'e çevirir. Eğer herhangi bir cevap gelirse siteye gider, yoksa http olana gider. Fakat "https everywhere" her site için önceden ruleset tutar ve aşağıdaki gibi gelişmiş yönlendirmelerde yapabilir.

```
http://fr.wikipedia.org/wiki/Chose

https://secure.wikimedia.org/wikipedia/fr/wiki/Chose
```

# HSTS (or HTTP Strict Transport Security)
Kullanıcyı http'den https'e yönlendirildiğinde sunucu bu header'ı döner:

> Strict-Transport-Security: max-age=16070400; includeSubDomains

max-age süresinde tarayıcı son kullanıcı http'ye gitmek istese bile https'e otomatik yönlendirecektir.

# Preloaded HSTS sites
HSTS için bir kere olsun siteye gitmek gerekiyor. bunu da yapmaya gerek kalmaması için tüm web tarayıcıların ortak tuttuğu bir liste var:

https://cs.chromium.org/chromium/src/net/http/transport_security_state_static.json

dosya içeriği çok büyük. bir kısmı:

```json
{ "name": "qualitymudjacking.com", "policy": "bulk-1-year", "mode": "force-https", "include_subdomains": true },
{ "name": "qualitypiering.com", "policy": "bulk-1-year", "mode": "force-https", "include_subdomains": true },
{ "name": "qualitypolyjacking.com", "policy": "bulk-1-year", "mode": "force-https", "include_subdomains": true },
{ "name": "qualitywaterproofingco.com", "policy": "bulk-1-year", "mode": "force-https", "include_subdomains": true },
{ "name": "quanquan.space", "policy": "bulk-1-year", "mode": "force-https", "include_subdomains": true },
{ "name": "qulixqa.com", "policy": "bulk-1-year", "mode": "force-https", "include_subdomains": true },
```

Bu listeye kadolmaz ücretsiz. bu bilgileri web tarayıcıları sürekli localde güncel tutuyor ve bu listedeki sitelere gitmek isteyen kullanıcıları direk https'e yönelndiriyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Diffie-Hellman key exchange
known also as:
- Diffie–Hellman key agreement
- Diffie–Hellman key establishment
- Diffie–Hellman key negotiation
- Exponential key exchange
- Diffie–Hellman protocol
- Diffie–Hellman handshake
- Diffie–Hellman-Merkle *(all combinations above)

Whitfield Diffie and Martin Hellman invented this algorithm.

Ralph Merkle is one of the inventor of asymmetric cryptography. Diffie-Hellman is one of the earliest practical examples of public key exchange implemented within the field of cryptography. therefor Diffie–Hellman known as "Diffie–Hellman-Merkle".

We use key exchange to generate a key (using a not secure connection) which is known only by communicator but not by middle attackers.

Let assume that Alice and Bob will communicate. They are in key exchange phase. There are many different alternatives for this phase. On this topic we will explain the Diffie-Hellman key exchange algorith.

"Eve" is the name of the middle listener/hacker.

g and p are genated randomly and publicly by alice and bob.

- g = public (prime) base, known to Alice, Bob, and Eve. g = 5
- p = public (prime) modulus, known to Alice, Bob, and Eve. p = 23
- a = Alice's private key, known only to Alice. a = 6
- b = Bob's private key known only to Bob. b = 15
- A = Alice's public key, known to Alice, Bob, and Eve. A = ga mod p = 8
- B = Bob's public key, known to Alice, Bob, and Eve. B = gb mod p = 19

"mod" is the modulo operation in math.

| Alice  Known       | Alice unknown | Bob  Known          | Bob Unknown | Eve  Known    | Eve Unknown |
|--------------------|---------------|---------------------|-------------|---------------|-------------|
| p = 23             |               | p = 23              |             | p = 23        |             |
| g = 5              |               | g = 5               |             | g = 5         |             |
| a = 6              | b             | b = 15              | a           |               | a, b        |
| A = 5a mod 23      |               | B = 5b mod 23       |             |               |             |
| A = 56 mod 23 = 8  |               | B = 515 mod 23 = 19 |             |               |             |
| B = 19             |               | A = 8               |             | A = 8, B = 19 |             |
| s = Ba mod 23      |               | s = Ab mod 23       |             |               |             |
| s = 196 mod 23 = 2 |               | s = 815 mod 23 = 2  |             |               | s           |

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# ileri güvenlik (or kusursuz ileri güvenlik or forward secrecy or FS or perfect forward secrecy or PFS)
şifrelenmiş bir iletişimde, her oturum açıldığında veya aynı oturumun farklı zaman aralıklarında rastgele bir ek anahtar ile oturum ek olarak şifrelenir. bu şekilde, ana anahtarımız çalınsa bile, geriye dönük data'lar açılamayacaktır. burada 2 husus söz konusudur: her otorumda (veya belli aralıklarda) yeni oturum anahtarı kullanımı + her oluşturulan yeni oturum anahtarının bir önceki ile ilişkisel olmaması.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Rassal değişken (or Random variable)
rastgele oluşturulan değişkendir.

# sözde rastsal (or pseudo random number)
bilgisayar ortamında rastgele değişken oluşturulamayacığından, sözde rastsal sayılar oluşturulabilmektedir.

# pseudorandom number generator (or eng-kısaltma:PRNG or deterministic random bit generator or eng-kısaltma:DRBG)
sözde rastsal sayı üretebilmek için kullanılan yazılımlardır.

PRNG initiali value'ya bakar. initial value aynı olursa sürekli aynı çıktıları üretir.

bahsi geçen bu initial value'ya __seed (or tohum)__ denir.

# tr:entropi (or eng:entropy)
kelime anlamı:

1- fizikte; Bir sistemdeki rastgelelik ve düzensizlik.
2- fizikte; Bir sistemin işe çevrilemeyecek enerjisi, kullanılmayan enerji miktarı.
3- istatistik biliminde; bir haber kaynağının haber içeriklerinin oranı.

# Hardware random number generator (or eng-kısaltma:HRNG or true random number generators)
donanımlar aracılığı ile rastgele sayı üretilememektedir (yazılımda olduğu gibi). fakat donanımlar bazı sensörler ile çevreden bilgi alıp rastgele sayı üretmeye çalışabilirler. örneğin; ısı sensörü gibi. aslında burada da %100 rastgele sayı üretilmiş olmuyor. fakat önceden kestirilemeyen (unpredictability) sayı üretiliyor.

bilgisyarlar rastglele sayı üretebilmek için, her cihazda olan aşağıdaki 2 referanstan yararlanır. Her donanımda olduklarından portable algoritmalar için tercih edilirler.
- saat-tarih
- CPU çalışmaya başladığından itibaren kaç cycle geçmiş gösteren __Clock Sequence__

# cryptographically secure pseudorandom number generator (or CSPRNG or cryptographic pseudorandom number generator or CPRNG)
%100 olmasada belli standartları destekleyen güçlü seviyede random sayı üreten kütüphaneler mevcut. bunlara verilen özel isimdir. örnekler:

| Platform                               | CSPRNG                                                |
|----------------------------------------|-------------------------------------------------------|
| PHP                                    | mcrypt_create_iv, openssl_random_pseudo_bytes         |
| Java                                   | java.security.SecureRandom                            |
| Dot NET (C#, VB)                       | System.Security.Cryptography.RNGCryptoServiceProvider |
| Ruby                                   | SecureRandom                                          |
| Python                                 | os.urandom                                            |
| Perl                                   | Math::Random::Secure                                  |
| C/C++ (Windows API)                    | CryptGenRandom                                        |
| Any language on GNU/Linux or Unix	Read | from /dev/random or /dev/urandom                      |

Bu tablodaki listede bulunan algoritmalar ek olarak donanımlardan da yararlanmaktadır. CPRNG'ın donanımdan yararlanması zorunlu diildir. Donanımdan yararlanmayan CPRNG'lar da mevcut. Yukarıdaki listedeki kütüphaneler, donanımdan aldıkları rastglele verileri CPRNG'a initial değer olarak verirler ve çıktı üretirler. Yukarıdaki API'ler genelde OS'un sunduğu API'lerden yararlanır. OS'ların sunduğu API'ler, kaynaklardan (donanımlarda oluşan event'lerden) bilgi toplarlar. Fakat bu bilgilerin zamana oranla üretimi kısıtlıdır (entropi düşüktür). Dolayısı ile belli zaman diliminde belli sayıda rastgele data üretilebilir. Daha sık üretilmesi için özel cihazlara (HSM gibi) başvurulmalıdır.

Her OS'ta aşağıdakilerin davranışları farklı olabilir.
- "/dev/random" entropi düşükken, isteği bloklar (bekletir). ne zamna yeni data doplanır o zaman cevabı döndürür.
- "/dev/urandom" ise, eğer entropi düşükse, eski data'ları kullanarak cevap döndürür.

/dev/random, TCP'de TLS/SSL tarafından da kullanılmaktadır. kaynak: (source-id: 298) 1inci paragraf.

# software based random number generators
bazı yazılımlar entropi üretmektedirler. OS'ların default entropi üreten modüller (yazılımları) çok basittir. Özellikle GUI'siz bir ortamda kullanılması pek önerilmez. kaynak: (source-id: 298) "Entropy Shortages" başlığı. 1inci paragraf.

Bu sebeple daha gelişmiş bazı yazılımlar kullanılır. Örnekler:
- haveged (özel isimdir. içerisinde "HAVAGE" isimli algoritmayı kullandığından "havaged" olarak isimlendirilmiştir. HAVAGE algoritması bunun kısaltmasından üretilmiştir: HArdware Volatile Entropy Gathering and Expansion).
- EGD (or Entropy Gathering Daemon)

# HAVAGE
HAVAGE algoritmasında, OS'un event'leri ve external event'ler HAVAGE generator'u sürekli reseed etmektedir. kaynak: (source-id: 300) "HArdware Volatile Entropy Gathering and Expansion:generating unpredictable random number at user level", yazarlar:André Seznec, Nicolas Sendrier, başlık: "6 havage: combining entropy/uncertainty gathering and pseudo-random number generation". 2inci paragraf, son cümle.

HAVAGE algoritması CPU'da kod işletiyor ve bu kodun CPU'daki state'ini sürekli inceleyip, bu state'lerden entropi üretiyor. kaynak: kaynak: (source-id: 298) "HAVEGE" başlığı, 1inci paragraf.

# rasgele sayı üretimi hakkında

- Teorik olarak; sadece, hiç input almadan rastgele sayı üretebilen bir platform ancak bize gerçekten rastgele sayı üretebilir.

- işletim sistemleri klavye ve mouse gibi bazı kaynaklardan yararlanarak rastgele sayı veren API sunarlar. örneğin posix'lerde: /dev/random'dan yararlanılır.

- random.org sitesi bir web servis üzerinden rastgele sayı servisi sağlıyor. bu servis hava durumundan yararlanıyor.

# UUID (or Universally unique identifier)

- (source-id: 302)'da belirtilen standartlardır. her versiyon hakkında bilgi yine bu standart altında belirtilmiştir. bu standartta 5 adet version belirtilmiştir. versiyonlama, olgunluk olarak belirlenmemiştir, sadece 5 çeşit UUID vardır. bunlar aşağıdaki gibidir:

  - version 1 (Time Based)

    cihazdaki MAC adresi ve data-time (en ufak birimi nanosecond olacak şekilde) bilgisi ile UUID üretir. aynı bilgilerle aynı UUID tekrar üretilebileceğinden bazı durumlarda takip edilebilirliği sağlamak amaçlı bu kullanılmaktadır.

    mac adresi olmayan durumlarda (cihazlarda/platformlarda) rastgele sayı kullanılabileceği RFC standartlarında belirtilmiştir.

  - version 2 (DCE Security)

  - version 3 (Name Based)

    UUID oluşturmak için namespace(url gibi) ve name'in MD5'i kullanılır. örnek kod:

    ```java
    String source = namespace + name;
    byte[] bytes = source.getBytes("UTF-8");
    UUID uuid = UUID.nameUUIDFromBytes(bytes);// bizim için MD5 hash alıyor
    ```

  - version 4 (Random)

    sistem random number generate ederken, önceden belirli datalardan yararlanmaz. bu sebeple genelde bu tercih edilir.

  - version 5 (Name Based)

    Version 3 ile aynı. tek fark: MD5 değil, SHA-1 istiyor.

- version

  most significant 4 bits of "time" block.

- variant

  UUID'nin ilk 2 bitidir.

  UUID'nin layout'udur. hangi bitlerde, hangi bilginin yer aldığı standartıdır.
  
  rfc4122'de sadece bir variant anlatılıyor.

  ("x" önemi olmayan bit anlamına geliyor)

  | bit-0 | bit-1 | bit-2 | explanation                                            |
  |-------|-------|-------|--------------------------------------------------------|
  | 0     | x     | x     | Reserved, NCS backward compatibility                   |
  | 1     | 0     | x     | rfc4122'de anlatılan formattır                         |
  | 1     | 1     | 0     | Reserved, Microsoft Corporation backward compatibility |
  | 1     | 1     | 1     | Reserved for future definition.                        |

  Leach-Salz (rfc4122 yazarlarının soyadları) UUID'nin 2'inci variantının (digit olarak bakıldığında varyant değeri "1") takma adı olarak her tarafta kullanılmaktadır.

- java code of version vs variant

  ```java
  UUID uuid = UUID.randomUUID();
  int variant = uuid.variant();
  int version = uuid.version();
  ```
  
- Tekil bir stringdir. 128 bit'tir.

- sayı çok büyük olduğundan aynı sayının aynı uygulama içinde üretilmesi matematiksel olarak çok azdır. bu sebeple standart olarak kullanılır.

- örnek kullanım alanlar:
  - MAC addresler
  - dosya sistemlerinde partition id'leri
  - db'lerde id'ler

- 36 karakterdir ve arada tire koyularak (tireler sadece notasyondur, 128 bite dahil değildir) 5 grup olarak gösterilir:
  > 123e4567-e89b-12d3-a456-426655440000
    
  her grup bir data'yı temsil eder:

  - time
  - version
  - clock_seq_hi
  - clock_seq_lo
  - node

- sadece küçük harf karakterler geçerlidir.

- Uniform Resource Name (or URN) gösterimi bu şekildedir:

  > urn:uuid:123e4567-e89b-12d3-a456-426655440000

- Nil UUID

  tümü sıfır olan UUID'dir.

# Globally unique identifier (or GUID)

Microsoftun UUID implementasyonudur. UUID'den hiçbir farkı yoktur. sadece variant değeri farklıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Open Web Application Security Project (or OWASP)
OWASP is an online community which creates freely-available articles, methodologies, documentation, tools, and technologies in the field of web application security.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Bot
Türkçe ismi de ‘bot''tur. Bazı kaynaklarda ‘robot' olarakta kullanılır. Otomatik işlem yapan yazılımlardır. örneğin; oyunlardaki bot'lar farklı yazılım modülleri (yazılımlardır).

# Internet bot
İnternet üzerinde otomatik işlem yapan yazılımlardır.

# Web crawler (or web spider)
Bir çeşit internet bot'udur. Sadece web sayfalarını dolaşan yazılımlardır. Bu dolaşma işlemi, sitelerin eski halalerini arşivlemek, siteleri arama motorları için indexlemek, bir siteyi tüm alt syafaları ile download etmek (bazı download manager'lar yapıyor) gibi birçok amaç için olabilir.

# Web scraper (or web harvesting or web data extraction or Web kazıma or web hasat or web veri çekimi)

HTML üzerinde verileri parse edip uygun verileri ayıklamak için gerekli yazılımdır. web crawler siteleri gezerken siteleri arkaplanda indirirler ardından, web scraper sitelerin içindeki bilgileri veritabanlarına uygun şekilde kaydeder.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# string vs char[] for passwords (on java)

şifreler programda string değil char[] tutulması önerilir. bunun birkaç sebebi var:

- program exception olup kapanırsa işletim sistemi variable'ların dump'ını bi yere atar. daha sonra birileri bunu okursa, string değeri okunabiliken, char[]'in değeri okunamaz. çünkü char[]'in toString()'i yoktur.

- char[]'in toString()'i olmadığından; biri yankışlıkla log atarsa log("" + password); ekranda şifre görülmeyecektir. biri direk şifreyi ekrana basmaz fakat obje içinde obje olduğunda bazen taşınma işlemlerinde yanlışlıkla log basılmış olabilir.

- Strings'ler immutable olduklarından referansları olmasa bile garbage collector temizleyene kadar ram'de tutulurlar. eğer uygulama hacklenirse ram'den okuma yapacak olan hacker bu değerleri görebilir. string ve char[], ram'den aynı şekilde okunur, fakat bu maddede bahsedilen, kullanıma ihityaç duyulmadığında, string'in memory'den silinmesinin zaman almasıdır. (kaynak: (source-id: 425))

Ek not:
- javax.swing kütüphanesinin JPasswordField sınıfı getText() metodu artık char[] dönüyor (eskiden string dönüyordu). bu sebepten böyle düzeltildi.

Ek not: 
- .net'te System.Security namespace'si altında SecureString isimli bir sınıf vardır. Bu sınıf aynı br string gibi davranmakta fakat işimiz bittiğinde bu sınıfı Dispose() (kelime anlamı: elden çıkarmak) metodu ile yokedebiliyoruz. Aynı zamanda, burada string memory'de şifrelenmiş olarak saklanmaktadır. şifreleme görevini .net ortamı'ı yapmaktadır.
