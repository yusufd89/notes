############################

############################
# UNICODE AND MULTI-LANGUAGE APPS
############################

############################

# Endianness

Bir veri başka bir yere taşınırken verinin taşınma sırasını temsil eder. __Big endian__'da değeri yüksek kısım (byte) (most significant byte) sağ tarafta olur. __little endian__'da ise (least significant byte) tersi geçerlidir.

Big Endian piyasada "__Motorola convention byte ordering__" yada "__motorola style byte ordering__" olarakta geçmektedir. çünkü mototora işlemcilerde hep big endian kullanılmaktadır. 

Bu sıralama bit bazında değildir. Bit bazında hangi sırada tutulduğu donanımın kendisi belirler. eğer bit bazındaki önceliklendirmeden bahsediyorsak; "__Bit endianness (or bit-level endianness)__" terimini kullanmak durumundayız. 

Fakat network dünyasınnda __endianness__ yerine "__network order__" terimi kullanılır ve bit bazındaki transfer yönünü belirler. network dünyasında; "__network byte order__" big endian'a denk gelmektedir.

# bit
__binary digit__'ten türemiştir.

# nibble
kelime anlamı: kemirmek.

'byte' ingizlicedeki ısırmak anlamına gelen 'bite' ile eşseslidir. bu sebeple nibble'a da bu isim takılmıştır.

türkçe'de bu terimin karşılığı yok. 'yarım byte' olarak ifade edilir.

yarım byte anlamına gelir.

bazı kaynaklarda;
- 'byte' ile yazımını benzetmek amaçlı __nybble or nyble__ olarak ta kullanılır.
- __half-byte or tetrade__ olarak kullanılır.
- network sistemlerinde genel olarak __semi-octet or quadbit or quartet__ kullanılır.

# charset (or karakter seti) vs character encoding (or karakter kodlaması)

charset, hangi karakterleri kullanılıp kullanılmayacağını belirtir. Örneğin; ABC kümesi bir charset olabilir. Fakat bunların binary bazında nasıl kaydedeği bilgisini charset içermez. binary bazında nasıl kaydedileceğini (tutulacağını) encoding kuralları belirler. A harfi bir encoding'de 8 bit olarak tutulurken, farklı bir encoding'de yine A harfi 16 bit olarak tutulmak zorunda kalabilir. Her encoding charset uzayının boyutuna göre ayarlandığından (formatlandığından/boyutlandırıldığından), belli bir charset'i destekliyor olur. Dolayısı ile bi yerde "charset=UTF-8" gibi bir ibare görülebilir. Bu ibare; UTF-8'in desteklediği charset'ler anlamına gelmektedir.

# ASCII (or American Standard Code for Information Interchange)
Bir encoding standardıdır. Sadece ingilizce ve en temel karakterleri içerir. 7 bittir. 1 bir ekstra olarak parity biti olarak kullanılır. dolayısı ile 8 bit yer kaplar.

# Extended ASCII (or EASCII or high ASCII or Genişletilmiş ASCII)
8 bittir. parity biti içermez. ilk 7 biti ASCII ile aynıdır. diğer bitler ise farklı karakterler içerir. diğer bitler için bir standart yoktur. her işletim sistemi ve kurulan dil paketine göre değişiklik gösterir.

# ANSI (or Windows-\*)

7+1 bittir. ASCII yetersizliğinden ortaya çıkmıştır. ASCII ile ilk 7 biti aynı karakter setine referans ettiği için ASCII ile uyumludur. Diğer 128 bit ISO-8859 standardının türevlerin değişiklik göstermektedir. Örneğin; Windows-1254; ASCII (ilk 127) + TR (diğer 127) içermektedir.

# ISO-8859

7+1 bittir. ASCII yetersizliğinden ortaya çıkmıştır. ASCII ile ilk 7 biti aynı karakter setine referans ettiği için ASCII ile uyumludur. Diğer 128 bit ISO-8859 standardının türevlerin değişiklik göstermektedir. Örneğin; ISO-8859-9; ASCII (ilk 127) + TR (diğer 127) içermektedir.

# Unicode Transformation Format (or UTF)

Bir encoding standardıdır. kendi içinde UTF-8, UTF-16, UTF-32 gibi ayrımları vardır. Format sürekli yenilenmekte ve yeni versiyon çıkmaktadırlar.

utf karakter boyutu çok büyük olduğundan boş atanmamış karakter noktaları/kodları da vardır.

- UTF-8: karakter'e göre 1-4 byte arsında her karakter uzayabilir. ilk 7 biti aynı karakter setine referans ettiği için ASCII ile uyumludur.

- UTF-16: karakter'e göre 2-4 byte arsında her karakter uzayabilir. ASCII ile uyumsuzdur. 

- UTF-32: her karakter 32 bittir. her karakter ayrı ayrı ayrıştırılabilir. ASCII ile uyumsuzdur. 

- UTF-1: artık kullanılmıyor ve standart değil

- UTF-7: birileri tarafından makalelerle yayınlanmıştır. fakat resmi bir UTF standardı değildir.

utf-8, 16 ve 32 tüm karakterleri gösterebilme yeteneğine sahiptir (hatta boş alanları dahi vardır).

UTF ile ilgili birçok terime buradan ulaşılabilir: (source-id: 426)

# code unit

bir karakteri utf-8, utf-16 gibi encodinglerle byte haline çevirdiğimizde ortaya çıkan byte bilgisine verilen isimdir. örneğin; A karakterinin code point'i U+0031 olsun, code unit'i UTF-8 için 0031, utf-16 için 00010031 olabilir (değerler tamamen uydurmadır). 

# Unicode

UTF-8, 16 ve 32 bir encoding formatı iken, bu encodinglerin baz alındığı(desteklendiği) karakter-seti Unicode'dur. utf-8 dahi tüm unicode'u desteklemektedir.

"Unicode" kelimesi microsoft windows'un bazı yazılımlarında yanlış kullanılmaktadır. bu sebeple karıştırılmamasına dikkat edilmeli. 

Birçok unicode karakteri bu linkte description, code point gibi birçok detay ile listelenmiştir: (source-id: 224)

# '€' karakterini utf-8 ile kodlayalım.

- € karakteri U+20AC kod noktasına tekabül eder

- 0010 0000 1010 1100 (binary) = 20AC (hexadecimal)

- U+20AC 2 byte'tır. fakat aralık Unicode standartlarında U+0800 ile U+FFFF arasında olduğu için 3 byte ile tutulmalıdır.

- 3 bayt olduğu için 3 tane 1 yanyana kulanılacaktır. 1'lerin bittiğini belirlemek için 1 adet sıfır sağ tarafa eklenecek. sonuç; 1110.

- 1110 4 karakter odluğu için 1 bayta tamamlanacak ve 0010 0000 1010 1100'nin en önemli 4 biti daha kullanılacatır. sonuc: 1110 0010

- daha sonraki kısmıda belirli algoritmalarla tamamlanıyor.

akışa bakıldığında; tüm metin için ortak bir yerde metadada saklanmadığı görülmektedir. yani her karakerin uzunluğu UTF-8 ve UTF-16 için karakterin başında bellidir. bu sebeple bir sonraki yada önceki karakterler ilgili karakterimizi boyutunu değiştirmemektedir.

# unicode karakter özellikleri

unicode standratlarında her karakterin bir meta bilgisi vardır. bu bilgi karakter kodundan diil, dökümantasyondan çıkartılmalıdır.

- genel kategori (or general category)

  30'a yakın kategori vardır (yıl 2019)

  kategoriler virgülle ayrılmış iki kısımdan oluşmaktadır. ilk kısım major class, ikincisi ise subclass'ı temsil eder.
  
  örnek: "Number, decimal digits", "Number, letter", "Number, Others".

  bazı kategoriler:

  - Other, control
    
    kod: Cc
    
    açıklama: "start of text", "end of line" gibi karakterleri buradadır.

  - Letter, Lowercase
    
    kod: Ll

  - Letter, Uppercase

    kod: Lu


  Fakat her kategori %100 şekilde uymamaktadır. geriye uyumluluk için bazı istisnalara tölerans gösterilmiştir. (bazıları yeni sürümlerde düzeltiliyor)

- code point

  U+0001 şeklindeki gösterimin ismidir. burada U+ hiçbir anlamı yoktur. unicode'un verdiği özel bir prefix'tir. Aslında asıl değer 0001'dir ve bu değer unicode karakter listesindeki 2'inci elemana referans eder. 0001, hexadecimal formattadır.

- name

  büyük harflerle alfanumeric, boşluk ve tire işaretli içerebilir. tekildir fakat her karakter için set edilmiş bir değer olmayabilir.

- name alias

  Unicode version 2 ile birlikte 

- script

  (başka başlıkta ne olduğu anlatılıyor)

  200'e yakın script vardır.

- Bidirectional class

  "Unicode Bidirectional (bidi) Algorithm" için gerekli bilgileri verir. metnin sağdan sola mı soldan sağa mı, yoksa etkisi olup olmadığı gibi... Bu bilgiden 25'e yakın var (yıl 2019). bu sebeple algoritma karışık. aynı satırda birden fazla farklı dilden metin olursa ne yana yaslanacağı belli kurallara göre (algoritma ile) belirlenmektedir. Aynı satırda farklı yönlerde karaktermetin olması durumunda o text bloğuna Bi-directional text (or BI-DI or BIDI) denir.

- Lowercase/uppercase Character

  aynı karakterin büyük yada küçük versiyonununun code-point'i.

- Mirrored

  karakterin mirroru olup olmadığı bilgisi. bu bilgi sadece true/false şekilde tutuluyor. hangi karakter bu karakterin mirror'u olup olmadığı bilgisi tutulmamaktadır. örnek mirrered characterler: < > ( )

- Decomposition

  bir karakter birden fazla karakterin birleşimindenoluşuyorsa, hangi karakterlerin birleşimindenoluştuğu bilgisi. örnek: vurgu işaretli e' karakteri; e ve vurgu karakterinden oluşuyor. dolayısı ile şapka yada tonlama işaretlerinden herhangi birini almış her karakterin unicode'u varklıdır. örneğin yunancadaki omega işraeti; ω, tonlama aldığı zaman (ώ) farklı codepoint'e sahip farklı karakter oluyorlar.

Bu gibi karakter özellikleri karakterlerin tipini algılamak durumunda olduğumuzda önemli olabiliyor. örneğin; Unicode'da her karakterin bilgisi saklanıyor. Eğer kullandığımız regex kütüphanesi bu bilgileri saklıyor ise; o zaman aşağıdaki gibi kontroller ile de regex yazabiliriz:

- Alphabetic
- Ideographic
- Letter
- Lowercase
- Uppercase
- Titlecase
- Punctuation
- Control
- White_Space
- Digit
- Hex_Digit
- Noncharacter_Code_Point
- Assigned 

kaynak: (source-id: 225) "Unicode support" başlığı.

# UTF mimarisinde karakterlerin sıralanması/gruplanması

- plane 

  plane kelime anlamı: tabaka

  tüm karakterler sıra bazlı gruplandırılmışlardır. sıfıra yakın plane'deki karaketerler, günlük hayatta daha çok kullanılıyor.

  örnek: 

  - plane 0

    aralık: U+0000 - U+FFFF

    adı: BMP (or Basic Multilingual Plane or 0 BPM or plane 0)

  - plane 1

    adı: 1 SMP (or Supplementary Multilingual Plane)

  - plane 2

    adı: 2 SIP (or Supplementary Ideographic Plane)

  - plane 3-13

  - plane 14

    adı: 14 SSP (or Supplement­ary Special-purpose Plane)

  - plane 15-16

  Yukarıdan görüldüğü gibi; U+FFFF - U+FFFFFF aralığı için plane'ler "supplementary" prefixini alıyor.

- block

  tüm karakterler plane'den daha ufak seviyede de gruplandırılmıştır. kolay hespalama olsun diye yapılmıştır. bazı block'lar:
  
  - U+0000 - U+007F

    ismi: Basic Latin

  - U+0080 - U+00FF

    ismi: Latin-1 Supplement 

  - U+0100 - U+017F

    ismi: Latin Extended-A 

  ...

  - U+0600 - U+06FF

    ismi: Arabic 

  ...

  - U+0750 - U+077F

    ismi: Arabic Supplement

  ...

  - U+08A0 - U+08FF

    ismi: Arabic Extended-A

  ...

# BOM (or Byte Order Mark)

UTF'lerde (little/big endian) önemlidir. Bu sebeple standartlara göre opsiyonel olarak text'in en başına byte order bilgisi atanır. Bu bilgi ile text'in hangi order'da olduğu belirtilir. Text editorler menülerde encoding'leri bu şekilde gösterirler: UTF-16-LE, UTF-32-BE olarak kısaltılırlar. UTF-16-with-BOM 'da kullanılrı fakat LE mi BE mi belli değildir. bu yüzden bu kullanım tavsiye edilmez.

BOM'un uzunluğu belirsizdir. çünkü birçok kombinasyonu vardır. UTF-8, 16, 32, 7 (ve daha fazlası) ve bunların LE BE kombinasyonları vardır.

# EOF (or End Of File)

EOF bir karakter değildir. Çoğu proramlama dilindeki dosya okuma yazma API'leri bunu karaktermiş gibi yansıtabilir. fakat karakter değildir. Böyle bir karaktere ihtiyaç yoktur, çünü tüm dosya sistemlerinde dosyaların boyutu bellidir.

# ETX (or End Of Text) vs NUL

birer karakterdir. Eskiden teknolojilerde (telegraf gibi) kullanıldıklarından, yeni encoding standartlarında geriye uyumluluk olması açısından karakter olarak yer almaktadırlar.

# newline (or line ending or end of line or EOL or line break or satır sonu)

birçok alternatifi vardır. işletim sistemide varsayılan olarak deişebilir:

- POSIX: LF (line feed) --> \n

- Windows: CR+LF (or CRLF) --> \n\r

- bazı sistemlerde sadece CR kullanılmakta, bazılarında ise LF+CR kullanılmaktadır.

açılımları:

CR: carriage return

LF: line feed

Atom text editor'de "invisible character" olarak nitelendirilen karakterler: boşluk, eof ve tab'dır. Atom, LF ve CRLF'yi simge olarak göstermektedir.

Bunlar dışında karakter setlerinden birçok kontrol (özel) karakter bulunmaktadır. örnek:

- paragraf sonu

- backspace

- delete

- ctrl-z

Bu karakterler önyüzde bir şey göstermek için değil, belli işlemler yaptırmak için kullanılır. bu karakterler sadece dosyadan okununca işe yaraması için yapılmamıştır. örneğin ctrz-z karakterini C gibi bir dilinde printf ile ekrana bastığınızda CTRL-Z olan "geriye al" işlemini yapar. yada klavyede basılan bir tuşu uzak makinada çalıştırmak için bu tarz kontrol karakterleri işe yarayabilir. Bu tarz karakterler "control" karakteri olarak Unicode'da da kullanılmaktadır.

# unicode'daki bazı özel karakterler

unicode'da özel karakterler diye bir grup yoktur. Bu başlıkta boşluk, satır sonu gibi karakterler hakkında açıklamalar vardır.

```
LF:    Line Feed, U+000A

VT:    Vertical Tab, U+000B

FF:    Form Feed, U+000C (yeni bir sayfa oldugugunu printer'a belirtmek için kullanılır)

CR:    Carriage Return, U+000D

CR+LF: CR (U+000D) followed by LF (U+000A)

NEL:   Next Line, U+0085 (bazı ibm platformları bunu kullanıyor.)

LS:    Line Separator, U+2028

PS:    Paragraph Separator, U+2029
```

yukarıdaki bazı karakterlere simge atayabilmek için farklı karakterler ile ikon seti belirlenmiştir:

```
U+2424 (SYMBOL FOR NEWLINE, ␤)

U+23CE (RETURN SYMBOL, ⏎)

U+240D (SYMBOL FOR CARRIAGE RETURN, ␍)

U+240A (SYMBOL FOR LINE FEED, ␊)
```

unicode'da 20'ye yakın farklı space vardır. bazıları farklı platformlarda kullanıldığı için, bazılarının ise uzunlukları farklı.

Unicode'un amacı yeni bir karaketer standardı yaratmak değildir. varolan tüm karakterleri tutmaktır.

# invisible characters
UNICODE'da birçok invisible karakter vardır. Bunların bazıları yazılımlar tarafından input olarak alındığında harcode olarak engellenmezken, bazıları engellenmektedir.

Örneğin bu projede: (source-id: 226) 1-"gizlenecek text" 2-"şifre" 3-"şifrelenmiş mesaj" input olarak programa veriliyor. "şifrelenmiş mesaj"ın en az 2 kelime olması zorunlu. şifrelenmiş mesajın boşluk kısmına (2 kelime arasına) gizli mesajın kendisi görünmez karakterler aracılığı ile gömülüyor. Aslında boşluk bir referans olarak kullanılıyor, yoksa gizlenen mesaj herhangi bir karakterin arasına da koyulabilir, çünkü zaten görünmüyor.

# URL encoding (or percent encoding)

URL 'lerde boşluk ve bazı özel karakterler kabul edilemez. dolayısı ile bu karakterler için yeni bir encoding geliştirilmiştir. bazı karakterler % ve sonrasında 2 adet sayı olacak şekilde bir karakteri temsil etmektedirler.

# StringUtils

apache-commons-lang kütüphanesinin içinde olan bir sınıf. Commons-lang içinde CharUtils, RandomStringUtils(random string üretiyor) sınıfıları da mevcuttur.

# trim

türkçe kelime anlamı: düzeltmek

bu metod birçok kütüphane içinde mevcuttur. birden fazla boşluk yanyana ise onları tek bir boşluk haline getirir. eğer boşluk en sağda yada en sonda varsa onları kaldırır.

# karakter grupları

karakterler son kullanıcı açısından gruplanmıştır. fakat bu grupların bir resmiyeti yoktur. örneğin; mobil uygulamalarda sanal klavyede i tuşuna basılı tututlduğunda i'nin türevleri çıkar. örnek: 'ı' gibi. bu karakter grupları o sanal klavyenin kendi ayarıdır. böyle bir gruplama utf yada farklı karakter setlerinde tanımlanmamıştır. 

ingilizcedeki küçük 'i' ve türkçedeki küçük 'i' ortak karakterdir. toLowerCase() metodu işletim sisteminden default dili algılar ve ona göre uygun büyük harfe çevirir. toLowerCase() metodu parametre olarak java Locale'i alır.

# accent (or aksan or şive)

örnek: alman türkçesi. ana dili türkçe olmayan kişiler kullanır. bu terim "ağız" terimi ile çok benzer fakat farklı. ağız, ülke içinde kullanılan farklı tonlamalar gibi ufak değişiklikleri temsil ederken, aksan yurtdışındaki insanların kullandığı tonlamalar gibi ufak farklılıkları temsil eden terimdir.

# lehçe (or diyalekt or Dialect)

örnek: Azerice (or Azerbaycan Türkçesi or Azerbaycanca) bir türkçe lehçesidir.

terminolojik olarak; resmi olarak lehçenin dilbilgisi farklıdır.

bazı kaynaklar dilbilgisindeki değişiklikler çok farklı olmadığından yada gereğinden fazla fark olduğundan lehçe yerine, "şive" yada "dil" termini de kullanmaktadır.

# ağız (or subdialect)

örnek: karadeniz türkçesi.

# aksan işareti (or aksan imi or grave accent)

örnek: ằ v̀ gibi hem sessiz hem sesli harflerde birçok farklı şekilde bulunurlar.

StringUtils.stripAccents("abc"); metodu aldığı string'deki vurgu karakterlerini silip, yerine vurgusuz halini koymaktadır. örnek égğ --> egg

strip türkçe kelime anlamı: soymak, üstünü çıkarmak.

(diğer başlıklarda anlatıldığı üzere) Unicode metadalarında hangi karakterlerin üzerinde hangi aksan işareti olduğu bilgisi tutulmaktadır. yani; v̀ için, "v ve aksan işareti" olduğu Unicode veritabanında mevcuttur.

# java.util.Locale 

bu sınıf jre içinde gelir. içinde static olarak en sık kullanılan değerler hazır bulunur:

static public final Locale ENGLISH = createConstant("en", "");

static public final Locale UK = createConstant("en", "GB");

static public final Locale US = createConstant("en", "US");

Locale 3 parametre alır:

Locale(String language, String country, String variant). sağdaki iki parametre opsiyoneldir. eğer atılmazsa boş olarak kullanılır. yani locale.getVariant() boş döner.

Locale sınıfının aldığı üç parametre ağız/lehçe/aksan kombinasyonu değildir. dil, kullanıldığı ülke ve türevi olarak algılanır. örnek:

- "azerbaycan türkçesi", türkçe'nin türevi diildir. kendisi bir dildir. ve ülkesi azerbaycan'dır.

# alfabe (or alphabet) 

bazı alfabeler:

- Latin alfabesi (ABCDEF...)

- Yunan (or Greek) alfabesi

- Kiril (or Cyrillic) Alfabesi (Rusya ve etrafında kullanılıyor)

- Ermenice (or Armenian) alfabesi

- Gürcü (or Georgian) alfabesi

- arap alfabesi

- İbrani alfabesi (or Hebrew)

> japonya, çin ve kore'de kullanılan alfaberlerde birbirinden farklıdır.

> arapça temelli dillerde alfabe hep aynı. bazı karakterler bazı dillerde yok yada fazlası var fakat temelde aynı karakterler kullanılıyor. yani farklı ülkeye gittiğinizde kelimeleri okuyabiliyor fakat ne anlama geldiklerini bilemiyorsunuz.

> arapça temelli dillerde, bazı karakterler yanındaki karakterlere göre şeklini değiştirmektedir (yanındaki karakterlere bağlanmaktadırlar). bu sebeple font viewer'larda gördüğümüz font'lar ile cümle içinde gördüğümüz karakterler aynı olmayabilirler.

# Yazı sistemi (or writing system or script)

yazı sistemi; bir dilin yazı stilidir. örnek: script arapça, bu script'in baz alındığı birçok dil vardır: Iraqi, Lebanese, Egyptian... Arapça baz alınan dllerin %100 arapça yazı stili kurallarına uymayacağı zaten ortadadır.

bazı diller birden fazla yazım sistemini desteklemektedir. örnek: Korece (or Korean), Japonca (or Japanese). Yani bu dillerde aynı cümleler farklı yazı ile yazılabilmektedir.

Örnek: japonca'da aşağıdaki yazım sistemleri vardır:
- hiragana: japonca kökenli kelimeleri yazmak için kullanılır
- katakana: yabancı kökenli sözcüklerin yazmak için kullanılır

japonca'da aynı cümlede birden fazla yazım stili olabilir.

Romanji; japon yazı sistemindeki her karaktere ve heceye karşılık gelen latin karakterleri olur. japonca'da yazılacak cümle, aynı karakterlere denk gelen latin karakterleri ile yazılır. Romanji'de kendi içinde türevleri vardır.

# Traditional vs Simplified Chinese
Çince zor dil olduğundan her katakter daha basit bir görüntü haline getirilip, ortaya daha basit okunabilen karakterler yaratılmıştır. Bu yeni sisteme Simplified Chinese ismi verilmiştir. Simplified Chinese'de her karakter değişmemiştir.

Japonca da benzer durum yok, çünkü japonca Simplified Chinese'e göre dahi daha kolay anlaşılır bir görüntüsü var.

# numbers

  - ## digit

    türkçede matematik'teki "basamak", "hane" olarak çevrilir.

    13'lük sayıs siteminden rasteel bir sayı alalım: 111A

    en sonda olan A (10 sayısına denk gelmektedir) tek başına bir basamak hanedir.

  - ## Unicode terminolojisi

    Unicode karışıklığa sebep olmaması bazı termleri şu şekilde kullanmaktadır:

    - digit: only numerical digits

    - Arabic digits yada Arabic-Indic Digits: Arabic script'e ait rakamlar

    - Western digits yada Latin digits yada European Digits: 0-9 rakamları

    - Indic digits: hint temelli dillerde kullanılan rakamlardır.

  - ##  Doğu Arap rakamları (or Eastern Arabic numerals or Arabic–Indic numerals or Arabic–Hindu numerals or Arabic Eastern numerals or Indo-Persian numerals)

    arapça tabanlı kullanılan bir sayı sistemidir. arap ülkeleri arasında da farklılık gösteriyor.

    arapça yazılım geliştirirken arapça sayı girişi olan input'larda arap ülkelerindeki kullanıcılar sadece "Doğu Arap rakamları" değil aynı anda klavye aracılığı ile "Arap rakamları"'na (0-9) geçiş yapabiliyor. bu durumda yazılımcıya ek iş yükü binmiş oluyor.

  - ## Arap rakamları (or Hindu–Arabic numerals or Indo-Arabic numerals or Arabic numerals or Western Arabic numerals or Western numerals)

    0-9 kullanan rakam karakterleridir.

  - ## Roma rakamları (or Roman numerals)

    Bazı kullanım alanları:

    - Kitapların başlangıçlarındaki sunuş ve önsöz gibi bölümlerde.
    - Aynı adlı padişah ve kralların ayrılmasında: II. Ahmet, XVI. Louis gibi.
    - Yüzyıl adlarında: XIX. yüzyıl gibi.
    - Tarihi olaylarda: II. Viyana Kuşatması, I. Dünya Savaşı gibi.

    Temel kurallar: 
    
    I = 1

    V = 5

    X = 10

    gibi daha birçok karakterden oluşur.

    sağına eklenenler toplanır, sola eklenenler çıkarılır. örnek:

    XIV = 14

    XXIV = 24

    karakterler üzerlerine düz çizgi de alabilirler. bu durumda o sayının 1000 katı temsil edilir.

  - ## çin ve arapça'da sayılar

    arapçada sayıların görünümü farklı fakat sistem olarak "Arap rakamları (0-9)" ile aynı. yani her basamak bir karaktere denk geliyor.

    çince temelli dillerde de sayılar bölgeden bölgeye farklılıklar gösterir.
    
    çince'de ise yazım sistemi de farklı. örnek üzerinden gidersek; "Mandarin çincesi"nde her karakter bir sayıyı ifade etmiyor. örnek: 
    
    - __四十二 42 iken
    - 九十 90 'ı temsil ediyor. görüldüğü gibi sayı daha büyük olmasına rağmen daha az karakterle temsil ediliyor.

    Özellikle programatik olarak __sıralama__ istendiğinde çok zor durumlarla karşılaşılmaktadır.

# CJK

Chinese, Japanese ve Korean dilleri için ortak terimdir. Bazı dilbilimciler Vietnamese (or vietnamca) dilinide bu gruba katarak, __CJKV__ kısaltmasını kullanırlar.

CJK karmaşıklığını gidermek için (mappinglerin daha düzenli olması için) Unicode projesinde ayrı gruplar çalışmaktadır. bu çalışmalar "__Han unification__" olarak isimlendirilmektedir. 

'Çin yazı karakterleri'ne '__Hanzi (or Han characters)__' deniliyor.

# Çin

Çinde birçok farklı türemiş dil mevcuttur. Ülke resmi olarak __"Mandarin"__ isimli dili kullanmaktadır. "Mandarin" Çin'de en fazla kullanılan dildir. Cantonese ve Wu dilleri diğer en çok kullanılan diller arasındadır.

Sadece "Çince" denildiğinde "Mandarin" kastediliyordur. 

Mandarin, Cantonese arasında farklar: bazı karakterler, grammer yapısı, tonlamalar, kelime hazinesi. Mandarin metni okunduğunda, sadece Cantonese bilen biri bu cümleleri anlayamıyor.

Çinde yüzlerce dialect ve dil vardır.

__Classical Chinese (or Literary Chinese)__ hala kullanılan ve İsa zamanına dayanan bir tarihi vardır.

Kore ve Japonya'da böyle bir durum söz konusu diildir, çünkü tek bir dil var fakat çok çok ufak bölgesel farklılıklar görülebilir.

# arapça
__Klasik arapça (or Classical Arabic or Quranic Arabic)__ 7 ve 19 uncu yüzyıllar arası kullanılan arapçadır. Şu anda daha çok dinsel eğitimlerde ve ibadetlerde kullanılmaktadır.

__Old Arabic (or eski arapça)__ klasik arapça'dan önce kullanılması ile ölen bir dildir.

__Modern Standard Arabic (or MSA or Standard Arabic or Literary Arabic or Modern Written Arabic or MWA or tr:Fasih Arapça)__ birçok ülke tarafından resmen tanınan bir arapça çeşididir. Günümüz sistemlerine uygun şekilde tasarlanmaktadır. "Klasik Arapça" temelli bir dildir. arapçada bu dile "El-Arabiyye el-fusha" denir.

Tüm arapça dillerinin alfabeleri aynıdır.

# alphanumeric (or Alfanümerik)

Apache-commons-lang StringUtils sınıfına göre; sadece isAlpha():

- işaret ve boşluk karakteri içermemeli. yani sadece "latter" içermeli. letter bilgisi Unicode'un "general category" bilgisinden gelmektedir.

- sadece unicode karakteri içermeli

- sayı içermemeli

isAlphanumeric(); isAlpha'nın sayı kuralını ignore eder.

# fontlar

her font belli bir karakter setini desteklemektedir. Eğer ekranda gösterilmesi gereken karakter seti o sıra kullandığımız font'ta tanımlı diil ise; web tarayıcıda isek; web tarayıcının kendisi, native bir uygulamada isek; OS'un kendisi karar verip, görüntülenemeyen karakter için şunu yapacaktır:

- default bildiği font, yada farklı bir font ile o karakteri gösterecektir

- sadece o karakteri hiç göstermeyecektir (boşluk yada hiç)

- hata fırlatacaktır (bu hiç tercih edilmeyen yöntem. neredeyse hiçbir program böyle bir şey yapmıyor)

- fallback karakterini gösterecektir.

- böyle bir karakter gösterecektir: (bir diktörgen içinde sayılar ve harfler oluyor)

  ```
   _____
  | 1 8 |
  | 2 f |
   ¯¯¯¯¯
  ```

   Bunun anlamı bu karakter: 16'lık gösterimde 182f'dir.

# replacement character (or missing glyph or replacement glyph or .notdef glyph)

- � (içinde soru işareti olan altıgen) karakteri simgesindedir.
- bu karakter utf kodlamasında hata alındığında, hata alınan karakter yerine bu karakterin konulması istenmektedir.
- code point'i U+FFFD'dir.
- Bu unicode'un bir standartıdır. bu sebeple her font'un fallback karakteri bu codepoint'e tekabül etmez. fakat her font dosyasında bir fallback karakteri olması beklenir. 
- Unicode'un unsopported character dökümanına bakıldığında: (source-id: 427) her fallback karakteri için "replacement character" kullanılmaması önerilmektedir. örneğin;
  - White_Space property içeren fakat tanımlanmamış karakterler yerine boşluk gösterilmeli
  - default-ignorable character'ler tanımlanmamışsa yerine hiçbir şey gösterilmemeli 

# tofu
kelime anlamı: soya peyniri

replacement character yazılımlar tarafından her zaman unicode'da belirtilen şekilde olmamaktadır. genelde boş kare yada içi noktalarla dolu kare işareti gösteirlmektedir. işte bu işarete yazılımcılar tofu demektedir. kelime anlamından gelmesi ona benzemesindendir.

# noto
no-tofu'dan üretilen bir kelimedir.

google'ın geliştirdiği font ailesinin ismidir. unicode'da olan dillerin tümünün alfabesini karşılamak için tasarlanmıştır. alfabeler dışında ekstra karakterlerde vardır, fakat öncelik dilin alfabeleridir.

# glyph
kelime anlamı: kabartma/oyma.

bir karakterin yada herhangi bir olgunun, simgelenmiş halidir (representation of character or thing). 

bazen bazı karakterlerin birden fazla glyph karşılığı olabilir. çünkü karakterler, kültürden kültüre (digital ortamda font'tan font'a) farklı görünebilirler. bu sebeple; bir font dosyasındaki her karakter, birer glyph'tir. fakat her "UNICODE karakteri" bir glyph diildir. UNICODE nasıl görüntüleneceği ile ilgilenmez. görüntü glyph'tir. bir karakter, görüntüsü olmadan bir şey ifade etmez. "karakter" tek başına sadece bir tanımdır.

# eng:grapheme (or tr:grafem)
dil biliminde; bir yazı sisteminin en küçük birimidir. 'karakter'ler buna örnek verilebilir.

# yüzde işareti (or percent sign)

% işareti ile temsil edilir. ingilizcede yüzde 5; 5% ile yazılırken, türkçede %5 ile yazılır.

‰ işareti "per mile" olarak isimlendiriliyor. fakat 1000'i temsil ediyor. "per mil" karakterindeki "mil" kelimesi uzunluk birimi olan mil'den (1 mil = 1 km değil! ve kara ve denizde farklı değeri vardır) gelmemektedir.

45% = 0.45 = 45/100 eşitliğini göstermek için kullanılır. + - işaretleri gibi her istenilen yere konulamaz. özel bir gösterim karakteri olduğu için bazı özel durumlarda kullanılır. örnek:

- 45% = 0.45 // tek başına kullanıldığında bu anlama geliyor.

- 200 − 10% = 180 //burada 10% ile; 200'ün yüzde 10'u alınmıştır. yani; 200-20=180.

- 200 − 10% + 3 //hatalı kullanım.

# dosyayı byte array olarak ekranda okuma

linux komut satırı uygulamaları ile yapılabilir. örnek olarak içeriği aşağıdaki gibi olan bir dosya için; 

123456789123456789

- 16'lık tabanda görebilmek için:

> hexdump myfile.txt

```
0000000 3231 3433 3635 3837 3139 3332 3534 3736

0000010 3938 3231 3433 3635 3837 3139 3332 3534

0000020 3736 3938 3231 3433 3635 3837 0a39     

000002e
```

- 8'lik tabanda görebilmek için:

```
0000000 031061 032063 033065 034067 030471 031462 032464 033466

0000020 034470 031061 032063 033065 034067 030471 031462 032464

0000040 033466 034470 031061 032063 033065 034067 005071

0000056
```

-- yukarıdaki çıktılarda ilk sutun aralıklardır. sadece output'u guplandırmak için komut satırı uygulamalasının kullandığı gurplama tekniğidir.

-- bir satırda sadece # karakteri var ise; bunun anlamı üstteki satır ile birebir aynı olduğudur. -v parametesi ile bu durum iptal edilebilir.

-- 8'lik tabanda output'ta gösterilen bir değer max 7 değerini alabilir. 7 için 3 bit'e ihtiyacımız var. 1 byte 8 bit olduğundan, 8lik tabanda 1 byte'ı göstermek için 3 karaktere ihtiyacımız var. ve en yüksek öncelikli karakterde gereksiz boş yer kalmaktadır. örnek: octal(177) = hex(7F) = binary(1 111 111). örnekte gözüktüğü gibi output'u en erimli görebilmek için 4 bite denk gelen 16'lık taban kullanılmalıdır. octal gösterimde 2'inci byte, örnekte 177'yi en az 1 arttırarak 200'a çıkaracaktır.

-- bazı text editörler satır sonu karakterlerini (örnek 0a) otomatik atarlar ve ekranda (son kullanıcıya - GUI'de) satır sonunu göstermeyebilirler.

-- bazı editörler BOM karakterini dosyanın başına otomatik atarlar.

# text dosyasında encodingi otomatik algılatma

text editorler dosyayı açtıklarında deneme yanılma yöntemi il doğru formatı bulmaya çalışırlar. örnek utf-16 mı diye sorguladıklarında, her karakter için bir karaktere ulaşılabiliyor ise o formatı geçerli kılarlar. fakat bu her zaman %100 doğru encoding'i bulabilme durumu söz konusu diildir.

# java char

java'da "char" 2 byte uzunluğundadır. unsigned 16 bit sayı olarak tutulur. bu sebeple unicode'daki U+FFFF üstü karakterler java'nın char tipi tarafından desteklenememektedir.

tanımlamak için: char myChar = '\u0003'; yazılır. Bu sebeple int'e cast işlemi sonucu "3" değerini alırız. 

Character sınıfı char tipini constructor'dan alır ve wrap eder. Character sınıfıda char'ı wrap ettiği için yine  U+FFFF üstü karakterleri destekleyemez.

Aşağıdaki gibi tanımlama yapabiliriz:

```java
char myChar = '\u0003';

Character myCharClass = new Character(myChar);

myCharClass.hashCode(); // int 3 değerini döndürür

myCharClass.compareTo(anotherCharacter); //eşitlerse 1 değillerse 0'ı döndürür. eşitlik unicode codepointi ile yapılır.
```

Character sınıfının metodları unicode'un her karakter için belirlediği property'leri de döndürmektedir. örnek: lowercase, unicodeblock... metod isimleri direk anlaşılmaktadır. tek istisna getType() metodudur ki bu "genel kategori" bilgisini döndürmektedir.

Char karakteri 16 bit olduğundan tüm unicode desteklenememektedir. daha sonraları char boyutu yükseltilmek istenmiş fakat bu köklü değişiklikler gerektirdiğinden string alternatifi farklı sınıfılar sunulmuş, ve Character sınıfına bazı destekleyici metodlar eklenmiştir. örnek:

charCount(int codePoint) metodu: codepoint'imizi int olarak gönderiyoruz. eğer U+FFFF 'ten büyükse (yani 16 bit'e sığmayacaksa) 2 dönüyor. diğer durumlarda 1 dönüyor.

boolean isSupplementaryCodePoint(int codePoint) metodu: charCount metodu ile ynı şeyi belirtmektedir fakat boolean ile dönüş yapar.

Character sınıfı içindeki birçok aynı isimde metod hem int (codepoint) yada char alacak şekilde ayarlanmıştır. char alan metodlar eskiden vardı, int alanlar ise sonradan geliştirildi. int almalarının sebebi codepoint'i U+FFFF üstü değerleri int olarak verebilmemizi sağlamaktadır.

Character.toCodePoint(char high, char low) --> char array gönderiyoruz. elimizdeki bir 2 ielemanlı bir char[]'in ilk ve ikinci elemanını buraya yolluyoruz. char[2] 32 bittir. buraya yolladığımız karakter br code-unit'tir. yani (int) char[2] bize codeunit vermelidir. bu metod ise bize onun code point'ini döndürmektedir. 

Character.toChars(int codePoint) --> codepoint'e karşılık char[2] yada char[1] döndürmektedir. döndürülen bu char[]; (int) char[2] bize codeunit verir.

Character.isSurrogatePair(char high, char low) --> toCodePoint metodu ile aynı parametreleri alıyor. toCodePoint'in iki elemanlı dizi dönüp dönmeyeceği bilgisini veriyor. 

# java String
String kelime anlamı: sicim (bir çeşit iplik)

String kendi içinde char[] tutar. her "char" kendi içinde Unicode codepoint'i ile tutulur. String'in mimarisini constructor'larına bakarak kavrayabiliriz: 

String constructor'u eğer String alıyorsa o zaman charset parametresi istemez. örnek: new String("abc"); çünkü yolladığımız string'i karakterlere böler ve char array'e atar. zaten her karakter artık bellidir. bu karakterlerin unicode'da tanımlı olması şarttır. zaten yolladığımız string'de bir java string'idir. bu işlem sonucu kopyalama işlemi gerçekleşir.

"new String(byteArray, "UTF-8");" ile byte-Array'ı char-array'e çevirmesi için karaketer seti bilgisini yollamamız gerekir. eğer yollamazsak default işletim sisteminin karakter-encoding'ini kullanacaktır. burada byteArray aslında UTF-8 encoding'inde olduğuu belirtiyoruz, ve constructor'a bize java String'i dönmesini istiyoruz. java string'inin ne tuttuğu önemli diil.

String constructor'u eğer unmappable karakter okursa bunu default/özel bir karakter ile replace eder ve bu şekilde char[] oluşturur.

String'in toString metodu dışarıya string'i verirken kendini return eder. bu string'i bir yere basmak için bir stream'e yollamak lazım. bu stream bunu alırken nasıl okuduğu önemlidir. stream, isterse karakter karakter okur, isterse byte byte okur.

"text".getBytes("UTF-8"); ile istediğimiz çeşit encoding'de byte array olarak text'i döndürür.

yukarıdan görüldüğü gibi; bizim için charset ancak şu durumlarda gerekiyor:
- string'den dışarı byte-array çıkarmak istediğimizde
- string'i byte-array ile initialize etmek istediğimizde

bunun dışıdan java kendi içinde nasıl tuttuğu önemli dğeil. her sürümde farklı şekilde tutuyor olabilir. emin olduğumuz bir şey var: jvm bizim için her karaktere tekabül eden codepoint'ler ile string'imizi tutuyor.


- örnek 1:

  yukarıda anlatıldığı gibi;
  - Java char'larda codepoint tutuyor
  - string ise char array tutuyor. 

  şimdi şöyle bir örnek üzerinden gidelim:

  sunucumuza CP1250 formatında request gelsin.

  HTTPServletRequest.getParameter("name") bize beklenmedik karakterler döndürüyor olsun. önce bu string'in bize gelmeden hangi aşamalardan geçtiğini trace edelim:

  - web server'a gelen istek servlet tarafından karşılanıyor.
  - servlet'e gelen istek byte array olarak karşılanır
  - arada filter'larımız olabilir
  - daha sonra getParameter("name") bize string olarak (ilgili alanı, sadece "name" kısmını) döndürür.

  getParameter bize hatalı döndü. çünkü java byte-array'i string'e çevirirken, byte-array'in CP1250 olduğunu bilmiyor ve farklı bir encoding'de okuyor. Doğal olarak; String'e yanlış çevriliyor. Örneğin; en başında belirttiğimiz kurallar gereği artık string'imiz: byte-array barındırmıyor, Code-point barındırıyor. Dolayısı elimizde ile artık yanlış code-point'li karakterler var. Artık string'imizi CP1250'e çevirme gibi bir durumumuz yok. Bu sebeple şöyle bir çözüme gidilebilir:

  Filter oluşturulur:

  ```java
  public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) {

    if (request.getCharacterEncoding() == null) { //Güncel HTTP standratlarında encoding bilgiside gönderilebiliyor.
      
        request.setCharacterEncoding("cp1250");
    }
    chain.doFilter(request, response);
  }
  ```

  Filter'da encoing set edilince artık, HTTPServletRequest.getParameter("name") metodu byte-array'den bizre string döndürürken cp1250 encoding'ini kullanacaktır.

  HTTPServletRequest.getParameter("name", "cp1250") gibi bir metod sunmuyor. bu sebeple yukarıdaki yöntemi kullanmak gerekli.

- örnek 2

  Console'dan karakter okuduğumuz zaman işletim sisteminini default encoding'i ile karakterler okunur. işlemi trace edersek:

  - console uygulaması input olarak karakteri byte'a çevirir.
  - console uygulaması byte'a çevirirken (özel ayar belirtilmemişse) işletim sisteminin default encoding'i ile karakterleri byte'a çevirir.
  - bu byte'ları array olarak programımıza yollar.
  - programımız stream'den (özel ayar belirtilmemişse) işletim sistemininin default encoding'i ile byte'ları string'e çevirir.
  
  Kod içerisinde (örneğin java) steram'in ecdoing'ini değiştirmek istersek şu kodu kullanabiliriz:

  ```java
  Scanner console = new Scanner(new InputStreamReader(System.in, "cp1250"));
  ```

# Modified UTF-8 (or MUTF-8)

JVM'in kendi içindeki sınıflarda kulandığı UTF-8 türevi encoding'dir. Dışarıya çıktı/girdi alan sınıflarda kullanılmaz. Dolayısı ile uç durumlar haricinde yazılımcıyı ilgilendiren bir durum diildir.

MUTF-8 encoidng'inin kullanıldığı yerler:

- DataInput sınıfı içindeki String readUTF() MUTF-8 okur ve bize String döndürür.

- JVM serialize/deserialize yaparken MUTF-8 kullanır.

# Console'a basarken yaşanan karakter problemleri

Bir log attığımızda eclipse console'u veya aynı text'i dosyaya attığımızda farklı biçimlerde ekranda görünebilir. bu tarz sorunların sebebi her Reader'ın (console, text editor...) okuduğunda encoding'i bilmemesinden kendi default varsaydığı encoding'de olduğunu varsayıp okuyup ekranda göstermesidir.

# code page

unicode çıkmadan önce her işletim sistemi belli karakter kümelerini gruplayarak isimlendirmekteydi. bu gruplara code page deniliyor.

code page bir encoding değil, sadece karakter setidir. örneğin; sistem hangi karakter seti destekliyor dendiğinde, X code page'ini destekliyor denilirdi.

bir code page içerisinde, her karaktere tekabül eden bir sayı vardır. bu sayıya "code point" denir. GUI aracılığı ile bir textbox'a metin girerken, ALT+123 şeklinde bir tuşlama yazdığımızda, işletim sistemininin varsayılan code point'i üzerindeki 123'üncü sayıyı çağırmış oluyoruz. ALT+123'a "alt code" adı verilir.

çoğu zaman codepoint'ler 256 karakter uzunluğunda tutulur. bu şekilde ilk karakter ve son karakter, bir sayı ile temsil edilmek istendiğinde hepsinin byte aralığı sabit olur (1 byte). aslında bu bilgiyi byte olarak dosyaya yazdığımızda encoding görevi görmüş olacaktır. fakat code page encoding standartdı dwğildir, çünkü code point'in nasıl bellekte tutulacağının bilgisini içermez. byte olarak kaydetmek en mantıklısıdır ve çoğu text editor, bir dosyayı bir code page standartlarında kaydettiği zaman, byte olarak kaydeder. fakat bunu BCD'de kaydedebilir, yada farklı yöntemlerde tercih edebilir. bu yazılımın kendisine kalmıştır.

ms-windows kendi API'lerinde code page'lerin tümünü bu şekilde referanslıyor:

aşağıdaki tabloda utf-8'i de görmekteyiz. bunun sebebi; o code page'in barındırdığı tüm karakterler, utf-8 'in desteklediği tüm karakterlerdir.

aşağıdaK linkte "mac" keywordü içeren satırlar mevcut. bunun sebebi; mac'te kaydedilmiş dosyaları, windows tarafında okuyabilmektir. 

- [code_page_identifiers.md](https://github.com/yusufd89/notes/blob/master/code_page_identifiers.md)

# GILT

Globalization, Internationalization, Localization and Translation'ın kısaltmasıdır.

yazılım geliştirme sürecinde dil desteği için kullanılan terimlerdir.

### Translation (or T9N)

bir yazılımın text'lerinin başka bir dile çevrilme işlemidir.

### Localization (or l10n)

yazılım geliştirme sürecinde, içeriklerin ve bilgisayar yazılımlarının belirli bir coğrafyaya ya da etnik topluluğa özgü pazar ya da coğrafi bölgede geçerli yerel dilsel ve kültürel özelliklere uyarlanmasıdır. dolayısı ile; T9N'u ve daha fazlasını kapsar.

### Internationalization (i18n)

bir yazılımın birden fazla dili göre destekleme işlemidir.

### Globalization (or g11n)

i18n'i ve daha fazlaısnı kapsar. i18n olaya sadece metin bazında bakarken, g11n; kültürel açıdan da coğrafyalara uyumlu olabilmesini kapsar.

# a11y

accessibility özelliğini kazandırma işlemidir. GILT grubuna dahil değildir.

# i18n kütüphaneleri

örnek bir kütüphaneyi inceleyelim: jQuery.i18n

ilgili dildeki string karşılığını döndürüyor:

> $.i18n( 'message-key-sample1' ); 

#### Placeholder

```js
var message = "Welcome, $1";

$.i18n(message, 'Alice'); // This gives "Welcome, Alice" 
```

#### Plural (or çoğul)

```js
var message = "Found $1 {{PLURAL:$1|result|results}}";

$.i18n(message, 1); // This gives "Found 1 result"

$.i18n(message, 4); // This gives "Found 4 results"
```

yada

```js
var message = 'Box has {{PLURAL:$1|one egg|$1 eggs|12=a dozen eggs}}.';

$.i18n(message, 4 ); // Gives "Box has 4 eggs."

$.i18n(message, 12 ); // Gives "Box has a dozen eggs."
```

Yuakarıdaki örnek ingilizce içindir. Bazı dillerde çoğul kelime olduğunda yanındaki kelimelerde hiçbir fark meydana gelmezken, bazı dillerde ise 2'den fazla form olabilmektedir.

__Common Locale Data Repository (or CLDR)__, Unicode ekibininin public olarak yayınladığı çoğul kelimelerin sayılara göre nasıl değiştiğini açıklayan kurallar dökümantasyonudur. Hem dökümantasyon hem de parse edilebilmesi için XML olarak yayımlanır. Bu dökümantasyona göre parse eden program kütüphaneleri mevcuttur.

CLDR plural form bilgileri gibi birçok bilgi tutmaktadır. örnek:
- Locale-specific patterns for formatting and parsing: dates, times, timezones, numbers and currency values, measurement units...
- Translations of names: languages, scripts, countries and regions, currencies, eras, months, weekdays, day periods, time zones, cities, and time units, emoji characters and sequences (and search keywords),…
- Language & script information: characters used; plural cases; gender of lists; capitalization; rules for sorting & searching; writing direction; transliteration rules; rules for spelling out numbers; rules for segmenting text into graphemes, words, and sentences; keyboard layouts…
- Country information: language usage, currency information, calendar preference, week conventions,…
- Validity: Definitions, aliases, and validity information for Unicode locales, languages, scripts, regions, and extensions,…

Yukarıdaki örnekte "{{PLURAL:$1|res" kod kısmı PRURAL yazdığı için 2 parametre alıyor. Burada CDRL parser ingilizce için 2 adet form olduğunu biliyor. bu sebeple 2 parametre alıyor. yani;

ingilizce için: var message = "Found $1 {{PLURAL:$1|result|results}}";

arapça için:  var message = "Found $1 {{PLURAL:$1|zero|one|two|few|many|other}}";

eğer arapça için şunu yazarsak: {{PLURAL:$1|A|B}} o zaman 0 için A, diğer tüm değerler için B kullanılacaktır.

Yuakrıdaki "var message" aslında dil dosyasındaki json text'inden gelmelidir. 

#### Gender (or cinsiyet)

```js
var message = "$1 changed {{GENDER:$2|his|her}} profile picture";

$.i18n(message, 'Alice', 'female' ); // This gives "Alice changed her profile picture"

$.i18n(message, 'Bob', 'male' ); // This gives "Bob changed his profile picture"
```

#### Fallback

kütüphane init yapılırken ayarlanır. ğer bir tet'in karşılığını o andaki dilde bulamazsa, fallback olarak set edilen dil dosyasında arar. eğer onda da bulamazsa 2inci fallback dilini kontrol eder.

#### Message documentation

en.json, tr.json gibi dosyalar ile aynı dizinde qqq.json dosyası bulunması önerilir. bu dosya eun-time sırasında okunmaz/kullanılmaz. tranlator'ların okuması için bir dosyadır. key'ler yetersiz olduğunda translator bu dosyaya bakıp ne yazması gerektiğini çıkarır. örnek qqq.json dosyası:

```json
{

 "appname-title": "Application name",

 "appname-sub-title": "explanation of the application",

 "appname-about": "About this application text"

}
```

# Bir sayıyı metne çevirme or metinden sayıyı çevirme

örnek: 

> 105 --> yüz beş

> 1208 -> bin iki yüz sekiz

bu işlemler i18n gibi kütüphanelerin görevi değildir. bu sebeple ekstra kütüphane kullanmak gerekiyor. 2018 yılı itibari ile hala bu işi yapan düzgün ve multi-language kütüphane mevcut değil.

bunu yapan kütüphaneleri genelde "number to word" terimleri ile arama yapmak gerekiyor.

# Tipoğrafik İşaretler

resmi dilin noktalama işaretleri dışında kalan karakterlerdir. aslında birer anlama gelen şekillerdir. @, &, # gibi karakterlerdir.

bir dilde tipografik olan karakter başka dilde tpografik olmayabilir.

# Font

#### Type Family
karakterlerinin yapısını belirleyen kuralları içerir. örnek: Helvetica 

#### Typeface (or typeface family or font family)
bir ‘type family''ye ek olarak; bold, italic olup olmaması bilgisini birlikte içerir. örnek: Helvetica Bold.

#### Font
Typeface'e ek olarak; boyut bilgilerini içerir. örnek: Helvetica Bold 12px

#### font-face
tipografi'de geçen bir terim değildir. sadece css için font keyword'üdür.

#### serif
her karakterin uç kısımlarına ufak bir çizgiler koyulur. bu çizgiler seriftir. sans-serif ise bu çizgiler olmadan ki karakterleri temsil ediyor.

#### opentype vs truetype vs PostScript
alternatif font dosya saklama formatlarıdır.

#### tipoğrafi
metin yazmada kullanılan özellikleri inceleyen sanat dalıdır.

#### ClearType
Microsoft'un ekranlarda tüm fontları daha ince göstermek için geliştirdiği teknoloji. tüm fontları farklı bir biçime sokuyor. fontlar tasarlanırken özellikle ClearType'a uygun şekilde tasarlanırsa, ClearType daha başarılı oluyor. ClearType genel olarak LCD ekranlarda daha smooth bir görüntü yaratıyor.

# NLP (or Natural Language Processing or Doğal Dil İşleme)

"doğal dil"'den kasıt insan konuşması, yani; düzensiz konuşmadır.

NLP yapay zeka ve dilbilim alt kategorisidir. bu dal ile her türlü dili sözlü veya yazılı olarak anlama işlevleri yerine getirilmeye çalışılır. bunun için yazılımlar geliştirilmiştir. bu yazılımların örnek bazı görevleri ve YSA'ya bunun neresinde ihtiyaç duyulduğu:

- sesi algılayıp yazıya çevirme
  
  sesi tam olarak algılanamadığında YSA ile cümlenin akışına göre tahminleme de yapılabilir

- metni okuma

  bir metin okunduğunda birçok kişi farklı tonlarda okuyor. bu tonların daha düzgün olması için YSA'dan yararlanılıyor. eğer YSA olmadan metin okutulursa robotun okuduğu çok belli oluyor.

- dilbilgisi hata denetimi

  sadece hata denetimi için YSA işlevlerinden yararlanılmaz, fakat yanlış karakterler yerine düzgün kelime önerilerinde YSA'dan yararlanılabilir

- cümleyi veririz, bize her kelimenin kökünü ve detayını verir. örnek: "ben eve gidiyorum" dönüş olarak: [ {kok: ev, aldıgı-ek:"e", tip: nesne, adet: tekil, sıra: 2, verb:false ... } ... ]

- farklı dile çeviri işlemleri

  YSA ile çevrilecek konular daha net bir şekilde algılanıp diğer dile çevrilmesi kolay olabilir)

- OCR

  ysa bu metinlerin tam okunamadığı zamanlar tahminlemede kullanılıyor)

- bir cümleyi kategorileme: örnek banka uygulamamız olsun. müşteri istediği işlemi söyleyecek/yada yazacak bizde o işlemin ne olduğunu anlayıp işlemi gerçekleştiricez. müşteririnin verdiği cümle, bizim işlem uzayımızıdaki hangi cümle ile aynı kategoride olduğunu tespit/tahmin edebiliyor. örneğin; eğer tahmin oranı sonucu %90 oranla A işlemi çıktıysa, direk müşteriyi A işlemi sayfasına yönlendiririz. oysa %70 oranla A çıktıysa, müşteriye tekrar ne yapmak istediğini  şekilde açıklamasını isteriz. 

  burada YSA tahminleme oranlamasında kullanılıyor

genelde her dil için ayrı NLP yazılımları geliştiriliyor, fakat bu ortak yazılımların olmayacağı/olamayacağı anlamına gelmiyor.

# zemberek

özellikle Türkçe olmak üzere Türk dilleri için geliştirilmiş açık kaynak kodlu bir doğal dil işleme java kütüphanesidir. openoffice ve libreoffice için türkçe yazım denetimi eklentisi bu kütüphaneyi kullanır ve eklentide aynı ismi taşımaktadır.

# Optical character recognition (or optical character reader or OCR)

resim'den metin algılama işlemidir.

Tesseract komut satırı uygulaması (açık kaynaklı) bu işi yapmaktadır. engine olarak libtesseract'ı kullanmaktadır.

# open source NLP yazılımları

açık kaynaklı kütüphaneler mevcut. fakat henüz (2018 yılı) son kullanıcıya sunulacak derecede başarılı diiller. hiçbir NLP konusunda ticari olmayan NLP özelliği mevcut diil.

# google speech Api

google'ın speeach api'si client olan her taraftan çağrılabilmektedir.

google api'si sesi gerçek input-stream'ler ile gerçek zamanlı da alabiliyor. yani baştan sonra tek dosya halinde ses atılmak zorunda değil.

google sesi sunucularına atıyor. kişi sesini gereksiz seslerden arındırma yeteneğine sahip. sesi sadece metine çevirmekle kalmıyor, aynı zamanda her kelimenin yüzde kaç doğrulukla metne çevrildiği de tespit ediliyor ve yapay sinir ağı tüm cümleyi devrik olmayacak şekilde doğrulamaya çalışıyor. yapay siir ağı olduğundan; yüzde yüz bir sonuç olmuyor. google api'sinin result'ı bir string listesi oluyor. her elemanında kişinin kurduğu tüm cümle oluyor (baştan sona konuşması).

listesinin ilk elemanı google'ın en doğru düşündüğü cümle. ikinci elemanı daha az ihtimalle doğru olan cümle. listenin elemanı sıfıra yaklaştıkça daha yanlış sonuçlara gidilmektedir. her string elemanının bir de güvenilirlik oranı mevcut. böylece yazılımcı eğer ilk eleman en az %90 güvenilir diilse, uygulamaya işlem yapma gibisinden davranış sergiletebilir.

google-translate'ten daha başarısız oranla dili de otomatik algılayabiliyor. daha başarısız çünkü alfabetik harfleri göremiyor. sadece okunuşuyla değerlendiriyor. bu sebeple otomatik dil tanıma özelliği sunulmuyor.
