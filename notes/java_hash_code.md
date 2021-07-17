############################

############################
# JAVA HASH CODE
############################

############################

# Nesne eşitliği

# Nesne eşitliğini bulma

Java'da == ifadesi iki nesnenin referasnlarının aynı olup olmadığına bakar. eğer karşılaştırılan nesneler primitive ise (int, boolean...), sadece değerleri karşılaştırılır.

Java'da her nesne, object sınıfından türemiştir ve equals(Object) metodu içerir. Bu metod ile iki obje karşılaştırılabilir. Bu karşılaştırmada metodunu yazılımcı override ettiği için istediğini döner. fakat asıl yapılması (beklenen) dönüş; sınıfın içindeki unique değerlerin kontrol edilerek dönüş almaktır. Tabi sadece unique değerler karşılaştırılarak olmaz, zira karşılaştırılan sınıflarda aynı tipte olmalıdır.

Eğer equals metodu override eilmez ise; oject sınıfındaki metoda göre referansları aynı olan sınfılar için true dönüşü alırız. Yani; override edilmezse == 'e denk geliyor.

hashCode veya equal kullanırken tüm elemanları göz önünde bulundurmak zorunda diiliz.

# hashcode
Equals ile benzer mantıkta olan hashCode() bir integer ile unique bir değer döndürmeli. hastable gibi modellerde, bir sınıfın hash değerini saklamak gerekir diye bu metod hazır olmalıdır. Integer dönmesinin sebebi; eşitlik kontrolünün equals'a göre daha hızlı yapılmasını sağlamaktır. Yani; equals ile aynı amaçta kullanılır fakat hashCode Integer olduğundan equals gibi her dai güvenebileceğimiz bir bilgi değildir. Dolayısı ile avantajlar/dezavantajlar konusuna dönmekteyiz.

Hashcode'un dönüş değeri integer olduğundan, kısıtlı çıktı kümesi vardır. Bu sebeple aslında; unique değildir. Bu sebeple bazı instance'ların hashcode'ları çakışır (hash collision). Buna en basit örnek string'lerdir. Bir string'in sonsuz farklı instance'ını yaratabiliriz. Bu durumda hashcode'lar illaki çakışacaktır. Örneğin javada; "Siblings" ve "Teheran", "Aa" ve "BB" aynı hashcode döndürür. Bu sebeple java-core'daki HashMap sınıfı önce hashCode'a bakar, eğer hashcode'u aynı olan nesneler tutuyor olursa, equals veya referans (==) kontrolüne tabi tutar. Böylece çakışmaları çözmüş olur. HashMap'in önce hashcode'a bakmasının sebebi, integer ile eşitlik kontrolünün bilgisayarlar tarafından daha hızlı yapılmasıdır.

Eğer dto'muz immutable ise, hashcode'u her defa hesaplatmak yerine, initialize olduğunda yada bir kere hashCode çarıldığında bunu bi field'da yerde tutup, hashcode'u sürekli bu field'dan döndürebiliriz. bu bize performans avantajı sağlar.

Hashcode'u (hiç özel kütüphane kullanmadan) yazmak için genelde bu yötem tercih edilir:

```java
// intellij (version 2020) auto-generated equals ve hashCode örneği

import java.util.Arrays;
import java.util.List;

public class TestDTO {

  private String valStr;
  private int valInt;
  private Integer valInteger;
  private TestDTO valTestDTO;
  private long valLong;
  private char valChar;
  private boolean valBoolean;
  private String[] valStringArray;
  private List<String> valStringList;

  @Override
  public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;

    TestDTO testDTO = (TestDTO) o;

    if (valInt != testDTO.valInt) return false;
    if (valLong != testDTO.valLong) return false;
    if (valChar != testDTO.valChar) return false;
    if (valBoolean != testDTO.valBoolean) return false;
    if (valStr != null ? !valStr.equals(testDTO.valStr) : testDTO.valStr != null) return false;
    if (valInteger != null ? !valInteger.equals(testDTO.valInteger) : testDTO.valInteger != null) return false;
    if (valTestDTO != null ? !valTestDTO.equals(testDTO.valTestDTO) : testDTO.valTestDTO != null) return false;
    // Probably incorrect - comparing Object[] arrays with Arrays.equals
    if (!Arrays.equals(valStringArray, testDTO.valStringArray)) return false;
    return valStringList != null ? valStringList.equals(testDTO.valStringList) : testDTO.valStringList == null;
  }

  @Override
  public int hashCode() {
    int result = valStr != null ? valStr.hashCode() : 0;
    result = 31 * result + valInt;
    result = 31 * result + (valInteger != null ? valInteger.hashCode() : 0);
    result = 31 * result + (valTestDTO != null ? valTestDTO.hashCode() : 0);
    result = 31 * result + (int) (valLong ^ (valLong >>> 32));
    result = 31 * result + (int) valChar;
    result = 31 * result + (valBoolean ? 1 : 0);
    result = 31 * result + Arrays.hashCode(valStringArray);
    result = 31 * result + (valStringList != null ? valStringList.hashCode() : 0);
    return result;
  }
}
```

yukarıda görüldüğü gibi Long, String gibi class'ların hashCode metodları zaten java-core'da implemente edilmiş durumda. DTO'larımızın hashCode'ları olmazsa onu kullanan sınıflarda hashCode alamayız.

Integer'ın hashcode'u (tahmin edildiği gibi) kendisidir.

boolean'ın hashcode'unu 1 veya 0 şeklinde çevirebiliriz. en basit çözüm olcaktır.

her field'ın 31 gibi sabit bir asal sayı (or prime number) ile çarpılması önerilir. Tek sayı (or odd number) olması diil, asal sayı olması önemlidir. Bunun sebebi matematikseldir. Burada önemli olan nokta şudur: asal sayı ile çarpmak unique sayı dönmesinin ihtimalini arttırmaz, onun yerine Collection'larda matematiksel avantaj sağlar.

Bunun uzun açıklaması şudur: Hash-map ve hashset gibi collection'lar, her hash-code değerlerini "bucket" denilen yerde saklar. İnsert yapıldığında, insert edilen objenin hash-code değerini (integer) saklaması gerektiğinde, nokta atışı yerini çabuk bulabilmek/belirleyebilmek için hash değerini bucket'ın index'i olarak kabul eder. Fakat bucket Integer.MAX büyüklüğünde olamaz. Öyle olursa çok yer kaplar. İşte bu sebeple hash'in modülünü (%) alır. Örneğin; bucket-size 20 ise ve hash-code değerimiz 21 ise, 21%20=1'dir. Yani bu hash ilk bucket'a kaydedilir. Diğer gelecek hash-değerleri eğer index 1'e denk gelmezse hash-map daha hızlı çalışacaktır. İşte modül işlemine tabi tutulduğunda, sonucun dağıtık olması için en basit çözümü bir asal sayı ile çarpmaktır. Yani; asal sayı ile çarpmak hashcode'un tekil olmasını değil, modül işlemine tabi tutulduğunda dağıtık (farklı) sonuç vermesi ihtimalini arttırmaktadır.

Ek not:
aşağıdaki rakamlar kütüphaneye göre değişkenlik gösterir ama genelde ortalama rakamlar şu şekildedir:
- hash-map init edildiğinde 20 bucket alanı rezerv edilir.
- bucket sayısı %75 doluluk oranına ulaştığında yeni bucket alanları otomatik olarak rezerv edilir (bucket sayısı arttırılır).

Hashcode'un kalitesini 2 şey belirler:
- olabildiğince unique olması (eğer instance sayısı Integer.MAX 'ı geçemez ise, unique olması, sıralama işlemleri için şarttır)
- mod alındığında dağıtık sonuçlar verebilmesi (hash ile işlem yapan collection'ların performance 'ını arttır)

Asal sayı olarak özellikle "31" sıkça kullanılır. çünkü 31, standart cpu'larda performans olarak basit bir işlem olarak yapılabilir. iinterpreter'lar bunu genellikle otomatik olarak aşağıdaki işleme çevirir:

```
31 * i = (i << 5) - i
```

Google-Guava kütüphanesi var ise aşağıdaki yöntem de kullanılabilir:

```java
import com.google.common.base.Objects;

import java.util.List;

public class TestDTO {

  private String valStr;
  private int valInt;
  private Integer valInteger;
  private TestDTO valTestDTO;
  private long valLong;
  private char valChar;
  private boolean valBoolean;
  private String[] valStringArray;
  private List<String> valStringList;

  @Override
  public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    TestDTO testDTO = (TestDTO) o;
    return valInt == testDTO.valInt && valLong == testDTO.valLong && valChar == testDTO.valChar && valBoolean == testDTO.valBoolean && Objects.equal(valStr, testDTO.valStr) && Objects.equal(valInteger, testDTO.valInteger) && Objects.equal(valTestDTO, testDTO.valTestDTO) && Objects.equal(valStringArray, testDTO.valStringArray) && Objects.equal(valStringList, testDTO.valStringList);
  }

  @Override
  public int hashCode() {
    return Objects.hashCode(valStr, valInt, valInteger, valTestDTO, valLong, valChar, valBoolean, valStringArray, valStringList);
  }
}
```

apache-commons kullanırsak bu şekilde de yapabiliriz:

```java
// apache-commons-lang v3 ve öncesi arasında hiçbir metod ve class ismi farkemiyor. sadece package farkediyor.

import org.apache.commons.lang.builder.EqualsBuilder;
import org.apache.commons.lang.builder.HashCodeBuilder;

import java.util.List;

public class TestDTO {

  private String valStr;
  private int valInt;
  private Integer valInteger;
  private TestDTO valTestDTO;
  private long valLong;
  private char valChar;
  private boolean valBoolean;
  private String[] valStringArray;
  private List<String> valStringList;

  @Override
  public boolean equals(Object o) {
    if (this == o) return true;

    if (o == null || getClass() != o.getClass()) return false;

    TestDTO testDTO = (TestDTO) o;

    return new EqualsBuilder().append(valInt, testDTO.valInt).append(valLong, testDTO.valLong).append(valChar, testDTO.valChar).append(valBoolean, testDTO.valBoolean).append(valStr, testDTO.valStr).append(valInteger, testDTO.valInteger).append(valTestDTO, testDTO.valTestDTO).append(valStringArray, testDTO.valStringArray).append(valStringList, testDTO.valStringList).isEquals();
  }

  @Override
  public int hashCode() {
    return new HashCodeBuilder(17, 37).append(valStr).append(valInt).append(valInteger).append(valTestDTO).append(valLong).append(valChar).append(valBoolean).append(valStringArray).append(valStringList).toHashCode();
  }
}
```

# java.lang.String.hashCode()

(source-id: 323)

bu şekilde tanımlanmıştır:

```java
/**
* Returns a hash code for this string. The hash code for a
* {@code String} object is computed as
* <blockquote><pre>
* s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1]
* </pre></blockquote>
* using {@code int} arithmetic, where {@code s[i]} is the
* <i>i</i>th character of the string, {@code n} is the length of
* the string, and {@code ^} indicates exponentiation.
* (The hash value of the empty string is zero.)
*
* @return  a hash code value for this object.
*/
public int hashCode() {
    int h = hash;
    if (h == 0 && value.length > 0) {
        char val[] = value;

        for (int i = 0; i < value.length; i++) {
            h = 31 * h + val[i];
        }
        hash = h;
    }
    return h;
}
```

Doc okunduğunda üssel işlem görünmektedir. Fakat metod impelementasyonunda üssel işlem görünmüyor. Aslında for loop debug edip tamamlandığında doc'taki işleme denk gelmektedir:

1. döngü:
> h = 31 * hash + s[0]

2.döngü:
> h = 31 * (31 * hash + s[0]) + s[1] 

yada bu şekilde de yazabiliriz:

> h = 31^2 * hash + 31 * s[0] + s[1]

3. döngü:

> h = 31 * (31 * (31 * hash + s[0]) + s[1]) + s[2]

yada bu şekilde de yazabiliriz:

> h = 31^3 * hash + 32^2 * s[0] + 31 * s[1] + s[2]

Sonuç olaak dikkat edersek doc'taki açıklama ile aynı kapıya çıktığını görebiliriz.

# primitive'lerin objece karşılıklarındaki eşitlik kontrolleri (primitive wrapper'ların eşitlik kontrolleri)
new Integer(5) = new Integer(5); --> false vermektedir. referansları yeni obje oldugu icin farklı.

Integer.valueOf(5) == Integer.valueOf(5) --> valueOf metodu Integer objesi dondurmektedir. normalde false olması beklenmektedir. fakat true vermektedir. çünkü; Integer sınıfı kendi icinde initialize olurken static olarak 1'den 256'ya kadar olan sayılar için birer Integer objesi saklamaktadır. çünkü bunlar genelde cok kullanılan sayılardır. valueOf metodu bu sayılar haricinde "new Integer()" calıştırıyor. fakat bu sayılardan ise hızlı olsun diye bunlardan donduruyor. bazı jvm'ler 256'dan daha fazla saklamaktadır.

java'da aynı string'ler aynı değeri göstermektedir. çünkü JVM, her string'i "__string pool__" denilen yerde saklamakta ve yeni oluşturulan string'ler aynı ise, referansını buradan dönmektedir. bu sebeple == equals yerine kullanılmaktadır. fakat new String("text") her zaman yeni bir referansla obje yaratmaktadır. bu sebeple bunlarda == kullanılamaz. new String("text").intern() metodu varolan jvm'deki string'lere referans etmemizi sağlıyor. bu şekilde bellekten tasarruf etmiş oluyoruz.

# hashcode and equals method for DB entity classes
lets define simply what is equals: Equals method should return true, if the identifiers of them are same.

- 1

if we don't implement the hashcode and equals methods, then if we read multiple times the same row from DB, the equals and the hashcode methods will return false for both instances because java will check the instance memory references.

- 2

if we will implement hashcode and equals method using all fields, that not's gonna work in this case:

```java
user1 = new User("Jack").
repository.save(user1);

user2 = repository.readByPrimaryKey("12345");
user2.equals(user1); // returns false because "id" field is null on user1 yet.
```

- 3

if we will implement the equals and hashcode based on "natural key", we will have un-consistent cases like this:

```java
user1 = new User("998877", "Jack").
repository.save(user1);

user1.setName(); // the user has a new identity number...

user2 = repository.readByNationalIdentityNumber("998877");
user2.equals(user1); // returns false.
```

The possible way is to do not use JPA's primary keys. we can manage them manually. We can initialize "id" field on constructor. And we have to compare only "id" field which is unique. For consistent ID generation we can use UUID.

Example abstract class for all entities on the project:

```java
public interface PersistentObject {
    public String getId();
    public void setId(String id);

    public Integer getVersion();
    public void setVersion(Integer version);
}

public abstract class AbstractPersistentObject
        implements PersistentObject {

    private String id = IdGenerator.createId();
    // JPA, DB'den okudğu zaman burası da her defasında çalışacak fakat JPA sonrasında setter'ı çağıracağı için eski data yazılacak. yani bir sorun yok

    private Integer version;

    public String getId() {
        return id;
    }
    public void setId(String id) {
        this.id = id;
    }

    public Integer getVersion() {
        return version;
    }
    public void setVersion(Integer version) {
        this.version = version;
    }

    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null ||
            !(o instanceof PersistentObject)) {

            return false;
        }

        PersistentObject other
            = (PersistentObject)o;

        // if the id is missing, return false
        if (id == null) return false;

        // equivalence by id
        return id.equals(other.getId());
    }

    public int hashCode() {
        if (id != null) {
            return id.hashCode();
        } else {
            return super.hashCode();
        }
    }

    public String toString() {
        return this.getClass().getName()
            + "[id=" + id + "]";
    }
}
```

Yukarıdaki örnekte neden version kullandık? Çünkü JPA normal koşullarda id field'ı boş ise bu instance'ı yeni row olarak algılıyor. Bu durumu çözebilmek için version sutunu kullandık. version sutunu eğer set edilmiş ise JPA bunu zaten kaydedilmiş bir instance olarak algılayacak. BUnun için şu confG'leri de yapmamız gerekli:

```xml
<?xml version="1.0"?>
<!DOCTYPE hibernate-mapping SYSTEM
"http://hibernate.sourceforge.net/
hibernate-mapping-3.0.dtd">

<hibernate-mapping package="my.package">

  <class name="Person" table="PERSON">

    <id name="id" column="ID">
      <generator class="assigned" />
    </id>

    <version name="version" column="VERSION"
        unsaved-value="null" />

    <!-- Map Person-specific properties here. -->

  </class>

</hibernate-mapping>
```

Source:
- (source-id: 324)
- (source-id: 325)
- (source-id: 326)
