############################

############################
# OTHERS
############################

############################

# python
- python dili jvm gibi runtime'a ihtiyaç duyar. garbage collector de mevctuttur.
- open source'tur.
- basit ve üst seviyeli bir dildir.
- python'un gömülü (npm gibi) paket yöneticisi vardır. ismi: "pip".
- komut satırında interactive arayüz sunar.
- gömülü birçok datatipi mevcuttur ve bunlar için API'lar sunar.
- dinamik tipler mevcut (tipinin deklere etmeye gerek kalınmayan instance'lar oluşturulailiyor)

Java ile karşılaştırıldığında son 3 özellik python'da daha iyidir. Javascript zaten nodejs ile masaüstü dünyasında çalışabilir duruma geldi. python bu sebeple masaüstü uygulamalarda yaygınlaştı. özellikle data-tiplerine olan native/built-in desteği sayesinde de "data science" (data mining, machine learning, big data, yapay zeka, data analizi) konularında birçok kütüphane python için yazıldı.

python birçok linux dağıtımında yüklü gelir. çünkü linuxta birçok uygulama python ile yazılmıştır. örneğin: yum paket manager python ile yazılmıştır. kaynak: (source-id: 29) 2inci paragraf. Default yüklü gelen sistemsel uygulamalar python'un yüklü gelen versiyonunu kullandığı için, python sürümünü değiştirmek bazen sıkıntılara yol açabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Memoization
Memoization performance'ı arttırmak için kullanılan bir tekniktir. Memoization tekniğinde; çağrılan fonksiyonların sonuçlarını bi yerde saklarız. bu şekilde tekrar aynı parametrelerde fonksiyon çağrılmak istendiğinde, sonucu sakladığımız yerden okuruz.

# dynamic programming (or dinamik programlama)
bir çeşit matematiksel optimizasyon tekniği olduğu için bazı kaynaklarda __dinamik optimizasyon (or dynamic optimizasyon)__ olarak geçer.

dynamic programming ile yazılan kodlar recursive veya iterative olabilir.

dynamic programming, problemi, sub-problemlere bölerek çözme yöntemidir. fakat bunu yaparken örtüşen (overlapping) olan bölümleri de ilişkilendirip performance'tan kazanmaya çalışan çözümler olması şarttır. örneğin; fibanocci'yi iterative kod ile memoisation ile çözersek, dynamic programming yapmış oluruz.

not: dynamic programming ve Memoization terimi birçok kaynakta yanlış anlamda kullanılıyor. Bazı kaynaklar top-down design veya bottom-up design yerine kullanıyorlar. fonksiyon implemente edildikçe top-down design veya bottom-up design ile aynı kapıya çıktığı doğru, fakat terminolojik olarak kök sebepleri farklı.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Özyinelemeli (or Recursive) solution vs Tekrarlamalı (or Iterative) solution
recursive kod dha fazla cpu ve ram harcar çünkü arkaplanda program her çağrılan fonksiyon için yeni bir call-stack açar. iterative kod ise görünürde daha uzundur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Syntactic sugar
programlama dillerinde insan için kolaylaştırılmak üzere geliştirilmiş syntax'a verilen isimdir. örneğin; C dilinde:

```c
a[i]
```

buna denk gelmektedir:

```c
*(a + i)
```

İşte bu durum Syntactic sugar olarak adlandırılır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# multitier architecture (or n-tier architecture) vs multilayer architecture (or n-layer architecture)
tier ve layer'ın kelime anlamları birbirine çok yakın (aynı denebilir, fakat belki detaylarda ayrılıyordur. tam bilmiyorum.). bu sebeple piyasada birbiri yerine kullanılıyor. fakat "layer", logical olarak aynı runtime'da birbirinden ayrılmış iş katmanlarını temsil eder. Örneğin; businnes layer, database-crud-services layer gibi... Sadece businnes ve database-crud-services olan bir yazılım 2-layered application'dır.

Oysa "tier" terimi fiziksel olarak ayrı olan katmanları temsil etmek için kullanılıyor. Örneğin; UI layer, busines service...

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# core dump (or memory dump or crash dump or system dump or ABEND dump)
dump kelime anlamı: çöplerin toplantığı yer.

Yazılım işletim sistemi tarafından zorla kapatılırsa memory'deki bilgisi ve diğer ek bilgiler bir dosyaya saklanır. bu şekilde daha sonra bu dosya analiz edilebilir. bu dosya core dump denir.

Eğer yazılımın memory'deki alanı dosyaya uygulama sağlıklı çalışırken alınırsa buna __snapshot dump (or snap dump)__ denir.

executable dosya çalıştırıldığında RAM'e yüklenir ("memory structure" başlığında anlatılıyor). Bu sebeple core dump içerisinde executable'ı bulabiliriz. Bu sebeple bazı kaynaklarda, core-dump'ın formatının, executable formatı olduğu yazar fakat bu tam olarak doru dil. Core dump'ta extra bilgiler (RAM'deki diğer bölgeler) de vardır.

core dumb'ın boyutu büyük olduğu ve kötü niyetliler tarafından okunabilir olduğu (güvenlik açığı yaratabileceği) için OS'lar genelde default'ta core dump yazmaz. Bunun için OS'a ayar çekmek gerekebilir. Bu ayarlar aynı çekirdekli OS'larda bile, OS'tan OS'a farketmektedir.

# GNU Project Debugger (or gdb)
Assembly, C, C++ , Objective-C, go, Fortran, Pascal, Rust  gibi dilleri komut satırından debug edebilmemizi sağlar. şu şekilde başlatılır:

```sh
gdb "/path/to/executable"
```

isteğe bağlı olarak core dump dosyasını da partametre alırsa, ayağa kaldırdığı uygulamayı direk bu state ile başlatır:

```sh
gdb "/path/to/executable" "/path/to/core_dump_file"
```

# Java core dump

- java core dump'ı dosyaya yazarken "hprof" formatını kullanır. 

- Java out-of-memory hatası verdiğinde core dump istiyorsak java app'imizi bu patrametrelerle başlatmalıyız:

```sh
java -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=<dump-file-path>
```

- Çalışmakta olan java uygulamasının dump'ını istersen şu şekilde alabiliriz:

```sh
jmap -dump:live,format=b,file=<dump-file-path> <java-process-id>
```

- JDK içerisinde gelen jvisualvm ile GUI üzerinden herhangi bir java uygulamasının aşağıdaki bilgilerini görebiliriz:
  - hangi parametrelerle başlatılmış
  - System.properties'te nelerin olduğu
  - historical CPU and memory usage
  - historical threads with states (waiting, running...)
  - and others...

jvisualvm ile bir uygulamanın thread-dump'ını alırsak, her thread'in hangi statüde ve hangi kod satırında olduğunu (stack-trace'i) görebiliriz.

Şu programımızı örnek alalım:

```java
public class MainAppX {

  public static void main(String[] args) throws InterruptedException {
      custom1();
  }

  private static void custom1() throws InterruptedException {
      
      while (true){
          System.out.println("for loop resume");
      }
  }
}
```

thread dump'ın bir kısmı bu şekilde olur:

```
"main" #1 prio=5 os_prio=0 tid=0x000002662e4b0000 nid=0xc1c4 waiting on condition [0x0000006bce5ff000]
   java.lang.Thread.State: TIMED_WAITING (sleeping)
        at java.lang.Thread.sleep(Native Method)
        at MainAppX.custom1(MainAppX.java:13)
        at MainAppX.main(MainAppX.java:7)

   Locked ownable synchronizers:
        - None

"VM Thread" os_prio=2 tid=0x0000026649a73800 nid=0xbc94 runnable 

"GC task thread#0 (ParallelGC)" os_prio=0 tid=0x000002662e4c7800 nid=0xb41c runnable 

"GC task thread#1 (ParallelGC)" os_prio=0 tid=0x000002662e4ca000 nid=0x4900 runnable 
```

Görüldüğü üzere JVM'inde application'ımıza bağlı bazı thread'leri var.

Eğer app'imizin Head dump'ını alırsak; her class'ın ayrı ayrı kaç adet instance'ı var görebiliyoruz ve her instance içindeki field'larn değerlerini görebiliyoruz.

# (for VisualVM) profiler vs sampler
profiling temelde instrumentation yöntemini kullanarak çalışır.

profiler runtime'da çalışan uygulamamıza bytecode ekleyerek müdahele eder. oysa sampler böyle bir yöntem uygulamaz. bu yüzden sampler daha hızlıdır. fakat profiler daha çok farklı bilgiler sunar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# HTTP exception practices

- facebook

```sh
curl -X GET https://graph.facebook.com/oauth/access_token?client_id=foo&client_secret=bar&grant_type=baz
```

```json
{
    "error": {
        "message": "Missing redirect_uri parameter.",
        "type": "OAuthException",
        "code": 191,
        "fbtrace_id": "AWswcVwbcqf6546546546"
    }
}
```

- twitter

```sh
curl -X GET https://api.twitter.com/1.1/statuses/update.json?include_entities=true
```

```json
{
    "errors": [
        {
            "code":215,
            "message":"Bad Authentication data."
        }
    ]
}
```

- default spring error

```sh
curl -X GET -H "Accept: application/json" http://localhost:8082/spring-rest/api/book/1
```

```json
{
    "timestamp":"2019-09-16T22:14:45.624+0000",
    "status":500,
    "error":"Internal Server Error",
    "message":"No message available",
    "path":"/api/book/1"
}
```

- google

```json
{
 "error": {
      "errors": [
              {
                "domain": "global",
                "reason": "invalidParameter",
                "message": "Invalid string value: 'asdf'. Allowed values: [mostpopular]",
                "locationType": "parameter",
                "location": "chart"
              }
      ],
  "code": 400,
  "message": "Invalid string value: 'asdf'. Allowed values: [mostpopular]"
 }
}
```

# rfc7807
bu rfc'de exception için standart yaratılmak istenmiş. 5 bilgi döndürüyor:

örnek:

```json
{
    // URL (or path) of help document.
    // "about:blank" bu konu hakkında doc olmadığında konuyulabilecek değer olarak reserve edilmiş durumda.
    "type": "http://www.mywebsite.com/help-doc/errors/incorrect-user-pass",

    // human readable title (shorter then "detail").
    "title": "Incorrect username or password.",
    
    // HTTP status code.
    // Bu zaten header'da geliyor. Fkata bazı durumlarda proxy server'lar HTTP status code'u header'da değiştirebiliyor. Buna karşı alınan bir önlem gibi düşünülebilir.
    "status": 401,

    // human readable message.
    "detail": "Authentication failed due to incorrect username or password.",
    
    // URI of error.
    // Burası URL de olabilir. Sadece identifier (URI) olması yeterli.
    "instance": "/login/jack"
}
```

Standratta isteğe bağlı olarak ek parametreler eklenebileceği belirtilmiş. kaynak: (source-id: 30) title: "3.2. Extension Members".

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# fail-fast vs fail-safe
fail-fast bir sistem internal bir error durumunda, o anda, dışarıya sundupu interface üzerinden hata döner. Oysa fail-safe bir sistem hata olması durumunda olabilecek diğer senaryoları tamamlar ve sonrasında dönüş yapar. Fail-safe sistem dönüş yaptığında içerde hata aldığını belirtip belirtmemesi bu konu dışındadır.

örneğin java'da bazı collection'larda for-loop içerisinde modifikasyon yapıldığında, diğer döngüye girildiğinde ConcurrentModificationException hatası alınır. İşte bu hata döngü tamamlanmadan verildiği için fail-fast'tir.

nor: java doc'ları detaylı okunduğunda şu görülürki; ConcurrentModificationException her zaman fırlatılmayabilir. yani bu hatanın fırlatılacağı garanti edilmez.

ConcurrentModificationException iterator kullanıp, collection elemanı silinirse veya eklenirse bu hata fırlatılır (daha doğrusu; fırlatılabilir). Eleman silme işi collection.remove() ile değil, iterator.remove() ile yapılmalıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# dead-letter queue (or DLQ)
Servis bus'larda kullanılan özel bir queue'dur. bir service-bus'a mesaj yollamak isteyelim. mesaj service-bus'a ulaşır fakat;
1- service-bus tarafından kabul edilemezse (herhangi bir sebepten ötürü: queue doluluğu gibi...)
2- yada service-bus'tan consumer mesajı okur ve consumer'ın ilgili thread'i hata fırlatır ise

service-bus bu mesajı DLQ'ya ekler. DLQ'da bir queue'dur.

yukarıdaki tüm bilgiler için kaynak: (source-id: 31) "The dead-letter queue" başlığı, 1 ve 2inci paragraf.

DLQ'ya hangi durumlarda mesajın atılacağı, DLQ'mun boşaltılma süresi, kimlerin DLQ'dan okuma yapabileceği gibi policy'ler service-bus implementasyonundan implementasyona fark edebilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# data warehouse (or DW or DWH or veri ambarı or bilgi ambarı or enterprise data warehouse or EDW)
ilişkili verilerin sorgulandığı ve analizlerinin yapılabildiği bir yazılımdır. Sadece veritabanı değil, verileri sabit diskten okuyan (load eden), verinin transformasyonu yapan yazılımlarla birlikte bu kümenin içindedir.

# data mart
mart kelime anlamı: çarşı, pazar, trade center

data mart is a simple form of a data warehouse that is focused on a single subject (or functional area). Data mart'lardan veri çekmek daha kolaydır. Çünkü daha client-centric (client isteklerine uygun) data tutulur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Continuous integration vs continuous delivery vs continuous deployment
integration'dan kasıt: 'main' branch'ine açılan PR'ın merge edilmesidir; yani entegre edilmesidir. "Continuous integration" CI tool'larında otomatik build ve test koşulduğu durumlardır.

"continuous delivery", "Continuous integration"'a ek olarak acceptence-test ve "stage" ortamına taşınma işleminin otomatize edildiği durumlardır. "stage" ortamı, prod ortamından önceki ortamdır.

"continuous deployment", "Continuous integration"'a ek olarak production ortamına da çıkışın otomatize edildiği durumlardır.

yukarıdakilerin tümü için kaynak: (source-id: 32)

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Reproducible builds
açık kaynaklı da olsa uygulamaların executable'larının hangi kaynak koddan üretildiğini bulabilmek için kullanılan bir yöntemdir.

kaynak kodların derlenmesi sonucu deterministik bir executable ortaya çıkacak şekilde build aşamaları hazırlanır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# thunk
kelima anlamı: gümletmek

as seen below; thunk is a function that returns a function and can be execute anytime. this type of calling is using in redux-thunk library/middleware.

```js
const topla = (x, y) => x+y;

// 'thunk' is a function that takes no arguments
const thunk = () => topla(3, 4);

// the thunk can then be passed around without being evaluated...
doSomethingWithThunk(thunk);

// evaluated it anytime
thunk(); // === 7
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# imlicit vs explicit
bu iki terim sıkça kodlama dünyasında kullanılır. implicit (anlamı: üstü kapalı), framework'ün arkaplnda söylemeden bir işlemi yapmasıdır. explicit (anlamı: açık/belirgin) ise; yazılımcının kendi halletmek durumunda kaldığı işlemlere denir.

örnek-1:

Java will provide us default constructor implicitly. Even if the programmer didn't write code for constructor, he can call default constructor.

örnek-2:
```java
// explicit Locking
Student student = entityManager.find(Student.class, id);
entityManager.lock(student, LockModeType.OPTIMISTIC);
```

örnek-3:

Explicit casting:

officialy name: widening conversion
```java
double x = 10.5;
int y = (int) x;
```

Implicit casting:

officially name: narrowing conversion
```java
int x = 10;
double y = x;
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# cucumber

- SmartBear firması tarafından geliştirilmektedir.
- JBehave ile apaynı mantıkta işlemektedir.
- JBehave daha core bir framework'tür, oysa cucumber biraz daha kolaydır.
- cucumber framework'ü bir çok dil için ayrı ayrı yazılmış ve ayrı ayrı repo'larda geliştirilmektedir. java, ruby, javascript için mevcuttur.
- testler (features dosyalarındaki her satıra karşılık gelecek fonksiyon/kod) java'da yazılcak ise;
  - cucumber-java8 dependency'sini eklemek gerekli (lambda desteği olduğunda java8 isimlendirilmiş)
  - cucumber-java ile sadece annotation'lar kullanılarak test yazılması sağlanıyor
  - eğer junit ile entegre çalışacak ise cucumber-junit dependency'si eklemek gerekli. her scenario'nun bir junit @Test'i olarak algılanmasını sağlıyor.
  - cucumber-jvm paketi deprecated'tır.
- testleri koştuktan sonra target dizini altında raporları özel formarda çıkarır.
- cucumber, .feature uzantılı dosyaları okur ve içerisindeki her satırı JBehave gibi işletir.
- .features dosyaları Gherkin dili ile yazılmıştır. örnek syntax aşağıdadır. her 1 feature dosyası altında bir den fazla senaryo var. her senaryonun içindeki her satır "step" olarak adlandırılır.

```gherkin
Feature: Guess the word

  # The first example has two steps
  Scenario: Maker starts a game
    When the Maker starts a game
    Then the Maker waits for a Breaker to join

  # The second example has three steps
  Scenario: Breaker joins a game
    Given the Maker has started a game with the word "silky"
    When the Breaker joins the Maker's game
    Then the Breaker must guess a word with 5 characters
```

# Karate
- cucumber üzerine kurulu bir framework'tür.
- karate'nin en temel artısı tüm testlerin sadece feature dosyalarında olmasıdır.
- karate gömülü DSL'ler barındırır:
  - direk HTTP calling sunan DSL'ler vardır.
  - direk web sayfasında selenium driver gibi gezinebilmemizi sağlayan dsl'ler vadır.
- karakte BDD frameworkü sayılmaz. Çünkü feature dosyalarında BDD'ye göre daha fazla teknik detay gerekir. Oysa BDD'deki cümleler ve yazılımcı olmayanın bile anlayacağı cinsten olması beklenir.

# Robot
- TDD frameworküdür.
- Karate mantığında çalışır. Gömülü BDD'lerin (bunlar ek modüllerle genişletilebilir) çağrılabilmelerini sağlar.
- robot testlerini yürütmek için onun executable'ına ihtiyaç vardır. robot python ile yazılmıştır. dolayısı ile test için oluşturacağımız project structure'sini tamamen kendilerini belirlemiştir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# What You See Is What You Get (or WYSIWYG)
microsoft Word, openoffice/libreoffice writer, birer WYSIWYG örneğidir. WYSIWYG'e uyan yazılımlar, direk olarak çıktıyı düzenlememizi sağlarlar.

Oysa markdown, latex gibi diller WYSIWYG diildir. onlar __WYSIWYM (or what you see is what you mean)__'e uyarlar. Aslında teknik anlamda bakıldığında microsoft word de latex'ten farksızdır. çünkü arkaplanda kendisi yine binary/xml olarak bilgileri tutmaktadır. fakat temel fark şu ki; ms-word de direk olarak çıktıyı düzenleyebildiğiniz bir arayüz sunuyor. latex or markdown'da böyle bir yazılım olmaz. zaten olması latex ve markdown'un mantığına ters olur.

Piyasada bu terimi baz alar birçok farklı terim kullanılmaktadır. örnekler: __WYCIWYG (or what you cache is what you get), WYGIWYS (or what you get is what you see), WYSIWYW (or what you see is what you want)__

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Chrome
Cr simgeli atomun özel ismi.

Chrome terimi bilişim dünyasında User Interface'nin dış tarafındaki kısımları temsil etmek için kullanılır. Eski amerikan araçlarında dış kaplaması krom olan arabalar vardı. Muhtemelen buradan esinlenerek bilişim dünyasına yansımıştır.

chrome terimi hangi context'ten bakıldığına göre değişmekte olan bir terimdir. işletim sistemi seviyesinde bakılırsa chrome; panel'dir (ms-windows'taki taskbar, başlat menüsü gibi). web tarayıcıları açısından bakılırsa chrome, web content'in (html'in) dışında kalan kısımlardır: örnek: url bar, menu bar, back and forward buttons...

Firefox, API ve dökümanlarında "chrome" terimini sıkça kullanır. "Google Chrome" ismi ise belliki esinlenmiştir.

Chrome ismini bambaşka amaçlarla özel isim olarak kullanan farklı API'ler ve yazılımlar vardır. Bu yazılımlar "chrome" terimini özel isim olarak kullanmaktadırlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# bean (dependency injection) vs static vs new
Bu karşılaştırmadoğru diil. Fakat yinede ne gibi artılar eksiler olabileceğini not almak amacı ile bu konu başlığını bırakıyorum.

Bir sınıftaki metodları 3 şekilde çağrabiliriz:

> CustomUtil.parseEmptyCharaceters();

- CustomUtils bir java-bean olur
- CustomUtils java-bean olmaz fakat parseEmptyCharaceters static metod olur
- CustomUtils java-bean olmaz ve parseEmptyCharaceters static değildir

3'üncü durumda objemizi bir yerden çağırmdığımızda "new CustomUtils()" ile çağırmak zorunda kalabiliriz. Bu her çağrışımıza 1 satır fazladan kod ekliyor ve her defasında yeni instance oluşturmak zoundayız. Eğer birçok kere kullanıyorsak belleği doldurmaya başlar. Aynı instance'ı kullanabiliyorsak java-bean yapmakta yarar var.

2'inci durumda static metodların genelde biçrok programlama dili teknik yapısı sebebi ile test etmek zordur. bunun için compiler'a ek fazlar, yada framework'lerden yararlanmak gerekmektedir. örnek: javada mockito static metodları override edemiyor. powermock frameworkünü kulanmak gerekiyor.

1'inci durumda scope'ları kulanma (her request için ayrı instance oluşturma) gibi, DI özelliklerinden yararlanabiliyoruz (lazy loading gibi). Bunu yanında içiçe dependency injection'ları constructor'da argüman olarak geçmek zorunda kalmıyoruz (çünkü new operatörünü çağırmıyoruz).

java-bean'ler test etmek için verimsiz bir altyapısı var ise, constructor based injection tercih edilebilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# multi-tenancy
tenancy kelime anlamı: kiracılık

bir web servisinin birçok client için çalışmasına göre ayarlanmış ise, o web servisi multi-tenancy destekliyordur. multi-tenancy'nin alternatifi şudur: her client için ayrı ayrı sunuculara ayrı ayrı kurulum yapılır.

multi-tenancy sistemlerde, genelde her veritabanı sorgusunda client-id parametresi where koşuluna eklenmelidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# dry run
A dry run testing is a process which is run is a controlled conditions to minimize the negative effects of any product failure.

örnek: iki dizini sync yapan bir uygulama olsun. sync işlemi riskli. bu sebeple öncesinde dry run koşulur. dry run ile sync uygulaması önce bir dry işlem yürütür. bu işlem gerçek kopyalama işlemi yaparmış gibi ilerler, tek farkı gerçekten kopyalamamasıdır.

dry run resmi bir tanım değildir. bu sebeple, dry run işleminin tam olarak ne yapacağı uygulamanın tasarımcılarına kalmıştır. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# API first
"database first" gibi bir yaklaşımdır. önce API hazırlanır, daha sonra bunun arka tarafı yazılmaya başlamnır. Bu şekilde testçiler, önyüzcüler de geliştirmeye daha sorunsuzca başlar. örneğin swagger/openapi ile hazırlayacağımız yml dosyasını herkesle paylaşırsak, herkes geliştirmeye paralelden başlar ve birbirini beklemek zorunda kalmaz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# subset (or altküme)
subset'in tersi: __superset__

if A is subset of B; then B-compiler can compile A code. subset/superset consepts are only about language syntax.

TypeScript is a superset of JavaScript. That means Javascript is a subset of Typescript. fakat; Her typescript compiler'ı, js codunu deryelebilecek diye bir kaide yok. bunun birçok sebebi olabilir. örnek: syntax uyabilir, ama native gelen primitive objeler uymak zorunda diil. sadece sytax uyuyor. default API'ler de aynı olmak zorunda diil.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# binary blob
blob kelime anlamı: damla

context'e göre farklı anlamları var:

-  açık kaynaklı bir OS çekirdeğinde; proprietary device driver (closed-source device driver)'ları için kullanılan bir terimdir. buradan yola çıkan bazı insanlar, daha sonra binary blob terimini açık kaynaklı olan bir yazılımın içindeki kapalı kod binary'leri içinde kullanmaya başlamışlardır. 

- database sistemlerinde; __Binary Large OBject (BLOB)__ olarak kullanılıyor. bu objeler media objeleri gibi herhangi bir binary dosyaları olabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# kernel space vs user space (or userland)
tüm user (root user'ı dahil) process'lerinin harcadığı memory bölgesi userspace'tir. kernel space ise, system call'lar yapıldığı sırada, system call'ların kendi içinde kullandığı ve OS çekirdeğinin kullandığı memory'dir.

# DMA (or direct memory access)
Her işlem için gerekli data CPU ya taşınmalıdır. kopyalama işlemleri de buna dahildir. fakat donanımlar özel olarak buna bir çözüm getirmişlerdir. donanımlar artık bir io'nun diğer io'ya direk data taşımasına izin vermektedir. bu duruma DMA denir.

DMA yapabilmek için hem donanımın desteklemesi, hemde OS ve DMA işlemi yapmaya çalışan yazılımın kodunun buna göre yazılmış olması gerekmektedir.

işlem başlatılması ve sonlanması gibi durumlarda CPU'ya gidecek fakat her data byte'ı tek tek CPU'ya taşınmaya gerek kalmayacak.

DMA işlemi aynı I/O cihazından aynı I/O cihazına da yapılabilir.

*nix'lerdeki read() system call'u arkaplanda datayı direk belleğe CPU'ya gitmeden taşımaktadır.

# zero-copy
user space'e taşımaya gerek kalmadan yapılan dosya kopyalama işlemidir.

Bunun implementasyonu OS'a göre değişebilmektedir. zero-copy için OS'a system call yapılır. systemcall'un nasıl çalıştığı yazılımcı tarafından bilinmez. sadece dosya kopyalama işlemini temsil eder.

- normal for döngüsü ile dosya kopyalama

  normal bir for-loop ile okusaydık önce system call ile birkaç byte okuyacaktık (*nix sistemlerde read() system call'u). kernel space'e taşınan byte, user space'e yollanacaktı. oradan da write ile user space'den önce kernel space, oradan da I/O'ya yollanacaktı.

  *nix'teki "read()" system call'unu işlemi çağrıldığında, öncelikli olarak DMA üzerinden işlem yapılıp bu data direk olarak kernel'a (read fonksiyonunun içine) taşınmaktadır. read fonksiyonu da user space'e taşımaktadır.

- zero-copy ile kopyalama:

  data, kernel space'e taşınır (fakat user space'e taşımaz). direk kernel space'den I/O ya yollanır.
  
  Burada unutmamak lazım ki; o işlemde kullanılan kernel space (belki) CPU'nun içindeki (RAM'den daha hızlı olan) belleklerde olabilir. bu durumda RAM'e hiç gidilmemiş olacaktır. bu da daha hızlı kopyalama anlamına gelecektir.

  Eğer OS implementasyonu daha iyi ayarlanmış ise; dosya kopyalama için belki de hiç RAM kullanılmayacak, direk DMA kullanarak harddisk'ten harddisk'e kopyalama yapacaktır.

  Yukarıdakilerden hangisinin olacağı OS'un implementasyonuna ve donanımın desteğine bağlıdır.

java'da NIO ile bu kopyalama işlemini yapabiliriz:

```java
RandomAccessFile fromFile = new RandomAccessFile("fromFile.txt", "rw");
FileChannel      fromChannel = fromFile.getChannel();

RandomAccessFile toFile = new RandomAccessFile("toFile.txt", "rw");
FileChannel      toChannel = toFile.getChannel();

long position = 0;
long count    = fromChannel.size();

toChannel.transferFrom(fromChannel, position, count); //returns the number of bytes that actually transferred 
```

*nix sistemlerde C'deki sys/socket.h içindeki sendfile() system call'u bunu yapmaktadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# lua
Portekizce'de 'ay' anlamına gelmektedir.

- lua dili, shell syntax'ına çok benziyor.

- betik dili olduğundan, sanal makine gerektiriyor.

- fonksiyonların return değerlerinde birden fazla değer dönebilmeyi destekliyor.

```lua
function triple(x)
    return x, x, x
end

local a, b, c = triple(5)
```

- lua içerisinde standart olan, "table" tarzı primitive gibi kullanılabilen yapılar mevcut.

- lua comment syntax

```lua
--[==[
  comment line 1
  We can include "]=]" inside this comment
--]==]

-- this is single line comment
```

# C API

- özellikle C ile interoperability'si çok başarılı olduğundan C ile (or herhangi bir dille) yazılmış uygulamaların bir kısmı or eklentileri Lua ile yazılmaktadır.
  
  bahsedilen interoperability Lua VM'inin yönetiminine izin veriyor. Lua ekibi, C için bir kütüphane yazmış. Bu c kütüphanesini import edip, bu kütüphane aracılığı ile Lua VM'i runtime'da açıp, üzerinde lua kodu çalıştırabilir, VM üzerindeki variable'larda değişiklik yapabilir.

  ```c
  #include <stdlib.h>

  // Lua C kütüphaneleri
  #include <lauxlib.h>
  #include <lua.h>
  #include <lualib.h>

  int main(void)
  {
      // open Lua VM
      lua_State *lvm_hnd = lua_open();
      
      // load libraries inside VM
      luaL_openlibs(lvm_hnd);

      // Load a standard Lua function from global table:
      lua_getglobal(lvm_hnd, "print");

      // Push an argument onto Lua C API stack:
      lua_pushstring(lvm_hnd, "Hello");

      // Call Lua function with 1 argument and 0 results:
      lua_call(lvm_hnd, 1, 0);

      // close VM
      lua_close(lvm_hnd);

      return 0;
  }
  ```

- Sanal makinesi çok ufak boyutta ve az bellek tüketimi yapıyor. Sanal makine C ile yazılmış. Bu sebeple C ile programlanan gömülü sistemlerde Lua da kolayca kullanılabilmektedir. Zira Lua sanal makinesi de C olduğudan, direk execute edilebilir ortam yakalanmış olur. Lua'nın gömülü sistemlerde tercih edilmesinin sebebi de budur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# httpbin
httpbin test amaçlı kullanılan, hazır http metodları sunan sunucu yazılımlara verilen genel bir prefix/suffix'tir. birçok httpbin servisi vardır:

- www.github.com/postmanlabs/httpbin
- www.github.com/kevin1024/pytest-httpbin

httpbin'lerin bazı hazır metodları:
- requestin herhangi bir header'ını dönen metodlar (örnek user agent)
- echo servisleri
- resim dönen servisler
- tüm bu servislerin get, post, put... kombinasyonları

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# gRPC (or gRPC Remote Procedure Calls)
google tarafından geliştirilen bir ptotokoldür. arkaplanda HTTP/2 ve __Protocol Buffers (or Protobuf)__ kullanılır.

supports: authentication, bidirectional streaming and flow control, blocking or nonblocking bindings, cancellation, timeouts.

gRPC sadece prtotobuf ile binary desteklesede, external olarak kullanacağımız kütüphanelerle json, xml gibi diğer formatlarıda desteklyebiliyor. kaynak: (source-id: 33)

# __Protocol Buffers (or Protobuf)__
binary'ye serileştirme yöntemidir. google tarafından geliştiriliyor. xml, json gibi human-readable çıktı yapmamaması dezavantaj, fakat performans ve memory konusunda çok daha verimli.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Kernel panic
*nix sistemlerde kullanılan bir terimdir. işletim sisteminin, çözümü olmayan durumu yakaladığında bilinçli olarak fırlattığı bir hatadır. windows'ta bu hata tipine __stop error (or blue screen of death or blue screen or BSoD)__ denir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# c# namespace
türkçeye "isimalanı" veya "isim uzayı" olarak çevrilmektedir.

java'daki package yapısına çok benzerdir.

java'daki gibi, dosyanın dulunduğu dizin ile paket adı aynı isminde olmak zorunda diildir.

```cs
using Other.Package.Name;
using System;

namespace namespace_name {
   // classes

   Console.WriteLine ("Hello there");
   // System.Console.WriteLine("Hello there"); // eger yukarıda "using System" yazmıyor olsaydı bu şekilde kullanmak zorundaydık.
}
```

- nested namespaces

```cs
namespace company.namespace1
{
    namespace namespace2 // inner namespace
    {
        class A {}
        class B {}
    }
}

// yukarıdaki yerine aşağıdaki de yazılabilirdi (birbirine denk)
namespace company.namespace1.namespace2
{
    class A {}
    class B {}
}

```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# location transparency
bir kaynağın erişim adresini (örneğin network ise ip'si, dosya istemi ise dosya adresi, mikroservisler ise servis'e erişmek için ip'si) bilmek zorunda kalmadığımız, onun yerine o kaynağa gidebileceğimiz sanal bir adres verilmesi durumudur.

örnekler:

- bir makinen gerçek ip'sini vermek istemiyorsa, o makineye bağlanan kişilere farklı bir ip veriririz ve yönlendirme yaparız. kişiler gerçek ip'yi bilmez.

- docker servislerimiz ayakta olsun. birbirinin ip'lerini bilmiyorlar. fakat birbirlerine hostname'ler aracılığı ile erişiyorlar. kimse kimin nerde olduğunu bulmak için ekstra efor harcamıyor. böyle bir durumda docker, sağladığı ortamda location transparency vardır diyebiliriz.

- kafka, yada axon'da event başlattığımızda, event'i başlatan uygulama event'i kimin çekeceğini bilmez. routing işlemini kafka veya event'i yöneten mekanizma yapar. bu durumda; axon veya kafka location transparency sağlar anlamına gelir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# single point of failure (or SPOF)
çökmesi/bozulması durumunda, diğer tüm alt sistemlerin durmasına sebep olacak alt sisteme denir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# NATS
ikinci adı: STAN (Nats'ın tersi) kaynak: (source-id: 34) (54 üncü satırda yorumda da bu isim kullanılmış)

publish/subscribe mesaj alışverişini sağlayan açık kaynaklı kütüphanedir. NATS ile haberleşilen ortamda "go" dili ile yazılmış bir sunucu bulunmaktadır. Sunucu kendi için kuyruk mekanizması barındırır. Birçok programlama dili için client yazılmıştır.

NATS; Neural Autonomic Transport System'ın kısaltmasından türetilmiştir. Geliştirici ekip, NATS'ı, merkezi bir sinir sistemi gibi çalıştığını düşündüğü için böyle bir isim üzerine karar vermiştir.

NATS'ın 2 çeşit sunucusu vardır: "NATS Streaming Server" ve "NATS Server". streaming server, normal NATS Server'ı wrap ediyor ve ek özellikler sunuyor. streaming server isminden anlaşılacağı gibi data steram'in yapmıyor. streamin server server'daki datayı persist ediyor (veritabanına kayıt ediyor) ve bunun sayesinde eski mesajları herkesin alabilmesini de sağlıyor. diğer tüm özellikler burada: https://nats-io.github.io/docs/nats_streaming/intro.html#features

nats-sub ve nats-pub go ile yazılmış, NATS client'larıdır. bu client'lar sadece komut satırından parametre alırak client işlem yaparlar. sadece demo/test amaçlı geliştirilmişlerdir.

örnek komut:

> nats-pub "hello world"

java client için basit kod örneği;

```java
Connection nc = Nats.connect("nats://localhost:4222");
nc.publish("topic1", "hello world");
nc.close();
```

streaming publish tarafının kodu:
```java
StreamingConnectionFactory cf = new StreamingConnectionFactory("cluster-id", "client-id");
StreamingConnection sc = cf.createConnection();
sc.publish("topic-id", "my-message".getBytes()); // synchronous
```

streaming subscribe tarafı kodu:
```java
// kendi içimizde tuttuğumuz bir obje. bu sadece bir integer. her defasında, value'sunu 1 düşürürüz.
// en sonda thread'imizi bekletmek için bu objemizden yararlanacağız
final CountDownLatch doneSignal = new CountDownLatch(1);// 1'den aşağıya geri sayım yapabileceğiz

Subscription sub = sc.subscribe("topic1", new MessageHandler() {

    public void onMessage(Message m) {
        System.out.printf("Received a message: " + m.getData() );
        doneSignal.countDown();
    }

}, new SubscriptionOptions.Builder().deliverAllAvailable().build() ); // 3rd parameter is Options

// burada countdown 0 olmadan thread beklemeye alınıyor
doneSignal.await();

sub.unsubscribe();
sc.close();
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Axon framework
java için açık kaynaklı CQRS, Saga, "event sourcing" pattern'lerini kolayca uygulamaya yarayan bir framework. CQRS, Saga, "event sourcing" patternleri manuel olarak yazılımcı tarafından da yapılabilir(implemente edilebilir). fakat framework'ün sunduğu birçok avantaj'da vardır.

__Eventuate__ axon'a alternatif bir frameworktür.

Axon'un JVM üzerinde çalışan bir sunucusu vardır. her uygulama sunucuya bağlanır. sunucunun içinde event bus mekanizması vardır. bu event bus, yazılımdaki event'lerimiz tutmaya yaramaktadır. Sunucu, event'leri görüntülemek için web GUI'de sunmaktadır.

Axon'da CQRS ve Saga opsiyonel iken; "event sourcing" kullanımı zorunludur. event sourcing metodları boş bırakılır ve her event sourcing işleminde agreegate objelerimiz JPA'ya basılırsa, "event sourcing" kullanılmamış varsayabiliriz. fakat böyle bir durumda sadece event base programming yapmış oluruz ve Axon kullanmamızın pek anlamı kalmaz.

Axon mikroservislerde veya monolitik uygulamalarda da kullanılabilmektedir.

Axon sunucusunun event bus'ında, Command Bus, Event Bus ve Query Bus sürekli çalışmaktadır.

Axon'da temel kod örneklerine bakalım:

```java
import org.axonframework.commandhandling.CommandHandler;
import org.axonframework.eventsourcing.EventSourcingHandler;
import org.axonframework.modelling.command.AggregateIdentifier;
​
import static org.axonframework.modelling.command.AggregateLifecycle.apply;
​
public class GiftCard {
​
    @AggregateIdentifier // bu değer id'nin bu aggregat için unique olduğunu belirtiyor. eğer birden fazla event/command çağrılırsa, "points" değeri aynı id'li tüm aggregate işlemleri için ortak olacaktır.
    private String id;
    private int points;
​
    @CommandHandler // CQRS'teki "command" e denk gelmektedir.
    //her command metodunun içinde bir den fazla event olabilir.
    // businnes logic katmanlarından (businnes logic bu class'ta diil. businnes login'ler buraları çağıracak) event çağıramayız. command çağırmak durumundayız. her command kendi içinde zaten birçok event'i gerekiyorsa çağıracaktır.
    // command metodları "decision-making/business logic" kodları içermelidir.
    public GiftCard(IssueCardCommand cmd) {
       
       // apply ile bir event çağrıyoruz. event'i çağırıyoruz. event'i çağırırken, parametreleri event CardIssuedEvent objesi içerisinde gönderiyoruz.
       apply(new CardIssuedEvent(cmd.getCardId(), cmd.getAmount()));
    }
​
    @EventSourcingHandler
    // CardIssuedEvent tetiklediğimiz event tamamlandığında çağrılacak metoddur.
    // bu metod içerisinde GiftCard objeminiz güncelleriz. GiftCard bizim database objemiz değildir. GiftCard şu anda Axon yapısının gerektirdiği bir sınıftır/yapıdır.
    // "state changes" lerin bulunduğu metodlar EventSourcingHandler metodlarıdır. state change'leri DB'deki ye yazılmaz. DB'ye yazacağımız metodlar farklı yerde.
    // "state changes" kesinlikle yukarıdaki command metodlarında yapılmamalı.
    // command metodları genelde state'i kontrol edip, event tetiklemelidir. eğer state te bir hata varsa, command metodu exception fırlatmalıdır.
    public void on(CardIssuedEvent evt) {

        // burada GiftCard sınıfının datalarını güncelleriz. bu şekilde bu sınıfta (GiftCard sınıfında) olan diğer metodlar(command metodlar) da güncel olarak isteği bilgileri okuyabilecektir. 
        id = evt.getCardId(); // bu işlemin en öncelikli yapılması lazımmki; diğer eventler aynı GiftCard property'lerini okuyabilsin.
        points = 0;
        //bu adımda db'deki GiftCardDB objemiz güncellenmemiştir. bu adım sadece GiftCard sınıfı (bu sınıf) içindeki dataları günceller. 
    }
​
    protected GiftCard() {
      // boş constructor Axon frameworkü tarafından zorunlu tutuluyor.
    }
}
```

```java
import org.axonframework.modelling.command.TargetAggregateIdentifier;
​
public class IssueCardCommand {
​
    @TargetAggregateIdentifier // bu değer, GiftCard objesindeki id'ye denk geldiğini gösteriyor. mutlaka bu olmalı.
    private final String cardId; 
    private final Integer amount;
​
    // constructor / getters / setters
}
```

# State storage
yukarıdaki kod örneğinde; "points" ve "id" değerleri storage'dir. storage'de tüm instance'ların değerleri mevcuttur. bu storage kısa süreli tutulması beklenen bir storage'dir. kalıcı olacak olan bilgiler zaten her event sonrası yada command sonrası db'ye yazılmalıdır. state storage'deki her değeri, o cammand'in çağırdığı her event okuyabilir. fakat dışarıdan kimse okuyamaz.

# event storage
her event'in kaydedildiği db'dir. Herhangi bir db kullanılabilir. fakat normal uygulamda çok fazla event olacağından (herşeyin modüler ve event yapısında olduğu düşünülürse), db'yi buna uygun şekilde seçmekte yarar var. AxonServer'ın kendi içinde buna spesifik geliştirilmiş bir API var. bu api dataları tutuyor ve yine select sorgusu atılabilmesini sağlıyor.

# Multi-entity Aggregates

Aggregate Root objemiz GiftCard olsun, onun altında bir çok transaction işlemi olsun. Bunu axon ile bu şekilde ifade ediyoruz:

```java
import org.axonframework.modelling.command.AggregateIdentifier;
import org.axonframework.modelling.command.AggregateMember;
import org.axonframework.modelling.command.EntityId;
​
public class GiftCard {
​
    @AggregateIdentifier
    private String id;
​
    @AggregateMember
    private List<GiftCardTransaction> transactions = new ArrayList<>();
​
    private int remainingValue;
​
    // command handlers, event sourcing handlers
}
​
public class GiftCardTransaction {
​
    @EntityId
    private String transactionId;

    private int transactionValue;
    private boolean reimbursed = false;
​
    public GiftCardTransaction(String transactionId, int transactionValue) {
        this.transactionId = transactionId;
        this.transactionValue = transactionValue;
    }
​
    public String getTransactionId() {
        return transactionId;
    }
​
    // command handlers, event sourcing handlers
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# lombok

lombok java için birçok ek özellik sağlayan altyapıdır. jar olarak classpath'e eklendiğinde build sırasında devreye girmektedir, bu şekilde özelliklerini devreye sokabilmektedir.

örneğin;
- getter-setter'ları bizim için oluşturmaktadır.
- builder oluşturmaktadır
- toString oluşturmaktadır
- equals fonksiyonlarını oluşturmaktadır

özelliklerin tüm listesi buradadır: https://projectlombok.org/features/all

IDE'nin derlemeden önce bazı şeyleri görebilmesi için lombok'un IDE eklentisinin yüklü olması gereklidir. IDE'de lombok-eklentisi yüklü ise aşağıdaki kodda hata almayız.

```xml
<dependencies>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.4</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

```java
public class UserIntegrationTest {
 
    @Test
    public void givenAnnotatedUser_thenHasGettersAndSetters() {
        User user = new User();
        user.setFirstName("Test");
        assertEquals(user.gerFirstName(), "Test");
    }
 
    @Getter @Setter
    class User {
        private String firstName;
    }
}
```

IDE eklentisi, direk kodları da generade ediyor. yani sadece eklenti olursa, dependency'ye ihtiyaç kalmadan ilgili kodları generate edebiliyor. bu özellik zaten IDE'lerin içinde var.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# ArchUnit
java test kütüphanesidir. derlenen projedeki java sınıflarının mimarisini kontrol edip, mimari açıdan uygun olup olmadığını test edebilmemiz sağlar. 

örnek:
- interfacelerin isimleri şunlarla başlamalıdır
- implemetasyonların prefixi şu olmamalıdır
- standart stream'lere  (system.out gibi) hiçbir yerden erişilmemiş olmalıdır

örnek:

aşağıdaki örnek 3 farklı test vardır. büyük harfle yazılanlar ArchUnit içerisinde yüklü gelen default mimari testler.
3'üncü loggers_should_be_private_static_final isimli fonksiyon'u ise biz tanımladık.

bu testleri junit içerisinde çağırıp koşabiliriz.

```java
@AnalyzeClasses(packages = "com.tngtech.archunit.example.layers")
public class CodingRulesTest {

    @ArchTest
    private final ArchRule no_generic_exceptions = NO_CLASSES_SHOULD_THROW_GENERIC_EXCEPTIONS;

    @ArchTest
    private final ArchRule no_java_util_logging = NO_CLASSES_SHOULD_USE_JAVA_UTIL_LOGGING;

    @ArchTest
    private final ArchRule loggers_should_be_private_static_final =
            fields().that().haveRawType(Logger.class)
                    .should().bePrivate()
                    .andShould().beStatic()
                    .andShould().beFinal()
                    .because("we agreed on this convention");
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# IntelliJ IDEA

JetBrains (firmanın eski ismi: IntelliJ) firması tarafından geliştirilen IDE. 2 tür lisans ile dağıtılıyor. Ücretsiz versiyon kısıtılı özelliklere sahip ve açık kaynaklı. Ücretli versiyonda kapalı kaynak eklentiler mevcut.

Genel olarak IDE Indexing konusunda diğer IDE'lere göre çok başarılı. Arkaplanda anlık yazdıkça indexleme yapılıyor ve bu yüzden geliştiriciye daha çok seçenek sunabiliyor (otomatik tamamlama gibi). bunları yaparkende herşeyi thread açıyor ve bu sebeple diğer IDE'lere göre hiç takılmıyor.

# Android Studio

IntelliJ IDEA üzerine ek olarak; android geliştirme ortamı için eklentiler ile google tarafından dağıtılan IDE.

# Android Developer Tools (or ADT) vs Andmore

Android plugin for Eclipse. It was developing by Google. Google now discontinued the project because they are developing plugins for IntelliJ Idea. Now the community fork the ADT project with new name: Andmore.

# project Structure of IDE's

birbirine denk gelen terimler aşağıdaki tabloda verilmiştir:

```
Eclipse       -> Workspace | Project

IntelliJ      -> Project   | Module

Visual Studio -> Solution  | Project

XCode         -> Workspace | Projects
```

- Android Studio, IntelliJ türevi olduğu için aynı mantıkta çalışmaktadır.

- IntelliJ bir pencerede birden fazla proje açmıyor. sadece 1 proje ve onun alt modülleri olabilir. IntelliJ aynı projeyi 2 farklı pencerde açılmasına da izin vermiyor. sadece sekmeler farklı sekmelerde açılabiliyor.

- IntelliJ'de eclipse'teki gibi perspektifler yoktur.

# maven/gradle/ide proje dizin yapıları hakkında
saf IDE'siz sadece gradle android projesi oluştursak bir gradle dosyası yeterli. gradle, maven gibi altprojeleri destekliyor. "android studio" proje dizininde gradle görürse alt modülleri daha iyi yönetebilir. bu sebeple react-native gibi komut satırı uygulamaları android studio'ya uygun android projesi yaratır. yine bu sebeple android kodlarımızın olduğu proje bir module olmaktadır. modülümüzün bir üst dizini (android studio için project dizini) kodsuz bir gradle projesidir. bu gradle'nin alt modülü bizim android projemizdir. eğer android'e bir library yazmak istersek onu da android ile aynı seviyede yeni bir modül olacak şekilde ayarlamalıyız.

# eclipse version history

| name     | release date   | version     |
|----------|----------------|-------------|
| Callisto | June 2006      | 3.2         |
| Europa   | June 2007      | 3.3         |
| Ganymede | June 2008      | 3.4         |
| Galileo  | June 2009      | 3.5         |
| Helios   | June 2010      | 3.6         |
| Indigo   | June 2011      | 3.7         |
| Juno     | June 2012      | 3.8 and 4.2 |
| Kepler   | June 2013      | 4.3         |
| Luna     | June 2014      | 4.4         |
| Mars     | June 2015      | 4.5         |
| Neon     | June 2016      | 4.6         |
| Oxygen   | June 2017      | 4.7         |
| Photon   | June 2018      | 4.8         |
| 2018-09  | September 2018 | 4.9         |
| 2018-12  | December 2018  | 4.10        |
| 2019-03  | March 2019     | 4.11        |
| 2019-06  | June 2019      | 4.12        |
| 2019-09  | September 2019 | 4.13        |
| 2019-12  | December 2019  | 4.14        |

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# CPU Scheduling algortithms (or process Scheduling algortithms)

# time slice (or quantum)
işlemin cpu'da kesintisiz olarak kalacağı minimum süredir.

# algortithms

  - ## Round-robin (or RR)
    round kelime anlamı: tur

    robin kelime anlamı: özel bir kuş türü

    quantum süresi vardır. tüm işlemler kuyruğa alınır. ilk işlem kuantum süresinde cpu'da kalır ve kuyruğun en sonuna atılır ve yeni gelen process varsa yine kuyruğun sonuna atılır. quantum bittiğinden dolayı tekrar skuyrukta sırada bekleyen işlem, cpu'ya alınır. bu işlemde kuyruğun sonuna tılır ve yeni gelen işlem varsa kuyruğun sonuna atılır...

  - ## First-Come, First-Served (FCFS) Scheduling
    İlk gelen kesintisiz olarak cpu'da kalır ve işlemin tamamlanması beklenir.

  - ## Shortest-Job-Next (SJN) Scheduling (or shortest job first or SJF)
    her zaman o anda kısa olan process tamamlanana kdar cpu'ya girer.

  - ## Shortest Remaining Time
    SJN'ye benzer. fakat quantum süresi vardır. quantum süresi her tamamlandığında, en kısa olan process işleme alınır.

  - ## Priority Scheduling
    her işlemin bir önceliği vardır. kalan zaman, arrival time gibi değerlerin yanında priority değerine bakarak ta hangi process'in cpu'ya gireceği karar verilir. bunun birçok implementasyonu vardır.

  - ## Multiple-Level Queues Scheduling
    birden fazla cpu kuyruğu yaratılır. her kuyruğun kendi içinde farklı algoritması olabilir. ve her 2 kuyruktan işleme alınacak değer seçilirkende farklı algoritmalar uygulanabilir. yani her kuyruk kendi içinde hangi process'in işleme gideceğini belirler. daha sonra her kuyruktan sunulan/belirlenen işlemler arasındada bir sçeim yapılır ve cpu'ya tek bir işlem yollanır. bu sebeple bu algoritmanında birçok implementasyonu vardır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# false positive (or type I error) vs false nagatif (or type II error)
medical testlerde, binary classification ve istatistik bilimlerinde kullanılan terimlerdir.

bir data incelenir (örnek: ocr ile bir karakter tespiti yapılmaya çalışılsın, yada hastalığın tanısı koyulama çalışılsın). inceleme sonucu X kararına varılır (örnek: ocr sonucu karakter 'A' olduğuna kanaat getirilsin, yada hastalığın zatüre olduğuna karar verilsin).

Eğer gerçek sonuç X ten farklı ise; bu duruma 'false positive' denir.

İnceleme sonuu 'X değil' kararına varılır (örnek: ocr sonucu 'A karakteri değil', yada 'hasta zatüre değil' kararına varılır).

Eğer gerçek sonuç X ise o zaman bu duruma 'false negatif' denir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Appmon
__Dynatrace__ firması tarafından geliştirilen "Application Performance Monitoring" yazılımıdır. örneğin; java web uygulamamızı takip eder ve ona gelen istekleri gruplayıp, dashboard'larda detayları gösterir. stacktrace'e kadar analiz edilmesini sağlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# jhipster
app genrator command line tool (boilerplate) for spring boot microservices (netflix), Angular, React, Bootstrap, Maven/Gradle, Elastic Stack, Docker.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# ramdisk
ram, ssd'lerdendahi çok daha hızlı. bir yazılım ram'de bellek ayırıp (bellekte sanal bir dosya sistemi yaratıp), bunu hard-drive mış gibi OS'a mount edebilir. tıpkı bir usb bellek gibi. işte bu ram'deki belleğe ramdisk denir.

piyasada bir çok ramdisk görevi gören uygulama mevcut.

linux'taki "mount" komutu ramdisk ihtiyacını giderebiliyor. örnek:

```sh
mkdir /dir_to_mount
mount -o size=16G -t tmpfs none /dir_to_mount
```

mount komutu ram'de 2 farklı sanal file system destekliyor: tmpfs ve ramfs(tmpfs'e göre daha eski)

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# CGI (or Commond Gateway Interface)
server'da istekleri karşılayıp, istekteki URL'deki path'lere göre iligli uygulamaya isteği yönlendiren yazılımdır. ISS, javaee sunucuları gibi gelişmiş sunucular çıktığında beri, özel durumlar hariç kullanılmıyor.

CGI'nin RFC'si vardır. yani belli standartlardadır. protokol hakkında detaylar RFC'de belirtilmiştir.

CGI kullanan birçok yazılım mevcut: mod_perl, mod_php4, mod_fastcgi

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Bottleneck (or darboğaz)
bu terim bilişim dünyasında bu tarz durumlarda kullanılmaktadır:
- network'e gelen istekler internet hızımız sebebi ile yavaşlaması. bu durumda network darboğaz edilir.
- bilgisyarda bir process cpu ve hdd aynı oranda hızlı olmadıklarından dolayı (örnek hdd yavaş ise), process'in yavaşlaması. bu durumda hdd darboğaz edilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# twelve-factor app

12factor.net'te yayımlanan, birçok contributer'ın desteği ile genel olarak tüm software-as-a-service yazılımlarda uyulması gereken 12 temel kural yer almaktadır. her kural 1-2 sayfa uzunluğunda açıklanmıştır. özetle:

- Codebase (Kod Tabanı): birkaç uygulama, aynı kodları içeriyorsa mutlaka o kodlar common lib yapılmalı.

- Dependencies (Bağımlılıklar): bağımlılıklar mutlaka hiyerarşik olarak tanımlanmalıdır

- Config (Yapılandırma): configler mutlaka codebase'den ayrı ve prod, test gibi ortamlar için ayrı gruplanmalıdırlar

- Backing Services (Destek Servisleri): dış kaynaklar/hizmetlere gidebilmek için sadece config'lerin değiştirilmesi yeterli olmalıdır. örneğin; farklı bir db'ye giderken codebase'de dğeişiklik yapılmamalıdır. bir config değişikliği yetmelidir.

- Build, Release, Run (Derleme, Sürüm, Çalıştırma): pipeline olmalıdır ve eski sürüme dönülebilmelidir

- Processes (Süreçler): stateless(durumsuz) ve shared-nothing(bir şey paylaşmayan) olmalıdırlar. veriler process'lerde diil, veritabanlrında saklanmalıdırlar.

- Port Binding (Port Bağlama)

- Concurrency (Eş Zamanlılık)

- Disposability (Kullanıma Hazır Olma Durumu): birden kesinti olma durumuna hazır olabilmelidir.

- Dev/Prod Parity (Geliştirme/Üretim Ortamlarının Eşitliği): dev ortamında kullanılan tool'lar ile prod/test ortamında kullanılan tool'lar mümkün oldukça aynı olmalıdır. devops kültürü mutlaka olmalıdır.

- Logs (Günlükler)

- Admin Processes (Yönetici Süreçleri): yazılım yönetimi işlemleri tool'lar aracılığı ile yapılmalıdır. ve sadece 1 kerelik yapılacak işlemler (örneğin bir sql işlemi), script haline getirilip tüm ortamlarda çalıştırılabilmelidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# metasearch engine
startpage.com ve searx projesi buna bir örnektir. diğer arama motorlarını kullanarak sonuçları yansıtan arama motorlarıdır. kendi veritabanlarını bulundurmazlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# apache hadoop

açık kaynaklı bir framework'tür. MapReduce mantığını temel alarak çalışır ve big-data'mız üzerinde işlem yapabilmemizi sağlar. merkezi servisimize istek gelir, hadoop java api'miz ile hadoop sorgumuzu yazarız ve data'ları çekmek için java-API her node'a istek atar. her node HDFS dosya sistemi ile datalarımızı tutmaktadır. her node kendi içerisinde bilgiyi bize (merkezi noktaya) döndürür. bu şekilde merkezi servisimizde yük diğer node'lara paylaştırılmış olur.

haddoop'un Mödülleri:

- common

  utilities like java API (lib)

- HDFS (or Hadoop Distributed File System)

  veritabanının formatıdır. bu tek bir makinede olmak zorunda değildir. birçok farklı lokasyonlardaki birçok farklı makinede parçalı şekilde bulunabilir.

Hadoop kendi içerisinde Zookeeper dan yararlanmaktadır. Hadoop'u kaldırmadan önce Zookeeper'ı ayağa kaldırmak gerekir. Zookeeper key/value bir storage manager'dır. (fakat piyasada geliştiriciler, açık olan web servisleri Zookeeper storage'sinde tutup Zookeeper'ı bir "servis discovery" olarak ta kullanmaktadırlar.)

# MapReduce

map ve reduce olarak iyi ayrı işlemi temsil eder. map, sorgunun başlangıcında HDFS'den topladığımız her değeri döner ve bu değer üzerinde değişiklik yapmamızı sağlayan fonksiyondur. reduce işlemi ise, map sonunda elde ettiğimiz tüm değerleri alır ve sonunda bir değer döndürmemizi sağlayan fonksiyondur. bu iki fonksiyon biribirini tamamlamaktadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Mesasuring maintainability

  - # line of codes (or LOC or source lines of code or SLOC)
     
  - # cyclomatic complexity

    if içinde if olma oranıdır. bu oran yükseldikçe maintainability düşer.

  - # depth of inheritance tree (or DIT)
  
    sınıfların birbirinden extend etme oranıdır. ne kadar çok üst sınfıtan extend edersek maintainability o kadar düşer.

# code smell
bu terim kodun best practice'ler ile yazılmadığını belli eden karateristikleri için kullanılır. "kodun kötü kokması" manasında kullanılan bir terimdir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Greenfield systems vs Brownfield systems
Greenfield projeler sıfırdan başlanılan projelerdir. Brownfield ise varolan sitemin güncellenmesi gibi durumları temsil eder.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# windows için paket yöneticileri

  - # Chocolatey
  windows için açık kaynaklı komut satırı paket yöneticisidir.

  programları standart olarak program files içerisine kurar. fakat bu dizin istenirse her program için ayrı ayrı override edilebilir. kurulan programlar, normal koşullarda windows dizinine dll atıyorsa, Chocolatey ile kurulursa da aynı şekilde dll atarlar. Chocolatey native setup/installer'ı çalıştırır. çalıştırırken yüklenecek dizinleri override eder.

  Burada birçok açıklama mevcut: (source-id: 35)

  - # scoop
  Chocolatey'e alternatiftir.

  - # Ninite
  son kullanıcı internet sayfası üzerinden kurmak istediği program listesini seçiyor ve ninite'nin o onda o listeye göre oluşturduğu exe dosyasını indiriyor. bu exe ile windows makineye kurulum yapılıyor. uygulamalar program files içerisine normal setup dosyaları internetten indirilerek kuruluyor.

# windows installers

  - InstallShield
  - Nullsoft Scriptable Install System (or NSIS): winamp'ı geliştiren Nullsoft firması tarafından geliştirilmiştir.
  - Windows Installer: uzantısı .msi'dir. microsoft'un resmi installer'ıdır. diğer installer'lar msi formatını kullanamaz. diğer installer'lar .exe formatını kullanmak zorundalar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# BCD code (or Binary Coded Decimal code)
onluk sistemindeki bir sayının her basamağın ayrı ayrı ikilik tabana çevrilerek yazılmış halidir. 2 çeşit BCD vardır:

- Genişletilmiş (Uncompressed) BCD

Her basamak 1 byte ile temsil edilir. örnek:

```
Onluk Taban: 91
BCD: 0000 1001 0000 0001
```

9; 1001'a eşit olduğundan her zaman 1 byte'ın yarısı boşa gitmektedir.

- Sıkıştırılmış (Packed) BCD

Her basamak 4 bit ile temsil edilir.

```
Onluk Taban: 91
BCD: 1001 0001 (aradaki boşluk olmamalı. okunabilirliği arttırmak için boşluk bırakıldı.)
```

```
Onluk Taban: 123
BCD: 0000 0001 0010 (aradaki boşluk olmamalı. okunabilirliği arttırmak için boşluk bırakıldı.)

min 8 bit olarak kullanılan bir makinede yukarıdaki BCD değerini sol tarafına 4 bit koymak zorundayız. sonuçta bunu elde ederiz:
BCD: 0000 0000 0001 0010 (aradaki boşluk olmamalı. okunabilirliği arttırmak için boşluk bırakıldı.)
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# eşlik biti (or parity bit or check bit)
binary data kümemizin başına yada sonuna konular bir çeşit kontrol bitidir. data kümemizde bulunan toplam 1 sayısı tek sayı ise 1, çift sayı ise 0 olarak eşlik biti kaydedilir (tersi de olabilir: eğer tek sayı için 0 verildiyse, çift sayı 1 için 1 kullanılır). bu şekilde datanın değişip değişmediği güvence altına alınmış olur. genelde iki bilgisyar arası haberleşme protokollerinde bu yöntem kullanılır. örnek:

| kontrol edilen data | count of "1" bits | data including parity |
|---------------------|-------------------|-----------------------|
| 0000000             | 0                 | 00000000              |
| 1010001             | 3                 | 11010001              |
| 1101001             | 4                 | 01101001              |
| 1111111             | 7                 | 11111111              |

Parity biti 1 bit değişikliğe uğrarsa, hatayı tespit edebilmemizi sağlıyor. fakat 2 bit değişikliğe uğramış ise o zaman hatayı tespit edemeyiz. dolayısı ile parity önemsiz data kontrollerinde kullanılmalıdır çünkü %100 doğruluğu yoktur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# media center
youtubeden video izleme, network'teki birçok protokol ile (örnek samba) paylaşılmış media dosyalarını direk açma, yayın protokollerini izleme, local media dosyalarını yönetme izleme gibi birçok media işlevini yerine getiren birçok mödülü olan uygulama.

# Kodi (or old-name:XBMC)
Cross platform, Açık kaynaklı media center uygulamasıdır.

# Windows Media Center
microsoft'un media center uygulamasıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Module (or modül) vs Component (or Bileşen)
- modül, bir bütünün içinde diğer elemanlarının çalışmasından bağımsız çalışabilen bir parça olarak tanımlanabilir. modül, load/unload edilebilen bir parçadır.
- Component tekrar kullanılabicek olan parçadır.
- modül tekrar kullanılabilir olma durumu söz konusu diildir.
- "Component-based software engineering" ve "Modular programming" teknikleri yukarıdaki bilgilere dayanmaktadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# context (or tr:kontekst or bağlam)
kontekst kelime anlamı: ortam, çevre

birçok api'de context terimi geçer. context bulunanan platform hakkında data bilgisidir. örneklerden gidersek daha net anlaşılır:

- servlet'e bir request geldi. servlet service metodu çalıştı 2 adet parametre aldı: request, response. service metodu içinden Servlet sınıfının getContext metodu çağrılabilir. getContext bize asıl amacımız olan request ve response dışındaki tüm data'yı sağlar. getContext Servlet'e (Servlet bu senaryoda platformumuz oluyor) geçilmiş parametreleri döndürüyor.

- kuberneteste komut satırından işlem yaptığımızda asıl amacımız container ağa kaldırmak, silmektir... Kubernetes'te context değiştirdiğimizde çalışma ortamımızın (platformumuzun) ayarlarını değiştiririz.

- android'te context bir sınıftır. Bu sınıf service, activity gibi sınıfıların super class'ıdır. context en tepededir ve uygulama seviyesinde (platform seviyesinde) bilgileri/metodları içerir. Android platformundaki android.content.Context sınıfının içindeki yorumlara bakacak olursak:

```
/**
 * Interface to global information about an application environment.  This is
 * an abstract class whose implementation is provided by
 * the Android system.  It
 * allows access to application-specific resources and classes, as well as
 * up-calls for application-level operations such as launching activities,
 * broadcasting and receiving intents, etc.
 */
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# header file (or copybook)
programla dillerinde genelde dosyanın tepesinde bazı kütüphaneler import edilir. eğer kütüphane import edilirse ilgili kütüphane dosyaları, ilgili dosyamızın içine kopyalanır. bu durumda kopyalanan bu dosyalar header dosyalarımız olur. C/C++ buna en iyi örnektir.

java c# gibi dillerde header file yoktur. çünkü sadece ilgili kütüphanenin referansı tutulur. bunlara da __dynamic library symbols__ denir.

# symbol (or sembol)
IDE'lerde "find symbol" olarak ta menulerde bu seçeneği görebiliriz. 

symbol bazı programlama dillerinde __identifier__ yada __atom__ olarak ta isimlendirilir.  

symbol programlama dillerinde: metod referansları, instance referansları ve sınıf referanslarıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# consul
kelime anlamı: konsolos

- açık kaynaklı discovery server'dır.
- Raft (kelime anlamı: sal) consensus (kelime anlamı: fikir birliği) algoritmasını kullanmaktadır.
- key/value storage'si ile configurasyon altyapısı da sunmaktadır.

# raft algortiması
raft algoritması node'ların aralarında nasıl anlaşmaya varacaklarını belirleyen protokol için kullanılmaktadır.

__Raf, Paxos__ algoritmasına dayanır.

Consul mimarisinde, her programcık, consule agent'ını (kütüphanesini) bulundurmak zorundadır. Consul agent'lar consul server'lara bağlanır. sistemde bir çok consul server vardır. consul server'lar ise kendi içlerinde lider seçerek haberleşirler.

1 agent birden fazla consul server'a bağlı olabilir. bu şekilde birine birşey oldumu diğerinden bilgi almaya devam eder.

raf'ta her node (consul server) 3 farklı state'de bulunabilir:
- follower
- candidate (aday)
- leader

İlk başta her node follower'dır. eğer bir lider'den haber alamazlarza, kendilerini candidate olarak belirleyebilirler. candidate olan node, diğer node'lara vote için request yollar. Bu olaya **"leader election"** denmektedir.

Sistemde bir data güncellemesi yapacak olalım. x=1 yapalım. client lidere x=1 bilgisini yolluyor. bu güncelleme her node'a leader tarafından yollanıyor. eğer çoğunluk (majority) dönerse, lider tekrar herkese bu bilginini herkes tarafından güncellendiğini onayladığı mesajını yolluyor. herkese bu bilgiyi yolladığında client tarafa da datanın güncellendiğini bildiriyor. bu olaya **"Log Replication"** deniliyor. Lider tarafından herkese yollanan data güncelleme request'ine **Append Entry message** deniliyor.

  - ## some timeouts

       - ### election timeout
         raft algoritmasında lider seçemk için her follwer'ın candidate olması için random bir süre vardır. genelde 150ms ile 300ms arasında değişir. bu şekilde tüm sistem aynı anda candidate olmamış olur.

       - ### heartbeat timeout
         lider sürekli olarak heartbeat ile follower'ları kontrol eder ve hepsinden dönüş alır. eğer follower'lar heartbeat isteğini liderden almazlarsa, o zaman yeniden o follower'lar election'a gidecektir. heartbeat için follower tarafında da bir timeout vardır.

# majority of votes
lider seçilirken, candidate'in en az sistemdeki node sayısı + 1 kadar oy alması gerekir. eğer bu sayı daha düşük olursa o zaman farklı bir candiate'te kendini lider olarak kabul edebilir.

# network sorunları
node'lar biribiri ile haberleşirken, node'ların bir kısmının biribi ile iletişiminin kesildiğini düşünelim. böyle bir durumda her iki grup kendi içinde lider seçecektir. client hangi lidere data güncelleme bilgisi yollarsa, artık datası sadece o grupta güncelleniyor olacaktır. bir süre sonra 2 grubun network erişimi tekrar düzelir ve birbirleri ile iletişime geçerlerse, iki grubun lideri daha çok oy toplamış bir grubun lideri karşısında kendini follower'a çekecek ve kendi güncellemelerini roll-back edecektir. yeni güncellemeleri lider'den alacaktır.

# Ethereum and Bitcoin
sanal para sistemlerinde consensus raft veya paxos yada bunlardan türemiş teknikler kullanılmamaktadır. çünkü sanal paralarda lider seçimi söz konusu değildir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Cycle detection

- ### Floyd's Tortoise and Hare
	
  Floyd tarafından geliştirilen bu yöntemde kamlumba ve tavşan birer pointer'dır.

	Aşağıdaki kod üzerinde Floyd  algoritması uygulanmış ve kaplumba=slow, tavşan=fast olarak isimlendirilmiştir.

  Floyd algoritmasında, tavşan kaplumpağadan önce döngü içerisine girecektir ve döngü içinde birbirlerine muhakkak denk geleceklerdir. algoritmanın kodlaması çok basittir. algoritma çalışmasında ek belleğe ihtiyaç duyulmaz. sadece 2 pointer vardır.

  Aşağıda şekilde döngüsel linkedlist'imiz olduğunu varsayalım.
  - Çizgiler x uzunluğunda (x adet node olsun), 
  - eşittir işaretleri y uzunluğunda
  - yıldız z uzunluğunda

  Eğer tavşan ve kamplumbağa yıldızlı node'ların başında buluşuyorsa;
  - Distance travelled by slowPointer before meeting = x+y
  - Distance travelled by fastPointer before meeting = (x+y+z)+y = x + 2y + z

  Bu durumda;
    
  > 2 * dist(slowPointer) = dist(fastPointer)

  > x = z çıkmaktadır

  Slow ve fast buluştuğunda liste döngüsel demektir. Bunun sebebi yukarıdaki demklem değil. Yukarıdaki denklem ek olarak bizim döngüdeki döngünün başladığı noktayı bulmamızı şu şekilde sağlayacak: Eğer slowpointer'ı dizinin en başına koyarsak ve her iki pointer'ı da artık aynı hızda ilerletirsek, 2 pointer döngünün başladığı nokta olan kısımda (bizim şeklimizde eşittir işaretinin en başı) buluşacaklardır. çünkü x=z'dir. 

  Aşağıdaki java kodu sadece listenin döngüsel olup olmadığını tespit etmektedir.

```
    <...x...>                      <....y
________________======================  :
                *                    =  :
                *                    =  v
                *                    =
                **********************
                  <...z...>
```

```java
public class App {

	public static void main(String[] args) {
		Node ten = new Node("10");
		Node twenty = new Node("20");
		Node thirty = new Node("30");
		Node fourty = new Node("40");
		Node fifty = new Node("50");

		ten.next = twenty;
		twenty.next = thirty;
		thirty.next = fourty;
		fourty.next = fifty;
		
		// here is the cycle.
		// we point to first node.
		fifty.next = ten;

		if (isCircle(ten)) {
			System.out.println("test passed.");
		}
	}

	static boolean isCircle(Node first) {
    
		Node fast = first;
		Node slow = first;

		while(fast!= null && fast.next != null){
		  fast = fast.next.next;
		  slow = slow.next;
		  
		  if( slow == fast )
		     return true;
		}
		return false;
	}

	static class Node {
		Node next;
		String data;

		public Node(String data) {
			this.data = data;
		}
	}
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# language server protocol (or LSP)

Language server IDE'den bağımsız çalışan bir yazılımdır. ide (client) sunucuya (language server'a) bağlanır ve ona kodları yollar, kodları alan sunucu sürekli olarak client'e rapor verir. her ide için ayrı eklenti yazmaktansa, IDE'ler bu protokolü desteklediği sürece her dile destek verebilirler.

language server ile neredeyse herşey yapılabilir. örnek:  code completion, hover tooltips, jump-to-definition, find-references...

language server ile client'ın haberleştiği protokol LSP'dir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Google Cloud

 - g suite
   - gmail
   - docs
   - keep (personel note)
   - calendar
   - google search
 - Google Cloud Platform
 - Firebase
   - Firebase Cloud Messaging (or FCM or old-name:Google Cloud Messaging (or GCM) ilk kurulduğundaki ismi: Android Cloud to Device Messaging (or Cloud to Device Messaging or C2DM)
   - Firebase Authentication
   - Firebase Crashlytics
 - compute
   - Compute Engine (remote VM)
   - App Engine (AWS Elastic Beanstalk alternatifi)
 - Google Maps Platform

Firebase: mobile uyglamaya (ios ve andorid) google-firebase-lib ekleniyor. lib google firebase servislerine bağlanıyor ve otomatik istatistik yolluyor.

Google cloud alt servislerinin ayrı ayrı, microsoft bulut ve amazon bulut hizmetlerinin hangilerinme denk geldiği tek tek burada listelenmektedir:

(source-id: 36) "Service comparisons" başlığı.

(source-id: 37) "Service comparisons" başlığı.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# virtualbox içerisinde Resolution ayarlama
Çözünürlük ilk makina kuruldugunda küçük gelir. Arttirabilmek için "guest additions" eklentisi ziyaretçi makinaya kurulmalidir. guest restart edilir. Virtualbox --> görünüm --> "misafir ekranini otomatik yeniden boyutlandir" seçenegi, anlik olarak guest isletim sisteminin virtualbox penceresini kaplayacak sekilde genislemesini saglamaktadir.

# virt-manager içerisinde Resolution ayarlama
direk olarak masaüstü görüntü ayarları genişletilebilir. ek bir ayara gerek yok.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Virtualbox üzerinde dosya paylaşımı

- ISO file
dosyaları direk olarak mount edebiliyoruz. Bu sebeple bir dosyayi virtualmachine tasimak istedigimizde ISO dosyasi içerisine atmamiz yeterli olacaktir. ISO dosyası direk 7zip, Peazip gibi uygulamalarla oluşturulamıyor. Linux ve Windows için şu çözümler kullanılabilir:
- Windows üzerinde dosyalari ISO dosyasina atabilmek icin "cdrtfe" (portableapps.com formatinda da mevcut) uygulamasi kullanilabilir. "cdrtfe" açildiginda "options" butonuna basilir. "ISO image" bölümünden "create image only do not burn" enabled edilir.
- Linux üzerinde şu komut ile iso yaratılır: mkisofs -o /home/user/folder.iso /home/user/folder

- drag and drop
"guest additions" eklentisi ziyaretçi makinaya kurulmalidir. guest restart edilir. bu sekilde kopyalanan metinlerde, ziyaretçi-host arasinda paylasilabilir olmaktadir. Bu özelligi enable etmek için, General --> Advance kismindan enable edilmelidir.
Drag and drop ile klasör tasima islemlerinde sorun oldugu görüldü. Tek dosya tasimak gerekebilir.
Drag and drop ve kopyalama panosu paylasimi özellikleri virtualbox 5'inci sürümü öncesi stabil olmayan eklentilerle saglaniyordu. Fakat 5'inci sürüm ile birlikte stabil ve eklentisiz desteklenmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# hypertext
gerek aynı dökümanın içerisinde bir yere referans ederek, gerekse farklı bir dökümana işaret eden linkler içeren text dosyalarına/dökümanlarına verilen isimdir.

# hyperlink
"link" ile eşanlamlıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# nexus vs artifactory
birbirine alternatif maven, gradle, npm gibi birçok farklı altyapılar için merkezi dependency/artifact barındırırısıdır.
sonatype firması nexus'u, JFrog firması artifactory'yi geliştiriyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# remote desktop software comparison

# Remote Desktop Connection (or RDC or Remote Desktop or (eski adı) Microsoft Terminal Services Client or (eski adı) mstsc or (eski adı) tsclient)
İsimleri çok genel bu yüzden karışıklıklara sebep olabilir. Microsoftun uzak masaüstü için kullandığı yazılımdır.

Client ve sunucu iletişiminde yine microsoft'un geliştirdiği Remote Desktop Protocol (RDP) kullanılmaktadır.

resmi mac, android, ios client versiyonları mevcuttur.

# Remmina
windows RDP'yi de destekleyen, linux için multi-protocol client.

# VNC
- Açık kaynaklı uzak masaüstü destekleyen bir protokoldür.
- Protokolü kullanan birden fazla ürün mevcuttur.
- VNC, teamviewer gibi ekran görüntüsünü paylaşmamaktadır. Sunucu tarafta sanal bir X session'u açmaktadır (bu __Xvnc__ oluyor). bu X session'ına client taraftan bağlanmayı sağlamaktadır.

# winvnc
VNC, x'e göre çalıştığından normal koşullarda ms windows ortamında çalışamaz. winvnc sadece ms windows için geliştirimiş bir vnc sunucu uygulamasıdır.

# x11vnc
standart VNC protokolü sadece uzak masaüstündeki sanal X11'e bağlanılabilmesini sağlıyor. fakat x11vnc; zaten açık olan X session'ına bağlanılmayı sağlıyor. x11vnc sadece server tarafındaki yazılımdır. herhangi bir vnc client'ta x11vnc'e bağlanabilir.

X11vnc ve vnc'nin yaptığını X zaten destekliyor. fakat vnc ve x11vnc bazı şeyleri disable ederek, network bağlantısında daha az data transferi üzerinden çalışmasını sağlıyor.

X11vnc projesinin geliştirilmesi 0.9.13 sürümünde durdu. daha sonra LibVNC github kullanıcısının, x11vnc reposunda forklanarak geliştirilmesi devam ettirilmektedir.

LibVNC kullanıcısının altındaki LibVNCServer ve LibVNCClient repoları cross-platform C kütüphaneleridir. Bu kütüphaneler ile vnc client veya vnc uygulaması geliştirilebilir.

# noVNC
VNC client using HTML5, WebSockets and Canvas.

# vnc kullanan uygulamalar ve diğer uygulamalar ile karşılaştırması:

| app name                                  | licence     | ms windows server | ms windows client | mac server | mac client | linux server | linux client | bsd server | bsd client | java client | android client | android server | ios client | ios server | chrome os client |
|-------------------------------------------|-------------|-------------------|-------------------|------------|------------|--------------|--------------|------------|------------|-------------|----------------|----------------|------------|------------|------------------|
| TightVNC                                  | GPL         | Yes               | Yes               | No         | Yes        | Yes          | Yes          | Yes        | Yes        | Yes         | Yes            | ?              | ?          | No         | ?                |
| TigerVNC                                  | GPL         | Yes               | Yes               | No         | Yes        | Yes          | Yes          | Yes        | Yes        | Yes         | No             | ?              | No         | No         | ?                |
| TurboVNC                                  | GPL         | No                | Yes               | No         | Yes        | Yes          | Yes          | Yes        | Yes        | Yes         | No             | ?              | No         | No         | ?                |
| UltraVNC                                  | GPL         | Yes               | Yes               | No         | No         | No           | No           | No         | No         | Yes         | No             | No             | No         | No         | ?                |
| X11vnc                                    | GPL         | No                | Yes               | Yes        | Yes        | Yes          | Yes          | ?          | Yes        | Yes         | ?              | ?              | ?          | No         | ?                |
| RealVNC Free                              | Proprietary | Yes               | Yes               | Yes        | Yes        | Yes          | Yes          | No         | Yes        | Yes         | Yes            | ?              | Yes        | No         | ?                |
| RealVNC Personal                          | Proprietary | Yes               | Yes               | Yes        | Yes        | Yes          | Yes          | No         | No         | Yes         | Yes            | ?              | Yes        | No         | ?                |
| RealVNC Enterprise                        | Proprietary | Yes               | Yes               | Yes        | Yes        | Yes          | Yes          | No         | No         | Yes         | Yes            | ?              | Yes        | No         | ?                |
| Remmina                                   | GPL         | No                | No                | No         | Yes        | No           | Yes          | No         | Yes        | No          | No             | ?              | No         | No         | ?                |
| Remote Desktop Services/Terminal Services | Proprietary | Yes               | Yes               | No         | Yes        | Yes          | Yes          | No         | Yes        | ?           | Yes            | ?              | Yes        | No         | ?                |
| SSH with X forwarding                     | GPL         | No                | Yes               | No         | Yes        | Yes          | Yes          | Yes        | Yes        | No          | Yes            | ?              | Yes        | No         | ?                |
| TeamViewer                                | Proprietary | Yes               | Yes               | Yes        | Yes        | Yes          | Yes          | No         | No         | Yes         | Yes            | Yes            | Yes        | No         | Yes              |
| Ammyy Admin                               | Proprietary | Yes               | Yes               | No         | No         | No           | No           | No         | No         | No          | No             | ?              | No         | No         | ?                |
| Apple Remote Desktop                      | Proprietary | No                | No                | Yes        | Yes        | ?            | No           | No         | No         | No          | No             | ?              | No         | No         | ?                |

# Teamviewer
mobile de bağlanılmasını sağlıyor.

birçok teamviewer uygulaması mevcut:
- Android markette "QuickSupport" uygulaması, mobile'e bağlantı yapılabilmesini sağlayan uygulama.
- "QS Add-on" prefixi ile başlayanlar QuickSupport uygulamasının yanına kurulan, her firma için ayrı ayrı logo ve hızlı bağlantı çeşitleri içeren uygulamalardır.
- Masaüstü versiyonlarda "QuickSupport" uygulaması kurulumsuz olarak başlayan ve sadece sunucu modunda açılan ayar sunmayan, iş yerleri müşterileri için hazırlanmış bir versiyondur.
- Android markette "Host" uygulaması android'e servis olarak kuruluyor. böylece uygulama açık değilken bile uzaktan bağlantıya izin veriyor.

# Chrome Remote Desktop
- masaüstünde chrome eklentisi olarak çalışıyor (sunucu modu dahi).
- mobile versiyon google chrome'a eklenti diil. android uygulaması.
- linux tarafında sunucu olması için bazı ayarlar yapmak gerekebiliyor.
- chromium tarayıcısında da çalışıyor.
- mobile'den masaüstü yönetiliyor. fakat mobil yönetilemiyor.
- google hesabı ile login zorunlu.

# Ammyy Admin
kullanılması tehlikeli derecede güvensiz bir uygulama.

ip'siz (id aracılığı ile) bağlanılabilmeyi sağlıyor.

windows harici sistemler için indirmesi ücretli.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# cron
cron kelimesi yunanca'da zaman anlamına gelen xronos'tan gelmektedir.

"cron" unix tabanlı sistemlerde istenilen saatlerde çalışması istenen scriptleri çalıştıran yazılımın özel ismidir. ismi çok sıkça kullanıldığından; cronjob denildiğinde, herhangi bir platformda arkaplanda scheduled yürütülen job'lar anlamında kullanılır. oysa bu terimi diğer job'lar için kullanmak tamamen yanlıştır.

- cronjob
cron uygulaması birçok farklı scripti farklı zamanlarda çalıştırabilir. her başlatılan script birer cronjob'tır.

- crontab
"cron table" cron uygulamasının configurasyon dosyasıdır. bu dosya tablo gibidir. her satırda zaman ve o zamanda başlatılacak script yazmaktadır.

scheduler görevi gören birçok uygulama yazılmıştır. bazıları aynı veya benzer komut satırı ismiyle çağrılmaktadır.

- expression format

  expression formatı her yazılıma göre değişmektedir. kaynak: (source-id: 38) "Features" başlığı, 11inci madde.

  - Unix (source-id: 39)
  - Cron4j (source-id: 40)
  - Quartz (source-id: 41)
  - Spring (source-id: 42)
  
  - diğerleri: nnCron

- tarih formatı

(Unix standartına göre anlatılmıştır)

```
* * * * * *
| | | | | | 
| | | | | +-- Year              (range: 1900-3000)
| | | | +---- Day of the Week   (range: 1-7, 1 standing for Monday)
| | | +------ Month of the Year (range: 1-12)
| | +-------- Day of the Month  (range: 1-31)
| +---------- Hour              (range: 0-23)
+------------ Minute            (range: 0-59)
```

- özel karakterler

(Unix standartına göre anlatılmıştır)

  - \*

    'her' anlamında kullanılır. örneğin, dakika sutununa yıldız koyarsak, her dakika anlamına gelir.

  - , 

    birden fazla değer koymak istediğimizde kullanılırız.

  - \-

    birden fazla değeri kullanmak için kullanırız. örnek: mon-fri, or 9-17 
  
  - */x

    'her n' anlamına kullanılır. örnek: her beş dakika için, dakika sutununa */5 yazılmalıdır.

- örnekler

(Unix standartına göre anlatılmıştır)

```
* * * * * *                                Each minute
       
59 23 31 12 5 *                            One minute  before the end of year if the last day of the year is Friday
									       
59 23 31 DEC Fri *                         Same as above (different notation)
       
45 17 7 6 * *                              Every  year, on June 7th at 17:45
       
45 17 7 6 * 2001,2002                      Once a   year, on June 7th at 17:45, if the year is 2001 or 2002
       
0,15,30,45 0,6,12,18 1,15,31 * 1-5 *       At 00:00, 00:15, 00:30, 00:45, 06:00, 06:15, 06:30,
                                           06:45, 12:00, 12:15, 12:30, 12:45, 18:00, 18:15,
                                           18:30, 18:45, on 1st, 15th or  31st of each  month, but not on weekends
        
*/15 */6 1,15,31 * 1-5 *                   Same as above (different notation)
       
0 12 * * 1-5 * (0 12 * * Mon-Fri *)        At midday on weekdays
       
* * * 1,3,5,7,9,11 * *                     Each minute in January,  March,  May, July, September, and November
       
1,2,3,5,20-25,30-35,59 23 31 12 * *        On the  last day of year, at 23:01, 23:02, 23:03, 23:05,
                                           23:20, 23:21, 23:22, 23:23, 23:24, 23:25, 23:30,
                                           23:31, 23:32, 23:33, 23:34, 23:35, 23:59
       
0 9 1-7 * 1 *                              First Monday of each month, at 9 a.m.
       
0 0 1 * * *                                At midnight, on the first day of each month
       
* 0-11 * * *                               Each minute before midday
       
* * * 1,2,3 * *                            Each minute in January, February or March
       
* * * Jan,Feb,Mar * *                      Same as above (different notation)
       
0 0 * * * *                                Daily at midnight
       
0 0 * * 3 *                                Each Wednesday at midnight
```

https://crontab.guru/ sayfası expression'a karşılık gelen zaman dilimlerini ekrana basıyor. buradan kontroller yapılabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Omnibox
Çok amaçlı adres çubuğudur. tarayıcılarda adres çubuğu sadece url'ye gitmek için değil, aynı zamanda arama yapma, matematik işlemleri yapma gibi birçok özellikte barındırır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Sistem Programcılığı
Daha çok işletim sistemi ile yada donanım bilgisi gerektiren yazılım dilleri ve kütüphaneleri kullanarak yazılım geliştirmedir. Bu sebeple; genelde üst seviyeli diller buna gruba dahil olmaz. Bu sebeple; genelde sürücü (driver) yazanlar bu gruba dahildir.

# sistem çağrıları (or çekirdek çağrıları)
İşletim sistemi ile kullanıcı programları arasında tanımlı olan arayüz, işletim sistemi tarafından tanımlanan bir prosedürler kümesidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# p2p (peer-to-peer or eşlerarası)

genel bir terimdir. client'ların direk birbiri ile haberleşip transfer yaptığı, sunucunun aracılık yapmadığı protokollerdir. sunucu sadece client'ların birbirini görebilmelerini sağlamakla yükümlüdür. eğer client'lar biribinin network adreslerini biliyor ise, sunucuya hiç gerek kalmaz. 

BitTorrent p2p'ye en iyi implementasyon örneğidir.

# BitTorrent

BitTorrent protokolün ismidir. aynı zamanda BitTorrent firmasının geliştirdiği, BitTorrent yazılımı bu protokolü kullanan bir client'tır.

# torrent

paylaşımda (or paylaşıma açık or hazır) olan dosya or dosyalar grubu için kullanılan terimdir.

# torrent file (or METAINFO)

.torrent uzantılıdır.

file that contains metadata about files and folders to be distributed, and usually also a list of the network locations of trackers.

# Availability

Also known as "distributed copies". The number of full copies of a file. Each seed adds 1.0 to this number. eğer 1 kişide tam dosya ve 1 kişide yarım dosya varsa o dosya için Availability 1.5 olur.

# Seed (or tohum)

seeder, dosyayı paylaşan toplam client sayısıdır.

# Leech (or sülük)

Leecher dosyayı çeken toplam client sayısıdır.

# Peer (or eş)

Seed ve Leech in toplamındır.

# Tracker

Torrentin bağlandığı sunucudur. Torrenti çeken Peerler ve Trackere dosya hakkında bilgi gönderirler. Diğer Peerler ise Trackere bağlanarak kimde hangi dosyanın hangi parçalarının olduğunu öğrenirler. Tracker üzerinden kesinlikle dosya transferi gerçekleşmez. sadece Kim nekadar dosya çekti ve ne kadar yükledi gibi İstatislik bilgilerinide barındırabilir.

# DHT (or Distributed Hash Table)

tracker'dan bağımsız çalışabilmek gerektiğinde tracker gibi tüm istatistikleri toplamak gerekir. işte bu toplanan bilgilerin tümü DHT tablosunda toplanır.

# Ratio (or oran)

torrent'in Upload işleminin Download işlemine oranıdır.

# Hit&run

Dosyayı çekip hemen paylaşımdan kaldırma işlemine ve kaldırana verilen isimdir. Torrent dünyasında kesinlikle sevilmezler.

# Choked

kelime anlamı: tıkanmış

diğer client'lar X client'ına dosyayı yollamıyorsa, X client'ı chocked olmuş olur.

# Lurker

dosyayı indiren ve paylaşan client'tır. fakat indirdiği dosya haricinde farklı bir dosya paylaşmayan client'tır.

# swarm

kelime anlamı: sürü

bir torrent'i paylaşan tüm client'lara verilen isimdir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# 3rd party software

terminolojik açıdan bakıldığında; developer 1, müşteri 2inci kişiler oluyor. 3 üncü kişiler ise 1 ve 2 dışında yazılım sağlayanlar oluyor. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# otonom (or autonomous)
kendi kuraları/işleyişi olan. özerk sistem.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# awesome

- bir rozet (or badge)'tir.

- "The awesome manifesto" altında tanımlaması yazılmıştır.

- en iyi kitaplar listesi, android open source uygulamalar listesi, c# için yazılmış ingilizce kitaplar listesi gibi koleksiyon sayfalarına bu etiketi her isteyen koyabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Input Form validasyonları

# Posta kodu (or postal code)
Her ülkede farklı terminoloji kullanılmaktadır. bazı örnekler:

- amerika da ZIP Code
- hindistan da PIN Code (Postal Index Number'ın kısaltması)
- Brezilya da CEP
- İrlanda da Eircode

posta kodu'nun formatı ülkeden ülkeye değişiklik göstermektedir (bazı ülkelerde harf boşluk ve tire işareti dahi mevcuttur). bu sebeple; son kullanıcıya önce ülke seçimi yaptırılmalı ve posta kodu validasyonu devreye girmelidir.

türkiyede posta kodu mahalle'yi temsil etmektedir. fakat bazı ülkelerde, şehir/semt/mahalle kavramlarının seviyeleri farklı olduğundan, posta kodu farklı bir seviyeye denk gelebilir.

türkiyedeki seviyeler (büyükten küçüğe):
- il
- ilçe
- semt
- mahalle veya köy (aynı seviyedeler)

Bazı ülkeler, bazı posta kodlarını spesifik kurumların adresine veriyor. bunlar genelde yoğun posta alan devlet daireleri gibi kurumlar, yada büyük kampüsler/yerleşkeler oluyor.

Genelde e-ticaret firmaları ülke bazlı kontrol yapıyor yada sadece karakter sayısını kontrol ediyor. adresin yanlış girilmesi sorumluluğu son kullanıcıya bırakılıyor.

# Administrative division (or idari bölünme)
her ülke kendi içinde birçok alt bölge ayrım içindedir. son kullanıcıya adres formu doldururken, eğer site uluslararası bir site ise (tüm dünyaya yada geniş bir alana hizmet veriyor ise) sadece ülke ve şehir bilgisi otomatik selectbox'tan tamamlanır. bir de her zaman son kullanıcıya adresi kendisi girmesi için textbox bırakılır. adres kullanıcının sorululuğundadır. çünkü her ülkeyinin tüm seviyelerinini otomatik selectbox'tan tamamlanması çok zordur. her ülkenin bilgisi dönem dönemde (zaman zaman) değişebiliyor. sürekli bu dataları güncel tutmak büyük maliyet. bazı kaynaklar bunları web servisi yada offline olarak sağlıyor, fakat tüm detayların doğru olduğundan hiçbir zaman %100 emin olamıyorsunuz. Google'ın "Places" servisi otomatik tamamlamayı ücretli şekilde sunuyor.

eğer birkaç yada tek bir ülkeye hizmet veren bir yazılım geliştiriliyorsa, tüm seviyelerin kaynaklarını bulmak kolay oluyor. fakat tüm dünya için bu detaylar çok maliyetli.

tüm dünyanın veritabanı olsa dahi, her seviyenin isminin hangi dilde son kullanıya gösterileceği de önemli. türkçe olarak sitede gezip form dolduran bir son kullanıcı, adres formunda amerikayı seçtiğinizde her seviyenin türkçe çıkması gerekecektir. bunların kombinasyonu çok fazla.

Bazı seviyeler bazı durumlarda atlanabiliyor (boş geçilebilmesi gerekiyor). Örneğin amerika'da Washington DC, bherhangi bir eyalete bağlı diil.

sadece şehir/ülke kombinasyonu yeterlidir. Amazon gibi büyük firmalar bu şekilde yapıyorlarlar (yıl 2018).

php'de kullanılan bir kütüphaneye baktığımızda ((source-id: 43)) veritabanı adres modelinin şu olduğu görülüyor:

- Country code
- Administrative area
- Locality (City)
- Dependent Locality
- Postal code
- Sorting code
- Address line 1
- Address line 2
- Organization
- Given name (First name)
- Additional name (Middle name / Patronymic)
- Family name (Last name)

Yukarıdaki modelin OASIS eXtensible Address Language (xAL) standard'ten alındığı belirtilmiş. Kütüphanenin github root readme dosyasında şu not düşülmüş:

The dataset is stored locally in JSON format ((source-id: 44)). Countries are generated from CLDR v37 ((source-id: 45)). Address formats and subdivisions are generated from Google's Address Data Service ((source-id: 46)).

Google's Address Data Service'inden TR/İstanbul'u seçtiğimizde bu sayfa karşımıza çıkmaktadır: (source-id: 47) içerdiği bilgi şudur:

```json
{"id":"data/TR/İstanbul","key":"İstanbul","lang":"tr","zip":"34","isoid":"34"}
```

# isim soyisim (full name)
- her ülkede farklı standartlar vardır.
- bazen nufusa yanlış yazılmış, fakat değiştirilmemiş karakterlerde çıkabiliyor. bu sebeple ülke bazlı dahi düzgün bir validasyon/regex mevcut değildir.
- yunan gibi alfabeler de hesaba katıldığında validasyon bulmak çok zor. bu sebeple bazı siteler validasyon yaparken sadece bazı karakterleri exclude ediyor. çünkü sadece kabul edilen karakterler çok fazla. 
- tüm karakterler kabul edildiğinde bu sefer işaret karakterleri de kabul edilmiş oluyor. bu durum yunanca gibi diller işin içine girince daha da zorlaşıyor.
- sayı(lar) içeren isimlerde mevcut.
- tek kural şu denebilir: isim ve soyisim en az birer karakterden oluşmak zorundadır ve bu karakterler Unicode'da control karakteri property'sine sahip olmamalıdır. (Tabi yine daha fazla detaya girilirse; Unicode'da farklı "boşluk" karaterleri var. Onları da exclude etmek gerekebilir.)
- standart olarak her zamanki gibi, XSS saldırıları için text'i denetlemek gerekir.

# yaş
- minimum yıl seçeneği çok eskiye dayanmalıdır. resmi olarak kayıtlarda ülkeye ölü bilgisi gelmeden o kişi ölü sayılamaz. ve sistemde kaydı açılması gerekiyor ise; bu kişinin doğum yılı çok eski tarih olabilir. e-devlet gibi sistemler düşünüldüğünde yaş validasyonunu yüksek tutmakta yarar var.

google, yahoo, apple gibi sitelerin kayıt sayfalarında 1865'ten itibaren doğum yılı validasyonları kabul ediliyor (yıl 2019).

# telefon mobil numaraları
her ülke için değişmektedir.

https://github.com/google/libphonenumber projesi c++, java ve js için ortak repo altında kütüphane sunmaktadır. bu kütüphane ülke bazında validasyon sağlamaktadır. aynı standartları uygulayan diğer diller için "Third-party Ports" başlığında listelenmektedir: https://github.com/google/libphonenumber#third-party-ports

# email ve url
email ve url'ler global oldukları için çoğu yazılımcı tarafında elle regex tanımlanarak kontrol edilir. elle yazmak mantıklı, fakat ayrıntıya girilirse çok detay var:

- domainin uzantısı en az 2 karakter olmalı
- domainin uzantısı istenildiği kadar uzun olabilir ve sayı içerebilir
- domainin uzantısı sayı ile bitemez
- bazı URL bilgilerinde IP girilebiliyorsa, regex çok daha karışık olmaktadır (IP4 ve IP6 da unutulmamalı)
- emaillerde john@server.department.company.com gibi subdomain'ler olabilir

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# windows kitaplıkları

windows'un yeni sürümleri ile birlikte dosya yöneticisinde kitaplık özelliği geldi. bir kitaplık birden fazla dizini aynı klasörmüş gibi gösterebiliyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# windows güncellemeleri

windows xp'den itibaren güncellemeleri toplu şekilde gruplandırarak "service pack" isminde ayrı setup'larda sunuyordu. tek tek güncelleme kurmak yerine bu tercih edilebilirdi.

windows 10 ile birlikte isimlendirme service pack olarak adlandırılmıyor. onun yerine piyasaya özel isimlerle sunuluyor. sırası ile 2018'e kadar aşağıdaki paketler sunuldu:

November Update

Anniversary Update

Creators Update

Fall Creators Update

April 2018 Update

October 2018 Update 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# type safe

programlama dilinin bir özelliğidir. eğer değişkenlerin tipleri belli edilmek zorunda ise o dil type-safedir. örneğin javada bir değişken oluşturulduğunda int, object, string olup olmadığı belirtilmek zorundadır bu yüzden java type-safe'dir. oysa javascript'te tüm değişkenler "var" ile belirtildiğinden type-safe değildir.

# Type Inference
tipin otomatik algılandığı dillerdir. bir objenin tipi dil tarafından otomatik algılanır ve ona göre tutulur. eğer ilerdeki kod satırlarında aynı referansa farklı bir tipte değer set etmeye çalışırsak runtime'da hata alırırız. kaynak: https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html title: "Type Safety and Type Inference".

# Static typing language vs Dynamically typing language
variable tiplerinin compile-time sırasında kontrol edildiği diller Statically typed dillerdir. tipler sadece run-time sırasında kontrol ediliyorsa Dynamically typed dildir.

her iki dilde de tip'ler vardır (type safety).

script dilleri genelde Dynamically typed'tır.

JS Dynamically typed'tır. fakat TypeScript Static typed'tır.

# static binding (or early binding) vs dynamic binding (or late binding).

Dog d1=new Dog();  --> static binding

Animal a=new Dog();  --> dynamic binding

# Compile Time Polymorphism vs Run Time Polymorphism

polimorfizm bir nesnenin farklı şekillerde davranabilmesidir. bu sebeple iki farklı polimorfizm gözlemlenebilir:

compile time --> Static binding veya Method overloading olan durumlarda geçerlidir

run time --> Dynamic binding veya Method overriding olan durumlarda geçerlidir

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Bağlaşım (or Coupling)

sınıfıların birbirine bağımlı olma durumlarıdır. X sınıfında değişiklik yapınca Y'de de değişiklik yapılması gerekiyor ise Y, X'ye bağlıdır.

# Gevşek bağlılık (or Loosely Coupled) vs Sıkı bağlılık (or Tightly Coupled)

sıkı bağlılık örnek:

```java
class Traveller {

    Car c = new Car();

    Public void startJourney() {

        c.move();

    }

}
```

gevşek bağlılığa örnek:

```java
class Traveller {

    Arac c; //burada injection şart

    Public void startJourney() {

        c.move();

    }

}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# debounce
bounce kelime anlamı: sıçramak

debounce kelime anlamı: sıçramayı engellemek

bir butona bastığımızda (or bir event olduğunda) genelde bir metod tetiklenir.  eğer bu event üstüste sürekli gerçekleşirse her defasında bu eventi yapmak yerine 3 saniyede bir yapmayı tercih ederiz. işte bu yapacağımız yöntem ile sıçramayı engellemiş oluruz.

örnek:

> var debouncedMethod = API.debounce(myMethod, 3);

artık debouncedMethod'i üstüte çağırırsak max 3 saniyede bir execute edilecektir. yani üstüste çağırmalarımız ignore edilecek.

Yukarıda API bir kütüphaneyi temsilen yazıldı. örneğin lodash'te debounce metodu vardır. her proramlama dili için debounce sağlanabilir.

debounce kullanım alanına örnekler:

- web syafasındaki form için post butonu event'i

- GUI'mizin resize olduğundaki event. her snaiye tekrar render yerine, 2 saniyede 1 render etmek cpu'yu daha az yoracaktır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Automatic content recognition (or ACR)

media yada belge dosyalarının otomatik tanınması teknolojisidir.

# acoustic fingerprinting

ses dosyalarının tanınması için tasarlanan teknolojilerdir. ACR'nin bir alt kümesidir.

# video fingerprinting

video dosyalarının tanınması için tasarlanan teknolojilerdir. ACR'nin bir alt kümesidir.

# Watermark (or tr:filigran or tr:suyolu)
fiziksel olan: örneğin paralarda sadece ışığa tutulduğunda görünen bir şekil vardır bu şekilde o paraya id atanabilir. fakat normal kullanımda kullanıcı bunu görmez/bilmez.

benzer şekilde digital dünyadada insan kulağının duymayacağı şekilde her ses dosyasına bir ses yerleştirilir. bu sesi ancak programatik olarak tespit edebiliriz. bu şekilde o ses dosyasını unique yapmış oluruz.

KuroLabs/stegcloak projesi buna örnek verilebilir (başka başlıkta anlatılıyor).

# AcoustID

açık kaynaklı acoustic fingerprinting teknolojisidir.

# Chromaprint

AcoustID için client side C kütüphanesidir. AcoustID fingerprint'i üretir. AcoustID, projenin ismi olarak kullanılmaktadır.

# acoustic fingerprinting temel çalışma prensibi

her acoustic fingerprinting farklı teknikler kullanmaktadır. fakat temel olarak işleyi birçoğunda aynıdır.

bir ses dosyasının acustic fingerprint'i uzunca bir string'dir. MD5 ve SHA'nın tersine, ses dosyasındaki ufak değişiklikler accoustic fingerprint çıktısında ufak değişiklikler yaratmaktadır. tabi bu da tölere edilebilir bir durumdur. örneğin bir web servsine Fingerprint attığımızda en yakın fingerprint'ler benzerlik oranları ile dönmektedir: 

```
{

    results =     (

                {

            id = "3fb2e35c-c4d5-4360-aaff-8dad0aad05e9";

            score = "0.976727";

        },

                {

            id = "b262c597-64b3-42c4-94b0-e89b8c496d76";

            score = "0.9310389999999999";

        },

                {

            id = "49f64d53-de52-4f4b-a08d-8d78ca0001cf";

            score = "0.690862";

        }

    )

}
```

Fingerprint'in %100 benzeşmesi zaten istenmeyen bir durumdur.

Fingerprint hesaplamaları ses çıktısı üzerinden yapılır, ses dosyası formatı ile bağlantılı bir durum diildir.

Örneğin bir ses dosyası olsun. Her 2 saniyesinin sonundaki ses anından bir bilgi üretilsin. bu bilgi 2 sn aralıklarla tutulmuş oluyor. AYnı şarkının farklı bir ses kaydında yada bir konserde, orjinal şarkı kaydı ile aynı tempoda gidilmeyeceği için kontrol edilen şarkı 1'er saniye delay yapılarak tekrar kontrol edililiyor. 

Müzik veritabanları incelendiğinde (public ve ticari olanlarda) veritabanında aynı şarkının birden fazla fingerprint'i olduğu görülür. bunun sebebi şudur: orjinal kayıt sanatçının kayıt/media/prodüksyon şirketi tarafından kaydedilir. 1 fingerprint o zaman oluşturulur. bu şirket hesabı onaylanmamış hesap olabilir. bu gibi bir durumda  bir ses kaydından fingerprint oluşturulup o şarkıya yollayan biri olabilir. yada konser versiyonunu fingerprint olarak o şarkıya atayan olabilir. bazı insanlar ise; bir şarkının konser yada remix versiyonunu  şarkı oarak kaydetmektedir. Bazı şarkılar  albümlerin içinde de gelmektedir, yada bir film müziği DVD'si içerisinde sountrack hediye olarak gelmektedir. onları da  şarkı olarak kaydeden olmaktadır.

Eski klasik müziklerde iş karmaşıklaşmaktadır. Bir semfoniyi komple bir şarkı olarak kaydedenler mevcuttur. Semfoninin ilk 3 ile 5inci bölümünü bir şarkı olarak kaydedenler vardır. bir semfoninin 4üncü bölümünü içeren bir ses dosyasını Chromaprint'e verdiğimizde bize tüm olasılıkları döndürecektir.

# Gracenote

müzik veritabanını dışarıya ücretli API ile sunan bir cloud web servis firması.

# MusicBrainz

açık kaynaklı müzik veritabanı.

# beets

açık kaynaklı müzik arşivi düzenleme programıdır.

# Picard

açık kaynaklı GUI kullanan AcoustID ile MusicBrainz foundution'dan local müzik dosyalarlının tag'leyen uygulama.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Android Studio ve IntelliJ Idea için "build" vs "Make" vs "rebuild"

aşağıdaki işlemler project veya module için sunuluyor. project explorer'da ne seçili ise, aşağıdaki seçenekler seçili olan seviye (proje yada modül) için çalıştırılıyor.

- "android studio: Make" "intellij idea: build" ikisinin sadece menüdeki isimleri farklı. arkada aynı görevi işletiyorlar.

  compile + depend olan kodları/modülleri de compile eder. fakat sadece değişik yapılan sınıfları build eder. bu sebeple path, paket ismi, lib gibi değişikliklerde "rebuild" yapılmalıdır. "make" isminden de anlaşıldığı gibi executable yaratmak için kullanır. zaten bu sebeple depend olan projeleri de birlikte derler.

- clean

  her koşulda target dizinlerini siler.

- Rebuild

  her koşulda herşeyi tekrardan build eder. öncesinde clean'i çağırır. artifact oluşturmaz.

- compile

  sadece bir class yada paket(class grubu) seçili iken menüde görülen bir seçenektir. sadece ilgili(seçili) paketlerin/sınıfların içindeki kodları compile eder.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Semantic Versioning (or Semver)

yazılım sürüm atlama kurallarıdır.

MAJOR.MINOR.PATCH şeklinde gider.

- Major: public API'lerimizde geri uyumlu olmayan geliştirmeler yapıldığında bu sürüm atlanır.

- Minor: public API'lere sadece eklemeler yapıldığında yada public API'ler değişmeden varolan davranışlar değiştiğinde bu sürüm atlanır

- Patch (or tr:yama): public API'lerde değişiklik olmadan çıkılan bugfix'lerde bu atlanır

Bazı firmalar yukarıdaki kurallara uymasada bu kurallarla resmi makale mevcuttur.

Yukarıda bahsedilen public API bir çok katman olabilir: örneğin komut satırından kullanırken ki komut parametreleri, web tarayıcısı için eklentilere sunduğu API, veya her ikisi birden olabilir.

Sayısal artış matematiktekinin tersinedir. yani; 1.9.0 < 1.10.0 'dır.

0.y.z sürümünde public API ile sunulan şeyler pek stabil değildir. 1.0.0 ile artık production ortamına geçilmelidir ve public API kullanılabilir bir stabilitede olmalıdır.

# Romantic Versioning (or RomVer)

HUMAN.MAJOR.MINOR şeklinde gider.

Semver daha çok son kullanıcısı teknik olan ve teknik işlerde kullanılan yazılımlarda kullanılmaktadır. Oysa romver daha son yazılım geliştirici olmayanlar için tasarlanmış yazılımlarda kulanılmaktadır.

Romverde Public API'nin yerini GUI almaktadır.

- Human: son kullanıcıyı ilgilendiren büyük değişikliklerde artar. örnek GUI.

- Major: eskisi ile aynı şekilde kullanılmayan özellikler içeriyorsa bu sürüm artar. örneğin menülerinin yerlerinin değişmesi. yani kullanım kılavuzunun değişmesi gerekeceği durumlarda bu sürüm artar. 

- Minor: GUI'de değişiklik olmadan çıkılan özellikler ve bugfix'ler.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# atom

electron tabanlı text editor.

# atom ide

atom'a ekstra ide prefix/suffix'li eklentiler kurularak atom ide halini alıyor.

# Nuclide IDE

atom tabanlı fakat paketlerin kurulu geldiği ve silinemediği bir ide. react-native projeleri için geliştirilmiştir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Jenkins

en üst seviyede "item"'lar tanımlarız. item'ların çeşitleri:

- project (or old-name:job): tanımlamarımızı yürütecek olan süreçtir.

- pipeline: build sürecinin her defasında dinamik olarak build edildiğinde tanımlabilen bir süreçtir. build'a başlamadan "Jenkinsfile" isimli dosyayı okur ve içindkeilere göre build yapar.

- folder: diğer item'ları bir diinde toplayabilmemizi sağlar.

- external job: jendkinsden bağımsız process'lerin takibi için yapılmış özel bir durum

- multibranch pipeline: bu bir plug-in'in getirdiği item'dır. default gelmez. çekilen kod'un her branch'i için ayrı ayrı Jenkinsfile'ı çalıştırır.

jenkins içinde bazı eklentiler varsayılan olarak yüklü gelir.

Her item "build" edilir.

Yeni bir item oluşturduğumuzda; bizden item'ın çeşidini seçmemiz istenir. buradaki çeşitler default mevcuttur bazıları ise jenkins'e eklediğimiz plug-in'ler tarafından sağlanır. Bazı item çeşitlerinin isminde Project keywordü yer alır. bu tamamen ismin bir parçasıdır. terminolojide project denilen bir kelime yoktur.

Bir item'ı seçtiğimizde ise yeni bir sayfada birçok ayar istenir. bu ayarlar gruplandırılışmıtır. komple bir grup bir jendkins eklentisi tarafından sağlanıyor olabilir. fakat default sunulan gruplarada eklentiler müdahele edebilir. eklentiler default grupların içine yeni form alanları ekleyebilir. bir form alanının sağ tarafında "?" simgesi vardır. ona tıkladığımızda o alan için kısa bilgi çıkar ve hangi eklentinin bu alanı buraya koyduğunu yazar. Eğer ? simgesi yoksa o alan default jenkins ile geliyordur.

Hangi grupların ve hangi form alanlarının gösterileceği, item'ın çeşidine göre değişir. item oluşturulduktan sonra item'ın çeşidini değiştiremeyiz.

# Agent

jenkins master'a, agent'lar bağlanır ve bu agent'larda taskları koşabiliriz.

# node

master ve agent'ların her birine verilen genel isimdir. bir node, agent yada master olabilir.

# Stage

pipeline (türkçe kelime anlamı: boru hattı) içindeki her iş grubuna verilen isimdir. örnek pipeline dosyamız ve içindeki stage'ler:

```js
pipeline {

    agent any 

    stages {

        stage('Build') { 

            steps {

                echo "build started"

                sh 'cd buil_dir'

            }

        }

        stage('Test') { 

            steps {

                sh 'javac soruce_dir'

            }

        }

        stage('Deploy') { 

            steps {

                sh 'docker push *file.jar'

            }

        }

    }

}
```

# step

pieline stage'sinin içindeki adımların her biri.

# Upstream
Upstream: akış yönünün tersine.

bir item diğer bir item'ı tetikleyebilir. tetikleyen item'a, tetiklenen item'ın upstream'i denir. tabi tetiklenen projede downstream oluyor.

# view

tüm item'ların listelendiği anasayfada item'lar gruplandırılabiliyor. her gruba "view" adı veriliyor. 

# workspace directory

her item için bir dizin vardır. her build aynı dizin üzerinde işlem yapar. eğer "workspace temizleme" aktif edilmezse eski build'deki dosyalar sürekli orada kalır.

# build directory

her build bittğinde metadalarını (log, baslangıç bitiş saat bilgisi, istatistik bilgisi ve artifact'ları) build dizini içine kopyalar.

# JENKINS_HOME

- config.xml

- plugins/

- workspace/

  - [itemName]

- jobs/

  - [itemName]

    - config.xml   (job configuration file)

    - latest       (symbolic link to the last successful build)

    - builds/

    - [buildId]/

Bazı jenkins sürümlerinde workspace dizini her JENKINS_HOME/jobs/[itemName]/'in altındadır.

# Pipeline types

iki çeşit Pipeline var:

- Scripted: Groovy dili ile yazılmış dosyadan okuyan pipeline'lardır.

- declarative: özel üst seviyeli bir dil (arkaplanda groovy kullanıyor). Scripted'a göre daha üst seviyeli olduğundan, Scripted'a göre daha kolay fakat daha az özellik sunuyor.

# jenkins'i docker ile kurup job içinde docker kullanma
docker içerisinde docker kullanma konusuna girmekteyiz. bunun için 3 yöntem var:

- container'ımız dışındaki dockerd'ye bağlanmamız gerekli. bunun için container'ımızı açarken bağlama işleminin bu şekilde yapabiliriz:

  > docker container run -d -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock jenkins-docker

  jenkins-docker içerisinde docker client'ın kurulu olması gerekli. artık jennkins joblarımızda, dockerd'ye komut yollayabiliriz.

  "/var/run/docker.sock" bir unix socket dosyasıdır. dockerd sürekli buradan dinleme yapar ve buradan gelen komutları kabul eder.

  Bu madde tavsiye edilmiyor, çünkü sıkıntı yaratıyor. kaynak: (source-id: 48) "The solution" başlığı.

- docker içerisinde docker'ı kurarız.

  buna genelde __DIND (or Docker in Docker)__ deniliyor. fakat nadir de olsa bazı kaynaklarda, DIND, bu başlıktaki diğer maddelerdeki çözümler içinde kullanılabiliyor.

  bunu yapan hazır bir docker image'si mevcut: (source-id: 49)

  Bu madde tavsiye edilmiyor, çünkü sıkıntı yaratıyor. kaynak: (source-id: 48)

- docker client ile container dışında olan bir dockerd'ye istek atarız. bu madde en çok tavsiye edilen çözümdür. kaynak: (source-id: 48) Tüm makaledeki en son satır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# GitLab

Continous integration, bug, repository hizmetlerinin sunucusu yönetimi sunan bir web yazılımıdır.

- ## ana menüler

- İlk açıldığında "Project" ve "Groups" sekmeleri karşımıza çıkar. "groups" projelerin gruplandırılmış halini içerir. projects ise direk projeleri (gruplamadan) gösterir.

  her repository (yani proje), repository-url'sinin önüne grup ve sub-group adını otomatik prefix olarak gelmektedir.

- "Activity" sekmesinde tüm projelerdkei her komiti bir arada listeleyebiliyoruz.

- "Milestones" sekmesindeki listenin her elemanı bir task grubunu kapsaması için yaratılmıştır. örnek: OnlineÖdemeler ismini verdiğimiz milestonumuz olsun. bunun altına yine GitLab'den açacağımız taskları bağlarız. Bu şekilde taksların yüzde kaçının bittiğini, her task ile bağlantılı olan kaç komit atıldığını vs istatistiksel olarak takip edebiliriz. Milestone, jira'daki Spring kavramına çok benzemektedir.

- ## alt menüler

Her projenin altında o projeye ait wiki, issues, CI/CD(Continous development), Settings, Merge Request, repository sekmeleri bulunur. bu başlıkta sadece "issues" in altındakileri inceleyeceğiz:

issues sekmesinin altında;

- list: tüm issue'lar listelenir

- board: issue'ler grup halinde listelenir: kapanmışlar, backlog'dakiler vs..

- milestones: (yukarıda anlatılıyor)

- labels: taskalara/issue'lara atanmak için yaratılırlar. issue'lara keyword atamak için kullanılır. eksta bir özelliği yok.

# roller

sadece bunlar var: Guest , Reporter, Developer, Master, Owner

her rol için detaylı bilgi burada yazıyor: https://docs.gitlab.com/ee/user/permissions.html

temel olarak;

- Guest: yeni issue açabiliyor + kod hariç herşeyi sadece takip edebiliyor (wiki, diğer issue'lar, artifacts, job'lar) 

- Reporter: guest + issue assign + label management + merge request assign gibi daha yönetimsel işleri yapabiliyor + ek olarak proje kodunu da görebiliyor.

- Developer: reporter + milestone yönetimi + kod gönderme isteği + wiki yazma + CI/DI için sadece stop-start gibi yetkilere sahip

- Master: Developer + user management + CI/DI yazma

- Owner: Master + remove everything

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# bootstrap kelime anlamı

sözlük anlamı: çizme (ayakabı) atkısı (üst kısmıdır)

bilişim dünyasında farklı anlamda kullanılmaktadır. direk örnekler üzerinden gidersek; 

- web sitemizde bootstrapper index.html dosyamızdır.

- bootstrap loader bir sistemi başlatan yazılım yada yazılımın ilk kodlarıdır. bootstrap loader; web sitemizi başlatacak olan framework/sunucu yazılımızıdır.

Bootstrapping; terimi ise yukarıdaki 2 maddeden bağımsızdır. Bootstrapping; bir sistemi kendi sisteminizle geliştirmenizdir. örneğin; C programlama dili'nin yeni versiyonları yine C dili ile geliştirilmektedir. bu geliştirme sürecine bootstraping denir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# ITIL (or Information Technology Infrastructure Library)

İngiltere Ticaret Bakanlığı tarafından geliştirilmiştir. ITIL kitaplar şeklinde iş dünyası için bilişim altyapısı standartları açıklamaktadır. BU stanardtalar dünyanın birçok firması tarafından özellikle uyulmakta ve takip edilmektedir. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Dependency hell

bu terim genelde Dependency'lerden kaynaklı sorunlar olduğunda kullanılır. bazen platfrom spesifik terimler kullanılır. örnek: jar hell, dll hell gibi.

Dependency hell birkaç çeşit formda karşımıza çıkabilir:

- Long chains of dependencies. muhtemel çözüm: microservisler. bir projeyi farklı executable paketlerle kullanılabilir halde ayırmak. belki portable uygulamacıklar sunmak.

- too many dependencies. muhtemel çözüm: microservisler. bir projeyi farklı executable paketlerle kullanılabilir halde ayırmak. belki portable uygulamacıklar sunmak.

- yürüteceğimiz bir programın bir bağımlılığı diğer yürüteceğimiz bir programın bağımlılığı ile sürüm çakışması yaşamaktadır. örnek: x proramı Dependency-A'yı max 3 sürümü kabul ederken, Y programı min 4 kabul etmektedir. muhtemel çözüm: container (örnek docker)

- cyclic dependencies: birbirine depend eden projeler. muhtemel çözüm: için projeleri birleştirmek yada ortak kodları başka üçünkü bir projeye taşımaktır.

# tree vs flat Dependency store management

nix ve yarn paket yöneticileri paketleri/bağımlılıkları bir dizinde tutar. buna store biçimine flat adı verilir. bu dizinde X paketi olsun. X paketinin bağımlılıkalrı X dizini içinde dğeildir. X ile aynı dizindedir. bu paket yönetim sistemi daha az yer kaplar. çünkü ortak bağımlılıklar ortak dizine referans eder.

tree'de ise her paket/Dependency kendi Dependency'lerini kendi içinde barındırır. ağaç şeklindedir. bu yöntem flat'e göre daha çok yer kaplar. fakat paketler taşınabilirdir. bir paketi başka sisteme kopyalayıp kullanabilirsiniz. çünkü herşey kendi içindedir. npm tree yöntemini kullanır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# declaration (or beyan or bildiri) vs definition (or tanımlama)

fonksiyon/variable imlazalarının kodlandığı yerde declaration yapılmış olur. oysa bunlara değer atama, metodu implemente etme (body kısmını yazma) gibi kodlarının yapıldığı yerde definition yapılmış olur.

örnek:

> int PI; //declaration

> PI = 3; //definition

```java
int function topla(int a, int b); //declaration

topla = function(int a, int b){

      return a+b;
}
```

declaration ve definition aynı kod bloğunda da olabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# truncate output

truncate türkçe kelime anlamı: kesmek, ayırmak.

bir komut satırı çıktısının sadece bir kısmını göstermek anlamında kullanılır. örneğin pi sayısını (3.123456789...) truncate edip göstereceksek 3.124 gibi yuvarlayamayız. onun yerine sadece bir kısmını göstermemiz gerekir: 3.123. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# accessibility (or erişilebilirlik) destekleyen yazılımlar

kullanıcıların birçok çeşit engeli olabilir:

- renk körlüğü (or Color blindness or color vision deficiency or gr:Αχρωματοψία)
  
  çeşitleri:
  - renkleri farklı görme: mavi yerine pembe gibi
  - sadece siyah beyaz görme
  - renkleri farklı yada doğru gören insanların bazıları renklerin farklı tonlarını algılayamamaktadırlar
  
  birçok insan renk körü olduğunu bile bilmiyor. bu sebeple renklere bağlı seçim yaptırırken dikkat edilmelidir. 

- hiç görememe

- duyamayanlar

- fareyi kullanamama

tüm engelliler klavyeyi kullanabiliyor.

dikkat edilmesi gereken bazı noktalar:

- html'de medya dosyalarına (video, resim, ses gibi) alt="media aciklamasi" atanmalıdır. göremeyenlere resimler gösterilmediğinde bu metin ekrana basılıyor, veya göremeyenler için bu metin okunuyor. bu metinlerde multi-language desteği olmalıdır.

- yazılımdaki tüm metinlerde kısaltmalar az ve hatta mümkünse hiç olmamalı. örnek 11 Feb 2017. Feb yerine February yazmak lazım. metin okuma programları kısaltmaları tanımlayamayabilir.

- standartlara uymak gerekli. örneğin html'de h1, h2, p gibi tagler çok önemli. sayfanın yapısı tarayıcı tarafından algılanabilmeli.

- metinler ve resimler net olmalı. ve ufak boyutta olmamalı. hiçbir obje ufak olmamalı. örneğin chechbox bile ufak olmamalı. karmaşık fontlar kullanılmamalı.

- linklerde title'ı mutlaka kullanmalıyız. örnek:

```html
<p>İşyerlerine başvuru için formu doldurmanız gerekli. <a href="form.html" title="İşyerine başvuru için tıklayın.">İşyerine başvuru için tıklayın.</a>  </p>
```

- form'da her eleman için "label" olmalı. form alanı doldururken buradaki bilgi ilişkili olduğu için engelli kişi için tanımlayıcı oluyor. örnek:

```html
<form>
    <label for="yourName">Your Name</label>
    <input name="yourName" id="yourName">
    <!-- etc. -->
```

- form elemanlarını mümkünse gruplamalıyız:

```html
<form action="somescript.php" >
    <fieldset>
        <legend>Name</legend>
        <p>First name <input name="firstName"></p>
        <p>Last name <input name="lastName"></p>
    </fieldset>
    <fieldset>
        <legend>Address</legend>
        <p>Address <textarea name="address"></textarea></p>
        <p>Postal code <input name="postcode"></p>
    </fieldset>
    <!-- etc. -->
```

- penceredeki elemanlara "Access Keys" atamaları yapılmalıdır.

- tema ve renkler olabildiğince flat olmalı. bu şekilde resimlerin tonlarını algılamayanlar için sorunlar ortadan kalkacaktır.

- sadece ses efekti ile uyarı yapıldığında, paralel olarak bildirim de yapılmalıdır.

- tarayıcılarda accesibility açıkken farklı css'ler kullanılabilir. bu şekilde çözüm üretilemeyen durumlarda, gerekirse bambaşka bir sayfa gösterilebilir. 

- bazen içeriklere hızlı erişim için ayrı ayrı linkler konulmalıdır. örnek:

```html
<header>
    <h1>The Heading</h1>
    <a href="#content">Skip to content</a>
</header> 

<nav>
    <!--loads of navigation stuff -->
</nav>

<section id="content">
    <!--lovely content -->
</section>
```

bunlar'ı css ile accesibility kapalı ise gösrmemeliyiz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# makefile

linuxta genelde program derlemek için önce "configure" komutu çağrılır. configure komutu o proje dizinindeki bir scirpt'in ismidir. root klasöründe olan bu script dosyasıdır. zaten bu sebeple ./configure diye çağrılır. bu dosyanın görevi projenin derlenebilmesi için ön-hazırlık ve kontrollerin yapılmasıdır. örnek: işletim sisteminde projeyi derlemek için gerekli program var mı tespiti yapılmaktadır. örnek: javac (java compiler) var mı gibi... Aslında burada "makefile" içerisindeki tüm komutların çalışabilmesi için gerkeli tool'ların yüklü olup olmadığı kontrol edilir.

daha sonra "make" komutu çalıştırılır. make komutu bir program. örneğin "gnu make" açık kaynaklı bir program. işletim sisteminde kurulu olması gerekli. birçok make programı mevcut. make proramı varsayılan olarak projenin root'undaki "makefile" dosyasını okur ve bu dosya içindeki tanımlara göre projeyi derler. makefile dosyası programlama dilinden bağımsızdır.

example "makefile" file:

```makefile
variable1 = value1

# format of makefile:

# target: prerequisite1(dependency1) prerequisite2(dependency2)
#   shell_command1(recipe1)
#   shell_command2(recipe2)

fileName1: # fileName1 is a file on project directory.
    echo "fileName1 called"
    echo $(variable1)
    echo ${variable1}
    echo $variable1 # Bad practice, but works.
    echo "end of fileName1"

fileName2: fileName1
    echo "fileName2 called"
    echo "end of fileName1"
```

command to run only fileName2:

```sh
make fileName2

# this command will call target fileName1 before fileName2, if only:
# the modification/create-date of "fileName1" file is later than
# the modification/create-date of "fileName2" file.

# "make" process does not store any meta-data about timestamps,
# it directly reads the dates from filesystem. 
```

command to run the default target:

```sh
make

# default target is the first target which does not include a dot (.) character. This is because normally all source-code files includes extensions (like ".java", ".c").
```

# install
bueğer target dosya ismine tekabul etmiyorsa, o zaman sürekli çağrılır. Bu sebeple "install" tagret'ı olursa (ve install dosyamız yok ise) bu artık bi script gibi çalıştırılacaktır. install genelde OS'a kurulum yapılması amaçlı yaratılan bir target'tır.

# shell script vs makefile
ikisi ile de proje yönetimi yapabiliriz. Makefile'ın en önemli artısı: dependency yönetmi yapması. yani bir fonksiyon, dependency'd ebelirtilen fonksiyonları (sadece gerektiğinde) otomatik çağrıyor. bu kolaylık shell'de default olarak mevcut diil. zaten shell'in amacı bu olmadığından böyle bir özelliğin varlığı beklenemez.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# handler vs listener

aralarında çok ince bir fark var. listener kaynağı dinler ve kaynak aksiyon aldığında handler'ı tetikler. handler ise event tetiklenince ne yapılacağına karar verir. şöyle düşünebiliriz:

```java
button.setOnClickListener( OnClickListener { 

    onClick() { 

        ...

    }

});
```

yukarıdaki kodda; OnClickListener bir listener, onclick metodu ise bir handlerdır. farklı bir örnek:

```java
button.addEventListener('click', function() {

   ...

});
```

yukarıdaki addEventListener metodu aslında bizim için kendi içinde listener oluşturuyor. bizden sadece handlerı parametre istiyor (anonym metodumuz - 2inci parametre).

Aslında; listener'da birşey tarafından tetikleniyor. bi bakıma listener'da bir handler olmuş oluyor. bu sebeple olaya nereden baktığımız önem kazanıyor. örneğin; bir java programında, proragmcı için listener; jvm'in işletim sistemi ile arasındaki kod/proram parçacığıdır. handler ise; programcının parametre yolladığı sınıftır. şimdi ise jvm açısından olaya bakalım: jvm için listener; işletim sisteminin event mekanizmasıdır, oysa handler jvm'in işletim sistemine event gerçekleştiğinde çalıştırması için gönderdiği kod/program parçacığıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# regular expression (or regex or reg-ex or regexp or rational expression)

arama yapabilmek için karakterlerden oluşan özel bir ifade dilidir.

birçok implementasyonu vardır. örnek: 
- IEEE POSIX'ta belirtilen: BRE (or Basic Regular Expressions)
- IEEE POSIX'ta belirtilen: ERE (or Extended Regular Expressions)
- IEEE POSIX'ta belirtilen: SRE (or Simple Regular Expressions)
- Perl Compatible Regular Expressions (or PCRE) kaynak: (source-id: 52) 1inci paragraf.

Unicode veritabanında her karakterin meta-bilgileri mevcut. Eğer kullandığımız regex kütüphanesi bu bilgileri saklıyor ise; o zaman aşağıdaki gibi kontroller ile de regex yazabiliriz:

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

kaynak: (source-id: 53) "Unicode support" başlığı.

# regex kullanımı

(aşağıdaki syntax bilgileri hangi notasyon standardına göre yazıldı bilmiyorum. aşağıdaki bilgiler farklı kaynaklardan toplama olduğundan farklı satndartlara ait bile olabilirler.)

| regex          | what it returns                                                                                                                                                                                                                                            |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ^merhaba       | starts with "merhaba"                                                                                                                                                                                                                                      |
| merhaba yusuf$ | ends with "merhaba yusuf"                                                                                                                                                                                                                                  |
| merhaba        | contains "merhaba"                                                                                                                                                                                                                                         |
| ab#            | a, ac, abc, abb, abbc döndürebilir. a kesin var. b'den istenildiği kadar olabilir. # karakteri sadece bir önceki karakter için bir kuralı kapsar. eğer bir önceki karakter birden fazla karakter olacak ise; a(bc)# olarak parantez içinde gruplandırılır. |
| a(bc)#         | a, abc, abcbc, abce döndürebilir.                                                                                                                                                                                                                          |
| ab+            | # karakteri ile aynıdır. tek farkı en az 1 adet b olmalıdır. ab, abb, abc                                                                                                                                                                                  |
| ab?            | # karakteri ile aynıdır. tek farkı en fazla 1 adet b olmalıdır. a, ab, ac                                                                                                                                                                                  |
| a?b+$          | ab, b, bb, abb, abbb dolar ile bittiğini belirttiğimizden en sağa c gibi farklı karakterler gelemez                                                                                                                                                        |
| ab{2}          | {} # gibi sadece bir önceki karakter için geçerli bir kural belirtir. {2} 2 tane b olması gerektiğini belirtiyor. abb, abbc, abbc                                                                                                                          |
| ab{2,}         | en az 2 adet b olmalıdır. abbb, abb, abbc                                                                                                                                                                                                                  |
| ab{3,5}        | en az 3 en fazla 5 adet b olabilir. abbbc, abbb                                                                                                                                                                                                            |
| hi∣hello       | hi veya hello içerenler döner.                                                                                                                                                                                                                             |
| (b∣cd)ef       | bef yada cdef içeren textler döner                                                                                                                                                                                                                         |
| [ab]           | [] sadece bir karakteri temsil ediyor. (a∣b) ile aynı şeydir.                                                                                                                                                                                              |
| [a-d]          | [abcd] ve (a∣b∣c∣d) ile aynı şey.                                                                                                                                                                                                                          |
| [a-zA-Z]       | regex aksi belirtilmedikçe case sensitive'dir. bu sebeple büyük küçük tüm alfabeyi kapsatır.                                                                                                                                                               |
| [0-9]          | sadece rakam olduğunu belirtir.                                                                                                                                                                                                                            |
| [a-zA-E0-8]    | ufak karakterler tüm alfabe, büyük karakterlerde a'dan e'ye kadar olan karakterler, sayılarda ise 0'dan 8'e kadra olan karakterler                                                                                                                         |
| a.b            | . bir karakteri temsil ediyor. acb, abb                                                                                                                                                                                                                    |
| ..             | en az 2 karakter olan değerler döner                                                                                                                                                                                                                       |

özel karakterler kullanılacak ise öncesinde backslash "\" kullanılmalıdır.

# javascript'te regex

```js
var myRegexObject = /hello world/i; // literal notation
// or
var myRegexObject = new RegExp('hello world', 'i'); // first param is 'pattern' and the second param is 'modifiers'.
// or
var myRegexObject = new RegExp(/hello world/, 'i');

var sonuc = "hello world coder".search(myRegexObject);
```

## Modifiers

- /i

Perform case-insensitive matching.

- /g

Perform a global match (find all matches rather than stopping after the first match)

- /m

Perform multiline matching.

## functions of RegExp object

- compile()

  Deprecated. Compiles a regular expression.

- exec(str)

  Tests for a match in a string. Returns the first match.

  ```js
  regex.exec("hello"); // returns the found string.
  ```

- test(str)

  Tests for a match in a string. Returns true or false.

  ```js
  regex.test("hello"); // returns true or false.
  ```

  test and exec functions are always moving the pointer. Therefor "regex.lastIndex" will increase everytime we call test or exec.

- toString()

  Returns the string value of the regular expression.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# synchronization (or senkronizasyon or eşleme)

eşgüdümleme kelimesi eş anlamlı değildir. eşgüdümleme koordine etme, işbirliği içinde hareket ettirme anlamına gelmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Headless software

örnek: "headless java", "headless Linux"

bu terim o yazılımın GUI'siz çalıştığını belirtir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# wordpress vs joomla vs brutal

açık kaynaklı php tabanlı content management sistemleridir. başlıktaki sırası ile basitten daha gelişmiş'e doğru gider. daha basit kullanımı olan wordpress neredeyse hiçbir teknik bilgi gerektirmeden kullanılabiliyor. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# dosya sistemi (or file system)

dosyaların bellekte tutulma formatıdır. örnek formatlar: 

- ntfs (or NT File system)

- FAT12 (or File Allocation Table, 12-bit cluster indices)

- fat16 (or File Allocation Table, 16-bit cluster indices)

- fat32 (or File Allocation Table, 32-bit cluster indices)

  FAT16'ya göre en önemli yenilik dosya maximum bellek alan desteğinin genişletilmiş olmasıdır.

- ReiserFS

- ext# (ext4, ext3...)

- XFS

- exFAT (or Extensible File Allocation Table)

  Bazı yerlerde FAT64 olarak isimlendirilir fakat resmi ismi bu diildir.

  FAT32'nin forkudur. FAT32 çok basit bir dosya sistemidir. Çok az özellik içerir. Onun forku yapıldı ve sadece minimum dosya boyutu desteği arttırıldı. Bu windows 7 ve sonrasında microsoft tarafından default olarak support ediliyor. Linux ve mac içinde paketler çıkarılmıştır. Cross-OS basit bir dosya-sistemi çözümü olarak sunuldu.

  exFAT external drive'lar için önerilir.

- Resilient File System (or ReFS)

  projenin kod adı: Protogon

  Microsoft'un ntfs'e alternatif yeni dosya sistemidir. Windows 8.1 ve sonrasında default support edilmektedir.

# iso9660

CD-ROM dosya sistemi

# journaling file system (günlükleme dosya sistemi or JFS)

hiçbir dosyaya direk olarak yazmaz. önce geçici bir dosyaya (journal) yazar, herşey kesinleştiğinde/bittiğinde dosya referansını yeni dosya adresi ile günceller. bu tarz dosya sistemlerine JFS tabanlı dosya sistemleri denir.

# Journaled File System

IBM'in geliştirdiği JSF tabanlı dosya sistemi. özel isimdir. teknolojisi ile aynı ismi barındırıyor.

# disk birleştrime (or disk difragment)

bir dosyanın fiziksel olarak yazıldığı noktalar bütünleşik olmayabiliyor. bu sebeple dosyalar arası boşluklar meydana geliyor ve tek dosya birçok parçalanma yaşayabiliyor. bu parçalanmalar dosya okuma yazma hızlarını da düşürüyor.  sebeple disk defragment yapan yazılımlar geliştirilmiştir.

ext4 gibi gelişmiş bazı dosya sistemlerinde okuma yazma yaparken akıllı algoritmalar sayesinde dosya bölünmeleri en aza indirgeniyor ve yeni dosyalarla boşluklar kapatılıyor. bu sebeple bazı dosya sistemlerinde disk birleştirme neredeyse hiç gerekmiyor.

# dosyaların silinmemesi

dosyalar dosya sisteminden silindiğinde, sadece dosya adresi silinir. bu sebeple hala dosyanın geri getirilme şansı vardır. bu sebeple bazı güvenlik yazılımları, silinene dosyaların üzerinden geçmek için, boş alanın tümünün üstüne yazar. boş alanı dolu olan bir bellekten dosyayı yazılımsal tekniklerle geri getirilme şansı yoktur. artık donanımsal/fiziksel çözümlerle eski dosyalar geri getirilebilir.

# inode

unix tarzı dosya sistemlerinde her dosya ve klasörün metadataları bir tabloda (inode table) tutulur. her inode bu tablonun her satırıdır. her inode (her satır) bir dosya yada klasörün meta data'larını tutar.

# hdd vs solid-state drive (or SSD or solid-state disk)

hdd mekanik ssd ise tamemen elektronik yapıdadır.

# hhd'nin fiziksel yapısı

- plak (or platter): hdd üstüste takılmış yuvarlak parçalardan meydana gelir. genelde bir hdd kendi içinde birkaç plak bulundurur. 

- track: her plak içinde dairesel kayıt kısmına denir. 

- sektör (or sector): her track kendi içinde ufak kısımlara bölünmüştür. en ufak birim sektördür ve genelde 512 byte'tır. 

- Cluster (or Block): bir hdd'de sektör sayısı çok fazla olduğundan dosya sistemleri kendi içlerinde ardışık olan sektörleri gruplandırırlar. böylece sanal olarak en ufak kayıt birimi cluster olur. windows temelli sistemler cluster terimini kullanırken, posix'lerde block terimi kullanılır. bu birime "allocation unit"'te denir. cluster genelde 4 sektörü kapsar.

# lock files

bir program işlem yaptığı dosyayı kilitleyebilir. bu şekilde başkaları bu dosyay erişmeye çalıştığında işletim sistemi izin vermeyecektir. dosya sistemi ve işletim sisteminin sunduğu bir çok lock çeşidi vardır. her işletim sistemi farklı çeşit lock seviyeleri sunuyor. örnek: bazı filesystem'ler dosyayı kilitleyip, diğer yazılımlara read-only açabiliyor. bazı dosya sistemleri dosyanın bir kısmını lock'lamaya izin veriyor.

# "size on disk" vs "size"

sadece "size" denildiğinde; dosyanın byte olarak ne kadar veri içerdiği kastedilir. oysa aynı dosya için "size on disk" çok daha fazla yada az bir değere tekabül ediyor olabilir. 

harddisklerde en küçük kaydedilebilir birim "allocation unit"'tir. dosya sistemimizin "allocation unit" boyutu 4096kb olduğunu varsayalım. bizim dosyamız ise 512kb olsun. bu durumda bizim dosyamız 4096kb "size on disk" değerinde olacaktır. 

dosya sisteminin şifreleme yada sıkıştırma gibi özellikleri oluyor. bu özellikler sonucunda dosyanın "size on disk" boyutu, "size"'a göre artmış yada azalmış olabilir.

# sparse file

dosya sistemleri bu özelliği native destekliyor olabilir. bazı dosyalar örneğin 1 gb yer almaktadır. fakat bir yazılım henüz dosyanın tümüne yazmamıştır. dolayısı ile yazılmayan kısımlar kullanılmaz. bu kullanılmayan kısımlar sayesinde "size on disk" değeri "size" değerinden düşük olabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# variable shadowing (or değer gölgeleme)

programlama dünyasında kullanılan bir terimdir. bir değer scope'ta ve üst scope'ta aynı isimde olabilir. örnek:

```java
class MyClass {

    int myVal;
    void method(int myVal){

         //burada 2 farklı myVal mevcut
    }
}
```

her zaman üst scope'taki değere 'shaddowed' adı verilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Short polling
polling kelime anlamı: seçme, oy verme 

sürekli olarak client for döngüsü içerisinde (belli zaman aralıklarında) işlemin sonlandığına dair bilgi almak için sorgu yapması tekniğidir.

pros: sürekli soket ve thread açık kalmaz.

cons: complex

# long polling
bu teknikte bağlantı sürekli sunucu ile açık kalır. sunucu işlem tamamlandığında client tarafa bilgi verir.

cons: soket sürekli açık kalır. bu sebeple soket resource'u ve sunucu tarafta bunu yöneten thread sürekli açık kalır.

pro: simple

# Comet programming
comet kelime anlamı: kuyruklu yıldız

web sayfası geliştiriminde kullanılan bir tekniktir. web sayfaları normalde son kullanıcı event'i olmadan sunucuya istek atamaz ve borsa, haber akışı gibi sayaflar güncellenemez. bunu çözmek için web siteleri iki farklı teknik izler:

- __comet programming__

  comet terimi buradaki makaleden gelmektedir: (source-id: 54). comet programming websocket gibi teknolojilerin kullanılması ile yapılan programlama tekniğidir.

- short polling (başka başlıklta anlatılıyor)

comet programlama ile  long polling çok benziyor fakat %100 aynı kapıya çıkmamaktadır. comet porgramming, long polling'i kapsayan daha büyük bir kümedir.

# server-push
sunucunun client'a istediği zaman data yollayabildiği tüm teknikleri kapsar. websoket yapısı buna uymaktadır. kaynak: (source-id: 55)

# ajax polling types

- ajax polling

```js
setInterval(function(){
    $('#myCurrentMoney').load('getCurrentMoney.php');
}, 30000);
```

- ajax long polling

server timeout süresini uzun tutar timeout'un en uzun süresine kadar bekler. sunucu cevap vermek istediği zamana bilgiyi döndürür, client tekrar bir request yollar. client2ın request'inde data gerekmez, client sadece tekrar cevap beklediğini bildirmek için request atar.

```js
refresh = function() {
    $('#myCurrentMoney').load('getCurrentMoney.php',function(){
        refresh();
    });
}

$(function(){
    refresh();
});
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# excel

# farklı dildeki ofis setlerinde formüller
excel dosyalarındaki formülller ofis dil yüklenmiş ofis paketlerinde sorunsuz açılabilmektedirler. çünkü formüller text olarak değil, referansları ile saklanmaktadırlar. dolayısı ile sadece ekrana basarken farklı dillerde gösterilmektedirler. fakat ekstra yüklenen eklentinin multi-language desteği yok ise, eklentinin sunduğu formüller doğal olarak multi-language olmayacaktır.

# $ işareti
excel'de $ işareti sutun yada satır adresinin önüne gelebilmektedir. örneğin; $A$2 yada $A2 yada A$2 olabilir. $ işaretinin olduğu bölüm (sutun yada satır), bulunduğu hücredeki formül kopyala yapıştır yapıldığında değişmemektedir. $ olmayan kısımlar her zaman değişebilir. örneğin bir satır aşağıya kopyalanan hücrenin içinde $ olmayan satır değerleri otomatik olarak 1 artar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# csv (or Comma seperated value)

csv dsya formatının avantajı şu: txt formatı gibi her editorle açılabiliyor. aynı zaman excel ve alternatifi uygulamalar csv açarken her virgül arasını bir sutuna koyup açtığı için aynı dosya excel ile de sutunlara bölünmüş şekilde açılabiliyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# getter-setter

kullanım sebepleri:

private değişkenlere erişim/read/write sırasında şunlar yapılabilmesini sağlar:

- yetki kontrolü yapılabilir

- set edilecek veri ise; verinin uygunluğu/validation'ı (null mı? formatı uygun mu? gibi) kontrol edilebilir

- getter setter işlemlerinde loglama yapabiliriz

- debug ederken setter veya getter'a log atılması işimizi hızlandırabilir ve debug edebilmemizi sağlar.

- immutability sağlayabiliriz (aynı objenin klonunu döndürürüz, setter'da ise işlem yaptırmayız.)

- Mocking, Serialization gibi kütüphanelerin hangi nesneleri alması gerektiğini belirtebiliriz. (bunu sadece annotation kullanarakta yapabiliriz)

- bizim sınıfımızdan extend etmiş sınıfların getter/setter'larda farklı davranmaları için esneklik sağlamış oluruz.

- getter'a tüm paketlerden erişimi açabilir, setter'a ise sadece aynı pakettekilerin erişebilmesini sağlayabiliriz (public getName, protected setName gibi)

- getter'ı herkese açıp, setter'ı tamamiyle private yapabiliriz (veya hiç setter yazmayabiliriz.)

- jpa'nın yaptığı gbi lazy-loading yapabiliriz. (bunu annotation'larla da yapabiliriz.)

- Mocking, Serialization, test için kolaylık sağlar. 

- event propagation. bir field set edildiğinde (değiştiğinde), bir event yada class'ta bir başka değişikliği tetiklemek isteyebiliriz.

Yukarıdaki bazı feature'leri annotation'larla da sağlayabiliriz. fakat bu durumda annotation'lara bağımlı kalırız.

Yukarıdaki özelliklerin hepsi "encapsulation" yapmış olmamızı sağlamaktadır. Bir class ilk yaratıldığında bu özelliklere encapsulation'a ihtiyacımız olmayabilir fakat bu durum ilerde de ihtiyacımız olmayacağı anlamına gelmez. Bu sebeple dışarıdan field'lara erişen diğer sınıfılara, ilk zamanlardan itibaren getter-setter'lı vermemiz daha doğru olacaktır. Aksi durumda encapsulation uygulamak istediğimizde, field'ları kullanan bütün diğer kod bloklarında değişiklik yapmamız gerekecek.

# naming convention
get/set prefixleri gerçek getter-setter amaçlı kullanılmayan metodlarda kullanılmamalıdır. Bu sebeple get yerine örneğin; fetch, find gibi prefix'ler verilmelidir.

# Accessor vs Mutator
programlama dünyasında; Accessors getter metodlarına verilen isim, mutators ise setter metodlarına verilen isimdir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Convention over configuration (or coding by convention or CoC)

örnek; jpa'da aksini belirtmedikce @entity ve @id'ye annotation'larina sahip tum pojo class'lar, attribute name'lerin ve class name'lerin birebir tablolarla ve column'larla eslestigi kabulu uzerine dayanir ki buna convention denir. yani özel olarak ek könfigürasyon belirtmediğimizce yapılan code'lamalar daha temiz ve daha sadece görünmektedir. fakat bunun dezavantajı şudur: codu okuyan başka birisinin kullandığımız framework/library'lere hakim olması gerekir. çünkü configler hep default'tur.

# Diamond Problem

```
  A

B  C

  D
```

Yukarıdaki elmas görünümlü şekil extend ağaçı olsun. A super class. B ve C, A'dan türemiş. D ise hem B hem C'den türemiş.

B ve C, A'nın X metodunu override etmiş olsun. D, A'nın X metodunu çalıştırmak isterse ne olacak? İŞte bu problme için birçok dil farklı  çözümler getirmiş durumdadır. 

# composition over inheritance

EFT ve Havale yapmak için sunucuya gönderdiğimiz iki ayrı nesnemiz olsun. bu nesnelerde tutar, karşı atarfın banka nosu, gibi ortak parametreleri var. Genelde yazılımcılar MoneyTransferCommonData objesi oluşturur ve içine amount, receiverNo gibi ortak değerleri atar. Daha sonra EFT ve Havale nesnelerini bundan türetir. Oysa "composition over inheritance" practice'si, bunun yerine  MoneyTransferCommonData objesini EFT ve Havale objelerinin içinde propertie olarak tutmamızı önerir. Bunun avantajları şudur:

- bazı diller birçok extend'e izin vermez. extend hakkımızı kullanmamış oluruz.

- ilgili sınıfımızı ilerde bir çok interface/abstract/sınıftan türetebiliriz. bu türetmeler sonucu (özellikle aynı isimdeki metodlar) debug işlemlerimiz çok zorlaşacaktır. oysa; myProperty.myMethod() çok daha okunaklı. sadece myMethod() bize mi ait super classtan mı geliyor diye sürekli bakmak gerekmektedir.

yani; "is a" ilişkisi yerine "has a" ilişkisi tercih edilmelidir.

# Halting problem (or Sonlanma problemi)

bir programı başlatırken birçok parametre ile başlatabiliriz. her parametreye karşılık bu programın sonsuza dek döngüye girip girmeyeceğini yada sonlanacağının garantisini veremeyiz. daha doğrusu bunu programatik olarak kanıtlayacak/ispatlayacak programı yazamayız.

örneğin IDE ile kodumuzu formatlarken sonsuz döngüye girme ihtimalimiz var. Böyle bir durumda IDE nasıl davaranacak? O kodun formatlanırken IDE'nin sonsuz döngüye girip girmeyeceğini bilemiyoruz. Bunu bilemediğimizden IDE'ler belli bir süre sonra format işlemini durdurmaktadır. Çünkü henüz bir programın sonsuz döngüye girip girmeyeceğini belirleyen bir program yazılamamıştır.

Alan turing böyle bir programın yazılamayacağını kanıtlamıştır. Kanıt "proof by contradiction (çelişki ile kanıt)" yöntemini kullanmaktadır.

A programımıza i inputunu verseydik; A programımız sonlanırmıydı?

isHalting( A, i );  
  - returns;
    - true(durur)
    - false(durmaz) 

isHalting'in koduna eklemeler yapmak amaçlı metodu wrap edelim:
- true(durur) dönerse; wrapper metodumuz sürekli çalışmaya devam etsin (kendini sonsuz döngüye soksun).
- false(durmaz) dönerse; wrapper metodumuz true(durur) dönsün ve kapansın.

Bu wrapper metodumuza isHalting+ adını verelim.

Şimdi şu işlemi yapalım:

isHalting+( isHalting+, (A,i) ); 

Bu metod bize ne dönecek?
- isHalting+ eğer true(durur) dönerse; isHalting(isHalting+, (A,i) ) false dönmüş demektir. Oysa isHalting+ hiç false dönemiyordu. False durumunda kendini (isteyerek - bu kodu biz yukarıda kendimiz ekledik) sonsuz döngüye sokuyordu. Böyle bir durum söz konusu olamaz (çelişki durumu). Yani makinemiz bize yanlış bilgi vermiş oluyor.

- isHalting+ false(durmaz) dönmek yerine kendini songuz döngüye sokuyordu (bizim yazdığımız kod). eğer kendini sonsuz döngüye sokarsa; isHalting(isHalting+, (A,i) ) true dönmüş demektir. Burası olağan gibi geliyor. Fakat isHalting(isHalting+, (A,i) ) true dönmüş olması için isHalting+'ın çalıştırıldığında sonlanmış olması; bir return değerini döndürmüş olması gerekli. isHalting+ sadece isHalting false durumunda true dönüş yapabiliyordu. diğer durumda sonsuz döngüye giriyordu. isHalting false ise; isHalting(isHalting+, (A,i) ) true dönmüş olamaz. Burada da bir çelişki söz konusudur.
  

# Project Management Triangle (or Triple Constraint or Iron Triangle or Project Triangle)

scope(kapsam), cost(maliyet), schedule(zaman) sabitlerinin köşeleri olduğu üçgendir. örneğin; maliyeti düşürürseniz diğerlerini arttırırsınız.

# Hofstadter yasası

Bir olay her zaman planlanan zamandan daha geç biter. Hofstadter yasasını hesaba katsan bile.

# Conway Yasası (or Conway's Law)
Melvin Edward Conway tarafından atılmış bir gözlemdir:

"Sistemleri tasarlayan organizasyonlar ... kendi iletişim yapılarının birer kopyasını üretmekle sınırlıdır" 

Bu söz ile; yazılım geliştirme sürecinde, birimler arası iletişim sorunlarının yazılımın çıktısına da yansıdığını savunur.

# Hollywood Principle

Hollywood'daki yapımcılar/yönetmenler önemli insanlardır (VIP - Very important person). onları aradığınızda ve bir teklif sunduğunuzda size bölye dönerler: "Don't call us, we'll call you".

Bu prensibe dayanan birçok yazılım Frameworkü mevcut. örnek: spring'in DI'ı bu prensibe dayalı çalışır: Bir java bena'i bir dependency'yi autowired ettiğinde, dependency'yi aramaz. spring o sınıfa dependency'yi getirir. "Don't call around for your dependencies, we'll give them to you when we need you."

# Brooks's law

bir projedeki kişi sayısı arttığında, projenin kısalma süresi gelen kişi sayısı ile doğru orantılı değildir. bu kişiler birbirleri ile iletişimde kaybedilen zaman artmaktadır. aynı zamanda birbirlerine olan aktarım süreleri de artmaktadır vs...

# law of demeter (or LoD or principle of least knowledge)

coupling'i azaltmak için temel bir prensiptir. her sınıf sadece kendi içindeki variable'ları çağırmalıdır.

# don't repeat yourself (or DRY)

tekrar yazılan kodları ortak yere alma prensibidir.

# Unix Felsefesi (or Unix philosophy)

Unix işletim sisteminin lider geliştiricilerinin deneyimine ve yaklaşımlarına dayalı yazılım geliştirme metodolojisidir. bu yöntemler genlde tüm POSIX'lerde tercih ediliyor.

genelde aşağıdaki metodolojilere dayanır:

- Write programs that do one thing and do it well.

- Write programs to work together.

- Write programs to handle text streams, because that is a universal interface.

# Secure by design

güvenlik açıklarını kökten çözüm bulan teknikler için kullanılan terimdir. güvenlik açıklarını spesifik açık bularak kapatmak yerine, kökten (mimarisel) çözüm bulunan yazılımlara/ortamlara "secure by design" denir. yani dizaynın kendisi zaten güvenlidir. örneğin;
- web tarayıcısı hacklenebilir. bunun için birçok güvenlik yöntemi ekleyebiliriz. fakat eğer tarayıcının kendisi, android üzerinde hiçbir yetki kullanmadan çalışır ise; uygulama hacklense bile hacker dış kaynaklara erişemeyecektir. tarayıcının kendisi istese dahi dış kaynaklara erişemeyecektir. işte bu tarz dizaynlara verilen genel bir teknik terimdir. docker veya sanal makinlerde uygulamalr açılarak güvenliğin sağlandığı birçok uygulama vardır.
- sanal paralar dayapısı da buna güzel bir örnektir. sanal paraları güvenli kılan faktör sadece kod güvenliği değildir. sistemin kendisi baştan iyi tasarlanmıştır. sanal para sahipleri kendi paralarının değerinin kaybolmaması için diğer sanal para sunucuları (node'ları) ile uyumlu çalışma durumundadırlar.

# SOLID prensipleri

object orianted için çıkmış 5 tane prensibi birarada bulunduran bir terimdir (baş harflerini birleştirilmiştir): SRP, OCP, LSP, ISP, DIP

- ## Bağımlılığın Ters Çevrilmesi Prensibi (or Dependency Inversion Principle or DIP)

  iki kuralı vardır:

  1. High-level modules should not depend on low-level modules. Both should depend on other high levels.

  2. Abstractions should not depend on details. Details should depend on abstractions.

  Burada; High level'dan kasıt şudur: üst seviyeli sınıf alt seviyeli sınıf'ın metodlarını çağırarak işlem yaratır. Örneğin; shopping servisi, ödeme servisini çağırarak işlem yapar.

  Yukarıdaki iki maddeden çıkaracağımız şudur: Üst seviyeli modüller/sınıflar, alt seviyeli sınıflara/modüllere bağımlı olmamalıdır. Alt seviyeli modüller üst seviyeli modüllere(modüllerin arayüzlerine) bağımlı olabilir.

  Örnek üzerinden gidelim; online ödemeler yapılacaktır. Birçok online ödememiz mevcut. Shop abstract'ımız (burada üst seviyeli sınıf/modül oluyor) online ödemeleri bu şekilde kullanıyor olsun:

  ```java
  public abstract Shop {

    private TaksitliOdeme taksitliOdeme;
    private KrediKartiOdeme krediKartiOdeme;

    ....

    public ode(){

      if(taksitliOdeme){

          alert("Taksitli ödeme icin vade farkı alınacaktır");
          taksitliOdeme.ode();

      } else if(krediKartiOdeme){

          krediKartiOdeme.ode();

      }

  }
  ```

  DIP prensibi yukarıdaki durumun yerine tüm ödemeleri bir interfaceden extend edip, bu interfaceyi Shop sınıfına inject edip kullanmamızı öneriyor. Çünkü aksi durumda ödeme sistemlerinde olacak bir logic değişikliği, shopping class'ında değişikliğe sebep olacaktır.

- ## Arayüzlerin Ayrımı Prensibi (or ISP or Interface Segregation Principle)

  Direk örnek üzerinden gidelim: Mesaj interfacemiz olsun. bunu implemente eden bir MesajImpl sınıfımız olsun. MesajImpl kendi içinde attahmentVideo, attahemtnPhoto gibi özellikler içericek. fakat her mesajda video olmayabilir. sadece foto olabilir. bu sebeple burada önerilen; birden fazla MesajImpl olsun ve her biri video için yada photo için spesifik geliştirilsin. (bir mesajda hem foto hem video olamayacağını varsayarak örnek verilmiştir). bu şekilde her implementasyon sadece tek bir işe odaklı yani; interfacenin metodlarını implemente etmeye odaklı olmalıdır. böylece kullanılmayan metodlar çıkarılmış olacaktır.

- ## Liskov'un Yerine Geçme Prensibi (or Liskov Substitution Principle or LSP)

  sınıfımızda, onu implemente edecek sınıflara özel fonksiyon yada field bulunmamalıdır.

- ## Single Responsibility Principle (or SRP)

  Bir sınıfın yahut metodun tek bir sorumluluğu olmalıdır. eğer metodun/sınıfın değişmesi gerekiyorsa; muhtemelen ona yeni sorumluluklar mı eklenecek şüphesi yaratmalıdır.

- ## Open/closed principle (or OCP)

  code/software should be open for extension, but closed for modification. yani; yeni eklemeler yapıldığında programda minimum değişiklik yeterli olabilmelidir. örneğin; online ödemeler. yeni bir ödeme geldiğinde yeni ödemeyi bir sınıftan implemente edip bir listeye eklememiz yeterli olabilmelidir.
  
  Farklı bir değişle; yeni geliştirme geldiğinde; varolan kodumuzu az editlemeliyiz fakat yeni sınıfılar yaratmalıyız. Bunu ne kadar iyi yapabiliyorsak, koduumuz OCP'ye o kadar yakındır.

# KISS (or Keep it simple, Stupid)

herşeyi basit olmasına dayanan feslefedir.

# Iterative and Incremental development

sürekli olarak ufak geliştirmeler çıkarak yapılan geliştirme yöntemidir. bu şekilde riskler düşürülür, feature/branch merge'ler kolaylaşır.

# Abstraction principle

yazılımı abstract sınıflar kullanarak tekrarlanan kodları azaltma metodolojisidir.

Abstraction; karışık bir implementasyonu, kullanıcıdan veya programdan gizlemek için yeni bir katmanın geliştirilmesidir. Bunun sonucunda anlaşılması ve kullanılması daha kolay bir arayüzün ortaya çıkması beklenir.

# Big Design Up Front (or BDUF)

yazılımın mimarisi oturtulmadan sayfaların/businnes logic'in geliştirmeye başlanmadığı yazılım geliştirme sürecidir.

# top-down design (or top-down approach) vs bottom-up design (or bottom-up approach)
bottom-up design'da bir case için problem çözülür, daha sonra 2 case için ve daha sonra tüm case'leri kapsayacak durumlar çözülür. oysa top-down'da bunun tam tersi yapılır.

# design by contract

direk örnek üzerinden gidersek;

```java
int böl(int a, int b)
{
  contract.requires(b != 0);
  return a / b;
}
```

static kod analizinde derleyici bu kodu yakalayacaktır. işte bu tarz kodlara anlaşmalı kodlar deniliyor.

# Defensive design

kodun kendini koruduğu, böylece alacağı parametrelerle uygulamanın akışının engellenmediği yazılımlara denir. örneğin; ekleyeceğiniz pluginler hiçbir şeyilkde uygulamanızı durdurmamalı. gerekirse plugin kill edilmeli ve uygulama devam etmeli. başka bir örnek: getterlarda döndürülen listeler sadece read only olmalıdır. fakat javada referans döndüğünüz için biri bizim listemizimyObj.getList().add("new element"); diyip ekleme çıkarma ayapabilir. self defensive olup getterlardan objenin klonunu yada read only halini döndürebiliriz. 

# service contract

servislerimizi inject edip başka yerden kullandığımızda inject ettiğimiz şey, bir interface olması görüşüdür. hangi implementasyonun run-tme'de kullanılacağına framework/mimarimiz karar vermelidir. bunun avantajları:

- service'lerimiz interface'lere depend eder implemetasyonlara değil. bu kural farklı patternlerden gelmektedir.

- bazen servislerimizde protected yada public metodlarımız olabilir. bu metodları her zaman dışarıya dğeil, diğer internal sınıfılarımıza açma gereği duyabiliriz. bu sebeple API'miz interface'lerden okunmalıdır. böylece herkes bilirki API sadece interfacededir.

Sadece 1 implementasyonumuz olacaksa bile bunu yapmalıyız. çünkü:

- ilerde 2inci implementasyon gelirse, buna hazır olmuş oluruz.

- API'miz interface olursa dışarıdan okuyan kişi daha kolay ve net olarak hangi metodları çağırması gerektiğini okuyabilir.

Yukarıda bir API'den bahsedildi. API uygulamamızın dışarıya açtığı metodları temsil eder. fakat internal sınıflarımızda API kullanıyoruz demek pek doğru olmaz. Bu sebeple "contract (or anlaşma)" denilmektedir. tabi buradan türeyen diğer terimlerde kullanılabilir: "interface contract", "service contract", "service interface"... Servislerimizin aldığı parametrelere "Message Contact", "data contract" da denilebilmektedir.

# YAGNI (or you aren't gonna need it)

ihtiyaç olmayan özelliklerin projeye eklenmemesi prensibidir.

# over-engineering

over-engineering çözümler her zaman gerekenden fazla özellikleri desteklemek için uygulanır. bu aslında YAGNI ile neredeyse aynı kapıya çıkmaktadır.

# interoperability (or Birlikte çalışabilirlik)
interop kelime anlamı: birlikte çalışma

genel bir terim olduğundan kullanılan domain'e göre farklı şeyi ifade edebilir. bazı örnekler:
- bir programlama dilinin interoperability karakteristiği; o dil ile yazılmış bir koddaki fonksiyonların, diğer diller tarafından yazılmış uygulamalar tarafından çağrılabilirliğini belirtir.
- diğer yazılımların kullandığı dosya formatına okuyup yazabilmekte, uygulamamızın interoperability karakteristiğini yansıtır.
- herkesin okuyabileceği ve yazabileceği bir dosya formatımız olursa, o dosya formatı için interoperability den bahsedilebilir.

İlk maddede belirtilen interoperability karakteristiğini şu maddelerle değerlendirebiliriz:
- dilin kullandığı primitive ve standart objeleri, diğer dillere pass edilebilirliği(uyumu) ve tersi
- diğer dillerden fonksiyonlar çağırdığındaki performansı ve tersi
- ve dahası...

- # Component Object Model (or COM)
microsoft ürünlerinde kullanılabilen IPC için kullanılan, ortak data obje modelidir. dilden bağımsızdır. bu interoperability için diil IPC için kullanılmaktadır. COM; primitive tipler içeren bir standarttır. her dil bu kurallara uyar. bu şekilde haberleştiklerinde ortak değerler ile haberleşirler.

COM; IPC için kullanılır, fakat microsoft dilleri arasında interoperability yapmak gerektiğinde de bu obje tipleri kullanılabilmektedir.

- # Distributed Component Object Model (or DCOM)
COM dan sonra çıkmış Remote procedure call'larda kullanılabilirlik eklenmiştir. bu sebeple Distributed prefixi eklenmiştir.

- # Object Linking & Embedding (or OLE)
COM'a dayanan bir teknolojidir. Bir programdan bir dosyaya referans edebilmemizi sağlar. Örneğin, bir word dökümanında, başka bir excel dosyasının br parçasını gösterebiliriz. excel her güncellendiğinde otomatik olarak word'deki excel görüntüsüde güncellenecektir.

- # CORBA (or Common Object Request Broker Architecture)
Dilden bağımsız geliştirilmiş, DCOM'a alternatif bir standarttır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# magic string
yazılımcılar arasında "hardcode string" olarakta adlandırılır. enum, yada final static olmayan kod içine direk olarak yazılmış string'lere verilen isimdir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# method/function invoke vs call

ikiside kelime anlamı olarak aynı. resmi bir farklılık yok. fakat çoğu zaman "invoke" kelimesi otomatik olarak çalıştırılan metodlar için kullanılırken kullanılır. örneğin; sınıf oluşturduk, içindeki before ve constructor metodları otomatik çalıştırıldı. oysa "call" ibaresi daha çok elle bir fonksiyonu çağırdığımızda kullanılır.

# 'Calling a method' vs 'sending a message to a method'

programlama dilinin metod çağırma yöntemidir. programlama dilini kullanan yazılımcı için, dilin hangi yöntem ile metodu tetiklediğinin bir önemi yok. fakat dil geliştiricileri için bu konu önemli.

örneğin C 'Calling a method' yöntemini kullanır. burada iligli kod bir fonksiyonu çağırdığında, kod direk o çağrılan fonksiyonun içine gider. Objective-C ise 'sending a message to a method' yöntemi ile çalışır. Objective-C'de bir metod mesaja cevap vermeyebilir. yada farklı metodlara yönlendirme gibi durumlar olabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Metot Aşırı Yükleme (or Method Overload)
yazılım dünyasında kullanılan genel bir terimdir. her programlama dili desteklemez. bir metod aynı isimde aynı sınıfta/scope'ta olabilir. fakat aldığı parametrelerin sayısı veya sayısı aynı fakat tipi farklı olabilir. bu duruma verilen isimdir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# IBM DataPower Gateway

donanımdır. web servise gelen isteklerde menipülasyon yapabilmemizi sağlar, genel istekleri filtreleyebilmemizi sağlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# chrome extension vs chrome app

chrome app'e daha çok api açık durumda olduğundan daha çok özellik'ten yararlanabiliyor. + app'ler tarayıcıdan bağımsız bir pencerede tarayıcı penceresi başlatılmaden dahi başlatılabiliyor. burada amaç kullanıcıya daha çok native prgrammış havası yaratmaktır. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# pure vs Impure function

- pure fonksiyonlar sadece bir hesaplama yapıp bir sonuç geri döndürürüler.
- uygulamanın içinde yada dış kaynaklarda hiçbir şeyi değiştirmezler.
- hiçbir şeyi değiştirmedikleri gibi hiçbirşey de okumazlar, okusalar bile, okudukları bu değeri hiç kulanmamalılıdırlar (zaten bu durumda o okuma boşuna yapılmış olur).
- bu şekilde sonuç olarak; her zaman aynı girişe karşı aynı çıktıyı verirler.
- deterministictirler.
- pure olmayan fonksiyonları çağıormazlar. pure olmayan fonksiyonlara örnek: Date.now(), Math.random() kaynak: (source-id: 56) "Handling Actions" başlığındaki, maddelerin olduğu kısımdaki 3 üncü madde.

impure metodlar ise bu kurala uymayan tüm metodlar için geçerli bir sıfattır.

# side effect

bir fonskyionun kendi içindeki değerler haricinde dışarda bazı kaynaklarda değişiklik yapmasıdır. yani dış dünyaya etkisi olmasıdır. örneğin; dosyaya yazması. console.log() metodu dahi dış kaynakları kullanır. console'u milyon saniyesede bir de olsa durdurur ve o kaynağın başkası tarafından kullanılmasını engellemiş olur. databseden veri okumak bile side effect yaratır. okunan veri için dışa kanyaklarda soket açılır, belki o soketler başkası tarafından kullanılacaktı. database sistemi ayarları sebbei ile biri okduğunda başkasının o veriler üzerinde değişiklik yapmasını engelleyebilir. bu da bir etkidir (side effecttir).

# Referential transparency (or referential opacity)

kodun bir satırında bir metod çağırdık. çağırdığımızı bu metodu kaldırıp yerine döndürdüğü değeri yağıştırdığımızıda, tüm yazılım yine aynı şekilde çalışmaya devam ediyorsa, bu metod için "Referential transparency" 'den bahsedilebilir demek oluyor. matematikte her fonksiyon için kesinlikle Referential transparency vardır. fakat yazılımda kesinlikle bu durum var diyemiyoruz. çünkü çağırdığımız metod pure bir metod değilse, "Referential transparency"'den bahsedilemez.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# digital media container vs codec
container dosya formatına denk gelmektedir. bir dosya container'ı kendi içinde birden fazla ses, video, birden fazla subtitle, metadata (album ismi, şarkıcı ismi, album resimleri...) bulundurabilir. bazı container'lar sadece ses içerebilir. bazıları ise sadece resim içerebilir (resim dosyalarınında container'ı var).

codec ise container'ın içindeki sesin veya videonun standartıdır/formatıdır.

bazı container'lar birden fazla codec desteklemektedir.

bir dosya uzantısı, o dosyanın container'ından gelmektedir.

| container name                            | description                                                                                                                                                                                                            |
|-------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AIFF                                      | IFF file format, widely used on Mac OS platform                                                                                                                                                                        |
| WAV                                       | RIFF file format, widely used on Windows platform                                                                                                                                                                      |
| XMF                                       | Extensible Music Format                                                                                                                                                                                                |
| FITS                                      | Flexible Image Transport System - still images, raw data, and associated metadata.                                                                                                                                     |
| TIFF                                      | Tagged Image File Format - still images and associated metadata.                                                                                                                                                       |
| 3GP                                       | used by many mobile phones; based on the ISO base media file format                                                                                                                                                    |
| ASF                                       | container for Microsoft WMA and WMV, which today usually do not use a container                                                                                                                                        |
| AVI                                       | the standard Microsoft Windows container, also based on RIFF                                                                                                                                                           |
| DVR-MS                                    | "Microsoft Digital Video Recording", proprietary video container format developed by Microsoft based on ASF                                                                                                            |
| Flash Video (FLV, F4V)                    | container for video and audio from Adobe Systems                                                                                                                                                                       |
| IFF                                       | first platform-independent container format                                                                                                                                                                            |
| Matroska (MKV)                            | not limited to any coding format, as it can hold virtually anything; it is an open standard container format                                                                                                           |
| MJ2                                       | Motion JPEG 2000 file format, based on the ISO base media file format which is defined in MPEG-4 Part 12 and JPEG 2000 Part 12                                                                                         |
| QuickTime File Format                     | standard QuickTime video container from Apple Inc.                                                                                                                                                                     |
| MPEG program stream                       | standard container for MPEG-1 and MPEG-2 elementary streams on reasonably reliable media such as disks; used also on DVD-Video discs)                                                                                  |
| MPEG-2 transport stream ( a.k.a. MPEG-TS) | standard container for digital broadcasting and for transportation over unreliable media; used also on Blu-ray Disc video; typically contains multiple video and audio streams, and an electronic program guide        |
| MP4                                       | standard audio and video container for the MPEG-4 multimedia portfolio, based on the ISO base media file format defined in MPEG-4 Part 12 and JPEG 2000 Part 12) which in turn was based on the QuickTime file format. |
| Ogg                                       | standard container for Xiph.org audio formats Vorbis and Opus and video format Theora                                                                                                                                  |
| RM                                        | RealMedia; standard container for RealVideo and RealAudio                                                                                                                                                              |

# kayıpsız ses
__Pulse code modulation (or PCM)__ kayıpsız olarak analog sesi, digital ortama kaydetme mantığıdır. bu bir format değildir. 

WAV formatı raw ses data'sını tutar. yani kayıpsızdır. Yani; PCM mantığındadır. PCM mantığında çalışan formatlar bellekten çok fazla yer kaplar. 5 mb'lik bir mp3 dosyası 500 mb'lik bir wav dosyasına denk gelmektedir.

FLAC gibi codec'ler kayıpsız sıkıştırma uygular. yani rar, zip tarzı sıkıştırma uygularlar. fakat sıkıştırılan dosya formatı belli olduğu için, sıkıştırma oranı çok yüksektir. örneğin; 500 mb WAV dosyası, kayıpsız şekilde sıkıştırılıp, 50 mb'lik bir flac dosyasına denk gelir.

Kayıplı sıkıştırmalar ise MP3 gibi dosyalardır. ses kalitesinden ödün vererek sıkıştırma uygularlar ve boyutları çok ufaktır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# BPM (or Business Process Manager)

İş akışını yöteten otomasyonlara verilen genel isimdir.

Piyasadaki bazı BPM Platformları:

- IBM BPM (eskiden Lombardi firması tarafından geliştiriliyordu. IBM satın aldı.)

- Activiti (açık kaynaklı, Alfresco firmasın tarafından geliştiriliyor)

- camunda (açık kaynaklı)

BPM platformları; BPM Engine'ini, IDE'ler için eklentiler, programlama dilleri için engin'i kullanmayı sağlayan API'leri, desteklediği formatları (örnek: BPNM) ve daha bir çok şeyi içinde kapsamaktadır.

BPM platformlarının birçok avantajı vardır. İş akışını belirler ve iş akışı için client tarafa data yollar. Örneğin HTML yollayabilir, bu şekilde her client bunu parse edip ekranda ne göstereceğine karar verebilir. ATM, Mobil, masaüstü, web clientları tek bir iş akışı sunucusundan aynı endpoint'lerden yönetilebilir. Sadece client'a data yollamaz, aynı zamanda session ile ilişkilendirilip her user'ın hangi iş akışına girebileceğini, iş akışı ekranının client tarafta yanlışlıkla kapanması durumunda devam etmesini sağlayabilir. Benzer şekilde hangi user'ların hangi process'lerde ve hangi sayfada olduğunu monitör edip admin'lere sunabilir. istenildiğinde user'lar engellenebilir. performans ölçümü yapılmasını sağlayabilir.

# Business Process Model and Notation (veya BPMN)

İş akışını gösteren bir xml standartıdır. Sürümleri mevcuttur. 

bir bpmn dosyasının içinde birçok akış (or flow) olablir.

her akış içerisinde bşrçok task olabilir. her task son kullanıcı çin birer sayfa gibi düşünülebilir. fakat öyle olmak zorunda diildir. client kendi için bir syafayı 2-3 sayfa içerisinde toplayıp sunucuya istekte bulunabilir. 

Gateway (geçiş) her tasktan taska giderken isteğe bağlı kullanılan karar mekanizmalarıdır. örnek diğer taska giderken, koşul koyulabilir. eğer koşula sağlanmıyorsa kullanıcı farklı bir taskta yönlendirilebilir.

flow, gateway, task gibi objeleri birçok türevi vardır.

bpm sürecini bir örnek ile açıklayalım: internetten kredi çekilebilsin. son kullanıcı banka sistemine login olur ve kredi sürecini başlatır. kullanıcıdan birçok bilgi alınıp son olarak onay tuşuna bastı. artık bu arada kredi henüz alınmadı. daha bankacının onay vermesi gerekmektedir. işte süreçte user 'a bir bildirim yapılıyor ve user daha ileri gidemiyor. ne zaman kredi çekmeye kalksa (yani süreci tamamlamak istese) "temsilcinizdenonay bekliyorsunuz" mesajını görüyor. artık bpm akışı bankacının akışına yönlenmiş durumda (bpmn formatında ok işareti). eğer bankacı kendi sürecini başlatırsa, ve kendi sürecinde olan kısmını tamamlarsa yine ok işareti müşterinini sürecinini içine ok işareti iel göstereceğinden, artık süreç müşteriden devam edecektir. müşteri artık kredi sayfasını açtığında karşısında raporu görecektir. rapor göstermede de sürecin (son) bir parçasıdır. eğer temsilci isterse kullanıcıyı başka bir akışa yönlendirip ek bilgi talebinde bulunabilirdi.  

sub-process, bir task gibi görünür aram referansı bir sub-process yani task grubudur. tekrar kullanılabilirlik sağlamak için kullanılırlar.

# camunda modeler 

İş akışlarını hazırlamaya yarayan masaüstü GUI yazılımıdır.

# kod örneği

aşağıdaki kod parçası Activity BPM Java kodudur:

```java
//engine'i devreye sokuyoruz

ProcessEngineConfiguration cfg = new StandaloneProcessEngineConfiguration()

        .setJdbcUsername("sa")

        .setJdbcPassword("");

    ProcessEngine processEngine = cfg.buildProcessEngine();

    String pName = processEngine.getName();

    String ver = ProcessEngine.VERSION;

//bir akış deploy ediyoruz

    RepositoryService repositoryService = processEngine.getRepositoryService();

    Deployment deployment = repositoryService.createDeployment()

        .addClasspathResource("moneytransfer.bpmn").deploy();

//processDefinition arama sonucunu içeriyor

    ProcessDefinition processDefinition = repositoryService.createProcessDefinitionQuery()

        .deploymentId(deployment.getId()).singleResult();

  

//money transfer akışının bir instance'ını başlatıyoruz

    RuntimeService runtimeService = processEngine.getRuntimeService();

    ProcessInstance processInstance = runtimeService

        .startProcessInstanceByKey("moneytransfer");

//bpm'in sunduğu bir çok servisi kullanmak için bir degere atıyoruz

    TaskService taskService = processEngine.getTaskService();

    FormService formService = processEngine.getFormService();

    HistoryService historyService = processEngine.getHistoryService();

//process dongusune girip tasklar cekiliyor ve her taksı içindeki data çekiliyor ve data service atılıyor

    while (processInstance != null && !processInstance.isEnded()) {

List<Task> tasks = taskService.createTaskQuery()

          .taskCandidateGroup("managers").list();

      System.out.println("Active outstanding tasks: [" + tasks.size() + "]");

      for (int i = 0; i < tasks.size(); i++) {

        Task task = tasks.get(i);

        System.out.println("Processing Task [" + task.getName() + "]");

        Map<String, Object> variables = new HashMap<String, Object>();

        FormData formData = formService.getTaskFormData(task.getId());

        for (FormProperty formProperty : formData.getFormProperties()) {

          if (StringFormType.class.isInstance(formProperty.getType())) {

            System.out.println(formProperty.getName() + "?");
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# swagger 

"SmartBear Software" tarafından geliştirilen REST API doc'u hazırlanması ve client/server API kodlarının otomatik oluşturulması amaçlı geliştirilen yazılım tool'larının bütünüdür.

# swagger definition file

rest API'lerin bilgilerinin swagger formatında yazıldığı JSON yada YAML dosyası.

# swagger editor

json/yaml dosyasını HTML'e çeviren (html API doc üreten) yazılımın adıdır. web projesidir. json/yaml'i verirsiniz, yan tarafta HTML sürümü görünür.

'swagger editor'ün arayüzü bu şekildedir: (source-id: 57)

# Swagger Hub
Closed-source cloud based (not self-hosted) web UI for:
- swagger-editor
- comment support on swagger-editor
- Visual editor support for swagger-editor.
- Team management (users, permissions...)
- Common models (DTOs) cross multiple(independent) Swagger(or OpenAPI) files(projects)
- versioning (simply: swagger-hub get a snapshots of current file and tags it.)
- visual comparator of Swagger(OpenAPI) files (this feature named as "Forking & Merging at documentation)
- push Swagger(OpenAPI) file to remote Source Management System
- Style validation (models should have example values, description must mot have empty string...)

# Swagger Codegen

programlama dilinde yazılmış kodları yml dosyasına çeviren ve yml dosyasından server/client kodu hazırlayabilen yazılımır.

# Swagger UI

swagger-ui sadece html/javascript'ten oluşan bir web yazılımıdır. bu kodları sunucuya attığınızda, index.html'i üzerinden bir web sayfası açılır. bu sayfa sizden yml dosyasının url'sini ister. url'yi girdiğinizde, sayfa otomatik olarak o yml'yi çeker ve parse eder. parse ettikten sonra, web syafasına REST API DOC'ları listeler. bu şekilde doc hazırlanmış olur.

aslında "swagger editor" arkaplanda bu yazılımı kullanır.

'swagger UI'ın arayüzü bu şekildedir: (source-id: 58) Dikkat edilirse yukarıda URL bekleyen bir textbox var. Buraya girilen yml dosyası çekiliyor ve parse edilip sayfanın aşağısındaki kısma DOC yansıtılıyor.

# swagger parser
OpenAPI dosyasını alıp, onu parse edebilmemizi sağlayan java kütüphanesidir. örnek kullanım:

```java
OpenAPI openAPI = new OpenAPIV3Parser().read("./path/to/openapi.yaml");

// Read details of file from openAPI object
```

# OpenAPI Specification (or OAS or old-name:Swagger Specification)
swagger yml dosyasında bir standartı var. bu wsdl dosyasının benzeri bir yml dosyası. bu dosyanın formatını 3.0 sürümüne kadar swagger kendi belirliyordu. 3.0 ile OpenAPI olarak yeni bir repo'da geliştirmeye başlandı. OpenAPI'nin ilk sürümü 3.0 ile başlamış oldu.

bankacılık sektöründe kullanılan "open api" ile hiçbir bağlantısı yoktur. "OpenAPI Specification"'daki "open" kelimesi spesifikasyonun açık kaynaklı standartlara dayandığını temsil etmektedir. OAS sadece REST için bir spesifikasyondur.

OpenAPI repo'sunda eski sürümlerin doc'ları da yer almaktadır. onlar "open api 2" diye yazılmış fakat swagger formatlarıdır.

Piyasada "open api" veya "public api" terimleri, API'nin dışarıya açıldığını göstremek için kullanılmaktadır. Bu da bazen karışıklığa sebep olabiliyor.

# swagger version history (or OpenApi versiyon history)
| version | release date | note                                             |
|---------|--------------|--------------------------------------------------|
| 3.1.0   | 2021-02-15   | Release of the OpenAPI Specification 3.1.0       |
| 3.0.3   | 2020-02-20   | Patch release of the OpenAPI Specification 3.0.3 |
| 3.0.2   | 2018-10-08   | Patch release of the OpenAPI Specification 3.0.2 |
| 3.0.1   | 2017-12-06   | Patch release of the OpenAPI Specification 3.0.1 |
| 3.0.0   | 2017-07-26   | Release of the OpenAPI Specification 3.0.0       |
| 2.0     | 2014-09-08   | Release of Swagger 2.0                           |
| 1.2     | 2014-03-14   | Initial release of the formal document           |
| 1.1     | 2012-08-22   | Release of Swagger 1.1                           |
| 1.0     | 2011-08-10   | First release of the Swagger Specification       |

# Springfox

java-spring projeleri için REST-DOC oluşturma parse kütüphanesidir. springfox bir interface sunuyor. Springfox kullanmak için springfox-swagger gibi implementasyonların projeye import edilmesi şarttır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# .net framework

sistemde yüklü olmalı ki, bu framework'ten yararlanan uygulama yürütülebilsin. aynı jvm'de olduğu gibi. .net, sadece c# değil, başka diller için de API'si mevcuttur. ".net" bir runtime'a ihtiyaç duyuyor. Aynı JVM gibi. bu runtime'ın ismi __Common Language Runtime (or CLR)__. JVM bytecode'u çalıştırabilirken, ".net" __Microsoft intermediate language (or MSIL)__'ı çalıştırmaktadır.

# .net core

.net'in sadece linux, mac ve windows'ta çalışılabilir bir türevidir. sadece windowsta çalışacak bir uygulama yazılacaksa .net tercih edilmelidir. ".net framework", .net core'a göre daha çok özellik içeriyor.

# .net standart

isim karışıklığına sebep oluyor fakat kendisi başlıca farklı bir kütüphane grubu. tüm platformlar (mobil/xamarin, desktop, core...) için ortak olan kütüphaneleri temsil ediyor.

# MONO

C# uygulamalarının windows harici sistemlerde derlenmesi ve çalıştırılması için gerekli tüm projeleri (IDE, api,...) kapsar. açık kaynaklı bir projedir.

Mono projesi .net'in açık kaynaklı  bir implementasyonunu içermektedir. fakat api'ler aynı olduğundan direk olarak uygulamaları derleyebilemkte ve yürütebilmektedir.

# MonoDevelop

mono projesi altında geliştirilen IDE.

# Xamarin

Mono projesi tabanlı bir framework. mobil platformlar için c#'ta yazılan uygulamaların diğer sistemlerde çalışabilmesini sağlıyor.

# ISS (or Internet Information Services)

Microsoft'un web server'ı.

# ASP (or Active Server Pages)

Microsoft'un jsf alternatifi framework'ü. 

# ASP.net

.net projesi'nin bir altkümesidir. .net'in sadece asp kümesini kapsar. 

# ASP.net core

.net core projesi'nin bir altkümesidir. .net core'un sadece asp kümesini kapsar. Bu yapı ile "ISS express" olarak adlandırılan portable ve windows harici sistemlerde çalışabilen bir ISS türevi geliştirilmiştir. böylece asp.net core ile cross platform sunucular çalıştırılabilmektedir.

# nuget

maven tarzı c# için dependency yöneticisi.

# steel toe

"spring cloud" mimarisindeki servislere entegrasyon sağlamak için hem sunucu hemde client kütüphanelerini içeren, c# için açık kaynaklı kütüphane.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Solr vs elastic search

Ikiside açık kaynaklı birbirine alternatif arama indexleyici ve döndüren yazılımlardır.

Solr'da field isimleri ve field type'lar baştan belirtilmek zorundadır. Yeni field eklemeye kalktığınızda bütün kayıtları tekrar Solr'a aktarmanız gerekiyor. elastic'te böyle bir durum yok. Çünkü elastic scheme barındırmıyor. No-sql-db gibi.

# elasticsearch
tüm field'a bağlı alanlar tek bir yerde index'lenir. örneğin;

```
1- a b c
2- x y z
3- a x
```

3 adet kaydımız olsun. elastic şu şekilde index tutar:

```
a -> 1, 3
b -> 1
c -> 1
x -> 2, 3
y -> 2
z -> 2
```

'x' terimini arattığımızda direk 2 ve 3üncü document'lerde olduğunu bulmamızı sağlar.

elasticsearch dışarıya REST API sunar, bu dilden bağımsız sorgu atabilmemizi sağlar.

### shard
kelime anlamı: parça

elastic'in tuttuğu her index tek bir makinede tutulmayabilir. onu partititon'lara ayırabiliriz. ayırdığımız her partititon'a shard denir.

1 node'a 'shard' dememek gerekli. çünkü 1 node 1'den fazla shard içerebilir ve aynı zamanda replica görevi de görebilir. kaynak: (source-id: 59) answer of 'prayagupd' at Nov 7 '13 at 15:29.

### replica
her shard'ın tutulacağı replika node'lara verilen isimdir.

### index
normal veritabanındaki tablo'ya denk gelen kavramdır. en üst seviye bilgi grubudur. her index'e bir alias atılmak zorunda değildir. fakat atılması mutlaka önerilir. bir sistemde min 1 index olmalıdır. kaynak: (source-id: 60)

### Indices
'index' teriminin çoğul hali olduğundan, relational-db'lerdeki veritabanına denk geliyor diyebiliriz. çünkü; birden fazla index yani tablo bir database'i tanımlar.

### Mapping
normal veritabanıdaki şemaya denk gelir. istenirse tipler önceden mapping ile belirtilebiliyor.

fakat elasticsearch yeni bir kayıt eklendiğinde verinini yapısını zaten tespit ediyor. kaynak: (source-id: 61) "Elastik" başlığı 1inci paragraf.

### Document

normal veritabanıdaki tablo içindeki kayda (row) denk gelir.

### Type

Document'in tipini belirtir. user, tweet tipinde farklı document'ler olabilir.

### field

normal veritabanındaki her tablo içinde olan bir sutuna denk gelir. elastic no-sql olduğu için json tutar ve her field bir json property'dir.

### kayıt eklemek

elastic search önceden şema istemediğinden attığımız yeni kaydı direk kabul eder ve bundan arama yapılabilmesini kendisi sağlar. yeni kaydımızı Rest api'si ile ekleyelim:

> PUT ELASTIC_SEARCH_URL/customer/_doc/1

```json
{
  "name": "John Doe"
}
```

dönüşü:

```json
{
  "_index" : "customer",
  "_type" : "_doc",
  "_id" : "1",
  "_version" : 1,
  "result" : "created",
  "_shards" : {
    "total" : 2,
    "successful" : 2,
    "failed" : 0
  },
  "_seq_no" : 26,
  "_primary_term" : 4
}
```

şimdi kaydımızı çekelim:

> GET /customer/_doc/1

dönüşü:

```json
{
  "_index" : "customer",
  "_type" : "_doc",
  "_id" : "1",
  "_version" : 1,
  "_seq_no" : 26,
  "_primary_term" : 4,
  "found" : true,
  "_source" : {
    "name": "John Doe"
  }
}
```

Birçok döküman indexlenecek ise, tek tek yerine performans açısından "_bulk" apisi tercih edilmelidir.

Birçok kayıt indexlemiş olalım. Şimdi bu kayıtlarımızı arayalım:

> GET /bank/_search

```json
{
  "query": { "match_all": {} },
  "sort": [
    { "account_number": "asc" }
  ]
}
```

dönüşü:

```json
{
  "took" : 63, //how long it took Elasticsearch to run the query, in milliseconds
  "timed_out" : false, // request timeout or not.
  "_shards" : { // how many shards were searched and a breakdown of how many shards succeeded, failed, or were skipped
    "total" : 5,
    "successful" : 5,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
        "value": 1000,
        "relation": "eq"
    },
    "max_score" : null,
    "hits" : [ {
      "_index" : "bank",
      "_type" : "_doc",
      "_id" : "0",
      "sort": [0],
      "_score" : null,
      "_source" : {"account_number":0,"balance":16623,"firstname":"Bradshaw","lastname":"Mckenzie","age":29,"gender":"F","address":"244 Columbus Place","employer":"Euron","email":"bradshawmckenzie@euron.com","city":"Hobucken","state":"CO"}
    }, {
      "_index" : "bank",
      "_type" : "_doc",
      "_id" : "1",
      "sort": [1],
      "_score" : null,
      "_source" : {"account_number":1,"balance":39225,"firstname":"Amber","lastname":"Duke","age":32,"gender":"M","address":"880 Holmes Lane","employer":"Pyrami","email":"amberduke@pyrami.com","city":"Brogan","state":"IL"}
    }, ...
    ]
  }
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# exif (or Exchangeable image file format)

Media dosyaları için kullanılan aynı dosyaya gömülen metada bilgilerinin formatıdır. "Exiftool" açık kaynaklı komut satırı programıdır. Bu program ile dosyalarının exif bilgileri okunup manipüle edilebilmektedir.

Exif bilgileri arasında birçok çeşit bilgi vardır. Örneğin; fotoğrafın çeken device bilgileri, fotoğrafın çekildiği saat, lokasyon...

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# protocol vs format vs codec (or Çözücü)

format dosyaların yapısını(standartlarını) belirlerken, protokol communication yapılarını belirlemektedir.

codec terimi ise; "coder-decoder" ın birleşiminden gelir. siyanl veya digital olan datayı, bir formdan başka bir forma convert(decode/encode) eden yazılım/yöntem/araç'tır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# popup

açılan ufak pencrelerin tümüne verilen genel isimdir.

# Modal vs Dialog

ikiside aynı anlama gelmektedir. Pencerede kullanıcı için focus olunan bir popup açılır. Core HTML'in dialog özelliği mevcut (Önemli: Alert değil! İçine istediğimiz objeleri atabildiğimiz popup  var.). Fakat bootstrap gibi kütüphaneler kendi dialog'larını da yazmıştır.

# Popover vs Tooltip

ikiside aynı anlama geliyor. Genelde fare ile bir objenin üzerinde durulduğunda açıklaması için açılan popup'a verilen isimdir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# International Standard Name Identifier (or ISNI)

birçok media tipinde verilere yada ürünlere id atamak için kullanilan sistemerin tümüdür (ailesidir). bazi medya/ürün tipleri su sekildedir:

- International Standard Book Number (or ISBN) (sadece kitap)

- Serial Number (dergi, gazete, website, database, yayin, makale, blog)

- Text Code (metin çalismalari)

- Musical Work Code

- Music Number

- Recording Code (video veya ses kayitlari)

- Wine Number (şarap)

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Sistem Programcılığı

Daha çok işletim sistemi ile yada donanım bilgisi gerektiren yazılım dilleri ve kütüphaneleri kullanarak yazılım geliştirmedir. Bu sebeple; genelde üst seviyeli diller buna gruba dahil olmaz. Bu sebeple; genelde sürücü (driver) yazanlar bu gruba dahildir.

# sistem çağrıları (or çekirdek çağrıları)

İşletim sistemi ile kullanıcı programları arasında tanımlı olan arayüz, işletim sistemi tarafından tanımlanan bir prosedürler kümesidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Controller Area Network (or CAN bus)

bir iletişim prtokolüdür. genelde araçlarda her birim arası haberleşme için tercih edilir. 

her birim ağı sürekli dinler ancak ağ boş ise mesajını tüm ağa yollar. her birim kendi alacağı mesajı önceden bilir ve kendisini ilgilendirmeyen mesajları dikkate almaz. haberleşme limitli max 1km uzunlukta kablo ve 1mb/sec hızında gerçekleşmektedir. çünkü sürekli ağı dinleyen birimler vardır. eğer ağın boş olduğunu düşünüp, birden fazla birim aynı anda mesaj yollamaya kalkarsa hata (çatışma - collision) meydana gelir. bu sebeple kablo uzunluğu ve veri boyutu sınırlı tutulur. bu şekilde ağ dinlemelerinde uzaktan gelen veriden habersiz olma gibi bir durum söz konusu olmaz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# file type detection

dosya formatını tanımak %100 olarak mümkün diildir. bazı uygulamalar her format için dosya kalıplrını (format yapısını-template'ini) inceliyor ve benzerlik oranına göre sonuç döndürüyor.

bazı dosya formatları genelde dosyanın en başına dosya formatını yazan birkaç bitlik bir yer bulundururlar. fakat bu bile bir dosyanın %100 txt olmayacağı anlamına gelmez.

# binary file

saf text olmayan bütün dosyalara verilen genel isimdir. anlamlı hale getirebilmek için basit yada komplex parse işlemleri yapılmalıdır.

pdf, word, zip, exe, bin dosyaları binary'dir. oysa json, xml, java, csv, sh dosyaları text dosyalarıdır. 

dosya sistemleri seviyesinde bir farklılık yoktur. sadece son kullanıcı için "text dosyası" ve "binary dosyası" olarak gruplandırılmışlardır.

bazı proramlama dilleri API'lerinde dosya okuma işlemlerinde binary olup olmadığı bilgisini isteyebilir. bunun birkaç sebebi var:

- eğer binary dosya açılırsa; satır sonu karakterlerini işletim sisteminin belirlediği default karaktere göre otomatik değiştirmez

- eğer binary açılırsa; end-of-file karakteri en sona otomatik koyulmaz.

- eğer binary açılırsa; write read metodları byte okur, oysa text açılırsa belli bir encoding'de string döner. 

her API farklı kuraller/tepkiler gösterebilir. bu sebeple API'yi incelemek gerekli. bazı kütüphaneler byte ve text için ayrı ayrı sınıf/metod sunuyor olabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Steganografi (or Steganography)

bilgiyi gizleme (önemli: şifreleme değil) bilimine verilen addır. Steganografi'nin şifrelemeye göre en büyük avantajı bilgiyi gören bir kimsenin gördüğü şeyin içinde önemli bir bilgi olduğunu farkedemiyor olmasıdır, böylece içinde bir bilgi aramaz. Bilişim dünyasında kullanılır. örnein; seste veya görüntüdeki küçük bozuklukları insan beyni farkedemediği için, kasıtlı olarak periyodik bozukluklar şeklinde dosyanın içine başka bir dosya saklanabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Cache (or Önbellek)

yazılımsal ve donanımsal olarak ayrılmaktadır. donanımsal önbellekler; daha hızlı erişilen belleklere denir. örneğin "cpu cache". cpu cache cpu üzerindedir ve ram'den dahi daha hızlı erişilebilir. fakat maliywtli olduğundan çok çok ufak boyuttadır. cpu cache'in, özel amaçlı donanımlar hariç, yazılımcılar tarafından kullanması önerilmez. fakat klasik işletim sistemi bu kısmın editlenmesi için API sunmuş olabilir.

# tr:tampon (or data buffer or buffer or ara bellek)
cache ile tamamen farklı kavramlardır. cache dataya hızlı erişmek için bir data'nın farklı fiziksel alanda tutulan bölgesidir. oysa buffer; bir data'nın bellekte fizisel olarak farklı bir yere taşınmadan önce tutulduğu bölgedir.

# JCache
JCache is the Java caching API. It was defined by JSR107.

Bunu kullanmamız bir için runtime'da bir implementasyona ihtiyaç duyarız. Örnek implementasyon: Ehcache.

interface'ler için maven dependency'si:

```xml
<dependency>
  <groupId>javax.cache</groupId>
  <artifactId>cache-api</artifactId>
</dependency>
```

JCache'nin RI (or reference implementation)'u mevcut. Fakat bu RI, prod ortamında kullanılmak üzere tasarlanmamıştır. Sadece implementasyonun işleyişini gösterebilmek adına tasarlanmıştır.

# Spring Cache
birçok implementasyon (jcache...) için bir wrapper API'dir.

# Guava Cache example

Guava isimli kütüphanenin cache modülü için örnek kod:

```java
CacheLoader<String, String> userLoader;
userLoader = new CacheLoader<String, User>() {
    @Override
    public User load(String userId) {
        return getFromDatabase(userId);
    }
};

LoadingCache<String, String> userCache;
userCache = CacheBuilder.newBuilder()
                        .maximumSize(50)
                        .expireAfterAccess(2, TimeUnit.MINUTES)
                        // or expireAfterWrite 
                        .removalListener(myListener)
                        .build(userLoader);

// or by weigh:
// if the userName is longer than 1000 it will be removed from cache.
userCache = CacheBuilder.newBuilder()
                        .maximumWeight(1000)
                        .weigher(new Weigher<String, User>() {
                            public int weigh(String userId, User user) {
                              return user.getName().lenght();
                            }
                        .build(userLoader);

System.out.println(employeeCache.get("100"));
// on below line, the data will be returned from cache:
System.out.println(employeeCache.get("100"));

// manually add vaue to cache:
employeeCache.put("300", new User("300"));
```

görüldüğü gibi getFromDatabase yerine tekrar çağrıldığında ram'deki bellekten getiriyor sonucu. yazılımsal cache'lerin en temel/basit örneklerden biri budur.

Bazı uygulamalar user-home dizininde bir klasörde cache isimli dizinler yaratmaktadır. uygulamalar kapandığında yada belli aralıklarla ram'deki bu cache datalarını dosyalara yazarlar. böylece uygulama restart edildiğinde, cache direk olarak RAM'e yüklenecektir. tekrardan cache'in dolması beklenmeyecektir.

# cache algorithms (or cache replacement algorithms or cache replacement policies)  

bu tarz algoritmalar bir sıralı listeyi yönetmek için kulanılırlar. bu algoritmalar, hangi parçaların tutulacağı ve yeni parçalara yer açmak için hangi parçaların atılacağına karar vermek zorundadır.

 örnekler:

- First In First Out (or FIFO)

- Last In First Out (or LIFO)

- Least Recently Used (LRU): en eski kullanılan veri, yeni eleman geldiğinde ilk çıkarılır.

- Most Recently Used (MRU): en yeni kullanılan veri, yeni eleman geldiğinde ilk çıkarılır.

- Least Frequently Used (LFU): en az sıklıkta kullanılan veri, yeni eleman geldiğinde ilk çıkarılır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# User Account Control (or UAC)

(başka bir başlıkta da bu konu hakkında yazı mevcut)

# Squirrel

Atom text editorun kullandığı bir altyapıdır. bu yaızlım sayesinde uygulama program files'e değilde, user-home dizinine kurulmaktadır. bu şekilde, uygulama güncellendiğinde son kullanıcıdan yetki istememektedir. çünkü proram files'teki yazlım güncellemesi için son kullanıcıdna yetki istenmektedir. Squirrel aynı zamanda update işlemlerini kolaylaştıran ve API sunan bir altyapıdır.

# Chrome auto update

GOogle chrome Squirrel veya benzeri bir yapı kullanmamaktadır. Chrome kurulduğu işletim sistemine update işlemi için windows servisi eklemektedir. bu servis admin yetkisindedir. bu sebeple son kullanıcya soru sormadan program files'teki chrome'u güncelleyebilmektedir.

# ms-windows (arkaplan) servisleri kullanıcı kısıtlamaları ile yürütülüyor

windows servisleri kullanıcı bazlı çalışmaktadırlar. bu sebeple yetkileri kısıtlanabilir. bu kullanıcıların home klasörleri olmayabilir. çünkü sadece yetki kısıtlama amaçlı oluşturulmuşlardır. az yetkiliden çok yetkiliye örnek kullanıcılar; LocalService, NetworkService, LocalSystem.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# mmap
Memory map'in kısatlmasıdır.

posix system call'udur. bir dosyayı memory'de adresler. dosyanın her byte'ına RAM'den erişilebilir olur. fakat birçok nmap implementasyonu tüm dosyayı ram'e kopyalamaz. lazy loading yapar.

# genel *nix mimarisindeki memory terimleri

- resident memory

  resident türkçe kelime anlamı: oturan, sakin, yerleşmiş

  sadece RAM'deki memory.

- shared memory

  diğer process'lerle ortak kullanılan bellek boyutudur. Inter-process communication protokolleri aracılığı ile (veya benzeri yollar ile) kullanılan ortak memory'dir.

- Virtual Memory (önce "Sanal bellek (or swap space or takas alanı)" başlığı okunmalı)

  virtual memory; swap memory'den farklıdır.

  virtual memory = swap + resident memory + mmap

# "Gnome system monitor" ile gorulen proceess degerleri

- memory

  memory = resident - shared (çıkarma işlemi)

- opened files

  "__lsof (list of open files__ kısaltmasından gelir)" komutu çıktısının aynısıdır. 

  bu listede bir processe ait açık olan tüm dosyalar tutulur. dosyalar soket, pipe (process output), binary files gibi dosyalar olabilirler (unix-like'ta herşey dosya olması yapısı)

- memory map

  bir process'in virtual memory'si için her detayın (kaynağın) tutulduğu haritadır. mmap system call'u ile alakası yoktur. bellekteki tüm değerler (swap + resident memory + mmap)  yanyana tutulmaz. parça parça tutulur. bu sebeple bu tüm parçaların başlangıç ve bitiş adreslerine memory map haritasından bakabiliriz.

# htop komutu ile gösterilen bazı sutunlar

- PPID

Parent process id

- PGRP

Process group id. her process'in group id'si parent process'in group id'sidir. fakat eğer process'in kendisi alt process'ler başlatmış ise, yeni bir group id alır. aldığı group id, process id ile aynı atanır.

- NI (nice)

işlemciye giriş için öncelik seviyesi. numara büyüdükçe önceliği yükselir.

- PR (priority)

PR = 20 + NI. Nice -20 +20 aralıdğındaki değerini gösteryor. bu değer user tarafından değiştirilebilen  öncelik seviyeleridir. oysa linux'ta çok daha fazla değer vardır. tüm değerleri priority gösterirken, kullanıcı bazlı seviyeleri NI gösteriyor.

# top/htop shows different result than gnome system monitor

cpu farkının sebebi: gnome system monitor 8 cpu'muz varsa 8'i %100'e tamamlıyor. yani tüm cpu'lar tümüyle harcanırsa ancak %100 gösteriyor. fakat top yada htop komutunda bu değer %800 oluyor. bu sebeple genelde 8 cpu'lu bir makinede gnome system monitor 8 kat daha düşük değer gösteriyor. tabi gnome system monitor aynı zamanda bu değeri yuvarlıyor.

memory: memory değerleri de yuvarlanıyor.

# Windows 10 task manager işlem detayları sekmesinde olan bilgiler:

- PID: Process ID

- Status: process state

- Session ID: Login user ID

- CPU Time: How much time the process use the cpu (not: process yaşam süresi değil)

- Image Path name: Path of executable which started

- Command Line: Hangi komut ile bu programın başlatıldığını yazar. Örneğin "myservice -param1 -param2" gibi. myservice buada full path'de olabilir.

- Platform: 32 bit or 64 bit executable is rurnning

- Operating System Context: Hangi uyumluluk modunda çalıştırıldığını belirtir

- Description: İşletim sistemi belirtmiş ise uygulama ismi, belirtmemiş ise process adı yazar.

- data execution prevention: cpu ve işletim sisteminin desteklemesi gereken bir özelliktir. bu özellik sayesinde belirtilen uygulama, işletim sisteminin belirttiği bellek alanları dışında bir yere erişmesi engellenir. bu alan, window'un bu programa bu güvenliği uygulayıp uygulamadığını yazar.

- UAC Virtualization: UAC windows'ta yeni gelen bir teknoloji. Bu tkenoloji ile uygulamaların yetkileri kısıtlanmaktadır. Eski uygulamalar ile uyumluluk sağlayabilmek amaçlı bu özellik o uygulama için enable hale gelebilir. Bir uygulama  için bu özellik aktif ise, uygulama yetkisi olmayan bir yere yazmaya kalkdığında, yetki hatası almıyor fakat bu dizine yazdığı dosyalar aktarılıyor: C:\Users\username\AppData\Local\VirtualStore

- Base priority: İşlemciye giriş için öncelik seviyesidir.

- Handles: Windows uygulamanın açtığı bazı kaynakları tutmak/yönetmek Handle kavramından yararlanır. Soket, dosya, pencereler, pencere objeleri gibi… Bunların yazılımdaki "sınıf"'ları gibi düşünülebilir. Bunların toplam sayısı bu alanda yazmaktadır.

- Cycle: CPU hayat döngüsünün (fecth-decode-execute instruction) yüzde kaçının bu işleme ait olduğunu yazıyor.

- Private working set: İşlemin kullandığı toplam RAM değeri

- Peak working set: Uygulamanın yaşam süresi boyunca aldığı maximum "working set" değeri.

- Working set: Private working set + Shared working set

- Working set delta: "Working set" değerindeki anlık değişimin toplam değeri. Örnek: 300'den 350 ‘ye çıkmış ise o saniyede 50 değerini alır.

- Shared working set: Diğer process'lerle paylaşılabilen toplam "working set" değeri.

- Commit size: Toplam Sanal bellek değeri

- Page faults: Uygulama bellekten bir bilgiye erişmek istediğinde, önce RAM'e bakar. orda yoksa "sayfa hatası" alır. bu demek oluyorki, sanal belleğe (yani; hdd/ss'ye yani; ikincil belleğe) bakması gerekli. uygulama başladığında itibaren kaç kere bu hatayı aldığını gösterir.

- PD Delta: "Page faults"'un o andaki değişim değeri.

# Linux Page Cache
Linux'ta olan bir özelliktir. "meminfo" ve "free" komutlarının çıktısında 'Linux Page Cache'nun kaç MB harcadığını 'Cached' başlığı altında görebiliriz. kaynak: (source-id: 62) "Memory Usage" başlığı ilk cümle.

Dosyadan read yapıldığında dosya memory'ye alınır. eğer dosya kod içerisinden kullanımı bırakılırsa; bu memory böylgesi Linux Page Cache'e saklanır. Eğer tekrar aynı dosya okunmak istenirse bu bölgeden okunur. kaynak: (source-id: 62) ilk paragraf.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Sanal bellek (or swap space or takas alanı)

sanal bellek terimi 3 farklı durum için eş anlamlı kullanılıyor:
- top komutunun manual'ında belirtildiği gibi 3 farklı memory var. bir çeşidi virtual memory olarak adlandırılmış. fakat bu bildiimiz swap dosyası alanı değil. (source-id: 422)
- swap space
- her process , OS tarafından sanal bir bellekteymiş gibi çalıştırılabilir (bunun en gerçek örneği comtainer'lar içindeki uygulamalardır). bu belleklere sanal bellek denilir.

bu başlıkta sanal bellek; swap space'e eş anlamı olarak kullanılmıştır.

sanal bellek; ram'in yetmediği durumlarda kullanılan diğer bellek alanına (burada hdd/ssd oluyor) verilen isimdir. burada; RAM __birincil bellek__, hdd/ssd ise __ikincil bellek__ olarak isimlendirilir.

Sanal belleğin hdd/ssd'deki karşılığı bir dosya da olabilir yada bir partition'da olabilir. windows'ta her zaman bu bir dosyadır: C:\pagefile.sys

"Takas" ibaresi şuradan gelir: OS'lar ikincil bellek alanından data okuyacağı zaman onu önce RAM'e (birincil belleğe) kopyalar. oradan okur. bu işlem __takas yapma (or swapping or paging in or faulting in)__ olarak adlandırılır. çok swapping yapmakta zaman kaybettirir. bu oranı OS'un iyi tutturması gerekir.

Bir programda üretilen/kullanılan adresler gerçek __fiziksel adresler__ değildir. Programda üretilen adreslere __"logical address (or mantıksal adres)"__ denir. logical adresler, işletim sistemi seviyesinde veya donanımsal katmanda gerçek fiziksel adreslere çevrilmektedir.

sanal bellek yapısı kullanan sistemlerde "logical adress" yerine __virtual adress__ ibaresi de kullanılabilmektedir. 

# segmentation (or segmentasyon)

OS'lar çalışan programlara ihtiyaçları kadar bellek atar ve bu bellekleri ardarda sıralayarak koyar. daha sonra bir process kapandığında onun kullandığı bellek kısmı silinir, fakat memory optimize edilmez. dolayısı ile memory'de arada boşluklar kalır. OS eğer boşluktan daha düşük memory isteyen bir uygulama gelirse, boşalan yeri dolduruyor. fakat %90 boşluğun tümünü doldurmayacağı için her zaman boşluklar kalıyor.

örnek:
```

   ******************
   *    100 MB      *  (A process için ayrılmış bellek alanı)
   ******************
   *                *
   *                *  (B process için ayrılmış bellek alanı)
   *    300 MB      *
   *                *
   ******************
   *    100 MB      *  (C process için ayrılmış bellek alanı)
   ******************


   B processi kapansın.


   ******************
   *    100 MB      *  (A process için ayrılmış bellek alanı)
   ******************
   *                *
   *                *  boş alan
   *    300 MB      *
   *                *
   ******************
   *    100 MB      *  (C process için ayrılmış bellek alanı)
   ******************


   250 mb isteyen E Processi gelsin.


   ******************
   *    100 MB      *  (A process için ayrılmış bellek alanı)
   ******************
   *    250 MB      *  (E process için ayrılmış bellek alanı)
   *                *  
   ******************
   *    50 MB       *  boş alan
   ******************
   *    100 MB      *  (C process için ayrılmış bellek alanı)
   ******************
```

Yukarıda görüldüğü gibi boş alanlar kalabiliyor. bu kalan kalıntılara __harici hafıza kırıntılarıdır (or external fragments or harici parçalar)__ denir. buna çözüm olarak __sayfalama (or Paging)__ yaklaşımı kullanılıyor.

# paging (or sayfalama)

fiziksel bellek alanı eşit büyüklükteki parçalara bölünür. Bunların her birine __sayfa (or page)__ denir. Bu sayfalara karşılık gelen fiziksel bellek alanlarına ise __sayfa çerçevesi (or page frame)__ denir.

sayfa ve çerçeve terimlerinin farklı olmasının sebebi şudur: bazı durumlarda birden fazla page, fziksel bellekteki aynı çerçeveye bakıyor olabilir. örnek durumlar:
- shared memory
- örneğin bir yazılımı 2 kere başlatalım. OS ve uygulama bunun tersini belirtmemişse, uygulamanın kendsi bellekte bir kere yer kaplar.
- common readed files
- bazen 1 page hiç pencereye bakmıyor bile olabiliyor: hiç initialize edilmemiş bir array olsun yada tümü null/0 olarak allocate edilmiş bir array olsun. bu gibi durumlarda OS bu frame'leri bayrak atıyor ve gerçek fiziksel bellekte karşılıklarını tutmuyor.

sadece "frame" terimi "page frame" yerine kullanılmamalı. bu yanlış. karışıklığa sebep oluyor. çünkü "frame" tek başına benzer anlamlar taşıyabiliyor.

Paging çözümünu, segmentasyona göre daha avantajlı fakat %100 verimli değil. 1 frame birden fazla uygulama tarafından kullanılamaz. bu sebeple en az PAGE_SIZE kadar process'lere alan tahsis edilir.

PAGE_SIZE=100 olsun. 1 process 210 mb isterse ona 100*3=300 mb'lik yer tahsis edilir. burada 90 mb boşuna harcanır. bu kalan kalıntılara __iç hafıza kırıntısı (or internal fragments)__ denir.

PAGE_SIZE küçüldükçe memory'deki kırıntılar azalır fakat her page mapping genişleyeceği için performansta farklı dezavanjlar yaşanacaktır. OS bu oranı iyi tutturmalıdır.

# haritalama (or mapping)

__page table__ OS'un kendi içinde tuttuğu bir tablodur. bu tablo ile __mapping__ yapılabilmesini sağlar. logical adres'leri fiziksel adreslere çevirir. örnek bir tablo;

| Sanal bellek mi gerçek bellek mi? | Page/segment'in başladığı gerçek fiziksel taban adresi |
|-----------------------------------|--------------------------------------------------------|
| gercek                            | 1000                                                   |
| gercek                            | 2000                                                   |
| sanal                             | 4000                                                   |

# sayfa hatası (or page fault)

bu konu "Windows 10 task manager işlem detayları sekmesinde olan bilgiler" altında nalatılıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# CAPTCHA (or Completely Automated Public Turing test to tell Computers and Humans Apart)
puzzle yapma, matematik işlemi yapma, ekrandaki metni girme, sesi dinleyip metne çevirme gibi birçok çeşidi vardır.

# No CAPTCHA
risk analizinden geçmiş kullanıcı akışına verilen özel isim.

# hcaptcha
privacy orianted bir CAPTCHA'dır. site sahiplerine her çözülen CAPTCHA için Ethereum üzerinden "Human Token" verilmektedir. 

# reCAPTCHA
google'ın sunduğu CAPTCHA hizmetinin özel ismidir.

v2 ve v3 gibi farklı sürümleri ve yetenekleri vardır.

google reCAPTCHA risk analizinde, Canvas Rendering fingerprint, User-Agent, screen resolutions'tan da yararlanılıyor. Bazı kaynaklarda mouse movements patterns'ler ile yapılan testlerde hiçbir fark görülmediği yazıyor. Kaynak: (source-id: 64) title: "Screen Resolution and Mouse".

google artık metin göstermiyor. Artık resim gösteriyor. bunları son kulanıcılara gruplandırtıyor (lategorize ettiriyor). bu şekilde kendi veritabanını ve yapay zekasını geliştiriyor.

google ocr olsun, resim olsun şu şekilde çalışıyor: 10 kutu resim seçeneği varsa bunların 6'sı google'ın ne gruba girdiğini %100 bildiği resim oluyor. Diğer 4 ü google'ın ne anlama geldiğini bilmediği resim oluyor. google bisikletleri seçin dediğinde, google aslında sadece 6 tane emin olduğu üzerinden validasyon(risk analizi) yapıyor. diğer 4'ü son kullanıcının insiatifine kalmış. bu bilgiler sunucuda tutuluyor. binlerce son kullanıcı bu 4 tane belirsiz resimlerde bisiklet olduğunu seçmiş ise, google bu seçilen resimlerin bisiklet grubuna girdiğine karar veriyor. işte böyle böyle google kendi veritabanını ve yapay zekasını geliştiriyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# NTFS long file names problem

NTFS, 255 Unicode karakter kabul ediyor. fakat eski dosya sistemleri etmiyor. bunun önüne geçmek için güncel ms-windows işletim sistemleri her dosya için 2 farklı dosya isim tutuyor. örneğin;

> Microsoft.txt
> MICROS~1.TXT

eski dosya sistemleri hem daha az karakterlerleri olmak zorunda, hemde büyük harf olmak zorunda gibi farklı kombinasyon kuralları içerebiliyor...

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# annotation vs xml (or any other format like json)

advantages of annotations:

- xml değiştirmek/okumak java koduna göre daha zordur (jpa da her entitity yi xml'de tanımladığınızı düşünün)

- bir sınıf hakkındaki tüm annotationlar (meta bilgiler) sınıfın içindedir.

- sınıf ismi değiştiğinde xml değiştirmek gerekmez

Advantages of xml files:

- annotation kulanımışsa; bazen hangi sınıfın görevini bilmiyorsak; onu tek tek dosyalarda arama yaparak anotasyonlarını bulmamız gerekir. bazen IDE'ler kolaylık sağlayabilir bu konuda. fakat xml'lerde tüm sistemi birkaç dosyada görebiliriz (bazen geçerli olan bir avantaj/durum).

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# data binding

bir değeri bir objeye atama işleminin adı binding'tir. iki türlü binding vardır:

- one way binding

  bir degeri js tarafında modelde tutalım. bu degeri ekranda bir input'a yazdırdık. kullanıcı bu inputu değiştirdiğinde otomatik olarak model'deki değer değişmez. aradaki senkronizasyonu proramcı yapmak zorunda kalır. input değiştiğinde, tetiklenecek change metodunda programcı model'i değiştirmelidir.

- two way binding

  burada senkronizasyonu MVC kütüphanesinini kendisi yapar. örneğin; angular.js'te two way binding vardır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Electron

nodejs ve chromium altyapısı ile cross platform uygulama geliştirmeye yarıyor. "Atom text editor", "visual studio code" bu altyapıyı kullanıyor. İlk olarak Atom text editor için geliştirilmiş, daha sonra herkes kullanmaya başlamıştır. bu sebeple eski ismi: "Atom Shell"dir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# eclipse IDE

Eclipse altyapısı ile birçok OSGI tabanlı uygulamalar oluşturulabilir. Bu uygulamalara "eclipse application (or eclipse software)" deniliyor. Bu uygulamalardan bir tanesi Eclipse IDE ‘dir.

Eclipse IDE kendi içinde  versiyonlar ile dağıtılıyor: Java, JavaEE, Android gibi. Bunlara "paket veya product" adı veriliyor.

Her paket kendi içerisinde farklı plug-in'lerden oluşuyor.

Birçok plug-in toplanılarak, "feature" olarak gruplandırılıyor. Son kullanıcı feature silip ekleyebiliyor. Feature başka featurelere depend edebiliyor.

extension çok teknik seviyede kullanılan bir terim. extension; eclipse eklenti geliştiricileri tarafından sunulan her objenin/kaynağın (functionality, help content gibi...) ismidir.

- "eclipse java" paketinde yüklü gelen feature'ler:

  - "Maven Integration for Eclipse" (or M2Eclipse or m2e)

  - "Mylyn" - Jira gibi sistemlerden kullanıcıya taskı gösteren eklenti.

  - "Eclipse Web Tools Platform" paketinden sadece XML editor ve tool'ları

  - "Egit" - git integration. egit based on jgit (git java implementation)

  - "code recommenders"

  - gradle (feature ismi bilinmiyor)

- "eclipse javaee" içerisinde gelenler:

  - "eclipse java" versiyonu ile gelenler + aşağıdaki liste:

  - "Data Tools Platform" - Database management plugin.

  - "Java EE Developer Tools"

  - "Eclipse Web Tools Platform" (or WTP)

  - Plug-in Development Environment: sadece eclipse paketi geliştirmek için gerekli altyapı.


Marketten indirebilenler:

WindowBuilder: GUI creator. pro version is exist.

# MyEclipse
eclipse IDE'den türetilmiş bir IDE.

# project facet
facet: façeta (elmasın yontulmuş yüzlerinden her biri).

facet Eclipse'in sunduğu bir özelliktir. pojeye'nin property'lerini açtığımızda, birçok teknoloji ismi listelenir. hangilerini seçersek  proje için o teknolojilere özgü özellikler otomatik devreye girmektedir.

Örnek: ear facet'i devreye alındığında projenin claspath'ine otomatik olarak deployment descriptor eklenmektedir.

Bazı facet'ler biribirine depend ederken, bazıları ise aynı anda aktif edilememektedir.

IntelliJ'de "Add framework support" menüsünde facet ekleme vardır. aslında bakıldığında birçok IDE'de facet terimi olarak geçmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# nohup

posix için komut satırı yazılımı. aldığı parametreleri komut olarak arkaplanda çalıştırtır. böylece komut satırı kapatıldığında uygulama çalışmaya devam eder. nohup'a alternatfi yazılımlar da mevcuttur. ms-windows için "start" komutu aynı görevi görür.

# nohup vs disown vs &

  Aşağıdaki 3 örnekte 'commandX' yeni processe atanır ve shell yeni komut alacak şekilde kendini ayarlar.

  aşağıdaki her işlemde de commandX'e sterr, stdin gibi streamler bağlanır.

| command usage                    | standart input (stdin)                      | standard output (stdout) and standard error (stderr)                       | shell her prosesi hafızasında | SIGHUP sinyalini               |
|----------------------------------|---------------------------------------------|----------------------------------------------------------------------------|-------------------------------|--------------------------------|
| commandX param1 param2 &         | program buraya data yollarsa hata alacaktır | hala terminal'e bağlıdır, bu sbeple durduk yere ekranda output görebiliriz | process hafızada tutuluyor    | proces'e yollar                |
| commandX param1 param2 \| disown | program buraya data yollarsa hata alacaktır | program buraya data yollarsa hata alacaktır                                | process hafızadan silinir     | proces'e yollanmasını engeller |
| nohup commandX param1 param2     | kapatır ve process'e EOF sinyali gider      | redirects to nohup.out                                                     | process hafızada tutuluyor    | proces'e yollanmasını engeller |

shell'e bağlı job'ların listesini 'job' komutu ile listeyebiliriz.

  Bazen programlar disown yada nohup'la başlatmamıza rağmen shell kapandığında process'te kapanır. bunun sebepleri:

  - shell user session'ına bağlanmıştır. shell kapatılınca logout olur ve process kapanır.

  - shell kapandığında stin, stdout gibi streamler null olduğundan nullpointer bigi hatalar alan program hata fırlatarak beklenmedik durum gereği kapanır. bu sebeple bazıları stout'u > file.txt gibi bir dosyaya yönlendirmemizi önerir.

# posix sinyalleri

Özel bir IPC event'idir. posix standartları altında tanımlanmıştır. çalışan processlere veya bir thread'e özel birçok çeşit sinyal gönderilebilir. bu sinyaller 64 tanedir. C'de signal.h içerisinde de tanımlıdırlar. Bazı sinyaller:

- SIGINT - 2 numaralı sinyal - komut satırında Ctrl+C tuşu aynı görevi işler. Bu yazılımcı tarafından handle edildiğinde gözardı edilebilir. yani program kapanmak zorunda değil.

- SIGKILL - 9 numaralı sinyal - Uygulamayı yazılımcı handle edemeden kapatır. Core dump dosyasını saklar.

- SIGSTOP - 18 numaralı sinyal - komut satırında Ctrl+Z tuşu aynı görevi işler - uygulamayı pause eder.

- SIGCONT - 19 numaralı sinyal - uygulamayı pause durumundan resume ile devam ettirir.

Bazı sinyaller piyasada kullanılmakta fakat POSIX standratlarında belirtilmemiştir.

Diğer sinyaller:

kaynak: (source-id: 65)

```c
#define	SIGHUP 1	/* hangup */
#define	SIGINT	2	/* interrupt */
#define	SIGQUIT	3	/* quit */
#define	SIGILL	4	/* illegal instruction (not reset when caught) */
#ifndef _POSIX_SOURCE
#define	SIGTRAP	5	/* trace trap (not reset when caught) */
#endif
#define	SIGABRT	6	/* abort() */
#ifndef _POSIX_SOURCE
#define	SIGIOT	SIGABRT	/* compatibility */
#define	SIGEMT	7	/* EMT instruction */
#endif
#define	SIGFPE	8	/* floating point exception */
#define	SIGKILL	9	/* kill (cannot be caught or ignored) */
#ifndef _POSIX_SOURCE
#define	SIGBUS	10	/* bus error */
#endif
#define	SIGSEGV	11	/* segmentation violation */
#ifndef _POSIX_SOURCE
#define	SIGSYS	12	/* bad argument to system call */
#endif
#define	SIGPIPE	13	/* write on a pipe with no one to read it */
#define	SIGALRM	14	/* alarm clock */
#define	SIGTERM	15	/* software termination signal from kill */
#ifndef _POSIX_SOURCE
#define	SIGURG	16	/* urgent condition on IO channel */
#endif
#define	SIGSTOP	17	/* sendable stop signal not from tty */
#define	SIGTSTP	18	/* stop signal from tty */
#define	SIGCONT	19	/* continue a stopped process */
#define	SIGCHLD	20	/* to parent on child stop or exit */
#define	SIGTTIN	21	/* to readers pgrp upon background tty read */
#define	SIGTTOU	22	/* like TTIN for output if (tp->t_local&LTOSTOP) */
#ifndef _POSIX_SOURCE
#define	SIGIO	23	/* input/output possible signal */
#define	SIGXCPU	24	/* exceeded CPU time limit */
#define	SIGXFSZ	25	/* exceeded file size limit */
#define	SIGVTALRM 26	/* virtual time alarm */
#define	SIGPROF	27	/* profiling time alarm */
#define SIGWINCH 28	/* window size changes */
#define SIGINFO	29	/* information request */
#endif
#define SIGUSR1 30	/* user defined signal 1 */
#define SIGUSR2 31	/* user defined signal 2 */
```

Yazılımcı kod içerisinde bir listener aracılığı ile bu sinyalleri handle etmesi gerekir. C üzerinden örneklersek:

```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <signal.h>

void sighandler(int);

int main () {

   //signal.h'taki bir fonksiyondur.
   //ilk parametresi: hangi sinyal için handle çalıştırılsın
   //ikinci paraetresi: handler fonksiyonumuz
   signal(SIGINT, sighandler);

   while(1) {
      printf("sleep for a second...\n");
      sleep(1); 
   }
   return(0);
}

void sighandler(int signum) {
   printf("Caught signal %d, coming out...\n", signum);
   exit(1);
}
```

Sinyaller processimize iletildiğinde, process thread'i beklemeye alınır ve handler'ımız execute edilir. handler bittiğinde main process devam eder. 

bir handler çalışırken, başka bir sinyal daha gelirse, önce ilk handler tamamlanır, sonra diğer handler için tekrar aynı handler devreye girer. 2inci handler bittiğinde main fonksiyonu çalışmaya devam eder. aşağıdaki kod ile bunun testini otuput kısmını inceleyerek görebiliriz. CTRL+C ile çalışan uygulamaya sinyal gönderildiğinde, uygulamanın çıktısı değişmektedir.

```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <signal.h>

void sighandler(int);

int main () {
   signal(SIGINT, sighandler);
   int mainLoopId = 0;
   while(1) {
      mainLoopId++;
      printf("main sleep -- mainLoopId=%d\n", mainLoopId);
      sleep(1); 
   }
   return(0);
}

int signalHandlerId = 0;

void sighandler(int signum) {
   signalHandlerId++;
   int loopId = 0;
   while(loopId<5) {
      printf("handler sleep -- signalHandlerId=%d loop=%d \n", signalHandlerId, loopId);
      sleep(1);
      loopId++;
   }
}
```

## Kimler ve hangi durumlarda sinyal alınıp/yollanabilir

- İşletim sitemi arkaplanda bu sinyalleri yazılımlara yollayabilir. örnek:
  - son kullanıcı işletim sistemini kapatmak için event açsın. bu durumda işletim sistemi uygulamaların tümüne kapanmaları için özel bir sinyal gönderir.

- Yeterli yetkisi olan son kullanıcı bir process'e sinyaller gönderebilir. örnek:
  - kill, signal komut satırı uygulamaları ile process-id'sini parametre olarak geçtiğimiz process'e, istediğimiz sinyali gönderebiliriz.

- yazılımcı kod içerisinden sinyal yollayabilir. örnek:
  - C'de; signal.h içindeki __int raise(int sig)__ fonksiyonu ile kendi işlemimize sinyal gönderebiliriz.
  - C'de; __int kill( pid_t pid, int sig )__ ile diğer process'lere sinyal gönderebiliriz.

# exit status (or exit code)

program kapandığında bir sinyal döner. bu sinyale verilen addır. bir sayıdır.

- 0 başarılı bittiği anlamına gelir.

- pozitif sayılar daha çok yazılımcı tarafından yakalanmış/yönetilmiş hatalardır.

- negatif sayılar yazılımcının yakalamadığı/yakalayamadığı durumlarda döndürülür.

java'da; System.exit(int status) metodu ile statü dönülerek işlem sonlandırılır.

Bazı exit statüsler standarttır. örneğin bazı status'ler POSIX standartlarında belirtilmiştir. örnek:

code - açıklama

1 - programatic error example: 1/0 divide zero

2 - binary file format exmaple: missing keyword. for example calling a funciton which is not on classpath 

126 - Command invoked cannot execute. example: file is not executable

127 - command not found to execute

128 - exit code integer değilse o zaman bu hatayı verir.

130 - Script terminated by Control-C

?(sağ tarafı oku) - exit code integer fakat 0-255 arası değilse; işletim sistemi yazılımcının girdiği değeri yazilimci_exit_code%255 yapar ve bunu döndürür.

Yukarıdaki pozitif değerler yazılımcı tarafından fırlatılabilir. fakat bu hiç önerilmez. best practice değildir.

c ve c++ dillerinde standart kütüphanelerinin (sysexits.h) içinde asagidaki degerler vardır. fakat bunlar işletim sisteminin yada başka programlama dillerinin ve hatta diğer c kütüphanelerinin resmi olarak tanıdığı standartlar değildirler.

opensource.apple.com/source/Libc/Libc-320/include/sysexits.h dosyasının içeriği aşağıdadır:

```c++
#ifndef	_SYSEXITS_H_
#define	_SYSEXITS_H_

/*
 *  SYSEXITS.H -- Exit status codes for system programs.
 *
 *	This include file attempts to categorize possible error
 *	exit statuses for system programs, notably delivermail
 *	and the Berkeley network.
 *
 *	Error numbers begin at EX__BASE to reduce the possibility of
 *	clashing with other exit statuses that random programs may
 *	already return.  The meaning of the codes is approximately
 *	as follows:
 *
 *	EX_USAGE -- The command was used incorrectly, e.g., with
 *		the wrong number of arguments, a bad flag, a bad
 *		syntax in a parameter, or whatever.
 *	EX_DATAERR -- The input data was incorrect in some way.
 *		This should only be used for user's data & not
 *		system files.
 *	EX_NOINPUT -- An input file (not a system file) did not
 *		exist or was not readable.  This could also include
 *		errors like "No message" to a mailer (if it cared
 *		to catch it).
 *	EX_NOUSER -- The user specified did not exist.  This might
 *		be used for mail addresses or remote logins.
 *	EX_NOHOST -- The host specified did not exist.  This is used
 *		in mail addresses or network requests.
 *	EX_UNAVAILABLE -- A service is unavailable.  This can occur
 *		if a support program or file does not exist.  This
 *		can also be used as a catchall message when something
 *		you wanted to do doesn't work, but you don't know
 *		why.
 *	EX_SOFTWARE -- An internal software error has been detected.
 *		This should be limited to non-operating system related
 *		errors as possible.
 *	EX_OSERR -- An operating system error has been detected.
 *		This is intended to be used for such things as "cannot
 *		fork", "cannot create pipe", or the like.  It includes
 *		things like getuid returning a user that does not
 *		exist in the passwd file.
 *	EX_OSFILE -- Some system file (e.g., /etc/passwd, /etc/utmp,
 *		etc.) does not exist, cannot be opened, or has some
 *		sort of error (e.g., syntax error).
 *	EX_CANTCREAT -- A (user specified) output file cannot be
 *		created.
 *	EX_IOERR -- An error occurred while doing I/O on some file.
 *	EX_TEMPFAIL -- temporary failure, indicating something that
 *		is not really an error.  In sendmail, this means
 *		that a mailer (e.g.) could not create a connection,
 *		and the request should be reattempted later.
 *	EX_PROTOCOL -- the remote system returned something that
 *		was "not possible" during a protocol exchange.
 *	EX_NOPERM -- You did not have sufficient permission to
 *		perform the operation.  This is not intended for
 *		file system problems, which should use NOINPUT or
 *		CANTCREAT, but rather for higher level permissions.
 */

#define EX_OK		0	/* successful termination */

#define EX__BASE	64	/* base value for error messages */

#define EX_USAGE	64	/* command line usage error */
#define EX_DATAERR	65	/* data format error */
#define EX_NOINPUT	66	/* cannot open input */
#define EX_NOUSER	67	/* addressee unknown */
#define EX_NOHOST	68	/* host name unknown */
#define EX_UNAVAILABLE	69	/* service unavailable */
#define EX_SOFTWARE	70	/* internal software error */
#define EX_OSERR	71	/* system error (e.g., can't fork) */
#define EX_OSFILE	72	/* critical OS file missing */
#define EX_CANTCREAT	73	/* can't create (user) output file */
#define EX_IOERR	74	/* input/output error */
#define EX_TEMPFAIL	75	/* temp failure; user is invited to retry */
#define EX_PROTOCOL	76	/* remote error in protocol */
#define EX_NOPERM	77	/* permission denied */
#define EX_CONFIG	78	/* configuration error */

#define EX__MAX	78	/* maximum listed value */

#endif /* !_SYSEXITS_H_ */
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# command line argumant passing types:

- POSIX like
  > myapp -myParam1 myValue1

- GNU like
  > myapp --my-param1 --my-param2=myValue2

- Java like

  Bu genelde D ve X olarak parameteleri gruplandırmak için yapılmaktadır.
  > myapp -Dmy.param1=myvalue1 -XmyParam1myValue1

- (no name for this)

  java-like gibi property1 ve property2 altında gruplayabilmek için kullanılır.
  > myapp --property1 myparam1=myvalue1 myparam2=myvalue2 --property2 myparam3=myvalue3
  

- (no name for this)

  tar -x -z -f myfile.tar.gz ile aynı olabilir. bu uygulamadan uygulama değişir.
  > tar -xzf myfile.tar.gz

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Test Double

stub, fake, dummy, mock gibi test için kullanılan datalara verilen genel bir terimdir.

# stub metod

bir metod daha yazılmamış ise (implemente edilmemiş ise) fakat başka yerlerden çağrılması gerekiyor ise metodun imzası hazırlanır fakat içinden null yada geçici bir değer dönülür. bu şekilde bu metodu kullanan diğer kodların geliştirmesi durmamış olur. böyle durumlarda bu metoda stub adı verilir.

# stub class

içinde stub metodları bulunan sınıftır.

# dummy data

genelde saece parametre yollamak(doldurmak) için kullanılan datalardır.

# mock data

bir yere yollandığında cevap olarak bir beklentimizin olduğu datalardır.

# fake data

asıl testimiz dışındaki kaynaklar için kullandığımız test datalarıdır. örneğin uygulamanın db'si ayağa kalkmazsa uygulama rest isteği hiç yapamaz. rest isteğini tets etmke istiyoruz. bu durumda database'yi fake yapabiliriz. database yerine memory'de tututal bir liste yapabiliriz. işte bu liste fake data oluyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# ribbon

microsoft office 2007 ile birlikte getirdiği toolbar türevidir (componenet'tir). daha önce farklı yerlerde tabbed-toolbar mantığı kullanılmıştır. bu sebeple lisans problemleri yaşanmaktadır. Mirosofot aynı zamanda bu component'e "Fluent UI" adını da vermiştir.

# Metro UI

microsoft'un geliştirdiği arayüz standardıdır. Marka sorunları sebebi ile yeni isimleri mevcuttur: "Microsoft tasarım dili" yada "Modern UI". Windows 8 ile gelen yeni başlat menüsü tuşu ile açılan sayfada Metro UI kullanılmıştır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Büyüklük/ölçü birimleri

# px (or dot or pixel or Gözek or picture element or eng:pel)
Görüntüdeki en ufak birimdir. Cihazdan cihaza boyutu değişir.

# sub-pixel
bu fiziksel bir kavramdır. tek bir pixeli oluşturmak için fiziksel olarak ihtiyaç duyulan birimlerdir. fakat yine en ufak görüntü birimi pixel kabul edilir. çünkü tek bir görüntü noktası (tek renk) olan en ufak birim pixel'dir.

# megapixel
1 milyon pxel'e sahip görüntüye denir. en*boy sonucu 1 milyon olan görüntüye denir. en boy oranı hakkında bilgi vermez. çubuk gibi de olabilir.

# Frame Rate
birimi __fps (or frame per second)__'dir. her saniye kaç görüntünün yansıtıldığı sayısıdır. ne kadar yüksekse o kadar görüntü daha akıcı olur.

fps değeri yükseldikçe, cihazda pixel değerini arttırmak fiziksel olarak çok fazla maliyetli olmaktadır. Aynı şekilde pixel dfeğeri yükseldikçe fps'yi arttırmak fiziksel olarak çok maliyetli oluyor.

__Refresh Rate__ cihazın her saniye kaç görüntü gösterebileceğidir. Birimi __Hz (or hertz)__'dir.

# notasyonlar
medya dosyalarında en ve boy oranları çoğu zaman orantılı olacağından notasyonlarda buna göre daha kısa yazılmaktadır. örneğin; 

- __1080p60__ --> 1920x1080 pixels, 60 fps anlamına gelir. 1920 notasyonda yazılmaz. çünkü piyasadaki şoğu cihazlar bu oranda medya dosyası hazırlamaktadır. Youtube gibi son kullanıcıya görüntü veren sitelerde bu tarz kısaltmalar kullanılırken daha akademik/endüstri standartlarında bu şekilde kısa kullanım önerilmez.

- __720p60__ --> 1280x720 pixels, 60 fps anlamına gelir.

- __720p__ --> 1280x720 pixels anlamına gelir. fps değerinden bahsedilmez.

# full HD
| name                           |  pixel notation  | resolution | approximately pixel | additional note | 
| -------------------------------| -----------------|------------|--------------------|-----------------|
| __Standard Definition (or SD)__ | 480p            |            |                   |                 |
| __HD (or high definition)__     | 720p            | 1,280 x 720 |  1 million    |                |
| __Full HD (or FHD)__           |  1080p          | 1,920 x 1,080 | 2 million | 2K - Blu-Ray standardı altındadır. |
| __Ultra HD (or UHD)__           |                | 3,840 x 2,160 | 8 million | 4K   |

# Inch (or inç or in)

çift tırnak işareti ile simgelenmektedir. 2,54 cm'e denk gelmektedir.

# PPI (or pixer per inch)

dpi ile benzer bir kavramdır.

# dpi (or dot per inch)

ppi'a benzerdir. ppi pixel bazında olduğu için her grafik çıktısı bu terimi kullanamaz. örneğin; ppi'ı sadece monitörler/ekranlar kullanır. printer çıktısında ppi'dan bahsedilemez. bu sebeple dpi terimine ihtiyaç vardır.

örneğin bir görüntü oluşturudğumuzda (photoshop ile) birimler dpi olabilir. dpi ile oluşturulan görnütüs o anda uygun olan pixel boyutuna çevrilecektir. fakat  cihazda  görünebilecektir. print etitğimizde  görünebilecektir. örnek belki photoshop, 1 dot = 1 pixel yapar, yada 1 dot 4 pixel yaparak ekranda gösteriyordur. işte burada o cihazın/yazılımın "dp" değeri önemlidir.

# dp (or dip or density (yoğunluk) independent pixels)

Standartlara göre değişen bir birimdir. örneğin; android'lerde 160dpi bir ekranda; 1dp = 1px'tir. 160 sayısı burada anroid standartıdır.  320dpi bir ekranda ise; 1dp 2 piksele eşit olacaktır.

# International System of Units (or SI)

üslerin pozitif olduğu değeler:

```
deca  hecto  kilo  mega  giga  tera   peta   exa    zetta  yotta

da    h      k     M     G     T      P      E      Z      Y

10^1  10^2   10^3  10^6  10^9  10^12  10^15  10^18  10^21  10^24
```

üslerin eksi olduğu değerler:

```
deci  centi  milli  micro  nano  pico   femto  atto   zepto   yocto

d     c      m      μ      n     p      f      a      z       y

10^1  10^2   10^3   10^6   10^9  10^12  10^15  10^18  10^21   10^24
```

Birçok teknik farklı kavramlar için ek birimler türetilmiştir. örnek:

Frekans birimi; hertz (or abb:Hz). s^−1 (saniyede salınım)

# uzunluk tanımı

Uzunluk hesaplamalarında metre referans olarak alınmaktadır.

1 metre, ışığın boşlukta 1/299.792.458 saniyede aldığı yol olarak tanımlanmıştır. 

# ağırlık tanımı

ağırlık hesaplamalarında gram referans olarak alınmaktadır.

Uluslararası kuruluşlarca Paris'teki Milletlerarası Ağırlıklar ve Ölçüler Bürosu'nda bulunan iridyum platinden yapılmış silindir şeklindeki cisim 1kg olarak kabul edilir.

Paristeki referansa en yakın tanım: gram, +4°C de 1 cm3 saf suyun kütlesidir.

Ağırlığı referans almak için piyasada şu yol izlenmektedir: dünyanın en yuvarlak nesnesi olan ve 2,15 x 10^25 adet silikon 28 atomuna sahip mükemmel küre şeklindeki bir cisim çok yüksek maliyetlere üretildi ve kopyalandı. kopyası dünyanın her tarafına dağıtıldı. herkes bu referansa göre ağırlığı tanımlıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# process states

- Created: yeni oluşturulmuş, fakat process hala tam olarak RAM'e alınmamıştır.

- Ready: CPU ya girmek için bekliyor.

- Running: CPUda işlem görüyor. Kernel mode ve User mode olarak çalışırlar. "User mode" kernel instructions'ları çağıramaz.

- Blocked: CPU ya girsede bir işe yaramayacak durumdadır, çünkü dış donanımlardan (kaynaklardan) cevap bekleniyordur.

- Terminated: işi bitmiş process. parent process "exit status"'u okumadığı için henüz , process bu statüde bekler. bu şekilde çok process olabileceğinden bunlara "zombie process" denir.

işletim sistemlerinin ek olarak birçok farklı statüleri olabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# concurrent (eş zamanlı) vs paralel

bu iki kavram sürekli birbirinin aynısı gibi bilinir. fakat ufak bir fark var: paralel çalışan işlemler, birden fazla cpu ile olmalıdır. yani 2 paralel thread var ise, en az 2 cpu olmalıdır. 2 işlem ancak bu şekilde paralel yürütülebilir. ancak concurrent işlemler; paralel olmak zorunda diillerdir. 2 farklı işlem birbirinden bağımsız yürür. aynı cpu'ya ikişer saniye aralıklarla girerlerse yine concurrent çalıştıkları anlamına gelir. kısaca; concurrent, birden fazla birbirindenbağımsız işlem olduğu; paralel ile zamanlama açısından ikisinin aynı anda işletileceğini belirtir.

# işlemci sayısı ve thread sayısı ilişkisi

- gerçekte bir bilgisayar tek thread çalıştırabilir. bir bilgisyarın cpu'su 2 işlemcili ise 2 thread aynı anda çalıştırabilir. yani 2 işlemi pararlel yapabilir. 

- standart bir pc'de işletim sistemleri binlerce thread aynı anda açık tutar. bu thread'lerin hepsi sanaldır. aslında her biri teker teker (daha doğrusu cpu sayımız kadarı) cpu'ya girerler. fakat işletim sistemi, üzerinde çalışan yazılımlar durmasın/hata vermesin diye onlara thread açar fakat beklemeye alır.

# fiber
kelime anlamı: lif

bir process birden fazla thread'e ayrılabilir. aslında thread'ler yönetim biçimlerine göre 2 ye ayrılır: fiber ve thread.

CPU bir thread'i herhangi bir anda interrupt edip, diğer thread ile işleme devam edebilir. Bu data-integrity için problem olabilir. Tabi burada multi-core cpu'nun avantajlarını yaşamış oluruz.

Oysa fiber'ler interrupt edilemezler. Daha doğrusu öngörüldüğünde (belli bir birimlik işi bitirdiğinde) interrupt edilirler.

Not: Her OS mutlaka thread'leri yukarıda yazıldığı gibi yönetecek diye bir kaide yok. Fakat genelde bu şekilde yönetir. Bu sebeple; fiber'ler user-seviyesinde manage edilirler. Genelde framework/kütüphane aracılığı ile yapılırlar. Bu sebeple genelde; fiber'lerden OS'un haberi yoktur.

thread'ler; __preemptive scheduling (or preemptive multitasking)__'e dayanır (preemptive kelime anlamı: öncelikli). Oysa fiber'ler; __cooperative scheduling (or non-preemptive multitasking or non-preemptive scheduling)__'e dayanır.

Terim anlamlarını incelersek; "scheduler"; taskları yöneten (başlatan, durduran...) sistemdir.

# cpu core

bir cpu içinde birden fazla çekirdeğe (core'a) sahip olabilir:

- Dual core --> 2 çekirdekli
- Quad Core --> 4 çekirdekli

# cpu socket (or cpu yuvası or cpu slot)

- isminden de anlaşıldığı gibi; anakart üzerinde bulunan, cpu'nun takılması için tasarlanmış fiziksel giriştir.

- bir anakartta birden fazla cpu slotu olabilir.

# Hyper-threading

cpu teknolojisi ismidir. bu teknoloji ile gerçekte x çekirdekli onlar bir sunucu daha fazla çekirdekliymiş gibi işletim sistemine gösteriliyor. yani bir nevi sanal cpu çekirdeği yaratılıyor. bu şekilde eğer çalıştırılan yazılımlar çok çekirdekli teknolojiye göre yazılmışlar ise; bir nebze kara geçilebiliyor. Çok basit anlamada; cpu'nun boşta kalabileceği sürelerde diğer thread'ler devreye gireceği için performans avantajı olduğu düşünülür.

gerçekte 4 core'umuz olsun. her core, 2 core gibi davransın. bu durumda işletim sistemi 8 adet "logical processor" olduğunu algılayacaktır.

# Virtual Processor vs logical processor

ikiside aynı anlamdadır. fakat Virtual sanallaştırma yaparken, sanal olacak işletim sistemine atadığımız cpu core sayısını belirtmek için kullanılıyor.

# intel vt-x vs amd-v

intel ve amd'nin donanım sanallaştırması için kullandığı teknolojlerin isimleri. bir donanımı sanal olan makinalara bölüştürmek için yazılımsal olarakta sanallaştırma yapılabiliyor, fakat donanım desteği olunca daha hızlı ve güvenlidir.

# intel CPU isimlendirme
her grubun alt modellerinin isimlendirmeleri ayrı formattadır.

- core
  - 5th generation
    - i3
      - farklı core sayıları
      - farklı cache
      - Processor Base Frequency
      - farklı gömülü grafik işlemcisi
      - ...
    - i5
    - i7
  - 6th generation
    - i3
    - i5
    - ...
  - 7th generation
    - i3
    - i5
    - ...
- Xeon
  - ...
- atom
- pentium
- xeon phi
- quark SoC
- celeron
- Itanium

## nitelik belirteçleri
U, Y, T, Q, H, G, K gibi keyword'ler içerebilir. Bunlar:

- U: Ultra Low Power. The U rating is only for laptop processors. These draw less power and are better for the battery.
- Y: Low Power. Typically found on older generation laptop and mobile processors.
- T: Power Optimized for desktop processors.
- Q: Quad-Core. The Q rating is only for processors with four physical cores.
- H: High-Performance Graphics. The chipset has one of Intel’s better graphics units in it.
- G: Includes Discrete Graphics. Typically found on laptops, this means there is a dedicated GPU with the processor.
- K: Unlocked. This means you can overclock the processor above its rating.

## örnek bir ürün
örnek product name: Intel Core i7-5950HQ Processor
- "quad core" gibi bir isimlendirme içermese de, 4 çekirdeklidir.
- cache değeri isminde yazmıyor. bu detaya intel'in resmi sitesinden bakmak gerekli.
- 5th Generation modeli. fakat bu da isminde yazmıyor.
- H ve Q nun ne olduğu yukarıda belirtildi.
- 5950 sadece özel modelin isimlendirmesi. Aynı numaraya sahip başka Generation veya i3, i7 gibi gruplardan bir ürün yok. fakat bu numara ile aynı olup farklı özelliklere sahip olan cpu'lar üretiliyor. ilk baştaki "5", 5th generation olduğunu temsil ediyor. Bu durumda sadece "core" grubundakiler için geçerli. 

## tüm liste ve diğer detaylar
Buradan tüm cpu seçimi yapılabilir ve her CPU'nun tüm detayları incelenebilir: (source-id: 66)

Buradan tüm cpu'lar tek sayfada listenmiştir: (source-id: 67)

Burada her grup için nasıl bir isimlendirme standardı kullanıldığı ve nitelik belirteçleri yazmaktadır: (source-id: 68)

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# wrapper sınfıları

tüm programlama dilleri için ortak bir kavramdır. bazen bazı değerlerin (nesnelerin) bir sınıfın içinde bulunmasını isteyebiliriz. bunun birçok sebebi olabilir. örneğin; javadaki collections'lar primitive değerler alamazlar. fakat elimizdeki primitive değerleri bir listede toplamak istiyoruz. böyle olunca bu değerleri geçici bir sınıfa atarız, ve bu sınıflardan oluşan bir collection yaratırız.

```java
Integer box = new Integer (x); // boxing

int y = box.intValue(); // unboxing
```

wrapper sınıfları bazen "holder" sınıfları olarakta geçmektedir.

__Autoboxing__ compiler'ın bizim için otomatik wrapper sınıfına atama yapmasıdır. örnek:

```java
Character ch = 'a';
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# liferay
Liferay, bir portal platformudur ve Ücretsiz (Community Edition) ve Ücretli (Enterprise Edition) olmak üzere iki şekilde sunulmaktadır.
liferay java'da yazılmıştır. OSGI kullanarak modüler bir yapıdadır.
liferay bir content management system (cms - içerik yönetim sistemi , joomla, drupal, WordPress gibi ) 'dır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# QA (or Quality Assurance or kalite güvencesi)

teknik insanlardan oluşan bir ekibin test ettiği platformdur.

# UAT (or User acceptance Testing)

müşterinin (veya ürününü kullanacak olan kişilerin) test ettiği platformdur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# profiling

bu terim yazılım geliştirme dünyasında, çalışan uygulamayı runtime sırasında monitör etmek (bellek, cpu kullanımı gibi parametreleri) anlamında kullanılmaktadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Telemetri (or Uzölçüm or Telemetry)
bir sistem ya da tesisin uzaktan kablo veya kablosuz olarak izlenmesi veya kontrol edilmesidir.

# tele
Yunanca "tele" (uzak, ırak) anlamına gelmektedir. bu kelime birçok bilişim kelimesi için ön ek olarak kullanılmaktadır. örnek: telecommunication, telegraf, telephone, television...

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Macromedia
Adobe tarafından satın alınan şirket.

# Adobe photoshop
fixed size grafikler için kullanılan uygulama. Vektör grafik çizilemez.

# Adobe illustrator vs Inkspace
Vektör grafik'ler çizim için tasarlanmış birbirine alternatif uygulamalar.

# Adobe Fireworks
hem bitmap hemde vektörel grafik tasarlamak için geliştirilmiş yazılım. sadece web teknolojileri/uygulama temeası geliştirme gibi işler için tasarlanmıştır. bu sebeple photoshop yada illustrator gibi gelişmiş değildir. daha basit basit ve hızlıdır.

# Adobe AIR
masaüstü için web teknolojileri ile uygulama yazmaya yarayan altyapı. air ile yazılmış uygulamayı run etmek için bilgisyarda "AIR Runtime" yüklü olmalıdır.

# Adobe Shockwave Player
Adobe Director tarafından geliştirilen uygulamalarını oynatan playerdır. web tarayıcısına eklentidir. "Flash Player"'dan tamamen bağımsız ve ona alternatif bir teknolojidir. flash temelde video oynatmak için tasarlanmıştır. oysa "Shockwave Player" web uygulaması geliştirmek için tasarlanmıştır.

# Macromedia Flash Player (or yeni adı: Adobe Flash Player)
Macromedia'nın geliştirdiği dönemlerde ismi "Shockwave Flash Player"'dı.

# Adobe Flex (or yeni adı: Apache flex)
flash uygulaması geliştirmeye yarayan framework.

# Adobe Dreamweaver
web sayfası tasarlamak için geliştirilmiş IDE'dir. HTML, CSS gibi web dilleri ile önyüz geliştirmek için tasarlanmıştır.

# 3ds Max (or old-name:3D Studio or old-name:3D Studio Max)
Autodesk firması tarafından geliştirilen 3d ve 2d grafik geliştirme yazılımı.

# AutoCAD
Autodesk firması tarafından geliştirilen teknik resim çizme yazılımıdır.

# teknik resim
Teknik resim, bir şeyin nasıl çalıştığını veya üretildiğini anlamak üzere yapılan çizim. mühendislik gibi alanlarda özellikle tercih edilir.

# Bilgisayar Destekli Tasarım (or CAD or Computer-Aided Design)
digital ortamdan yararlanılarak yapılan teknik resim çizimidir

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# null vs nil
temelde aynı manaya gelselerde bazı programlama dillerinde çok ince farklılıkları olabiliyor.

bazı proramlama dillerinde Nil ve nil dahi birbirinden farklı da olabiliyor. büyük harfle başlayan "Nil" obje hali oluyor.

"nil" kelime anlamı: hiçbir şey, boş
"null" kelime anlamı: değersiz
"void" kelime anlamı: geçersiz

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# GUI design patterns
Burada çok sade şekilde açıklanmış: (source-id: 69)

# responsive
ekran küçülüp büyüdükçe tüm nesneler kendi içinde sürekli büyür veya küçülür. belli boyutlarda değişmesi beklenmez. her cihaza uyumludur, çünkü aynı tasarım tüm kalıplara uyacak şekilde tasarlanmıştır. ekrana sığmaya çalışır. ekranın boyutu, uç noktalardayken (eşik değerlerinde - aşırı büyük yada aşırı ufak olduğunda) "adaptive" tasarım kullanımına geçilebilir. yani 2 dizayn birlikte kullanılabilir.

# adaptive
sayfada her nesne fix boyuttadır. pencere boyutu büyültüp küçültüldüğü zaman ekrandaki nesnelerin yeri değişmektedir. ekran boyutu farklı boyutlardayken farklı davranır. fakat responsive gibi her boyut için tekrar şekil almaz. belli boyut aralıkları için belli bir dizyna geçer. dolayısı ile cihaz gruplandırılması söz konusudur.

# static
pencere içerisinde ekrna küçülsede büyülsede nesnelerin yeri ve büyüklüğü değişmemektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Heroku

Bulut hazır işletim sistemidir. Amaç; deploymentların hızlı şekilde yapılabilmesi için platform sağlamaktadır. Kodların derlenipr otomatik olarak derlenip deploy edilmesi, dışarıya açılması, makinelerin dışardan hazır API ile yönetilebilmesi gibi birçok ihtiyacı karşılayabilmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# robots.txt

dosyaya erişim domainin url'sinin root'undan olmalıdır. bu dosyada yazan adresler arama motoroları tarafından indexlenmemektedir. fakat buna uymayan robot'lar da mevcuttur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# tr:barkod (or eng:barcode or eng:bar code or çubuk kod or çizgi im)
2 boyutlu barkodlara __matrix code (or 2D barcode or 2D code or matrix kodu or iki boyutlu barkod)__ denilmektedir.

1 veya 2 boyutlu bir resimde kare kare siyah ve beyaz noktalar mevcut. Bunların her biri birer ikiliğe (byte) denk geliyor. Bu değerler resnimden okunduğu (tarandığı) zaman, soucunda uzunca bir byte array elde ediliyor. bu artık istenilen formatta anlamlandırılıyor. bu byte-array'i anlamlandırmak için birçok standart var. bu standartlardan biri de "__QR Code (or Quick Response Code)__"'dur.

Piyasada QR Code gibi birçok alternatif mevcut. tüm bu alternatiflere genel olarak barcode adı verilir. bu alternatiflerin bazı farkları:

- bazı barkod'lar renkli, bazı barkodlar sadece siyah beyaz

- bazı barkodlar 1 boyutlu (çizgi şeklinde), bazıları 2 boyutlu (matriks şeklinde), bazıları ise farklı geometrik şekillerden okunurlar. bu tarz farklılıklara buradan bakılabilir: (source-id: 70) "Matrix (2D) barcodes" başlığı.

- byte-array'in maximum boyutu

- byte array'in okunacak formatın encoding'i.

- byte array okundupuktan sonra string'e çevriliyor fakat bu string ne anlama geliyor: örneğin:
  - calendar event
  - contact information
  - email adres
  - geo location
  - phone number
  - sms
  - text
  - url
  - wifi information (with password)
  
  burada desteklenen format tipleri kısıtlı olmaktadır.

- byte array okununca yanlış okunmuş olabilir veya barcode eski olduğundan bazı kısımları net olmayabilir (sönük vs..). bunların doğru olup olmadığını anlamak için barkod'un bir kısmı hata tespiti için hash gibi kısımlar içeriyor.

- ve daha birçok özellik standarta göre değişebiliyor

# bazı barcode çeşitleri:

| 1D product            | 1D industrial | 2D           |
|-----------------------|---------------|--------------|
| UPC-A                 | Code 39       | QR Code      |
| UPC-E                 | Code 93       | Data Matrix  |
| EAN-8                 | Code 128      | Aztec        |
| EAN-13                | Codabar       | PDF 417      |
| UPC/EAN Extension 2/5 | ITF           | MaxiCode     |
|                       |               | RSS-14       |
|                       |               | RSS-Expanded |

# ZXing ("Zebra Crossing")
açık kaynaklı java barcode okuma kütüphanesidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Unix-like'ta herşey dosya

unix tabanlı sistemlerde tüm kaynaklar dosyalama mantığı ile çalışmaktadır. bu dosyalar UNIX-like'larda "özel dosyalar" olarak adlandırılırlar. komut satırından bir dizindeki dosyaları listelediğimizde, bir dosyanın özel olup olmadığını; yetki satırındaki ilk harfinden anlayabiliriz. birden fazla dosya tipi vardır:

- regular file : dosya sistemindeki normal özelliksiz bir dosya

- dizin : dosya sistemindeki klasör/dizin

- Symbolic link (or symlink or soft link) : windowstaki kısayol

- Named pipe : Inter-process iletişimi için gerekli boru hatları dosyaları

- Socket : Inter-process iletişimi soketleri. network soketi ile karıştırılmamalıdır. bazı kaynaklarda "UNIX domain socket"'i diye de geçmektedir.

- device : driver dosyası

- Door : sadece Solaris işletim sisteminde kullanılan IPC için gerekli bir dosya

# dosya vs API

unix tabanlı olmayan sistemlerde (örnek windows) her kaynağa işletim sistemin sunduğu API'ler aracılığı ile erişilebilir. Örneğin; bir stream'e veri atarken windows'ta MyAPIClass.writeValue("new value"); diye yazılırken, Linuxta herhangi bir outputstream ile ilgili dosyaya byte veri yollamak yeterlidir.

Stream olmasının en temel yararı stream kütüphanleri her dilde varolduğundan her dilden API ihtiyacı olmadan işlemleri gerçekleştirebilmemizi sağlar.

örneğin; linuxta komut satırında "command > output.txt" komutu command'ı çalıştırır ve komut satırı çıktısını output.txt'ye aktarır. unix sistemlerde 3 özel dosya vardır. şu işlevi görür : 

- "firefox > /dev/null" çalıştırırsan çıktılar hiçbir yere aktarılmaz. her yazım işlemi sonrası EOF döndürülür.

- /dev/random sürekli okumak için tasarlanmıştırç. sürekli random sayı döndürür.

- /dev/zero sürekli okumak için tasarlanmıştır. ASCII'deki 0x00 (null) değerini döndürür.

# maximum açık dosya limiti

*nix'lerde açık dosya sayısının bir limiti vardır.

bu limit root yetkisi var ise arttırılabilir. sadece özel olarak bir process için dosya sayısı limitlenebilir, aynı şekilde sadece user yada tüm OS bazında limitler belirlenebilir.

böyle bir limitin olmasının sebebi *nix'lerde herşeyin dosya olmasıdır: soket, process herşey bir dosya. dolayısı ile bir program kendisi çok bellekten harcarsa (örneğin durmadan integer array'ler oluşturursa) memory doldu hatası alacaktır. yani bu işletim sistemini etkilemez. fakat program durmadan soket açarsa, process açarsa, OS bunlara karşılık birer dosya oluşturur. bu durumda dosya sistemi bu durumdan etkilenecektir. dosya sistemi memory'd eolmadığı için ve fiziksel olarak bilgiler diskte kaydolacağı için bu durum bilgisayarı çökertebilir. bunu engellemek amaçlı dosya sayısı limitlenmektedir.

# fork-bomb
sürekli olarak process açıp sistemi sıkıntıya sokan programlardır. sürekli dosya açılması sıkıntı yaratır.

# file descriptor (or dosya betimleyicisi)

her dosya kullanımında process içerisinde bu dosyanın adresi (programlama dilindeki obje/nesne) tutulur. bu adres file descriptor'tur. C dilinde bu bir integer'dır. Dosyalar sanal olarak  /prod/pid/fd (/prod/process-id/file-descriptor) gibi dosyalarda tutulur. örneğin; /prod/1001/48 dosyası bir doman soketine yada bir sürücüy denk geliyor olabilir. bu dosyalar gerçekten de o dizinde yaratılırlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# StackExchange
çeşitli konularda soru-cevap sitelerini bir araya getiren site ağı. StackExchange, aralarında Matematik, İstatistik, Din, Astronomi, Bilgisayar programcılığı gibi belirli konularda özelleşmiş 130'un üzerinde soru-cevap sitelerini barındırmaktadır.
- bilgisayar proramcılığı (yazılım geliştirme) ile olan site Stack Overflow'dur.
- bilgisar kavramları ile ilgili tüm soruların olduğu site: http://superuser.com/'dur.
- ubuntu hakkındaki soruların sitesi: http://askubuntu.com/
- network/sistem soruların sitesi "Server Fault"'tır.
- StackExchange ile ilgili sorular: "örnek nerede bu soruyu sorabilirim", "neden konulara cevap yazamıyorum"... meta.stackexchange.com'da soruluyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# PMP (or Project Management Professional)
bu aynı zamanda bir sertifikasyondur. proje yönetimi konusunda en yaygın kabul gören sertifika özelliğine sahiptir. bu sertifika, merkezi abd'de bulunan proje yönetimi enstitüsü (or project management institute or PMI) tarafından verilmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Cocoa vs Cocoa Touch
Cocoa Apple altyapılı ürünler için GUI ve diğer uygulamaların çalışması için kütüphane kümesidir. Cocoa Touch, kısmen Cocoa modülleri içeren ve sadece tv, saat, telefon gibi ürünler için gerekli kütüphaneleri içerir.

# CocoaPods
xcode projelerinde third party kütüphanelerin yönetimini sağlayan paket yöneticisidir. javadaki maven gibi. xcode projesi ilk açıldığında pod desteği olmaz. pod desteğini proje dizinine giderek "pod init" komutu ile veririr. daha sonra projenin içinde "podfile" isminde bir dosya oluşur. buranın için kütüphanelerimizi ekleriz. her ekleme sonrası komut satırından "pod install" komutunu çalıştırmak durumundayız.
pod yapısı, aynı xcode workspace'inin içine "Pods" isminde bir proje daha oluşturur. bu projede tüm third party kütüphaneler mevcuttur. asıl projemiz sadece pod projesine depened eder.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Breadcrumb
Bir uygulamada (web/desktop) kullanıcı bir ekrandan diğerine yönlnedirilmektedir. bazen içiçe sayfalar çok sayıda olabilmektedir. böyle durumlar için syafada nerede olduğunu gösteren ağaç-tarzı yapılara breadcrumb denilmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Kurumsal kaynak planlaması (or işletme kaynak planlaması or Enterprise Resource Planning or ERP)
işletmelerde mal ve hizmet üretimi için gereken işgücü, makine, malzeme gibi kaynakların verimli bir şekilde kullanılmasını sağlayan bütünleşik yönetim sistemlerine verilen genel addır.

ERP'nin alt modülleri:
- __CRM (or customer relationship management)__: Satış programı, Pazarlama programı, Müşteri servisleri programı, teknik destek programı gibi görevleri içeren yazılımdır.
- İnsan kaynakları modülü
- muhasebe modülü
- ...

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Standard streams

In computer programming, standard streams are preconnected input and output communication channels between a computer program and its environment when it begins execution. The three I/O connections are called standard input (stdin), standard output (stdout) and standard error (stderr). Originally I/O happened via a physically connected system console (input via keyboard, output via monitor), but standard streams abstract this. When a command is executed via an interactive shell, the streams are typically connected to the text terminal on which the shell is running, but can be changed with redirection, e.g. via a pipeline.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Luna

SafeNet firması tarafından geliştirilen, HSM (Hardware security Module)'dür. Yazılımsal API'si aracılığı ile network üzerinden aldığı bilgileri şirreleyip açabilmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# PIN pad (or PIN entry device or PED)
PIN girilen cihazlara verilen genel isimdir. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Jmeter

web servislerini test etmek (yük testi) için gerekli yazılım.

# JavaMelody

Java uygulamalarını (sunucu üzerinde olsada) runtime sırasında monitör etmek için kullanılan yazılım. java kütüphanesi olarak, incelenecek/run edilecek projenin içine eklenmelidir. Çlaışn bu kütüphane runtime sırasında bir port açıyor ve browser üzerinden istatistikleri sunuyor. Uygulamaya yapılan http requestler hakkında istatistikler, databaseye yapılan sql'ler hakkında birçok  istatistik mevcut.

# jvisualvm

sadece jdk paketinin içinde bulunan (bin dizininde) görsel bir uygulamana performans monitör etme yazılımıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# SonarQube
Kod kalitesini arttırmak/incelemek amaçlı yazılımdır. Bu yazılım comitlenen kodları sürekli olarak incelemeye alıp, kodun durumu hakkında rapor/bilgilendirme yapmaktadır. Bazı algortimalar kod üzerinde tekrarlanan kısımları tesipt edebilir, potansiyel hataları bulabilir (runtime'a ihtiyaç duymadan direk kodu inceleyerek karar verebilir).

"__Sonar__" projenin eski adıdır. __SonarLint__ ise; Eclipse IDE için yazılan eklentiye verilen isimdir.

# jshint vs eslint vs jslint
javascript için potansiyel kod hatalarını ve düzenini sağlamak için kullanılan yazılımlardır.

- IDE'mizde ilgili paketin eklentisi var ise, root dizinimizde ilgili pkaetin config dosyasını ayar ve bu konfiglere göre kodumuzu düzeltir, yada uyarı verir vs...
- komut satırından çağrılarak, hatalar (sonuçlar) çıktı olarak görülebilir.

# eslint-plugin (or eslint-parser) vs eslint-config
eslint için birden fazla parser (rule) çeşidi yazılabilir. bu parserlar pluginler tarafından yazılır. config'ler ise hangi parserların enable/diable/error/warning olarak gösterileceğini belirler (extend eder). örnek: airbnb-plugin-eslint, babel-plugin-eslint piyasada sık kullanılan yazılımlardır.

ilgili dizin içerisinde .eslintrc dosyasında configler (parser plugini yazılır, hangi rule'ler disbale edilecek belirtilir gibi) yazılır. IDE'deki ilgili plugin yada çalıştırılan komut satırı uygulaması alt dizinlerde bu kurallara göre hataları bulur.

IDE'lerin genelde kendi formatter'ları oluyor. bu formatter eklentileri, eslint'ten bağımsız çalışıyor. eslint'in kendi formatalama kısayol tuşu oluyor. burada bu durum tartışılmış: (source-id: 71)

Eslint'te hatalar ve formatlama farklı kavramlar. genellikle bu ikisi (bazı yazılımcılar tarafından) bazı durumlar için karıştırılabiliyor. bu sebeple eslint formatter'ı, (hataları gidermeyeceği için) formatlamamış olarak düşünülüyor. oysa eslint formatter'ı zaten hataları gidermez.

# lint (or linter)
potansiyel kod hatalarını yakalamk ve düzenini sağlamak için kodun kontrol edilmesi/eden tool'a verilen genel isimdir.

# EditorConfig
.editorconfig dosyası projemizin root'unda durur. EditorConfig'in neredeyse tüm IDE'lerde default/gömülü support gelir. Sadece kodun formatını belirleyen standartlar içerir.

EditorConfig, "Prettier" gibi formatlamak için executable içermez. EditorConfig sadece IDE'ye nasıl çalışaması gerektiğini içeren bir standart dosyadır.

Eslint ve Prettier ile aynı projede EditorConfig de bulunabilir. Bunda bir sakıncası yoktur. Bu 3'ünün kısmen aynı görevleri gördükleri yerler var, fakat temelde farklı görevleri var: Eslint kod analizi yapar (kullanılmayan variable'ları uyarması gibi), Prettier ve EditorConfig ise aynı amaçtadır. Fakat Prettier IDE'lerde native desteklenmez, hep eklenti gereklidir. Her developer farklı IDE'de açıp ufak bir değişikliği comit etmek istyeyebilir. Bu sebeple EditorConfig her zaman kullanılmalıdır.

# Code coverage
testler yazılırken, belirli metodlar çağrılmaktadır. yani belirli satırlar kodda çağrılmaktadır. code coverage yüzdelik cinsindendir. %100 olan kod'da, her satıra en az bir kere girilmiş demektir.

# static vs dinamik test

static test, asıl uygulamanın kodu yürütülmeden yapılan analizler/testlerdir. örneğin; kodun temiz olup olmaması, derlenip derlenmediği, dökümanlarının yazılıp yaızlmadığı gibi faktörlerin testini kapsar. dinamik testlerde ise; junit ve integration testleri koşulur.

# integration test (or entegrasyon testi) vs unit test (or birim testi) vs end-to-end (or e2e test or uçtan uca test)

unit test bir birimin kendi içinde çalışıp çalışılmadığının testidir. örneğin; login işlemi olup olmadığı. unit testlerde mock kütüphaneleri ile diğer sistemler mock'lanır. böylece diğer sistemler çalışmıyor olsa bile unit testler tamamlanır.

birden fazla unit'in birbiri ile düzgün çalışıp çalışmadığını test eden testler entegrasyon testleridir. burada sistemin bazı kısımları mock'lanır.

e2e testlerde ise sistem hiç mock'lanmaz.

__system test (or sistem testi)__ terimi genelde e2e testi yerine kullanılıyor. fakat e2e terimini kullanmak daha net olduğu için e2e terimi tercih edilmelidir.

# happy path test (or golden path test or happy day scenario test)

uygulamanın işleyip işlemediğini test etmek için yapılacak en basit testi ifade eder. örneğin ufak bir update çıkıldı. tüm sistem testi çalıştırılacak zaman olmasın. happy path testi ile login olunur, hızlıca bir alışveriş yapılır ve happy test başarılı olmuştur.

# smoke test

smoke test happy path'in eş anlamlısı değildir, fakat aynı anlama gelmektedir.

# Disaster Recovery Test
Deprem gibi felaket durumlarında olabilecek senaryolar test edilir.

kaynak: (source-id: 450)

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# .htaccess

apache htpp server'ın kullandıgı bir dosyadır. bu doaya içerisinde basit belirtimler ile hangi dosyaların dışarıya açık, hangilerinin hangi ip'lere açık, 404 durumunda hangi dosyanın response olarak gideceği gibi bir çok özelliği ayarlanabilmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Endüstri 4.0 (or 4. Sanayi Devrimi or Industry 4.0 or Industrie 4.0 or the fourth industrial revolution)

Tarih boyunca endüstride birçok devrim yaşanmıştır. sırası ile:

1. su ve buhar gücünün daha verimi kullanan sistemler oluşturulması (1800 yılları)

2. üretim bandı tasarımı ve elektriğin seri üretimde kullanılmaya başlanması

3. mekanik ve elektronik teknolojilerin yerini dijital teknolojiye bırakmasına sebep olan programlanabilir makinelerin kullanılmaya başlanması (1950 yılları)

4. burada amaç; endüstrinin (dikkat: sadece fabrikanın değil) siber-fiziksel (tüm fiziksel sistemlerin) sanal ortamla iletişimde kalarak çalışmasıdır.

   programlanabilir embeeded cihazlar fabrikalarda belli firmalar tarafından dağıtılıp, sadece belirli işler için kullanılabiliyordu. bu sebeple çoğu yazılım özel-tasarım işletim sistemlerinde çalışıyordu. 4.0 ile yazılan yazılımlar daha modüler ve daha farklı amaçlarda kullanılabilmesi planlanıyor. Bunun için işletim sistemi yapılarının ortak olması gerekiyor. Ancak bu şekilde başkası sizin yazılımınıza depend olabilir yada fork edebilir. bu şekilde hem daha hızlı/kolay uygulama geliştirilebilecek, hemde tekrar kullanılabilir modüler uygulamalar artacak. burada işletim sistemli bu cihazlar iot cihazlarına denk gelmektedir. kolay ve hızlı uygulama geliştirme sayesinde ise; big data, yapay zeka gibi kavramlardan daha çok yararlanılabilecek. hatta bu durumdan sadece fabrikalar değil, o endüstriye bağlı internet siteleri etkilenecek. mesela e-ticaret sitesinde ürün stokları fabrikadaki stok sayısından otomatik gösterilecek. e-ticaret sitesindeki kullanıcıların isteğine bağlı renkte ürünler fabrikadan otomatik üretilecek ve teslim edilecek gibi...

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# İş zekası (or Business Intelligence)

endüstride, ham veriyi anlamlı ve kullanışlı bilgiye dönüştüren teoriler, metodolojiler, süreçlerin, mimarilerin ve teknolojilerin bir kümesidir. iş zekası işinde çalışanlar; istatistik, veri madenciliği, iş/süreç analizi, raporlama gibi bir çok farklı şeyden yararlanarak şirket için kararların alınmasında rol oynarlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Daemon (or Disk and Execution Monitor)
Daemon kelime anlamı: şeytan

Yazılım dünyasında bu terim arkaplanda çalışan uygulamalara verilmektedir. Direk olarak kullanıcı ile iletişimde değildir, fakat arkaplanda komut/request almak için beklemektedir. genelde uygulamanın isminin sonuna "d" harfi koyulur. örneğin; syslogd, işletim sisteminde system log'larını tutan arkaplan uygulamasıdır. sonundaki d harfi deamon'dan gelmektedir. windows'taki servisler birer Daemon örneğidirler.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Internet Information Services (or IIS)

Web sayfalarının yayınlanmasını ve web uygulamalarının çalışmasını sağlayan, istemcilerden HTTP ve FTP üzerinden gelen talepleri Microsoft Windows sunucu tabanlı işletim sistemlerinde karşılayan birimdir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Sanal gerçekçilik (or Virtual Reality or VR)

Son kullanıcıyı tümüyle sanal bir ortama aktarıp, orada hareket etmesini sağlayan sistemlerdir.

# Artırılmış gerçeklik (or Augmented Reality or AR)

Gerçek fiziksel dünya son kullanıcıya zenginleştirilip yansıtılmasıdır. Örneğin bir gözlük aracılığı ile; son kullanıcı sokakta gezerken aslıdna olmayan bir insanı görebilir. SAdece o insan sanaldır. kalan herşey gerçektir.

# Mixed Reality (or Karma Gerçeklik or MR)

AR içide kullanılan sanal objeler gerçek dünyadaki objeler ile daha uyumludur ve onlarla etkileşimdedir. örneğin bir buzdolabı kapağı açıldığında içinden meyve dökülmesini MR ile yapabilirsiniz. fakat AR buna müsait değildir. AR direk sanal objeleri belli bir konuma yerleştirir. onlara son kullanıcı dokunarak temas eder. fakat MR, gerçek dünyadaki objelerin tipini, konumunu da algılayıp sanal nesneler ile etkileşimli olmasını sağlar.

# Holografi

Uzayda bir cismin varlığına ait bilgi bize genellikle ses veya ışık dalgaları halinde ulaşır. Holografi, cisimlerden gelen dal­galardaki bilgileri belirli bir şekilde depo edip, bu bilgide hiçbir kayıp olmadan tekrar ortaya çıkartmayı sağlayan bir tekniktir.

# Piyasadaki cihazlar

Microsoft - Hololens

Oculus/Facebook - Rift

Samsung - Gear VR

Google - Daydream

Sony - PlayStation VR

HTC/Valve - Vive

# Kinect

Microsoftun donanım cihazı. ufak bir yerde sabit duruyor. karşısındaki kişinin vucut yapısını uzaktan algılıyor. kullanıcının kıpırdamalarını (el, ayak vs) uzaktan algılıyor. bu şekilde oyun oynamayı sağlıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# GNU Projesi (or GNU Tasarısı or GNU Project)

Richard Stallman tarafından fikir olarak ortaya atılmış bir akımdır. bu tasarı temel olarak __özgür yazılım__ felsefelerini içerir. yazılımlar "__özgür yazılım__" olabilmesi için şart olan kurallardır.

- 0 numaralı özgürlük: Herhangi bir amaç için yazılımı çalıştırma özgürlüğü

- 1 numaralı özgürlük: Her ne istiyorsanız onu yaptırmak için programın nasıl çalıştığını öğrenmek ve onu değiştirme özgürlüğü

- 2 numaralı özgürlük: Kopyaları dağıtma özgürlüğü. Böylece komşunuza yardım edebilirsiniz.

- 3 numaralı özgürlük: Tüm toplumun yarar sağlayabileceği şekilde programı geliştirme ve geliştirdiklerinizi (ve genel olarak değiştirilmiş sürümlerini) yayınlama özgürlüğü.

Özgür yazılıma tamamen uyan yazılımlar bazen bazı developer'larca terchi edilmemektedir. Bunun bazı sebepleri:
- yazılımı ticari kullananlar belli oranda para desteği verirse, yazılım daha hızlı gelişebilecektir.
- %100 aynı yazılımı forklayıp farklı isimde dağıtıp, insanlardan istatistik toplayan yazılımlar forklanmaktadır ve bu firmalar bedava gelir elde etmekte ve forkladıkları projeye hiçbir katkı sağlamamaktadır. En azından bu firmalar belli yaptırımlar getirilmesi savunulmaktadır.

# GNU yazılımları

"GNU Tasarısı" nı baz alarak geliştirilen yazılımlardır.

# GNU

GNU; "GNU Tasarısı" nı baz alarak geliştirilen bir işletim sistemidir. İsmi çok yerde yanlış anlamda kullnılmaktadır. İsminin açılımı "GNU's Not Unix" (GNU Unix değildir) dir. Bu ismi almasındaki sebep de tasarımının Unix'e benzerken kendisinin özgür yazılım olması ve herhangi bir UNIX kodunu içermemesidir. Linux çıkana kadar geliştirilen işletim sistemi stabil bir sürüm çıkaramadı. Liuxun doğuşu ile geliştirilmesi durduruldu.

# GNU/Linux

Bu ibarenin kullanılmasının sebebi; Linux'un bünyeside GNU araçlarını barındırmasıdır.

# libre
"free" kelimesi ingilizcede hem ücretsiz hemde özgür anlamına gelmektedir. ücretsiz yazılım ile özgür yazılım arasında çok büyük farklar var. bu iki terimi ayırt etmek için özgür terimi yerine ispanyolcada özgür anlamına gelen "libre" terimi kullanılmaktadır.

# FOSS (or F/OSS or Free and open-source software) vs Free/Libre and Open Source Software (or FLOSS or F/LOSS)

sadece bir sınıflandırmadır. lisans değillerdir.

FOSS ve FLOSS arasındaki fark "libre" başlığında anlatılmıştır.

# Copyleft (or Telif feragatı)

Telif haklarının belirli bölümlerinden yazarı tarafından belirtilen şartlar altında feragat edilmiş olan bir esere işaret eder.

- işareti; 🄯 (daire içinde sola dönük "C" harfi)

# Copyright (or Kopyalama hakkı or telif hakkı or röyalti or royalty)

telif kelime anlamı: eseri yaratan kişinin, bu eserden doğan haklarının hepsi.

- bir kişi ya da kişilerin her türlü fikri emeği ile meydana getirdiği bilgi, düşünce, sanat eseri ve ürününün kullanılması ve kopyalanması ile ilgili hukuken sağlanan haklardır.

- copyleft'in zıttıdır.

- işareti; © (daire içinde "C" harfi)

# trademark (or trade mark or trade-mark or tr:Alametifarika or marka or brand)
baskı yolu ile çoğaltılabilecek her türlü simge, isim, çizim gibi her türlü ifadelerdir.

™ yada (TM) işareti kullanılır. yasal olarak "registred" olursa ® yada (R) işareti kullanılır.

# tescilli (or Registered)
tescil; Herhangi bir şeyi resmi olarak kaydetme, kütüğe geçirme'dir.

tescilsiz markalarda ticaret Kanunlarının "Haksız Rekabet" hükümlerince yinede korunur. fakat tescilli markaların korunmaları daha önceliklidir.

tescilli markalar, türkiyede zorunlu olunmasada, ® yada (R) işaretini markanın yanına eklemektedirler. bu işaret tüm dünyada kullanılmaktadır.

Ses veya melodi'ler baskı yolu ile çoğaltılamayacağı için tescil alınamayacağı düşünülebilir, fakat melodinin ve sözlerin notaya dökülmüş halinin patenti alınabileceğinden

# patent
ingilizce'de de aynıdır.

patent belli bir özellik için alınır. örneğin marka'nın patent'i alınamaz. bir markanın ancak tescili yapılabilir. markanın tescili türkiye'de "Türk Patent Enstitüsü"'ne yapılır. enstitüdeki patent ismi birçok kişide karışıklık yaratıyor. 

# freeware
ware kelime anlamı: mal

resmi olarak kullanılan bir terim değildir. ücretsiz kullanılabilen veya ücretsiz dağıtılabilen uygulamaların lisanslarının olduğu gruptur.

# shareware
belirtilen süre içinde (deneme süresi) kulanımı ücretsiz veya kısıtlı özelliklerle kulanımı ücretsiz olan uygulamaların lisanslarının olduğu gruptur.

# Digital Millennium Copyright Act (or DMCA)
Amerika'nın digital hakları korumak için onayladığı yasanın özel ismidir. Aynı isimde develete bağlı olmayan bir kuruluş vardır (dmca.com).

# digital rights management (or DRM)
Digital hakları koruyabilmek için kullanılan teknolojilere verilen genel isimdir. örneğin apple'ın sunduğu müzik servisinden indirilen müzikler kopyalanamıyor. bunu engellemek için apple'ın çalıştırdığı mekanizma DRM görevi görmektedir.

# Creative Commons (or CC)

Hem firma, hemde bu firmanın yarattığı lisans'ların prefix'leridir. CC firmasının birçok lisansı vardır. bazıları:

- Creative Commons Attribution (or CC-BY)
- Creative Commons Attribution-ShareAlike (or CC-BY-SA)
- Creative Commons Attribution-NoDerivs (or CC-BY-ND)

# EULA (or End User License Agreement or Software license agreement)

yazılım lisanslarına verilen genel isim.

# Piyasada kullanılan bazı lisanslar

detaylı karşılaştırma: (source-id: 454)

en çok kullanılan lisansların karşılaştırması: (source-id: 453)

Yukarıdaki listedeki bazı özellikler:
- Commercial use
  
  Yazılımın ticari kullanıma açık olup olmadığına izin verilip verilmediği bilgisidir. şirket içindeki işçilerin kullandığı tool'larda ticari kullanıma girmektedir. Yani sadece direk olarak para kazanmamızı sağlayan değil, dolaylı yoldan ticari iş akışımızı işletmemize yarayan yazılımlarda "ticari kullanım" sürecine dahil edilmektedir. Fakat genelde alternatif yazılımlar tercih edilebileceği için ticari kullanıma kısmen izin veren lisanslar da bulunmaktadır.

- Distribution

  Yazılımın dağıtılıp dağıtılmayacağı. sadece ticari olarak diil, kişinin tek olarak başkasına verebilmesi de bu durumu kapsar.

- Modification

  Yazılım üzerinde modifikasyon yapılıp yapılamayacağı iznidir

- Patent use

  Katkıda bulunanlarda hak sahibi (paten alabilme hakkı) olup olmadığını belirtir

- Disclose source

  Eğer modifiye edilmiş kodun derlenmiş hali piyasaya sürülürse, kodun açılması gerekir.

- License and copyright notice

  Projedeki lisans dosyası yeni projenin içerisinde bir yere konulmalıdır.

- Network use is distribution

  web tarayıcısı yada web servisi gibi hizmetlerden kodun derlenmiş hali piyasaya servis olarak açılırsa, kodun tamamamı da dağıtılmalıdır.

- Same license

  Yeni kod yine aynı lisans ile dağıtılmalıdır. (choosealicense.com çok detaya inmemiş. karşılaştırma tablosunda, bazı lisanslarda bu koşul işaretlenmiş fakat bazı durumlarda benzer lisanslarla da fork'a izin verilebilmektedir. mutlaka aynı lisans istemeyen lisanslarda var.)

- State changes

  Changes made to the code must be documented.

Yukarıdaki choosealicense.com karşılaştırma listelerinden bazı notlar:

- GNU AGPL (or Affero GPL) vs GNU Genel Kamu Lisansı (or GPL or GNU GPL or General Public Licence)
  
  ikisinin 3'üncü sürümleri ile ilgili not: 

  Birbirlerine aşırı benzerdir. Tek temel farkı; AGPLv3 web'den sunulan bir hizmet olsada kodların tamamı açılmak zorundadır. Oysa GPLv3de network'ten açılan servislerde bu zorunluluk yoktur. fakat her iki lisans'ta da diğer tüm durumlarda kodun tamamı açılmalıdır.

- LGPL (or Kısıtlı GPL or Lesser GPL)

  GPL ile çok benzerdir. Tek fark: GPL'e ek olarak şu özgürlüğü sunar: LGPL ile patentlenen yazılım, istenirse özgür olmayan yazılımlar tarafından kullanılabilir. bu lisans genelde formatlarda ve eklentilerde kullanılmaktadır.

- MIT Lisansı

  "özgür yazılım" tanımına uyar. ve türetip kullanılan kodun ne yapılması gerektiği konusunda hiçbir kısıtlama sunmaz. istenirse yeni kod ticari kullanılabilir, yada tamamen kapatılabilir.

- BSD

  MIT Lisansı ile temelde aynıdır. ek olarak şu madde vardır: kaynağı alınan kod referansı bir yerlerde belirtilmelidir.

- Apache License 2.0

  BSD ile çok benzerdir.

# farklı projeler için farklı lisanslar
font, data, media için ayrı ayrı uygun lisanslar mevcut. bu sebeple projelerin birden fazla lisansı olabiliyor. her lisans projenin ayrı ayrı kısımları için belirtiliyor.

projenin dökümantasyonu kod ile aynı sınıflandırılabilir. yani yazılım için geçerli lisanslar, dökümantasyon içinde kullanılabilir.

# lisanssız projeler
lisanssız her proje Copyleft'tir. fakat github gibi sitelerden yayınlanan kodlar bazı hakları esnetebilir. Bu sebeple lisansız projeleri kişisel kullanımda dahi kullanmamak gerekir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Statistical Package for the Social Sciences (SPSS)

İstatistik analiz yazılımıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Programming paradigm

paradigm türkçesi: paradigma

paradigma kelime anlamı: 1-örnek, 2-bir şeyin nasıl üretileceği konusunda örnek/model

proramlama dilinin özellikleridir: örneğin cephe yönelimli olması, nesneye yönelimli olması birer paradigmadır.

# multi-paradigm programming language

bazı programlama dillerinin bazı özellikleri birden fazla paradigmayı desteklemektedir.

# Microcode
işlemcinin kendi içinde kullandığı instruction'lardır. işlemciye dışarıdan makine kodu gelir, işlemci bu makine kodlarını microcode'lara çevirir.

# programlama dilleri jenerasyonları

- 1inci jenerasyon (1GL): 1 ve 0'lardan oluşan programlama dilleridir. 2inci dünya savaşında Nazi almanyasının şifreli mesajlaşma makinesi olan Enigma'yı çözebilmek için, Alen Turing, Turing makinesi ile 1940'larda ilk programlama mantığı ortaya atılmıştır. Fakat proramlama dilleri olmadığı için manyetik teypler panel aracılığı ile kapatılıp açılıyordu (switch/toogle). bu şekilde sadece 1 ve 0'lar ile işlemler yapılıyordu. Bu sebeple bu jenerasyonun dillerinde kodu çevirmeye ihtiyaç yoktur. direk kod makinede işletilebilir durumdadır.

- 2inci jenerasyon (2GL): düşük seviyeli programlama dilleri. assembly. İlk 1950'lerde ortaya çıkmıştır. Bu jenerasyonda temel yenilik, 1 ve 0'ların insanlar tarafından okunmasının aşırı gereksiz ve zor olmasıdır.

- 3inci jenerasyon (3GL): yüksek seviyeli proramlama dilleri. C, C++, C#, Java. Bu jenerasyonda temel yenilikler:
  - 2GL'nin daha çok cihazlara bağlı syntax'lar içermesinden kurtulmak
  - daha human-readable bir syntax yapmak
  - byte üzerinden yönetilebilen yeni bütünleşik veri tipleri oluşturabilmek. örnekler:
    - array
    - Class/obje
    - OS'un register'larının desteklemediği büyüklükte sayılar

- 4inci jenerasyon (4GL): diğer jenerasyondakiler gibi sadece bit, byte veya bunların üzerine kurulmuş temel veri tiplerini yönetmekle değil, direk olarak logical anlamda "veriler" kullanabilmektedirler. örneğin tablo üzerinde direk işlem sağlanabilmekte, ve ekrana GUI raporu alınabilmektedir. Örnekler: SPSS, Unix shell, SQL. Bazı araştırmacılar, bu jenerasyonun sadece DSL olduğunu düşünmektedir. Araştırmacılar bu jenerasyonun domaine özel geliştirilen bir dil olduğunu düşünmektedir. örneğin; web development, database manipulating/reporting, mathematical optimization, GUI development...

- 5inci jenerasyon (5GL): programcının algoritma geliştirerek çözüm geliştirmesinin ötesinde, koşulları ve kısıtları bilgisayara verdiğinizde, bilgisayarın çözümü kendisinin bulmasına yönelik olarak tasarlanmaktadır. Bazı arastırmacılar, bu tarz dillerin jenerasyon grubu altında olamayacağını belirtmekte.

- akademik kaynaklar 4 ve 5inci jenerasyonları çok net bir çizgi ile ayırmış durumda diil. 5inci jenerayonun, bir jenerasyon olmaması gerektiğini düşünenlerde var.

- Bir dil, birkaç jenerasyona birden uyabilir.

- jenerasyon yükseldikçe, daha kolay şekilde donanımdan daha bağımsız uygulamalar yazılması sağlanır. "high level programming language" terimi üst seviyeli diller için kullanılır.

- en üst seviyede dahi donanımdan bağımsız veya donanıma bağımlı uygulama yazılabilir. çağırdığımız API (kütüphaneler) ve/veya dilin binary/bit bazında işlem destekleyip desteklememesi gibi özellikler sayesinde donanıma bağımlı uygulamalar en üst seviyede de yazılabilir.

# bazı diller
popüler yüksek seviyeli diller (çıkış tarihleri ile - yıllar draft veya stable olabilir):
- Fortran (1954)
- Lips (1956)
- COBOL (1959)
- PASCAL (1970)
- Prolog, SQL, C (1972)
- Ada (1980)
- C++, Objective-C, ABAP (1983)
- MATLAB (1984)
- Perl (1987)
- Visual Basic, Python (1991)
- Lua (1993)
- R (1993)
- Java (1995)
- PHP 1995
- Ruby (1995)
- JavaScript (1995)
- VBScript (1996)
- ECMAScript (1997)
- ActionScript (1998)
- C# (2000)
- Visual Basic .NET (2001) (Bu dil "Visual Basic"'dan farklı. successor olarak yayımlandı.)
- Scala (2003)
- Groovy (2004)
- Go (2009)
- CoffeeScript (2009)
- Rust (2010)
- Kotlin (2011)
- TypeScript (2012)
- Swift (2014)

# go
golang olarakta adlandırılmaktadır.

native derlenen bir dil. Sadece çok basit özellikler içeriyor. bu durum ona performans kazandırıyor.

concurrent uygulamaların az yer harcayacak şekilde çalışması için mimarisi uygun tasarlanmış. OS thread'i yerine, "goroutine" denilen kendi içinde sanal thread management'ı var. OS thread'i gibi çok bellek harcamıyor, çünkü temelde daha basit özellikler içeriyor. programcının hiçbirşeyden haberi olmuyor.

# Yordamsal programlama dili (or Procedural programming language or prosedürel programlama dili)

kod tekrarı engellemek amaçlı (goto/jump gibi terimler yazmaya gerek kalmadan) programın yordamlara bölünmesi ile yazılmayı destekleyen programlama dilleridir.

yordamsal programlama'da, programın dallandığı yerlere "subroutine (or subprogram or callable unit)" adı verilir. dolayısı ile kullandığımız dilin diğer paradigmalarına göre "prosedure" şunlardan biri olacaktır: "function", "method".

fonksiyonel programlamadan temel farkı; fonksiyonel programlamada daha çok "pure" fonksiyonar ile çalışırken, prosedürel'de genelde pure fonksiyonlar yoktur.

# object orianted (or nesneye yönelimli) vs object based (or nesne tabanlı)

javascript nesneye yönelimli değildir. nesne kullanır bu sebeple nesne tabanlıdır. fakat nesneye yönelimli dillerin desteklemesi gerektiği özellikleri destekleyecek şekilde özenle geliştirilmez. örneğin javascriptte inheritance ve polimorfism yoktur. son çıkan javascript sürümlerinde sınıflar gelmiştir. fakat bu seferde encapsulation yoktur.

bu iki kavram piyasada sürekli biribir ile karıştırılmaktadır.

object orianted'lar ikiye ayrılır:

- # class based
  sınıfıları kullanarak implementasyon yapan dillerdir. (java buna bir örnektir)

- # prototype based
  bazı kaynaklarda bu şekilde de isimlendirilir: prototypal, prototype-oriented, classless, instance-based programming

  obje klonlayarak implementasyon yapan dillerdir. her obje türetilen objenin prototype'ını referans olaak tutar. bu yapının en güzel özelliği runtime sırasında prototype'a metod veya field eklenebilir. ve hatta prototype referansını tutan instance'lara da bu değişiklikler yansıtılabilir. (javascript buna bir örnektir)

# 4 major principles of object orianted programming 

Aşağıdaki 4 madde sadece en temel prensiplerdir. Birbirlerine çok yakın prensiplerdir.

"interface" veya "abstract" sınıflar ile OOP'nin aşağıdaki maddelerini gerçekleyebilmemizi sağlar. 

not: her dilde; java'daki gibi hem "interface" hemde "abstract" sınıf kavramları birden olmayabilir.

- # encapsulation (or kapsülleme)
  
  2 temel kavramdan oluşur:

  - Information hiding

    modifier'lar (public, private...) gibi keyword'ler bunları yapabilemizdir.

  - Packaging

    paket(ler) veya sınıf(lar) içerisinde tüm bilgilerin/metodların, bir unit olarak dışarıya sunulmasıdır..

- # Abstraction (or soyutlama)

  sınıf içerisindeki detayların (property'lerin/metodların), dışarıdan sınıfı çağıranlar tarafından bilinmesine gerek kalmamasıdır.

- # Inheritance (or kalıtım)

  sınıfların bir yada birden fazla yerden türeyebilme özelliğidir.

- # Polymorphism (or polimorfizm or çok biçimlilik)

  türeyen sınıflar, süper sınıfın metodlarını isterse override edebilmesidir.

# fonksiyonel programlama (or functional programming)

fonksiyonel programlama genelde;

- rekursiv işlemlerin yapıldığı,

- pure fonksiyolar ile çalışıldığı

- fonksiyonlar fonksiyonlara parametre olarak geçilebildiği

dillerdir.

Burada "multi-paradigm programming language" baslıgında belirtildiği gibi her dilin birden fazla özelliği desteklediğini hatırlatmak gerekli. Aynı zamanda yordamsal, fonksiyonel, nesneye yönelimli terimleri programlama dilinin bir özelliği değildir. aslında bir yazım tarzıdır. daha farklı bir bakış açısıyla;

- fonksiyonel dil: devide and concur mantığı ile problemlerin çözüldüğü diller

- prosedürel dil: sıralı şekilde birbiri ardına işlem yapılarak bir işin gerçekleştirildiği diller

- nesneye yönelimli dil: gerçek hayattaki nesne yapıları oluşturularak bunlar üzerinde biribirinin aksiyonları çağrılarak yazılan uygulamalardır

tabikide eğer bir dilde nesne yapısı hiç yoksa nesneye yönelimli tarzda uygulama yazmak mümkün olmayacağı için bu terimler sanki dilin bir özelliğiymiş gibi anlatılıyor. oysa diil.

# Olaya dayalı programlama (or olay güdümlü programlama or event driven programming)

GUI, donanım sinyalleri gibi olaylar sonrası aksiyon alan programlama dilleridir. aslında tüm programlama dilleri kütüphaneleri desteklediği sürece event bazlı olabilir. fakat genelde ağırlıklı olarak event'lere dayalı programlar için bu terim kullanılır. örneğin javascript. sadece son kullanıcı sayfada bir yere tıkladımı, yada sayfa yüklediğinde bir aksiyon alınır. onun dışındaki aksiyonlar nadirdir. zaman tetiklemeleri mevcuttur. belirli zamanda event tetiklenir. timeout metodları gibi...

örneğin komut satırı ile işlem yapan script'ler event bazlı değildir.

# declarative programming

decleration türkçe kelime anlamı: beyan etmek, bildirmek

dekleratif diller işin nasıl yapıldığına karışmaz. sadece ne yapılması istendiğini belirtir. örnek: SQL, CSS, HTML, Java'daki annotation'lar...

# imperative programming

imperative türkçe kelime anlamı: zorunlu, mecbur

declarative'in tersidir. nasıl olacağına tam olarak karışır ve sonucta ne istediği dilin kendisini ilgilendirmez.

# reactive (or tr:reaktif) programming

reactive türkçe kelime anlamı: duyarlı, tepkili.

reactive bir programlama paradigmasıdır.

çoğu yerde fonksiyonel programlama ile karıştırılır fakat farklı kavramlardır. fakat reactive programlamak için fonksiyonel programlama en idealidir.

a = b + c; dediğimizde b ve c toplanır sonucu a'ya atanır. peki b değişirse a değişir mi? normalde hayır. fakat reactive programlamada değişmesi bekleniyor. reactive programlama; data'ların değişimi ve bu değişimin etkileri/yayılımı'na dayanır.

Reactive programlama ile yapılan herşey diğer programlama paradigmaları kullanılarakta yapılır. burada amaç; development sürecine bir yön vermektir. şunlar ağırlıklı kullanılır:

- reactive'de event'lere subscribe işlemi çok sıkça kullanılır.

- data değişimleri de birer event olarak algılanır

- subscribe olurken Listener/handler sınıfı atmak yerine sadece ilgili metod atılır. listener sınıfı komple oluşturulmaz. kod fazlalığı olmaz. listener sınıfı yarattığımızda override etmek zorunda kaldığımız fakat kullanmadığımız metodlarda olur. onları da yazmak durumunda kalmayız.

- event'lerimiz non-blocking thread mekanizmasını destekliyor olur (başka yerde anlatılıyor)

- fonksiyonel dil / lamda / stream gibi teknolojilerden çok sıkça yararlanılır

- bazı listenerlarda hatayı yakalamk için try/catch mekanizması gereklidir. fakat reactivede hatalar onError metodları ile yakalanır.

- diğer paradigmalarda, databaseden veri çekerken tüm veriyi çekeriz. oysa reative'de 10 adet veri çekilir event tetiklenir. daha sonra diğer 10 adet daha çekilir ve event tetiklenir. amaç data geldikçe harekete geçmektir. eskisi gibi aldım yolladım kaydettim bitti mantığı yok. data aktıkça, sistem buna hazırdır (tepkilidir).

sonuc olarak reaktife uygun yazarken, event başladığında yaptığınız işlemde side effectleri düşünmezsiniz. çünkü zaten her side effect'in subscriber'ı mevcuttur. onlar işlerini yapacaklardır. bir programda binlerce/milyarlarca side effect olduğunu düşünürseniz reactive çok ideal olacaktır. yani kod akışını takip etmek yerine, olayları takip etmeye çalışırız.

# reactive vs event driven

reactive event-drive'ın bir çeşididir. klasik event driven developement bir event gerçekleştiğinde devreye giren kodları barındırır, fakat react'ta event data'nın da değişmesini kapsar. yani data değiştiğinde event tetiklenir. klasik event driven sistemlerde data'nın değişmesi diye bir kavram yoktur.

# reactive system

büyük resme bakıldığında (mimarisel olarak) reactive bir sistem için aşağıdakiler şarttır ve bunlar www.reactivemanifesto.org'da belirtilmiştir:

- Responsive/Duyarlı: sistem her event'e cevap veriyor olmalı ve mümkün olduğunca hızlı cevap vermelidir. timeout gibi hata durumlarında da hata event'leri devreye girmelidir.

- Resilient/dirençli: sistem hatalar karşısında da responsive davranır 

- Elastic/esnek: ölçeklendirilebilir durumda olmalıdır. daha fazla kaynak üzerinde çalıştığında daha hızlı cevap verebilmelidir. 

- Message Driven/mesaj güdümlü: herşey asenkron mesajlaşma tekniği ile gerçekleşmelidir.

reactive programming, reactive sistem'in uygulanabilmesi için uygun bir programlama paradigmasıdır.

not: reactif manifesto'da reactive programlama'daki data değişimine tepki gösterme zorunluluğu maddesini içermemektedir.

# Reactive Streams

"Reactive Streams" reactive programlamaya uygun data çekme/işleme politikası için olan sınıf/sınıflardır. örnek: data çekerken tüm data yerine 10'ar 10'ar çekmemizi sağlayan api'ler react yapısına uygundur. dikkat edilirse 10'ar 10'ar çekme işlemi bir stream yapısıdır. bu sebeple "reactive stream" olarak adlandırılır.

Java 9 ile gelen reactive API'sinin ismi de "Reactive Streams"'dir. __java.util.concurrent.Flow.*__ paketi altındaki sınıfları içeriyor.

reactive-stream paketleri 1.0.2 öncesi org.reactivestream.* altındaydı. 1.0.2 ile birlikte jdk'ya dahil edildi ve __java.util.concurrent.Flow.*__ altına taşındı. kaynak: (source-id: 452)

Aşağıdaki dependency her iki pkaetinde birbirine referans edebilmesini sağlıyor.

```xml
<dependency>
   <groupId>org.reactivestreams</groupId>
   <artifactId>reactive-streams-flow-adapters</artifactId>
  <version>1.0.2</version>
</dependency>
```

```java
public class MySubscriber implements java.util.concurrent.Flow.Subscriber<Employee> {

	private Subscription subscription;
	
	private int counter = 0;
	
	@Override
  //subscribe işlemi gerçekleştiğinde bu metod çalışır.
	public void onSubscribe(java.util.concurrent.Flow.Subscription subscription) {
		System.out.println("Subscribed");
		this.subscription = subscription;
		this.subscription.request(1); //requesting data from publisher
		System.out.println("requested 1 item");
	}

	@Override
	public void onNext(Employee item) {
		System.out.println("Processing Employee "+item);
		counter++;
		this.subscription.request(1);
	}

	@Override
	public void onError(Throwable e) {
		System.out.println("Some error happened");
		e.printStackTrace();
	}

	@Override
	public void onComplete() {
		System.out.println("All Processing Done");
	}

	public int getCounter() {
		return counter;
	}
}
```

```java
// Create Publisher
SubmissionPublisher<Employee> publisher = new SubmissionPublisher<>();

// Register Subscriber
MySubscriber subs = new MySubscriber();
publisher.subscribe(subs);

List<Employee> emps = EmpHelper.getEmps();

// Publish items
System.out.println("Publishing Items to Subscriber");
emps.stream().forEach(i -> publisher.submit(i));

// wait untill processing of all messages are over
while (emps.size() != subs.getCounter()) {
  Thread.sleep(10);
}

publisher.close();
```

# ReactiveX (or Reactive Extensions)

tüm programlma dilleri için reactive API kütüphanesi oluşturmayı amaçlayan proje. 

# RxJava

ReactiveX java implementasyonu. Aynı zamanda Java 9 ile gelen "Reactive Streams" implementasyonudur.

# Reactor

Java 9 ile gelen "Reactive Streams" implementasyonudur.

Spring 5.0 ile birlikte, __spring-webflux__ paketi ile spring mvc'ye reactor ile reactif programlama desteği getirmiştir.

Reactor; Mono ve Flux objelerini sunar. Bu objeler, java 9 ile gelen 'reactive stream'in Publisher'ını implemente eder.

- # reactor.core.publisher.Flux

  is a publisher that produces 0 to N values. It could be unbounded. Operations that return multiple elements use this type.

- # reactor.core.publisher.Mono

  is a publisher that produces 0 to 1 value. Operations that return a single element use this type.

örnek basit bir kod:

```java
@RestController
public class GreetReactiveController {

    @GetMapping("/greetings")
    public Publisher<Greeting> greetingPublisher() {

        Flux<Greeting> greetingFlux = Flux.<Greeting>generate(sink -> sink.next(new Greeting("Hello"))).take(50);

        return greetingFlux;

    }
}
```

Temel olarak non-blocking olması için akış bu şekilde ilerliyor:

greetingFlux objesi özel bir webflux sınıfı. greetingPublisher metodu neredeyse başladığı gibi bitiyor. fakat greetingFlux objesi onsuccess yada onerror olunca spring webflux altyapısı servlet'ten cevabı önyüze dönüyor. onerror yada onsuccess olması uzun zaman da alabilirdi. fakat biz, greetingPublisher metodunun thread'ini kapatmış oluyoruz. dolayısı ile onerror veya onsuccess ne kadar geç tamamlanırsa tamamlansın, thread'imiz açık kalmamış olacaktır.

# Reactive Streams vs legacy stream
reactive stream özel bir kütüphane ismidir. reactive stream kendince belli özellikleri barındıran stream'lerdir. örnek: backpressure, consumer-producer modeli, data'ları parça parça çekebilme... Buı tarz nitelikler java'daki standart stream'lerde yoktur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# back-pressure (or backpressure or geri tepme or back pressure)
publisher çok fazla data sağlar ve subscriber bu dataları işlerken yavaş ise, subscriber back-pressure yapmalıdır. yani; subscriber publisher'a bir şekilde daha az data yollamasını iletebilmelidir. bu yeteneğe back-pressure denir.

back-pressure sistemi yavaşlatacaktır fakat sistemin, daha stabil (yoğunluğun stabiliteyi bozmayacak düzeyde akışkan) çalışmasını sağlayacaktır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# method vs function

metod; bir objenin fonksiyonudur.

fonksiyon ise; sınıflardan bağımsızdır.

Object orianted dünyasında "metod" ismi kullanılır. Bunun çok detaylı bir sebebi yok. "metod" terimi, "yöntem" terimi ile aynıdır. detaylı düşünüldüğünde; bir yöntem/metod ile bir akışı başlatmak için o yöntemi uygulayan bir varlığın (kod içerisinde: sınıfın) olması şarttır. Örneğin Canlı interfacesinden türemiş aslan ve insan sınıfılarının (varlıklarının) "koş" isimli metod'ları düşünülebilir. oysa "fonksiyon"; matematik'te de olduğu gibi bir varlığa ait diildir. tüm sistemden bağımsızdır.

nesneye yönelimli dillerde, her fonksiyon birer metoddur. nesneye yönelimli olmayan dillerde ise hepsi fonksiyondur. istista olarak nesneye yönelimlilerdeki static metodlar vardır. bunlar sınıfın fonksiyonlarıdır fakat sınıfa bir bağlılıkları yoktur. bu sebeple her zaman tartışma konusu olmuşlardır.

bu tanımların farkı yazılımcılar arasında bilinmediğinden; çoğu zaman yanlış yerlerde kullanılırlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# aspect oriented programming (or cephe yönelimli programlama or AOP)
başka başlıkta bununla iligli şeyler yazıldı.

Bütün programlama yaklaşımlarında kodlar uzadıkça, kodların anlaşılabilirliği çok düşmekte, bazen de içinden çıkılmaz bir hal almaktadır.

aspect felsefesi ile ortak olan kod parçaları bir yerde toplanır. uygulamanın her hangi bir kısmında bu ortak metodları kullanarak kodu kısaltmış oluruz. aspect felsefesi budur. ascpect felsefesi uygularken kütüphane şart değildir. kendimiz elle metodları çağırabilir. fakat %90 kütüphane kullanılır. sebebini bir örnekle açıklayalım: programımız her metod çağırdığında log atsın istiyoruz. bu ortak log metodunu sürekli her metodun başına ekleyebiliriz. fakat bir kütüphane olsa bize bunu otomatik yapar. bu en belirgin ve basit örnektir. eklenecek kütüphanenin metodların başına/sonuna işlem ekleme (method-interceptors) yapabiliyor olması gerekir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Behaviour Driven Development (or BDD)

TDD benzeri fakat X olursa şunu yap gibi terimlerle desteklenen test yazım felsefesidir.

Java'da JBhave frameworku (genelde) tercih edilmektedir.

given/when/then gibi terimler kullanılır.

(aşağıdaki 3 madde için kaynak: (source-id: 72))

- Given kodları kısmı; test edeceğimiz metod çağrılmadan ortamı hazırladığımız kısımdır. örnekler: test edeceğimiz metoda giden parametreleri hazırlamak, test edeceğimiz metodun içindeki dışa bağımlılıkların mock'lanması.
- when'de ise test metodumuzun çağrıldığı kısımdır.
- then'de sonuçta beklenen duruun olup olmadığının kontrol edildiği kısımlardır.

Bu belirtimler DSL ile yazılabileceğinden, konuşma dili ile yaızlan cümleller içerebilir. DSL'e indirgenebilmesi BDD'nin bir avantajıdır.

örnek:

```
Feature: User trades stocks
  Scenario: User requests a sell before close of trading
    Given I have 100 shares of MSFT stock
       And I have 150 shares of APPL stock
       And the time is before close of trading

    When I ask to sell 20 shares of MSFT stock
     
     Then I should have 80 shares of MSFT stock
      And I should have 150 shares of APPL stock
      And a sell order for 20 shares of MSFT stock should have been executed
```

Mockito kütüphanesinin org.mockito.Mockito sınıfının metodların isimlendirmeleri BDD'ye uygun diil. Bu sebeple org.mockito.Mockito'ile aynı işlevi gören (direkl olarak onun metodlarını aynen çağıran) bir implementasyon tasarlandı: org.mockito.BDDMockito. kaynak: (source-id: 72)

# Test-driven development (or TDD)

Önce test sonra kod yazıma gidilerek yapılan kodlama felsefesidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# MATLAB
"matrix laboratory" nin kısaltması olarak isimlendirilmiştir.

MathWorks tarafından geliştirilen sayısal hesaplama/analiz yazılımıdır. MATLAB isimli programlama dili yada diğer programlama dilleri ile çalışılabilir. 

MATLAB isimli uygulamada, microsoft acces gibi, kullanıcıyı arayüz sunan ekranlar da hazırlanabilmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# DevOps

development ve operations kelimelerinin kısaltmalarının birleşiminden meydana gelmiştir. IT'deki tüm ekiplerin (yazılım geliştirme, destek...) birbiri ile ilişkili şekilde çalışması kültürüdür. Bu kültürün oluşabilmesi için operation kısmındaki birçok işin otomatize edilmesi gerekmektedir. İşte "devops enginneer" burada devreye giriyor.

operation kısmı şu birimlerden oluşmaktadır: sistem mühendisleri, sistem yöneticileri, sürüm mühendisleri, veritabanı yöneticileri (DBAs), network mühendisleri, güvenlik uzmanları vs...

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Microsoft Azure (or old-name:Windows Azure)

Eski adı işletim sistemi sürümü gibi algılandığı için terminolojik kargaşa yaratabilir.

Microsoft'un bulut bilişim hizmetleri altında birçok hizmet vermektedir. örneğin; Windows kurulu makineler, yada windows üzerinde kurulu SQL Server yüklü hazır makineler sunulmaktadır. Amazon Web Services'a alternatiftir.

Bulut'ta yüklü Windows sürümleri özel bir Windows değildir. normal windowsa göre ufak eklemeler çıkarmalar yapılıyor olabilir. aynı durum Amazon Web Services'te böyledir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# path: canonical vs absolute and relative

örnekler:

- absolute path: C:\XyzWs\\.\TEST.TXT  -> dosya sistmeinin root'undan alınan fakat noktalama işaretleri ile yönlendirmeler alabilen path

- canonical path: C:\XyzWs\test.txt  -> dosya sistmeinin root'undan alınan fakat noktalama işaretleri ile yönlendirmeler içermeyen path

- relative path: .\TEST.TXT -> dosya sisteminin başından değilde o anda runtime sırasında bulunan dizinden itibaren verilen path'tir.

  relative path için kullanılan işaretler:

  - ./images/image1 --> bulunduğumuz dizin altındaki images klasörü

  - ../images --> bulunduğumuz dizin üstündeki dizindikeri images klasörü

  - ../../images --> bulunduğumuz dizinin 2 üstündeki dizindeki images klasörü

  - ~/images --> user'ın home klasörünün içindeki images klasörünü temsil eder. bu relative path değildir. direk olarak root'tan verilmiş bir dizin olduğundan canonical path'tir. ~ işareti sadece bir kısaltmadır.

# canonical form
bilişimde ve matematikte bir gösterim şeklidir. canonical form; "__normal form__" yada "__standard form__" olarakta adlandırılır.

canonical form'un kuralları yoktur, bir standart diildir. bir terim (matematik objesi, yada bilişimdeki herhangi bir değer(value, string...)) canonical form'da ise; canonical form'da olan herhangi bir value ile karşılaştırıldığında, eşit olup olmadıkları kanaatine varılabilmelidir. örneğin; File-path değeri canonical path ise; iki file-path'i canonical path ile karşılaştırmamız eşit olup olmadıkları bilgisini elde edebilmemiz için yeterli olmalıdır. bu sebeple; canonical form'da olan değerler; net ve ilgili objenin en basit halinde (formunda) olmalıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Uniform Resource Name (or URN)

örnek: 

- ISBN numarası: urn:isbn:096139210

- amazon servislerindeki bir kaynağın tanımı: arn:partition:service:region:account-id:resource

# URL (or Uniform Resource Locator)

örnek:

- mailto:myemail@servise.com

# Uniform Resource Identifier (or URI)

bir resource için unique id tanımıdır. URL ve URN bunun birer implementasyonudur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Library (or kütüphane) vs Framework (or yazılım iskeleti or yazılım çerçevesi or yazılım çatısı)

Library, API'lerini çağırarak işlem yaptığımız ve bazen dönüş aldığımız yazılımlardır. Framework'te ise durum tam tersidir. Framework kendi çalışır ve bizim uygulamamızdaki API'leri çağırır. Bizi kendi akışının bir parçasıymış (modülüymüş gibi) kullanır.

Örneğin; Libary; Log4J, ApacheCommonStringUtils verilebilir. Framework; Web uygulaması sistemi verilebilir: Spring, JavaEE gibi. Spring içerisinde bizim uygulamamız bir modül gibi kalıyor. Onun sınıflarını extend ederek akışlar oluşturuluyor.

# Toolkit vs SDK (Software Development Kit)

Bir kütüphaneyi yada bir framerowrk'ü kullanmak yada ondan yararlanmak için zorunlu/isteğe bağlı olarak kullanılan yazılımlardır. resmi tanım olmadıklarından; ikiside aynı anlama gelmektedir. fakat piyasada genel olarak sdk daha çok; başka bir işletim sistemi yada ortam(platform) üzerinde uygulamayı yürütmek için gerekli olan yazılımlar için kullanılamktadır. toolkit'ler ise SDK içinde yüklü gelebilirler ve daha çok opsiyonel kaynakları barındırırlar.

# yazılım (or software) vs program vs appllication (or app or uygulama)

- program ;blgisayar biliminde makineye işletilmesi için verilen talimatlardır (kodlardır).

- yazılım; proramlar grubudur.

- app; son kullanıcı ile etkileşimde olması şart olan bir yazılım çeşididir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# yorumlayıcı (or Interpreter)
Interpreter kelime anlamı: tercüman, yorumlayan

bir yazılımdır. bu yazılım kaynak kodu direk olarak yorumlar ve yorumladığı şeyleri yürütür. Kodu makine koduna çevirmek zorunda diildir. "Shell" buna en iyi örnektir. Shell aldığı komutları makine koduna çevirmez, kendisi yorumlar.

# JIT (Just-in-time) compile
Interpreter'lar gibi runtime sırasında kodu alır fakat Interpreter'lardan farklı olarak; okuduğu kodu makine koduna çevirir ve o kodu CPU'da işletir.

- JIT programlama dilinin özelliği değildir, runtime'da kodu işleten programın özelliğidir.

- JVM güncel sürümlerinde bu özelliği kullanılır.

# Ahead of time (or AOT) compiler
Ahead of time kelime anlamı: Vaktinden önce

c, c++ dilleri direk olarak makine koduna çevrildiğinden, runtime sırasında derleme işlemine gerek kalmaz ve bu sebepten daha hızlı çalışır.  bu şekilde direk makine koduna çevren compiler'lara AOT denir.

# betik dili (or script or scripting language)
Betik dili; bir environment üzerinde manipülasyon yapabilen dillerdir. kaynak: (source-id: 74) "4 Overview" başlığı 2inci paragraf.

örnekler:
- ECMAScript: web sayfası ortamında html css'lerde manipülasyon yapabilmektedir. ECMAScript ilk zamanlar, scripting language olmak için tasarlanmıştı. fakat daha sonra genel amaçlı oldu. (source-id: 74) "4 Overview" başlığı 2inci paragraf.
- shell (bash, zsh...): OS ortamında manipülasyon yapabilmektedir

Bir dili tamamiyle script dili yada script dili olmadığı söylemek çok zor. kaynak: (source-id: 423) "Stavros Macrakis (macrakis@osf.org) replied" başlığı son paragraf. + (source-id: 424) "Description" başlığı 4üncü paragraf.

# compiled language
interpreter'e ihtiyaç olmayan ve direk makine koduna çevrilen dillerdir.

# bytecode (or portable code or p-code)
yorumlayıcı gerektiren dillerde yorumlayıcının okuduğu dosyadır. JVM için .class dosyalarıdır.

# java bytecode
java kodları (.java uzantılı dosyalar) derlenir ve bytecode'a çevrilir. java için bytecode .class dosyalarıdır.

Scala, Kotlin, Clojure ve Groovy, Java diline alternatiftir ve derlendiklerinde Java'da olduğu gibi bytecode'a (.class dosyalarına) çevrilirler. Yani JVM'de run edilmek için tasarlanmışlardır.

# assembly language (or assembler language)
- En düşük seviyeli dildir.
- Makine kodu; 0 ve 1'lerin okunabilir hale getirilmesi için kullanılır. tamamı olmasada assembly, neredeyse 1:1 mapping yapılarak makine koduna çevrilebilir.
- Windows (veya diğer işletim sistemleri) üzerinde çalışan .exe (veya diğer executable) uzantılı dosyalar, hem makine dilinden hemde işletim sisteminin anlayacağı kısımlar içerir. Bu sebeple; C'de yazılmış basit bir satırlık printf satırlık kod, linuxta derlenirse FreeBSD'de, mac'te or windows'ta çalışmamaktadır. Executable formatı zaten her işletim sisteminini farklıdır.
  - linux'un executable formatı: __Executable and Linkable Format (or ELF or Extensible Linking Format)__. dosya uzantıları: .axf, .bin, .elf, .o, .prx, .puff, .ko, .mod, .so
  - ms windows2un executable formatı: __Portable Executable (or PE)__. dosya uzantıları: .acm, .ax, .cpl, .dll, .drv, .efi, .exe, .mui, .ocx, .scr, .sys, .tsp

  Zaten executable dosyaların formatları aynı olsa bile, sistem kütüphanelerinin ismi, api'leri, çağrılan api'lerin return kodları, dosyaların dizinleri farklı olacağından yine runtime'da sorun yaşayacaktık.

- Aynı işletim sistemine sahip 2 işletim sistemi olsun: Debian, Suse. Debian üzerinde bir kod derledik. Eğer kod içerisinde Suse'de olmayan bir kütüphaneye link var ise, uygulama run edilir fakat runtime sırasında hata alınır.
- Compiler'ın yaptığı şey: kodları bir dosyaya aktarmak (executable yaratmak). Bu sebeple ms-windows için, linux üzerinde derleme işlemi yapılabilir. örnek bunu yapan compiler: mingw.

# machine code (or makine kodu) vs assembly vs instruction

|                     | karşılığı  |
|---------------------|------------|
| machine code        | 1010100000 |
| Assembly            | ADD 21     |
| instruction name    | ADD        |
| instruction operand | 21         |

instruction direk cpu'nun işleteceği komuttur. dışarıdan cpu'ya iletebilen en düşük seviyeli istektir.

__instruction set__ bir cpu'nun kabul ettiği tüm instruction'ların kümesidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# WebP

Google'nin geliştirdiği resim formatı. Daha çok web sayfalarında gösterilmesi için geliştirilmiştir. bu sebeple; hızlı yüklenme ve az boyutlu olacak şekilde tasarlanmıştır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# .tar formatı

tarball adı verilen bu dosyalar sadece arşivlenmek amaçlı kullanılmaktadır. unix sistemlerinde ki dosyalar için, dosya sistemindeki bilgilerini de .tar dosyası içerisinde saklamaktadır. oysa zip gibi formatlarda sadece windows dosya sistemindeki bazı bilgiler saklanmaktadır. tar formatı sıkıştırılmadığından, genelde ek araçlarla sıkıştırılır ve dosya uzantısının yanına bir uzantı daha eklenir yada dosya uzantısı tamamen değiştirilir.

# iso formatı

iso formatı bazı dosya sistemlerinin partititon bilgileride tutmak için kullanılmaktadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# windows işletim sistemi dizin yapısı

> RECYCLED 

> RECYCLER

> $Recycle.Bin

işletim sistemi versiyonuna göre ismi değişmektedir. bölümün root dizinindedir. çöp kutusu aslında burdadır. windows çöp kutusu buradaki tüm dosyaları tek klasördeymiş gibi gösterir.

> System Volume Information

NTFS dizinlerinde root'ta bulunur. bu dizin içerisinde system restore bilgilerini, hızlı arama (index) için bilgileri, kısayol ve link edilmiş tipteki dosyaların bilgileri vs gibi bilgileri tutar.

> Program files

"C:\Program files (x86)"" 32 bit uygulamaları barındırırken, 64 bit uygulamalar "C:\Program files" dizinindedir.

> C:\ProgramData

tüm kullanıcılar için ortak data saklayabileceği dizindir. uygulamalar alt klasörler yaratarak dosya saklayabilirler.

> C:\Documents and Settings\username

Microsoft Windows 2000, XP and 2003 için home dizini

> C:\Users\username 

Microsoft Windows Vista, 7, 8 and 10 için home dizini

> C:\Users\AllUsers

C:\ProgramData dizine kısayoldur.

> C:\Users\Default

windows yeni kullanıcı açtığında buradaki dosyaları yeni user'a aktarır.

> C:\Users\Public

Tüm kullanıcılara ve networkteki kullanıcılara açık olan dizindir. kolay dosya paylaşımı yapabilmek için kullanılmaktadır.

> C:\Users\UserName\AppData\Roaming

Microsoft user syncronizing feauture sync only these files.

> C:\Users\UserName\AppData\Local
ve
> C:\Users\UserName\AppData\LocalLow

app can store files here the files which will not sync with their windows-ms-account

> C:\Windows\System

16 bit dll dosyalarını bulunduruyor.

> C:\Windows\System32

32 bit dll dosyalarını bulunduruyor.

> C:\Windows\SysWOW64

64 bit dll dosyalarını bulunduruyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# ISO (or International Organization for Standardization)

Teknik ve teknik olmayan konularda standartlar belirleyen komisyon. Sadece IEC'in (Uluslararası Elektroteknik Komisyonu) ilgilendiği konularda standart belirlemiyorlar.

ISO terimi kurumun başlığının kısaltması diildir. Yunancadaki "isos" kelimesinden esinlenilmiştir: kaynak: (source-id: 76) book: "The Illustrated Network", yazar: Walter Goralski, "ISO, or International Standards Organization" ilk paragraf.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# mantıksal analiz robotu (or yapay zeka or Artificial intelligence or AI)

bir bilgisayarın, gerçek bir düşünebilen canlı gibi davranması (insan zekasını taklit edebilme) yeteneğidir.

# yapay sinir ağı (or YSA or Artificial neural network or ANN)

yapay zeka'nın bir alt dalıdır. YSA, yapay zeka yapabilmek için bir mimaridir/yöntemdir. yapay zeka için YSA kullanılmak zorunda değiliz. onun yerine eski oyunlarda olduğu gibi araba yarışı tasarlayabilir ve diğer yarışçıların da akıllı davranabilmesini sağlayabiliriz.

# Makine öğrenimi (or machine learning)

araştırmalarının odaklandığı konu; bilgisayarlara algılama ve bir data ile kendini geliştirme yeteneğini kazandırmaktır. Makine öğrenimi yapan bir yapay zeka her zaman bir veriden kendini geliştirmek zorunda değildir. eski oyunlarda akıllı olan bilgisayar yarışçıları datadan beslenmiyorlardı. Makine öğrenimi yapay zekanın bir alt dalıdır.

# derin öğrenme (or deep learning or deep structured learning)

makine öğrenmesinin bir alt dalıdır. çok katmanlı YSA'ların kullanılmasıdır. çok katmanlı YSA'lar ile birlikte her level (katman) kendi içinde de ysa'lar barındırmaktadır. örnek: araba kullanan robot yapacağız. fonksiyonumuz araba kullanmak. fakat alt fonksiyonlarımız var: direksiyonu yönetme, acil durumlarda arabayı tamir etme gibi... İşte bu katmanlar ayrı ayrı birleştirilmektedir.

çok katmanlı YSA'ların kullanılması özellikle görüntüden resim cisim/obje ayıklama/sınıflandırma için çok uygundur. grafik kartları (GPU) lar bu konularda özel çalışmalar yapmaktadırlar.

# Bulanık mantık (or bulanık eseme or puslu mantık or Fuzzy logic)

Bulanık mantığın temeli bulanık küme ve alt kümelere dayanır. Klasik yaklaşımda bir varlık ya kümenin elemanıdır (1) ya da değildir (0). bulanık mantık ile bir varlık üyelik derecesine göre birden fazla kümenin elemanı olabilir. üyelik derecesi 0-1 arasındadır. örnek olarak sıcaklık derecesi verilebilir. belirli bir seviyedensonrasını sıcak belirli bir seviyedensonrasını soğuk olarak ele alırsak; ılık sıcaklıklar ve bazen yarı-sıcak ve ılık sıcaklıkların olduğu dereceler bulabiliriz.

# Sinaptik (or Sinaptic)

Sinaps (or Synapse) kelimesinde geliyor. Sinaps; nöronların (sinir hücrelerinin or neuron) diğer nöronlara ya da kas veya salgı bezleri gibi nöron olmayan hücrelere mesaj iletmesine olanak tanıyan özelleşmiş bağlantı noktalarıdır.

# YSA yapısı

Girişler her hücreye (or node or düğüm) geldiğinde ağırlıklar (or W or Weight) ile çarpılır. Her girişten gelen aynı derecede önemsenmeyeceği için bu çarpım işlemi yapılır.

Bütün girişler çağrıldıktan sonra sinir içerisinde bir matematiksel işleme tabi tutulurlar. Bu işlem "toplama fonksiyonu" olarak adlandırılır. Burada isim karışıklığı olabilir. BU metod sadece toplama çarpımı değildir. Herhangi bir matematiksle işlem olabilir.

Çıkan çıktı ise en son yine bir matematiksel işlemden geçer. En sonki bu işlem çıkış için bir filtre görevi görür ve aktivasyon fonksiyonu ismini alır. Burada da isim karışıklığı olabilir. "aktivasyon fonksiyonu" matematikteki özel bir fonksiyona denk geliyor. Fakat YSA'da bu fonksiyon herhangi bir işlem olabilir.

# YSA Katmanlar (or Layers)

YSA'nın ilk girdi aldığı hücreler ve son çıkışa giden hücreler arasında da hücreler olabilir. aradaki katmanlara (ilk ve son katmanlar hariç) gizli katmanlar (or ara katmanlar) denir. Dolayısı ile gizli katmanlı olan bir ağ, en az 3 katmandan oluşuyordur.

çok katmanlı ysa en az 2 katmandan oluşur.

bir YSA en az 1 katmandan oluşabilir.

# Ağın Eğitilmesi

YSA'nın eğitilmesi için doğru olarak bilinen giriş ve çıkış değerlerinin elimizde olması gerekir. YSA'ya girdiler verilir ve YSA'nın verdiği çıktı ile gerçek çıktı karşılaştırılır. İşte bu hata payına göre, W (weight or ağırlık) değerleri her işlem sonrası değiştirilir. Bu eğitim şekline geri beslemeli (or geri yayılım or back propagation) eğitim denir. Birçok farklı eğitim şekli düşünülebilir.

Ağa ilk W değerleri ya rastgele yada belli referanslara dayanılarakta atanabilir.

Test süreçlerinde YSA'nın eğitilmemesi gerekmektedir.

# Hopfield Ağları (Hopfield Net)

Aşağıdaki kurallara uyan sinir ağlarına verilen özel isimdir. Bunun gibi birçok ağ mevcuttur.

- Tüm hüclerelerde sadece 1 ve 0 değerleri giriş çıkışlarda olmalıdır

- Nöronlara gelen ağırlıklar aktivasyon fonksiyonuna gelmeden hemen önce toplanırlar

- Nöronlarda aktivasyon fonksiyonu olmalı ve eşik değeri kullanılmalıdır

Katman kavramı yoktur. Tüm hücreler diğer tüm hücrelere bağlıdır. Yani aslında tek katmanlıdır diyebiliriz. Böylece tüm girişler (hücreler) aynı zamanda çıkışları verecektir. n girişli ve n çıkışlıdır. Her bir hücre çıkışı, bir sonraki iterasyonda diğer tüm hücrelerin girişine etki etmektedir.

# iterasyon vs epoch

epoch'un türkçe kelime anlamı: devir, çağ, dönem'dir.

iterasyon YSA'nın bir kere input alıp, bir kere çıktı vermesine kadar olan süreçtir.

YSA'lar eğitilirken bir eğitim seti (giriş ve çıkış seti) olmaktadır. BU tüm set ysa'ya verilir ve ysa kendini sonuçlara göre eğitir. Tüm eğitim seti dolalışdığında bir epoch süresi geçmiş sayılır. YSA eğitiminde bazen epoch sayısını (aynı eğitim seti için) birçok kere geçmek gerekebilir.

# Basamak (or adım or step or staircase) fonksiyonu

Belirli aralıklarda sadece 1 sayıyı çıktı olarak veren fonksiyonlar grubudur. Örnek; "Heaviside step function", "signum", "Constant" bu kümenin içindedir.

# Sigmoid fonksiyonu (simge: S)

bu fonksiyon her girdi için 0 ile 1 arasında değer üretir.

f(x)= 1/1+e^(-1)

# Eşik Değer (treshold) fonksiyonları

bu bir fonksiyon grubudur. sigmoid ve basamak fonksiyonları grubun içindedir. eşik değerlere göre sonuç verirler.

# Birim fonksiyon (or özdeşlik fonksiyonu or özdeşlik gönderimi or özdeşlik dönüşümü or birim dönüşüm or birim işlev or unit)

f(x) = x

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# İşaretleme dili (or etiketleme dili or markup language)

Latex, HMTL, XML, XHTML gibi dillerdir. Bir dilin markup language olabilmesi için; parse edilip işlenmesi sonrası ortaya elektronik bir döküman çıkması gerekli. Bu dillerle bu dökümanın stili ve yapısı belirlenmektedir.

Bu sebeple Json bir markup language değildir. XML markup'tır, çünkü SVG gibi yapılarda bir döküman outputu verdiği görülür.

- Markdown
  - Çok basit bir markup dilidir. türevleri:
    - Github Flavored Markdown (or GFM). spesifikasyonu: (source-id: 77)
    - CommonMark. farklı sürümleri mevcut: (source-id: 78)
    - farklı birçok türev mevcut: (source-id: 79) "4.  Examples for Common Markdown Syntaxes" başlığında türevler listelenmiştir.
  - dosya uzantısı '.md'dir

github artık CommonMark kulanmaya başlayacak. kaynak: (source-id: 80)

- Asciidoc
  - Markdown'a göre daha gelişmiş ve fakat daha kompleks bir markup dilidir.
  - dosya uzantısı '.adoc'tur.
  - "asciidoc", "a2x", "Asciidoctor" isimli uygulamalar Asciidoc formatındaki bir dosyayı html, pdf gibi formatlara çevirmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# OpenStreetMaps (OSM)

Açık kaynaklı dünya haritası veritabanıdır. forsquare gibi firmalar bu veritabınından yararlanır. sadece veritabanı sunduğundan, API'ler ancak üçüncü partiler tarafından yayınlanır.

Opesseamaps OSM'nin içindedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Dokuman yonetim sistemleri

| name       | comment                                                                                                                       |
|------------|-------------------------------------------------------------------------------------------------------------------------------|
| confluence | Atlasian'ın geliştirdiği wiki tool'u                                                                                          |
| MediaWiki  | wikipedianın altyapısını sağlayan wiki tool'u. bu wordpress gibi hazır bir yapı. direk wikipedia gibi site oluşturulabiliyor. |
| XWiki      | open source                                                                                                                   |

# CI sistemleri

- Bamboo

Atlasian şirketinin geliştirdiği CI (Continuous Integration) tool'u.

Agent dediğimiz uygulamalar, bamboo'ya bağlanıyor. Bambo bir task yapmak istediğinde, agent makineleri (agent'ın home klasörü ve her bir task için yaratılan workspace) üzerinde çalıştırıyor ve sonucu alıyor. Bambo bulunduğu makinede bir işlem yapmıyor. Herşey agent'larda yapılıyor. Bu agent'lar; amazon sunucusunda, docker'da yada aynı makinedeki birden fazla işletim sistemi user'ında olabilir.

Bmabodaki scriptler büyükten küçüğe şu şekilde gruplandırılıyor: Plan -> Stage -> Job > Task

- alternatifler: Jenkins, Hudson

# SCM sistemleri

- alternatifler:

| name                                                  | comment                                                 |
|-------------------------------------------------------|---------------------------------------------------------|
| Atlasian BitBucket                                    | Server                                                  |
| gitlab                                                | Server (ekstra CI özellikleri içeriyor)                 |
| EGit                                                  | Eclipse plugin (default installed)                      |
| Atlasian SourceTree                                   | Client Desktop                                          |
| SmartGit                                              | Client Desktop                                          |
| GitHub                                                | web site (Proprietary software)                         |
| git-gui                                               | Default Git's Client Desktop without history/log viewer |
| gitk                                                  | Default Git's Client Desktop only history/log viewer    |
| CA Harvest Software Change Manager (or CCC/Harvest) | develop by microsoft                                    |
| Bazaar (or Bazaar-NG)                               | Server                                                  |

# SVN sistemleri

| name        | comment                                                       |
|-------------|---------------------------------------------------------------|
| Subversive  | Eclipse plugin (default installed on old versions of Eclipse) |
| TortoiseSVN | Client Desktop                                                |

# SCM, CI gibi bir yazılımın tüm hayat döngüsünü sağlayan paket yazılımlar

- Sourceforge

- Launchpad

- Team Foundation Server

  Hem localde hemde Azure'de yayımlanan sunucu versiyonları mevcut. Kendi SCM protokolünü içermektedir. İstenirse "git" yazılımıda kullanılabilmektedir. TFS sadece SCM değil, aynı zamanda birçok işlevi CI, Proje yönetimi, test hayat döngüsü gibi de içermektedir. Bir yazılım için gerekli tüm hayat döngüsünü sağlayacak altyapıya sahiptir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Systems development life cycle (or SDLC or application development life-cycle)

genel bir terimdir. aşağıdakilerin kümesini kapsar.

# Agile (Çevik) proje yönetimi

bir proje (yazılım projesi olmak zorunda diil) yönetim (işleyiş) biçimidir.  Gereksinimleri açıkça belirli olmayan, değişime açık, karmaşık projelerin yönetimi için uygulanmaktadır. agile manifestosu şu şekildedir:

türkçe:
```
Bizler daha iyi yazılım geliştirme yollarını

uygulayarak ve başkalarının da uygulamasına yardım ederek ortaya çıkartıyoruz.

Bu çalışmaların sonucunda:

Süreçler ve araçlardan ziyade bireyler ve etkileşimlere

Kapsamlı dökümantasyondan ziyade çalışan yazılıma

Sözleşme pazarlıklarından ziyade müşteri ile işbirliğine

Bir plana bağlı kalmaktan ziyade değişime karşılık vermeye

değer vermeye kanaat getirdik.

Özetle, sol taraftaki maddelerin değerini kabul etmekle birlikte,

sağ taraftaki maddeleri daha değerli bulmaktayız.
```

ingilizce:
```
 We are uncovering better ways of developing

software by doing it and helping others do it.

Through this work we have come to value:

Individuals and interactions over processes and tools

Working software over comprehensive documentation

Customer collaboration over contract negotiation

Responding to change over following a plan

That is, while there is value in the items on

the right, we value the items on the left more.
```

# Scrum
kelime anlamı: itişip kakışma, saldırı

Agile'ın bir türevidir. Sprint (kelime anlamı: sürat koşusu), backlog (kelime anlamı: rezerv, birikim), daily meeting gibi kavramlar bunun içindedir. Sadece yazılım projelerinde uygulanmak için tasarlanmıştır. Scrum'ın türkçe kelime anlamı itişip kakışma anlamına gelir fakat özel türkçe karşılığı yoktur.

Scrum temel olarak agile'a göre, sürecin nasıl işleyeceği ile ilgili detaylandırılmış şeklidir. Agile ise işin felsefik/üst seyiveyi/soyut kısmıdır. örneklerdne gidersek:
- agile'da yüzyüze iletişim olması gerektiği belirtiltilir; scrumda ise, müşteri ile birlikte çalışmak çok verimli olduğu belirtilir.
- Agile'da iterasyonlarlar bahsedilir, scrumda sprint ile detaylandırılmıştır.
- agile'da visualizing önemli denir, scrumda, scrum board'dan bahsedilir.

sprint içerisinde analistler her zaman yeni sprint belirmeden önce analizleri hazırlamış ve teknik ekibe yollamış olmalı. teknik ekip retro-toplantısı ile yeni sprint puanları verilmeden önceki arada bunları okumalıdır.

Scrum'ın yıllar içinde klavuzu güncellenmektedir. akışta ve ifadelerde değişiklikler yapılmaktadır. 2020 sürümü buradadır:

(source-id: 81)

(source-id: 82)

Diğer sürümlerdeki değişikler burada: (source-id: 83)

# Scrum çalışmalarında geçen kavramlar

# scrum'daki kişiler

- __scrum master__: sadece scrum sürecini ve teknik olmayan konularda yaşanan engelleri çözmek için ilgili kişidir. bu kişi; taskların içeriği değilde, scrum süreçinin işlediğinden emin olmalıdır.

- __project manager (proje yöneticisi)__: bazı agile sistemlerde bu role varken, bu rolde bir kişi scrum'da yoktur. çünkü srum'da takım self-organized'dır.

- __team leader (or takım lideri)__: klasik proje yönetimlerinde bu vardır. scrumda böyle bir role yoktur. çünkü team self organized'dir.

- __scrum team__: product owner, scrum master ve development'lardan oluşan kümedir.

- __development team__: 2020 yılı sürümünde sadece "__developers__" olarak adlandırılır. sprint içerisinmdeki taskları yapacvak olan kişilerdir. alt kümelere ayrılamazlar. eğer ayrılması gerekiyor ise, farklı/bağımsız bir scrum takımı kurulmalıdır. analistler ve testçiler dahil ayrı grup olarak görülmemelidir.

  3'ten az veya 9'dan fazla kişi olması tavsiye edilmez.

- __product owner (or PO or ürün sahibi)__: tüm kararlardan/araştırmalardan sonra en son ürün için yapılacak taskları onaylayan, üründe hangi geliştirmeleri yapılacağını söylemeye yetkili kişi. PO sürekli müşteri ile temas halindedir. müşterinin isteklerini anlar ve backlog'daki tasklara businnes value'ları set eder. backlog'daki tasklardaki istekleri yazar/detaylandırır. teknik bilgisi olan kişi değildir. sadece businnes odaklıdır.

  PO tüm işlerini development team'e de yaptırabilir. fakat sorumlulukları ona aittir.

  sprint iptalini sadece product owner verebilir. fakat stackeholder'lar, scrum master ve geliştirici takımda bu kararı yönlendirmede etkili olabilir. sprint iptal edilirse, yarım kalan tüm tasklar gözden geçirilir ve yeni sprint'e başlamak için gerekli toplantılar ayarlanır.

  sprint sonlarındaki DEMO'lar product owner'a yapılır.

# scrum events
retropektif, grooming gibi toplantıların tümünü kapsayan kümedir. her toplantı mutlaka önceden belirlenmiş kısıtlı sürelerde (time-boxed) yapılmalıdır.

- __sprint__: 1 aydan uzun olmamalıdır.

- __sprint planning (or Sprint Planlama)__: bu toplantıda:

  - hangi taskların başlayacak olan sprint'e alınacağı belirlenir.
  - eğer bilinmiyorsa yüzeysel olarak o işlerin teknik anlamda nasıl/ne şekilde yapılacağı belirlenir.
  - her task için yapılmamış ise "Defination of done" belirlenir.

  Bu sorular sprint planning'de cevaplandırılmalıdır:

  - Bu Sprint Neden Değerlidir? (bu 2020-November tarihli scrum sürümünde geldi)
  - Bu Sprint’te ne tamamlanabilir?
  - Seçilen iş nasıl yapılacak?

  1 aylık sprint için 8 saat ile sınırlıdır. daha kısa sprint'ler için daha kısa olmalıdır.

- __günlük toplantılar (or daily scrum meeting)__: her gün yapılmalıdır. sadece; dün ne yaptım, bugün ne yapacam ve engelim varmı konuşulmalıdır. toplam 15 dk olmalıdır.

- __sprint review (or sprint değerlendirme)__: bu toplantı herkesin katılabileceği bir toplantıdır. sprint sonunda yapılır. biten her taskın demo'su yapılır. sprint içerisinde hangi engellerle karışalıldı, nasıl çözüldü konuları tartışılır. biten tasklar ile ilgili sorular varsa onlar cevaplanır. scrum team ve stackeholder'lar genel görüşlerini bildirir. stackeholder'lar; scrum team'i dışında kalan ve ürün hakkında yorum, öneri yapabilen tüm kişilerdir.

  bu toplantının scrum terminologisinde resmi bir yeri yoktur.

  1 aylık sprint için max 4 saat olmalıdır. daha kısa sprinmt'ler için daha kısa olmalıdır. 

- __retrospective (retrospektif) toplantısı__: retrospektif kelime anlamı: 'dünden bugüne', 'geriye dönük'. her sprint sonu takımın ve scrum master'ın toplanarak yağtığı başarısızlıkları ve başarıları konuştukları toplantı. 3 saat veya daha az olmalıdır. burada hem teknik hemde scrum süreci hakkındaki değerlendirmeler yapılır. fakat ideal olan scrum/agile süreci hakkında konuşmaktır. fakat teknik konulara da girilmez diye kural yok. süreç ne kadar başarılı gitsede her süreçte geliştirme amaçlı şeyler konuşulmalıdır. aksi durumda iyiye gidiş olmaz. bu toplantıda herkes şu 3 başlıkta maddeleri toplar:
  - neleri daha iyi yapabilirdik?
  - neleri iyi yaptık?
  - neleri kötü yaptık?

  bu toplantıya sadece 'scrum team'in katılması beklenir.

  'Sprint Değerlendirme'den sonra ve 'Sprint Planlama'dan önce yapılır.

- __Product Backlog refinement__: 

  refinement kelime anlamı: iyileştirme.

  bu toplantı __Grooming toplantıları__ olarak kullanılıyor fakat bu yanlış. "grooming" kelime anlamı: prepare or train (someone) for a particular purpose or activity.

  Product Backlog refinement, resmi olarak scrum doc'unda yazıyor fakat "scrum events" bağlığı altında diil.

  bu toplantıda backlog'daki herhangi bir item için süre ve detay verilir.

  süre olarak tüm ekibin sprint zamanının %10'unu aşmamalı.

# scrum artifacts (or scrum eserleri)
- __increment__: tüm projenin hayatı boyunca hedefe ulaşmak için yapılan her katkıya denir. somut bir adım olması şarttır. __Done (or bitti)__ olmayan iş increment olamaz. increment, kağıt üzerinde sayılabilen bir değer diildir.

- __Product Backlog (or ürün iş listesi)__: Product Owner tarafından yönetilen sprint dışındaki tüm task'lar kümesidir.

- __sprint backlog (or spint iş listesi)__: sprint içerisindeki tüm iş listesi kümesidir.

# scrum için diğer terimler

- __Planning poker (or Scrum poker)__: ekipçe her taska süre verirken uygulanan bir tekniktir. herkes kapalı kağıtları ile her taska süre verir.

  resmi scrum doc'unda geçen bir terim diildir.

- __çapraz fonksiyonlu takım (or cross-functional team)__: farklı becerilerde/alanlardan geliştiriciler olabilir ve hepsi birlikte sprint'in amacına ulaşabilmesi için yeterli olmalıdırlar. "cross functional" terimimi farklı becerilerde insanlar olması gerektiğini belirtmektedir. çünkü scrum takımı dışarıya bağımlı olmamalıdır. sprint'im amacı için gerekli tüm yetkinliğe sahip olmalıdır.

  çaprazdan kasıt şu diildir: development team içindeki her kişi, diğer herkesin işini yapabilecek yetkinlikte olmalıdır.

  resmi scrum doc'unda geçen bir terimdir.

- __Businnes Value__: iş önceliği. product owner'ın karar verdiği değer. product owner için iş ne kadar önemli.

  resmi scrum doc'unda geçen bir terim diildir.

- __Story points__: estimation ve işin zorluk (komplekslik) değeri çarpımıdır. alabildiği değerler: Fibonacci-like değerleridir: 0, 0.5, 1, 2, 3, 5, 8, 13, 20, 40, 100. Daha yüksek değer verilmemelidir. eğer daha yüksek değer vermek gerekiyor ise; sub-tasklara bölünmelidir. bug veya teknik elemanların açtığı task'larda story point olmalıdır. sonuçta product owner onaylıyor ve bunlar sprint'te çalışılıyor.

  resmi scrum doc'unda geçen bir terim diildir.

- __story point vs hour__: bir işin ne kadar süreceği net olarka belli olmaz. bu sebeple karşılaştırma tekniği ile ölçüm yapılması alternatif bir çözüm olarak sunulmuştur. story point'i karılaştırma değeri olarak  alırız. her sprint bir önceki sprint'te alınan toplam story point ile karşılaştırılarak her taska story point atanır. birçok agile master'ı projelerde saat yerine, story point ile değerlendirildiğinde, bir süre sonra story point'lerin saate göre daha doğruyu yansıttığı gözlemlenmiştir.

- __Estimation__: işin bir kişi tarafından bitirilmesi süresidir. resmi scrum doc'unda geçen bir terim diildir.

- __Burn-down Chart__: resmi scrum doc'unda geçen bir terim diildir. spring içerisinde kalan işleri gösteren grafiktir.

- __Burn-up Chart__: resmi scrum doc'unda geçen bir terim diildir. sprint içerisinde biten işleri gösteren grafiktir.

- __Definition of Done (or DoD)__: resmi scrum doc'unda geçen bir terimdir. bir taskın kapanması için gerekli tüm definitionlar. burada o taskın production'a çıkması için gerekli tüm bilgiler olmalıdır.

- __spike__: spike kelime anlamı: sivri uç. bazı taskların çıktısı olmaz ve ya olması için önce araştırma gerektirir. bu araştırma tasklarına verilen genel isimdir.

# The Chicken and the Pig
It is a business fable. It was also mentioned in the official "Scrum Guide" but it has been removed.

The chicked and pig decided to open a restaurant. They both should serve a food to customer as partners. the chicked had to serve his eggs and the pig had to serve meat which will be part of itself. In the bottom line; The Chicken is involved, but the Pig commits. This situation is simulated on scrum framework as: the Development Team, Product Owners & Scrum Masters are considered as people who are committed to the project while stakeholders, customers and executive management are considered as involved but not committed to the project.

# Kanban

Agile'ın bir türevidir. Sadece yazılım projelerinde uygulanmak için tasarlanmıştır.

Kaban, scrum ile karşılaştırıldığında;

kambanda; toplantılar ve belirli aktiviteler bulunmamaktadır. Fakat yaşanan darboğaz durumlara göre aksiyonlar alınmaktadır. Her projede, süreç kendini geliştirmektedir.

kambanda; Yazılımcıların estimation vermesi opsiyoneldir.

kambanda; Agile'daki gibi roller (scrummaster gibi) belirlenmemiştir.

Kambanda; iterasyon opsiyoneldir. Agile'da sprint (iterasyona denk geliyor) zorunludur.

# Extreme programming (or XP)
Agile'ın bir türevidir. Sadece yazılım projelerinde uygulanmak için tasarlanmıştır. Bu metodda kaliteli kod ön plandadır. Gerektiğinde ufak/büyük refactoring'ler yapılmalıdır. Merkezde sürekli çalıştırılabilir kod olmalı ve ufak ufak parçalar halinde geliştirmeler yapılıp bu koda eklenmelidir. Testler kodda önce yazılmalıdır. Basit tasarım ve kodlama standardı gibi kavramlara önem verilir.

# WaterFall Model (or Şelale modeli)
Kod baştan sona analize göre tasarlanır ve müşteriye teslim edilir. Günümüz şartlarına pek uygun değildir. Zira tüm yazılım detaylandırılması önceden uzun bir zaman ve maliyet alması bir yana, analiz sürecinde de gelişmeler meydana gelmektedir. Bunları o süreçte yakalama ve ona göre analiz yapmak neredeyse imkansızdır. Aynı zamanda müşteri bazen ne istediğini tam olarak bilemez. Geliştirme sürecine müşteri katılır ve zaman ile gelişimini inceler ise (diğer modellerde olduğu gibi), ürün teslimi sonunda müşterinin beklenmedik şeylerle karşılaşması zorlaşır.

Tüm proje boyunca bazen proje önmeli süreçlere bölünebiliyor (scrum'daki sprint sonu gibi). bu noktalara waterfall modelinde; milestone (kilometre taşı, dönüm noktası) diye isimlendiriliyor.

# Lean software development (or yalın yazılım geliştirme)
Lean ürün geliştirme süreci ilk olarak Toyota firmasının üretim bölümünde kullanılan kültüre verilen isimdir. Daha sonra Mary Poppendieck ve Tom Poppendieck 2003'te yazdıkları "lean software development" kitabında bu konu yazılıma uyarlandı.

Lean prensipleri genel olarak optimize çalışmaya dayanan, sadec egerekli işi yapmaya odaklı (kullanılmayan özellikler içermeyen) üretim sistemlerine dayanır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# plug-in (or plugin or add-in or addin or add-on or addon or extension or uzantı or eklenti)

Hepsinin kelime anlamı aynıdır. Yazılım dünyasında işlevlerin farklılığını belirten bir standart yoktur. Her yazılım, ona yazılacak eklentinin çeşidini kendi rastgele karar vererek isimlendirir. Örneğin firefox; eklentilere add-on derken, chrome extension diyor. fakat iki tarayıcıda adobe flash tipindeki eklentiler için plug-in kelimesini kullanıyor.

Uzantı kelimesi farklı anlamlara da gelebiliyor. Uzantı bir dosya formatının, dosyadaki kısa adıdır. Bazı yazılımların eklentilere uzantı demesinin sebebi de burda geliyor. Çünkü eklentilerin setup dosyalarının uzantıları, o yazılıma eklenti kurmaya yarıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# OS/2

IMB ile Microsoftun çok eskiden birlikte geliştirdikleri işletim sistemi. Daha sonra sadece IBM geliştirmelere devam etmiş, fakat sonrasında IBM'de geliştirmeyi tamamen kesmiştir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Critical section

Paralel execute edildiğinde dead-lock olabilecek bölgeye verilen özel isim.

# race condition

birden fazla thread'in olduğu yazılımlarda aynı kaynaklara eriştiklerinde bazen sorunlar olabiliyor. aynı anda datayı değiştirdiklerinde diğeri bunu görmüyor vs.. Fakat bu durum her test yapıldığında olmuyor. çok nadiren yada her zaman olabiliyor. bu tarz hatalarda kodun, race condition'ı sağlanmadığı söylenir.

# Mutex (or Mutual Exclusion or Karşılıklı dışlama) vs Semafor (or Semaphore)

Semafor kelime anlamı: ulaşımda kullanılan işaret

sadece 1 işlemin o anda belirtilen kod bloğu içerisinden geçmesini sağlar. Oysa semaforlarda bu limit 1 den fazla olabilir. Semaforlarda örneğin en fazla 10 kişi sunucuya bağlanacak diğerleri sırada bekleyecek denilebilir.

# binary Semaphore vs counting Semaphore
binary; mutex gibi sadece 1 işlemin o anda belirtilen kod bloğu içerisinden geçmesini sağlar. counting Semaphore'da bu sayı birden fazladır.

binary Semaphore ve mutex aynı işi görür. fakat yapısal olarak farklıdırlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# JNI (or Java Native Interface)

Java ile native kod'u çağırma ve native kod'dan javayı çağırma işlemlerinin yapılabilmesini sağlar. aşağıdaki örnekte görüldüğü gibi navite keywordu ile başka dilden metod çağırmaktayız.

```java
public class Native {

        static {

                System.loadLibrary("native_library");

        }

        public static native int sum(int x, int y);

        public static void main(String[] args) {

                System.out.println(sum(3, 5));

        }

}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Inter-process communication (or IPC)

İşletim sistemleri üzerinde yürüyen işlemlerin birbirleri arasında haberleşme (uzak metod çağırma işlemi dahil) mekanizmasıdır.

# DBus (or D-Bus)

Açık kaynaklı bir IPC kütüphanesidir. Birçok implementasonu ve default bir implementasyonu vardır.

# Unix-domain socket

IPC için uygulamalar birbirlerine veri trasnfer ederken; örneğin; localhost:7011 üzerinden de haberleşebilir. fakat bu best practice'lere uymaz. 3 sebepten;

- TCP/IP soket kuralları ile bu işin olması tercih edilmeyebilir

- 7011 portuna herkes istek yapabilir. bu güvensizdir.

- IPC metodları localhost'ta daha hızlı çalışır. localhost/loopback işlemlemleri zaman kaybettirebilir.

IPC işlmelerinde unix-like'larda "unix-domain soket" kullanılır.

# dbus

her yazılım kendi içinde dışarıya birçok path (servis grubu açabilir). her path tüm işletim sisteminde uniqeu olmalıdır. bu path'lerin her biine bus denir. örnek:

> /com/appname/account

yukarıda account servisi var. bu servis içinde birçok parametre alan metod olabilir.  

örnek java d-bus kodu:

```java
import org.freedesktop.dbus.DBusInterface;

public interface ReceiveInterface extends DBusInterface {

   public int echoMessage(String str); // "member" terminolojik adı.

}
```

main app code:

```java
try {

    DBusConnection conn = DBusConnection.getConnection(DBusConnection.SESSION);

    conn.requestBusName("com.myapp"); //bu tüm OS'ta unique olmalı. bu değeri d-bus kendi içinde kullanıyor.

    conn.exportObject("/com/myappname/accounts", new JavaReceive()); //we export a service here. JavaReceive burada "object" deniliyor.

} catch (DBusException e) {

    e.printStackTrace();
}
```

send signal:

```java
Message message = new Message("/remote/object/path", "MethodName", arg1, arg2);

Connection connection = getBusConnection();

connection.send(message);
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Oyun moturu (game engine)

oyun geliştirmek için directX, opneGL gibi framework'lerin üzerine daha hazır API'ler sunarak, oyun yazılımını hızlandırmak amaçlı yazılmış kütüphanelerdir. Game engine'ler içerisinde audio engine, Physics engine, yapay zeka gibi API'ler bulundururlar.

# rendering engine vs game engine

Oyun içerisindeki modeller (insan, araba gibi) modelleri ve API'leri oyun motorları bulundurur. Fakat bunları derleme işlemleri için render engin'e ihtiyaç vardır. Render engin opengl, directX olabilir fakat embbed bir renderda içerebilir, yada belirli kısımları kendi derleyip bazı kısımları cross-rendered da tasarlanmış olabilir.

# Unreal vs Unity vs Source

Cross platform (çapraz platform) kapalı kaynak oyun motorlarıdır. Source Engine, Valve firması tarafından geliştirilmekte ve Counter-Strike, Half-life gibi oyunlarda kullanmıştır.

# Unity Web Player

Geliştirilimi durdurulmuş bir tarayıcı eklentisidir. BU eklenti ile Unity oyunları  tarayıcı üzerindeki sayfalardan direk oynanabilmektedir.

# Quake

Quake oyununda kulla ıldığı için ismi aynı olan, açık kaynaklı oyun motorudur.

# Render Engine

Önceden tasarlanmış modelleri işleyerek arayüze sunan uygulamadır. HTML rendering ve graphic rendering gibi birçok çeşit render sayılabilir.

# Blender

Açık kaynaklı 3d modelleme yapılması sunan tool'dur. "Blender Game Engine" de içermektedir. "Autodesk 3ds Max"'e alternatiftir.

# graphic engine

genel bir tanımdır. "Window system" yada opengl bu tanıma uymaktadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# on-screen display (or OSD)

bir yazılımın üzerinde açıldığı zaman ekranın her zaman önünde duran pencere yapısına verilen genel isimdir. örneğin; işletim sistemlerinde yada TV'lerde, ses açılıp arttırıldığında ekranda çıkan ses göstergesi OSD'dir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Opt-out vs Opt-in (or Double Opt-in)

izinli pazarlama (reklam mail/sms'leri yapma) altındaki kavramlardır.

opt-out; kullanıcının onayı alınmadan reklam içerikli email gönderilebilir, ancak kullanıcı dilediğinde, çok kolay bir şekilde mail/sms listesinden çıkabilir, anlamına gelmektedir.

opt-in ise; kullanıcıya önceden izni alınmadan hiçbir reklam gönderilemez. kullanıcı reklamları kabul ederse, tekrardan istediği zaman çıkabilmesi gereklidir.

opt-in ve opt-out terimleri en çok reklam sms ve emailleri için kullanılsada, genel olarak herhangi bir 'hizmet/servis' içinde kullanılabilir. 

- opt ingilizcede 'tercih etmek' anlamına geliyor
- opt-out ingilizcede 'ayrılmak/vazgeçmek' anlamına geliyor

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Chromecast

Google'ın geliştirdiği bir cihaz. USB bellek boyutundaki ufak cihaz, USB girişi şekilde HDMI girişi mevcut. HDMI girişini direk televizyona bağlıyoruz. Bu şekilde televizyonda akıllı-TV özelliği olmasa bile, chromecastin içerisindeki işletim sistemini HDMI aracılığı ile kullanmaya başlıyoruz. Cihazın USB girişi de mevcut. BU girişi ile cihazı aynı zamanda paralelden elektrik alması için beslemek gerekiyor.

chromecast içerisindeki işletim sisteminde uygulama çalıştırılmıyor. chromecast ile aynı wi-fi'deki herhangi bir cihazın içerisindeki uygulama, chromecast'e istediği ekran görünütüsünü ve sesi aktarıyor. chromecast'e ekran görüntüsü atan yazılımlar: android, ios, chrome-os, chrome eklentisi ile google-chrome.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Jasper Reports

Jasper report; raporun bir kere tasarlanması, çıktının ise dilediğiniz formatta (pdf, xml, csv, txt, vs.), kodda veya tasarımda değişiklik yapmadan üretilmesini sağlayan sistemdir.

Raporlar belli bir formatta hazırlanır. Bu raporlar dilediğimiz formatta runtime sırasında çıktıyı verirler.

JasperReports ve iReports'un geliştiricileri daha sonra birleşerek JasperSoft isimli profesyonel bir şirket kurdular ve şu an Jasper Reports konusunda danışmanlık veriyorlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# bitwise operators
| Operator | Name                                                                   | Description                                         | Usage Example |
|----------|------------------------------------------------------------------------|-----------------------------------------------------|---------------|
| &        | AND                                                                    | Sets each bit to 1 if both bits are 1               | 5 & 1         |
| \|       | OR                                                                     | Sets each bit to 1 if any of the two bits is 1      | 5 \| 1        |
| ~        | NOT                                                                    | Inverts all the bits                                | ~ 5           |
| ^        | XOR                                                                    | Sets each bit to 1 if only one of the two bits is 1 | 5 ^ 1         |
| <<       | left shift (or zero-fill left shift)                                   | (read below)                                        | 9 << 1        |
| >>       | right shift (or signed right shift or arithmetic right shift)          | (read below)                                        | 9 >> 1        |
| >>>      | unsigned right shift (or zero-fill right shift or logical right shift) | (read below)                                        | 9 >>> 1       |

not: "left shift" ile "right shift" birbirinin tersi yönlü işlemler diildir. Aşağıda detayları açıklanmıştır.

Her programlama dili ve her veri yapısı signed bit'i (positif veya negatif için kullanılan bit) kullanmıyor olabilir. Bu sebeple her dilde bu başlıkta bahsedilen shift operatörlerinin tümü olmaz.

# Left shift (<<) («)
c++'ta bu işaret 2 farklı amaç için kullanılıyor. bir tanesi burada yazan.

soldaki operatörü bit bazında sola doğru kaydırır. kaydırma işlemi; ikinci operatörde belirtilen sayı kadar gerçekleşir. bu durumda en sol'daki (leftmost) değerler yok olur (discard edilir). Sağda yeni oluşacak değerler ise "sıfır" değeri ile doldurulur.

Bu işlem Non-circular shifting'dir. Yani leftmost değer, rightmost'a transfer olmaz.

Bu işlem sonrası ilk-operator, ikinci-operator'ün iki katının üssü kadar artar. Yani; 6 << 3 = 6 * (2)^3'tür. (not: shift edeceğimiz operatör'ün max basamak sayısında değer var ise o zaman bu üs hesaplaması geçersiz olacaktır.)

# Logical right shift (>>>)
'Left shift'in sağ yöne olan tersidir.

Bu işlemin tersine ihtiyaç olmayacağı için (gereksiz olduğu için), <<< işlemi yoktur. 

# Arithmetic right shift (>>) (»)
c++'ta bu işaret 2 farklı amaç için kullanılıyor. bir tanesi burada yazan.

\>>> işlemi ile çok benzerdir. Tek farkı, padding yaparken sıfır kullanmaz. Onun yerine 'most significant bit (or MSB)'i kopyalar ve padding olacak yerlere yapıştırır. "Two's complement" (başka başlıkta anlatılıyor) representation'una göre daha doğru sonuç verecek şekilde çalışmaktadır. Örnek:

-2,147,483,552 >> 4 = -134,217,722

(denk gelen aynı işlem: -2,147,483,552 / (2^4) = -134,217,722 )

Yani; 
```
10000000 00000000 00000000 01100000 (-2,147,483,552) ("Two's complement" formatında)

11111000 00000000 00000000 00000110 (-134,217,722) ("Two's complement" formatında)
```

-2,147,483,552'da ilk bit negatif numarayı temsil ediyor. Bu sebeple; 4 adet "1" sol tarafa padding olarak geldi. Eğer pozitif sayı olsaydı, yani; 'most significant bit (or MSB)' "0" olsaydı, o zaman 4 adet "0" padding olarak gelecekti.

# all operators
| Operator                        | Symbols and examples                                                                  |
|---------------------------------|---------------------------------------------------------------------------------------|
| Post-unary operators            | expression++ , expression--                                                           |
| Pre-unary operators             | ++expression , --expression                                                           |
| Other unary operators           | - , ! , ~ , + ,                                                                       |
| Multiplication/division/modulus | * , / , %                                                                             |
| Addition/subtraction            | + , -                                                                                 |
| Shift operators                 | << , >> ,  >>>                                                                        |
| Relational operators            | < , > , <= , >= ,  instanceof                                                         |
| Equal to/not equal to           | == , !=                                                                               |
| Logical operators               | & (Bitwise AND) , ^ (Bitwise exclusive OR) ,  \| (Bitwise inclusive OR)               |
| Short-circuit logical operators | && (Conditional-AND), \|\| (Conditional-OR)                                           |
| Ternary operators               | boolean expression ? expression1 : expression2 (shorthand for if-then-else statement) |
| Assignment operators            | = , += , -= , *= , /= , %= , &= , ^= , \|= , <<= , >>= , >>>=                         |

# implementation of some functions for bit-wise operations

- returns the i'th bit of number

```java
int getBit(int num, int i) {
  int temp = num >> i; // shift the bit to first index.
  return temp & 1; // 1 = 00000001
}

// test
getBit(0b110, 1) == 1 // i=1 means the second index, 0 is the first index.
```

- set bit as 1

```java
int setBit(int number, int index) {
  return number | (1<<index); //eturns the new value
}
```

- set bit as 0

```java
int clear(int number, int index) {
  int mask = ~(1 << index);
  return number & mask;
}
```

# ternary operator
ternary kelime anlamı: üçlü, üç parçadan oluşan

programlama dillerinin desteklediği bir syntaxtır. if bloklarını bu şekilde yazabilmemizi sağlar:

```js
var y = x === 4 ? `4'e eşit` : `4'e eşit değil`;
```

# unary operation
unary kelime anlamı: birli, sadece 1 parçadan oluşan

Sadece bir operand'a sahip olan operasyonlara unary operation adı verilir. 

```c
++x;
x--;
```

# unary function
Sadece bir argüman alan fonksiyonlara unary function adı verilir.

```js
var func = x => x + 1;
```

# n-ary function and operations
- unary (or monadic)
- binary (or dyadic)
- ternary (or triadic)
- quaternary (or tetradic)
- Quinary (or Pentadic)
- Senary (or Hexadic)
- Septenary (or Hebdomadic)
- Octonary (or Ogdoadic)
- Novenary (or Enneadic or nonary)
- Denary (or Decadic or decenary)

şeklinde devam etmektedir.

birden fazla parametre alan tüm function'lara __Multary (or multiary or Polyadic)__ denir.

hiç parametre almayan fonksiyonlara __niladic function (or nullary function or 0-ary function or zero-airy function)__ denir.

# constant function (or sabit fonksiyon)
her zaman aynı değeri döndüren fonksiyondur.

# Arity
(bu kelimenin direk olarak türkçesini bulamadım.)

matematik veya yazılım dünyasında; bir fonksiyona geçilen parametre sayısıdır.

# statement vs expression
Expression ve statement terimleri dilden dile değişiyor. kaynak: (source-id: 84) title: "1.4.1 Expressions", 1st paragraph.

Fakat genelde; "statement", kod dosyasında gördüğümüz her satıra denk gelmektedir. genelde noktalı virgül ile ayırırız. "expression" ise; en az 1 operator ve 1 value'dan oluşan parçadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Amazon Elastic Compute Cloud (Amazon EC2)

Amazon firmasının, Amazon Web Services (AWS) isimli hizmet gruplarından bir tanesidir. Uzak masaüstü ile bağlantı yapılabilen sunucular (sadece makina) sunuyor. Bunlardan sistem gücüne göre saatlik ücret alıyor. Bu makineler üzerindeki HDD partitionlarının backup'ları anında alınabiliyor (Amazon Machine Image - AMI) ve tekrar kullanılabiliyor - public olarak dağıtılabiliyor.

Amazona ücret ödendikten sonra verilen kullanıcı ve şifre ile uzaktan Amazon API ‘leri kullanılarak programatik olarak yeni makine yaratıp kapatılabiliyor. Bu şekilde gereksiz makinalar kapatılarak ücretten kar edilmiş olunabiliyor.

# Regions and Availability Zones

Amazon belirli bölgeler arasında sunucularını birbirinden bağımsız tutmuş (maaliyet gibi sebeplerden). Bu sebeple bu bölgeler arasındaki makinelerdeki haberleşme normal internet üzerinden yürümekte, bu sebeple daha yavaş haberleşme olmaktadır. Backup alma işlemleri kısıtlı yürüyebilmektedir gibi.

# Elastic Beanstalk

AWS'nin bir alt hizmetidir. Heroku alternatifi bir sistemdir.

# amazon networks:

büyükten küçüğe doğru:

- region (asia vs…): maliyetten düşülmesi için amazon coğrafik konum olarak  yerlerde biribrindenbağımsız sistemler kurmuş. biz bunlar arasındaki sanal ortamlara erişmke istediğimizde, makinelerimizin public ip'lerimizi kullanmamız şart.

- vps (or Virtual Private Cloud): Amazonun bulutta diğer network'lerden izole şekilde kullandırttığı network kümesidir. Amazon bulut makinaları subnet'lr altında gruplanır. Bu subnet'ler birbirine erişebilir. Fakat bu subnet'ler gruplandırıldığında VPC'ler altında toplanırlar ve birbirlerine erişemezler. VPC kısaltması birçok farklı ismin kısaltması olduğundan bazı yerlerde karışıklığa sebep olabilir.

- availibity zone

- subnet

# elastic ip

elastic ip kullanıcının makineye atadığı public ip'dir. makine yeniden oluşturulduğunda değişmez. "public ip"' ise her makine yeniden oluşturulduğunda değişir.

# security group

varsayılan olarak tüm makinelerin tü portları dışarıya kapalıdır. elle kullanıcı rule tanımlamalıdır. tanımlanan bu rule'lar gruplar altında toplanmaktadır. bu grubun ismi security group'tur.

# Network Interface

her makinada en az bir tane olmak üzere Network Interfaces attach olmuş olmalıdır. bu network kartı'dır. Bir makine yarattığımızda default Network Interface tanımlanır. bu interfaceyi direk başka bir cihaza atach edebiliriz. default ismi eht0'dır.

# device farm

amazonun mobil uygulamalar için test servisi. verilen testleri istenilen tüm cihazlarda koşmaktadır. sonuçları videolu şekilde kaydetmektedir. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# DSL (Domain Spesific Language)

Kendi programlama dilinizi özel bir iş için geliştirdiğinize bu dil DSL olur. DSL sayesinde belirtilen syntax'ta ki yapılar, programlama diline çevrilir ve işlenir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# serverless

sunucu tarafta, businnes logic'i dışındaki işlerle ilgilenmemek için güvenlik, oturum yönetimi, ölçeklendirilebilirlik, kurulum konfigürasyonları, ağ yönetimi gibi konular için dışardan hazır hizmet alınması tercih edilmektedir. bu da servlerless mantığını ortaya koymuştur. isminden server olmama gibi anlaşılabilir, fakat olay bu değildir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Omniture vs Google Analitics vs CoreMetrics

Piyasada en çok tercih edilen istatistik toplama ve analiz etme sistemleri. Geliştirilen yazılımda, son kullanıcının yaptığı her aksiyon bu sitelere belirli formatlarda yollanıyor. BU siteler ise, bu bilgilerle ilgili istatistikleri yazılımcılara sunuyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Xray

Test yönetimi sunan Jira eklentisi. ‘Test execution', ‘Test' gibi issue tipleri yaratıp bunları arayüzdendüzenlemeyi sunuyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Selenium

web sayfaları testi için kullanılan yazılım paketleri.

# Selenium IDE:

Firefox eklentisi. Bu araç kullanılarak tarayıcı üzerinde elle yapılan işlemler script'lere dökülebilmektedir. IDE eklenti desteklemektedir.

# Selenium Client

Programlama dilleri için geliştirilen API. Test scriptleri herhangi bir dilde yazılıp, execute edilebilir.

# Selenium WebDriver

API üzerinden yapılan istekler web-driver tarafından execute edilir (tarayıcıda çalıştırılır). Bu yüzden webdriver browser spesific yazılmaktadır. Selnium Web driver'ına gelen istekler sadece Selenium API ile olmayabilir. Aynı komutları kim gönderirse, uygun cevap dönülmektedir.

# HtmlUnit

Selenium'un geliştirdiği simülasyon tarayıcısıdır.

# SeleniumGrid (or Selenium Standalone Server)

birden fazla web driver olan test makinesi yönetimi içi kullanılan yapının genel ismidir. java ile yazılmış bir uygulama mevcut. bu uygulama ya sunucu yada node rolünde başlatılabilmektedir (ikiside tek executable). sunucu bir adet olmalıdır (seleniumHub). node'lar ise istenildiğikadar olabilir ve sunucuya attach (register) olmaları gereklidir. Tüm test istekleri Hub'a gelir. Hub ilgili yönlendirmeleri uygun node'a havale eder. Bu şekilde birçok test paralelden çalıştırılabilir.

bir selenium node'unun konfigürasyonlarına webdriver dizini verilmelidir. bu şekilde ilgili node, hangi tarayıcıların driver'lerini çalıştırabiliyorsa, o testleri üzerinde yapmaya hazır şekilde bekler.

# Selenium RC

Eski sürüm selenium'larda kullanılırdı. WebDriver yerine bu vardı.

# SeleniumGridScaler

selenium-grid'in eklenti altyapısı mevcut. pom.xml'e selenium-grid eklenirse, bu sınıflardan yararlanarak bir java projesi oluşturulursa bu java projesi artık bir eklenti olmuş olacaktır. selenium-grid başlatıldığında, SeleniumGridScaler'ın install edilmiş hali (jar) class-path'e verildiğinde SeleniumGridScaler'ın kodları da yürütülmektedir.

SeleniumGridScaler eklentisi ile amazon AMI'leri üzerinde node'lar sadece ihtiyaç olduğunda açık tutulurken, ihtiyaç olmadığında kapatılıyor. bu şekilde maliyet kazancı sağlıyor.

# RemoteWebDriver

webdriver'dan extend etmiş bir sınıftır. uzakta driver servlet'i var ise ona bağlanmak için kullanılır. örnek kodlardan daha kolay anlaşılabilir:

remote example:

```java
String Node = "http://localhost:4444/wd/hub";

DesiredCapabilities cap = DesiredCapabilities.chrome();

webDriver = new RemoteWebDriver(new URL(Node), cap);

local example:

System.setProperty("webdriver.chrome.driver", "/Users/murat/DEV/chromedriver");

webDriver = new ChromeDriver(); //chrome driver'de webdriver'dan extend etmiştir.
```

# jsoup
java html parser'dır. dosya içeriği url'den yada herhangi bir string olarak verilir, html'i parse etmiş şekilde okuyablmemizi sağlayan api'ler sunar. arkaplanda headless web browser çalıştırmaz. bu sebeple js motoru yoktur. bu sebeple sadece statik sayfalar parse edilebilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# gitweb

belirtilen dizinlerdeki git projelerinin web tarayıcısından açılmasını sağlayan bir web arayüz projesidir. bu arayüzden commitler, loglar, history'ler kolayca incelenebiliyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# CDN (or Content Delivery Network or İçerik Dağıtım Ağı)

CDN dünyanın bir çok yerine dağıtılmış sunucuların oluşturduğu bir alt yapıdır ve CDN'nin amacı ziyaretçilere, site içeriği en hızlı şekilde ulaştırmaktır. Bant genişlikleri, bölge bölge hız değerleri göz önüne alınarak dağıtım yapılır ve sunucular her tarafa uygun hızda iletim sağlamaya çalışır.

CDN hizmeti sunan birçok firma var. TÜm global düyayı takip edip sunucuları uygun yerlere koyuyorlar.

CDN hizmetine atılan dosyaları çekmek daha hızlı olacağından;

```xml
<script src="js/jquery-2.0.2.min.js"></script> 
```

yerine;

```xml
<script src="http://code.jquery.com/jquery-2.0.2.min.js"></script>
```

yazılması daha iyi olacaktır. Ziyaretçi önceden farklı siteden CDN li linki indişmiş ise tarayıcı cache'e dahi alacaktır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# dos (or disk operating system)
özel isim'dir.

bir işletim sistemidir. birçok firma tarafından farklı türevleri ve sürümleri çıkarılmıştır. freedos (open source), ms-dos gibi.

# ms-dos (or microsoft dos)

ms-dos 1980 yıllarında çıkmıştır. microsoft, windows 2000 sürümü ile NT ailesine geçiş yapmıştır. NT, dos çekirdeğini ortadan tamamiyle kaldırmıştır. NT öncesi, komut satırı DOS'un arayüzüydü (her işletim sisteminde olduğu gibi). Dos komutları ile aynı görevi yapan ve benzer isimlere sahip olan komutlar, NT sonrası da vardır. bu sebeple birçok kişi NT sonrası işletim sistemlerinde hala Dos'un komut satırı olduğunu sanmaktadır.

# windows NT ailesi

Windows 3'üncü sürümü ile hem dos hem de NT tabanlı sistemleri pararlel geliştiriyor ve paketliyordu. NT tabanlılar sunucu ve kurumsal makinalara kuruluyor, dos tabanlıları ise ev kullanıcılarına veriyorlardı.

# OS/2
Microsoft'un IBM ile birlikte geliştirdiği bir OS. DOS uyumlu olması için dikkat ediliyordu. 1990 ile 2006 yılları arasında geliştirildi ve kullanıldı. kaynak: (source-id: 85) "Microsoft + IBM == OS/2 … briefly" başlığı.

# Windows Me (or Windows Millennium Edition)

Windows 98 İle Windows 2000 arasındaki sürümdür.

# Pocket PC

Microsoft'un geliştirdiği, cebe sığacak boyutta donanım cihazı. Üzerinde windows kurulu geliyor.

# windows insider

microsoft lisanslı windows ürünleri için isteyen kullanıcıları windowsun önceki sürümlerinin updatelerini alabilmelerini sağlamaya başladı. birçok microsoft ürünü için insider opsiyonu mevcut. insider seçeneği aktif olan kişilere aynı anda güncelleme gelmiyor. bazı kullanıcılara bazı updateler çok önceden getiriliyor. düzenli şekilde gruplama mevcut.

# Microsoft Surface (or Surface RT)
Microsoftun donanımını da geliştirdiği, windows işletim sistemi windows yüklü gelen tablet cihazlar serisinin ismidir.

İçinde windows rt vardır. windows rt, windows 8.x'in arm için türevidir. windows rt sadece windows store uygulamalarını açabiliyor. daha sonra mcrosoft geliştirmeyi kesti.

# MSDN
Microsoft'un sadece geliştiriciler için sunduğu web portal.

# TechNet
Microsoft'un tüm kullanıcılar için sunduğu web portal. örneğin visual studio ide ile ilgili indirmeler yada dökümanlar burada bulunmaz.

# RTM (or released to manufacturers)
microsoft windows ürününü piyasaya sunmadan son halini bazı gruplara açar. bu gruplar özellikle akademik ve donanım üreticileridir. bu şekilde piyasaya windows dağıtılmadan hazırlıklar yapılır. bu dağıtılan sürüm RTM'dir.

# microsoft windows version history
Burtada hem server hemde masaüstü PC'ler için; Windows version, Codenames, Release date, Release version, Editions, Latest build, Support status (date) olarak detaylı tablo mevcut: https://en.wikipedia.org/wiki/List_of_Microsoft_Windows_versions "Personal computer versions" ve "Server versions" başlığı altındaki tablolar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Gerçek Zamanlı İşletim Sistemleri (or Real time operating system or RTOS)

Üzerinde çalışan uygulamalar (servisler ve yazılımlar vs..)  gerçek zamanlıdır. yani belirli bir süre içerisinde belirli bir işe cevap vermek zorundalardır. bu durumun oluşabilmesi için; işletim sistemi gerektiğinde, kendisinden daha öncelikli işlemlere öncelik verebilmesi gerekmektedir. aynı zamanda procesler arası çalışmalarda öncelik yönetimininde, normal işletim sistemlerine göre daha çok seçenek sunmaktadır. bu tarz yönetimlere destek veren işletim sistemlerine RTOS denir. CPU önceliklendirilmesi özel olduğundan, bu işletim sistemlerinin sundukları API'ler, arkaplandaki servislerde buna göre yazılmıştır.

Genellikle RTOS'larda donanıma ve sürücülere bağımlılık yüksektir.

Örnekler: 
- Quantum Software Systems OS (or QNX)
- Microsoft Windows CE
- RTLinux (or Real-time Linux)

# monolithic kernel

linux'un kullandığı çekirdek tipidir. tüm sistem tek bir yapıda bulunur. bir hata olduğunda, yada içinden bir şeyin tekrar başlaması gerektiğinde komple sistem restartı gerekir. fakat daha stabildir.

# microkernel

unix bu tiptedir. sistem daha modüler yapıdadır. kernel modda çok az şey çalışır. bu sebeple bir parça (örnek driver) hata verdiğind eve restart istediğinde tüm sistem resatart edilmek zorunda diildir. daha az stabildir.

# hybrit kernel

windows'un NT ve sonrası kullandığı çekirdek yapı tipidir. NT öncesi monolitic kullanıyordu. bu tarz sistemlerde; bazı kısımlar çok bütünleşikken, bazıları hiç diildir (modülerdir).

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# IaaS (or Infrastructure As a Service or Altyapı olarak servis)

uzaktaki sunucularda sizin adınıza sanal bir sistem (donanım) oluşturuluyor ve içine işletim sistemi kurulu şekilde hazır oluyor. (Örnek firma hizmeti: Amazon WS)

# PaaS (or Platform As a Service)

Bu sınıf yapısında size bir servis havuzu sunuluyor ve siz bu servislerden ihtiyacınıza göre ekleme çıkarma yapabiliyorsunuz. Tabiki her bir servis platformu belirli limitlerden sonra ayrı ayrı (+) maliyet demek. Örneğin; çeşitli servisler mevcut (Maven, MySQL veritabanları gibi). (Örnek firma hizmeti: Windows Azure)

# SaaS (or Software As a Service)

sunulan özel yazılımlar ile, lokalde hiçbir işgücü ve bakım maliyeti olmadan yazılımlardan istifade edebiliyorsunuz. örneğin; attlasian jira, gmail gibi.

# Mobile backend as a service (or MBaaS or backend as a service or BaaS)

mobil uygulamalar için bulut sistemi hizmetleridir. örneğin notification yönetimi, app için analitik bilgi toplama işlemleri, crachs hakkında bilgi toplama servisleri, kolayca erişilebilir veritabanları. Örnek hizmet: Google Firebase.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Genetic algorithm
belli bir sayıda aday çözüm üzerinde seçim, çaprazlama ve mutasyon operatörlerini kullanarak en optitmum çözümler elde etmeye çalışan algoritmalardır.

Temel olarak şu döngü ile süreç işletilir:
- başlangıç popülasyonu (çözüm kümesi) (rastegel yada tahmin üzerine)
- uyumluluk hesaplaması (çözüm kümesindeki her eleman için uyumuluk hesaplaması yapılır)
- seçim operatörü uygulaması (her çözümün ayrı ayrı en iyi olanının incelenmesi)
- çaprazlama operatörü
- mutasyon operatörü
- program devam? program dur? kararı (en iyi çözüm yeterli mi? değilmi?)
  (eğer devam edilirse program 2'inci adıma dönecektir)
