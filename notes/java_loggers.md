############################

############################
# JAVA LOGGERS
############################

############################


# log
log kelimesi türkçede "kayıtların bütünü" anlamına geliyor. (çok farklı anlamları da var.)

# graylog
java ile yazılmış bir sunucudur. buraya herkes http gibi  protokollerle log atıyor uzaktan. kolay bir arayüz sunuyor logların okunması için. tüm sunucular buraya log atıyor. tek bir yerde depolanıyor ve yönetiliyor.

# log4j
java için log kütüphanesi.

default olarak; log4j.properties yada log4j.xml dosyasından konfigürasyonları okur.

log4j 2'inci sürümü log4j2.properties yada xml dosyasını okur.

# logback
log4j'nin 1'inci sürümündeki bazı köklü sorunlarını gidermek için başlatılan proje. log4j 2'inci sürümünde bunları giderdi, fakat logback projesi hala devam etmektedir.

logback config örneği:

aşağıdaki dosya opsiyonel olarak farklı profil dosyalarına referans ettirebiliriz:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration debug="true">
    <springProfile name="prod">
        <include resource="logback-prod.xml"/>
    </springProfile>
    <springProfile name="test">
        <include resource="logback-test.xml"/>
    </springProfile>
    <springProfile name="default,development">
        <include resource="org/springframework/boot/logging/logback/base.xml"/>
    </springProfile>
</configuration>
```

logback-prod.xml dosyası örneği:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<included>
    <!--include ile spring'in içerisinde gelen default tanımlaraı import ediyoruz-->
    <include resource="org/springframework/boot/logging/logback/base.xml"/>

    <!--propery variable'ı kullanıyoruz. burası sping properties'ten variable çekmemizi sağlıyor.-->
    <springProperty scope="context" name="application_name" source="spring.application.name"/>

    <!--console'a basmamızı sağlayan appender. file-appender, yada logstash-tcp-appender gibi alternatifler vardır.-->
    <appender name="flatConsoleAppender" class="ch.qos.logback.core.ConsoleAppender">

        <!--encoder'lar içerisine yazılan bilgileri formatlı yazar. logstash içerisinde gelen bu encoder ilk logstash'in kolayca parse edebileceği bir formata çeviriyordu data'ları fakat daha sonrada generic bir encoder halini aldı. -->
        <encoder class="net.logstash.logback.encoder.LoggingEventCompositeJsonEncoder">,

            <!-- providers içerisindeki her data direk output'a gönderilecek anlamına gelir.-->
            <providers>
                <timestamp>
                    <timeZone>UTC</timeZone>
                </timestamp>
                <version/>
                <logLevel/>
                <message/>
                <threadName/>
                <context/>
                <pattern>
                    <pattern>
                        {
                        "my_custom_env": "${my_custom_env}",
                        "java_class": "%C",
                        "trace": {
                            "trace_id": "%mdc{X-B3-TraceId}",
                            "span_id": "%mdc{X-B3-SpanId}",
                            "parent_span_id": "%mdc{X-B3-ParentSpanId}"
                            }
                        }
                    </pattern>
                </pattern>
                <stackTrace/>
            </providers>
        </encoder>
    </appender>

    <!--log 7seviyesi info olan log'ları içerisindeki appender'a yazar.-->
    <root level="info">
      <!--yukarıdaki appender'ımızın name'i-->
        <appender-ref ref="flatConsoleAppender"/>
    </root>
</included>
```

yukarıdaki config ile her satırın (log'un) örnek çıksı:

```json
{
    "@timestamp": "2020-10-16T10:19:47.741Z",
    "@version": "1",
    "level": "WARN",
    "message": "log message from log.info( message ) ",
    "thread_name": "org.springframework.kafka.KafkaListenerEndpointContainer#0-0-C-1",
    "application_name": "user-service",
    "hostname": "hostname_of_machine",
    "java_class": "org.apache.kafka.clients.NetworkClient",
    "trace": {
        "trace_id": "43344532",
        "span_id": "436546574",
        "parent_span_id": "34645364"
    }
}
```

# log4j12
log4j'nin 1.2'inci sürümünün paket adıdır. artık geliştirilmemektedir.

# commons-logging (or old-name:Jakarta Commons Logging or old-name:JCL)
java için log kütüphanesi. apache-commons projesinin bir parçasıdır.

commons-logging, SLF4J gibi tek başına kullanılamaz. başka bir logger altyapısına yönlenmesi gerekir. slf4j ile benzer yapıdadır, fakat SLF4J'den önemli bir farklılığı vardır: jcl claspath'te olan bir kütüphaneyi bulur ve logları ona yönlendirir. yani kulanılacak logger kütüphanesi jcl implementasyonu olmak zorunda diildir. örneğin bir projede log4j ve jcl kütüphanesi olması yeterlidir. jcl otomatik lo4j'ye yönlenecektir.

# SLF4J (or Simple Logging Facade for Java)
Birçok java log kütüphenesi için facada (ön adaptör) sunan bir kütüphanedir. bu şekilde kullanıcı istediği log kütüphanesine geçişi çok kolay bir şekilde yapabilmektedir. SLF4J tek başına kullanılmaz. diğer kütüphanelerin ortak bir API üzerinden kullanılmasını (çağrılmalarını) sağlar.

slf4j ilk başladığında bir implementasyon arar. eğer yok ise; default olarak kendi içinde gelen no-operation (or NOP or NOPLogger) implementasyonunu kullanır. eğer birden fazla implementasyon kütüphanesi classpath'e eklenmiş ise; o zaman slf4j bunlardan sadece 1 tanesini kullanır ve bize sadece bir uyarı verir. kullandığımız kütüphanelerde (örneğin; sql-server-client) slf4j implementasyonu "optional" dependency olarak gelir. böylece herkes eklediği her kütüphanede birden fazla slf4j implementasyonu sorununu yaşamamış olur.

slf4j başlarken org.slf4j.impl.StaticLoggerBinder sınıfını arar. bu sınıf her slf4j implementasyonunda mevcuttur.

- slf4j-simple: çok basit bir slf4j implementasyonudur.

- slf4j-jdk14: bir slf4j implementasyonudur. Java.util.logging kullanmamızı sağlar.

- slf4j-api: slf4j core kütüphanesinin paket adıdır.

- slf4j binding: bu terim slf4j implementasyonunu kullanılması anlamında kullanılır 

# slf4net
slf, facade olduğundan birçok dilde aynı API'yi destekliyor. bu pakette .net frameworkü için geliştirilmiş slf'dir.

# example of slf4j with log4j binding
asagidaki dependency'ler şarttır:

- slf4j-api
- log4j-slf4j-impl
- log4j-api //log4j impl bunu şart koşuyor.
- log4j-core //log4j için gerekli bir bağımlılık

# bridge vs migrator
bridge paketleri jul-to-slf4j gibi arada "to" olacak şekilde isimlendirilir. migrator paketlerinde ise arada "over" keywordü yer alır. örnekler:

> jcl-over-slf4j

> log4j-over-slf4j

> jul-to-slf4j

- migrator paketleri classpath'te varolan diğer log kütüphanesinin kodlarını(API'lerini) ezer ve logları slf4j'ye aktarır. örnek: jcl-over-slf4j: classpath'te jcl olan kütüphanenin kodlarını ezer ve slf4j'ye aktarır.

- bridge paketlerinin de amacı aynıdır. fakat farklı şekilde çalışır. örnek üzerinden gidersek: jul-to-slf4j paketi, classpath'teki JUL apilerine Handler ekler ve logları slf4j'ye aktarır. Bu handler'lara SLF4JBridgeHandler ismi verilir.

JUL migrator paketi olamaz. çünkü; jul java.# paketleri altındadır. bu paketler ezilemeyeceğinden jul için migrator paketi yaratılamıyor.

# java.util.logging (or JUL)
jre içinde geliyor. logging.properties dosyasını okur.

val l = java.util.logging.Logger.getLogger("MyClass"); //aldıgı parametre o andaki sınıfın ismidir. böylece logu attığımızda hangi sınıın o logu attığını okuyabiliriz. 

# isteğe bağlı handlerlar
handler atanmazsa her zaman default handler olur.

```java
val h = new ConsoleHandler

h.setLevel(Level.ALL) // we output ALL the logs to the console

val f = new FileHandler("warn.log", true)

f.setLevel(Level.WARNING) // we also send all WARNINGs and more criticals to a file

f.setFormatter(new SimpleFormatter)

l.addHandler(h)

l.addHandler(f)
```

# log4j FileAppender vs RollingFileAppender vs DailyRollingFileAppender

RollingFileAppender FileAppender'dan extend eder ve dosya boyutu maximuma geldiğinde yeni bir dosya oluşturur eskisini backuplar.

DailyRollingFileAppender RollingFileAppender'ı extend eder ve dosya boyutu maximuma gelince değil, istenilen gün sayısı sonrasında yeni dosyayay geçiş yapar.

# log levels
slf4j ve log4j ve log4j2 için:

- Trace: sadece developerın anlayacağı loglardır. fonksiyonların içlerinde kodun nerede oldugunu belli etmek için kullanılır.

- Debug: it'cilerin de anlayacağı loglama olmalı. it'ciler bir sorunu incelerken buraya başvurabilmeli.

- Info: servis başladı. kapandı gibi bilgileri vermek için kullanılır.

- Warn: uygulama için bazen önemli olabilecek akışları bildirmeli. örneğin; soket timeout verdi. tekrar deneniyor. buralar bir hata değildir. sayısı çok arttıkça uygulama incelemeye alınmalı, yada uygulamada bir terslik oldugunda ilk bakılacak kısımlar burada olmalı.

- Error: hataların yazıldığı seviye

- Fatal: sistemin durması gerektiğinde veya zarar gördüğü durumlarda

- All: bu bir seviye değildir. log basarken tüm logların basılacağını belirtir.

Yukarıdaki level'lar kütüphaneden kütüphaneye değişebiliyor. bazılarında bazı levellar olmuyor, bazılarında yukarıdakilerden daha fazla çeşit level sunuluyor. bazı diğer leveller:

- level -> yukarıdaki seviyelerden denk olanı

- SEVERE (türkçe kelime anlamı: şiddetli) -> Error

- WARNING -> Warn

- CONFIG -> Info

- FINE -> Debug

- FINER -> Debug

- FINEST -> Debug/Trace

- VERBOSE (türkçe kelime anlamı: gereksiz sözler) -> Trace

# audit trail (or audit log)
audit kelime anlamı: denetim

trail kelime anlamı: iz

audit log'lar domain event'leri gibi, domain'de olan her olayın log'larıdır. örnek: a transaction is created, a user is performing an action...

# best practices:
- SLF4 kullanırken;

log.debug("Found " + records + " records matching filter: '" + filter + "'");

yerine bunu kullanmak daha iyi:

log.debug("Found {} records matching filter: '{}'", records, filter);

log4j'de SL4j gibi bir metod yok. bu sebeple ilk satırdaki yöntem kullanılmak zorundadır.

- if(logger.isDebugEnabled) gibi kodlar kullanılmamalı

- hatalar sadece bu şekilde loglanmalıdır:

log.error("Error reading configuration file", e);

- log.debug("the name is");

  log.debug(name);

gibi iki satıra kesinlikle yayılmamalı. pararlelden gelen loglar bu ikisi arasına girebilir ve loglar anlamını kaybeder.

- her sınıfın tostring'i olmalı ki loglar düzgünce basılabilsin. fakat gizli bilgiler loga basılmayacağı için onlara ekstra dikkat edilmeli. gerekirse tostring'den gizli bilgiler çıkrılmalı veya hashlenerek tutulmalı (or hashlenerek print edilmeli).

- log.info("Processing ", request.size());  request'in null gelme durumunda bu kod satırı patlayacaktır. request null kontrolü yapılması istenmiyor ise; request'in tostringi olmalı ve size() metodu kulanılmamalıdır. zaten logger tostring'i çağırdığında, logları okuyan kişi dizinini boyutunu da çıkarabilicektir. eğer bu şekilde istenmiyor ise; null kontrolü yapılmalıdır.

# spring'de logging
spring'de java sınıflarının bulunduğu paket isimleri ile log level'ı belirleyebiliriz. örnek:

```yml
logging:

  level:

    ROOT: ERROR  # tüm sistem için genel seviyeyi temsil ediyor

    org.springframework: ERROR 

    org.springframework.security: DEBUG 

    org.springframework.security.web.FilterChainProxy: ERROR 

    com.myapppackages: INFO # kendi sınfılarımız 

    org.mongodb: ERROR   # üçünçü parti dependency olsa bile bunu yapabiliriz

  file: /Users/myapp/application.log 
```

Spring kendi içinde commons-logging kullanıyor. SLF4J kullanılmamasının sebebi eskiden kalma olduğundan değiştirilmesinin çok maliyetli olmasıdır. commons-logging yerine sl4j kullanıcaksak, jcl-yi exclude edip sl4j'yi eklememiz (ve slf4j implementasyonu eklememiz) yeterli olcaktır. fakat log4j kullanacaksak; log4j eklemek yeterli olcaktır. jcl zaten otomatik log4j'yi görmektedir. 

spring-boot starter, default olarak jcl'yi logback'e yönlendirilmektedir ve default olarak logback-spring.xml dosyasından config'leri okumaktadır.

# logstash
sunucu olarak çalışan bu uygulama, ona gelen log'ları veritabanına kaydediyor. gelen logları kaydetmeden onları üzerinde manipülasyon yapılmasına da izin veriyor. çoğunlukla veritabanı olarak elastic search kullanılıyor.
