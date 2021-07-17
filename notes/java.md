############################

############################
# JAVA
############################

############################

# Annotation based vs Java based (JavaConfig) vs XML based configuration
Spring kendi kütüphaneleri ile "Annotation based" veya "XML based" işlem sağlayabilir. fakat spring JSR standartları (java standartları) dışında kendi paketlerini sunmaktadır. Spring dökümanlarında; "Annotation based"'Den kasıt spring'in kendi kütüphaneleridir. Spring aynı zamanda Java standart annotationları ile de işlem yapabilmemizi sağladığı için "Java based" configuration olarak ayrı bir kavram mevcuttur. Oysa JavaEE kitaplarında "Annotation based vs Java based" kavramları aynı şeye denk gelmektedir, çünkü JavaEE zaten sadece JSR kütüphanelerini kullanmaktadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# variable scope

Java standart'larında aşağıdaki terimler kullanılamktadır. Fakat aynı terimler farklı programlama dillerinde farklı seviyeler için kullanılıyor olabilir.

## Local variables
   kod bloğu tamamlandığında, yokedilen değerlerdir.

## Instance variables
   garbage collector'ün temizlemesine girme durumu olan variable'lar.

## Class variables
   tüm program sonlanana kadar kullanılan değerlerdir.

```java
public class MyClass { 
  
  final static int MAX_LENGTH = 5;  // class variable
  int length;                       // instance variable

  public void method() { 
    int inches = 40;                // local variable
  }
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# JCE (or Java Cryptography Extension) vs JCA (or Java Cryptography Architecture)
JCE eskiden JDK dışında olan bir kütüphane grubuydu. Bağımsız geliştiriliyordu. Aynı zamanda JCA, JDK içerisinde geliştiriliyordu. İkisi benzer işleri yapabiliyordu.

JCE, JDK 1.4 ile birlikte JCA ile birleştirildi ve JDK altında geliştirilmeye devam edildi.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# template engine
java için açık kaynaklı template engine'lerdir:
- thymeleaf
- freemarker

- her ikiside sadece html dosyalarını değil, herhangi bir dosyayı da model ile doldurabilmektedirler.
- her iksininide özellikle spring ile de opsiyonel kullanılabilen entegrasyon modülleri vardır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# apache's commons-beanutils BeanUtils class vs org.springframework.beans.BeanUtils
Spring'in BeanUtils'i spring bean'lerinin instance'larında değişiklik yapabilmek için tasarlanmıştır. Oysa apache'ninki sadece getter-setter içeren java objelerinin instance'ları üzerinde işlem yapabilmek için tasarlanmıştır.

apache's commons-beanutils BeanUtils example:

```java
Course course = new Course(); // Course has "String name" and "List of codes" as filed.

String name = "Computer Science";
List<String> codes = Arrays.asList("CS", "CS01");
 
PropertyUtils.setSimpleProperty(course, "name", name);
PropertyUtils.setSimpleProperty(course, "codes", codes);
```

apache's commons-beanutils BeanUtils example:

```java
// copies from different types of classes, if fields are same name.
BeanUtils.copyProperties(courseEntity, course);
```

org.springframework.beans.BeanUtils example:

```java
// copies from different types of classes, if fields are same name.
BeanUtils.copyProperties(courseEntity, course);
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# LLVM
dilden bağımsız bir derleyicidir. LLVM, klasik VM'ler ile (Java VM gibi) benzerlikler göstermektedir. Bu sebeple LLVM ismi, "Low Level Virtual Machine"'den esinlenerek verilmiştir. Dolayısı ile "Low Level Virtual Machine" kısaltması değildir. LLVM özel bir isimdir. kaynak: (source-id: 341)

C ve C++ için full support'u vardır. Rust dili de LLVM ile çalışacak şekilde tasarlanmıştır. 

LLVM programatik olarak kullanılabilecek bir API'ye de sahiptir. Programcı bir Java dili için JIT yazıyor olsun (örneğin JVM'e alternatif bir VM geliştiriyor olsun). Programcı, java kodunu önce  __intermediate representation (or IR)__'a, daha sonrada makine koduna çevirebilir. Bu 2 işi yapmak içinde LLVM'in sunduğu programatik API'leri kullanabilir. kaynak: (source-id: 342) "LLVM defined" başlığı.

LLVM-frontend saf kodu IR'a çevirirken, IR'ı native binary'ye LLVM-backend ile çevrilir. kaynak: (source-id: 343) "C to IR" başlığı ilk paragraf. 

LLVM-optimiser ise IR'a çevrilmiş kodu optimize eder. örneğin kullanılmayan kod akışlarını siler gibi... kaynak: (source-id: 343) "The stages are" altındaki ikinci madde.

__intermediate representation (or IR or Intermediate code or Intermediate language)__ genel olarak programlama dünyasında; derlenmenin öncesinde, kodun çevrildiği bir biçimdir. birçok IR standardı vardır. 

Aslında bakıldığında JIT'lerin ve VM'lerin kabul ettiği native kodlar (örneğin jvm bytecode) bir IR'dır.

__Common Language Infrastructure (or CLI)__ microsoft'un  ".net" platformu için geliştirdiği IR ve bunu işletecek JIT satndartlarının tümünün ismidir. __Common Intermediate Language (or CIL or old-name:Microsoft Intermediate Language or old-name:MSIL or old-name:Intermediate Language or old-name:IL)__ ise bu standartlara uygun olarak implemente edilmiş bir IR'dır. Şekil üzerinden bu durumu göstermek gerekirse:

(source-id: 345)

# GraalVM
Oracle tarafından geliştirilen OpenJDK türevi VM'dir. OpenJDK'ya ek olarak sunduğu özellikler:

- OpenJDK'nın JIT compiler'ına göre bazı durumlarda avantaj sağlayacak ek özellikleri/optimizasyonları var.

- LLVM toolchain

  Birçok farklı dilde yazılmış kodun 'LLVM bitcode'una çevrilmesi için derleyici içeriyor.

  C'de yazdığımız bir kodu aşağıdaki komut ile 'llvm bitcode'una çevirebiliyoruz:

  ```sh
  $LLVM_TOOLCHAIN/clang my_c_code.c -o my_llvm_bitcode_binary
  ```

  Bazı diller için direk olarak support gelmemektedir. Onları "graavlVM Updater" ile kurmamız gerekiyor:

  ```sh
  gu install python
  ```

- LLVM-based diller için run-time içeriyor. Yani; "LLVM bitcode"'unda olan binary'leri run edebiliyor.

  LLVM bitcodu'na çevrilmiş binary'leri run edebilmemiz için aşağıdaki komut çalıştırılmalıdır:

  ```sh
  lli my_llvm_bitcode_binary
  ```

- Native derleme
  - Ahead-on-time compiler olduğu anlamına gelir.
  - GraalVM java kodunu native derlendiğinde, derlemesi uzun sürüyor. Çünkü sadece çağrılabilecek sınıfıları embeeded hale getiriyor.
  - GraalVM reflection yapamıyor. Fakat java kodumuzda reflection varsa şöyle bir yöntem sunuyor: Build aşamasında bütün sınıfıların ve metodların imzalarını bir json dosyasında saklıyor. bu json dosyasını embeded native kodun içerisine gömüyor. reflection gerektiği anda, json dosyasındaki bilgilere göre fonksiyonları çağrıyor.
  - GraalVM içinde gelen 'native-image' isimli executable ile compile edilen kodlar, herhangi bir OS'ta native çalışmaktadır (hangi OS'ta derlenirse, o OS için executable oluşturulur). Fakat native kod'da çalışması için reflection gibi teknolojileri kullanmamak gerekli. Örneğin spring framework reflection kullandığı için şu anlık desteklenemiyor (yıl 2019 sonu). Bu sebeple; direk native derlenebilmesi için uygun __Quarkus__ ve __Micronaut__ projeleri geliştirildi. Bu projeler enterprise framework ve library'lerden oluşan birbirlerine alternatif projelerdir.
  - java ile yazılan kodlarda garbage-collector'un arkada çalışması şarttır. bu sebeple native executable'ın içerisinde ufak bir virtual-machine gömülüyor. JVM'e göre çok hafif ve daha az yeteği var. Bu vm'e '__SubstrateVM__' ismi verilmiş.

# Quarkus

```xml
<dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-universe-bom</artifactId>
        <version>1.1.1.Final</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
    </dependencies>
  </dependencyManagement>
```

Daha sonra buradan istediğimiz extension'u dependency olarak eklememiz gerekmektedir: (source-id: 346) Bu listedeki her bir extension ayrı bir maven dependency'dir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Apache Lucene
İlk başta sadece java için tasarlanan fakat daha sonra birçok programlama için geliştirilen indexleme ve arama motoru kütüphanesidir.

Bir dökümanı (database, list, text file...) parçalara böler, indexler ve daha sonra da arama yapılabilmesini sağlar. bunların tümü için ayrı ayrı programlama dillerine API'ler yazılmıştır. Lucene sunucu gibi kendi başına çalışmaz.

querydsl'in Lucene'nin query (arama) tarafı için desteği vardır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Spring Boot Actuator
Actuator kelime anlamı: 1. işletici, çalıştırıcı 2. uyarıcı

spring'e dependency olarak eklendiğinde, o spring uygulaması için rest endpoint'leri açıyor ve bu endpoint'ler üzerinden health check, disk usage, heap dump gibi bilgiler dışarıya veriyor.

http://localhost:8080/actuator -> bize actuator'ın açtığı tüm metric gruplarının URL listesini döner. Liste aşağıdaki gibidir. Her URL, kendi içerisinde istediği bilgileri dışarıya açabilir. Bazı temel örnekler:

- http://localhost:8080/actuator/metrics -> current thread count, current memory usage, system update, all java classes
- http://localhost:8080/actuator/beans -> all spring beans
- http://localhost:8080/actuator/env -> all environment variables (her prop app.yml, bootstrap yml, kubernetes'ten mi gelip gelmediği detayı ile birlikte yazıyor)
- http://localhost:8080/actuator/info -> information about spring boot
- http://localhost:8080/actuator/trace -> all rest endpoints

Örneğin; "kubernetes java client"; podname, namespace gibi bilgileri actuator/info'dan döndürüyor. Kubernetes isterse ekstra url'de açabilirdi. ama kubernetes java client geliştiricileri bu url'den döndürecek şekilde geliştirme yapmış.

# Micrometer
JVM uygulamaları için facade kütüphanesidir. Bu kütüphane JVM based uygulamamız dışarı spring-actuator gibi bilgi vermektedir. spring-actuator bilgileri dışarı açarken belli bir formatta/standartta sunmaz. oysa Micrometer birçok monitöring tool'a destek verecek şekilde bunları dışarı açar.

Micrometer'ın support ettiği monitoring tool'lar:

AppOptics, Azure Monitor, Netflix Atlas, CloudWatch, Datadog, Dynatrace, Elastic, Ganglia, Graphite, Humio, Influx/Telegraf, JMX, KairosDB, New Relic, Prometheus, SignalFx, Google Stackdriver, StatsD, Wavefront.

Micrometer JVM uygulamalarında spring-actuator ile de entegreli çalışabilir. eğer istenirse spring-actuator'sız, saf java projesinde de çalışabilir.

# Grafana
Elasticsearch, Prometheus, Graphite, InfluxDB gibi veritabanlarından verileri çekerek, kendisinin sunduğu web arayüzünden visualize eder. belli event'lerde oto notify/email sistemi gibi ek özelliklerde sunar.

# Prometheus
bir servis olarak ayağa kalkar. önceden her servisin healt (örneğin spring'deki actuator endpoint'leri) url'si promotheus'a tanıtılır. promotheus bu url'lere giderek düzenli olarak data çeker ve kendi db'sine kaydeder.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# webjars

maven'a aşağıdaki eklendiğinde:

```xml
<dependency>
    <groupId>org.webjars</groupId>
    <artifactId>jquery</artifactId>
    <version>3.1.1</version>
</dependency>
```

html'lerimizden get isteği ile script'i çekebilmemizi sağlar:

```html
<script src="/webjars/jquery/3.1.1/jquery.min.js"></script>
```

configürasyonu bu şekildedir:

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
 
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry
          .addResourceHandler("/webjars/**")
          .addResourceLocations("/webjars/");
    }
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# eclipse compiler java (or ECJ)
- Eclipse IDE'nin java compiler'ının ismidir.
- Java'nın default compiler'ından farklıdır.
- en temel farklar:
  - kod düzgün derlenmemiş olsa bile, onu paketleyebilir (derleyebilir, jar/war oluşturur). örnek bir class fiziksel olarak yoksa fakat bir başka class içinden referans edilmişse, jdk normalde hata verirken, eclipse IDE bu hatayı esgeçebilir. dolayısı ile runtime'da classNotFound gibi bir hata alırız.
  - kısmi derlemelere imkan sunar. kodun sadece bir kısmını değiştirdiğimizde sadece o kısımları derler.
- tomcat'te JSP'leri derlerken ECJ kullanır. bu şekilde en ufak hatada tüm sistemi derlememezlik yapmaz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# jre/jdk bin directory binaries

- java
  
  java app starter

- javaw

  wraps the "java" command, and starts the application on a new terminal interpreter. kaynak: (source-id: 347)

- javaws

  java web starter

- javac

  java code compiler

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# java.util.concurrent.Future

```java
public class SquareCalculator {    
     
    // ExecutorService java içinde gelen, Birçok thread'i yönetebilmemizi sağlayan bir yapıdır.
    private ExecutorService executor = Executors.newSingleThreadExecutor();
     
    public Future<Integer> calculate(Integer input) {

        return executor.submit(() -> {

            Thread.sleep(1000);
            
            return input * input;
        });
    }
}

Future<Integer> future = new SquareCalculator().calculate(10);
 
while(!future.isDone()) {
    System.out.println("Calculating...");
    Thread.sleep(300);
}
 
Integer result = future.get(); //get metodu eğer yukarıdaki while'ı yazmamış olsaydık, işlem tamamlanana kadar bekleyecekti. şimdiki durumda beklemesine gerek yok, çünkü zaten ukarıda işlemin bittiğine dair kontrolümüzü while içerisinde yaptık.
```

Future sınıfı şu metodları sunar:

- Boolean Cancel(boolean mayInterruptIfRunning)

  eğer task zaten kapanmışsa yada kapatılamadıysa false döner.

- V get()

  V dönüş objemiz. metodun ne yaptığı kod yukarıdaki kod içinde açıklandı.

- V get(long Timeout, TimeUnit unit)

  metod belli aralıkta dönmezse TimeoutException fırlatır.

- Boolean isCancelled()

- Boolean isDone()

# java.util.concurrent.CompletableFuture
java.util.concurrent.Future implementasyonudur. ek özellikler sunar. Future'nin eksiklerini kapatmak için daha sonradan geliştirilmiştir. kapattığı eksikler:

- zincir oluşturabilme

  üstüste Futur'leri sırası ile execute etme

- exception handling

- manually complete the future

  ```java
  completableFuture.complete("Future's Result");
  ```

  bu satır sonrası, completableFuture'ı kullanan tüm  metodlar isDone=true olacaktır.

- callback metodu verebilme

  ```java
  CompletableFuture<Void> future = CompletableFuture.runAsync(new Runnable() {
    @Override
    public void run() {
        // any code here
    }
  });

  future.get()
  ```

  Aynı işi lambda ile çok daha kısa yapabiliriz:

  ```java
  CompletableFuture<Void> future = CompletableFuture.runAsync(() -> {
      // any code here
  });
  ```

  Sadece future kullansaydık; get()'ten sonra metodumuzu elle çalıştırmak zorunda kalacaktık ve işlemin success mi olup olmadığını da kontrol etmemiz gerekecekti.

  Burada callback metodumuz istersek obje de dönecek şekilde ayarlayabilirdik.

CompletableFuture'ın bazı metodları birbirlerimne çok benziyor. Asıl farkları bir önceki callback metodundan dönen parametreyi alıp almadıkları ve kendilerinin ne döndürdükleridir. aşağıdaki tablo üzerinde özet bilgiye ulaşılabilir:

tablo kaynağı: (source-id: 420)

| Method         | Async method        | Arguments                               | Returns                        |
|----------------|---------------------|-----------------------------------------|--------------------------------|
| thenRun()      | thenRunAsync()      | –                                       | –                              |
| thenAccept()   | thenAcceptAsync()   | Result of previous stage                | –                              |
| thenApply()    | thenApplyAsync()    | Result of previous stage                | Result of current stage        |
| thenCompose()  | thenComposeAsync()  | Result of previous stage                | Future result of current stage |
| thenCombine()  | thenCombineAsync()  | Result of two previous stages           | Result of current stage        |
| whenComplete() | whenCompleteAsync() | Result or exception from previous stage | –                              |

# Promise
standart java içerisinde Promise objesi yoktur. CompletableFuture, diğer dillerde kullanılan promise kavramına en yakın objedir. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# java package names

- java.lang.* tüm buradaki paketler otomatik import olmuş oluyor.

- java.* - jre içinde olan core paketler

- javax.* - jre içinde gelen fakat genelde extension (daha çok core pakete girmesi zorunlu olmayan: örnek jaxb) sınıflarını içermektedir.

  Bazı paketler javax.\*'dan java.\*'ya geçmiştir.

- önerilen isimlendirme:
  
  com.company_name.region_or_project_name.package_purpose

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# InputStream
reads bytes from any type of stream

# OutputStream
writes bytes to any type of stream

# flush
türkçe kelime anlmı: 1. su ile temizlemek. "The toilet doesn't flush." gibi kullanılıyor. 2. utançtan yüzü kızartmak.

OutputStream'de olan bir metoddur. bazı stream'ler write ile yazdığımız datayı karşıya hemen yollamaz. bunun bir çok sebebi olabilir: cache, buffer, protokol standartları gereği belli bir boyuta gelmesi beklenir... Flush metodu stream'e / protokole yazma sinyali göndermektedir. öncelikte stream'in flushable olması gereklidir. flushable olsa dahi bu metod işlemin fiziksel olarak karşıya gidip gitmeyeceğini garanti etmez. örneğin TCP soket'e yazarken flush metodu kesinlikle bunun garantisini vermiyor, çünkü tcp standartları belli data'nın bir byte'a gelmesini bekliyor. ancak tcp soket kapatılırken, data kesinlikle yollanıyor.

# InputStreamReader
kind of InputStream that read only character type from stream.

# DataInputStream
kind of InputStream that reads all kind of primitive types from stream.

# BufferedInputStream
buffer türkçe kelime anlamı: tampon, koruma.

kind of InputStream that reads only bytes with buffer mechanizm.

# Reader
read chacarter from any type of stream

# BufferedReader
kind of Reader that reads only character with buffer mechanizm.

# Scanner
reads primitive types and string with regex from any type of stream.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# generics
"generic programming" tüm programlama dilleri için bir terimdir. java da bu özelliği destekler. örnek:

generic'in türkçe kelime anlamı 'genel'dir. fakat bazı yerlerde jenerik olarak çevrilir. jenerik yanlıştır. hiçbir resmi kaynak bu şekilde çevirmez. jenerik türkçede 'tanıtım' anlamına gelir.

örnek generic java kodu:

- kullanıldığı kod:

```java
List<String> c = new ArrayList<String>(); //java 8 ile birlikte artık sağ tarafta generic-tipini belirtmeye gerek yoktur.

c.add(new Object()); // compile-time error fırlatır
```

- tanımlandığı kod:

```java
public class Entry<K, V> {

    private final K key;

    private final V value;

    public Entry(K key, V value) {  

        this.key = key;

        this.value = value;
    }

    public K getKey() {

        return key;
    }

    public Object method1(){

        return new Collection()<? extends K>;
    }
}
```

K, V harfleri istenilen karakter yada string olabilir. Genelde alışkanlık olduğundan, T (type), E (Element), V (value) and K (key) kısaltmaları kullanır. 

Yukarıdaki örnekte V yerine gerçek bir sınıf ismi yazmaya gerek yoktur. zaten o sınıf belli ise (fix ise) o zaman generic yapmaya gerek yoktur. BU sebeple oraya ne yazarsak yazalım sınıf ismi değil, özel bir keyword olarak algılanacaktır.

Yukarıdaki örnekte new Collection()<? extends K>; satırındaki "extends" tahmin edilen anlamından farklı bir anlama geliyor. K'nın subclass'ı olduğu herhangi bir sınıf gelmeli buraya anlamına geliyor. eğer tersi olursa runtime'da hata alırız. extend yerine super yazarsa, aşağıdaki satırda hata amayız. çünkü süperi "String" olan bir sınıf anlamına gelecekti:

Box<? super String> list = new Box<String>();  //super'i String olan bir sınıfı gelecek anlamına geliyor

list.add(new String("Hello World"));

Oysa yukarıda super yerine extend yazsaydı daha compile sırasında hata alacaktık.

# PECS (or Producer Extends Consumer Super)

Yukarıdaki super ve extend'li kod satırlarına dikkat edersek; super yazdığımız zaman aşağıdaki satırlarında listeye ekleme yapabiliyoruz. çünkü ne ekleyeceğimizi biliyoruz. oysa extends'de ne ekleyeceğimizi bilmediğimizden, ekleme yapamıyoruz sadece okuma yaabiliyoruz. Bu sebeple extend keywordü ile işlem yaptığımızda kodumuz "Producer" görevi görüyor. bu sebeple producer'lar extend etmeli terimi ortaya çıkmıştır: "Producer Extends". Benzer şekilde "Consumer Super" terimi ortaya atılmıştır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# static initializer

class Person {
   static {
           int a = 10;
           System.out.print("this block is 'static initializer' ")
   }

   {
          int b = 20; 
          System.out.print("this block is 'instance initializer' ")
   }
}

kod çalışma sırası:

1- static initializer

2- instance initializer

3- constructor (türkçe keliem anlamı: inşaatçı)

Yukarıdaki kodda int a ve b classın field'ları değil. block'un local field'larıdır. initializer block'ları ile class'ın fiels'larını set etmek için kullanırız. class'ların field'larını asagidaki gibi de set edebiliriz:

```java
class ABC {

  private a = 5;
}
```

fakat "instance initializer" ek özellikler de sunar. örneğin; if koşullarına göre farklı değerler set edebiliriz. bazı durumlarda log attırabiliriz.

# instance initializer vs constructor
yukarıda bahsedilen set etme olayı neden constructor'da yapılmıyor?

1- instance initializer'ın sınıfın 'final' değişkenlerini set etme özelliği de bulunuyor.

2- birden fazla constructor olduğunda hepsinde aynı set etme işlemini yapmak zorunda kalabiliriz. bunun yerine tüm constructor'lar için ortak olan kodu "instance initializer"'a atmakta yarar vardır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# objenin metodları

aşağıda açıklaması geçmeyen metodlar başka yerde anltılıyor.

- tostring
- wait
- notify
- notifyall
- finalize: object JVM tarafından destro edilmeden önce çağrılır.
- clone: tüm variablelelerin aynı olduğu yeni bir obje yaratır. bunu user'ın kendisinin override etmesi gerekir. eğer user ovverride etmediyse direk CloneNotSupportedException fırlatacak şekilde default implemente edilmiştir.
- getClass

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# ServletContext
Bir web uygulamasında sadece bir ServletContext olabilir.

ServletContextListener'dan implemente etmiş bir sınıfı spring'e tanıtırsak, ServletContext init olduğunda (yani uygulama deploy olduğunda) ve uygulama durduğunda çalışacak eventleri tanımlayabiliriz (ServletContextListener içerisinde override edilen metodlarda bu event'ler var çünkü).

__javax.servlet.ServletContext__ her Servlet kullanan java uygulamasında olmak zorundadır. Spring ile bağlantısı yoktur. Spring ile entegreli çalışabilmeleri için spring'in sunduğu __WebApplicationContext__ kullanılır. __ServletContext__; __WebApplicationContext__ veya __ApplicationContext__'e alternatif değildir. Tamamen farklı kavramlardır.

Herhangi bir servlet içinde servlet'in kendi configlerine erişmek için bu __ServletConfig__ kullanılır:

```java
ServletConfig servletConfig = getServletConfig(); //getServletConfig javax.servlet.Servlet sınıfında zaten tanımlıdır.
String servletName = servletConfig.getInitParameter("ServletName");
```

Fakat tüm servlet'lerde kullanılacak olan bilgiler ServletContext'ten çekilir:

```java
ServletContext servletContext = getServletContext();
String projectOptions = servletContext.getInitParameter("projectOptions");
```

# request.getSession().getServletContext() vs getServletContext()
__getServletContext()__ Servlet class'ından extend eden sınıfılarda direk kullanılabilir bir metoddur. oysa request objesi herhangi bir kod satırında kullanılabilir. request'ten de ServletContext'e erişilebilir. İkisi aynı instance'ı döndürürler.

# RequestContextListener
Bu sınıftan implemente etmiş bir sınıfı spring'e tanıttığımızda request oluştuğundaki event'lerimizi tanımlayabiliriz.

# DispatcherServlet
Dispatch türkçe kelime anlamı: sevk etmek. yazılım dünyasında metoda/fonksiyona mesaj(parametre) yollama(sevk etme) anlamında kullanılır.

SpringMVC'de __front controller__'ın ismidir.

__DispatcherServlet__, __HandlerMapping__'e basvurararak ilgili Controller bilgisine ulasir. Varsayilan olarak __BeanNameUrlHandlerMapping__ handler olarak kullanilir.

her servlet'in bir url'si vardır. alt-url'ler 1 adet servlet sınıfının kodunun içinde if blokları ile dağıtılır. fakat Sping MVC bunu bizim için otomatik yapar. Spring MVC'nin (request'i ilk karşılayan) servlet'i __org.springframework.web.servlet.DispatcherServlet__'dir.

# WebApplicationContext
__ServletContext__'i içinde barındırır. ApplicationContext'e ek olarak "getServletContext()" metodunu barındırır. __WebApplicationContext__, __ApplicationContext__'in web uygulamaları için uyarlandığı bir türevidir.

örnek web.xml'imizde aşağıdaki servlet tanımımızda spring MVC'nin config'lerini değiştiriyoruz.

```xml
<web-app>

  <listener>
      <!-- Burada application context'in hangi framework loader'ı ile ayağa kaldırılacağını belirtiyoruz. ContextLoaderListener default olarak /WEB-INF/applicationContext.xml dosyasını okur. fakat biz bu örnekte bunu, <context-param> ile override ettik. -->
      <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>

  <context-param>
      <!-- root-context'imiz: applicationContext. app-context içerisinde bean'lerin tanımları mevcut.-->
      <param-name>contextConfigLocation</param-name>
      <param-value>/WEB-INF/app-context.xml</param-value>
  </context-param>

  <!--
  Yukarıda dikkat edilirse xml based bir tanımlama yaptık. Eğer bean'lerimizi annotation ile tanımlamak istersek: 
  <context-param>
      <param-name>contextClass</param-name>
      <param-value>
        org.springframework.web.context.support.AnnotationConfigWebApplicationContext
      </param-value>
  </context-param>
  -->

  <servlet>
      <servlet-name>app</servlet-name>
      <!-- bu servlet'imiz bizim elle tanımladığım değil, spring'in spring-mvc (spring web mvc) modülünde sunduğu front-contoller patternine karşılık gelen servlet'idir. bu servlet exception-handling, view-resolver, request mapping (for redirection of sub-url's to other servlets), MultipartResolver gibi görevleri yapabiliyor. -->
      <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
      <init-param>
          <!-- child-context'imiz: webApplicationContext. dispatcher-servlet-context-1.xml içerisinde bean'lerin tanımları mevcut. bu bean'ler sadece bu DispatcherServlet'in yönettiği Servlet'ler tarafından kullanılabilir. -->
          <param-name>contextConfigLocation</param-name>
          <param-value>/WEB-INF/dispatcher-servlet-context-1.xml</param-value>
      </init-param>
      <load-on-startup>1</load-on-startup>
  </servlet>

  <servlet-mapping>
      <!-- servlet-name bir ID'dir. detayları yukarıda tanımlı. burtada sadece hangi URL'yi karşılayacağı yazıyor. -->
      <servlet-name>app</servlet-name>
      <url-pattern>/app/*</url-pattern>
  </servlet-mapping>

</web-app>
```

Bu tanımı özellikle servlet için yapmak durumundayız. çünkü;
1- web projeleri, war dosyalarından oluşur. app server'lar, war dosyalarını okurken (standartlar gereği), önce web.xml'ini okur. bu sebeple; servlet sınfımızın, spring tarafından yönetildini app server'a belirtmemiz gerekmektedir.
2- Aynı zamanda "dispatcher-servlet-context-1.xml" tanımı olmazsa dispatcher-servlet-context-1.xml'de belirtilen bean'lerimizi ilgili servlet'imizde kullanamayız. Servlet'ler birer "spring bean" olmadıkları için onları inject edebilmemiz için ek olarak "dispatcher-servlet-context-1.xml" tanımlaması şarttır.

Yukarıda 2'inci maddede belirtildiği gibi normal koşullarda servlet'ler bean değildir. fakat bean olarak tanımlanırlarsa spring boot bunları servlet container'a otomatik ekler. kaynak: (source-id: 348) "Registering Servlets, Filters, and Listeners as Spring Beans" başlığı, 1inci paragraf.

Yukarıdaki gibi birçok __DispatcherServlet__'i aynı projede kullanabiliriz. Her __DispatcherServlet__'in url'si farklı olacaktır.

Kısaca özetlersek:

Tek bir jar/war içerisinde aşağıdakiler olabilir:

```
ApplicationContext-1   > WebApplicationContext-1 > servlet-1
                                                   servlet-2 (dispatcher-servlet)
                                                   servlet-3 (dispatcher-servlet)
                                                   servlet-4
                                                   ...
                       > WebApplicationContext-2 > servlet 9
                                                   ...
ApplicationContext-2 > ... ... ...
                       ... ... ...
```

Yukarıdaki şekilden de görüldüğü üzere 1 dispatcher-servlet yada 1 servlet, birden fazla WebApplicationContext'e sahip olabilir. kaynak: (source-id: 349) "1.1.1. Context Hierarchy" 2. paragraf.

Yukarıdaki örnekte;
- __ServletContext__; her "WebApplicationContext-\*" için ayrıdır.
- __ServletConfig__; her "servlet-\*" için ayrıdır.

Sonuç olarak; __WebApplicationContext__ bize __javax.servlet.ServletContext__ ile bütünleşik çalışabilmemizi sağlar. __WebApplicationContext__ aracılığı ile ayağa kaldırılan her bean, __ServletContextAware__'ten implemente ettiği takdirde, __javax.servlet.ServletContext__'e erişebilecektir. 

__ServletContextAware__ koduna bakarsak; ServletContext'in inject ediliğini görürüz:

```java
package org.springframework.web.context;

public interface ServletContextAware extends Aware { 
     void setServletContext(ServletContext servletContext);
}
```

WebApplicationContext genelde 1 uygulamada 1 adet olur. Tabi bu durumda repository, businnes-logic-service'lerimizde WebApplicationContext içerisinde olur. Çünkü servlet'e gelen istekten bu diğer bean'leri çağırmamız gerekecektir. kaynak: (source-id: 349) "1.1.1. Context Hierarchy" 1. ve 2. paragraf.

# spring boot embedded tomcat or jetty server
tomcat gibi app server'lar servlet container barındırır. Bu sebeple spring özel bir ApplicationContext türevi kullanır: ServletWebServerApplicationContext. Bu sınıf aynı zamanda WebApplicationContext türevidir. Bu sınıf otomatik olarak ServletWebServerFactory bean'lerini bulur. Bu bean'lerin impelemntasyonları da runtime sırasında TomcatServletWebServerFactory, JettyServletWebServerFactory gibi karşımıza çıkar.

# Spring Boot
sağladığı en temel yetenek: öntanımlı konfigürasyonlardır. diğer tüm özellikler buradan türer. örnekler:
- Konfigürasyon yapmadan Embeed servler container getiriyor. böylece app server'a atma ihtiyacı duyulmuyor.
- projeye lib olarak database ekledik. eğer database ayarları yapılmadıysa in-memory database açıyor. bunu @EnableAutoConfiguration ile yapıyoruz.

# spring boot version history
| version | released year | change log                                                                                                                                                                   |
|---------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1.1     | June 2014     | improved templating support, gemfire support, auto configuration for elasticsearch and apache solr.                                                                          |
| 1.2     | March 2015    | upgrade to servlet 3.1/tomcat 8/jetty 9, spring 4.1 upgrade, support for banner/jms/SpringBootApplication annotation.                                                        |
| 1.3     | December 2016 | spring 4.2 upgrade, new spring-boot-devtools, auto configuration for caching technologies(ehcache, hazelcast, redis, guava and|infinispan) and fully executable jar support. |
| 1.4     | January 2017  | spring 4.3 upgrade, couchbase/neo4j support, analysis of startup failures and RestTemplateBuilder.                                                                           |
| 1.5     | February 2017 | support for kafka/ldap, third party library upgrades, deprecation of CRaSH support and actuator loggers endpoint to modify|application log levels on the fly.                |
| 2.0     |               |                                                                                                                                                                              |
| 2.1     |               |                                                                                                                                                                              |
| 2.2     |               |                                                                                                                                                                              |

Her sürüm için ayrı ayrı, changelog'lar özet olarak burada açıklanmaktadır: https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.2-Release-Notes


# @SpringBootApplication
bu anotasyon şu 3'ünü içeriyor:

- @Configuration (başka başlıkta anlatılıyor)

- @EnableAutoConfiguration (örneğin projeye lib olarak database ekledik. eğer database ayarları yapılmadıysa in-memory database açıyor. yukarıdaki ikinci madde.)

- @ComponentScan (eğer parantez içinde parametre vermezsek, sadece bulunduğu sınıfın paketindeki ve altpaketlerdeki sınıfları Spring ayarlarına kabul ediyor.)

# AutoConfiguration
tüm oto configuration sınıfları tek bir jar ile dağıtılır: spring-boot-autoconfigure-{version}.jar

Bu sınıflar condition içerir. eğer biz önceden config bean'lerimizi oluşturmadıysak, condition'lar sayesinde AutoConfiguration bean'leri load edilecektir. 

örnek: org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration sınıfında 

```java
@Configuration

// sql lib are in claspath
@ConditionalOnClass({ DataSource.class, EmbeddedDatabaseType.class })

// default properties will be bind, if datasource properties are written in application.properties
@EnableConfigurationProperties(DataSourceProperties.class)

// other depended configurations
@Import({ Registrar.class, DataSourcePoolMetadataProvidersConfiguration.class })

public class DataSourceAutoConfiguration 
{
```

some other auto config classes:

- org.springframework.boot.autoconfigure.web.DispatcherServletAutoConfiguration 
- org.springframework.boot.autoconfigure.orm.jpa.HibernateJpaAutoConfiguration 
- org.springframework.boot.autoconfigure.data.jpa.JpaRepositoriesAutoConfiguration 
- org.springframework.boot.autoconfigure.jackson.JacksonAutoConfiguration

# profiles
uygulama içinde interfaceler @autowired ederiz. runtime sırasında hangi implementasyonun instance olarak ayarlanacağına spring profiller aracılığı ile karar verir.

örnek:
@autowired ile WeatherService ekledik. 

bir implementasyonumuz da bu olsun:

```java
@Service
@Profile({"sunny", "default"})
public class SunnyDayService implements WeatherService {
   ...
}
```

applciation.properties'te;

```
spring.profiles.active=sunny
```

satırı olmalıdır. "default" isimli profil özeldir. dfault aktif hale gelir.

Eğer bir profilde bir component'in hiç scan edilmemesini istiyorsak ünlem işareti kullanırız. örnek:

```java
@Profile({"!sunny","default"})
```

## default implementasyon
spring veya javaee'de bir interface'yi bir sınıfın içinde inject ettiğimiz zaman, framework o nesneye path'te olan bir implementasyonunu atar. path'te en az bir inplementasyon yok ise hata fırlatır.

Aşağıdaki örnekte; request o anda isteği yapan request bilgilerini içerir.

```java
@Autowired
private HttpServletRequest request;
```

Bu durum yukarıda bahsi edilen default implementasyonla bağlantılı değildir. Burada instance'ı ele alıyoruz, yukarıda bahsi edilen durum hangi implementasyonun (yani sınıfın) kullanılacağıdır.

Eğer birden fazla implementasyon classpath'te ise, o zaman önceliği vereceğimiz sınıfın tepesine @Primary yazmamız gerekmektedir.

# conditional beans

MyConditions içerisindeki matches metodunun dönüşüne göre Bean tanımlanıyor yada tanımlanmıyor.

```java
@Bean
@conditional(MyConditions.class)
MyBean myBean(){
  return new MyBean();
}
```

```java
class MyConditions implements Condition {

  boolean matches( ConditionContext cc, AnnotatedTypeMetadata meta){

      // ConditionContext gives info about the environment: classloader, beanFactory...

      // AnnotatedTypeMetadata gives info about the Bean which will be included or not

      if( context.getEnvironment("my_keyword") == null ){

           return false;
      }
      return true;

  }
}

```

# application.properties

spring basladiginda default olarak proje içindeki application.properties dosyasını okur. farklı dosya verilmek istenirse;

> -Dspring.profiles.active=dev -Dspring.config.location=file:C:/application.yml

profillerde dosya içinde --- (üç çizgi) ile ayrışmalıdır:

```yml
spring:
  profiles: dev

prop1: val1
prop2: val2

---

spring:
  profiles: prod

prop1: val1
prop2: val2
  
```

3 çizgi yml formatının bir özelliğidir. kaynak: (source-id: 443) ("4.3.2. Document Boundary Markers" başlığı)

# bootstrap.yml vs application.yml
bootstrap dosyası microservisler ile karşımıza çıktı. config serverdan her servis configlerini aldığı için, spring boot uygulaması ayağa kalkmadan bazı propertieleri tutması gerekli: örneğin; config server'ın portu ve ip bilgisi. microservis; config'den aldığı port numarası bilgisi ile kendisini hizmete açacaktır.

# Aware
türkçe kelime anamı: farkında, tetikte, haberdar

ServletContextAware gibi birçok aware interfacesi vardır. ServletContextAware örnek olarak alınırsa, bu sınıftan implemente ettiğimiz her bean ServletContext'i inject etmesine gerek kalmaz. örnek:

```java
@RestController("/mycontroller")
public myController implements ServletContextAware {

    private ServletContext context;

    @Override
    public void setServletContext(ServletContext context) {

        //setServletContext ServletContextAware interface'sinin bir metodu. "context" private değerine istediğimiz ismi verebiliriz.
        
        this.context = context;
    }
}
```

# sping security
spring varsayılan olarak Authentication tarafı için birçok implementasyonu destekliyor: HTTP Basic, HTTP digest, LDAP... Bunların içinde JWT(JSON Web Token) yok. JWT için implemetasyonu yazılımcının kendisi yapması gerekiyor. Zaten JWT bir security metodu değildir, JWT data transferi yöntemidir.

## Spring security modülleri:

- spring-security-core.jar
  core spring paket'i. aşağıdaki java paketlerini içeriyor: 
  - org.springframework.security.core
  - org.springframework.security.access
  - org.springframework.security.authentication
  - org.springframework.security.provisioning 

- spring-security-remoting.jar

  remote method calling için gerekli.

- spring-security-web.jar

  url based servlet control. filtreler buranın içinde.

- spring-security-ldap.jar

- spring-security-oauth2-core.jar

- spring-security-oauth2-client.jar

  client tarafta java uygulaması varsa bu client kullanılabilir.

- ve diğer modüller

## foundamental process
As we know, Servlets have feature which called Filter. Merging multiple Filters called a filter chain. Spring has it default chain which is called: __org.springframework.security.web.FilterChainProxy__ named as __springSecurityFilterChain__. This class is reponsible for all security things. This class is also an implememtation of servlet-Filter.

When we enable spring boot security default configuration, it adds the __springSecurityFilterChain__ to our servlet. As spring-boot defaults, it registers to front-contoller URL's(servlet). In order to do that, sping-boot adds a filter to our servlet which is called __DelegatingFilterProxy__.

__DelegatingFilterProxy__ is a Filter which invokes a sping managed beans which is also Filter. It named DelegatingFilterProxy, because it invokes another filter which is called "target bean" or "delegate". In this case our target bean is __springSecurityFilterChain__.

We can register our filters the __springSecurityFilterChain__ without __DelegatingFilterProxy__. But that will not be recommended. Also in order to do that, we will need extra configurations.

## ayarlar

asagidaki sınfıta istediğimiz ayarlı belirliyoruz:

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

 @Override
 protected void configure(HttpSecurity http) throws Exception {

  http
    .authorizeRequests()
     .antMatchers("/css/**", "/index").permitAll()
     .antMatchers("/user/**").hasRole("USER")
     .and()
    .formLogin().loginPage("/login").failureUrl("/login-error");
 }

 @Autowired
 public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {

  auth
   .inMemoryAuthentication()
    .withUser(User.withDefaultPasswordEncoder().username("user").password("password").roles("USER"));
 }
}
```

Artık controller taraflarında ekstra bir ayar yapmaya gerek kalmıyor.

## Role
Roller username, password ile aynı tabloda bir string şeklinde saklanabilir.

## SecurityContext
bu sınıf tüm login olmuş kullanıcıların listesini tutar. kullanıcıları Authentication objesi ile saklar.

## SecurityContextHolder
SecurityContext'e direk erişim tavsiye edilmez. SecurityContextHolder aracılığı ile erişebiliriz.

## Authentication
__org.springframework.security.authentication.Authentication__ bir interface'dir. birçok implementasyonu var. örnek:
- UsernamePasswordAuthenticationToken. UsernamePasswordAuthenticationToken'a göre; login olmaya çalışan kullanıcı username ve password bilgisini göndermesi yeterlidir.

## AuthanticationManager
Sadece 1 metodu vardır:

Authentication authenticate(Authentication authentication) throws AuthenticationException

Authentication alır ve authentication objesi döndürür. Aldığı Authentication objesinde henüz granted authorities yoktur. Fakat döndürdüğünde vardır.

Temel akış:
- Authentication implementasyonu (yukarıdaki örnekteki UsernamePasswordAuthenticationToken) AuthenticationManager'a pass edilir.
- AuthenticationManager kendi içinde AuthenticationProvider aracılığı ile kullanıcıyı login eder yada hata fırlatır.
- AuthenticationManager içinde birden fazla AuthenticationProvider olabilir.
- Kullanıcı login olabilirse; AuthenticationManager bir Authentication instance'ı döndürür. bu döndürülen instance SecurityContextHolder.getContext().setAuthentication(…​) metoduna yollanır. setAuthentication metodu o andaki user'ın Authentication instance'ını değiştirecektir.

"Spring security diagram" internette aratıldığında açıklayıcı görseller bulunabilir.

örnek olarak manuel bir kullanıcıyı autahntike edelim:

```java
SecurityContext context = SecurityContextHolder.createEmptyContext(); 
Authentication authentication = new TestingAuthenticationToken("username", "password", "ROLE_USER"); 
context.setAuthentication(authentication);
SecurityContextHolder.setContext(context); // use ThreadLocal for it's values
```

TestingAuthenticationToken yerine UsernamePasswordAuthenticationToken kullanmalıyız.

En sık kullanılan __AuthenticationManager__ implementasyonu: __org.springframework.security.authentication.ProviderManager__

# AuthenticationProvider
Bazı implementasyonları:
- ActiveDirectoryLdapAuthenticationProvider
- AnonymousAuthenticationProvider
- DaoAuthenticationProvider
  
  sadece UserDetailsService ve PasswordEncoder kullanarak username ve password onayı ile çalışır.

- org.springframework.security.ldap.authentication.LdapAuthenticationProvider
- OpenIDAuthenticationProvider
- org.springframework.security.authentication.TestingAuthenticationProvide
- org.springframework.security.oauth2.server.resource.authentication.JwtAuthenticationProvider

## UserDetailsService
interfacedir. birçok implementasyonu var. örnek: InMemoryUserDetailsManager. UserDetailsService sadece şu metodu içerir:

```java
public org.springframework.security.userdetails.UserDetails loadUserByUsername(String username) throws UsernameNotFoundException
```

Spring arkaplanda loadUserByUsername metodunu çağırır. Kullanıcının gönderdiği credentials bilgileri ile UserDetails'i karşılaştırır. Eğer bilgiler uyuşuyorsa kullanıcıyı login eder.

## Subject vs Principal vs User vs realm vs credentials
Bilişim güvenliği dünyasında;

- subject; bir objeye erişmek için izin isteyen yazılım parçasıdır. web tarayıcısı, thread, process, birer subject'tir.

- user: sadece son kullanıcı (bir insan) hesabından bahsediliyor ise bu "user" olarakta kullanılır.

- Principal: identifiable attribute of the subject. like: username, social security number, user ID... kaynak: (source-id: 351) title: "Principal".

- Realm: A Realm is a component that can access application-specific security data such as users, roles, and permissions. kaynak: (source-id: 351) title: "Realm".

- credentials: A credential contains information used to authenticate the subject to services. kaynak: (source-id: 353) 4üncü paragraf.

## SecurityContext metodları
- getAuthentication
- setAuthentication

## Authentication metodları:
- getCredentials: o andaki isteği yapan user'ın credential'i döndürür. credential tam olarak şu demek: kullanıcının login olabilmesi için kullandığı token/şifre veya bunların kombinasyonlarının tutulduğu objedir. Bu metod user otantike olduktan sonra boş dönüş yapabiliyor. bu tamamen güvenliği arttırmak için yapılan tercihi bir tekniktir.

- getDetails: o andaki isteği yapan hakkında ekstra bilgiler içerir: örnek: IP.

- getPrincipal: o andaki isteği yapanın hesabı ile ilgili bilgileri içerir. örnek: username, password, roles, email. dönüş değeri object'tir. bazı case'lerde __org.springframework.security.core.userdetails.UserDetails__ Interface'inin instance'ını döndürebilir.

- isAuthenticated: isteği yapan kullanıcının token'ının onaylanmış olup olmadığı (login olup olmadığı)

- setAuthenticated

- getAuthorities: GrantedAuthority'den implemente etmiş obje listesi döner. Her GrantedAuthority bir işlemin yetkisini ifade eder. örnek: READ_AUTHORITY, WRITE_PRIVILEGE.

## Herhangi bir kod satırında kullanıcı bilgileri çekme
herhangi bir satırda;

```java
Authentication auth = SecurityContextHolder.getContext().getAuthentication();

auth.getPrincipal();
```

metodları çağrılabilir. getPrincipal'ı çağırmak yerine isteğe bağlı controller requestinde şu parametre eklenebilir:

```java
@RequestMapping("/messages/inbox")

public ModelAndView findMessages(@AuthenticationPrincipal CustomUser customUser) {

     //some code here
}
```

# org.springframework.security.web.AuthenticationEntryPoint
It is not Security-core's feature. It is security-web feature.

If a client make an unauthanticated request to a resource (which the client is not authorized) AuthenticationEntryPoint step is invoking.

some implementations:

- BasicAuthenticationEntryPoint

  it only sends HTTP 401 response to client.

- DigestAuthenticationEntryPoint
- Http403ForbiddenEntryPoint

  it only sends HTTP 403 response to client.

- LoginUrlAuthenticationEntryPoint

  redirects to Login page (which is spesified as parameter)

AuthenticationEntryPoint implementations should override this method:

```java
commence(HttpServletRequest request, HttpServletResponse response, AuthenticationException authException)
```

# AbstractAuthenticationProcessingFilter
Creates Authentication instance from request, and pass it to AuthanticationManager.

implementations:

- OAuth2LoginAuthenticationFilter
- OpenIDAuthenticationFilter
- Saml2WebSsoAuthenticationFilter
- UsernamePasswordAuthenticationFilter

## role vs GrantedAuthority
Her role bir GrantedAuthority kümesidir. Yazılımcı; role listesi verildiğinde GrantedAuthority listesi dönen bir metod sunmalıdır. Bunu da UserDetails.getAuthorities() metodunu implemente ederek yapmalıdır.

# Entegrated methods with Servlet

Servlet method calls spring security's method. Those are explained on this link:

(source-id: 444) title: "15.1. Servlet API integration".

## configure metodu içeriği
http objesinin aşağıdaki gibi metodlara ayırmakta fayda var. bu şekilde daha okunaklı oluyor.

```java
@Override
protected void configure(HttpSecurity http) throws Exception {

         // hepsini bir arada yazmamak için metodlara bölüp
         // gruplandırmış olduk
         csrf(http);
         login(http); 
         logout(http); 
         exceptionHandling(http);
         authorizeRequests(http);
}

protected void csrf(HttpSecurity http) throws Exception {

    http
    .csrf().enable();
    /*banka sitemiz olsun. Kullanıcı login oldu ve logout olmadan baska siteye gitti (X sitesi). X kendi içinde bizim bankamıza istek yapabilir. İstek yaparken cookie'yi barındıramayacağı için (çünkü JSESSIONID yada Session-ID bankamıza ait domain spesifik cookie'ye bagli saklaniyor) isteği geçersiz olacaktır. fakat cookie'ler her zaman %100 güven sağlayamıyor. bazen farklı sitelerce yada web tarayıcısı dışından da çekilebiliyor. örnek:
    
    - kötü niyetli web tarayıcı eklentileri ve bug'ları
    - web tarayıcı bug'ları
    - işletim sisteminde kurulu native uygulamanın web tarayıcısından cookie'leri çekmesi
    - X sitesi iframe içinde bankamızı açar ve üzerinde css işlemleri ile bir butonuna basmamızı sağlayabilir...
    
    gibi açıklarla cookie çalınabiliyor veya cookie bir şekilde kullanılarak adımıza request atılabiliyor.

    bu durumu engellemek için spring'in çözümü var. bu çözümde her istek için için sunucu tarafta o anda random bir token üretiliyor. buna csrf-token deniliyor. token client tarafa yollanıyor ve cookie'de saklanmıyor. direk sayfaya gömülü oluyor. bu değeri yazılımcının client tarafta her istekte yollaması gerekiyor. burada yazılımcının da bir şey yapmasına gerek kalmıyor her form alanının içine otomatik spring hidden-input olarak bu değeri sokuyor eğer sayfa jsp/jsf ise. fakat javascript olan sayfalar için iş yaızlımcının kendisine düşüyor. 
    */
}

protected void login(HttpSecurity http) throws Exception {

  http
  .formLogin() // cookie based form login için gerekli ayarlar

          .loginPage("/login") 
          //web sayfası olarak login formunun olduğu sayfa url'si

          .loginProcessingUrl("/loginservice") 
          // /login formu ve diğer login olmak isteyenler buraya istek yapacakalar

          .failureUrl("/loginfailed") 
          //login işlemi başarısız olursa, login http isteği buraya yönlendirilir (redirection)

          .successHandler(authenticationSuccessHandler)
          //success işlemleri eventlerinin tanımlamaları

          .failureHandler(authenticationFailureHandler);
          //fail işlemleri eventlerinin tanımlamaları

    // .formLogin(withDefaults()); 
    // spring will generate a default login page for us.
}

protected void logout(HttpSecurity http) throws Exception {

  http
      .logout() 
      //logout config ayarları

          .logoutUrl("/logout") 
          // default: /logout

          .logoutSuccessUrl("/my/index") 
          // default: /login?logout

          .logoutSuccessHandler(logoutSuccessHandler) 
          // eger bu set edilmisse logoutSuccessUrl ignore edilir

          .addLogoutHandler(logoutHandler)

          .deleteCookies("JSESSIONID");
          // auto olarak silinmesi istenen cookie'ler
}

protected void exceptionHandling(HttpSecurity http) throws Exception {

  http
     .exceptionHandling()
          .authenticationEntryPoint(new Http403ForbiddenEntryPoint());
          //when someone try to access a URL which is not pemitted
}

protected void authorizeRequests(HttpSecurity http) throws Exception {

  http.
     authorizeRequests()

          .mvcMatchers("/login/impersonate*").hasRole(ADMIN_ROLE)
          // only ADMIN_ROLE users can access these URLs

          .mvcMatchers("/login/anotherpage*").hasAuthority(USER_ROLE_1)

          .mvcMatchers("/logout/impersonate*").authenticated()
          // any authenticated user can  access these URLs

          .mvcMatchers("/**").permitAll();
          // allow all (even anonym) users can access these URL's.
          // mvcMatchers("/**") yerine anyRequest()'de kullanılabilir.

          //not: buradaki config'lerde mvcMatchers yerine antMatchers kullanılabilir. fakat MVC request'i ise mvc tercih edilmelidir.

          //not: mvcMatchers("/**") kısmı, authorizeRequestsher() 'ın her zaman sonunda çağrılmalıdır. çünkü authorizeRequests() kısmı URL'leri spesifikten genele doğru bir sıra ile ayarlanmalıdır. farklı bir örnek:
          .antMatchers("/auth/admin/*").hasAuthority("ADMIN")
          .antMatchers("/auth/*").hasAnyAuthority("ADMIN", "USER")
}
```

## Session-based Authentication vs Token-based Authentication
Session-based'de bir random bir id yaratılır ve login olmuş kullanıcının referansı bu olur. kullanıcı bilgileri sunucudadır. JavaEE ve Spring'de bu session-Id default olarak "JsessionID" olarak adlandırılır. yani statefull'dır. burada token; session-id'dir.

Token-based'de ise token random bir string değildir. şifreli ve kullanıcının session bilgilerini içeren bir stringdir. dolayısı ile bilgiler sunucuda tutulmaz. yani stateless'dır. JWT, Token-based'e en iyi örnektir.

jwt içerisindeki blok şifrelenmiştir ve sadece sunucu tarafında açılıp/okunabilir. sunucu taraf kimlere jwt verdiğini bilmez. jwt bir kere üretilir ve sonra salınır. dolayısı ile jwt her geldiğinde içindeki bilgilerde olan son kullanma tarihine bakılır. son kullanma tarihi geçmişse artık bu token geçersizdir. jwt içinde son kullanma tarihi ve userId olması yeterlidir. zaten data kimse tarafından değiştiirlemeyeceği için sunucu bunu güvenle kullanabilir.

jwt'deki sakınca şudur: eğer jwt token'ını hacker çalarsa, o kişi adına jwt'nin son kullanma tarihine kadar işlem yapabilir. hackerın çaldığını sunucu ve client bilsede bunu engelleyemezler. çünkü jwt'lerin geçerliliği sunucu tarafta tutulmamaktadır. sunucu tarafta hiçbir bilgi tutulmamaktadır. bu sebeple genelde jwt'nin son kullanma tarihi çok kısa tutulmaktadır. bu sebeple jwt'de refresh token atyapısı mevcuttur. (baska başlıkta anlatılıyor)

Token-based Authentication'ın avantajı sunucu tarafta datanın tutulmamasıdır. sunucu tarafta birnden fazla aynı işi yapan sunucuları loadbalancer ile bağladığımızı düşünelim. her login datası güncellendiğinde tüm sunucuların senkron olması gerekceke. senkronizasyon işlemi hem sistemi yavaşlatacak hemde sunucu çöküşlerinde sorun yaratacak. cluster'ın olaylarında konfigürasyon gerekecek. jwt bizi bu sorunlardan kurtarıyor. özellikle load balancing yaptığımız sunucular fiziksel olarak uzak mesafelerde ise "Session-based Authentication" facialara sebep olabilir.

## RedirectStrategy
security modülü içinde olan bir Interface'dir. DefaultRedirectStrategy isminde bir implementasyonu mevcut. RedirectStrategy, filter'ların yada authanticationSuccessHandler gibi sınıfıların içinde inject edilir. bu inject edilen nesne ile filter içerisinde gelen istekleri farklı bir url'ye yönlendirmemiz mümkündür. örneğin; login olmuş ve header'ında admin olan kullanıcıyı admin sayfasına yönlendirebiliriz. admin olmayanları ise farklı bir syafaya yönlendiririz.

DefaultRedirectStrategy, sendRedirect(request, response, url); metodunu içerir. url burada yönlendireceğimiz path'tir.

# forward vs redirect
http isteklerinde forward; sunucuya gelen isteği  bir yere yönlendirir. bunu yaparken client'ın bu yönlendirmeden hiçbir haberi olmaz. oysa redirect'te, client'a 30x kodunda repsonse dönülür. aynı response'ta client'ın yapması gereken yeni isteğin nereye olacağı bilgisi de dönülüdür. burada client ikinci isteği yapar. web tarayıcıları bu isteği otomatik (son kullanıcıya sormadan yapar). 

forward vs redirect birçok yerde kullanılan metdo isimleridir. örnek:

- response.sendRedirect("login.jsp");

- request.getRequestDispatcher("login.jsp").forward(request, response);

Dispatch türkçe kelime anlamı: sevk etmek. yazılım dünyasında metoda/fonksiyona mesaj(parametre) yollama(sevk etme) anlamında kullanılır.

# @EnableResourceServer
bu anotasyonun atıldığı service auth2.0 API'si olmaktadır (başka yerde auth2.0 API nedir anlatılıyor.)

# @EnableOAuth2Sso

bu anotasyonun olduğu service auth2.0 client'i oluyor. bu anotasyon aşağıdaki iki anotasyonu içermektedir:

- @EnableOAuth2Client : OAuth2RestTemplate ile yaptığımız isteklerde access-token'ı karşı tarafa otomatik yollamaktadır.

- @EnableConfigurationProperties(OAuth2SsoProperties.class) : eğer yetkisiz istek gerçekleşirse gelen isteği otomatik olarak /login'e (daha doğrusu Authorization Server'a) yönlendirir.

# spring security örnek kod:

```java
@Service

public class CustomAuthenticationManager implements AuthenticationManager {

 @Override
 public Authentication authenticate(Authentication authentication) throws AuthenticationException {

      //authentication nesnesi otomatik dolduruldu spring tarafından. içinde user'ın login olmaya çalışırken yaptığı istekteki bilgiler var.

      // asagida username string'i kullanıcının formdan gönderdiği "username" alanıdır.

      // password ise password alanıdır.

      String username = authentication.getPrincipal() + "";

      String password = authentication.getCredentials() + "";

      // fetch from database

      // User user = dbCOnnection.fetch(username);

      // check password

      //get roles of user

      List<GrantedAuthority> grantedAuths = new ArrayList<>();

      grantedAuths.add(new SimpleGrantedAuthority("ROLE_USER"));

      if(username.equals("ahmet")) {

          throw new AuthenticationException("Engellenmis/bloke kullanıcı");

          //eğer throw edilmeyip null döndürülürse, spring bir sonraki auth-provider ile işlem yapmaya çalışacaktır.
    }

     return new UsernamePasswordAuthenticationToken(username, password, grantedAuths); 
     //bu constructor'ın içinde "super.setAuthenticated(true);" satırı mevcut.
 }
}
```

authenticate metodundan dönen Authentication instance'ı artık o kullanıcın principal ve credentials'ini tutuyor ve her tarafta bu objelere erişebiliyoruz. principal ve credentials birer java obje sınıfıdır. dolayısı ile buralarda istediğimiz herşeyi tutabiliriz.

CustomAuthenticationManager'ı spring'e kullanmasını belirtmeliyiz:

```java
@EnableWebSecurity //bu satır zaten vardı

public class SecurityConfig extends WebSecurityConfigurerAdapter { //bu satır zaten vardı

  @Autowired
  private CustomAuthenticationProvider authProvider;

  @Override
  protected void configure(AuthenticationManagerBuilder auth) throws Exception {

         auth.authenticationProvider(authProvider);
 } 
}
```

# AuthenticationException
AuthenticationException fırlatılacak olan sınıftır. BUnun birçok türevi vardır. Fakat tüm exception'lar sadece string error'u döndürür. farklı bir parametre eklemek istersek ya bu string alanına bir json yazmamız gerekecek yada daha sonraki aşamalarda devreye girecek kod bloklarına yeni kodlar eklememiz gerekecek.

AuthenticationException'dan türemiş bazı sınıflar: AccountStatusException, AccountExpiredExcepitn, DisabledException, LockedExcepitn, BadCredentialsExcepition, UserNameNotFoundExcepiton

# client taraftan login isteğinde username vs password haricinde değer yollama
Authenticate metodu sadece Authentication parametresi alır. "Authentication metodları" başlığına bakılırsa görüleceği credential, details ve principal birer objedir. yani custom bir Authentication nesnesi yaratıp buraya request parameterları ekleyebiliriz. bunun için bir filter eklememiz gerekli:

Securty config sınıfına bunlar eklenmelidir:

```java
@Override //burası zaten olmalı
protected void configure(HttpSecurity http) throws Exception {  //burası zaten olmalı

    http  //burası zaten olmalı

      .addFilter(authenticationFilter())

        .... 

      //addFilter yerine addFilterBefore, addFilterAfter gibi metodlar da mevcut.
}

public MySimpleFilter authenticationFilter() throws Exception {

    MySimpleFilter filter = new MySimpleFilter();

    filter.setAuthenticationManager(authenticationManagerBean());

    return filter;

}
```

Aynı zamanda filter sınıfımızı tanımlayalım:

```java
public class MySimpleFilter extends GenericFilterBean {

  public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain)

    throws IOException, ServletException {

      //get params from request

      //and create token object to pass to next filter or auth-provider

      UsernamePasswordAuthenticationToken token = ...

      chain.doFilter(req, res);
  }
}
```

Yukarıdaki UsernamePasswordAuthenticationToken nesnemizi custom bir obje yaparız ve kendi custom-auth-provider'ımızıda cast ederek kullanabiliriz.

GenericFilterBean'dan türemiş birçok hazır sınıf mevcuttur.

Eğer MySimpleFilter içinde "token.setAutanticated=true; ve SecurityContextHolder.getContext().setAuthentication(token);" yapıp o sesison'daki user'ı otantike yaparsek o istek için auth-provider kodu çalışmayacaktır.

Filterlar user login olmuşsa bile her istekte çalışır. auth-provider'a sadece login olmamışsa yönlendirilir.

# spring'in default filterlarının bazıları:

- ChannelProcessingFilter: en önce olan filter'dır. http'den gelenleri https'e yönlendirme, sendRedirect ile gelen yeni isteklerin nerelere yönlendirileceğini belirten tanımlar mevcut.

- SecurityContextPersistenceFilter: SecurityContextHolder ve HttpSession'ın o request için tanımlanmasını sağlıyor.

- ConcurrentSessionFilter: aynı anda, aynı kullanıcı iki farklı session ile login olabilir (örneği 2 ayrı web browser'dan). bunların yönetimini sağlayan filter'dır. burada bir önceki session iptal edilebilir yada devam etiririlebilir...

- AbstractAuthenticationProcessingFilter'dan türemiş sınıfların olduğu filter'dır. autt-proiver'a Authentication nesnesini hazırlarlar.

# JWT

spring'in içinde default jwt entegrasyonu yok. elle kod yazmka gerekli. BUnu yaparken Java'nın JWT kütüphaneleri mutlaka kullanılmalı, yoksa iş uzar. 

JWT ekleyeceksek security filter şart. JWT yapısında bu şekilde kullanıcıyı header'ındaki bilgi ile her istekte login olup olmadığını tespit edebiliriz.

JWT yapacaksak refreshToken, createToken gibi tüm metodlarımızı için rest-controller  açmamız gereklidir. bu metodlara tüm doğru user bilgisi olan kişiler erişebilmelidir. bunun için bir ROLE belirlemek gerek. BU role her user'da olmalı. çünkü herkes bu metodlara erişebilmelidir.

JWT'de login işleminide rest servisine bağlamamız gerekli. Login tamamen public bir metod/url olmalı. Login controller'a "@Autowired AuthenticationManager" 'ı inject edip, login metodunda token'ı oluşturup authenticationManager.authenticate(token) metodunu çağırmalıyız. auth-provider'ımızı burada çalışacaktır. ve login metodunun sonunda da kulanıcıya header'a eklemesi gerek JWT Token'ımızı dönmeliyiz.

# Method security
Main sınıfımıza @EnableGlobalMethodSecurity(securedEnabled = true) eklenmelidir. Daha sonra herhangi bir metodun yetkisini kısıtlmak istediğimizde o metodun tepesine anatation atarız. örnek:

```java
@Secured("ROLE_USER")
public String myMethod() {
    return "Hello";
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# dependency Injection types

## Constructor-based

```java
public class Service {

  private Collaborator collaborator;

  Service(Collaborator collaborator) {

    this.collaborator = collaborator;
  }
}
```

## Setter-based

```java
public class Service {

  private Collaborator collaborator;

  @Required
  public void setCollaborator(Collaborator c) {
    this.collaborator = c;
  }
}
```

## field-based

```java
public class Service {
  @AUtowired
  private Collaborator collaborator;
}
```

# Avantajlar ve dezavantajlar
- field-based daha sade-okunabilirdir. diğerlerinde kod blokları daha uzundur.
- field-based olmayanlarda instance'larını kontrol etme ve kontrol sonrası duruma göre aksiyon alabilmemiz mümkündür. ne gibi kontroller yababiliriz:
  - inject edilen sınıfların null gelme durumları
  - inject edilen sınıfların içindeki default variable değerlerini kontrol etme durumu
  - inject edilen sınıfların hangi class referansı olduğu durumu. çünkü spring duruma göre (profillere, classpath'e göre) farklı çeşit class'lar inject edebilir.

Constructor-based'de tüm instance'ları tek bir metodda kontrol edebiliriz. bu şekilde bir instance'ın özel bir durumu diğerini etkileyebilir. oysa setter-based'de sadece ilgili instance için aksiyon alabiliriz.

bir sınıfımıza gereğinden fazla field eklediğimizi düşünelim. bu sınıfı parçalara bölmek genelde doğru bir çözüm olmaktadır. eğer constructor-based injection kullanırsak, static code analizi yapan eklentiler bizi constructor çok fazla eleman kabul ediyor diye uyaracaktır. fakat field ve setter based injection'larda bu uyarıları alamayız.

Field-based injection yapılan bir sınıfı spring app container'sız init etme şansımız yok (tek şansımızı reflection kullanmak).  bu sebeple spring continer'sız çağrılabilecek sınıflar (bu durum bazen spring kullanılmayan unit testlerimizde olabiliyor) var ise o sınıfların içinde field-based constructor kullanmamalıyız.

# circular dependency
A bean'i B sınıfını inject ediyor ve B sınıfı, A sınıfını inject ediyorsa runtime sırasında BeanCurrentlyInCreationException hatası alırız.

Bu durum bir anti-pattern'dir. Mimari yeniden düzenlenmesi önerilir. Fakat redesign yapılamazsa birçok workarround çözümleri vardır. bazıları:

- circular dependency yaratan bean'lerin inject edildiği yerlere @Lazy anotation'u koymak. 
- setter-based injection kullanmak.

Bu workarround çözümler temelde şunu yapar: spring, circular dependency problemi çıkaran bean'leri aynı fazda initialize etmez. spring birini sonradan initialize eder. böylece circular dependency problemi olmaz. Örneğin; constructor injection yapıldığında tüm field'ları spring aynı anda initialize etmeli ki constructor çağrılabilsin. Bu sebeple constructor injection'da circular dependency problemi alabiliriz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# app server vs web server
Web suncusuna bir istek geldiğinde, sunucu bu isteği basitçe en iyi karşılayabilecek programa aktarır. kısacası; yapılan çağrıları ilgili yerlere aktarmaktır ve dönen cevabı döndürmektir. load balancing, caching, gibi bir çok ek işlevi de yapabilir..

örnek sunucular: Apache HTTP Server, nginx

uygulama sunucusu ise; iş mantığını yürüten (işleten - üzerinde uygulamlacıklar çalıştıran) ve API sunan bir motordur.

örnek sunucular: GlassFish, weblogic, jboss (or WildFly), IBM WebSphere

Java dünyasının standartlarına göre; "EJB Container" içermeyen hiçbir yazılım uygulama sunucusu olamaz. Bu tanıma göre; tomcat bir web sunucusudur.

benzer şekilde sadece web sunucusu olanlar: Jetty

# uygulama neden sunucuya ihtiyaç duyuyor?

her java app server birer JavaEE implementasyonudur. JavaEE kütüphaneleri maven'a eklenirken interfaceler ve abstractlar bazen de sınıflar tanımlanır. fakat uygulama ayağa kalkması için runtimede bunların implementasyonlarına ihtiyaç duyar. her uygulama sunucusu JavaEE'yi kendisi farklı implemente etmiş olabilir.

Bir "web" uygulamasını ayağa kaldırabilmek için en az "Servlet Container"'a ihtiyaç vardır. İşte bu kütüphane tüm app serverlarda + tomcat'te dahi mevcuttur. Spring-framework uygulaması dahi bunu yapmaya zorunludur. Fakat spring bu kütüphaneyi direk olarak kendi içinde bulundurmaktadır. Daha sonra hayata geçirilen Spring-boot projesi bu kütüphanelerin uygulama içerisine gömülmesini daha çok kolaylaştırmaktadır. Spring projesini bir app server'da çalıştırdığımızda, spring uygulaması app server'ın "servlet container"'ını kullanabilir.

Servlet container bu sebeple "web container" olarak ta adlandırılmaktadır.

not: Spring sadece 'servlet container'a ihtiyaç duyuyor. Oysa javaee bir spesifikasyon ve komple tüm library'ler sunucu içerisinde.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# deployment descriptors

| file                   | platform        | directory           |
|------------------------|-----------------|---------------------|
| application.xml        | Java EE         | META-INF            |
| application-client.xml | Java EE         | META-INF            |
| beans.xml              | CDI             | META-INF or WEB-INF |
| ra.xml                 | JCA             | META-INF            |
| ejb-jar.xml            | EJB             | META-INF or WEB-INF |
| faces-config.xml       | JSF             | WEB -INF            |
| persistence.xml        | JPA             | META-INF            |
| validation.xml         | Bean Validation | META-INF or WEB-INF |
| web.xml                | Servlet         | WEB-INF             |
| web-fragment.xml       | Servlet         | WEB-INF             |
| webservices.xml        | SOAP            | META-INF or WEB-INF |

# "Java EE deployment descriptors" vs "runtime deployment descriptors"
JavaEE implementasyonları (app server'lar) kendi içlerinde ek olarak xml istiyor olabilir. bunlar "runtime deployment descriptors"tır. örnek: sun-application.xml, sun-web.xml.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# annotation
türkçe kelime anlamı: dipnot

annotationlar birer @interface annotation'undan türemiş objelerdir. örnek:

tanım:

```java
@Target(ElementType.METHOD) //annotation nerelerin önüne koyulabilir

@Retention(RetentionPolicy.RUNTIME) //annotation hangi adımlarda kullanılacak (runtime, source, class olabilir)

@interface Todo { //annotation ismi

 public enum Priority {LOW, MEDIUM, HIGH} //annotation'un parantez içinde verilen bir parametresi

 public enum Status {STARTED, NOT_STARTED} //annotation'un parantez içinde verilen bir parametresi

 String author() default "Yash"; //annotation'un parantez içinde verilen bir parametresi

 Priority priority() default Priority.LOW; //annotation'un parantez içinde verilen bir parametresi

 Status status() default Status.NOT_STARTED; //annotation'un parantez içinde verilen bir parametresi

}
```

kullanım:

```java
@Todo(priority = Todo.Priority.MEDIUM, author = "Yashwant", status = Todo.Status.STARTED)
public void myMethod() {

          //Some code here...
}
```

# annotation kendi içinde nasıl businnes logic uyguluyor?
- RetentionPolicy.RUNTIME
  Runtime sırasında iş yapan annotationlar (): Runtime sırasında annotation'u sunan framework reflection kullanarak hangi sınıflarda annotation varsa a onları buluyor. her annotation'un içinde tuttuğu bir data var. bu data'lar annotation çağrılınca yazılımcı tarafından veriliyor. bunları kullanarak runtime sırasında framework businnes logic uyguluyor.

  Diğer fazlarda (compile gibi) çalışan annotation'lar farklı şekilde işliyor.

- RetentionPolicy.SOURCE
  @Override, @SuppressWarnings gibi sadece IDE'lerin görmesi beklenen, derleme sırasında önemsenmeyen ve derlenmeyen annotation'lardır.

- RetentionPolicy.CLASS
  derleme sırasında kullanılırlar fakat derlenip class olarak kullanılmazlar. örneğin; compile sırasında dökümantasyon oluşturmak için kullanılabilirler. 

  CLASS annotation'ları derleme sırasında java derleyicisi tarafından çağrılırlar. İşte burada "java source code generator" yazılımı ortaya çıkıyor. java derleme yaparken farklı source code generator'lar kullanmamıza izin veriyor. eğer farklı bir generator (processor) kullanmak istiyorsak java compiler'ına bunu belirtmek gerekiyor.

  örnek:

  - komut satırından: javac -processor com.MyProcessor Person.java

  - maven'dan:

```xml
<build>
  <plugins>
      <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <configuration>
              <annotationProcessors>
                  <annotationProcessor>
                      com.MyProcessor
                  </annotationProcessor>
              </annotationProcessors>
          </configuration>
      </plugin>
  </plugins>
</build>
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Class objesi
Class bir sınıftır. Bu sınıf her sınıfın içinden myClassIntance.getClass() yada (static) MyClass.class ile çağrılabilmektedir. bu iki değerin referansı birbirine eşittir. 

Class sınıfı, MyClass'ın özelliklerini yansıtan metodlar içermektedir. Bu şekilde MyClass hakkında bilgiler alabilmekteyiz. örneğin; myClass'ın ismi, paket ismi gibi…

# Class objesinde olan bazı metodlar/property'ler:

- static forName(String className) : metoddur. Bu metoda herhangi bir sınıfın ismi string olarak gönderilebilir. bize gönderdiğimiz sınıf için Class objesini döndürecektir. Örnek: Class myCarClass = Class.forName("Car");

- getAnnotation(Class < A > annotationClass): parametre aldığı annotation sınıfından ilgili sınıfta var ise o annotation'u döner. java.lang.annotation.Annotation döner. bu sınıfı tüm annotation'lar extend eder.

- Annotation[] getAnnotations(): o sınıfta kullanılantüm annotation'ları dönder.

- ClassLoader getClassLoader(): ilgili sınıfın clasloader'ını dönüyor.

- diğer metodlar: enum olup olmadığı, field'lar, anonym olup olmadığı...

# reflections (or yansımalar)
java.lang.reflections paketleri altında olan bu sınıflar, metodlar ve sıfınılar hakkında meta bilgileri alabilmemiz ve hatta gerektiğinde ismi ile aşağıdaki örnekte görüldüğü gibi metodları execute edebilmemizi sağlayabilmektedir.

```java
Method m = valueObject.getClass().getMethod(methodName, new Class[] {});

Object ret = m.invoke(valueObject, new Object[] {}); //m isimli metoda parametre yolluyoruz
```

Çok sade bir örnekle java'da reflection'ları incelersek:

```java
Class insanClass = Insan.class;
Field surnameField = insanClass.getField("surname"); // surnameField sadece meta bilgidir. bir instance değildir.

Insan ahmet = new Insan("ahmet", "kara"); // name: ahmet, surname: kara

String surname = surnameField.get(ahmet); // ahmet instance'ının surname'ini çağırdık. bize dönüş değeri yine instance'tır.

surnameField.set(ahmet, surname); // ahmet instance'ının, surname değerini set ediyoruz (tekrar aynı değerle set etmiş oluyoruz. örnek olsun diye yapıldı.)
```

# java arrays
Obje sınıfından türemiştir. fakat runtime'de dinamik oluşturulurlar. örnek:

```java
int[] x = new int[3];

System.out.println(x.getClass().getName()); //ekrana [I basar. int[][] ise [[I basar.  [[I sınıfı dinamik oluşturulur.
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# jrebel
JVM için yzılmış bir bir Classloader extension'udur. Varolan classloader'a ek olarak kendi logic'lerini çalıştırır. Birçok IDE için yazılmış eklentisi de vardır.

jrebel ile deploy edilen uygulama (app server içerisinde çalışsa dahi) hot-deploy yapılabiliyor. sadece değişen java sınıfları deploy ediliyor ve uygulama restart istemiyor. normalde javada hotdeploy özelliği var fakat metod imzası değişmesi gibi durumları desteklemiyor. bu eklenti ile daha fazla durumda hotdeploy yapılabilmesi sağlanıyor.

ASM ve Javassist framework'leri, bytecode'u runtime sırasında manipüle edebilmek için kullanılan projelerdir. jrebel'da bunlara alternatif bir yazılım geliştiriyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# war (web application archives) vs ear (enterprise archives) vs jar (java archive)

- jar sadece java sınıfları ve resource'leri barındırır.

- war, jar'a ekstradan, servlet ve jsp dosyalarını barındırır.

- ear ise servlet (war) + "ejb modülü" olarak ayarlanmış jar dosyaları bulundurması gerektiğinde kullanılır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# JVM memory spaces

- Heap Space
  - Young Generation
    - Eden Space : 'new' keywordü ile oluşturulan her nesne bu alanda tutulur
    - Survivor Space : garbage collector (or GC), "eden space" alanını gezip ölü nesneleri yokeder. yaşayanları bu alana taşır.
  - Old Generation
    - Tenured Space: garbage collector, "Survivor space" alanını gezip ölü nesneleri yokeder. yaşayanları bu alana taşır.
- Non-Heap
  - Permanent Generation (PermGen) : JVM'in uygulamanın içindeki sınıfların meta bilgilerini (metod imzaları gibi) tutmak için kullandığı alandır.
  Java8 Update: PermGen is replaced with Metaspace which re-sizes dynamically at runtime.
  - Code Cache (Virtual or reserved) : hotspot kod kısımlarının, native kod'a çevrildiğinde saklandığı cache bölgesi

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# apache commons
birçok java kütüphanesi barındıran projenin ismidir. altındaki kütüphaneler birçok  amaç için yazılmıştır. sadece ihtiyaç duyulan kütüphanenin jar dosyası ayrı ayrı indirilmektedir. alt modüllerin bazıları:

- commons-codec: General encoding/decoding algorithms (example: phonetic, base64, URL).

- commons-lang: extra feature for java.lang (core java library)

- commons-cli: command line argument passer

- commons-collection: datastructures library

- commons-dbcp: jdbc üzerinde pool'ların yönetimini yapmamızı sağlayan kütüphane. ORM kütüphanesi değildir.

# Google Guava
apache commons gibi birçok farklı iş için geliştirilen java kütüphaneleri grubudur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# JNDI (or Java Naming and Directory Interface)
Java API'sidir. 

propertie dosyalarından okurmuş gibi obje yaratabilmemizi sağlamaktadır:

```java
Context context = new InitialContext(); 

MyDataSource ds = (MyDataSource) context.lookup("service-name");
// genelde bu şekilde isimlendirilir: jdbc/UrDataSourceName
```

Yukarıdaki kodun çalışabilmesi için bu kod satırı çalışmadan önce uygun servis'in init edilmiş olması gerekmektedir:

```java
MyDataSource ds = new MyDataSource();

ds.setPassword("abc");

Context context = new InitialContext(); 

context.bind("service-name", ds);
```

JNDI en çok database bağlantıları ve LDAP gibi sistemler için kullanılıyor. Örneğin; tomcat, jboss bize JNDI ile database'e bağlanabilmemiz için kendi data-source nesnesini döndürüyor. bu nesneyi kendi tabımlıyor, biz tüm deploy ettiğimiz java uygulamalarından bu JNDI'ları okuyabiliyoruz. Okduğumuzu bu JDNI objelerinden örneğin; daatbase connection'ı açabiliyoruz.

MyDataSource objemiz istediğimiz custom metodları barındırabilir. örneğin; dbDataSOurce.getConnection(); gibi...

MyDataSource yerine herhangi bir EJB objemiz de olabilir. örnek:

```java
MyObject myObject = (MyObject) context.lookup("myObject");
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# modes of jvm
client ve server mod var. client daha çok jit kullanmayı sever. oysa server mode daha uzun vadede istatistik toplayıp, ilgili kod bloklarını daha yavaş şekilde jit kullanmaya başlar. yeni olarak "tiered compilation" modu gelmiştir. bu mod hem client hemde server karışımıdır. bu mod; uygulamanın başlangıcında client mod temelli çalışır, daha sonraki zamanlarda server mod temelli çalışır.

"java -version" komutu ile jvm'in çalıştığı mode çıkıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Garbage Collector
Yaptığı işlemlere teknik özel isimler verilmiştir. JVM parametresi geçmek gerektiğinde, yada GC'nin algortimaları araştırıldığında bu terimlere ihtiyaç duyulabilir.

# mark
scan and marking all reachable (kullanılan) objects

# sweep
scan and free unmarked objects

# copy collection
coping collection to another memory block (example: from eden to survivor space)

# paralel collection
GC uses multiple threads for itself

# concurrent collection
GC uses concurrent threads for itself

# compacting
moves objects inside memory for defrag

# stop the world
GC pause all app threads to finish its job

# minor collection
garbage collection for young generation

# major collection
garbage collector for old generation

# Types of GC
GC kullandığı algoritmalara göre ayrılmaktadırlar:

- Serial collector
  - tek cpu'lu cihazlara uygun
  - GC işe başladığında tüm sistemi durdurur
- Parallel (throughput) collector
  - multiple cpu'lar için uygun
  - GC paralel thread'ler açarak işlem yapıyor
  - GC işe başladığında tüm sistemi durdurur
- concurrent (or CMS or concurrent-mark-sweep) collector
  - old generation için arkaplanda sürekli GC işlemi yapar. bazen sistemi durdurur bazen durdurmaz. bu mantığa low-pause collection deniliyor.
  - young generation için hep sistemi durduruyor
  - GC kendi içinde concurrent çalışmaktadır (paralel'den farklı mantıktır. başka başlıkta anlatıldı.)
- G1 (or garbage first) collector
  - CMS ile benzer mantıkta çalışmaktadır.
  - çok büyük heap size verilmiş sistemler için uygun.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# JVM components

# byte code verifier

kodları okuyup jvm sürümüne uygunluğunu ve validation'ununu yapan mekanizmadır.

# class loader

class'ları bellekten okuyarak JVM'e aktarır. classloader'da bir java sınıfıdır yada sınıflar grubudur. aynı jvm'de her app farklı classloader kullanabilir. tomcat ve spring'in kendi classloaderları var.

- jvm'in içindeki default classloaderın ismi "bootstrap class loader (or primordia class loader)"'dır. bunun asıl amacı /lib ($JAVA_HOME\lib\rt.jar ve diğerleri) dizinindeki core jre kütüphanelerini import etmektir.

- "Extension Class Loader" ise bootstrap'in bir child'ıdır. bootstrap tarafından çağrılır. \lib\ext\ içini yükler.

- "Application Class Loader (or System Class Loader)" ise Extension tarafından çağrılır. Extension'ın child'dıdır. jvm başlatılırken, jvm'e paramtre geçilen path'lerden class'ları yüklemekle görevlidir.

# execution engine

ya JIT yada interpreter'a iletilerek kodun çalıştırılmasını sağlar.

# garbage collector

boş referanslı verileri temizlemektedir.

# security manager

private metodları çağırılmasını engellemek gibi güvenlik duvarı görevi görmektedir. jvm'e parametre geçilerek herşey serbest bırakılabilmektedir.

# Tomcat classloader

Tomcat sırası ile bunları işletir:

- JVM's bootstrap classloader (with it's child-class loaders)

- System class loader

  $CLASSPATH variable'ında olan sınıfları yükler. fakat /tomcat/bin/catalina.sh or /tomcat\bin\catalina.bat script'i CLASSPATH değerini ignore eder ve CLASSPATH'e kendisi /tomcat/bin/ içerisindeki bazı lib'leri yükler.

- Common class loader

  Aşağıdakileri load eder:

  - unpacked classes and resources in $CATALINA_BASE/lib
  - unpacked classes and resources in $CATALINA_HOME/lib
  - JAR files in $CATALINA_BASE/lib
  - JAR files in $CATALINA_HOME/lib

- WebappX

  sadece bu classloader'dan yüklenen class'lar webapp'a özeldir. diğer web app'ler bunları göremez. bu dizinleri sırası ile yükler:

  - /WEB-INF/classes
  - /WEB-INF/lib

Tomcat'in loader configurasyonunda aşağıdaki belirtildikçe yukarıdaki sıra geçerlidir. eğer aşağıdaki belirtilmişse sıra aşağıdaki gibi olur:

```xml
<Loader delegate="true"/>
```

- bootstrap of jvm
- WebappX
- System
- Common

Tomcat'te default açık olmayan classloader'lar:

- Server: sadece tomcat'in görebildiği kütüphaneler.
- Shared: tüm web uygulamalarından görülebilen kütüphaneler. buradakilerin tekrar yüklenmesi için tomcat'in restart edilmesi gerekir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# jvm parametreleri
jvm paramtrelerinde -x ile başlayanlar her jvm de farklı implemente edimiş olabilir. fakat x'siz başlayanlar her vm'de olmak zorundadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# exceptions

# try with resource 
try parantezinin içinde olan BufferedReader java.lang.AutoCloseable'dan implemente eder. bu şekilde java onu hata olursa otomatik kapatır.

```java
try( BufferedReader br =new BufferedReader(new FileReader(path)) ){

   return br.readLine();

} catch (Exception e) {
    //no need to close the "BufferedReader br"
}
```

# class hiyerarşisi

- Object

  - Throwable

    - Error

      - VirtualMachineError

        - InternalError

        - OutOfMemoryError

        - StackOverflowError

        - UnknownError

      - AssertionError

      - OutOfMemoryError

      - ThreadDeath

      - AnnotationFormatError

    - Exception

      - RuntimeException

        - NullPointerException

        - ArithmeticException

      - IOException

        - FileNotFoundException

- Tüm throwable nesneleri throw/catch edilebilirdir.

- Error ve altındaki objeler manuelde "throw new OutOfMemoryError()" şeklinde fırlatılabilirler. fakat catch edilmek zorunda dillerdir.

- Error'lar ne kadarda genel VirtualMachine sorunları gibi gözükselerde, Exception'lar gibi belirli bir satırdan fırlatılırlar. Örneğin OutOfMemoryError tam olarak bu satırdan fırlatılabilir: "new byte[999999999];"

# Checked exception vs unchecked exception
bazı Throwable'lar catch edilmek zorundadır. yoksa kod compile edilemez. catch edilmek zorunda olan Throwable'lar "checked"'dır.

RuntimeException ve Error ve bunların subclass'ları haricindeki tüm Throwable'lar checked'tır.

Eğer unchecked exception yaratmak istiyorsak, yeni exception'umuzu unchecked excepiton'lardan türetmeliyiz.

# finally block on java

finally metodu her türlü çalışır. thread'in try veya exception bloğuna girmiş olması, hatta önceden "return" çarılmış olması birşey ifade etmez. örnek:

```java
public static void main(String[] args) {
  System.out.println(test1());
}

public static int test1() {
  try{
      System.out.println("try");
      return 1;
  }catch (Exception e){
      // any code here...
  }finally {
      System.out.println("finally");
      return -1;
  }
}
```

prints:

```
try
finally
-1
```

# best practices
- istisnalar dışında; sadece checked olan Throwable'lar fırlatılmalıdır. örneğin; arithmeticexcepiton (uncheckted) fırlatılmamalıdır. çünkü zaten unchecked excepiton'lar JVM tarafından fırlatılıyor. Tekrar yazmanın bir anlamı yok. kod kalabalığı yaratırız. örnek:

  ```java

  if( a == 0){
    throw new ArithmeticException();
  }
  return b/a;
  ```

  Yukarıdaki kod sadece kod kalabalığı yaratmaktadır. zira arithmetic excepiton bu metodu çağıran yazılımcı tarafından yakalanmak zorunda diildir.

- her çeşit exception ayrı ayrı fırlatılmalıdır. hepsi gruplanıp fırlatılmamalıdır. böylece yakalan metod ne her exception çeşidi için ayrı ayrı ne yapacağına karar verebilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Java Specification Requests (or JSR)

Java ve JavaEE için toplulukların yayımladığı spesifikasyon yayımlarıdır.

# JDK Enhancement Proposal (or JEP)

OpenJDK için toplulukların yayımladığı spesifikasyon yayımlarıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# @transient

basic java annotation'ıdur. serialize edilirken bu objenin esgeçilmesini sağlar. gson ve diğer tüm serialize etme kütüphaneleri bu değeri kullanır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# remote debug

java uygulaması çalıştırıldığında debug parametresi ile başlatılır ise; jvm bir port üzerinden "debugger" uygulamasının kendisine bağlanmasına izin verir. debugger uygulaması genelde bir IDE'dir. IDE uygulamaya bağlanır. IDE üzerinde önceden proje tanımlanmıştır, bu şekilde source code ile java uygulaması arasında ilişki kurulabilir.

bir uygulamayı localde IDE ile debug ettiğimizde, IDE arkaplanda bu işlemi yapar fakat yazılımcıya farkettirmez. remote=localhost olur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# java Serializable

bi sınıfın içindeki anlık değerler ile byte olarak kaydedilmesidir. De-Serialization işlemi ise byte dizisinden java sınıfına aktarılmasıdır. byte'a çevrilecek sınıf  Serializable sınıfının implemente etmek zorundadır.

# serialVersionUID

bu deger Serializable'dan implemente edilmiş sınıflarda olmalıdır. bu deger byte'a çevrilen sınıfın içine gömülür. byte dizisinden De-Serialization yapıldığında eğer sınıfın serialVersionUID'si aynı ise De-Serialization uyumlu buldugu tüm degerleri sınıf degerlerine doludurur. eğer serialVersionUID farklı ise, direk olarak hata alınacaktır. bu sebeple yazılımı geliştirirken serialVersionUID 'leri manuel atamakta yarar var. aksi durumda derleme sırasında bu değerler rastgele atanacak ve dosyadan De-Serialization işlemlerinde aynı serialVersionUID olmayacağı için, yeni alan eklenmiş sınıflara dahi De-Serialization olumlu sonuçlanmayacaktır.

# Eclipse'in sunduğu otomatik serialVersionUID seçenekleri

1- default serialVersionUID: 1L (long tipinde 1 değeri) atanır. serialVersionUID degeri önemsiz olan sınıflara atılması için önerilir.

2- oto generated serialVersionUID: sınıfın içindeki tüm değişkenlere bakılır. tüm bu değerlere göre bir hash üretilir. bu hash ile serialVersionUID oluşturulur. bu algoritma ile aynı aynı olan tüm sınıfların serialVersionUID'leri aynı olacaktır. bu şekilde başka bir yazılım tarafından okuanan serialize edilmiş veri başarılı şekilde okunabilecektir. java sınıfımızda bir değişiklik yaptığımızda serialVersionUID otomatik değişecektir. artık modelimiz serialize edilmiş dosyadan okuyamayacaktır. zaten beklenen de budur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# java SE (or java standart edition or old-name:J2SE) vs java EE (or Jakarta EE or java enterprise edition or Java 2 Platforms or java Platform or old-name:j2ee)

ortalama bir desktop bilgisayar ihtiyaçlarını karşılayan platformlar için java-runtime içinde bulunan kütüphanaler javaSE grubudur.

javaee, javase'yi kullanan ekstra kütüphanaler içerir. runtime sırasında hangi kütüphanelerin olup olmayacağına çalışan uygulama (sunucu) belirler. ek kütüphanaler jar'ın içinde yada classpath'te bulunmalıdır. bu kütüphaneleri barındıran sunucular glashfish, weblogic'tir.

# sürümler

jre'nin sürümleri ile jdk aynı olmalıdır (or geriye uyumlu modda çalışılır). fakat javaEE'nin sürümleri jre'den bağımsızdır. Fakat javaEE jre ile aynı zaman dilimlerinde aynı sürüm numaralarını kullanmaya çalışır. bu tamamen isteğe bağlı yapılan bir seçimdir.

javase version history:

(eskiden jdk ile bütünleşik geliyordu, bu sebeple ilk isimleri jdk olarak geçmektedir)

- JDK 1.0 (1996)

- JDK 1.1 (1997)

- J2SE 1.2 (1998)

- J2SE 1.3 (2000)

- J2SE 1.4 (2002)

- J2SE 5.0 (2004)

- Java SE 6 (2006)

- Java SE 7 (2011)

- Java SE 8 (2014)

- Java SE 9 (2017)

- Java SE 10 (2018)

- Java SE 11 (2018)

- Java SE 12 (2019)

- Java SE 13 	(2019)

- Java SE 14 	(2020)

- Java SE 15 	(2020)

- Java SE 16 (2021)

javaEE version history

- 2EE 1.2 (1999)

- J2EE 1.3 (2001)

- J2EE 1.4 (2003)

- Java EE 5 (2006)

- Java EE 6 (2009)

- Java EE 7 (2013)

- Java EE 8 (2017)

# jdk (or java development kit)

jdk içinde javaee kütüphaneleri bulunmaz.

jdk içinde; wsimport (web service yaratma tool'u), keytool (sertifika import/export tool'u) gibi birçok utility + jre + compile tool'ları bulunur.

# oracle jdk (or old-name:sun jdk) vs openjdk

(not: jdk'lar kendi içlerinde kendi jvm'lerini içermektedirler.)

OpenJDK, javaSE'nin 7'inci sürümü ile artık referans implementasyon olmuştur. yani sadece desktop makinalar için jvm implementasyonu olarak openjdk gösterilidir. yani; artık oracle jre'si openjdk üzerine kuruludur. eskiden de openjdk ve oraclejdk birbirleri ile ortak kodları kullanarak ilerliyorlardı, fakat 7inci sürüm ile artık kesin olarak oraclejdk, openjdk implementasyonu olacağı garantisi verilmiştir.

oracle-jdk ie openjdk arasındaki farklar şunlardır:

- oraclejdk'nın lisansı farklıdır

- Java Plugin and Java WebStart

- JRockit Mission Control (detaylar baska yerde yazıyor)

- font'lar

- bazı ek kütüphanaler

- oracle jdk 11 ve jvm 11 artık ücretli olmuştur. her canlıya atılan paket için oracle'a ücret ödenmelidir.

Openjdk aslında sadece soruce code'u temsil etmek için kullanılan bir terimdir. AdoptOpenJDK; openjdk'yı manipüle edip derlemektedir. aşağıda farklı başlıkta detaylı tablosu mevcut. 

# IcedTea

openjdk'yı geliştiren community tüm OS'ları desteklememektedirler. bu sebeple farklı bir topluluk openjdk'yı diğer OS'lara entegre eder. yani openjdk'yı farklı platformlar için build eder.

# IcedTea-Web

openjdk'da olmayan bir ek modüldür. bu modül web tarayıcıları için java eklentisi sunar. java-plugin'e açık kaynaklı alternatiftir.

# Eclipse Enterprise for Java (or EE4J)

JavaEE oracle tarafından geliştiriliyordu. 2017'de oracle eclipse vakfına geliştirmeyi bıraktı. eclipse ise JavaEE'yi, JakartaEE olarak değiştridi. JakartaEE ve onunla ilişkili diğer tüm projeler için root proje olarak EE4J ismi verildi.

# WebStart vs java plugin

java plugin; web tarayıcıya kurulan eklentinin ismidir.

WebStart; appletlerin bir sonraki adımı gibi düşünülebilir. local siteme uygulama (applet benzeri ufak uygulama) indirme, çevirimdışı daha sonra açmak için işletim sistemine kısayol atama, kurulan uygulamaları yönetebilme, sürüm güncelleme gibi işlevlerin yapılmasını sağlar. bu uygulamalar tarayıcıdan direk olarak kurulabilir. bu uygulamacıklarda permission'lar çok kısıtlıdır.

# java applet

java runtime'a ihtiyac duyar. client tarafta tarayıcı üzerinden java-plugin aracılığı ile uygulama çalıştırır.

# javafx

masaüstü uygulaması yazılmasını sağlıyor. ek olarak webview kullanımını kolaylaştırmıştır. vewbview içerisini editleme ve üzerinde farklı syntax'lar ile düzenlemeler yapma özellikleri (entegrasyon) sunmaktadır. vewbview içerdiğinden, birçok GUI elementi HTML elementi olacağından, javadaki diğer GUI kütüphanelerine göre daha cross-platform olduğu söylenebilir.

# hotspot

jvm spesifikasyonunu implemente eden birçok jvm mevcuttur. oracle'nin resmi jvm'inin ismi "hotspot"'tur. piyasada onlarca jvm implementasyonu mevcut. örnek: JRockit(java 7 döneminde geliştirilmesi durduruldu), IBM J9, OpenJDK...

oracle'ın jvm ismi olan hotspot, içerdiği hotspot teknolojisinden gelmektedir. sun jvm, oracle tarafından satın alınmadan önce JRockit olarak adlandırılıyor.

hotspot ilk bu isimle çıktığında, özel bir teknoloji barındırıyordu. bu teknoloji; sık kullanılan kod bloklarını, daha hızlı erişebileceği bir bellekte tutmakta ve o kod blokları için optimizasyonu arttırmaktadır. kodlar hakkında istatistikler tutmaktadır. bu istatistikler sonucunda;

- sık kullanılan kod blokları native makine koduna çevrili şekilde hazır tutulmaktadır

- gereksiz bazı kod blokları yürütülmemektedir

- bazı kod bloklarındaki sık girilen if blokları başa taşınmakta, az kullanılan if'ler alta taşınmaktadır

- ve daha birçok teknik kullanılmaktadır

"hotspot" kelimesi sık kullanılan bölgeleri (sıcak bölgeleri/noktaları) belirtmek için kullanılan genel bir terimdir. jvm'in ismi de buradan gelmektedir.

Java dili eskiden interpreter gerektiren bir dildi. Artık güncel sürümlerde hotspot teknolojisinin gelişmesi ile bazı kod blokları, native kod olarak saklandığı için, tekrar interpreter tarafından işletilmiyor. direk olarak makinada run ediliyor (native app gibi). dolayısı ile yeni jvm sürümleri yarı interpreter yarı native kod çalıştırır durumdadır.

java -version ile komut satırından bilgi alındığında "mixed mode" çıktısı; JIT'in de kullaıldığı anlamına gelmektedir. isteğe bağlı bu özellik devre dışı bırakılabilmektedir.

# native lib

java hotspot ile sık girilen kod bloklarını native makine koduna çevirip saklamaktadır. fakat önceden yazılmış default kütüphaneler (jvm içerisden default gelen sınıflar) önceden makine koduna derlenmiş saklanabilmektedirler. bunlara native lib denmektedir.

nativelib içerisindeki kütüphaneler işlemcilerin özelliklerinden de yararlanmaktadırlar. örneğin System.arraycopy() metodu array kopyalamayı işlemcinin özelliğinden yararlanarak yapar. bu tarz metodlardan faydalanmak uygulama hızını çok etkilemektedir.

# Corretto
amazon firmasının geliştirdiği, openjdk forkudur. oracle jdk ücretli olunca (11.inci sürüm) böyle bir çözüme gidildi.

# openJDK builds
openjdk stabil olsada, production-ready build'leri resmi olarak süreklilik garantisi verilerek dağıtılmamaktadır. dolayısı ile production-ready değildir. fakat production ortamında kullananlar vardır. bu sebeple; open-jdk kullanmak istemeyenler farklı jvm implementasyonları kullanırlar. zaten nerdeyse tüm jvm'ler openjdk'yı referans alır ve üzerine eklemeler/çıkarmalar yapılarak dağıtılırlar.

- openjdk, oracle tarafından geliştirildiği için openjdk'nın sitesinde https://openjdk.java.net/install/ indirme linkleri oracle-djk'yı indirir. çünkü openjdk türevi olan production-ready örneği olarak oracle kendini gösterir. dolayısı ile download linkleri buraya yönlenir: https://www.oracle.com/technetwork/java/javase/downloads/index.html

- OpenJDK build'leri ise buradan indirilebilir: https://jdk.java.net/archive/

- https://adoptopenjdk.net projesi openjdk'yı direk olarak saf haliyle derleyip sunmaktadır. projenin arkasında güçlü destekçiler vardır.

- Ubuntu "apt install openjdk-8-jre" komutu ile openjdk'yı kurar.

# Oracle jdk vs adoptOpenjkd

detaylı bilgiye buradan ulaşılabilir: (source-id: 445)

| Oracle JDK 8 proprietary component         | Alternative component     | OpenJDK 8         | OpenJDK 11        |
|--------------------------------------------|---------------------------|-------------------|-------------------|
| Java Web Start                             | IcedTea-Web               | yes               | no                |
| JavaFX                                     | OpenJFX                   | no                | no (coming soon)  |
| T2K font rendering engine                  | Freetype                  | yes               | yes               |
| Monotype Lucida fonts                      | Relicensed Lucida fonts   | no (coming soon)  | no (coming soon)  |
| Ductus 2D renderer                         | Pisces/Marlin             | yes (Pisces)      | yes (Marlin)      |
| Kodac Color Matching System (KCMS) library | LCMS                      | yes               | yes               |
| SNMP                                       | Use JMX (or SNMP4J)       | yes (not bundled) | yes (not bundled) |
| Sound drivers                              | Use Windows sound drivers | yes (not bundled) | yes (not bundled) |
| Java Flight Recorder (JFR)                 | Java Flight Recorder      | no (coming soon)  | yes               |
| Java Mission Control (JMC)                 | Use JDK Mission Control   | no (coming soon)  | no (coming soon)  |

Not: JavaFX, JFR, and JMC, java 8 ile Oracle tarafından openjdk projesine dahil edildi.

# Technology Compatibility Kit (or TCK)
JVM olabilmek için belirlenmiş standartlardır. Tüm JVM'ler TCK'da belirtilen kurallara uymak zorundadırlar.

# zulu
Azul firması tarafından geliştirilen openjdk türevidir.

# openj9
eclipse vakfının ürettiği openjdk türevi jvm implementasyonu.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# java 7 vs 8

- lambda expressions + function interface (konular başka başıkta anlatılıyor)

- stream

- javafx tümüyle jdk içinde entegre gelmektedir.

- Nashorn (konu başka başıkta anlatılıyor)

- "Optional" sınıfı geldi (konu başka başıkta anlatılıyor)

- Java Misson Control: Java yazilimlarinizi kontrol edebileceginiz bir tool. Mesela programiniz ne kadar CPU, hafiza ve threats kullaniyor.

- permgen politikası değiştirildi

- new Date-Time API. "java.time" isimli yeni kütüphahe paketi eklendi. eski sürümlerde hem java.util.Calendar hemde java.util.Date kullanılıyordu. hala jvm'lerde geriye uyumlu çalışabilmesi için kaldırılmadılar.

- default keyword: interface'de metod önüne "default" keyword'ü atılıp o metodun body'si yazılabiliyor. Eğer yazılırsa artık implementasyonlarda o metod override edilse bile interfacedeki metod çağrılıyor. Yani abstract sınıftakilerden  bir durum var.

  Burada Java zorunlu implementasyon yaptırmak istemiyordu. sadece interfacede metod implemente edilmesi isteniyordu. fakat zorunlu implementasyon geriye uyumluluğu sağlamak için eklendi. şu sebepten:  örnek üzerinden gidelim: List interface'sine bir metod eklenmek isteniyor. bu metodu JDK eklerse tüm güncel yazılımlar artık kullanılamaz hale gelecektir. çünkü tüm yazılımdaki list implementasyonları çalışmaz olacaktır. çünkü interfacedeki tüm metodları implemente etmek zorundalar. fakat artık implemente etme zorunlulukları olmadığı için bu metodlar sorunsuz çalışıyor olacaktır. 

- java.util.Base64 ile base64 işlemleri birçok implementasyon destekleyecek şekilde tasarlandı (başka yerde anlatılıyor)

# java 8 vs 9

- Java REPL (or JSHELL or Java Shell). 'Kulla' projesi altında geliştiriliyor.

- modülerlik. 'Jigsaw' isimli projesidir. artık her jar, kendi descriptor'unda hangi paketleri dışarıya açılacağını (dışarıdan göreülebilir olacağını) ve hangi modüllere depend ettiğini belirtebilmektedir.

- Process API geliştirmeleri. alt-process'leri yönetirken artık ok daha fazla API mevcuttur.

- Factory Methods for Collections. artık factory metodlar mevcut. örnek:

  > Set<Integer> ints = Set.of(1, 2, 3);

  > List<String> strings = List.of("1", "2");

- Reactive Streams (başka yerde anlatılıyor)

- Optional ve Stream API'lerindeki gelişmeler

- \@Deprecated (forRemoval=true , since="9") ile artık hangi versiyondan sonra bu metodun var olmayacağını dökümante edebiliyoruz.

- HTTP/2 ve websocket geldi. Eski sürümlerde üçüncü parti kütüphanelerle kullanılıyordu. javaee ve spring kendi içinde üçüncü parti kütüphaneleri gömülü getiriyor ve onları kullanıyordu. bu sebeple eski sürüm java kullanılsa bile, javaee veya srping kullanarak websocket ve http2 kullanılabiliyordu. 

  Aslında bu modül incubator olarak java 9 ile geldi. kaynak: (source-id: 354) "2. Initial Setup" başlığı.
  
  incubator'dan çıkışı 11'inci sürüm oldu. kaynak: (source-id: 355) ilk cümle.

# java 9 vs 10

- var list = new ArrayList<String>(); type safe olmayan nesneler tutulabiliyor

# modülerlik

- Java 9 ile artık "java.se" modülü jre içindeki kütüphaneleri barındırıyor.
- Java 9 ile java.se artık jaxb gibi JavaEE'ye ait olduğu düşünülen kütüphaneleri deprecated olarak işaretlendi.
- Java 9 ile jaxb gibi JavaEE'ye ait olduğu düşünülen kütüphaneler default classpath'te gelmiyorlar fakat JDK içerisinde yüklü geliyorlar. Yani development yaparken ilgili jar'ları hala bulabiliyoruz fakat projemizde ufak config yapmak gerekiyor.
- JDK 11 ile jaxb gibi javaee'nin olduğu düşünülen paketler jdk içinden tamamen kaldırıldı.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# tomcat variants

tomcat: servlets + jsp

tomee: tomcat + jsf + JPA + CDI

tomee-jax-rs: tomee + jax-rs

tomee+: tomee-jax-rs + jax-ws

detailed comparison:

|                                                      | Tomcat | TomEE | TomEE JAX-RS (~ Microprofile) | TomEE+ | TomEE PluME | OpenEJB |
|------------------------------------------------------|--------|-------|-------------------------------|--------|-------------|---------|
| Java Servlets                                        | +      | +     | +                             | +      | +           |         |
| Java ServerPages (JSP)                               | +      | +     | +                             | +      | +           |         |
| Java ServerFaces (JSF)                               |        | +     | +                             | +      | +           |         |
| Java Transaction API (JTA)                           |        | +     | +                             | +      | +           | +       |
| Java Persistence API (JPA)                           |        | +     | +                             | +      | +           | +       |
| Java Contexts and Dependency Injection (CDI)         |        | +     | +                             | +      | +           | +       |
| Java Authentication and Authorization Service (JAAS) |        | +     | +                             | +      | +           | +       |
| Java Authorization Contract for Containers (JACC)    |        | +     | +                             | +      | +           | +       |
| JavaMail API                                         |        | +     | +                             | +      | +           | +       |
| Bean Validation                                      |        | +     | +                             | +      | +           | +       |
| Enterprise JavaBeans                                 |        | +     | +                             | +      | +           | +       |
| Java API for RESTful Web Services (JAX-RS)           |        |       | +                             | +      | +           | +       |
| Java API for XML Web Services (JAX-WS)               |        |       |                               | +      | +           | +       |
| Java EE Connector Architecture                       |        |       |                               | +      | +           | +       |
| Java Messaging Service (JMS)                         |        |       |                               | +      | +           | +       |
| EclipseLink                                          |        |       |                               |        | +           |         |
| Mojarra                                              |        |       |                               |        | +           |         |

full comparison: (source-id: 421)

# tomcat version history

| version | jsp | websocket spec | servlet spec | java version                         | release date | Latest release | Latest version release date |
|---------|-----|----------------|--------------|--------------------------------------|--------------|----------------|-----------------------------|
| 2.0     |     |                |              |                                      | 1998         |                |                             |
| 3.0     |     |                |              |                                      | 1999         | 3.3.2          | 2004-03-09                  |
| 4.1     | 1.2 |                | 2.3          | 1.3 and later                        | 2002-09-06   | 4.1.40         | 2009-06-25                  |
| 5.0     | 2.0 |                | 2.4          |                                      | 2003-12-03   | 5.0.30         | 2004-08-30                  |
| 5.5     |     |                | 2.4          | 1.4 and later                        | 2004-11-10   | 5.5.36         | 2012-10-10                  |
| 6.0     | 2.1 |                | 2.5          | 5 and later                          | 2007-02-28   | 6.0.53         | 2017-04-07                  |
| 7.0     | 2.2 | 1.1            | 3.0          | 6 and later (web socket icin min 7 ) | 2011-01-14   | 7.0.96         | 2019-07-29                  |
| 8.0     | 2.3 | 1.1            | 3.1          | 7 and later                          | 2014-06-25   | 8.0.53         | 2018-07-05                  |
| 8.5     |     | 1.1            | 3.1          | 7 and later                          | 2016-06-13   | 8.5.43         | 2019-07-09                  |
| 9.0     |     | 1.1            | 4.0          | 8 and later                          | 2018-01-18   | 9.0.22         | 2019-07-09                  |

# servlet version history

| Servlet API version | Released       | Specification    | Platform                                                  | Important Changes                                                           |
|---------------------|----------------|------------------|-----------------------------------------------------------|-----------------------------------------------------------------------------|
| Servlet 4.0         | Sep 2017       | JSR 369          | Java EE 8                                                 | HTTP/2                                                                      |
| Servlet 3.1         | May 2013       | JSR 340          | Java EE 7                                                 | Non-blocking I/O, HTTP protocol upgrade mechanism                           |
| Servlet 3.0         | December 2009  | JSR 315          | Java EE 6, Java SE 6                                      | Pluggability, Ease of development, Async Servlet, Security, File Uploading  |
| Servlet 2.5         | September 2005 | JSR 154          | Java EE 5, Java SE 5                                      | Requires Java SE 5, supports annotation                                     |
| Servlet 2.4         | November 2003  | JSR 154          | J2EE 1.4, J2SE 1.3                                        | web.xml uses XML Schema                                                     |
| Servlet 2.3         | August 2001    | JSR 53           | J2EE 1.3, J2SE 1.2                                        | Addition of Filter                                                          |
| Servlet 2.2         | August 1999    | JSR 902, JSR 903 | J2EE 1.2, J2SE 1.2                                        | Becomes part of J2EE, introduced independent web applications in .war files |
| Servlet 2.1         | November 1998  | 2.1a             |                                                           | First official specification, added RequestDispatcher, ServletContext       |
| Servlet 2.0         | December 1997  | N/A              | JDK 1.1                                                   | Part of April 1998 Java Servlet Development Kit 2.0                         |
| Servlet 1.0         | December 1996  | N/A              | Part of June 1997 Java Servlet Development Kit (JSDK) 1.0 |                                                                             |

# servlet 3.1 non-blocking IO

```java
public void doGet(request, response) {
    final AsyncContext asyncContext = request.startAsync();

    asyncContext.start(new Runnable() {                        
        @ Override
        public void run() {
            // do some work here which is on a new thread. that makes free the blocking http thread.

            // burada aslında aşağıdaki gibi bir şey yapmazsak neredeyse hiçbir anlamı kalmaz
            asyncHttpCLient.sendPostRequest().
                                    than(response -> {
                                                       log(response);
                                                       response.getOuputStream().print(response);
                                                       asyncContext.complete();
                                    })
        }
    });
}
```

# Catalina
tomcat'in servlet container'ın ismidir.

# Jasper
tomcat'in jsp derleme motorudur. JSP derlenir ve bir servlet'e dönüştürülür.

# $CATALINA_HOME
Tomcat runtime dosyalarının bulunduğu dizindir.

# $CATALINA_BASE
birden fazla tomcat instance'ı aynı anda çalıştırılabilir. her instance'ın bulunduğu config'ler CATALINA_BASE içinde olmalıdır.

eğer CATALINA_BASE set edilmemişse; CATALINA_HOME değeri ona set edilecektir.

# eclipse tomcat config files
eclipse tomcat'i başlatırken config dosyaları için workspace içinde otomatik olarak "/eclipse-worksce/Servers/Tomcat v6.0 Server at localhost-config" isminde bir dizin oluşturuyor. bu dizindeki config'ler tomcat dizini içindeki config'leri override ediyor.

tomcat start edilirken ona zaten tüm config parametreleri (config dosyalarının path'leri, örnek server.xml) komut satırından geçilebiliyor. eclipse'te bu config dosyalarını, tomcat binary'sine otomatik olarak parametre geçiyor. yani gerçek tomcat dizinini override etmemiş oluyor. böylece tek bir tomcat dizini birden fazla eclipse workspace'i tarafından kullanılabiliyor.

# root dizinler

- bin: executable files and "start tomcat", "run as service" like scripts

- lib: jar available for all webapps

- logs

- work: sadece jsp dosyaları, servet'e çevrildiklerinde, burada o servlet'ler saklanır.

- conf: server.xml gibi config dosyalarının bulunduğu dizin

  - catalina.policy:  
    
    yetkilendirme tanımları bu dosyadadır. örnek:

    permission java.util.PropertyPermission "java.version", "read";

  - catalina.properties

    paket(java class paketleri) bazında ve jar bazında hangi projenin hangislerini okuyabileceğinin bilgisinin yer aldığı dosya.

  - server.xml

    sunucunun tüm ayarları buradan yapılabiliyor. detaylı anlatım aşağıda mevcut. bu dosyadan her war dosyasının içinde olamaz.

  - web.xml

    bu dosya her war içindeki web.xml parse edilmeden önce işletilir. daha sonra war içindeki web.xml okunur.

- webapps

  - docs: dökümantasyon içeren bir proje

  - examples: örnek jsp sayfaları ve kaynak kodlarını gösteren bir site

  - ROOT: contextpath'i olmayan bir proje. burada sadece tomcat'e hoşgeldiniz ve diğer apache.org projelerine linkler verilmiş bir site bulunmaktadır.

  - manager: tomcat üzerinde JVM memory detayları, yüklü olan projeleri context-path'leri gibi bir çok detay monitör edilebilir ve deploy/undeploy işlemleri yapılabilmesini sağlar.

  - host-manager: "Virtual Host" özelliğini monitör etmek için kullanılmaktadır. Virtual host birden fazla webapp klasörü yaratılabilmesini her her webapp içindeki projelerin birer domain-name'e karşılık gelmesini sağlamaktadır. Örneğin; google.com ve haberturk.com'a yapılan istekler aynı tomcat instance'ımıza gelecek ve fakat farklı webapp dizinlerindeki projelere yönlendirilebilir.

# Realm
realm türkçe kelime anlamı: diyar, krallık, alan, alem

A Realm is a "database" of usernames and passwords that identify valid users of a web application. this database includes also roles of users.

Tomcat içinde belirlediğimiz uygulamalar, güvenlik katmanlarında isterlerse bu kullanıcıları kullanabilirler. Böylece tüm uyguamalar için ortak kaynak belirlemiş oluruz.

Tomcat içinde gelen "manager" uygulaması, varsayılan olarak Realm'daki user'lara göre kullanıcıların login olup arayüzde işlem yapmasına izin vermektedir.

Realm kaynağı kulanmak için org.apache.catalina.Realm'dan türemiş bir implementasyona ihtiyacımız var. Tomcat içerisinde bunlar yüklü gelmektedir:

- JDBCRealm
  
JDBC jar'ı aracılığı ile veritabaına bağlanır. tabloları bizim oluşturmuş olmamız gereklidir.

/tomcat/conf/server.xml'de buna benzer bir tanımlamayı eklememiz gereklidir:

```xml
<Realm
    className="org.apache.catalina.realm.JDBCRealm"
    driverName="org.gjt.mm.mysql.Driver"
    connectionURL="jdbc:mysql://localhost/authority?user=dbuser&amp;password=dbpass"
    userTable="users" userNameCol="user_name" userCredCol="user_pass"
    userRoleTable="user_roles" roleNameCol="role_name"/>
```

veritabanında yapılan satır dğeişiklikleri tomcat'e anında yansımaktadır. fakat bir kullancının rolü değişirse, yada kullanıcı kaldırılırsa, kullanıcı logout olana kadar session'ı kullanabilecektir.

eğer servlet'lerde biri protected bir kaynağa erişmek isterse tomcat otomatik olarak org.apache.catalina.realm.JDBCRealm.authenticate() metodunu çağracaktır.

- DataSourceRealm

JNDI tanımı aracılığı ile veritabanına bağlanmaktadır.

```xml
<Realm
   className="org.apache.catalina.realm.DataSourceRealm"
   dataSourceName="jdbc/authority"
   userTable="users" userNameCol="user_name" userCredCol="user_pass"
   userRoleTable="user_roles" roleNameCol="role_name"/>
```

- JNDIRealm

JNDI tanımı aracılığı ile LDPA sunucusundan kullanıcı bilgilerini çeker.

- UserDatabaseRealm

JNDI racılığı ile XML'den kullanıcı bilgilerinini okunduğu realm'dır. varsayılan olarak XML dosyası /tomcat/conf/tomcat-users.xml'dir. örnek tomcat-users.xml:

```xml
<tomcat-users>
  <user name="tomcat" password="tomcat" roles="tomcat" />
  <user name="role1"  password="tomcat" roles="role1"  />
  <user name="both"   password="tomcat" roles="tomcat,role1" />
</tomcat-users>
```

- MemoryRealm

demo için geliştirilmiş bir implementasyondur. UserDatabaseRealm ile aynıdır (aynı xml'i okur), tek eksisi xml'de yapılan değişiklikler restart edilene kadar algılanmaz.

- JAASRealm

istek yapan kullanıcıları "Java Authentication & Authorization Service (or JAAS)" ile onaylayan Realm'dır.

- CombinedRealm

birden fazla sub-real kullanabilmemize imkan tanıyan Realm'dır.

```xml
<Realm className="org.apache.catalina.realm.CombinedRealm" >
   
   <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
          resourceName="UserDatabase"/>
   
   <Realm className="org.apache.catalina.realm.DataSourceRealm"
          dataSourceName="jdbc/authority"
          userTable="users" userNameCol="user_name" userCredCol="user_pass"
          userRoleTable="user_roles" roleNameCol="role_name"/>
</Realm>
```

- LockOutRealm

CombinedRealm'dan türemiştir. kullanıcıları, fazla şifre denemesi isteği yaptıkları durumda onları engelleyebilmektedir.

# context path

comtext tomcat'te bir war dosyasına denk geliyor (server.xml'den de anlaşılacağı gibi).

comntext path; URL'de host ve port'tan sonra gelen web projesinin ilk seviye url'sidir.

Webapp altındaki her proje URL'den http://host/directoryName olarak çağrılırlar. tek istisna ROOT folder'ıdır. o direk http://host/ ile çağrılır. root içerisindeki bir web projesi, örnek /tomcat/webapps/ROOT/webapp1, http://host/webapp1 olarak çağrılır.

TOMCAT/WEBAPPS/demo#v1#myfeature/ projesi url'den bu şekilde erişilir: http://host/demo/v1/myfeature context.

\## (çift diez) örnek: foo##2.war sürüm olarak algılanmaktadır. sürüm numaraları url'ye (context path'e) yansıtılmaz.

/tomcat/conf/server.xml dosyası sadece tomcat restart edildiğinde işlenir, bu sebeple context'lerin server.xml'e yazılmaması önerilir.

# context.xml

bu dosya server.xml içindeki host elementinin içine yazılan kısmı taşıyabilir. bir sistemde birden fazla context belirteci olabilir. aynı sistemde birden fazla belirtec yazılmış olabilir. bunlar birbiri ile çakıştıklarında öncelik sırası parantez içerisinde verilmiştir (önceliği yüksek olan 1 numara):

- (1) /tomcat/conf/context.xml

- (1) tomcat/conf/server.xml içindeki context elementi

- (2) /tomcat/conf/[Engine_name]/[Host_name]/war-name.xml

- (2) /tomcat/conf/context.xml

- (3) war içindeki /META-INF/context.xml 

Tek istisna: tomcat/conf/server.xml içindeki context elementinde "override=true" yok ise; sistemin herhangi bir yerine yazdığımız context değeri algılanır.

# META-INF
Bu dizin war dosyalarının içindedir. war export edilirken, bu dizinin içindekiler tomcat/webapps/app1/ içerisine taşınır.

# server.xml

```xml
<Server>

  <Service name="MyService1">

    <Connector port="8443"/>

    <Connector port="8444"/>

    <Engine>

      <!-- default appBase: webapps -->
      <Host name="yourhostname" appBase="/webapps2"> 

        <!-- file1 path is: TOMCAT/webapps2/file1.war -->
        <Context path="/webapp1" docBase="file1.war" />

        <Context path="/webapp2"/>

      </Host>

    </Engine>

  </Service>

</Server>
```

- Görüldüğü üzere her bilgi __server__ içerisine yazılıyor. 

- örnekte 1 adet service içerisinde birden fazla connector (bunlar sadece port'u dinleyip yönlendirme yapmaya yarıyor), webapp1 vs webapp2'ye yönlendirme yapıyor.

- 2 ayrı port tek bir engin'e yönlenmiş durumda. webapp1 ve webapp1 bir adet __engine__'e bağlanmış durumdalar.

- __engine__ burada __Catalina__'ya denk geliyor. cataline ise bir __servlet container__'dır.

- Service, engine gibi gruplamalar log'lardan da takip edilebildiği için büyük kolaylık sağlamaktadır.

- 80'e gelen istekleri eğer client ssl bağlantısı kurma isteği yapıyorsa 443'e yönlendirebiliriz:

```xml
<Connector port="80" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="443" />
```

Bu connector tanımı yetmeyecektir. Çünkü son durumda 443'ün tanımı yoktur. 443'ün tanımını da yapmalıyız:

```xml
<Connector port="443"
           protocol="org.apache.coyote.http11.Http11Protocol"
           SSLEnabled="true" 
           scheme="https" 
           secure="true" 
           sslProtocol="TLS" 
           keystoreFile="/path/to/kestorefile" 
           keystorePass="my_keystore_password"/>
```

Bazı Connector parametreleri:

- address

  br sunucu birden fazla ip alıyor olabilir. bunlardan hangisinin o connector tarafından listening'de olacağını belirtir. default olarak tüm ip'ler dinlenir.

- maxPostSize

  post requestinin max boyutu. varsayılan 2 mb.

- scheme

  protokolün ismidir. url'deki değer değildir. default http.

- secure

  java kodumuzda request.isSecure() true/false dönüşü yapsın istiyorsak bu değeri true olarak set etmeliyiz.

- URIEncoding

  URL'nin encoding'idir. default ISO-8859-1.

- useBodyEncodingForURI

  eğer request'in header'ında "contentType" varsa, URIEncoding değerini hiçe sayar ve contentType'a göre url'yi parse eder. default değeri false.

Yukarıda protocol ile class ismi (implementasyon) belirtmezsek tomcat otomatik olarak bir implementasyon seçecektir. SSL standartır. bu sebeple bu implementasyonlar ssl protokolünün işleyişinde bir dğeişiklik yapmıyorlar, bunlar sadece configürasyonları farkettiriyor.

- JNDI

Direk \<server> içerisine bu tanımlama yapılabilir. bu şekilde tüm uygulamalar ismi ile JDNI'a erişebilir olur.

```xml
<GlobalNamingResources>
  <Resource name="UserDatabase" auth="Container"
            type="org.apache.catalina.UserDatabase"
            description="the user informations"
            factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
            pathname="conf/tomcat-users.xml" />
</GlobalNamingResources>
```

Bu JNDI'ı kullanacak war dosyaları kendi web.xml'lerinde bunu belirtmek zorundalar:

```xml
<resource-ref>
    <description>
          database of tomcat
    </description>
	  <res-ref-name>
          UserDatabase
    </res-ref-name>
	  <res-type>
          org.apache.catalina.UserDatabase
    </res-type>
	  <res-auth>
          SERVLET
    </res-auth>
</resource-ref>
```

Yukarıdaki res-aut "CONTAINER" da olabilirdi.

- Environment variables

Direk \<server> içerisine bu tanımlama yapılabilir. bu şekilde tüm uygulamalar için environment variable atamış oluruz.

```xml
<Environment name="simpleValue" type="java.lang.Integer" value="30"/>
```

- catalina alternatives

catalina dışında bir container kullanmak istersek:

```xml
<Service name="MyService1" className="com.my.class.Name" >
```

Eğer className verilmezse default olarak org.apache.catalina.Service interface'si kullanılır.

- Listeners

Birçok event listener mevcut. Bunlar default olarak catalina'ya assign edilmiş durumdadır.

```xml
<Listener className="org.apache.catalina.startup.VersionLoggerListener" />
```

# shutdown

aşağıdaki satır jvm'in 8005'ten port dinlemesi ve SHUTDOWN string'i o porta yollandığı takdirde kendini kapatmasını belirtmektedir.

```xml
<Server port="8005" shutdown="SHUTDOWN">
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# jsp (or JavaServer Pages)

jsp'de sayfalar, sunucu tarafta derlenip clienta gönderilir. her jsp sayfası, bir servlete çevrilir. servlet java sınıfıdır.

jsp dosyaları, java servlet sınıfına çevirirlirken:

jsp dosyası:

```xml
<html>
  <%
    double num = Math.random();
    if (num > 0.95) {
  %>
      <h2>You'll have a luck day!</h2><p>(<%= num %>)</p>
```

Java servlet sınıfı:

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
public class MyServlet extends HttpServlet {

  // Runs when the servlet is loaded onto the server.
  public void init() {
     // servlet init codes here...
  }

  // Runs on a thread whenever there is HTTP GET request

  // Take 2 arguments, corresponding to HTTP request and response

  public void doGet(HttpServletRequest request, HttpServletResponse response)

        throws IOException, ServletException {

     // Set the MIME type for the response message

     response.setContentType("text/html");

     // Write to network

     PrintWriter out = response.getWriter();

     // Your servlet's logic here

     out.write("<html>\r\n  ");

     double num = Math.random();

     if (num > 0.95) {

        out.write("<h2>You will have a luck day!");

        ....

  }
```

# JSP ile single page application
Bu konu başlığı da okunması faydalı olacaktır: [web.md "submit request vs Ajax"](https://github.com/yusufd89/notes/blob/master/web.md)

JSP ile single page application yapısına uygun değildir. fakat eğer yapılmak isteniyor ise bir çok farklı yöntem uygulanabilir.

normalde jsp tüm sayfayı döner ve html'e o output yazılır. fakat biz eğer servlete isteği, js'te olduşturduğumuz manuel bir ajax işlemi ile yapar ve dönüş değerini manuel sayfanın bir kısmını güncelleyecek şekilde ayarlarsak o zaman single page applicaiton yapmış oluruz. aynı şey spring-mvc içinde geçerlidir.

# JSP debug
eclipce debug perspektifindeyken, variables view'ı jsp doayasında debug poıint koymamıza izin veriyor. runtime'da hangi değerlerin olduğunu da gösteriyor. bunun için eclipce'te WTP (or web tools platform) plugin'i yüklü olmalıdır.

# JavaServer Pages Standard Tag Library (or JSTL)
JSTL JavaEE'nin bir modülüdür.

jst jsp için core seviyede jsp tag'leri içerir. Gruplanmışlardır.

sadece ihtiyacımız olan grubu jsp dosyamıza import ederiz:

```jsp
<%@ taglib prefix = "c" uri = "http://java.sun.com/jsp/jstl/core" %>
```

- ## Core Tags
     ```jsp
     <c:set>
     <c:forEach>
     <c:when>
     ```

- ## Formatting tags
     ```jsp  
     <fmt:formatNumber>
     <fmt:parseDate>
     ```

- ## SQL tags
     SQL sorgusu çalıştırmayı ve bunu bir değere atayabilmemizi sağlar.
     ```jsp
     <sql:query>
     <sql:transaction >
     ```

- ## XML tags
     XML parse işlemleri yapmamızı sağlayan metodlar içerir.

- ## JSTL Functions
     Hazır temel fonksiyonlar içerir. Çoğu string işlemleridir.

# jsf (or Java Server Faces)

jsf; jsp üzerine kurulu bir yapıdır. JSF'te, JSP gibi derleme ve servlet'in cevabı dönme işlemine ek olarak; altyapısı lifecycle'lar üzerinden hareket etmesini sağlamaktadır.

jsp'de her jsp dosyası bir class'a denk gelirken, jsf'te her jsf dosyası tek bir servlet üzerinden (faces servlet) dağıtılır.

jsf; MVC mimarisinde şu şekilde ayrılır:

- M: modellerimiz (veritabanı modleleri gibi)

- V: xhtml dosyalarımız

- C: FacesServlet ---> çünkü view'lardaki değerleri güncelleyecek olan kodlar, aynı zamanda modelleri güncelleyecek olan kodlar buradadır.

# primefaces vs icefaces vs richfaces vs myfaces

primefaces ve icefaces ve richfaces; jsf üzerine kuruludur. jsf tag'lerine ek kendi taglerini sunar.

myfaces; bir jsf implementasyonudur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# front controller
genel bir server uygulama patternidir. bir server'a gelen istekleri yakalayan ilk sınıftır/servlettir. Bu servlet'in görevi ilgili yere bu isteği taşımaktadır.

# DispatcherServlet
Dispatch türkçe kelime anlamı: sevk etmek. yazılım dünyasında metoda/fonksiyona mesaj(parametre) yollama(sevk etme) anlamında kullanılır.

SpringMVC'de front controller'ın ismidir.

# FacesServlet
JSF için frontcontoller'ın ismidir.

# servlet
groupId: javax.servlet, artifactId: javax.servlet-api paketi servlet interface'lerini içeriyor. bu paket jdk içinde de geliyor. runtime sırasında javaee app server'ında bunu implemente eden sınıflar zaten çalışıyor. kod direk implementasyonları çağrıyor.

javax.servlet.Servlet interface'sinin birçok implementasyonu var: FacesServlet, GenericServlet, HttpServlet.

javax.servlet.Servlet şu metodları barındırıyor:
- destroy() servlet artık hiç kullanılmayacağı zaman çağrılıyor
-	init(ServletConfig config) uygulamamızın hayatı boyunca 1 kere çağrılıyor
- service(ServletRequest req, ServletResponse res) her request'te çağrılıyor
- getServletConfig() servlet ayarlarında verdiğimiz config'leri çekebilmemizi sağlıyor

1 servlet instance'ını birden fazla thread aynı anda kullanıyor olabilir. eğer hiçbir thread o instance'ı kullanmazsa o zaman servlet container bu servlet'i destroy edebilir. bu şekilde resource'ları boşaltmış olur. fakat hemen ardından gerekiyorsa yeni instance oluşturur. bu kararlar servlet container'a kalmıştır.

javax.servlet.http.HttpServlet ise javax.servlet.Servlet'ten extend eder ve bu metodları da içerir:
- doGet(HttpServletRequest req, HttpServletResponse resp)
- doHead(HttpServletRequest req, HttpServletResponse resp)
- doPost(HttpServletRequest req, HttpServletResponse resp)
- ...

# Context path
servlete erişmek için kullanılan URL'dir (domain hariç kısmı).

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Look And Feel
sadece tema diil, aynı zamanda efektler ve objeler davranış biçimlerini de kapsayan bir "UI" terimidir. Sadece "tema" terimi kullanıldığında son kullanıcının UI'a karşı tüm hissiyatini kapsamamaktadır. Bu sebeple "Look And Feel" terimi daha geniş bir terimdir.

# AWT (or Abstract Windows Toolkit) vs SWING
AWT, OS'un native GUI objelerini kullanır. Fakat hepsini ortak bir Interface üzerinden yönettiği için, sadece ortak özellikler kullanılabilmektedir. AWT her platformda farklı göründüğünden, "Look And Feel" aynı olmamaktadır.

SWING ise, pixel pixel ekrana kendi GUI objelerini basmaktadır ve tüm platfrmlarda aynı görünüme ve davranışlara sahiptir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# http clients for java
Client'lar sundukları feature'lara göre değerlendirilir. genel olarak 3'ye gruplayabiliriz (abstraction level):
- Response ve request'leri mapping yapanlar (high level)
- Response ve request'leri mapping yapmayanlar (low level).
- bazı client'lar ise (aşağıdaki listede "very high" olarak belirtildi) diğer tüm decoder/encoder'ları, http client'ları wrap etmemizi sağlıyor. örneğin feign-client bu kategöride ve bu şekilde setup'ı yapılabilir:

```java
BookClient bookClient = Feign.builder()
  .client(new OkHttpClient())
  .encoder(new GsonEncoder())
  .decoder(new GsonDecoder())
  .logger(new Slf4jLogger(BookClient.class))
  .logLevel(Logger.Level.FULL)
  .target(BookClient.class, "http://localhost:8081/api/books");
```

Yukarıdaki builder'a geçebileceğimiz parametreler iyi bir görsel ile burada gösterimiştir: (source-id: 356). Görseldeki bazı kısımlar buraya kopyalandı:

- clients
  - java.net.URL
  - apache http
  - apache HC5
  - google HTTP
  - JAVA 11 HTTP2
  - OKhttp
  - ribbon
- async clients
  - java.net.URL
  - apache HC5
- contracts
  - feign
  - jax-rs
  - jax-rs 2
  - spring 4
  - soap
  - spring boot (3rd party)
- encoders/decoders
  - gson
  - jackson 1
  - jackson 2
  - jackson jaxb
  - sax
- metrics
  - dropwizard metrics 5
  - micrometer
- extras
  - hystrix
  - slf4j
  - mock

| name                             | abstraction level | comment                                                                                                                                                                                                                                                                                                                                                                                                             |
|----------------------------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| apache commons httpclient        | low               | Proje sonlandı. kaynak: (source-id: 357)                                                                                                                                                                                                                                                                                                                             |
| Apache HttpComponents httpclient | low               | "apache common httpclient" has been replaced by the Apache HttpComponents project in its HttpClient and HttpCore modules                                                                                                                                                                                                                                                                                            |
| java.net.http.HttpClient         | low               | java 10+ ile geldi. dependency istenmeyen projelerde terchi edilebilir. java da her zaman java.net.HttpURLConnection API'si vardı. Fakat bu API yeni http sürümlerini desteklemiyor ve API'leri yeni metodolojileri desteklemiyordu ve async çalışmıyordu.                                                                                                                                                          |
| google-http-java-client          | high              | google'ın kendi android için kütüphanelerinde kulanmak amaçlı geliştiridği library                                                                                                                                                                                                                                                                                                                                  |
| async-http-client                | ?                 | Proje sonlandı. kaynak: (source-id: 358)                                                                                                                                                                                                                                                                                                             |
| RestTemplate                     | high              | java.net.HttpURLConnection (java 11 öncesinde varolan API) tabanlı. Yakın zamanda deprecated olacak. çünkü sadece sync işlemleri destekliyor. spring, yeni olarak org.springframework.web.reactive.client.WebClient'ı çıkardı. webclient hem sync hem async destekliyor. kaynak: (source-id: 359) |
| FeignClient                      | very high         | Declarative olarak client tanımlamamızı sağlıyor (Interface-based implementation). kendi içinde java.net.HttpURLConnection (java 11 öncesinde varolan API) ve reflection'lardan yararlanıyor. kaynak: (source-id: 360)                                                                                                          |
| Retrofit                         | very high         | feign client gibi Declerative client oluşturabilmemizi sağlıyor. feign-client ile karşılaştırıldığında retrofit daha az kütüphaneyi/özelliği wrap edebiliyor.                                                                                                                                                                                                                                                       |
| okhttp                           | ?                 | ?                                                                                                                                                                                                                                                                                                                                                                                                                   |
| unirest                          | ?                 | ?                                                                                                                                                                                                                                                                                                                                                                                                                   |

# jax-ws

javaEE de SOAP web servisi spesifikasyonudur.

# jax-rs

javaEE'nin rest spesifikasyonudur. Sadece API'dir. interface'leri aşağıdaki dependency ile projemize ekleyebiliriz:

```xml
<dependency>
    <groupId>javax</groupId>
    <artifactId>javaee-api</artifactId>
    <version>7.0</version>
    <scope>provided</scope>
</dependency>
```

Runtime sırasında ise javaEE implementasyonumuz (server'ımız örnek: tomee) bunu implemene eden paketi sunacaktır.

# jax-ws vs jax-rs implementasyonları

javaEE'de default implementasyon kavramı yoktur. hangi suncuya atarsak jboss, tomcat kendi implementasonunu sunar. üzerinde çalıştırdığımız sunucununkinden farklı implementasyon istersek, biz spesifik jar'ları yükleyip configürasyon yapmak gerekecektir.

| name       | jax-ws | jax-rs | Installed Default                                  |
|------------|--------|--------|----------------------------------------------------|
| Apache CXF | yes    | yes    | TomEE, WebSphere                                   |
| axis       | yes    | no     |                                                    |
| axis2      | yes    | yes    |                                                    |
| Jersey     | no     | yes    | GlassFish Server, Payara Server                    |
| RESTEasy   | no     | yes    | JBoss EAP (Enterprise Application Server), WildFly |
| Restlet    | yes    | ?      |                                                    |

Spring framework, Spring MVC modelinde bu hizmeti sunmaktadır. JAX-RS implementasyonu değildir. Spring'in aynı modülü model-view-controller özelliğini de sunmaktadır.

Yukarıdaki bazı implementasyonlar (bunlardan biri RESTEasy) hem server hem de client tarafını da sunmaktadır.

Spring ile spring-mvc kullanılmak zorunda diiliz. alternatifleri de spring ile kullanabiliriz. örnek: spring-boot-starter-jersey. kaynak: (source-id: 448) "7.3. JAX-RS and Jersey" başlığı.

# wsimport
JDK içinde yüklü gelen komut satırı uygulaması. WSDL'den, SOAP web service client Java kodu generate etmemize yarıyor.

# eclipse GUI client generator
elipse IDE'de herhangi bir projeye sağ tıklayıp, New --> Web Service Client --> diyip wsdl'iveriyoruz bize java kodu üretiyor. burada eclipse IDE arkaplanda axis'in generator'ını kullanıyor.

# axis vs axis2
axis'te büyük değişiklikler yapıldı ve yeni proje olarak fork edildi. artık rest'te destekliyor. "axis2" projenin yeni adıdır. axis2'nin yanına sürüm numarasını gelecektir.

# RPC (or Remote procedure call)

Uzak makinede yada aynı makinede farklı processler arasında metod çağırıp işletme mekanizmasıdır. bu bir consept'tir. protokol dğeildir. herkes uzaktaki bir metodu çağrıp dönüş alabilir. genelde programlama dilleri kendi protokollerini/standartlarını kullanıyor. bu sebeple cros-language değilledir.

# Remote Method Invocation (or RMI)

Java'nın kullandığı RPC'dir.

# XML-RPC

bir çeşit rpc standardıdır.

# wsdl içinde geçen terimler

wsdl 2.0 sürümü http isteklerini kısmen desteklemektedir.

aşağıdaki her tanımın "name" isminde property'si mutlaka olmalıdır.

tüm wsdl xml'inin root elementi < definition > etiketindedir.

| 1.1       | 2.0       | aciklama                                                                                                                                       |
|-----------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------|
| port      | Endpoint  | gidilecek olan isteğin URL'sidir (path ile bilikte)                                                                                            |
| service   | service   | her endpointi birer binding'le eşleştiren mappingdir. örnek: X servisi A binding'i ile eşleşir.                                                |
| binding   | binding   | operation'lar kümesidir. + istek hakkında meta bilgiler içerir                                                                                 |
| portType  | Interface | operation'lar kümesidir. + her operation içinde gidip gelecek olan dto'ları da tanımlamaktadır. + error durumunda dönecek dto tanımı burdadır. |
| operation | operation | her metod bir operation'dur.                                                                                                                   |
| message   | (yok)     | bir request yada response'un tüm dto'dur. her message bir type kümesidir. message etiketi içinde her type "part" isimli etiket ile tanımlanır. |
| types     | types     | her dto bir type'tır. type tüm request yada response olmak zorunda diildir. bir kısmı da olabilir.                                             |

# Subset WSDL (or SWSDL)

sadece bir metod kümesini kapsar. swsdl alınıp client üretilirse, swdl içindeki metodlar çağrılabilir.

# marshalling

marshalling işlemi bir nesnenin farklı bir makineye parametre olarak geçilebilmesi için byte dizisi olarak (dosyaya yazılabilir halde oluyor doğal olarak) taşınması işlemidir. Kelime ve temel bilgisayar biliminde aslında "serialize" ile aynı şeye denk gelmektedir. fakat java dünyasında bu iki işlem birbirinden farklıdır.

# java dünyasında marshalling

java dünyasında marshalling işlemi sonucu üretilen çıktıda java sınıfının içindeki codebase + set edilmiş değeler tutulmaktadır. oysa serialize işleminde sadece sınıfın set edilmiş değerleri tutulmaktadır. marshalling işlemi java standratlarında belirtilmiştir. Sadece RMI işleri için kullanılır. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# codebase

- RMI uzaktan java metodu çağırır. dönüşünde ise bir sınıf alır. dönüşte alacağı sınıfı client bilmeyebilir. client sadece o sınıfın interfacesini bilir. fakat dönecek implementasyonu bilemez. böyle durumlarda RMI çağırdığı metoddan dönen codebase bilgisine bakar. codebase sınıfın id'sini barındırır. eğer aynı id'de bir sınıf localde varsa; client localdeki sınıfı kullanır. fakat eğer locaklde yoksa; uzakdan o sınıfı download eder.

- codebase kelimesi yazılım dünyasında soruce-code'un tümüne verilen isimdir. genelde generated-file'ları barındırmaz. sadece insanların yazdığı kodların tümüne denir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# java stack yapısı
stack; sadece thread'e bağlı değerleri tutan veri yapısıdır. her thread için ayrı stack vardır. main thread'de buraya dahildir. primitive değerler ve objelerin referansları, stack deposunda tutulur. fakat objeler heap'te tutulur.

thread'de (stack'te) her metod, kendi içinde ona pass edilen tüm verileride tutuyor. yani stack içinde her metod için ayrı bir bölge var. bu sebeple;

```java
metod1(){

     User user1 = new User("ahmet");

     metod2(user1);

     print( user1.name ); --> burasi ekrana ahmet basacaktır.

}

metod2(User user){

    // burada; metod2 bölgemizde; sadece user diye bir variable var.
    
    user = new User("Ayse");  //bu satırda user variable'nin üzerine yeni bir variable atamış oluyoruz. sadece metod2 bölgesinde bir değişiklik yaptık. eski instance yaşamaya devam ediyor.

}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# call by value (or pass by value) vs call by reference (or pass by reference)
genel programlama dillerinde kullanılan terimlerdir.

Java primitive ve objeler için (yani her zaman) için call-by-value yöntemini kullanır. burada bir konuyu netleştirelim: java'da objenin value'si geçilirken, aslında objenin heap'teki referansı geçilir. buraya kadar herşey normal. fakat geçilen bu referans'ın kopyası (clone'u), stack içindeki sadece o metoda ait yerde tutulur. yani hem dallandığımız metod içerisinde hemde metodu çağırdığımız metod içerisinde 2 adet kopya olmuş olur.

yani; 'reference' değilde, 'referance value' yollamış oluyoruz. aslında reference yollanıyor fakat kopyası yollanıyor. yukarıdaki kod örneğinde bu kopya değerinin üzerine yeni objeminizin (Ayse) adresini yazıyoruz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# java debugger features
eclipse ve intellij debug mode'dayken aşağıdaki butonları sunar:

"force" prefix on intellij: intellij'de neredeyse her özellik force kombinasyonu ile de sunuluyor. force ile bir işlem yapınca yapmak istediğimiz işlemin içerisinde dubg point varsa, o debug point'ler ignore ediliyor.

- __step into__

  eclipse simgesi: ↴   (rightwards arrow with corner downwards)

  intellij simgesi: eclipse ile aynı fakat altçizgili.

  ilgili metodun içindeki ilk satıra gider.

  ek not: Intellij default olarak bazı metodların içine girmez. Bunlar jre'nin içindeki bazı metodlardır (örneğin System class'ı). Bu davranış biçimi ayarlardan değiştirilebilir.

- __smart step into__

  bu sadece intellij'de var. eclipse'te yok.

  intellij smgesi: ⇅   (upwards arrow leftwards of downwards arrow)

  "step into" ile aynı. fakat 1 satırda bazen birden fazla fonksiyon olabiliyor. örnek:

  > print( count() );

  intellij her fonksiyonu renklendirip hangisine girmek istediğimizi soruyor.

- __force step into__

  bu sadece intellij'de var. eclipse'te yok.

  intellij simgesi: "step into" ile aynı.

  "step into" eğer girdiğimiz metod 3üncü parti bir jar içinde ise ignore eder ve bir sonraki satıra geçer. fakat "force step into" 3üncü parti jar içine de olsa girer.

- __step over__

  eclipse simgesi: ↷   (clockwise top semicircle arrow)

  intellij simgesi: eclipse ile aynı fakat altçizgili.

  iligli satırı işletir ve sonraki satırda yine beklemede kalır.

- eclipse name: __step return__

  intellij name: __step out__

  eclipse simgesi: ↱   (upwards arrow with tip rightwards)

  intellij simgesi: ↑   (underlined upwards arrow)

  o anda bulunduğumuz metodun execute edilip sonlanmasını sağlıyor.

- __resume__

  simgesi: ->   (rightwards arrow)

- eclipse name: __run to line__

  intellij name: __run to cursor__

  eclipse simgesi: ->|   (rightwards arrow and cursor)

  intellij simgesi: eclipse ile aynı.

  thread durdurulmuşken buna bastığımızca, caret'in (imleç'in) gösterdiği satıra kadar hiç durmadan gider. Yani kod execiton'ı satır satır devam eder. Ancak bizim bulunduğumuz satırda yine beklemeye alınır.

- eclipse name: __drop to frame__

  intellij name: __drop frame__

  eclipse simgesi: ☰->   (triagram and small rightwards arrow)
  
  intellj simgesi: x☐   ("x" and empty box)

  o anda bulunduğumuz metodun tekrardan işletilmesini sağlıyor. bunun için:
  - o metodun içinde yaratılmış bütün kaynakları (string, int...) yok ediyor
  - debug noktasını metodun en başına taşıyor

  bu durumda metodun aldığı parametrelerin referanslarında değişiklik yapmışsak, o değişiklikler kalmaya devam ediyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# stringbuilder vs stringbuffer

aynı işi gören iki kütüphanedir. tek farkı stringbuffer'ın thread safe olmasıdır. bu da stringbuilder'ı daha performanslı yapıyor.

thread safe konusu stringbuilder ile başka başlıkta anlatılıyor.

# string vs stringbuilder

compiler "b" + "a" gibi satırları stringbuilder ile yapıyor ve bu şekilde memory'den kazanmamızı sağlıyor. fakat derleyici %100 her zaman stringbuffer'a çeviremeyebiliyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# immutable types
- tersi mutable'dır.
- immutable‘ın türkçe kelime anlamı: durağan, sabit, değişmeyen.

bir nesnenin içindeki referans değişken değiştirilemez olduğunda bu nesne immutable tipinde demektir. örneğin unmodifiable collections'lar immutable'dır. çünkkü içindeki referans değişkenler (liste elemanları) değiştirilemezler. burada karıştırılmaması gereken nokta;

List<Character> immutablelist = Collections.unmodifiableList(list); //immutable yaptık

immutablelist.add("yeni_deger"); //burası hata vermeli

immutablelist = list2; //burası hata vermemeli. çünkü immutable-list kavramı nesnenin kendisinin bir özelliğidir, nesnenin referansı konu dışıdır.

User nesnesi içindeki TC değişmemeli (kanun gereği kesin olduğunu varsayarsak); User immutable mı olur?  Hayır. Çünkü User içindeki ad, soyad her zaman değişebilir. User nesnesinin içindeki hiçbir değişken değiştirilemez olursa ancak immutable olur.

# Immutability avantajlari

- Istedigimizde getter'lardan bu objeyi döndürürüz

- multitread uygulamalarda guvenlik saglar

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# optional
java 8 ile gelmiştir. nullpointer kontrollerinin gerekmediği daha temiz kod yazılabilmesini sağlamaktadır.

```java
String message = null;

Optional<String> opt = Optional.ofNullable(message); // ofNullable null değer alırsa nullpointer fırlatmaz.


opt.filter(m -> m.length() > 5) // filter, filtreleme yapmamızı sağlayan ek bir metoduddur
      .ifPresent(System.out::println); // eğer filtre sonucundaki değeler null değilse, bu kod bloğu işletilir. böylece null kontrolü yapmamış oluyoruz.
```

Bu şekilde if(message ==null) gibi sorgular yazmayız.

- Optional<Double> empty = Optional.empty();

  boş bir Optional nesnesi oluşturur
  
- Optional<String> of = Optional.of("Merhaba");

  of metodu null değer alırsa nullpointerexception fırlatır
  
- Optional<Integer> ofNullable = Optional.ofNullable(null);

  ofNullable null değer kabul eder hata fırlatmaz.

- ifPreset metodu
  
  Preset kelime anlamı: mevcut

  eğer opt içindeki değer null değilse ifPresent metodu koşar.

  ```java
    opt.ifPresent(num -> {
        Double karesi = Math.pow(num , 2);
        System.out.println("Sonuç: " + karesi);
    });
  ```

- orElse

  ```java
  Integer numara = null;

  Optional<Integer> opt = Optional.ofNullable(numara);

  int result = opt.orElse(0); //opt null ise 0 döndürür.
  ```

- orElseThrow

  opt null ise parametrede geçeceğimiz exception'u fırlatır.

  ```java
  int result = opt.orElseThrow(RuntimeException::new);
  ```

- orElseGet

  orElse ile aynı mantıkta çalışmaktadır. tek bir obje yerine fonksiyon parametre alması. eğer opt null ise; parametre geçtiğimiz fonksiyonumuzun döndürdüğü değeri döndürür.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Nashorn
java ile yazılmış, javascript motorudur.

js komutu ile javascript dosyası execute edilebiliyor (node.js teki gibi).

# java'dan js çağırma örneği:

- js kodu:

```js
var fun1 = function(name) {

    print('Hi there from Javascript, ' + name);

    return "greetings from javascript";

};
```

- java kodu

```java
ScriptEngine engine = new ScriptEngineManager().getEngineByName("nashorn");

engine.eval(new FileReader("script.js"));

Invocable invocable = (Invocable) engine;

Object result = invocable.invokeFunction("fun1", "Peter Parker");

System.out.println(result);

System.out.println(result.getClass()); //prints java.lang.String
```

# javascript tarafından java kodu çağırma örneği:

- java kodu:

```java
static String fun1(String name) {

    System.out.format("Hi there from Java, %s", name);

    return "greetings from java";

}
```

- js kodu:

```js
var MyJavaClass = Java.type('my.package.MyJavaClass');

var result = MyJavaClass.fun1('John Doe');

print(result);
```

# object types

js tarafından java'ya obje parametresi geçerken;

- çervilebilen değerler (json standardındakiler) java.lang içindeki String, int, boolean gibi sınıflara çevriliyor.

- objeler java tarafından bilinmeyen objeler ise (örneğin bir json objesi) ; o zaman "jdk.nashorn.internal.scripts.JO4" Sınıfına cast ediliyor. Bu sınıftan get("myJsValue") gibi metodlarla sınıf objelerini çekebiliyoruz.

- MyJavaClass.fun2(new Date()); gibi genel olarak kullanılabilecek sınıfları "jdk.nashorn.internal.objects.NativeDate" gibi sınıflara çeviriyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Orika
object to object mapper for java runtime.

örnek: 

```java
mapperFactory.classMap(Source.class, Dest.class);
MapperFacade mapper = mapperFactory.getMapperFacade();
Source src = new Source("abc", 99);
Dest dest = mapper.map(src, Dest.class);
```

Yukarıda "Source" class ve "Dest" class'ında aynı isimde property'ler olmalı. eğer farklı property'leri map edecek isek;

```java
mapperFactory.classMap(Source.class, Dest.class).field("nom", "name").field("surnom", "nickname").register();
```

# Dozer
orika'ya alternatif ve nerdeyse aynı kod API'si olan kütüphane. Dozer, reflection'lardan yararlanarak mapping yaparken, Orika mapping yapılacak objeyi bytecode'a çevirir ve sonrasında mapping yapar.

# JMapper vs modelmapper vs MapStruct
orika ve dozer'a alternatif kütüphanelerdir.

# Mapstruct
örnek bir mapstruct mapper'ı:

```java
// import org.mapstruct.Mapper; aşağıdaki satırlar commente alındığı için burayı da comment'e aldım.
import org.mapstruct.Mapper;

@Mapper
public interface EmployeeMapper {

    /*

    istersek bu şekilde custom mapping'ler belirtebiliriz.
    bu örnekte comment olarak bıraktım.

    @Mappings({
      @Mapping(target="employeeId", source="entity.id"),
      @Mapping(target="employeeName", source="entity.name")
    })
    */
    EmployeeDTO employeeToEmployeeDTO(Employee entity);
    
    /*
    @Mappings({
      @Mapping(target="id", source="dto.employeeId"),
      @Mapping(target="name", source="dto.employeeName")
    })
    */
    Employee employeeDTOtoEmployee(EmployeeDTO dto);
}
```

Mapstruct compile sırasında bu interface'in bir implementasyonunu oluşturuyor "target" dizini içerisinde:

```java
public class SimpleSourceDestinationMapperImpl implements SimpleSourceDestinationMapper {

    @Override
    public SimpleDestination sourceToDestination(SimpleSource source) {
        if ( source == null ) {
            return null;
        }
        SimpleDestination simpleDestination = new SimpleDestination();
        simpleDestination.setName( source.getName() );
        simpleDestination.setDescription( source.getDescription() );
        return simpleDestination;
    }

    @Override
    public SimpleSource destinationToSource(SimpleDestination destination){
        if ( destination == null ) {
            return null;
        }
        SimpleSource simpleSource = new SimpleSource();
        simpleSource.setName( destination.getName() );
        simpleSource.setDescription( destination.getDescription() );
        return simpleSource;
    }
}
```

Compile sırasında mapstruct hata verebilirken, IDE'lerdeki eklentiler sayesinde compile etmeden de hataları görebiliriz.

Spring entegrasyonu için ilgili mapper'a bu eklenmelidir:

```java
import org.mapstruct.Mapper;

@Mapper(componentModel = "spring")
```

Böyle olunca implementasyonun teepsine mapstruct sadece @Component anotation'unu ekliyor. Böylece spring otomatik bunu bean olarak algılıyor ve istediğimiz yerden Autowired edebiliyoruz.

Mapstruct'ın en verimli yanı, basit bir yöntem tercih etmesi. Implementasyonları IDE'den direk görebiliyoruz. Hatta implementasyonları kopyalıyıp projemize yapıştırırsak, mapsttruct'ı tamamen (dependency olarak) projeden silebiliriz. Yani implementasyonlar anotation olmayan saf java kodlarıdır. Mapping'ler bazen çok karışık olabiliyor (map yapılan dto'larda içiçe objeler, abstact generic sınıfılar olabiliyor). Mpastruct'ın runtime sırasında ne yapacağında şüphe duymadan, direk implementasyonu (getter/setter'lardan oluşan core java sınıfılarını) inceleyebiliriz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Jeasy
java için birçok birbirinden bağımsız kütüphaneler geliştiren projenin ismidir.  

j-easy github ve www.jeasy.org'u kullanırlar. 

# easy-random
Jeasy'nin bir kütüphanesidir.

easy-random'un API'sine bir java sınıfı veririz, easy-random bu java sınıfının içindeki değerleri random bilgilerle doldurulmuş (değerleri set edilmiş) şekilde döndürür. 

4.0 sürümü öncesi, projenin ismi random-beans'tı. 4.0 ile easy-random yapıldı. Aynı sürümde io.github.benas paket ismindeki kodlar, org.jeasy altına taşındı.

Bu kütüphane test yazımında büyük kolaylık sağlar.

örnek:

```java
EasyRandom easyRandom = new EasyRandom();
Person person = easyRandom.nextObject(Person.class);
```

Opsiyolenl olarak, random olacak bilgilerin aralıklarını vs verebiliriz:

```java
EasyRandomParameters parameters = new EasyRandomParameters()
   .seed(123L)
   .objectPoolSize(100)
   .randomizationDepth(3)
   .charset(forName("UTF-8"))
   .timeRange(nine, five)
   .dateRange(today, tomorrow)
   .stringLengthRange(5, 50)
   .collectionSizeRange(1, 10)
   .excludeField(named("age").and(ofType(Integer.class)).and(inClass(Person.class)));

EasyRandom easyRandom = new EasyRandom(parameters);
```

