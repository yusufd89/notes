############################

############################
# JAVA SPRING
############################

############################

# dependency yönetimi
maven-pom'da şu eklenirse:

```xml
<parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.2.RELEASE</version>
</parent>
```

spring'in 1.5.2 versiyonunun tüm dependency'leri artık tanımlanmış (eklenmemiş,sadece tanımlanmış!) olur. Artık aşağıdaki gibi bir kütüphane ekleyebiliriz:

```xml
<dependencies>
        <dependency>
             <groupId>org.springframework.boot</groupId>
             <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
</dependency>
```

spring-boot-starter-web'in sürümünü belirtmeye gerek yok çünkü zaten parent'ta tanımlanmıştı.

spring-boot-starter-web projesi default olarak embeeded tomcat kullanır. biz bunun yerine jetty kullanmak istersek aşağıdakini yazmamı yeterli olacaktır:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-tomcat</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-jetty</artifactId>
    </dependency>
</dependencies>
```

# Starters
spring-boot-starter-XYZ formatında yazılırlar. XYZ uygulamamızın tipidir.

örneğin;

spring-boot-starter-web; spring-mvc ve tomcat embeded getirir.

spring-boot-starter-jersey; web'e bir alternatiftir. spring-mvc yerine Apache Jersey kullanır.

spring starter'lar spring-boot-dependencies'i kullanılarlar. spring-boot-dependencies sadece her paketin versiyonunu barındırıyor. oysa stretler'lar birçok paketi bir arada barındırıyor. örneğin web dediğimizde tomcat vs yüklenmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# org.springframework.web.filter.OncePerRequestFilter
Klasik filter ile aynı özellikleri içerir. Fakat bu filter, her request için en fazla 1 kere çalıştırılacağını garanti eder.

bir request'i başka bir servlet'e redirect edebiliriz. eğer redirect ettiğimiz servlet'in bir filter'ı var ise, o zaman o filter'larda devreye girecektir. işte böyle bir durumda; eğer OncePerRequestFilter'dan türemiş bir filter var ise, ve bu filter birden fazla servlet'in önünde ise, birden fazla çalışması durumu olmayacaktır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# stereotype
kelime anlamı: klişe, basmakalıp.

bu terim javaee ve spring'de kullanılan bir terimdir. java core'a ait değil. 

- javaEE'de; javaee tarafından yazılmış bir (custom) annotationdur. bu annotation javaee'nin kendi yazdığı bazı annotationların içinde kullanılır. bu annotation'un bir işlevi yoktur. amaç sadece gruplandırmak (mark etmektir).

- spring'de; asagidaki annotation'lar org.springframework.stereotype paketi altındadır. amaç (javaee'dekine benzer olarak) sadece gruplandırmaktır.

  - Component
  - Controller
  - Indexed
  - Repository
  - Service

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# spring-retry

```xml
<dependency>
    <groupId>org.springframework.retry</groupId>
    <artifactId>spring-retry</artifactId>
    <version>1.1.5.RELEASE</version>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aspects</artifactId>
</dependency>
```

```java
@Configuration
@EnableRetry
public class AppConfig { ... }
```

```java
@Service
public class MyService {

    @Retryable(
              // spring will try same method if the method throws SQLException
              value = { SQLException.class }, 
              // spring will try 2 times
              maxAttempts = 2,
              backoff = @Backoff(delay = 5000))
    void retryService(String sql) throws SQLException{
       // any code here
    }
    
    // Recover is optional. sping will call this method if 2 attemp will not work above.
    @Recover
    void recover(SQLException e, String sql){
       // any code here
    }
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Properties Class of Java
Java Map sınıfından türetilmiştir. Properties dosyalarına tekabül eden (bu mantıkta çalışmalar için) özel tasarlanmıştır.

# System Environments from Java

- Java kodları içerisinden sistemin environment değerleri (PATH, JAVA_HOME gibi) çağrılabilmektedir: System.getenv();

- Benzer mantıkta java programına yada JVM argümanarına parametre geçilebilir: "java -Dmyparam1=myvalue1 -jar myapp.jar". Bu parametreleri kod içerisinden almak için System.getProperties("myparam1") kullanılır.

- program argümanları ise; main'e string args[] ile geçilen paramerelerdir.

# Spring framework Externalized Configuration
Spring uygulaması başlarken onlarca sınıftan data okur. okuma öncelik sırasına göre aşağıdaki gibidir:

- Devtools global settings properties in the $HOME/.config/spring-boot folder when devtools is active.

- @TestPropertySource annotations on your tests.

- properties attribute on your tests. Available on @SpringBootTest and the test annotations for testing a particular slice of your application.

- Command line arguments.

- Properties from SPRING_APPLICATION_JSON (inline JSON embedded in an environment variable or system property).

- ServletConfig init parameters.

- ServletContext init parameters.

- JNDI attributes from java:comp/env.

- Java System properties (System.getProperties()).

- OS environment variables.

- A RandomValuePropertySource that has properties only in random.*.

- Profile-specific application properties outside of your packaged jar (application-{profile}.properties and YAML variants).

- Profile-specific application properties packaged inside your jar (application-{profile}.properties and YAML variants).

- Application properties outside of your packaged jar (application.properties and YAML variants).

- Application properties packaged inside your jar (application.properties and YAML variants).

- @PropertySource annotations on your @Configuration classes. Please note that such property sources are not added to the Environment until the application context is being refreshed. This is too late to configure certain properties such as logging.* and spring.main.* which are read before refresh begins.

- Default properties (specified by setting SpringApplication.setDefaultProperties).

kaynak: (source-id: 361) "2. Externalized Configuration" başlığı.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# SpringApplicationBuilder
spring boot uygulamamız başlatılmadan önce ayarlar set etmemizi sağlar. kullanımı direk @SpringBootApplication atılan sınıfın içinde olmalıdır. örnek:

```java
@SpringBootApplication
public class WebApplication extends SpringBootServletInitializer {

    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {

        application = new SpringApplicationBuilder();

        application.parent(new Object[]{"classpath:file1.xml", "classpath:file2.xml"})

       .profiles("abc")

       .properties("key1:test1", "key2:test2") 

      .showBanner(false)

      .logStartupInfo(true)

       .headless(true)

      .application()

      .run();

        return application;
    }

    public static void main(String[] args) throws Exception {

        SpringApplication.run(WebApplication.class, args);
    }
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# spring MVC
Rest supportu bu modül içindedir. ModelAndView objesi de bu modül içindedir.

## ModelAndView
Rest controllerımızı normal yazıyor ve gelen request'e cevap olarak ModelAndView döndürüyoruz.

```java
@Controller
class RegistrationController {

  @RequestMapping(value = "/register", method = RequestMethod.GET)
  public ModelAndView showRegister() {
    ModelAndView mav = new ModelAndView("register");
    mav.addObject("user", new User("Ahmet"));
    return mav;
  }
}
```

ModelAndView içinde 'model' ve 'jsp dosya path'i bilgisini barındırır. Spring "ViewResolver" sınıfında belirlendiği ayarlarla jsp'yi bulmaya çalışır. viewresolver config örneği;

```java
@Configuration
@EnableWebMvc
class WebConfig extends WebMvcConfigurerAdapter {

  @Bean
  public ViewResolver viewResolver() {
        InternalResourceViewResolver resolver = new InternalResourceViewResolver();
        resolver.setPrefix("/WEB-INF/views/");
        resolver.setSuffix(".jsp");
        resolver.setExposeContextBeansAsAttributes(true);
        return resolver;
  }
  
  @Override
  public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
    
        configurer.enable();
  }
}
```

Viewresolver'da belirtilen View'ı (jsp'yi) model ile doldurup response olarak yolluyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# @Configuration

```java
@Configuration
public class MyClassConfig {

    @Bean
    public TransferService transferService() {
        return new TransferServiceImpl();
    }
}
```

artık TransferService bean'i uygulamamızın herhangi bir yerinden çağrılmak istendiğinde (contextten inject edilmek istendiğinde), "new TransferServiceImpl()" instance'ı çağrılacaktır.

Configuration'ın üstüne @Profile("development") gibi profiller tanımlanabilir.

@Bean anotasyonu projenin herhangi bir dizininde (componentScan içinde olmak şartıyla) kullanılabilir. ve o metodun dönüş değeri bean olarak tanımlanacaktır. fakat @configuration anotasyonu ile bu beanleri gruplamış oluyoruz. ve bazı profillerde istediğimiz bean'ler aktif olurken, diğer profillerde  bean'leri aktif edebiliriz. örnek:

```java
public class MainApp {

   public static void main(String[] args) {

      ApplicationContext ctx = new AnnotationConfigApplicationContext(MyClassConfig.class);

      TransferService ts = ctx.getBean(TransferService.class);

      ts.doSomething();
   }
}
```

# org.springframework.context.annotation.Import sınıfı
annotation tanımımızın üstüne @Import(MyClass.class) yazabiliriz. bu şekilde o annotation'u barındıran sınıfta artık MyClass'ta olan herşey tanımlı olacaktır. MyClass'ın @Configuration barındıran bir sınıf olması şarttır.

Import sayesinde configuration'ları kolayca sınıflara grupandırıp tek bir sınıfta birleştirebiliriz. @Import, sadece @Configuration ile birlikte çalışabilmek için tasarlanmıştır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Spring framework

# SpringSource
spring framweork'ünü geliştiren firmanın eski ismi. firma ismi daha sonra spring oldu.
 
# Spring Tools (or STS or Spring Tools Suite)
Eclipse için spring eklentisidir. Eclipse'e yüklü şekilde de direk indirilebiliyor.

# spring modules

Spring birçok modül sunuyor. Bu modüller gruplandırılmış durumda ve her modül, farklı gruptan olsa da, başka bir modüle depend ediyor olabilir.

Aşağıdaki listede en üst seviyedeki başlıklar (örnek: "Data access & Integration", "Core Container") sadece gruplamak için yazılmıştır. bir artifact'ı temsil etmiyorlar. Oysa alt seviyedeki her madde birer artficat (jar) dosyasıdır ve maven'a eklendiklerinde ihtiyacı olan tüm bağımlılıkları çeker.

- Data access & Integration
  - __spring-jdbc__
  - __spring-orm__
  - __spring-oxm__: Object/XML mapping implementations for JAXB and other library
  - __spring-tx__: transaction support
- Web & Remoting
  - __spring-web__: httpclient + servlets (does not include REST classes like: @Controller)
  - __spring-webmvc__ (unofficial name: __web-servlet__): içinde spring-web'i barındırır. sadece REST supportu (örnek @Controller) buradadır, aynı zamanda ModelView classlarıda bu modüldedir.
  - __spring-websocket__
  - __spring-webmvc-portlet__ (unofficial name: __web-portlet__)
- Core Container
  - __spring-core__: IoC özelliği bu modülün içinde tanımlıdır.
  - __spring-beans__: BeanFactory özelliği bu modülün içinde tanımlıdır.
  - __spring-context__: ApplicationContext özelliği bu modülün içinde tanımlıdır.
  - __spring-expression (or spEL)__: "Expression Language" modülüdür. string üzerinde kelime işleme özellikleri barındırmaktadır. aynı zamanda bean property'lerine variable atayabilmek için özel syntax kullanımını sağlıyor.
- Aspect
  - __spring-aop__: method-interceptors (spring's own Aspect library)
  - __spring-aspects__: AspectJ ile entegrasyonu sağlamakadır (alternative of spring-aop)
- Others
  - __spring-test__: JUnit + TestNG support.
  - __spring-instrument__: support for class loader implementations

# maven artifact-id isimlendirmesi

Spring yukarıdaki modüller hariç de birçok özellik sunuyor. Yukarıda yazan modüller temel seviyede olduklarından;

- group-id: org.springframework
- artifact-id: spring-* (örnek spring-webmvc)

şeklinde dağıtılıyorlar. Yuakrıda olup "core container" grubu içerisinde olanlar:

- group-id: org.springframework
- artifact-id: org.springframework.* (örnek org.springframework.context)

şeklinde dağıtılıyor. Yukarıda olmayan modüller (örnek cloud, boot, batch) ise şu şekilde dağıtılıyor:

- group-id: org.springframework.* (örnek: org.springframework.batch)
- artifact-id: org.springframework.* (örnek spring-batch-core)

Spring her paketi paralelde OSGI uyumlu şekilde sunar. O paketlerin isimleri farklıdır. OSGI uyumlu paketler Enterprise Bundle Repository (EBR) üzerinden dağıtılmaktadır. Örnek: 

- group-id: org.springframework
- artifact-id (maven central): spring-core 
- artifact-id (Spring EBR): org.springframework.core

kaynak: (source-id: 362) "Spring modules on the Maven repository başlığı". yazarlar: "Rob Harrop", "Clarence Ho", kitap adı: "Pro Spring 3"

# spring version naming

(spring cloud versionları başka başlıkta anlatılıyor.)

- GA (or General availability): stable versiyon.

- RC (or Release candidate): beta versiyon.

- M (or Milestone build): nightly versiyon.

Yukarıdaki sürüm terimleri genel olarak tüm yazılım sürüm politikalarınca kullanılmaktadır. sadece spring'e özgü terimler diildir.

# spring version history

| version number | release year | compatible jdk version |
|----------------|--------------|------------------------|
| 0.9            | 2002         |                        |
| 1.0            | 2003         |                        |
| 2.0            | 2006         |                        |
| 3.0            | 2009         |                        |
| 4.0            | 2013         |                        |
| 4.3            |              | 6-8                    |
| 5.0            | 2017         | 8-10                   |
| 5.1            |              | 8-12                   |

# spring initializr
https://start.spring.io sitesinin altyapısı olan projedir. bu site ile web arayüzden spring modülleri seçebiliyoruz, paket ismi vs form girişi yaptıktan sonra bizim için gradle/maven, java/groovy gibi hazır boş spring projesi oluşturmaktadır. bu projeyi anında download etmemizi sağlıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Spring batch
temel olarak 3 işlevi yerine getirmek için geliştirilmiş altyapıdır:

- reading data
- processing data
- writing data

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Javaee dezavantajlar
- application server specific deployment descriptors

- lots of xml files even the most basic EJB - Güncel sürümlerde XML yerine annotation kullanılıyor (spring bu durumu daha önceden çözdüğü için sprig projesi ortaya çıkmıştı. Güncel sürümlerde bu sebep kalktı.)

- sunucu ayağa kalkma süresi (çünkü tüm kütüphaneler sunucu içerisinde) - Güncel sürümlerde sunucular çok hızlandı spring daha büyüdüğü için kısmen daha yavaşladı

- sunucuya bağımlılık

# spring dezavantajlar

- app sever üzerinde çalıştırılırsa ticari destek alınamaz

- app server'sız çalıştırılıdığında monitoring tool'ları genelde javaee sunucularına uyumlu olduğundan, monitoring işlemlerinde sıkıntılar yaşanabilir

not: Spring sadece servlet container'a ihtiyaç duyuyor. Oysa javaee bir spesifikasyon ve komple tüm library'ler sunucu içerisinde.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •
