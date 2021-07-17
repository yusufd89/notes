
############################

############################
# PATTERN DOMAIN DRIVEN DESIGN
############################

############################

# Domain-driven design (or DDD) vs data-centric design (or database-centric design or data-driven design)
DDD ilk olarak Eric Evans tarafından "Domain-Driven Design: Tackling Complexity in the Heart of Software" kitabında, 2003 yılında ortaya atılmıştır. Daha sonra, 2014'te Eric, tanımların referanslarını kısaca yazdığı "Domain-Driven Design Reference: Definitions and Pattern Summaries" isimli kitapta özetlemiştir ve çok ufak eklemeler yapmıştır.

Büyük çapta ve businnes logic'in kapsamlı ve kompleks olduğu uygulamalarda kullanılması tercih edilen bir yaklaşımdır.

Domain expertleri ve yazılımcılar ortak isimlendirme kullanmalıdır. isimlendirmeler teknik değil; domain uzmanlarının verdiği isimler olmalıdır. Bu sebeple bu isimlendirmeye "Ubiquitous (yaygın) Language" adı verilmiştir. 

DDD'yi anlamak için __data-centric design__ ile karşılaştırmak verimli olacaktır. Çünkü DDD, __domain-centric design (or domain-driven design)__ mantığı ile iş geliştirmeyi yapmamızı savunur.

Program yazarken önceliği hangi katmana vereceğimiz önemlidir. DDD, merkezde domain'i barındırırken, data-centric yapıda merkezde data vardır. DDD, önce domain modellerini çıkarılıp, daha sonra kalıcı veriyapısı (data) kısmı tasarlanmasını tavsiye eder. Domain ve persistence DB'deki tablolarımız farklı olabilir. Domain tarafında bu DB'den hiç habersiz geliştirme yapılmalıdır. Domain busisineess'i geliştirilirken domain modelleri üzerinden konuşulmalıdır. Oysa data-centric yapıda; data'lar bussiness ile içiçe karışmış olmasa bile (yani; iyi bir dizayn yapılmış olsa bile), data'ya göre businnes akışı ayarlanabiliyor. Örneğin; data-centric bir yapıda DB'deki birçok verimizi belli kategorilere atadık ve bu kategorileri ayrı tablolarda tuttuk. Sürekli sorgularımızı bu kategoriler üzerinden gerçekleştiriyoruz. Bu DB tarafında verimli bir çözüm olsa da, bu kısmın domain tarafında hiç bilinmemesi gerekiyor. İşte DDD bu yönelimin hiç olmaması için mimarsel çözümler sunuyor. Çünkü yazılımın temel ihtiyacı domain'e hizmet vermektir. DDD'de konular çok keskin bir şekilde ayrılmış diil yani şu şu şekilde yapılacak yoksa DDD olmaz diye öneriler mevcut diil. DDD sadece bir dizayn yaklaşımıdır.

Yukarıdaki paragrafı şuradan çıkarabiliriz: book: "Patterns, Principles, And Practices Of Domain-Driven Design", authors: "Scott Millett" and "Nick Tune", title: "Domain Model Implementation Patterns", subtitle: "domain model", 63 page, 1st paragraph.

DDD'de bir sistem 4 temel katman bulunmalıdır (kaynak: "Eric Evans", "DDD", "Layered Architecture" başlığı.):

- User Interface (or Presentation Layer): web servislerinin bulunduğu, önyüzlerin bulunduğu kodlar.

- Application: bu kısım 'use case'leri içerir. örneğin stok kontrolü... bu kısımda businnes logic yoktur. Controller'larımızın gittikleri ilk servisler diyebiliriz.

  Örneğin; Application seviyesinde; farklı client'lar için yapılan transformation ve validasyon işlemleri yapılabilir.

- Domain: tasarımın asıl ihtiyacı. bu kısım businnes logic'lerin olduğu asıl kısımdır. Sistemin tüm diğer katmanları bu katmana hizmet verecek şekilde tasarlanmalıdır. DDD'yi sadece burada uygulayacağız.

- Infrastructure: diğer hizmetlerin (mail, database...) ve kütüphanelerin bulunduğu servisler/kodlar. Bu kısma aynı zamanda ORM mapperlar'da dahildir. 

Yukarıdaki her maddenin ayrımı için kaynak: "Eric Evans", "DDD", şekil: "Figure 4.1. Objects carry out responsibilities consistent with their layerand are more coupled to other objects in their layer.".

DDD, birçok pattern'i öneriyor/içeriyor.

Eric'in kitabından bazı notlar:

- subdomain

  Domain: ecommerce, sub-domain: checkout, order.

  bir domain'de birden fazla subdomain olabilir. bir sub-domain'de birden fazla bounded context olabilir.

  best-practicelere göre 1 bounded-comntext, 1 sub-domain'e denk gelmelidir. Fakat bunu yapmak çok zordur.

- core domain

  bir doktor için yazılım düşünelim. Temelde 2 ihtiyaç var: 1-randevu sistemi, 2-hastaların bilgileri

  Burada core domain 2inci oluyor. Çünkü; hastaların bilgilerini tutma, tahlil sonuçlarını göstermek temel amaç. Bu sebeple randevu, __supporting domain__'dir.

- bounded context

  Bir model herkes için farklı görünebilir. örnek; USB ile satılan bir java yazılımı; aynı şirkette;
  - satış departmanı için satılacak ürün
  - lojistik depatmanında kargo
  - yazılımcı içinse bir jar dosyasıdır

  Farklı bir örnek olarak; bir "user", bazı domainlerde "customer", bazı domainlerde "işçi" olabilir.

  Herkes için farklı görünebilir, fakat aslında aynı kaynaktan (varlıktan) bahsediliyor.

  "Bounded context" bir model'in (yada modellerin) belli sınırlar içindeki anlamını ifade etmek için kullanılan bir terimdir. Yani "context içerisindeki sınırlandırılmış model" olarak türkçede düşünebiliriz. Her bounded context'te (satış, lojistik, yazılım...), farklı modeller ile bu "jar" dosyasını temsil edebiliriz. tabi bu durumlarda context'ler arası haberleşmede mapping yapmak durumunda kalabiliriz. (context mapping konusu)

  Bazı durumlardan 1 mikroservis tek başına bir bounded context'i temsil edebilirken, birden fazla mikroservis birlikte 1 bounded context'i temsil edebilir. kaynak: (source-id: 231) "Bir Bounded Context == Bir Mikroservis ?" başlığı. + (source-id: 232) 1inci paragrafın sonu.

- context map/mapping
  
  bounded context'ler arası ilişkilerin nasıl yönetileceği için disiplinleri belirler. bunların bazıları:
  
  - Shared kernel
    
    farklı bounded context'ler ortak model paylaşabilir.

  - Customer/Supplier Development Teams
  - Conformist
  - Anticorruption Layer
  - Open Host Service
  - Published Language

- Ubiquitous Language

  kod, diyagramlar, analizler, takım arası iletişimdeki konuşmalar ve yazışmalar tek bir dil üzerinden yürümelidir. bu dil domain expert'lerinin kullandığı dil olmalıdır. herkes bu dili kullanmaya zorlanmalıdır.

- continuous integration 

  sürekli test otomasyonları ile test yapılmasının önemine değinilmektedir. hem integration hemde unit testler sürekli koşulmalıdır. sürekli test; domain/businnes ihtiyaçların doğru karşılandığından emin olabilmemizi sağlayacaktır.

- model designers

  developer ekibi her zaman domain expert'ler ile birlikte çalışmalı ve Ubiquitous Language ile iletişimde olmalıdır. kodun herhangi bir yerine müdahale edecek tüm yazılımcıların domain modellerine hakim olması gerekmektedir.

- layered architecture

  domain models should be free of how storing themselves, displaying themselves...

- Domain Events

  domain expertlerini de ilgilendiren olaylar kolay takip edilebilir olmalıdır. aynı zamanda her event'in ismi/tanımı ve ne yaptığı açıkça belirtilmeli ve herkes tarafından event sonrası ve öncesi nelerin gerçekleştiği herkes tarafından bilinmeli. isimlendirmeler yine ortak (Ubiquitous) olmalıdır.

- servisler

  objelerin doğasında olmayan yazılımsal süreçler servis olarak tasarlanmalıdır. servis isimleri yine ortak (Ubiquitous) olmalıdır.

- modüller

  - bir modül içinde bulunan modeller ve diğer sınıflar, diğer modüllerdeki modellere "low coupling" olacak şekildeyse, modüllerimizi optimum bölünmüştür demektir.

  - Model, Services, Repositories gibi yazılımsal anlamdaki konseptlerine göre bölünmemeli. Bunun yerine domain temelli bölünmelidir: UserRepository, UserService...

- Aggregate vs Aggregate Root

  birden fazla entity'nin transaction'larda birlikte uyumlu şekilde iş akışını tamamlamaları gerekir. birden fazla entity'nin birlikte kullanılması durumu "__aggregate__" olarak (kitapta) ifade edilmektedir. yani aggregate, entity'ler grubudur. aggregate; koda baktığımızda sadece bir sınıf ile temsil edilmez. aggregate; logical bir kavramdır.

  "__aggregate root__" ise; direk örnek üzerinden gidersek: "sipariş" bir 'aggregate root'tur. ancak siparişe bağlı, 'ödeme bilgisi', 'müşteri bilgisi' entity'ler aggrete root'a bağlı (normal) entity olarak nitelenirler.

  Aggregate Root direk olarak diğer Aggregate Root'larla bağlantıda olabilir. bir Aggregate Root, bir entity ile direk ilişki içinde olamaz. yani; agreegate root'un primary-id'si ancak başka bir aggregate root'ta veya o agreagte içindeki herhangi bir entity'de olabilir.

  aggregate root; repository tarafından yönetilir ve client bir data load ettiğinde ancak aggregate root'a erişebilir. kaynak: (source-id: 233) answer of Jeff Sternal at Dec 24 '09 at 15:33. fakat pratik'te böyle kod yazılmaz. genelde client'a sadece ihityacı olan data kısmı yollanır. bu durum anti-pattern değildir. client için gerektikçe optimizasyon yapılabilir.

- Repository

  DAO'dan farklı bir kavramdır. (Farklı başlıkta detaylı anlatılıyor)

- Refactoring, Clean&Readable Code, Factory sınıfları, takım çalışmasının önemi, side effect free functions...

  Önemlerine bir kez daha bu kitapta özellikle değiniliyor. zaten çoğu bilgi kitap ilk yazıldığında piyasada bilinmiyordu.

# DDD kitabında geçen bazı terimler
Aşağıdaki bazı terimleri direk olarak kitap içerisinde açıklanmış.

  - # domain
    domain is the field for which a system is built. Airport management, insurance sales, coffee shops...

  - # model
    representation of a real world object. example: student class is not a real student object. student class includent only name, surname, age and some others representations.

  - # domain model vs database object
    domain objeleri, database objelerine benzer fakat database objelerinden tamamiyle ayrı olabilir. ilk uygulama tasarlandığında, "modeller" tasarlanmalıdır. daha sonra db-admin bunları nasıl isterse o şekilde databaseye kaydeder. databasede hızlı arama olsun diye bazı şeyler bölünebilir, tipi değiştirilebilir vs... fakat bu optimizasyonlar database objelerinde yapılmalıdır.
  
    bu ikisi arasında gerçek hayata en benzer olan; domain objeleridir. çünkü db-admin'ler gerçek hayata uzak değişiklikler yapabilir.

  - # domain model
    domain model (class) is the model which is using by a domain.
    
  - # DTO (or Data Transfer Object)
    DTO is the class/structure which is using to store data. It can be using to send data from network protocols or passing argumants to functions. DTO can store model or models or any data...  

    gerçek bir uygulamadan örnek verirsek; repository'den dönen entity class'ı dto'ya çevrilir ve client'a dönülür. işte bu dto bizim modelimizdir (bir domain altında çalıştığımız için 'domain modelimiz'dir).

    DTO'lar, modellerimiz ile aynı Obje/class olacakları anlamına gelmez. Farklı da olabilirler. Yada aynı olabilirler ama modelleri direk döndürmek yerine mapping yaparak aynı field'lara sahip farklı obje'ler de kullanabiliriz. Çünkü DTO'lar sadece Data transfer obje'leridir ve servisler arası haberleşme'de data tranferi için kullanırlar. Remote servis çağrıları maliyetli olduğu için, tek bir istekde birçok data'yı birden taşımak isteriz. Bu sebeple DTO' pattern'i ortaya atılmıştır. kaynak: (source-id: 234) 1inci paragraf.
    
    Sun/Java community DTO'lara sadece "transfer obje" demektedir. Bu pattern'in yazılım dünyasında genel adı "Data Transfer Object (or DTO)"tir. kaynak: (source-id: 234) son paragraf.

  - # entity
    yazılım framework'lerinde entity terimi veritabanındaki bir tablonun yazılım tarafındaki temsilidir. fakat Eric'in DDD kitabında bu farklı amaçla kullanılmaktadır. kaynak: "Eric Evans", "DDD", "Entities (a.k.a. Reference Objects)" başlığı, 13'üncü paragraf.

    Eric'in kitapta bahsettiği entity kavramı; eşleştirilmeye kalktığımızda (bir eşitlik sorgusunda) field'ları ile değil, sadece id'si ile kontrol etmemiz gereken domain modellerimizdir. kaynak: "Eric Evans", "DDD", "Entities (a.k.a. Reference Objects)" başlığı, 12'üncü paragraf'ın ilk cümlesi.

  - # value object
    property'leri eşit olduğunda, birbirleri yerine kullanılabilen objeler'dir.
    
    örnek-1: 
    
    Ahmet1 ve Ahmet2 veritabanı objelerimiz olsun. ikisinin tüm property'leri (isim, soyisim, yaş...) aynı olsun. buna rağmen bu objeler birbirlerine eşit değildir. bu sebeple bu objeler "value object" değildir.

    örnek-2:

    Koordinat düzlemindeki noktayı tutan bir point1 ve point2'miz olsun. bu objelerin property'leri (x, y, z) eğer ynı ise bu 2 obje birbirlerine eşit demektedir. bu sebeple point objesi bir "value object"'tir.

    örnek-3:

    adres bir value object'tir. kaynak: kaynak: "Eric Evans", "DDD", "Is "Address" a VALUE OBJECT? Who's Asking?" başlığı.

    örnek-4:

    renkler birer value object'tir. kaynak: kaynak: "Eric Evans", "DDD", "Is "Address" a VALUE OBJECT? Who's Asking?" başlığının hemen sonrasındaki ilk cümle.
