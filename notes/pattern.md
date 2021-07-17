
############################

############################
# PATTERN
############################

############################

# GOF (or Gang of Four)
1994'te "Design Patterns: Elements of Reusable Object-Oriented Software" isimli kitap Erich Gamma, Richard Helm, Ralph Johnson ve John Vlissides tarafından yazılmıştır. bu kitapta birçok objcet orianted pattern anlatılmaktadır. kitap birçok yazılımcı tarafından bilinir. bu kitabın yazarlarına "Gang of Four" takma adı verilmiştir. işlenen bazı konular:
- genel object orianted felsefesi
- Structural patterns (adapter, bridge, composite, decorater, facade, proxy...)
- Creational patterns (abstract factory, builder, factory method, prototype, singleton...)
- Behavioral patterns (observer...)
- c++ üzerinden örnekler

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Dont Use Exceptions For Flow Control (Anti-Pattern)
Exception kullanımının kodun akışını belirlememesi gerektiğini savunana bir görüştür. Bu durum dil'den dile değişmektedir. yani; bu öneri her dil için geçerli değildir. kaynak: (source-id: 145) 7'inci bölüm (her bölüm çizgi ile ayrılmış).

Örneğin; aşağıdaki gibi for-loop içinde bir döngümüzde kullanmamız önerilmez:

```java
try {
	for (int i = 0; i++){
		array[i]++;
    // Do naything here with "array[i]"
  }
} catch (ArrayIndexOutOfBoundsException e) {
  // exit from for-loop at this point or add any logic here
}
```

kaynak: (source-id: 145) 2'inci bölüm (her bölüm çizgi ile ayrılmış).

Ancak, bizim yazmadığımı herhangi bir kütüphane exception fırlatıyor ise; o zaman elden birşey gelmez ve onu yakalamak gerekir: 

```java
} catch(RedirectException e) {
	response.sendRedirect(e.getURL());
}
```

kaynak: (source-id: 145) 5'inci bölüm (her bölüm çizgi ile ayrılmış).

Aşağıdaki örneklerden birinde excepiton kullanılmış, diğerinde kullanılmamış:

```cs
if (conn.State != ConnectionState.Closed)
{
    conn.Close();
}
```

```cs
try
{
    conn.Close();
}
catch (InvalidOperationException ex)
{
    Console.WriteLine(ex.GetType().FullName);
    Console.WriteLine(ex.Message);
}
```

Yukarıda hangisini kullanmak önerilir? Eğer çoğunlukla excepiton case'ine düşülüyor ise; if bloğu ile kontrol etmek gerekli. Eğer nadir düşülecek bir case ise excepiton kullanmak gerekir. Çünkü eğer nadir karşılaşılıyor ise; if bloğu olmayacağı için hç if-kontrolü yapılmamış olacak. kaynak: (source-id: 148) "Handle common conditions without throwing exceptions" başlığı.

# performans etkileri
Exception kullanmak, performance konusunda bazen avantaj sağlarken bazen dezavantaj sağlayabilir. Bu dilden dile ve kod akışının durumuna göre değişiklik gösterebilir. 

Artık JIT kavramı da Java dünyasına geldiği için, bu durum (performance) birçok faktörden etkileniyor. Burada (kaynak: (source-id: 149)) yazan tüm cevaplarda; java dünyasında; try bloğuna girmenin neredeyse hiçbir maliyeti olmadığı belirtilmiş. Fakat asıl maliyet exception olduğunda ortaya çıktığı belirtilmiş.

Java'daki bu durum şundan kaynaklanıyor: bytecode içerisinde try bloğu yoktur. Kod akışı aynen devam etmektedir. Fakat exception-table olarak isimlendirilen bir tabloda try catch gibi blokların meta bilgileri tutulmaktadır. Dolayısı ile herhangi bir exception olduğunda, JVM, bu tabloyu incelemekte ve buna göre akışı yönetmektedir. İşte maliyet burada ortaya çıkmaktadır. Eğer thread'in başlangıç noktasına kadar olan stack-trace'imiz büyükse (yani içiçe metodlar çağrılmış ise), bu durumda her metod için exception-table JVM tarafından okunup kontrol edilecektir. kaynak: (source-id: 150) "The Non-Heap Exception Table" başlığı. + bu kaynakta bytecode örneği verilmiş. bu örnekteki bytecode'da try-catch olmadığı da örneğin içerisinde yazmaktadır: (source-id: 149) Kingshuk Bandyopadhyay'nin cevabı.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Pattern list by types

Aşağıdaki liste sıra ile anlatılmıştır.

- Structural pattern
  - Private class data pattern
  - Facade pattern
  - Proxy Pattern (or vekil deseni)
  - Delegation Pattern
  - Adapter pattern
  - Composite pattern
  - Bridge pattern
  - Decorator pattern (anlatımı henüz yok)
- Behavioral pattern
  - command pattern
  - Iterator pattern
  - Null object pattern
  - Observer pattern (or Gözlemci deseni)
  - State pattern
  - Specification pattern
  - Template pattern
- Concurrency pattern
  - Thread pool pattern
- Architectural pattern
  - çoğunlukla microservis tabanlı sistemde uygulanabilecek pattern'ler
    - Sidecar pattern (or sidekick pattern or decomposition pattern)
    - database per service pattern
    - Decompose by business capability Context
    - microservice pattern (or mikroservis deseni) vs Monolithic pattern (or monolitik desen)
    - Externalized configuration pattern
    - api gateway pattern
    - api composition pattern
    - Circuit Braker (or devre kesici)
    - CQS (or Command Query Separation) vs CQRS (or Command Query Responsibility Segregation)
    - two-phase commit (or 2PC)
    - saga pattern
    - Transactional outbox pattern
    - event sourcing pattern
    - Circuit Braker pattern (or devre kesici deseni)
    - Service registry pattern
    - Client-side Service Discovery Pattern vs Server-side Service Discovery Pattern
    - Self Registration pattern
    - Blue-Green Deployment Pattern
    - Microservice chassis
  - Domain driven design (or DDD) vs data-centric design (or database-centric design or data-driven design) - [pattern_ddd.md](https://github.com/yusufd89/notes/blob/master/pattern_ddd.md)
  - MVC vs MVP vs MVVM vs Redux vs Flux [pattern_mvc.md](https://github.com/yusufd89/notes/blob/master/pattern_mvc.md)
  - Data Access Object (or DAO) pattern (Bu pattern "Structural" grubu altında da sayılabilir)
  - Repository pattern
  - Front Controller pattern
- Creational pattern
  - Prototype pattern
  - Singleton pattern
  - Builder pattern
  - Factory pattern + Factory method pattern + abstract factory pattern (or Factory of Factory pattern)

"Microservices patterns" kitabının yazarı Chris Richardson, kendisinin katkıda bulunduğu microservices.io/patterns sayfası altında "Deployment patterns" olarak aşağıdakileri ayrı ayrı birer pattern olarak listelemiştir. Aşağıdaki konular bu dökümanda anlatılmamıştır.

- Multiple service instances per host - deploy multiple service instances on a single host
- Service instance per host - deploy each service instance in its own host
- Service instance per VM - deploy each service instance in its VM
- Service instance per Container - deploy each service instance in its container
- Serverless deployment - deploy a service using serverless deployment platform
- Service deployment platform - deploy services using a highly automated deployment platform that provides a service abstraction

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Private class data pattern
bir java sınıfında sınıf değişkenleri tamamen dışarıya kapatılmak istenebilir. bunun için tüm değişkenleri private yapıp setter'larını kaldırmamız gerekecek.
Fakat buda yetmez bu dataların o sınıftan dahi değiştirilmemesini isteyebiliriz. Bunun için tüm data'yı yine sınıf değişkeni olarak; bütün dataları içeren tek bir sınıf yaratabiliriz. Bu oluturduğumuz yeni sınıf consctuctor haricinde setter'a sahip olmamalıdır.

```java
class Math{
  private int kose1;
  private int kose2;

  alanHesapla(){....}
  
  //getters
}
```

Bu yapılması daha iyi olacaktır:

```java
class MathData{
  private int kose1;
  private int kose2;

  MathData(kose1, kose2){...}

  //getters
}

class Math{
  private MathData data;
  alanHesapla(){....} // can call: data.getKose1();
  .....
}
```

Artık Math sınıfımızda data.setKose1(); çağıramayız. Oysa ilk Math sınıfımızda kose1=3; yapabilirdik.

Yani dışarıya kapattığımız yetmezmiş gibi; ilgili sınıfımızda da önlem almış oluyoruz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Facade pattern
facade kelime anlamı: cephe, Bir yapının ön tarafta bulunan bölümü

birden fazla sınıfın işlevini birleştirip çağırmak durumunda kalabiliyoruz. örneğin; getComputer() işlemi kendi içerisinde %90 getKlavye(); getMotherBoard(); gibi işlemleri yapması gerekiyor. Bunları tek tek çağırmak yerine facada sınıfı yaratıp, sadece facada sınıfından yararlanma metodolojisidir.

örnek: Simple Logging Facade for Java (SLF4J). SLF bir interface ile tüm implementasyonların değil, birçok log kütüphanelerinin kullanılabilmesi için arayüz sunmaktadır. burada SLF4J kütüphanesinin init() metodunu çağırdığımızda:
- A log kütüphanesi için 2 adet metod
- B log kütüphanesi için ise 1 metod çağrıyor olabilir.

Patternin tanımında belirttiğimiz gibi; bir metod (init metodu) diğer tüm ihtiyaçlarımızı görecek metodları çağırmaktadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Proxy Pattern (or vekil deseni)

- CommandExecuter --> Interface olsun
- CommandExecuterImpl --> türemiş sınfımız olsun
- CommandExecuterProxy --> türemiş sınfımız olsun

- CommandExecuterProxy sınıfının içinde CommandExecuterImpl otomatik initialize olsun.
- CommandExecuterProxy sınıfının runCommand(String commandStr) metodunu çağırdığımızda bizim için CommandExecuterImpl metodunun runCommand'ını çağırır. fakat ek olarak önce komutu koşturabilicek yetki olup olmadığı kontrol edilir. BUnun gibi birçok kontrol yapılabilir. Benzer şekile otomatik CommandExecuterImpl initialize edilirken ona gerekli parametreleri geçer. 

Proxy pattern'i CommandExecuterImpl 'ın kullanımına aracılık ediyor ve bize kolayklaştırıyor. Daha da spesifik bir örnek verirsek; CommandExecuterProxy yerine CommandExecuterUser yada CommandExecuterAdmin isimli 2 proxy yapabiliriz. Bu proxy'ler CommandExecuterImpl'ı initialize ederken parametrelerini biliyor olucak ve komutu çalıştırmadan doğru yetkilerle kontrol edeceklerdir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Delegation Pattern (or Delegator Pattern)
bazı kaynaklarda "__proxy chains__" olarakta geçmektedir.

proxy pattern'e çok benzer.

Genelde kalıtım yerine, composition tercih edilir. işte bu durumda composition olacak sınıfın metodlarını, sınıfımızın içindeki proxy objesi ile çağırırız. bu gibi durumlarda Delegator pattern kullanılabilir.

proxy ile farkı şudur: Delegator pattern, referan olsuğu sınıfın metodlarını aynen çağırırken, proxy pattern arada loglama, kontrol gibi birçok işlev görebilmesi söz konusudur.

kaynak: (source-id: 152)

```java
class MyClass {

  Delegator d;

  method1(){
    d.method1();
  }

  method2(String a){
    d.method2(String a);
  }
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# adapter pattern

adapter is a bridge between two incompatible interfaces.

örnek;

```
- Reader         (Interface)
  - PpdfReader   (Implementation)
  - DocReader    (Implementation)
  - PhotoReader  (Implementation)
```

Yukarıda Photo, pdf ve doc'tan çok farklı bir media dosyası. örneğin; Reader interfacesi getAllAsText(); metoduna sahip. Fakat bunu photoda nasıl implemente edeceğiz?

Öncelikle getAllText yerine fotonun meta-data bilgilerini text olarak döndüreceğimizi kabul ederek ilerleyelim.

Foto'dan meta-data'ları döndüren sınıfımız olsun:

```
PhotoMetaDataReader   (Interface)
 - getPhotoDate()     (Method)
 - getPhotoId()       (Method)
```
 
Yeni bir adapter sınıfı yaratırız:

```java
class PhotoReaderAdapter {

    PhotoMetaDataReader p;

    getAllMetaData(){

       return p.getPhotoDate() + p.getPhotoId();
    }
}
```
Artık PhotoReaderAdapter'ı PhotoReader içinde kullanabiliriz.

Böylece PhotoReader ile PhotoMetaDataReader'ı PhotoReaderAdapter ile birbirine bağlamış olduk.
Burada adaptee rolünde olan PhotoMetaDataReader interface'sidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# composite pattern

- örnek;

Data clasımız olsun. Folder ve File implementasyonumuz olsun. File sadece tek bir "Data" Objesi barındıracaktır. Oysa Folder, bir Data Listesi barındıracaktır. Bu "Data" listesi içinde file yada folder olabilir.

Şimdi main class'ımızda ;

```java
Folder root = new Folder();
root.add(new Folder());
root.add(anotherSubFolder);
```

yukarıdaki kod akışında içiçe dizinler yaratabiliyoruz. İşte bu tarz bileşik data tutulup ağaç yapısı hazırlabilicek tasarımlara "composite pattern" denir. 

- örnek;

```java
class Employee {

  String name;
  List<Employee> subEmployees;
}
```

YUkarıdaki obje ile tüm şirketin hiyerarşisi bile yaratılabilir. en üstte genel müdür employee'si olacaktır.

- örnek;

AritmeticExpression sınıfı. Bu sınıf büyük bir denklemi barındırıyor. List<Operand> barındırıyor. Her operan yine kendi içinde operand listesi barındırıyor.

1 # ( 2 + ( 3 + 4 ) ) denklemimizi örnek alabilir. bir Operand 1,# ve X'i barındırıyor olacak. X operand'ı ise içinde; 2, + ve Y operandını bulunduracak. Y operandı ise; 3, + 4 ü barındırıyor olucak gibi...

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# bridge pattern

Satış raporlarının çıktısı alan kodlarımız olsun:

```
- Rapor         (Interface)
  - Internet    (Interface)
    - PDF       (Implementation)
    - Doc       (Implementation)
  - Magaza      (Interface)
    - PDF       (Implementation)
    - Doc       (Implementation)
```

Bridge pattern'i diyorki; ilgili sınıftan soyut olan bir yapıyı ayırın. Bizim sistemde soyut olan kavram "format" (pdf, doc) olmasıdır. PDF ve doc'u soyutlaştırmamız gerek.

Sonuçta bu olması isteniyor:


```
- Rapor         (Interface)
  - Internet    (Implementation)
  - Magaza      (Implementation)

- Format      (Interface)
  - PDF       (Implementation)
  - Doc       (Implementation)
```

Artık yeni rapor yaratmak istediğimizde yaratılacak rapor nesnesine Format sınıfını parametre geçeceğiz.

Köprü rolünde olan sınıf Format'tır. FormatBridge diye adlandırabilirdik.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# command pattern
Yapılacak bir işin detaylarını, bu işi tetikleyen taraftan soyutlamak için kullanılan bir pattern'dir. örnek:

```java
class RemoveThingsFromDB implements Runnable {
    public void run() {
        System.out.println("Removing things from DB...");
        // add here many code
    }
}
 
class EditThingsOnDB implements Runnable {
    public void run() {
        System.out.println("Editing values on DB...");
        // add here many code
    }
}

public class MainApp {
    public static void main(String[] args) {
        Thread thread = new Thread(new RemoveThingsFromDB());
        thread.start();
         
        Thread thread1 = new Thread(new EditThingsOnDB());
        thread1.start();
    }
```

Yukarıdaki kod örneğinde; mainm thread'in diğer thread'lerde yapılan işlemlerdne hiç bilgisi yok. Sadece ne yapmak istediğini söylüyor ve işi iligli sınıfın ilgili metodu hallediyor. Böylece işleri biribirinden soyutlamış oluyoruz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Iterator Pattern 
for loop yerine iterator objesi ile dönmemizi sağlayan pattern'dir.

Iteratorler'in avantajı şudur:
- uygulamamızda tüm koleksiyon nesnelerimiz aynı iterator interfacesinden türemiş sınıfları kullanır. bu şekilde bize gelen koleksiyon tipini düşünmeden o koleksiyonda işlem yapabiliriz (döngü kurma gibi).
- koleksiyon sınıfımızdaki iterator objesi bize filtreli dönüşte yapabilir. örnek:

Radyo dinleme cihazımız olsun.

```java
Kanal {
   Frekans;
   Language;
}

class KanalListesi {

   kanalEkle(Kanal);
   kanalSil(Kanal);
   
   iterator(Language);
}
```

Yukarıdaki KanalListesi koleksiyonumuzun döndüreceği iterator'ın next(); metodu bize aldığı Language parametresine göre filtrelenip dönecektir. Zaten iterator'ın next() metodunun implementasyonunu KanalListesi sınıfını yazan yazılımcı yazacaktır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Null Object Pattern
AbstractUser class'ımızı olsun. bundan 2 tane implementasyon olsun. 1 tanesi normal koşullarda yapacağımızı User implementasyonumuz, diğeri ise NullUser implementasyonumuz. NullUser hiç null pointer döndürmesin. örnek: NullUser.getName(); --> "User not available" dönsün. gibi. 

Bir ekran koruyucu yazılımımız olsun. Bu yazılım ekranda toplar gösterecek olsun. Toplar için efect'lerimiz olsun. Efectler biz dizinden yükleniyor olsun. dizinde hiçbir dosya olmadığında NullEffect sınıfımız devreye girecek ve default olarak ekranın efektsiz çalışmasını sağlayacaktır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Observer pattern (or Gözlemci deseni)

Observer tasarım deseni; birbirleri ile bire çok (yani bir nesnenin içinde başka bir nesnenin listesinin bulunması olarak düşünebiliriz) ilişki olan nesneler arasında olay bazlı bir etkileşim olduğu durumları düzenler. Örnek senaryolar:

- Bir e-ticaret sitesinde bir üründeki stok değişiminde o ürünü takip eden üyelere haber verilmesi" 

- facebookta bir paylaşıma yapılan yorumlar için paylaşımcıya ve diğer yorumculara bildirim gitmesi

İlk senaryodan gidelim;

- "Observer (or consumer)" yapısına denk gelen sınıf "Üye" sınıfı olsun. 

- "Observable (or Subject or object)" yapısına denk gelen sınıf "Ürün" sınıfı olsun. 

ürün içinde, üyelerin listesi olsun.

Urun.updateFiyat(int newFiyat) metodunun içinde tum uye listesine email ile fiyatın değiştiğini haber veren işlem yapılmalıdır.

# publish-subscribe vs Observer
publish-subscribe sistemlerde arada event bus (or sistemde adlandırabileceğimiz herhangi bir mekanizma: broker, message broker, event bus) vardır. oysa observer sistemde event bus yoktur. Observer'da, subject direk Observer'ların metodlarını çağırır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# state pattern

Her durum için ayrı nesneler yaratılıp, akışın her duruma göre davranışlarını bu yarattığımız nesnelerde bulundurabiliriz. Bu şekilde if/else gibi durumlardan kısmen kurtulmuş oluruz.

örnek:

```java
WebApp app = new WebApp(); // web app started on desktop browser which was used in a small area
...
app.alert(); //the alert was opened as OS native (big popup alert)
...
app.setState(new FullScreen()); //user now changed the browser screen as fully screen
...
app.alert(); //the alert is a modal now. because user is already focused on screen
...
```
• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Specification pattern
Yazıcağımız kaynakların dışarı açılacak metodlarını protected olabilir. Dolayısı ile herkesin erişmesini istemediğimiz metodlar olabilir. Sadece dışarıya erişime açmak istediğimiz metodları bir interface aracılığı ile açmalıyız. bu açtığımız interface'lere "contract (or şartname)" de deniliyor.

Bu konu "service contract" başlığında daha detaylı anlatılıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Template pattern
template kelime anlamı: şablon

Spring'deki restTemplate gibi *template sınıfıları bu patterni baz almaktadır.

Bir süper class'ta bir iş akışını belirleriz. Bu iş akışı hbirçok farklı implementasyon için çalışır. Eğer isterse implementasyonlar bu akışı değiştirebilir. Fakat büyük resimde ne olacağı bellidir. böylece kod tekrarından kurtulmuş oluruz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Thread pool pattern
İlgili uygulamada thread sayısının merkezi bir modülden limitlenerek sırası ile çalıştırılma patternidir.
Merkezi modülümüz isterse thread'leri önceden işletim sisteminde hazır tutabilir, yada işi biten thread'leri kapatmadan, sıradaki thread'e direk teslim edebilir... Fakat bu detaylar pattern'e ait değildir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Sidecar pattern (or sidekick pattern or decomposition pattern)
Bir uygulama yanında sidecar dediğimiz farklı bir uygulamayı bulundurur. Sidecar, asıl uygulamamızın yapması gerekn bazı işlevleri onun için yerine getirecektir. Bunun avantajını direk örnek üzerinden inceleyelim:

Spring Cloud Eureka (discovery server) client'leri java için yazılmış durumda. Peki cloud'da nodejs microservisimiz nasıl eureka'ya bağlanacak. işte böyle bir durumda sidecar pattern aklımıza gelir.

- Yeni bir microservis yaratırız.
- spring-cloud-netflix-sidecar bağımlılığını ekleriz.
- sidecar projesinin config dosyasına da nodejs'in healt-check url'sini veririr.
- nodejs uygulamamızın bir portundan sürekli olarak healtcheck (spring cloud doc'unda standardı yazıyor) status OK cevabı döneriz.

Proje ayağa kaldırıldığında sidecar sürekli olarak healcheck'e request atacak ve cevap aldığı sürece asıl eureka server'ımıza register olacak. sidecar eurekaya register olması için nodejs'e aracılık etmiş oluyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# database per service pattern
her microservisin kendi database'i olması mimarisidir. temel olarak şu tarz alt çözümlere gidilebilir:

  - Private-tables-per-service – each service owns a set of tables that must only be accessed by that service
  - Schema-per-service – each service has a database schema that’s private to that service
  - Database-server-per-service – each service has it’s own database server.

tablolar arası ilişkilerin nasıl tutulacağı konusu için çözümler aşağıdadır. aşağıdaki listedeki her 2 durum içinde ilişkiler db tarafında tutulduğubda, kolonlarda foreign key olamayacak.

  - 1- ilişki tablosu sadece 1 veritabanında olacak.
  - 2- ilişki tablosu ilgili tüm servislerde tutulacak.

Yukarıda 1'inci durumda bir servis eğer ilişki tablosunu içermiyor ise; her defasında ilişki tablosunu kullanan microservice istek yapacaktır. bu da network yavaşlığına sebep olacaktır.

2inci maddede ise, ilişkiler iligli servislerin veritabanlarında olacağı için 2 dezavantaj var:
  - dublicate veriler oluyor (ilişkiler birçok veritabanında saklanıyor)
  - update ve add işlemleri tüm veritabanlarında güncelleniyor. bu yavaşlık sebebi.

avantajı ise:
  - 1inci çözümde olduğu gibi her ilişki tablosuna erişim gerektiğinde diğer servislere istek yapılmıyor. direk db'den okunuyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Decompose by business capability Context
Sadece CRUD servislerimiz olsun. Örnek order service, user service. bu servisler businnes logic içermesin. onların önüne farklı microservisler koyabiliriz. bu servislerimiz ise daha yüksek seviyeli işler yapsın. businnes logic içersin ve CRUD servislerini kullansın. bu tarz mimarilerde öndeki servislere __capability servis__ denir (terminolojik olarak birçok alternatifi mevcut).

burada CRUD servislerimizde olması beklenen businnes logic'leri decomposition yapmış olduk.

Bunu yapmanın avantajları:
- CRUD ile bussines logic'leri ayırmak. daha basit yapı oluşturma.
- "database per service pattern" uygulandığında ilişki tabloları için her servis diğerine gitmesi gerekecek. oysa önlerinde capability servis olsa, herşeyi o yönetse ilişki yönetimini tek bir noktadan daha kolay yapabiliriz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# microservice pattern (or mikroservis deseni) vs Monolithic pattern (or monolitik desen)

microservice'lerde bağımlılıkların neredeyse hiç olmaması (veya minimum olması) gerekiyor. bu da ortak kod bloklarının microservisler arasında hiç olmamasını gerektiriyor. genelde kullanılan ortak kod bloklarını gruplandırarak incelersek;

- database model
  
  her microservis kendi db'sine gitmesi gerekir. örneğin user ve adres modellerimiz olsun. her servis kendi db'sinde verileri ve ilişkileri tutmalıdır. ilikşikler arası bağlantı kurmak gerekirse, diğer servise runtime sırasında sorgu atması gerekecektir.

  bu konu "database per service pattern" başlığında daha detaylı anlatılıyor.

- utility kodları

  bir borsa uygulaması düşünelim. para çevrimi aşaması neredeyse her servis tarafından kullnılır. klasik mimarilerde olsa common sınıfa utility olarak yazılır ve herkes bu kod parçasına depend olur. oysa microservislerde 'money-converter' isimli bir servisimiz olur ve herkes runtime sırasında bu servise sorgu atarak para çevrimi yapması beklenir.

- 3party dependencies

  tabiki apache-common-utils gibi servisleri her projemizde kullanabiliriz.

- config strings

  config'ler farklı bir config micro-servisinden okunmalıdır.

- common maven configs + common maven dependencies + common codes

  runtime sırasında olmayan konfigler pom.xml gibi config dosyalarında tanımlanır. bunları standart tutmak istiyorsak, template'ler haline getirip, bu template'leri hızlıca kopyalanabilir şekilde ayarlayıp, her projeye ayrı ayrı atabiliriz. bu konu "Microservice chassis" patterni başlığında anlatılıyor.

  bu son madde için bazı developer'lar common dependency yapılabilir olduğunu düşünüyor. bu konuda farklı görüşler var. burada görüş ayrılığı olmasının sebebi şu: businnes logic olan kısımlarda bağımlılık olmazsa genelde sorun olmayacağı düşünülür. çünkü businnes logic olmayan kodlar teknoloji için gerekli utility sınıflarıdır. aynı apache-commons-util'de olduğu gibi. dolayısı ile bizde kendi şirketimiz içinde bir utility yazmış sayılıyoruz.

  shared lib olabilmesi için örnek: (source-id: 153) "Exceptions" başlığı

  Bazı developer'lar ise kod dublikasyonu olsa bile common lib yapılmaması görüşünde. kaynak: (source-id: 154) "Do you share anything?" başlığı.

  Bu konu burada da cevaplanmış: (source-id: 155)

  Fakat genel olarak; teknik ortak kodların olmasında pek sakınca görülmezken, businnes logic olan kodların kesinlikle ortak olmaması öneriliyor.

# avantajlar

- bir projede bir kütüphane değiştirildiğinde diğer kütüphanelerin zarar görmediğinden emin olabilir. örneğin; springmvc kullanırken aynı projede, spring'in  bir modülünü ekleyeceğiz. yeni kütüphaneyi eklerken springmvc dependency'leri ile çakışmıyor görünse de, her zaman beklendiği gibi olmayabiliyor. bu durumun önüne geçilmiş oluyor. docker gibi her proje/yazılım birbirinden bağımsız olmuş oluyor.

- her proje farklı dillerde yazılabiliyor.

- projelerde aynı kütüphanenin farklı sürümleri kullanılabiliyor

- projeler çok ufak ve fazla parçalara bölünmüş olacağından; deploymentlar daha ufak parçalar şeklinde ve daha az riskli şekilde yapılabilecektir. yani; tüm paketi birden çıkmak zorunda kalmıyoruz. continuous delivery'yi kolaylaştırıyor.

- projeler çok ufak ve fazla parçalara bölünmüş olacağından; doğası gereği modülerliği arttırmaya yöneltiyor.

- bir modülde sorun çıkınca tüm sistem çökmemiş oluyor. sadece o modül kullanılamıyor.

- update işlemleri için tüm sistemi durdurmaya gerek yok.

- localde development için tüm sistemi açmaya gerek yok.

- operasyonler işlerde startup süreçleri hızlanır.

- devre dışı bırakılacak modüller için sistemi kapatmaya gerek yok. sadece o servisleri kapatmak yeterli.

# dezavantajlar

- her projenin farklı databasesi olması, özel sorgular ve atomic işlemler için zorluk çıkarabiliyor (transactional işlemlerdeki zorluklar)

- Complex communication:
  - network ağı sürekli haberleşme ihityacı arttırığında yoruluyor
  - hangi businnes akışında, hangi servisin nereye gittiğini bulmak ve bir servisteki değişikliğin, diğer hangi serviste etki yaratabileceği ancak e2e testlerinde görülebiliyor.

- mikroservis, monolitike göre çok sonradan çıkan bir pattern. dolayısı ile şu anda piyasada olan birçok uygulama monolitik. bunları mikroservis yapısına geçirmek çok zorlu bir süreç gerektirebiliyor.

- Infrastructure requirements. tüm servisleri (özellikle farklı DC'ler var ise) manuel yönetmek çok zor. bunun için çoğu proje kubernetes/openshfit/istio gibi çözümlere para vermek veya depend olmak zorunda kalıyor. Aynı zamanda bunları yönetecek bilgi sahibi birilerine ihtiyaç duyuluyor.

- daha tecrübeli yazılımcı ihtiyacı doğuruyor:
  - dependency olmaması gerektiğinden, tecrübeli yazılımcılar olmazsa, dublicate kodların sonucunda code smell'ler oluşabiliyor.
  - genel olarak bakıldığında; daha fazla infrastructure requirement bilgisi gerektiriyor. en basitinden lokal ortamda bağımsız development yapmak için bile kuberntes kaldırmak gerekebiliyor.

- iyi optimize edilmezse, bazı durumlarda sistem requirement'leri (RAM gibi...) daha fazla harcayabiliyor (özellikle ufak projelerde dezavantaj yaratıyor).

# cloud native architecture
bir mimaridir. "native", doğal anlamına gelir. 'cloud native'den kasıt; cloud yapısına en uygun olandır.

spring'in cloud native'i karşılayan modülleri vardır. "Spring cloud netflix" ismi ile geçer çünkü tüm implementasyonlar netfix'in spring'den bağımsız geliştirdiği uygulamaları kullanabilmek için yapılmıştır.

# Enterprise application integration
monolitik uygulamalar'ın birbirleri ile haberleşebilmesi için gerekli entegrasyonlardır. Tam olarak neleri kavradığı belli olmayan (resmi şekilde yazılı olmayan) fakat piyasada sıkça kullanılan bir terimdir.

destekleyen bazı framework'ler:
- Spring Integration
- Apache Camel
- Red Hat Fuse
- Mule ESB
- Guaraná DSL 

Gregor Hohpe ve Bobby Woolf, Enterprise application integration için gerekli 65 pattern'i "Enterprise Integration Patterns" isimli kitapta anlatmıştır. Bu kitaptaki patternleri burada bulabiliriz: (source-id: 156) enterpriseintegrationpatterns.com'a apache camel'ın resmi sitesinden referans verilmiştir. kaynak: (source-id: 157) 1st sentence.

Bu kitaptaki bazı patternler:
- File Transfer
- Shared Database
- Remote Procedure Invocation
- Point-to-Point Channel
- Publish-Subscribe Channel
- Message Bus
- Synchronous (Web Services)

# service bus (or enterprise service bus or ESB)
ESB birçok monolitik uygulamanın birbiri ile haberleşebilmesi ve entegrasyonunu sağlamak için merkezde olan bir component'tir. ESB'ler ek olarak, mesaj formatını değiştirme, filtreleme, yönlendirme, bazı businnes logic içerme gibi özellikleri de vardır.

"Enterprise application integration" içinde önerilen mimarilerden biridir.

ESB'nin dezavantajları:
- Adding additional step/call in the service flow and add a slight delay to the response time. 
- Additional cost to setup ESB servers, VPNs, and other infrastructure
- All services are routed through a single place; it will have a single point of failure. 
- Not having too much options to scale up a single service in ESB infrastructure. 

# ESB vs SOA vs microservice vs Monolithic
karşılaştırma yapılabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Externalized configuration
config server pattern'idir. servislerin tek bir servisten tüm configleri çekebilmesidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# api gateway
bir sunucu yazılımdır. edge server gibi çalışır. özellikleri:

- Farklı protokoller arası dönüşüm. örnek: SOAP->REST, TCP->SOAP
- darboğaz (throttling) yönetimi. her user'dan gelen istekleri sınırlandırmak. yani; belli zamana dilimlerinde, bazı isteklere limit getirebilmek.
- kimlik doğrulama
- api versiyonlama
- api grubu devreye alım/kapatma/açma
- Loglama, izleme, bildirim
- Servis birleştirme (service composition). birden fazla iç servisi tek bir servis olarak dışarıya açabilme.
- caching

piyasadaki bazı api gateway'ler: tyk, Kong

# kong
kong yazılımı başladığında config'leri 3 farklı yerde okuyabilir:
- bir yml config dosyasından
- özel bir port üzerinden http istekleri ile config'ler belirtilebilir. her ayar ayrı ayrı da yollanabilirken, tek bir seferde tüm config http api isteği ile de atılabilir. kong runtime sırasında kendini güncelleyebiliyor.
- config'leri database'den okuyor.

kong açıldığında default olarak bu port'lardan hizmet vermeye başlar:

- :8000 listens for incoming HTTP traffic from your clients, and forwards it to your upstream services.
- :8443 same of 8000 but SSLL enabled
- :8001 admin api
- :8444 admin api with SSL

örnek config dosyası:

```yml
_format_version: "1.1"

services:
- name: my-service
  url: https://example.com # servisimizin hizmet verdiği url
  plugins:
  - name: key-auth # bu servise istek geldiğinde devreye girecek (araya girecek) eklentiler
  routes:
  - name: my-route # sadece routing'in ID'si.
    paths:
    - /my-service1 # artık http://kong-host:8080/my-service1 'e gelen istekler https://example.com 'a yönlendirilecektir.
```

Kong'da eklentiler lua ile yazılmaktadır. eklenti altyapısı oldukça basit. Servlet filter'ı yazar gibi request ve respons'u alıp manipüle edip bir sonraki eklentiye yollabiliyoruz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# API Composition
api gateway uygulamaları bunu bizim için yapabilir. edge proxy diye adlandırılan bu sunucular api'lerimizi dışarıdan erişime açarken tek bir endpoint'ten açar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# CQS (or Command Query Separation) vs CQRS (or Command Query Responsibility Segregation)
Segregation kelime anlamı: ayırma

ikisi çok benzerdir fakat farklı patternlerdir.

2 pattern de metodları iki farklı gruba alınmasını önerir:

- Commands: Objenin veya sistemin durumunu değiştirir. Void dönüş yapar.

  'command' yerine modifier veya 'mutator' terimleri de kullanılır. kaynak: (source-id: 158)

- Queries: Sadece sonucu geriye döner herhangi bir objenin veya sistemin durumunu değiştirmez.

Bir command metodu (eğer dönüş yapmasının yan etkisi olmayacaksa), dönüş yapabilir. fakat bu pek tercih edilen bir yöntem olmamalıdır.

CQS daha çok mikro seviyede, CQRS  ise makro seviyede sistemi ele alan pattern'lerdir. CQS büyük resimden bakıldığında sistemdeki herhangi bir fonksiyonun ya query yada read işlemi yapmasını önerir. kaynak: (source-id: 158)

oysa CQRS (büyük resimden bakarak) bunların da ayrılmasını önerir:
- fonksiyonlara yollanan ve response alınan modeller/objeler
- microservislerin sadece query veya command olarak ayrılması
- sadece fonksiyon seviyesinde değil, sınıflar bazında ayrılması (yani; bir sınıftaki tüm metodlar ya query yapacak yada command yapacak)

kaynak: (source-id: 160) Luke Puplett'in cevabında açıklama mevcut. Mesajın altında Greg Young cevap yazmış fakat Greg web projelerinde kullanımı hakkında yorum düşmüş.

CQRS ilk "Greg Young" tarafından ortaya atılmıştır.

## query ve command'lar için DB modellerinin ayrılması
DB modelleri ayrılmaz ise classic CRUD işlemleri yapan sistemin metodlarını ayırmış gibi oluruz. Bu durumda sadece command servislerimizi scale ettiğimizi düşünelim. DB server instance sayımız aynı olacağı için bunun faydasını görmeyeceğiz. Çünkü darboğaz olarak DB karşımıza çıkacaktır. Fakat eğer command ve query'lerimiz ayrı modeller olursa, ayrı DB'lere kaydedebiliriz. Hepsine ayrı çözüm uygulayabiliriz. örneğin; sadece query microservislerimizi scale ettikten sonra, sadece query yapacağımız DB instnce'larınıda scale edebiliriz. Oysa tersi durumda; tüm sistemi scale etmemiz gerekecekti.

CQRS bir sistemde kesinlikle query ve read modelleri ayrı olacak diye bir kesinlik yotkur. kaynak: (source-id: 161) 9uncu paragraf.

## View Models (or Projections or Query Models)
Query fonksiyonlarımız data okur (veritabanından). bu data'lar yansıtılmak için kullanılan datalar olduğu için, CQRS pattern'i dökümanlarında bu şekilde isimlendirilmiştir.

Bu patternin faydaları:
- CQRS yapıldığında "event sourcing"'de kolaylaşacaktır. çünkü sadece "Commands" servisimize gelen istekleri loglamamız yeterli olacaktır.
- Bazı servislerimiz sadece database'ye read yetkisi olduğundan o servislerimizde güvenliği arttırmış oluruz. (secure by design)
- Sistemimizi micro servislere bölüştürmemiz kolaylaşacaktır.
- Read only query metodlarımız, yazma işlemi yapan metodlarla aynı sınıflarda olmayacağı için büyük DAO'lar karşımıza çıkmayacak. Çünkü command modeli ile view model'leri aynı olmak zorunda diil.
- Database'yi değiştiren servislerin hangileri olduğunu bildiğimizden hata tespiti kolaylaşabilir.
- read ve write yapan DB'ler aynı olmak zorunda diil. Zira write yapıldıktan sonra async bir thread'de de farklı bir DB'ye raporlama için (query servislerinin yararlanması için) kayıt atılabilir. Dolayısı ile; query ve command'lerin kullandıkları db'ler farklı. bununda sonucunda; farklı db çözümleri sunabiliriz. örneğin; kayıt command'ler kayıt atarken mongdo kullanıp, raporları okurken oracle kullanmalarını performance açısından verimlilik sağlayacak ise bu şekilde kullanılmasına olanak sağlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# two-phase commit (or 2PC)

database/network sistemlerinde transaction işlemi yapacak yazılım karşıya önce "prepare for commit" mesajı iletir. eğer OK dönüşünü alırsa "commit" mesajını, her servise ayrı ayrı gönderir. Bu yaklaşım genelde uzakta birden fazla birbirinden bağımsız veritabanlarında işlem çalıştırılacağı zaman yapılır. böylece atomic işlem daha garantiye alınmış olunur.

2PC'de yazılım, diğer servise yada veritabanı servisine "prepare for commit" mesjaını atması ve dönüşünü alması fazına __voting phase__ denir.

Klasik sistemlerde ise direk olarak ilk işlemde "commit" mesajını gönderilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# saga pattern
türkçe kelime anlamı: destan

Saga pattern önyüzde de kullanılan bir pattern'dir. örnek redux-saga; saga'larımızın yönetimini sağlar.

2PC'ye alternatiftir. 2PC senkron bir çözümdür. saga asenkron ve reaktiftir. saga'nın asenkron olabilmesi için, tüm servislerin ortak bir event bus'a bağlı olmaları gerekir. bu şekilde saga, global yürüyen transaction sürecinden haberdar olabileceklerdir. kaynak: (source-id: 162) "saga pattern" başlığındaki ilk paragraf.

2PC'deki gibi birçok dağıtık servisimiz olsun. birçok servisimiz kendi bağımsız veritabanına kayıt/güncelleme işlemi yapıyor olsun. ortak bir event bus ile birbirleri arasında haberleşebiliyor olsun. son kullanıcı global bir transaction işlemini tetiklesin. transaction'ın ilk adımı (yani ilk event) event bus'a yollansın. bu event'i ilgili servis kendine çekecek ve işletmeye başlayacak. ilgili event'ler tamamlandıkça diğer event'lerde çağrılacak.

peki hata olursa ne olacak? işlemler geri alınacak. işte 2PC ile fark burada. saga'da işlemin sonucu, isteği yapan service, isteği gerçekleştiren servis tarafından döndürülür. isteği yapan servis, businnes logic'e göre tekrar aynı servise geri alma işlemini yollayacaktır. 2PC'de geri alma işlemi veritabanına hiç yazmamaktır, oysa saga'da geri alma işlemi güncelleme yada (event sourcing kullanılıyor ise) yeni bir event state'i oluşturmak olacaktır. kaynak: (source-id: 162) "Two-phase commit (2pc) pattern" balığında ikinci resimde görülmektedir ki, bir işlem abort edildiğinde, ilgili servise verilerin veritabanına kayıt edilmemesi isteği yollanmakta. Diğer kaynak: (source-id: 164) "All transactions in the sequence complete successfully or compensating transactions are ran to amend a partial execution." yani; compensating (telafi) transaction'ları yine sequence içerisinde tanımlanır.

Saga ile işletilen transaction büyük resme bakıldığında "__long-lived transaction (or LLT or long-running transaction)__" olarak kabul edilir. çünkü logic olarak bakıldığında atomik birçok işlem başka servislere yaptırılır. Bu durumda birçok ufak işlemleri birbiri ardına çağıran servis uzun süreli bir işlem olacaktır. kaynak: (source-id: 165) "Long-running business activity" başlığı. Diğer kaynak: 'saga' teriminin ilk ortaya atıldığı belge: (source-id: 166)

saga'nın debug'ı, 2PC'e göre daha zordur. kaynak: (source-id: 162) "saga pattern" başlığındaki ilk paragraf. "Disadvantages of the Saga pattern" başlığı.

benzer şekilde saga'nın reactif olması da bir avantajdır. reactif olmasından kasıt şu: tüm event'lerin çağrılıp daha sonra thread'in kapatılması ve callback'in çağrılması yeteneği. 2PC'de işlemler bitene kadar thread'imiz açıkken, saga'da işlemler çağrılıp thread sonlanabilir. event'ler bittiğinde, bir callback metod tetikletebiliriz. 

2PC'de bir transaction sadece bir servisin kendi içinde (seviyesinde) değil, tüm servisler (sistem) seviyesinde kullanılır. dolayısı ile transaction'ın başladığı andan, bittiği ana kadar veritabanında bazı değerler kilitli kalacaktır. bu durum saga'da değildir. çünkü saga'da; 'transaction' sadece servislerin kendi içlerinde(seviyelerinde) gerçekleşecektir.

2PC'de kaynakların (örnek veritabanı) kilitlenmesi, 2PC'nin reactif manifestosuna uymamadığını gösterir. kaynak: (source-id: 168) "The Saga Pattern in a Reactive Microservices Environment", authors: "Martin Stefanko", "Ondrej Chaloupka", "Bruno Rossi", title: "INTRODUCTION" başlığında ikinci paragrafın ortasında.

transaction yönetimleri saga ile 2 farklı şekilde yönetilebilir (implemente edilebilir):

- __Choreography (or tr:Koreografi)__

  bazı kaynaklarda "event" yöntemi olarak adlandırılıyor. fakat bu çok doğru diil.
  
  Koreografi kelime anlamı: Bir dans gösterisini oluşturan adım, figür ve anlatımların bütünü.

  her event diğer event'leri tetiklemesi için event bus'a mesaj gönderir. dolayısı ile tüm sistem merkezi bir noktadan yönetilmez. örnek: bir servis tetikledi, o servis diğer servisleri de tetikleyebilir. yani bir orchestrator yoktur. kaynak: (source-id: 170) "Choreography-Based Saga" başlığındaki ilk paragraf.

- __Orchestration__

  bazı kaynaklarda "command" yöntemi olarak adlandırılıyor. fakat bu çok doğru diil.

  merkezi bir yerden tüm event'ler çağrılır. çağrılan servisler diğer başka servisleri tetiklememelidir.
  
  Orchestration biraz daha çok 2PC'e benzemektedir.

(source-id: 171) sayfasında event driven architecture'ın deprecated ve saga ile replace olduğu yazmaktadır. bunun sebebi şudur:

her event driven architecture saga gibi reversable işlemler zorundadır, aksi durumda event'ler event'leri tetikleyemez. (işlemler reversable olmak zorunda olamayan durumlar teorikte tabi olabilir, fakat pratikte neredeyse hiç mümkün diildir)

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Transactional outbox pattern
bir servis atomic olarak hem DB'ye kayıt hemde message event'i atmak isteyebilir. Bu işlemlerin atomic olduğunu garanti edebilmek için outbox pattern kullanılır. İligli servis DB işlemlerini yapar ve aynı DB-transaction'ında DB'ye event tablosuna da yazar (bu tabloya "Outbox table" denir). DB'ye yazıldıktan sonra, DB'den sürekli olarak kafka veya bağımsız bir servis event kayıtlarını okur ve işletmeye başlar. Yani direk olarak kafka'ya diil, arada DB vardır.

2 şekilde implemente edilebilir:

- # Polling publisher pattern
  Bağımsız bir service (scheduled job) sürekli olarak outbox table'ı okur. Butadan sonra ilgili event'i kafka'ya fırlatır.

- # Transactional Log Tailing
  DB seviyesinde transaction-log'lardaki değişiklikler takip edilir. Her değişiklikle kafka'ya direk DB tarafından kayıt atılır.

  Bu patterni uygulayan yazılımlara "__Change data capture (or CDC)__" deniliyor. örnek sistemler: Debezium, Kafka Connect (with a connector).

Outbox pattern, "dual write" problemine bir çözüm olabilir. "dual write"; hem db hem kafka'ya atomik yazmamız gereken fakat yazamadığımzı durumlarda (hata aldığımzıdan ötürü) görülebilen bir hatadır. tekrar aynı flow'lar, aynı request-data'sı ile çağrıldığında işlem yarım kaldığı için, sistemin tekrar benzeri kayıtları atması durumunda "dual write" oluşur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# event sourcing pattern
order tablosundan gidelim. order'ın tamamlanması için birçok aşama vardır. işleme alınma, ödeme alınma, kargoya verilme gibi... bunların her biri event'tir bu event'ler "event store" da tutulmalı.

böylece;
- order'ın son haline event'leri takip ederek bile ulaşabiliriz.

  not: order'ın son halini sadece query'lerimiz (CQRS pattern'indeki query'lerimiz) için bir tabloda tutarız. fakat her event sonunda bu order tablomuzu güncellemeyiz. sadece tüm event'ler tamamlandığında order tablomuzu güncelleriz.

- event-driven architecture sağlar (reactive sistemler için ideal bir yapı)

- her event ne yapacağına kendi karar verecektir. bu da daha modüler/mikro servis mimarisine geçişimizi uygun kılacaktır.

# isimlendirme
event isimler geçmiş zaman olmalı ve fiil içermelidir. uygulamanın hangi durumda olduğunu net bir şekilde açıklamalıdır. örnekler: 

| Badly named     | Well named      |
|-----------------|-----------------|
| AccountInserted | AccountCreated  |
| AccountUpdated  | FeeCharged      |
| AccountUpdated  | MoneyWithdrawn  |
| AccountUpdated  | AccountCredited |
| AccountDeleted  | AccountClosed   |

# Event storming
domain expertlerin ve devleoper'ların bir araya gelerek yaotığı toplantıdır. bu toplandıda event'lerin ne olduğuna karar verilir.

# domain events vs event-sourcing

domain event'leri microservislerimiz arasındaki haberleşmede kullanılan event'ler olarak düşünülebilir. event sourcing ise her microservisin kendi içinde tuttuğu event'lerdir. bu 2 event'ler ayrı ayrı tablolarda tutulması önerilir. böylece her node bağımsızca test edilebilir ve geliştirilebilir olacaktır.

domain event'lere örnekler:

- A user has registered
- An order has been received
- The payment deadline has expired

Domain event'leri, event sourcing event'lerine göre daha yüksek seviyelidir. Domain expertleri tarafından anlaşılırlar. Bu sebeple teknik olmamalıdırlar. Oysa evet sorucing eventleri daha alt seviyeli ve yazılım teknik elemanları tarafından anlaşılabilirler.

bu durumu bu linkteki: (source-id: 172) "Events from Event Sourcing ≠ Domain Events" başlığındaki bu resim iyi açıklamaktadır: (source-id: 173)

Martin'in bloğunda bu geçmektedir: (source-id: 174) "Event Sourcing ensures that all changes to application state are stored as a sequence of events." Dolayısı ile her event sourcing işlemi application'ın state'inde değişiklik yapmaktadır. Her değişiklik sonrası state veritabanında saklanmalıdır.

# snapshots
event'lerin sayısı çok artabilir ve bir command birçok event çalıştırabilir. dolayısı ile, bir her event son durumu (state'i) okumak için sürekli ilk event'in log'undan son event'in loguna kadar okuyup, hesaplama yapması gerekebilir. örneğin; aynı kullanıcı toplu transaction işlemleri üstüste yapıyor. her event; yani transaction öncesi bakiyede para kalıp kalmadığını kontrol edeceğiz. tüm eventlerin ne kadar harcadğını bulmak zorundayız. bunu yapmak yerine 10 adet işle sonrası yeni bir snapshot yaratabiliriz. bu snapshot'ta soon durumun özeti olabilir. bu snapshotları event tablosunda da tutabiliriz yada farklı bir tabloda sadece snapshot'ları tutabiliriz.

her snapshot'un event tablosunda tutulduğu bir örnek: (source-id: 175)

snapshot'ların ne aralıklarda alınacağı, sistemin mimarisi, uygulamanın domaini ve performans ölçekleri gibi birçok parametreye bağlıdır. snapshot almak; hem maliyetli hemde kod logici ve karmaşıklığı getrdiği unutulmamalıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Circuit Braker pattern (or devre kesici deseni)
başka başlıkta anlatılıyor (Hystrix ile birlikte anlatılıyor).

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Service registry
"discovery server" konusu altında (başka başlıkta) anlatılıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Client-side Service Discovery Pattern vs Server-side Service Discovery Pattern
her iki pattern'de de, service discovery'ye her node kendi ip'sini bildiriyor.

Client-side pattern'inde her node, service discovery'ye erişerek, diğer node'lara gideceği ip adreslerini alır.

Server-side pattern'de ise her node direk olarak sistemdeki "load balancer"'a istek yaparak gitmek istediği servise erişir. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Self Registration pattern
her node'un kendini service regisrty'ye kaydetmesi gerekmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Blue-Green Deployment Pattern
tüm mikroservisleri durdurup yeni sürüm çıkmak ve hata olma durumunda geri alınmasını beklemek çok zaman alabilir. bunun önüne geçmek için bir ortamda daha yeni sürüm sistem ayağa kaldırılır. eski sistem hala ayaktadır. yeni sistem sadece tek bir yönlendirme yapılarak canlıya alınmış olur. bu yönteme Blue-Green Deployment denir.

yönlendirme yapılmadan önce yeni ortamda happy path testler koşulması önerilir.

"green"; o anda "production" ortamını, "blue" ise "staging" ortamını ifade etmek için kullanılan renklerdir.

Netflix bu renkleri red/black olarak kullanıyor. kaynak: (source-id: 176) title: "Blue/Green Deployment".

# canary releasing (or canary deployment)
release kelime anlamı: 1.serbest bırakmak 2. gösterime sokmak/yayına sunmak

"canary" terimi yazılım dünyasında "early version of software" anlamında kullanılıyor. bunun hikayesi; kömür madencilerinin önceden ortam havasından hastalanmalarını engellemek için kanarya kuşunu kullanmaları hikayesi olan 'canary in the coal mine'dan geliyor.

canary releasing bu tekniğinde; hem yeni, hemde eski ortam ayağa kaldırılır. canlı'nın trafiği azar azar yeni ortama açılır. burada monitoring mekanizlamalarımızın çok iyi şekilde tasarlanmış olmalıdır. çıkacak hata oranlarının eskisi ile karşılıştırılması ile yenisinin trafiği yavaş yavaş arttırılır.

# Rolling release (or rolling update or rolling deployment)
büyük paketler çıkarak güncellemek yerine, ufak ufak güncellemeler çıkılarak gerçekleştirilen deployment'lardır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Microservice chassis
chasis türkçe karşılığı: şasi (Motorlu kara taşıtlarının iskelet bölümü)

her yeni mikroservis oluşturulduğunda bir framework'ten yararlanıp, cross-cutting concern'lerin (loggining, security...) tekrar tekrar yazılmaması ve bununla zaman kaybedilmemesi gerekmektedir. örnek spring boot-starter bunun için ideal bir örnektir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# data access object (or DAO) pattern
örneğin Employee sınıfı modelimiz olsun. bunun erişimi için gerekli aşağıdaki sınıfları bir EmployeeDAO isimli sınıfına koyabiliriz:

```java
List<Employee> findById();

List<Employee> findByName();

boolean insertEmployee(Employee employee);

boolean updateEmployee(Employee employee);
```

Bazıları pattern olmadığını, sadece "seperate of logic" temeline uyduğunu belirtiyor. Bazıları ise "Structural" pattern altında olduğunu belirtmektedir.

# repository pattern
DAO sadece persistence odaklıdır ve persistence işlemlerinin ayrılmasını sağlar. "repository" ise ona çok benzerdir fakat farklı kavramlardır.

Repository, sadece aggregate root'ları yönetmek için kullanılırken, DAO direk DB objeleri manipüle eder.

Repository, "collection of objects" olarak düşünülmelidir. Yani bir collection (liste) var ve biz bu collection'a ekleme çıkarma, o collection'da arama (query) gibi işlemler yapıyoruz. Aynı arrayList'in metodlarında yaptığımız gibi. collection tek tipte bilgi store ettiğinden, repository tek tip model üzerine odaklanır, örnek: UserRepository, OrderRepository gibi...

Repository; Eric Evans'ın DDD kitabında anlatılıyor. kaynak: "Domain-Driven Design: Tackling Complexity in the Heart of Software", 2013, page 106.

Her aggregate veya aggregate root için sadece 1 repository class'ı kullanmamız önerilir. kaynak: (source-id: 178) "Define one repository per aggregate" başlığı, 1inci cümle. İşin aslına bakıldığında; bir aggregate altındaki tüm entity'ler aggregate root'lar tarafından update edilmektedir. Yani aggregate için yazılan repository aslında aggregate root için yazılmış oluyor (aynı kapıya çıkıyor). Aggregate altındaki diğer entity'ler için ayrı repository yazılmamalı. Bu durum tüm aggregate'in consistency'si için önemli.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Front controller pattern
Spring MVC'deki dispatcher-servlet bir Front controller örneğidir. tüm request'ler buradan geçer. Bu şekilde ortak olan concern'ler (security, internationalization, and providing particular views for certain user...) burada halledilir.

"Martin Fowler", "Patterns of Enterprise Application Architecture" isimli kitabında bu pattern'den bahsetmiştir. kaynak: (source-id: 179)

Burada da detaylı şekilde anlatılmaktadır: (source-id: 180)

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# prototype pattern
Prototip deseni belirli nesnelerin kopyasını oluşturarak daha sonra yapılacak işlemler için, oluşturulan kopyanın kullanılmasını sağlayan yaratımsal desendir.

```java
User user2 = user1.clone();
user2.setName("mehmet");
```

Örneğin biyolojik bir hücre kendini iki parçaya bölüyor ve aynı hücreden iki tane oluyor.

Bazı durumlarda new ile obje yaratmak, her değeri tek tek set edileceğinden çok maliyetli olabiliyor. Bu gibi durumlarda tercih edilebilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# singleton pattern
bir objeyi, tüm uygulamada aynı instance'ı kullandırma yöntemidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# builder pattern

```java
User myUser = User.UserBuilder("ahmet", "agaogli")

                  .age(30)

                  .phone("1234567")

                  .address("Fake address 1234")

                  .build();
```

avantajlar:
- okunaklılığı arttırıyor. bir constuctor'da 10 tane parametre olursa, hangi parametre nedir anlaşılmaz.
- constuctor'lara tüm parametreleri vermek istemeyiz. null göndermek yerine bu yapı tercih edilir. 10 adet alabilen bir constuctor için tüm kombinasyonları hazırlamak maliyetli olacaktır ve kod kalabalığı yaratacaktır.

__Chaining Methods (or Cascading or named parameter idiom)__ bir metodun kendi instance'ını sonda döndürmesi durumudur. böylece zincirleme metodları üstüste çağırabiliriz. "chaining" sadece builder pattern'inden kullanılmaz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# factory pattern (or simple factory pattern)
tek bir metod ile; new MyClass(param1, param2...) gibi bir yapıya ihtiyaç duymadan yeni sınfıları türetme yöntemidir. örneğin; sadece getMyClass(param1, param2...) yazıp aynı ihtiyacı giderebiliriz.

Bu pattern'de bir factory sınıfı vardır ve bu sınıfın içinde factory metodları vardır. factory metodlar dışında public metodlar olmamalıdır.

# Factory Method pattern
"factory pattern" ile aynıdır. tek farkı abstract bir sınıf döndürmesidir.

```java
interface Interviewer
{
    askQuestions();
}

class Developer implements Interviewer
{
    askQuestions()
    {
        print('hey developer!');
    }
}

class Manager implements Interviewer
{
    askQuestions()
    {
        print('hey Manager!');
    }
}

abstract class HiringManager
{
    // Factory method
    abstract Interviewer makeInterviewer();

    doInterview()
    {
        Interviewer interviewer = this.makeInterviewer();
        interviewer.askQuestions();
    }
}
```

Now "HiringManager" should be implemented like "DevelopmentManager", "MarketingManager"...

# abstract factory pattern (or Factory of Factory pattern)
2 farklı implementasyon/kullanım mevcut:

1- Burada factory dönen metod bize factory tarafından sunuluyor:

```java
public interface Shape {
   void draw();
}

public class RoundedRectangle implements Shape {
   @Override
   public void draw() {
      System.out.println("Inside RoundedRectangle::draw() method.");
   }
}

public class RoundedSquare implements Shape {
   @Override
   public void draw() {
      System.out.println("Inside RoundedSquare::draw() method.");
   }
}

public class Rectangle implements Shape {
   @Override
   public void draw() {
      System.out.println("Inside Rectangle::draw() method.");
   }
}

public abstract class AbstractFactory {
   abstract Shape getShape(String shapeType) ;
}

public class ShapeFactory extends AbstractFactory {
   @Override
   public Shape getShape(String shapeType){
      if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new Rectangle();
      }else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new Square();
      }	 
      return null;
   }
}

public class RoundedShapeFactory extends AbstractFactory {
   @Override
   public Shape getShape(String shapeType){    
      if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new RoundedRectangle();
      }else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new RoundedSquare();
      }	 
      return null;
   }
}

public class FactoryProducer {
   public static AbstractFactory getFactory(boolean rounded){   
      if(rounded){
         return new RoundedShapeFactory();
      }else{
         return new ShapeFactory();
      }
   }
}
```

2- İlişkili Factory metodlarını aynı class içerisinde bulundururuz. örnek kapımız ve kapıyı montaj edecek uzman (door fitting expert) olsun. bu kisinin ilişkili olması gerekli.

```java
interface DoorFactory
{
    public Door makeDoor();
    public DoorFittingExpert makeFittingExpert();
}

class WoodenDoorFactory implements DoorFactory
{
    public Door makeDoor()
    {
        return new WoodenDoor();
    }

    public DoorFittingExpert makeFittingExpert()
    {
        return new Wooden_Door_Fitting_Expert();
    }
}

class IronDoorFactory implements DoorFactory
{
    public Door makeDoor()
    {
        return new IronDoor();
    }

    public DoorFittingExpert makeFittingExpert()
    {
        return new Iron_Door_Fitting_Expert();
    }
}
```

# static factory method vs constructor

örnek: 

```java
new BigInteger("3")
```

vs

```java
BigInteger.valueOf("3")
```

- static'lerin avantajları:

  - constuctor'da metod ismi kullanmaz. sınıf ismi kullanır. bu sebeple constructor'ı çağırdığımızda yapılacak işin amacı için dökümantasyona bakmak şarttır. koddan direk anlaşılmaz.

  - static metod bize zaten varolan instance'ı dönebilir. oysa consctuctor'ın yeni instance yaratması şarttır.

  - bazı diller constructor overload'a izin vermiyor. eğer SL4J, SLF.net gibi tüm cross-language facada hazırlanacaksa static factory kullanmak gerekebilir.

  - static factory metod'lar aldığı parametreye göre (uygunluğu varsa) farklı bir sınıfta dönebilir. bunu constructor'da yapamayız.

- static'lerin dezavantajları:

  - OOP felsefesine aykırı

  - constructor'u olmayan sınıflar'dan subclass yaratılamaz. bu sebeple sadece static metod yaratıp, constructor'ları yazmaktan kaçamayız. fakat hem static hem constructor olunca, API'mizi kullanan developer'lara çok fazla seçenek sunmuz oluruz. 
  
    constructor'larımızı protected yaratabiliriz. fakatbu sefer başka paketlerden kendimiz çağıramayız. bu dezavantajı gidermek için, sub-class yaratmak yerine "composition over inheritance" yapabiliriz. yada constructor'ları çok basit tutarız ve kullandırtmak istemiyorsak bunu DOC'lara not düşeriz.

genelde kullanılan static factory metod isimlendirmeleri:

- from: örnek Date.from(instant); isntant birçok formatta olabilir. from bize istediğimiz sınıf yada subclass'a cast edecek.

- of: Set\<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING); birçok parametre alarak bize uygun olan classı döner.

- valueOf: from ile aynı.

- getInstance veya instance: Calendar.getInstance(); getInstance bazen ekstra paramere isteyebilir.

- create or newInstance: Array.newInstance(classObject, arrayLen); yeni bir instance döndürür. ayarları prametre olarak alır.

Yukarıdaki isimlendirmeler zorunlu diildir. fakat genelde bu isimlendirme kullanılır. örneğin; Calendar.getInstance() aynı instance'yi döndürmüyor. singleton pattern'de getInstance metodu aynı instance'yi döndürür. fakat calendar buna uymamış. calendar bu metodu şu amaçla böyle isimlendirmişler: önce default Locale'i bul ve bana instance'yi oluştur.
