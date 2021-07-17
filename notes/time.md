############################

############################
# TIME
############################

############################

# zaman

zaman hesaplamalarında saniye referans olarak alınmaktadır.

saniyenin tanımı şu şekildedir: Uluslararası Birimler Sistemine göre saniye, en düşük enerji seviyesindeki Sezyum-133 atomunun iki hyperfine seviye arasındaki geçiş radyasyonunun 9.192.631.770 periyoduna karşılık gelen süredir.

Bir saniyeye denk gelen birçok farklı yöntem geliştirilmiştir. Bu sebeple her cihaz yıllar sonra ufak sapmalar meydana getirmektedir.

# TimeStamp (or Zaman damgası)

Fiziksel olarak zaman damgası; mürekkep ile belge üzerine basılan tarihtir. bu istenilen bir formatta olabilir. örneğin; etrafı çerçeveli, sadece gün/ay/yıl olan, ek olarak saati içerebilir gibi. Aynı şekilde elektronik ortamda da TimeStamp kullanılmaktadır. Bu değer istenilen formatta olabilir ve bazen sadece hesaplama ile bulunacak bir sayı ile temsil edilir.

> örnek1: unix timestamp

> örnek2: Tue 01-01-2009 6:00

> örnek3: 07:38, 11 December 2012 (UTC))

# Unix-Epoch time (or POSIX time or Unix time or seconds since the Epoch)
1 Ocak 1970 UTC+0 Grinviç tarihinin gece yarısından bu yana geçen zamanın saniyeler cinsinden değeridir. terminolojik olarak bakıldığında; herhangi bir formatta tarih gösterimi "timestamp" olduğundan, "Unix time" da bir çeşit 'timestamp'tir.

İlk olarak; 3 November 1971'deki "Unix Programmer's Manual (PDF) (1st ed.)"'inde tanımlanmıştır. kaynak: (source-id: 390). İlk tanımlandığında 32 bit ve '00:00:00, 1 January 1971'den itibarenki saniyeyi temsil ediyordu. 

# gösterim

zaman dilimi dünyanın herhangi bir yerinde aynıdır. sadece bölgesel olarak gösterilmek istendiğinde UTC+2 gibi ibarelerle gösterilirler. örneğin; aynı anda oluşturulan iki java-calendar objesi olsun. biri amerika biride türkiye bölgesine göre ayarlı olsun. bu değerler sadece ekrana basılırken farklıdır, aslında kendi içlerinde tuttukları "zaman" değeri ikisinde de aynıdır. yani; bu 2 calendar objesinin "Unix time"'ını alsak aynı değeri alırız.

# GMT (or Greenwich Mean Time)

Londra'nın Greenwich bölglesinden geçen sıfır meridyeninin referans alınarak yapılan saat dilimi sistemidir.

12 saat doğuda, 12 saat batıda parçalara bölünmüştür.

# Universal Time (or UT)
birçok versiyonu vardır. bunlar sürüm gibi düşünülmemelidir. hepsi birbirine alternatiftir.
- UTC (or Coordinated Universal Time)
- UT0
- UT1
- UT1R
- UT2

# Coordinated Universal Time (or UTC or Eş Güdümlü Evrensel Zaman)

- UTC'nin baş harflerinden kısaltma elde edilmemektedir. bunun sebebi tamamen siyasidir.

- UTC saniyeleri IS (ISO standart birimleri) standartlarına göre alır (atomik saniye). Oysa GMT astronomik değerlere göre saniyeyi baz alır. UTC bu sebeple daha güvenlidir. Fiziksel cisimlerin duruma göre değişmez. GMT'nin açılımı 'Greenwich Mean Time'dır. Buradaki 'Mean' ortalama anlamına gelir. Yani GMT de bir yıl güneşin ve dünyanın dönüşünü tamamlayacak ortalama en optimum düzeyde hesaplanmıştır ve bu şekilde kabul edilir. 

- GMT ve UTC arasında çok çok az bir zaman farkı vardır. Bu fark zaman geçtikçe artabilir or azalabilir. Çok ilerdeki tarihlerde fark çok açılabilir. 2019 yılına kadar, aradaki fark maximum 1 saniye olmuştur. Bu saniyelerde "__artık saniye (or leap second)__" uygulaması ile giderilmektedir. Leap second GMT'ye uygulanmaz. UTC'ye uygulanır. GMT'ye uyumlu olması için yapılan manuel değişikliktir. Bu değişiklik uluslararası birimler tarafından ortak karar alınarak yapılır.

# artık saniye (or leap second)
çok hassas hesaplamalar sonucu uluslararası alınan karar ile bazı günlerin sonuna (örnek 31 aralık gecesi) 1 saniye eklenmektedir yani 59:00'dan 00:00'a gçeiş 2 saniye sürmektedir.

- İlk artık saniye 1972'de uygulanmıştır.
- Şu ana dek (yıl 2019) sadece Haziran ve Aralık (yılın sonu ve ortası) aylarında artık saniye uygulanmıştır.
- Bazı yıllarda hem aralık hem de haziran ayı artık saniye uygulanmıştır.
- (source-id: 391) sayfasının "Announced leap seconds to date" başlığında uygulanan tüm artık saniyeler listelenmektedir.

POSIX time'da bu saniye ignore edilir (yani saniye ekleme yada çıkarma yapılmaz). kaynak: (source-id: 392) "A.4.16 Seconds Since the Epoch" başlığı ilk paragraf.

# artık yıl (or leap year)
miladi takvimde yaşanan bir durumdur.

dünya güneş etrafında 365.24 küsür günde dönüyor. miladi takvime göre; her yıl 365 kabul edilmiştir. 4 yılda bir kere 29 şubat kullanılmaktadır. 29 şubat olan yıla "artık yıl" denir. artık yılın 4 senede bir olmasının bazı istisnası vardır:

istisnaya bir örnek: 100'ün katlarından 400'e kalansız bölünenler artık yıl diildir. örnek: 1600 artık yıldır. 1700 diildir. (bunun sebebi 1 yılın 365.24 küsür olması. 0.25(1/4) değil).

# UTC mi GMT mi "Unix-Epoch time" mi kulanmak gerekir?

Örneğin, uzayda herhangi bir gezegende yada noktada, örneğin uydulardaki astronotların, GMT ile bilgi alışverişi yapması best bractice olmayacaktır. orda UTC kullanılmalıdır. Çünkü UTC atomik saniyeyi baz alır.

GMT'yi eledik. Unix-Epoch time ve UTC kullanmak ikiside doğrudur. UTC kullanılabiliyorsa tercih edilmelidir. sebepleri:
- debug işlemlerini çok hızlandıracaktır çünkü direk okunduğunda değerin ne olduğu human-readable'dır.
- Unix-Epoch saniye bazında zaman tutuyor. eğer saniyeden ufak bir bilgi (birim) tutmaya ihtiyacımız olursa sorun yaşayabiliriz. Ek not: Unix-Epoch time için bazı kütüphaneler saniyeden ufak birimleri desteklemek için noktadan sonrasında da karakter desteklemektedir (örnek: 123456789.123). Fakat bunun resmi bir standartı yoktur. Dolayısı ile kullanmamakta fayda var.

Not: Özellikle string yerine integer gibi değerlerle kullanılan formatlarda birçok farklı problem de yaşanabiliyor:
- Y2K bug: 2000 yılına girildiğinde, yıl değerinin sadece son iki hanesini tutan sistemler sorun yaşamıştır.
- Y2K38 bug: signed 32 bit integer ile tututal Unix-Epoch değerleri, "03:14:07 UTC on 19 January 2038" sonrasını gösteremeyecek, onun yerine sıfır değerine resetlenecek yada hata fırlatacaktır.
- diğerleri: (source-id: 393)

# güneş zamanı (or solar time)

Güneş'in ve dünyanın konumunu temel alan zaman birimleridir. temel zaman birimi gündür. ingilizcede gün'e 'solar day' de denir.

# Yaz saati uygulaması

DÜnyanın bazı ülkelerinde uygulanırken bazılarında uygulanmamaktadır. Genelde avrupada ve amerikada kullanılıyor. Yaz saati uygulaması varken türkiye; kış ve yaz, UTC+3 ve UTC+2 arasında değiştirirdi. Her ülke kendi yasalarınca saatleri kendi belirlediği için, her ülkenin saati meridyene göre hesaplanamamaktadır.

# timezone

dünyanın birçok noktasında timezone'lar belirlenmiştir. genelde her ülkenin bir timzone noktası vardır. ve bu noktanın etrafındaki belli bir bölge aynı saati kullanır.

confrafya ve ticari sebeplerden birden fazla timezone noktası aynı ülkede olabilir. bu noktalar için saatin kaç olacağı da sadece meridyene göre belirlenmemektedir. ticari ve siyasi sebeplerden meridyenle alakasız saat farkları olabilir. aynı zamanda; yaz saati uygulaması gibi belli dönemler aynı noktadaki saatler farklılık gösterebilir.

Timezone yıllara göre ve bölgeye göre (ülkeye göre olmak zorunda diil) değişmektedir. Örneğin;

- moment-js-with-data kütüphanesi yıllara göre timezone'u buradan almaktadır: (source-id: 394) kaynak: (source-id: 395) "mj1856" commented on Jul 27, 2016. 1inci paragraf.

- jdk'da bulunan timezone'u güncellemek için açık kaynaklı bir updater var. Bu updater'da bilgileri IANA'dan almaktadır. kaynak: (source-id: 396). Jdk sürümü eski kalsın isteyenler fakat time-zone bilgisine ihtiyaç duyan canlı'da olan projeler için gelilştirmiş bir tool(updater) bu.

not: unutulmamalıdır ki; yaz saati veya benzeri bir uygulama 100 yıl boyunca X noktasında aynı kuralla tekrar edilmemektedir. örneğin; türkiye +03:00 kuralına 2014 ile geçilmiştir. bundan önceki yıllarda oradaki timezon +02:00'dır.

Timezone'lar text olarak gösterilmek istendiğinde; KıtaAdı/ŞehirAdı formatı kullanılmaktadır. bu resmi bir format değildir. fakat genelde böyle kullanılır. Örneğin; Europe/Istanbul, America/Chicago. Bazı yerler için sadece direk ülke yada şehir ismi kullanıldığı da olur.

örneğin türkiye için 3 farklı gösterim ile karşılaşılabilir:
- Europe/Istanbul
- Asia/Istanbul
- Turkey

# özel timezone isimleri

Özellikle sık kullanılan timezone'lara bu şekilde eş anlamlı kelimeler atanmıştır. örnek: 

- UTC+2, "Eastern European Time (or EET)" ile eş anlamlı kullanılır.

- "Eastern European Summer Time (or EEST)" ise UTC+3 ile eş anlamlıdır.

Politik sebeplerden "Central Africa Time (or CAT)" ve "South African Standard Time (or SAST)" UTC+2 ile eş anlamlıdır.

Yani bir timezone'un birçok eş anlamlı ismi olabilir. genelde sık kullanılanlara bu tarz takma isimler atarlar. Bir ülke (or bir bölge) belli bir zaman diliminde (örneğin kışın ve bahar mevsimleri) EET kullanır, fakat yaz mevsimine geçerken EEST kullanabilir. Yani; EET kendi içinde kış veya yaz olarak farklı saat dilimlerine geçiş yapmamaktadır.

# mevsim (or season)
mevsimler programatik olarak bulunması gerektiğinde ay bazında değil gün bazında bulunduğu unutulmamalıdır. örneğin 23 Eylül öncesi kuzeyde yaz mevsimi iken, 23 eylül sonrası sonbahardır. aynı tarihlerde güney yarımküredeki ülkeler için zıt mevsimlerdir. bu durumda son kullancıın kendi IP'sinden lokasyon tespiti yapmak gerekebilir.

# astronomical seasons vs meteorological seasons

İngiltere ve daha kuzeyinde, ırak ve daha güneyinde meteorological mevsim tarihleri kullanılmaktadır. yani mevsimler aynı fakat  başlangıç ve bitiş tarihleri vardır. meteorological mevsimler hava durumuna göre ayarlanmaktadır. oysa astronomical mevsimler dünyanın güneş etrafındaki dönüşüne göre ayarlanmaktadır. 

bazı ülkelerde mevsimler, o ülkelerin resmi dil kurumlarınca daha fazla sayıya bölünmüştür.

# Gregorian calendar (or miladi takvim or tr:Gregoryen takvimi)

milat: İsa'nın doğduğu gün'dür. bugünü başlangıç yılı ve 1 yılı 365 gün kabul eden takvimdir.

# takvim
tüm zaman kavramlarını ele alan zaman sistemidir: gün, saat, yılın kaç ay olduğu, ay isimleri ve hangi ayın kaç gün olduğu...

Gregorian takvimi en çok kullanılan takvim. fakat bazı ülkelerde hala diğer takvimler %50'ye yakın oranla kullanılmaktadır (istatisitk tarihi: 2017). örnek:

- Hicri takvim (or Müslüman takvimi or İslami takvim or Hijri calendar)
  
  Muhammed'in Mekke'den Medine'ye yolculuğunu başlangıç yılı (1. yıl) kabul eden ve 1 yılı 354 ya da 355 gün olan takvimdir. orta-doğu ülkelerinde kullanılmaktadır.

- Hebrew calendar (or Jewish calendar or İbrani takvimi or Yahudi takvimi or Musevi takvimi) - israil

- Etiyopya takvimi (or Ethiopian calendar) - Etiyopya ülkesinde kullnılan takvim

- Buddhist calendar - Thailand, Sri Lanka (ve onlara yakın bazı ülkeler)

- Hindu calendar (Indian national calendar yada Shalivahana Shaka calendar yada Saka calendar) - hindistan

- Hint takvimi - sadece eskiden Hinduizm'de kullanılan bir takvimdir.

- Jülyen takvimi (or Julian calendar) - batı tarafından Miladi takvim'in kabulüne kadar (1582 yılı) kullanılan takvimdir.

Yukarıdaki takvim sistemleride kendi içlerinde yıllar içinde değişime uğramıştır.

# yılbaşı (or new year's day)

her takvimde yılbaşı farklı gün olabilir. isa'nın doğduğu günün kesin olmaması sebebi ile, Jülyen takvimini kullanan ülkeler farklı tarihlerde isa'nın doğumunu kutluyordu. bazıları 25 aralığı doğduğu gün olarak sayıyor, ve 25 aralığı temsilen yılbaşı olarak sayıyorlardı. bazı bölgelerde ise bu 1 ocak'tı. daha sonra Gregorian takvimine geçildiğinde isanın doğuşu 25 aralık (noel), 1 ocak ise yılbaşı olarak belirlendi.

# resmi tatil (or public holiday or legal holiday)

milli bayram (or national holiday) ve din bayramları, başlıktakilerin birer altkümesi olarak ayrılır. başlıktaki terimler sadece kurumların kapalı olduğunu belirten terimlerdir.

programatik olarak bu bilgileri her ülke için elde etmek zordur. her ülkenin resmi tatilleri yaşanan olaylar sebebi ile değişebilmektedir. türkiye'de 15 temmuz'un tatil oluşu gibi. "Administrative division (or idari bölünme)" başlığına benzer bir durum söz konusudur.

benzer şekilde mezhepler de kendi içlerinde farklı mezhepler türettiklerinden her bölgede aynı bayramlar aynı tarihte kutlanmamaktadır. 

# Bank holiday

bu terim sadece ingiltere ve birkaç ülkede kullanılan bir terimdir. her ülkede ise farklı anlama gelmektedir. örneğin; ingiltere'de resmi tatilleri kapsarken, irlanda'da sadece banka'ların tatil olduğu günleri temsil eder.

# time vs date vs datetime

- time: saat/dakika/saniye gibi bilgileri içeriyor.
- date: günün yıl içerisindeki yerini tutuyor
- datetime: hem date hemde time'ı içerir.

# java.sql.Date

java.util.Date'ten extend etmiştir. sql.Date time bilgisini içermez sadece date içerir. "time" bilgisi, java.util.Date'te olduğundan extend etmiş sınıfta da vardır. buna çözüm olarak java.sql.Date bu değerleri sıfır olarak set edilir. Benzer durum java.sql.Time 'da da vardır: date bilgisi 0'dır.

# java.sql.Time 

java.util.Date'ten extend etmiştir. date bilgisi içermez fakat time içerir.

# java.sql.Timestamp

java.util.Date'ten extend etmiştir. java.util.date'e ekstradan nanosecond da içerir. java.util.date en ufak birimi millisecond'dır.

# java.util.Calendar

java.util.Date'e alternatif java 7 ile gelen takvim sınıfıdır. java.util.Calendar abstractır bu sebeple direk kullanılamaz. GregorianCalendar ise onu extends etmiştir.

# java.time.*

java.util.Calendar'e alternatif java 8 ile gelen takvim paketidir. java.util.date ve java.util.calendar geriye uyumluluk için hala java içerisinden kaldırılmamıştır.

# Joda Time

java için date ve calendar'ın eksiklikleri sebebi ile geliştirilen kütüphane. java 8 ile gelen java.time.# joda'nın forkudur. java 8 çıktığında joda projesi artık resmi olarak gereksiz olmuş ve geliştirilmeme kararı alınmıştır.

# min time unit

| name               | support min time unit  |
|--------------------|------------------------|
| epoch time         | second                 |
| joda               | millisecond            |
| java.time          | nanosecond             |
| java.util.Date     | millisecond            |
| java.util.Calendar | millisecond            |
| java.sql.Time      | millisecond            |
| java.sql.TimeStamp | nanoseconds            |

# java.time.*

__LocalDate__ sadece gün ay yıl tutuyor.

```java
// init metodları
LocalDate localDate = LocalDate.now();
LocalDate.of(2015, 02, 20);
LocalDate.parse("2015-02-20");

// diğer metodlar
LocalDate tomorrow = LocalDate.now().plusDays(1);

// ChronoUnit, java.time.* içindeki özel bir obje
LocalDate previousMonthSameDay = LocalDate.now().minus(1, ChronoUnit.MONTHS);

// Period, java.time.* içindeki özel bir obje.
// Period date birimleri ile ilgilenirken, Duration sınıfı time birimleri ile ilgilenir.
LocalDate finalDate = initialDate.plus(Period.ofDays(5));


DayOfWeek sunday = LocalDate.parse("2016-06-12").getDayOfWeek();

int twelve = LocalDate.parse("2016-06-12").getDayOfMonth();

boolean notBefore = LocalDate.parse("2016-06-12")
  .isBefore(LocalDate.parse("2016-06-11"));
```

__LocalTime__ sadece saat, dakika, saniye ve ek olarak nano seviyesinde bilgi tutuyor.

```java
// init metodları
LocalTime now = LocalTime.now();
LocalTime sixThirty = LocalTime.parse("06:30");

//diğer metodlar
LocalTime sevenThirty = LocalTime.parse("06:30").plus(1, ChronoUnit.HOURS);

LocalTime localtime = LocalTime.parse("00:01:02.5");
//prints: "seconds: 2 nano seconds: 500000000"
System.out.println("seconds: " + localtime.getSecond() + " nano seconds: " + localtime.getNano() );
```

Yukarıdaki kod'da "nano" tüm zamanın nano seviyesindeki karşılığını döndürmüyor.

__LocalDateTime__ date ve time'ı birlikte tutar. LocalTime ve LocalDate ile aynı isimde metodlar sunar.

__ZonedDateTime__; LocalDateTime'e ek olarak time zone bilgisini de tutar. zone bilgisi bölgesel bir bilgidir. Yani; kanunlar gereği bir conrafi bölgedeki saat dilimi değiştirildiğinde, ZonedDateTime değeri de otomatik değişecektir.

__OffsetDateTime__ ZonedDateTime ile aynıdır. tek farkı zone bilgisi değil, sadece offset bilgisi tutar. bu sebeple;kanunlar gereği bir coğrafi bölgedeki saat dilimi değiştirildiğinde OffsetDateTime sınıfının değeri etkilenmez. çünkü OffsetDateTime sadece "+03:00" gibi offset değeri tutar. oysa ZonedDateTime "Asia/Turkey" gibi bir değer tutar.

```java
ZoneId zoneId = ZoneId.of("Europe/Paris");
Set<String> allZoneIds = ZoneId.getAvailableZoneIds();

ZonedDateTime zz = ZonedDateTime.parse("2015-05-03T10:15:30.5+01:00[Europe/Paris]");
ZonedDateTime zonedDateTime = ZonedDateTime.of(localDateTime, zoneId); // LocalDateTime objesine timezone ekler.
```

__ZonedDateTime__ parse ve toString metodlarında ISO 8601 formatını kullanır. tek istisna opsiyonel olarak timezone'un isim olarak \[Europe/Paris] şekilde yazılabilmesidir.

# javax.xml.datatype.XMLGregorianCalendar

jre içinde bulunan bir interface. implementasonu da burda: 

> com.sun.org.apache.xerces.internal.jaxp.datatype.XMLGregorianCalendarImpl

W3C'ün XML şemalarında birçok farklı tip vardır (base64Binary, boolean..). bunların arasında zaman ile ilgili data tipleri de vardır. örnek:

gYearMonth, gYear, dateTime, time, date...

XML üzerinde örneklersek:

```xml
<myxlmroot>

 <TestgYearMonth>1999-02</TestgYearMonth>

 <testAnyelement>1</testAnyelement>

 <TestdateTime>2002-10-10T12:00:00-05:00</TestdateTime>

</myxlmroot>
```

Yukarıda 1999-02 stringinini hangi formata olacağı W3C tarafından belirlenmiştir. Eğer xsd dosyası bu xml elementinin bir W3C XML şeması olduğunu gösteriyorsa o zaman Java'daki XML to object parser'lar bunu Javadaki XMLGregorianCalendarImpl'a çeviririyor. Yukarıdaki xml şu java sınıfına döndürülüyor:

```java
public class Myxlmroot {

private XMLGregorianCalendar testgYearMonth;

private int testAnyelement;

private XMLGregorianCalendar testdateTime;

//getter setters

}
```

XMLGregorianCalendarImpl gYear, gYearMonth gibi tüm değerleri tek bir sınıftan okuyabilmemizi sağlıyor. getXMLSchemaType() metodu bize XMLGregorianCalendar'in hangi şemadan (gYearMonth, time)  xml'e çevrildiğini döndürüyor.

XMLGregorianCalendar kendi içinde date time işlemleri yapmıyor. zaten gün ekleme çıkarma gibi işlem yaptıran public metodlar sunmuyor. sadece set/get, birçok constructor ve birkaç utility metodu mevcut. XMLGregorianCalendar kendi içinde GregorianCalendar'ı kullanıyor (fakat ondan extend etmemiş).

# ISO 8601

date time format standardıdır. formatta esneklikler vardır. bazı değerler gösterilebilir yada gösterilmeyebilir.

- Gregorian calendar veya UTC kullanılır.

- TZD, time zone designator'ın kısaltmasıdır ve formatta +hh:mm seklinde gösterilir. sadece Z kullanılırsa +00:00 anlamına gelir. (Z harfi "Zulu time"'dan gelmektedir. Zulu kelimesi NATO'nun kendi içinde Z karakteri için kullandığı bir kodlamadır)

- T işareti ise date'in bittiği ve time'a geçilen kısma atılır.

- DD ve diğerleri her zaman çift hane olmak zorunda. 01 yerine 1 yazılamaz.

- AM/PM ayrımı yoktur. 24 saat özelliği kullanılır.

- örnekler;

  - YYYY-MM --> 1997-07

  - YYYY-MM-DDThh:mm:ssTZD --> 1997-07-16T19:20:30+01:00

  - YYYY-MM-DDThh:mm:ss.sTZD --> 1997-07-16T19:20:30.45+01:00

- mm ve MM ayırt edilebilmesi için küçük büyük olup olmadıkları önemlidir.

- eğer 's' karakteri var ise; en az 1 karakter olmak zorundadır. maximum kaç karakter olacağı standartlarda belirtilmemiştir. aslında 's' millisecond değildir. bu kısım yazılımcının kendisine kalmıştır.

- ISO 8601'de haftalar pazartesi ile başlar. senenin başında hafta ancak pazartesi ise başlar. yani 1inci hafta ilk pazartesi olan haftadır. örnek 1 ocak çarşamba günü ise; 1 ocak hala eski yılın son haftasıdır.

  haftalar da output olarak basılabilir. örnek: 2018-W08 Format: YYYY-Www

# SimpleDateFormatter

Java içinde gelen SimpleDateFormatter'ın kendine özgü formatı vardır (global anlamda bir standart değildir). 

- YYYY-MM-DDThh:mm:ss kabul etmez. T harfini ' tırnak içinde ister: YYYY-MM-DD'T'hh:mm:ss

- YYYY'yi büyük harf olduğundan kabul tanımamaktadır. küçük harf olması şarttır.

- MMMMM ay'ın kelime karşılığını yazıyor: Mart, July gibi.

- a, AM PM 'i ekrana basıyor.  

- küçük s second, büyük S millisecond anlamına geliyor. ss hep iki karakter olmak zorunda iken, SSS 3 karakter olmak zorundadır.

- yy yılın son 2 karakterini ekrana basacaktır. örneğin yıl 2012 ise; 12 basacaktır. 

- yyyyy; yıl 2012 ise ekrana 02012 basacaktır.

daha fazla detay: (source-id: 446)

# millisecond (or ms)

saniyenin 1000'de biri.

# salise

Saniyenin 1/60'ıdır. bu terimin ingilizce karşılığı yok.

# AM ve PM

Kısaltmalar Latince kelimelerden geliyor.

AM/PM sistemi "__12-hour clock__" sistemidir. "__24-hour clock__" sistemine (formatına) alternatif olarak kullanılır.

AM = A.M = Ante meridiem = Before noon = before midday = öğleden önce = ö.ö. = gece yarısı(00:00) ve öğlene kadar(12:00) olan süre

PM = P.M = Post meridiem = After noon = after midday = öğleden sonra = ö.s. = öğleden gece yarısına kadar olan süre

# bazı terimlerin ingilizceleri

aşağıdaki terimlerin resmi saat aralıkları yoktur.

- Öğle (or öğlen or midday or noon)

- afternoon (or ikindi)

- akşam (or evening)

- gece (or night)

- gece yarısı (or midnight)

# 0 yılı öncesi ve sonrası

CE = MS = M.S. = Milattan Sonra = Common Era = Current Era = Christian Era = İsa'dan Sonra = İS = İ.S. = Anno Domini (efendimizin yılı anlamına geliyor) = AD

BCE = MÖ = M.Ö. = Milattan Önce = Before Common Era = İsa'dan Önce = İÖ = İ.Ö. = BC = before Christ

# 00:00:00

time değerleri sıfır olduğunda o günün başlangıcını temsil etmektedir. 00:00 yerine 24:00 da resmi olarak kullanılabilir.
