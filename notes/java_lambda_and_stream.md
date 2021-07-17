############################

############################
# JAVA LAMBDA AND STREAM
############################

############################

# lambda expression (or tr:lamda ifadeleri)
Kalkülüs (or eng:calculus) hesap anlamına gelektedir. __"lambda calculus (or λ-calculus)"__ matematikte fonksiyonların ifade edilmesi için bir çeşit syntax'tır. programlama dillerindeki aynı yapıdır.

lambda programlama dünyasında anonim fonksiyon yaratmak için kullanılan özel bir syntax ismidir. örnek lamdba expression:

> (param1) --> { print(param1) }

lambda, programlama dünyasında anonim fonksiyon anlamına gelmemektedir. fakat anonim fonksiyon yaratmak için kullanılır. anonim fonksiyon için tek yol bu diildir. örneğin javascriptte şu şekilde de anonim metod yaratılabilir:

> function(param1){ print(param1) }

Yani; lambda expression kullanılmadan da anonim metod yaratılabiliyor.

javascript'te "lambda expression" terimi yerine; "arrow function expression" kullanılır.

# java dilinde lamda
java 8 ile hem lamda expression hemde fonksiyon arayüz (or function interface) özelliği gelmiştir.

```java
@FunctionalInterface //bu notasyon isteğe bağlı. hiçbir özelliği yok. ama atılması öneriliyor. cünkü normal interface'ler ile aynı syntax'ı var asagidaki kodun. farkını okuyan görebilmeli.
interface MyInterface {

    MyResultObj myMethod(int myParam);
}
```

ile yukarıda tanımlama yaptık. asagida da kullandık:

```java
MyInterface myInterface = realParam -> {

            System.out.println(realParam);
};

myInterface.myMethod(3);
```

myMethod'u implemente etmiş olduk. interfacede myMethod gibi sadece bir metod olabilir. daha fazla olamaz. bu sebeple metodu implemente ederken hiç "myMethod" string'ini hiç kullanmadık.

- myMethod iki adet parametre alsaydı, kullanım kısmında şu satır olacaktı:

  > MyInterface myInterface = (realParam, realParam2) -> {

- myMethod metodumuz isterse parametre döndürebilir. doğal olarak dönüş parametresi kullanım ksımında myInterface.myMethod(3) ‘teki myMethod metodundan dönüyor olacaktı.

- Interface ‘ler extend edebilirler.

- kullanım kısmında; System.out.println(3);  etrafındaki süslü { } parantezler yazılmayayabilir (tek satırlı kodlar için geçerli.)

- java.util.Function altında birçok hazır fonksiyon interfaceleri tanımlanmıştır. örnek: BiConsumer<T,U>, Consumer<T> gibi… Bunlar hazırdır. Çünkü; çoğu zaman genellikle fonksiyon interfaceleri 1-2-3 parametre alır ve bir parametre döner yada dönmez. Bunlar için sürekli yeni fonksiyon interface tanımlaması yapmamız gerekir. bu sebeple hazırları oluşturulmuştur. örnekler:

  - Consumer (tüketici) yani herhangi bir paramtre alır ama hiçbir şey dönmez

    ```java
    @FunctionalInterface
    public interface Consumer<T> {
        void accept(T t); // t-> {}
    }
    ```

    Consumer'a alternatif olan diğer birçok örneği tabloda toplarsak:
    
    (T, U, R herhangi bir class'ı temsil eder)

| interface adı  | aldıgı parametrelerin tipi | döndürğü parametre tipi |
|----------------|----------------------------|-------------------------|
| Consumer       | T                          | void                    |
| BiConsumer     | T U                        | void                    |
| Function       | T                          | R                       |
| BiFunction     | T U                        | R                       |
| UnaryOperator  | T                          | T                       |
| BinaryOperator | T T                        | T                       |
| Predicate      | T                          | boolean                 |
| BiPredicate    | T T                        | boolean                 |
| Supplier       | void                       | T                       |
| ToIntFunction  | T                          | int                     |
| DoubleConsumer | double                     | void                    |
| ObjIntConsumer | Object int                 | void                    |

# lambda vs closure
lambda closure ile aynı anlama gelmiyor. çoğu yerde aynıymış gibi yansıtılıyor. lambda bir syntax. closure ise return edilen bir fonksiyon aracılığı ile farklı scope'tan değer değiştirmemize yarayan metotdur. lambda desteği olan yazılımda mutlaka closure olabileceği için bu iki terim aynıymış gibi kullanılıyor.

# metod referansları
tanımlama kısmında, implemente etmiş olduğumuz metod zaten başka bir yerde zaten var ise, başka yerdekini direk referans edebiliriz. örnek;

```java
MyInterface myInterface = AnotherClass::otherMehod; //otherMehod is static method

MyInterface myInterface = anotherObj::otherMehod; //anotherObj is an instance

MyInterface myInterface = AnotherClass::new; //refers the constructor method
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# java stream
java 8 ile gelmiştir.

lamda'ya bağımlı olan (onu kullanarak yapılan) bir özelliktir. bu özellik java programlama dilinden gelmemiştir. java'daki kütüphaneler kendi içlerinde hazır, işe yarar interfaceleri bulundurmaya başlamışlardır. bu interfacelere genel olarak stream denilmiştir. Collection'dan türemiş tüm sınıfılar için işlemler ortak olduğundan, tüm stream kütüphaneleri ortak olarak java.util.stream paketi altında toplanmıştır. böylece tüm collection yada bir kütüphanede herkes ortak/bilindik metodları kullanabilmektedir. isteğe bağlı kendi stream interfacelerimizi yazabiliriz.

Java'ının içinde bulunan Stream tanımına bakarsak daha iyi kavrayabiliriz:

```java
public interface Stream<T> extends BaseStream<T, Stream<T>> {

   // Predicate kelime anlamı: yüklem, doğrulamak, belirtmek
   Stream<T> filter(Predicate<? super T> predicate);

   LongStream mapToLong(ToLongFunction<? super T> mapper);

   //yukarıdaki gibi birçok metod daha burada...

}
```

Yukarıdaki tanımlamada Stream<T> sınıfı sade basit bir interface. içindeki metodlarda implemente edilmeyi bekleyen metodlar. metodlar dikkat edilirse lambda fonksiyonu kabul ediyor. işte bu yüzden Stream, lambda teknolojisine dayalı bir kütüphanedir.

Şimdi ise örnek kullanımına bakalım:

```java
// sum(), mapToLong'dan tamamen bağımsız metod. 

long total = myList.stream().mapToLong(Long::parseLong).sum();

// yada

long total = myList.stream().mapToLong(

     valueFromStream -> Long.parseLong(valueFromStream) 
     
    ).sum();
```

```java
//en temel stream örneği. collectionlar artık stream metodlarını içermektedir.

List names = Arrays.asList("Ali","Veli","Selami");

Stream stream = names.stream(); //burada bir Stream implementasyonu dönmektedir. bu implementasyon  java.util.List tarafından hazırlanmış durumda.

stream.forEach(name -> {

    System.out.println(name);

});

names
    .stream()
    .filter(name -> name.length() == 4)
    .forEach(System.out::println);



//java.io içerisinde bazı sınıflarda stream döndüren metodlar gelmiştir.

Path dir = Paths.get("/var/log");

Stream pathStream = Files.list(dir); //list java 8 ile gelen yeni bir metod'dur.

//dizi içeriğini alarak direk hazır stream döndüren metodlar vardır. önceden dizi oluştumaya gerek kalmıyor.

IntStream intOf = IntStream.of(1, 2, 3); 

IntStream intRange = IntStream.range(1, 10); 

DoubleStream doubleOf = DoubleStream.of(1.0, 3.5, 6.6); 

```

En son örnekte görüldüğü gibi sadece java.util.stream.Stream yok. Bunun gibi biçok stream çeşidi var. örnek: java.util.stream.DoubleStream. Bunun gibi kendi stream'lerimizi de yazabiliriz.

Stream interfacesinde olan tüm metod imzalarından görüldüğü gibi çoğu metod yine Stream döndürüyor. Bu kolaylık olsun diye tasarlanmış bir yapı. böylece üstüste metod çağırmak istediğimizde her defasında stream'i tekrar çekmeye gerek kalmıyor.

java.util.stream.Stream içindeki ir kaç metoda detaylı bakalım:

```java
// collect: bir önceki stream'den dönen listedeki elemanları, collect'e parametre olarak verdiğimiz metoda yollar. ve dönen değeri döndürür.
List number = Arrays.asList(2,3,4,5,3);
Set square = number.stream().map(x->x*x).collect(Collectors.toSet());

// map: return değerinde olan elementler ile yeni bir liste oluşturuyor. daha sonrasında bu listeyi collect'te verdiğimiz metod'a parametre geçiyoruz.
List number = Arrays.asList(2,3,4,5);
List square = number.stream().map(x->x*x).collect(Collectors.toList());

// filter: map gibi yeni elemenlar döndürmüyor. sadece filtreden true dönen elemanları içeren yeni bir liste oluşturuyor.
List names = Arrays.asList("Reflection","Collection","Stream");
List result = names.stream().filter(s->s.startsWith("S")).collect(Collectors.toList());

// sorted
List names = Arrays.asList("Reflection","Collection","Stream");
List result = names.stream().sorted().collect(Collectors.toList()); 

// forEach: her eleman için fonksiyon çağırır
List number = Arrays.asList(2,3,4,5);
number.stream().forEach(y->System.out.println(y));

// reduce
// not: range 1, 2, 3 elementlerinden oluşan bir liste yaratıyor.
// recude metodu kümülatif işlemler yapmamızı sağlıyor.
// reduce önce 1 ve 2'yi bizim yolladığımız fonksiyona atıyor. daha sonra sonucu "3" ile yine bizim yolladığımız parametreye yolluyor. ve en sonda sonucu döndürüyor.
// yani; şu işlemler sırası ile oluyor:

// (1,2) -> 1+2   (buradan 3 geliyor)
// (3,3) -> 3+3   (buradan 6 geliyor)

// OptionalInt=6 olarak dönüyor.

OptionalInt reduced = IntStream.range(1, 4).reduce( (a,b) -> a+b  );

// Match operations
List<Notification> notificationList = Arrays.asList(notification1, notification2, notification3, notification4);

// noneMatch: her elementi kontrol eder. Belirtilen kriter listede hiçbir elemanda bulunmuyor ise true döndürür.
boolean isNoneMatch = notificationList.stream().noneMatch(notification -> notification.getTitle().contains("a"));

// allMatch Belirtilen kriter listede tüm elemanlarda bulunuyor ise true döndürür.
boolean isAllMatch = notificationList.stream().allMatch(notification -> notification.getTitle().contains("a"));

// anyMatch Belirtilen kriter listede herhangi bir elemanlarda bulunuyor ise true döndürür.
boolean isAnyMatch = notificationList.stream().anyMatch(notification -> notification.getTitle().contains("a"))
```

# intermediate vs terminal operations
filter() gibi metodlar yeni bir stream objesi döndürür, bu sebeple intermediate olarak nitelendirilir. oysa terminal operation metodları, Stream.forEach gibi, stream değilde, herhangi farklı bir obje döndürür.

intermediate metodlar 2'ye ayrılır:
- stateless

  bir önceki stream'den hiçbir state tutumazlar. örnek: filter and map.

- stateful

  örnek: sorted

# parallel vs serial
Collection sınıfı içinde stream() and parallelStream() metodları vardır. sadece buna göre stream'lerin paralel yürütülüp, yürütülmeyeceğine karar verilir.

örnek:

```java
List number = Arrays.asList(2,3,4,5);
number.parallelStream().forEach(y->System.out.println(y));
```

Paralel olan stream'ler paralel çalışacağı için sıra önemsiz olan kod logic'lerinde kullanılmalıdır. Paralel olanlar daha hızlıdır.

# StreamSupport
Iterable'larda stream dönen metod yok ( iterableInstance.stream() yok ). Bu sebeple özel olarak StreamSupport geliştirildi.

```java
Iterable<String> iterable = Arrays.asList("1", "2", "3", "4", "5");

List<String> result = StreamSupport.stream(iterable.spliterator(), false)
                                          .map(String::toUpperCase)
                                          .collect(Collectors.toList());
```

# java.util.stream.BaseStream
java.util.stream.Stream, BaseStream'den türemiştir. BaseStream ise sadece java.lang.AutoCloseable'dan türemiştir. AutoCloseable sadece "close" metodu içerir. Fakat her stream close metodunu implemente etmek zorunda diildir. I/O işlemi yapan streamler close'u implemente etmelidir.

public interface BaseStream<T, S extends BaseStream<T, S>> metodları:

- Iterator<T> iterator();

  Stream ile dönülecek data'ları java.util.Iterator instance'ına atar ve bu iterator'ı döner.

- Spliterator<T> spliterator();

  java.util.Spliterator, jaava.util.Iterator'a benzer bir yapıdır. iterator gibi çalışıyor, fakat tüm iterasyonu sıra ile yapmak zorunda bırakmıyor. onun yerine parça parça gruplara ayırıp, istersek her parçayı farklı thread'lerde iterate edebilmemizi sağlıyor.

- boolean isParallel();

  kullanılan stream'in paralel olup olamdığının bilgisi döner.

- S sequential();

  Aynı stream'in sıralı olan 5isnatnce'ını döndürür. zaten sıralı bir stream ise, kendisini dönebilir.

- S parallel();

  Aynı stream instance'nın paralele olan instance'ını döndürüyor. eğer zaten partalel steram ise yine kendisini de dönebilir.

- S unordered();

  sequential()'ın tersini yapıyor.

- S onClose(Runnable closeHandler);

  AutoCloseable'ın metodu diildir. Burası close yapıldığında çalıştırılacak callback metodunu parametre alır.
