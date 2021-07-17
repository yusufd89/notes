############################

############################
# SECURITY JWT
############################

############################

# JSON Web Token (or JWT)
alternative pronunciation: "jot". kaynak: (source-id: 268) "The JWT Handbook", "Sebastián E. Peyrott", "Auth0 Inc.", Version 0.11.0, 2016-2017, title: "Chapter 1", sub-title: "Introduction".

Session yönetimlerinde giden token'ın (kullanıcı auth konusuyla ilgili giden gelen tüm bilgilerin) formatı ile ilgili özel bir standarttır. içinde ne gideceği ve nasıl doğrulanacağı hakkında standart içermez.

JWT iki standarttan birini implemente ederek kullanılabilir: kaynak: (source-id: 269) title: "7.2. Validating a JWT", madde 7.
- __JSON Web Signature (or JWS)__
- __JSON Web Encryption (or JWE)__

# JWS vs JWE
Aşağıdaki tüm açıklamalar için kaynak: kaynak: (source-id: 268) "The JWT Handbook", "Sebastián E. Peyrott", "Auth0 Inc.", Version 0.11.0, 2016-2017, title: "Chapter 5", sub-title: "JSON Web Encryption (JWE)", 1-4th paragraph.

JWS; data kısmını şifrelemiyor. Dolayısı ile JWS'de token herkes tarafından okunabiliyor. JWS, token'ın diğer bağımsız makinelerden valide edilebilmesini sağlıyor. Oysa JWE; token'ın third party'lerin okuyamamasını sağlıyor. çünkü data kısmını şifreliyor. Sadece secret'a sahip kişiler token'ın içini açabiliyor/okuyabiliyor.

JWS ve JWT iki farklı scheme ile yetki yönetimini sağlıyor:

- shared secret scheme

  tüm sistemde sadece tek bir secret key var.

  - JWS bu şekilde işletiyor:

    secret key'e sahip kişiler:
    - yeni token oluşturabiliyor (token'ı imzalayabiliyor)
    - varolan token'ı valide edebiliyor

    Dikkat edilirse böyle bir sistemde, client web browser ise, muhtemelen secret key'e sahip olmayacak ve token'ı valide edemeyecek. Fakat içindekileri görebilecek. (yani web browser imza kısmını doğrulayamayacak).

  - JWE bu şekilde işletiyor:

    secret key'e sahip kişiler:
    - yeni token oluşturabiliyor (encrypt edebiliyor)
    - varolan token'ı decrypt edebiliyor

- public/private-key scheme

  - JWS bu şekilde işletiyor:

    | sahip olunan key | token generade (token sign) | token decrypt | token validate |
    |------------------|-----------------------------|---------------|----------------|
    | private key      | true                        | ?             | true           |
    | public key       | false                       | ?             | true           |

  - JWE bu şekilde işletiyor:

    | sahip olunan key | token generade (token encrypt) | token decrypt | token validate |
    |------------------|--------------------------------|---------------|----------------|
    | private key      | true                           | true          | ?              |
    | public key       | true                           | false         | ?              |

    JWE kullanımı dikkat edilirse, web tarayıcılarındaki SSL çalışma mantığı ile aynı. Herkes (her tarayıcı) şifreleyebiliyor, fakat sadece tek bir server bunları açabiliyor.

Yukarıdaki tablolarda soru işaretleri, ilgili kısmın JWS veya JWE'nin ilgi alanı olmadığından kaynaklıdır. örnek "token validate", JWE'yi ilgilendiren bir konu diildir.

# JWE
İki şekilde serialize edilebilir: kaynak: (source-id: 271) title: "7. Serializations", all subtitles.

- JWE Compact Serialization

  ```
  BASE64URL(UTF8(JWE Protected Header)) || '.' ||
  BASE64URL(JWE Encrypted Key) || '.' ||
  BASE64URL(JWE Initialization Vector) || '.' ||
  BASE64URL(JWE Ciphertext) || '.' ||
  BASE64URL(JWE Authentication Tag)
  ```

- JWE JSON Serialization

  ```json
  {
  "protected":"<integrity-protected shared header contents>",
  "unprotected":<non-integrity-protected shared header contents>,
  "recipients":[
    {"header":<per-recipient unprotected header 1 contents>,
    "encrypted_key":"<encrypted key 1 contents>"},
    {"header":<per-recipient unprotected header N contents>,
    "encrypted_key":"<encrypted key N contents>"}],
  "aad":"<additional authenticated data contents>",
  "iv":"<initialization vector contents>",
  "ciphertext":"<ciphertext contents>",
  "tag":"<authentication tag contents>"
  }
  ```

# Unsecured JWT
algoritması "none" olan bir JWT token'ıdır. (Aynı zamanda algoritması none olan bir JWS'tir.)

# JWT yapısı
JWT üç temel kısımdan oluşur:

- ## jwt header
__Javascript Object Signing and Encryption (or JOSE)__'da denir. çünkü JWT; JWS standartlarındaki JOSE header'ını kullanır.

header'da aşağıdaki iki kısım standart'tır. ekstra isteğe bağlı field'lar eklenebilir.

```json
{
    "alg": "HS256", // (algorithm). Veri bütünlüğünü korumak için kullanılacak cryptotic algoritmayı belirtir.
    "typ": "JWT" ,// (type). sabit bir değerdir. farklı bir json objesi olup olmadığını ayır edebilmek için bu şekilde verilmiştir.

    // other custom fileds can be put here...
}
```

Bazı header property'leri önceden belirlenmiş durumda. listesi burada: (source-id: 272) title: "4.1. Registered Header Parameter Names" all subtitles. Bunlardan bazıları kısaca:

- alg (algorithm)
 
  JWS based JWT'lerde content'i şifrelemek için kullanılan algoritmanın adını içerir.

  JWE based JWT'lerde ise; content'i şifrelemek için kullanılacak key'i (__Content Encryption Key (or CEK)__) şifrelemek için kullanılacak algoritmanın adını tutar. kaynak: (source-id: 268) "The JWT Handbook", "Sebastián E. Peyrott", "Auth0 Inc.", Version 0.11.0, 2016-2017, title: "5.1.3 The Header".

- enc (Encryption Algorithm)

  Bu JWE standartından geliyor. (JWS'de bu yok.)

  content'i şifrelemk için kullanılan algoritmanın adını tutar. kaynak: (source-id: 268) "The JWT Handbook", "Sebastián E. Peyrott", "Auth0 Inc.", Version 0.11.0, 2016-2017, title: "5.1.3 The Header".

  Ek not: content, __Content Encryption Key (or CEK)__ ile şifrelenir. kaynak: (source-id: 268) "The JWT Handbook", "Sebastián E. Peyrott", "Auth0 Inc.", Version 0.11.0, 2016-2017, title: "5.1.3 The Header".

- zip

  compression algorithm

- jku (JWK Set URL)
- jwk (JSON Web Key)
- kid (Key ID)
- x5u (X.509 URL)
- x5c (X.509 Certificate Chain)
- x5t (X.509 Certificate SHA-1 Thumbprint)
- x5t#S256 (X.509 Certificate SHA-256 Thumbprint)
- typ (Type)
- cty (Content Type)
- crit (Critical)

- ## jwt payload (or jwt claims)
jwt payload içerisindeki her field'a __claim__ denir. "claim" terimi iddat etmekten gelmektedir. bu sebeple payload'a onun çoğul hali olan "claims"'te denir.

```json
{
    "userId": "3344552266",
    "expire": 1486220816,
    "roles": ["admin", "user"]
}
```

payload içerisinde ne olacağına JWT karışmaz. fakat standart olması (çakışma olmaması açısından) amaçlı bazı önceden belirlenmiş property'ler vardır. bunların bazıları: (source-id: 269) "4.1.  Registered Claim Names" başlığı.

Registred claim'lere "__public claims__" de de niliyor. bu durumda, kendi projemizde kullandığımız custom claim'ler "__Private Claims__" oluyor. kaynak: kaynak: (source-id: 268) "The JWT Handbook", "Sebastián E. Peyrott", "Auth0 Inc.", Version 0.11.0, 2016-2017, title: "3.2.2 Public and Private Claims".

| field | long name       | description                                                                 | example               |
|-------|-----------------|-----------------------------------------------------------------------------|-----------------------|
| iss   | Issuer          | principal generate the JWT                                                  | account.google.com    |
| sub   | Subject         | subject                                                                     | jack1321342@gmail.com |
| aud   | Audience        | this is an identifier of the service which which this token generated for   | mail.google.com       |
| exp   | Expiration Time | expire date-time of this jwt token                                          |                       |
| nbf   | Not Before      | date-time on which the JWT will start to be accepted for processing.        |                       |
| iat   | Issued at       | creation date-time of this jwt                                              |                       |
| jti   | JWT ID          | Case sensitive unique identifier of the token even among different issuers. |                       |

- ## jwt imza

bu kısım bu algoritma ile oluşturulur:

```java
String signatureOfJtw = base64(toHMACSHA256(urlBase64(headerJson) + "." + urlBase64(payloadJson), SECRET_KEY_OF_SERVER));

String jwt = urlBase64(headerJson) + "." 
           + urlBase64(payloadJson) + "."
           + signatureOfJtw; 
```

Dikkat edilirse; her kısım arasında . (nokta) vardır. Giden token url-base-64 encoded olduğundan yazılımcı bu token'ı URL'den de sunucuya atabilir. Dikkat edilirse veri bütünlüğü sağlandığı için sunucuda session ihtiyacı kalkar. Tüm bilgiler token içerisinde saklanabilir.

JWT token'ı url-base-64 encoded olduğundan; içeriği (json'lar) okunabilir ve client tarafından da değiştirilebilir. Fakat imza kısmındaki secret olmadığından (sadece serverda olduğundan), veri bütünlüğünü sağlayamaz ve token geçersiz sayılır.

Standartlarda olmasada genelde JWT http requestinin header kısmına şu şekilde skalanır: 

> Authorization: Bearer JWT_TOKEN_BURADA

# jwt token types

- access token: isteği yaptığımızda kontrol edilen jwt token'ı.

- refresh token:
  - kullanımı opsiyonel'dir.
  - bunun formatı da jwt'dir.
  - claims'ler, access token'ın claim'sleri ile aynı diildir.
  - access token'ın geçerlilik süresi çok kısa olmalıdır. refresh token'ınki ise ona göre uzun olmalıdır.
  - refresh token'lar sunucuda DB'de tutulmalıdır. (eğer hacker, refresh-token'ı çalarsa, ilgili refresh token'ı bloklamak için DB'de kayıtlı olmalıdır)
  - refresh token, access token'ı yenilemek için istek atıldığında kendisi yenilenmez. aynı kalır. eğer aynı kalmazsa refresh-token DB'miz şişer. Fakat uzun bir süre sonra refresh-token kendisini güncelleyebilir. Güncellenip güncellenmeyeceğinme sadece sunucu karar vermelidir. Bu güncelleme işlemi için bazen son kullanıcıdan OTP de istenebilir, yada istenmeyebilir (yada benzeri bir kullanıcı otorizasyonu istenebilir). Bu durum; bussinnes tarafından belirlenir. Eğer refrehs token yenilenmez ve refresh token'ın süresi biterse, o zamn artık son kullanıcının nroaml login akışını tekrarlaması gerekir.

  hacker acces token'ı çalarsa, access token'ın son kullanma tarihine kadar işlem yapabilir. bunu kimse engelleyemez. bu sebeple access token'ın süresi çok kısa tutulur. client, sıklıkla yada access token expire olduğunda, refresh token'ı sunucuya gönderir. reponse olarak sunucudan daha güncel bir access token ve refresh token cevabı alır.

  refresh token'ın 2 avantajı var:

  - bu işlem %100 bir güvenlik sağlamasada; access token çalınma durumunda ve refresh token'ın çalınmaması durumunda güvenliği sağlamaktadır. en azından hacker sadece acces token'ın süresi boyunca işlem yapabilecektir.

  - eğer refresh token çalınırsa, son kullanıcı refresh token'ı bloke etmesi için sunucuya bildirimde bulunabilir. refresh-token'ı çalışnmış kullanıcıyı genel olarak sistemden bloklama (örnek DB'den user'ı disable etme) pek verimli bir çözüm diil. Çünkü user'ı tekrar aktif ettiğimizde, hacker'ın aynı refresh token ile gelip gelmeyeceğini bilemeyiz. Fakat refresh token'ı iptal edersek, son kullanıcıya normal login süreci işleterek yeni refresh token verebiliriz. Böylece son kullanıcıyı hiç disable etmeden sistem hizmet vermeye devam edebilir olacaktır.

  not: refresh tokenlar sunucu tarafta tutulmaktadır. bu durum token-based'in mantığını bozmamaktadır. çünkü refresh token'lar bir databasede tutulabilirler. yani hızlı erişim belleğinde tutulma ihtiyacı yoktur. çünkü az sıklıkla erişilmektedirler. database'de olan bu tarz bilgiler 'state' statüsünde değillerdir.

# jwt dezanatajlar
- login olmuş user'ın role veya permission bilgileri jwt token'da olduğu için, login olmuş kullanıcnın rolü veya permission'u değiştirilirse direk aktif edilememektedir.
- servise jwt ile istek yaptık. serviste giden istek, diğer internal microservislere yönlenmektedir. 10 servise gitti ve her biri arasında 3'er saniye kaybetti. 30 saniye sürdü. eğer 20inci saniyede token expire olursa, bir sonraki mikroservis isteği geri atacak çünkü jwt token artık invalid olacaktır.

# jwt nerde saklanmalı
access token memory'de (JS'te), refresh token katı kurallarla cookie'de saklanmalıdır. refresh-token'dan access token üreten HTTP requestimiz sadece POST olmalı. Çünkü; Kötü niyetli siteden CSRF atak olursa:

- (auto medya loading olursa) GET olabilir

  Karşılığı olan refresh-token POST olacağı için hiçbir şey elde edemeyecek.

- (Eğer user tıklayıp form submit ettirilmesi başarılırsa) POST olabilir

  submit işlemi sonrası JS tarafı (ilgili sekme) response'u okuyamaz.

Diğer bir önlem ise: tarayıcının otomatik yapmayacağı bir yöntem seçmek. örneğin: "Bearer" ile header'da bu bilgiyi manuel javascript ile yollarsak, başka bir sekmeden kötü niyetli bir kodun bu isteği yaratma şansı düşer. örneğin; farklı domaindeki kötü niyetli kod, cookie'de olan JWT'yi okuyabilirse, JS tarafında manuel request oluşturması gerekecek (hacker bunu da yapabilir, ama ihtimali düşürüyoruz). Oysa cookie'de olan bir jwt token'ı otomatik web tarayıcıya (tarayıcının kendisi aracılığı ile) yollatsaydık, o zaman farklı sekmedeki bir request bizim domain'e istek yaptığında, coookie'leri tarayıcı request'e otomatik eklerdi.
