############################

############################
# JAVA SERIALIZERS
############################

############################

# gson
java için java objelerini json'a çevirip tekrar java objesine çevirme kütüphanesidir.

# JAXB (Java Architecture for XML Binding)
- Java içinde gelen XML kütüphanesidir.
- javax.xml.bind.* paketleri kümesini kapsar.
- Java 9 ile debrecated olarak işaretlendi, 10 ile tamamen kaldırıldı.
- marshalling ve unmarshalling yapar ve verilen xml şemasına göre Java objeleri oluşturur.
- marshalling işlemi sonrası bir xml oluşur. bu xml hem kolay okunabilirliği de sağlar, aynı zamanda üzerinde un-marshalling yapmadan önce değişiklikler de yapılmasını kolaylaştırır. oysa serializable'da bir nesne dosyaya dönüştürülmüşse artık değişiklik mümkün diildir.

# Jackson
asıl öncelikleri JSON olan, fakat ekstradan XML gibi birçok formatı ayrıştıran, üreten, işleyen bir Java Kütüphanesidir.

2.x'ten eski sürümler org.codehaus.# paketi altında dağıtılıyordu, 2.x sürümü ise com.fasterxml.* altında dağıtılıyor.

```java
@JsonPropertyOrder({"age", "id", "name"})
public class Person {
  
    @JsonProperty("_id")
    private String id;

    private String name;

    private int age;

    @JsonIgnore
    private String note;
}
```

Jackson 3 farklı alt projeden oluşuyor:

- Streaming (jackson-core)

  Burada xml/json derleme gibi işlemleri yapan core kodlar mevcut. alttaki tüm altprojeler bu projeye depend eder.

- Annotations (jackson-annotations) 

  sadece annotation'lar ayrı olarak bu projede barındırılıyor. annotation kullanmak istemeyenler bu projeyi classpath'te bulundurmak zorunda diil.

- Databind (jackson-databind)

  ObjectMapper/XmlMapper gibi sınıfıların bulunduğu paket.

Yukarıdaki tüm dependency'leri tek bir maven paketinden bulabiliriz:

```xml
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
    <version>2.10.0</version> 
</dependency>
```

Yukarıdaki maven dependency'si sadece xml formatı için objectmapper türevini içerir. "jackson-dataformat-xml" yerine buradaki formatlardan birini tercih edebiliriz: (source-id: 316)

## ObjectMapper vs XmlMapper
ObjectMapper, json işleme metodlarının bulunduğu API. XmlMapper ise projeye sonradna eklendi. XmlMapper, ObjectMapper'dan türemiş bir sınıf. tüm metodları override edilmiş ve sadece xml işleme için kullanılmak için tasarlanmıştır.

## Modules
Jackson 3th parti module altyapısını destekler. moduller araya girerek birçok ek özellik katabilir. modülleri jackson'a register etmemiz gereklidir:

```java
ModuleX moduleX = new ModuleX();
objectMapper.registerModule(moduleX);
```

Eğer manuel registration yapmaz isek bu metod ile claspath'te bulunan tüm metodları oto register yapabiliriz:

```java
ObjectMapper.findAndRegisterModules();
```

Jackson wiki'lerinde "Core modules" kısmında, yukarıda belirttiğimiz 3 proje gösteriliyor: Streaming, Annotations, Databind. fakat bunlar birer modül gibi register etmek gerekmiyor.

Bazı modüller aşağıdaki repo'larda geliştiriliyor. her repo'nun içinde birden fazla modüle mevcut.
- (source-id: 317)
- (source-id: 318)

Bazı modüller:

- ## Jackson Module JAXB Annotations
  JAXB, Jackson'a alternatiftir. önceden jaxb kullanıyorsak, JAXB'nin annotation'larını bazı java bean'lerimize atmış olabiliriz. bunları Jackson'ın da algılamasını istiyorsan bu projeden yararlanmamız gerekir.

  ```xml
  <dependency>
    <groupId>com.fasterxml.jackson.module</groupId>
    <artifactId>jackson-module-jaxb-annotations</artifactId>
    <version>2.4.0</version>
  </dependency>
  ```

- ## jackson-datatype-jdk8
  jdk 8 ile gelen optional değerler için support sağlıyor. örnek: serialize edeceğimiz sınıfımızda bu değere destek verebiliriz:

  ```java
  class Person {
      private final String name;
      private final Optional<String> email;
  ```

- ## jackson-datatype-jsr310
  Java 8 ile gelen java.time.* kütüphanesinin serileştirmesine yardımcı olur.
 
  ```xml
  <dependency>
      <groupId>com.fasterxml.jackson.datatype</groupId>
      <artifactId>jackson-datatype-jsr310</artifactId>
  </dependency>
  ```
