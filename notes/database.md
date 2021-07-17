############################

############################
# DATABASE
############################

############################

# cluster vs data center (or data centre)
data center fiziksel bir kavramdır. data center aynı LAN'a bağlı olan bilgisayarlar topluluğudur. Oysa cluster tamamen logically sınıflandırılmış/gruplandırılmış yazılımlar kümesi anlamına gelir.

Aynı yazılımın 1 cluster'ı içerisinde birden fazla data center olabilir. Veya 1 data center içerisinde, aynı yazılımın birden fazla cluster'ı olabilir.

1 cluster içerisindeki veriler sync olmak zorunda diil. parçalanmış olabilir, yada sadece bazı data'lar sync, bazı data'lar parçalanmış olabilir. Bu tamamen yazılımın nasıl çalıştığına bağlıdır.

Yazılım sunucuları birçok node'da ayağa kaldırıldığında bu yazılımlara her cluster ve her data-center'ı tanıtmak gerekir. Çünkü data-center'lar arası data paylaşım politikası ile data-center içerisindeki data paylaşım politikası farklı olabilir. Örneğin; cassandra'da, aynı cluster içindeki farklı data-center'larda farklı politika şizlemesini sağlayabiliyoruz. örnek:

```sql
CREATE KEYSPACE custom_keyspace
-- here column names...
WITH REPLICATION = { 'class' : 'NetworkTopologyStrategy',
                     'datacenterNewYork':5,
                     'datacenterDubai':10
                   }
```

# availability domain
hata töleransına karşı ortak yada kısmen ortak verileri sunmaya çalışan data center'ların tümüdür.

# High-availability clusters (or HA clusters or fail-over clusters)
fail-over kelime anlamı: yük devretme

Bu terim sıkça DB alanında kullanılsa da, bilişimde diğer birçok alan içinde geçerlidir. Herhangi bir server yazılım grubu için High-availability'den bahsedilebilir.

Her DB'nin genelde klone'u/replikası tutulur. Bu şekilde bir DB instance'ına zarar gelirse, yedeği olmuş olur. Bunu yapmak için birçok farklı teknik var:

- __Active/active__

  her node sync bir şekilde birbirinin her güncellemesini anlık olarak alır/sync olur. Bu yavaş bir tekniktir fakat en stabilidir. Her instance/node sürekli dışarıya hizmet veriyor olur.

- __Active/passive__

  passive node'lar, active olan (dışarıya hizmete açık olan) db node'larındaki tüm değişiklikleri kendine sürekli olarak alır. Fakat passive node'lar dışarıya hizmet vermezler. Eğer active bir node'a zarar gelirse, passive olan herhangi bir node active duruma geçer.

# Oracle's High Availability Architectures and Solutions
Oracle DB ürünü (default'ta) sadece tek başına tek 1 instance ve tek 1 cluster olarak çalışır. Diğer her feature ekstra çözüm uygulamak gerekir. Bunlar burada detaylı listelenmiştir: (source-id: 86)

Bu çözümlerden biride 'Data Guard'dır. Bu çözümde "Primary database" e hem yazılıp hem okunabiliyor. Fakat farklı data-center'larda olan birden çok oracle instance'ı "Standby database" olarak çalışıyor. Primary'ya yapılan her işlem otomatik olarak her standby'a da yollanıyor. Standy sürekli olarak sadece read-only hizmet verebiliyor. Fakat eğer primary çökerse, bir stanby primary olarak çalışmaya başlıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# CAP theorem (or Brewer's theorem)
dağıtık bir sistemde veri üzerinden sunulan hizmet için aynı anda 3 özelligin sağlanamayacağıdır. En fazla 2 tanesininin sağlanabildiğidir. Bu 3 özellik nedir:

- Consistency (or Tutarlılık): dağıtık sunuculardan birine X bilgisini kaydettik. diğer herhangi bir sunucudan o veriyi okumak istediğimizde X okuruz.
- Availability (or Erişebilirlik): istediğimiz zaman sunuculara erişim açık olacaktır (sunucular erişilebilir durumda olacaklardır)
- Partition Tolerance (or Bölünebilme Toleransı): sistemdeki data'lar tüm node'larda değil, parçalanmış durumda olması durumudur.

Örneğin; ağ arasındaki haberleşme giderse (P); C'nin sağlanması mümkün olamaz. Fakat A sağlanabilir.

Örneğin; Eğer data partitioning yaptıysak (P) ve node'lar arasında network sorunu olduğunda şu iki çözümden birini uygulamamız şart:
- client'tan gelen request'leri geri çevir --> bu durumda; sistemin tutarlılığı sağlanmış olur (C), fakat availablity'den (A) feragat etmiş oluruz
- client'lardan gelen request'lere, eldeki en sonki güncel data ile cevap ver --> bu durumda; sistemin tutarlılığı sağlanmamış olur (C), fakat availablity (A) sağlanır.

(yukarıdaki örnek için kaynak: (source-id: 87) "Peki bu Partition Tolerance ne işe yarıyor ? Hala tam anlayamadım diyorsanız biraz daha konunun üzerine gidelim." maddesi.)

Facebook gibi sosyal medya yazılımlarında, "like" sayıları anlık olarak herkese doğru gösterilmeyebilir. "Like" gibi tölerans gösterilebilen birçok data tipi vardır. Bunlar için uygun teknoloji seçimi yapmak gereklidir. CAP teoremi yazılarında, hangi ikili istendiğinde hangi veritabanı kullanılabileceği de yazmaktadır.

```
                                 CONSISTENCY (All client get the same data)
                                           x
                                        x     x              MongoDB
          RDBMS                    x             x           Redis
          MySql               x                      x       HBase
          MariaDB         x                             x    MemcacheDB
                     x                                     x
                 x                                             x
            x  x  x   x   x   x   x  x   x  x  x  x  x  x  x  x  x 
AVAILABILITY                                                       PARTITION
(All clients can                   Cassandra                 (The system is not effected
always read and write)             Riak                       by network partitioning)
                                   CouchDB
                                   Dynamo
```

# Consistency Models
RDBMS'ler "Immediate Consistency" sunarlar. fakat ayarlanır ise; bazı NO-SQL veri tabanlarıda "Immediate Consistency" sunabilir.

birçok çeşt Consistency Model'i var. bunlar Miguel Diogo, Bruno Cabral, Jorge Bernardino'nun "Consistency Models of NoSQL Databases" isimli çalışmasında da anlatılmış. Kaynak: (source-id: 88) Yazar: Miguel Diogo, Bruno Cabral, Jorge Bernardino, "Consistency Models of NoSQL Databases", "Figure 2.Consistency Models based on Reference" görseli.

Consistency nereden bakıldığına göre (client ve sunucu açısından) değişir.

## User-centric consistency models

- ### Consistency Guarantees

  Bu başlık altındakiler birer model dğeildir. Fakat birer feature olarak değerlendirilirler.

  - ### read your own writes (or read-your-writes or read your writes or RYW)
    bir client bir bilgiyi kaydettikten hemen sonra o bilgiyi okumak isterse, güncel kaydettiği bilgiyi okur.

  - ### Monotonic writes (or MW)
    bir client sırası ile istek attığında bunlar sırası ile işletilecektir.

  - ### Monotonic reads (or MR)
    client bir bilgi okumuş ise; o bilgi okunduktan sonra tekrar update edilmedi ise, o bilgi tekrar tekrar okunduğunda aynı dönecektir.

- ###  Writes Follow Reads (or WFR)

- ### Eventual consistency (or nihai tutarlılık)
  weak ile strong arasında kalan bir tutarlılık biçimidir.

  weak'teki gibi; client'lar eski data'ları çekiyor olabilir. fakat nihai olarak, belli süre geçtikten sonra aynı datayı çekecektir. burada Weak Consistency'den fark; işlemlerin sıralı olmasıdır. Weak Consistency'de sıra sağlanamadığından, herkes aynı zaman aralıklarında farklı data çekebilir.

  Bu fark neden olur? Cassandra'yı ele alalım. Cassandra'da, update ile insert işlemi aynı kapıya çıkıyor. 2 farklı cassandra sunucusuna istek geldiğini düşünelim, ikiside insert işlemi(yada update) yapıyor olsun. ikisi aynı anda replica'lara dağıtılırken/sync olurkenı, o sıra data okumaya çalışan farklı client'lar var ise, farklı sunuculardan okurlarsa aynı anda farklı data çekmiş olacaklar.

  Cassandra örneğimizde; en son yazılan data, (belli bir süre sonbra - nihai olarak) tüm replica'lara klonlanacağı için, nihai tutarlılık sağlanmış olacak.

  eventual consistency 3 şeyi garanti eder:

  - ### read your own writes (or read-your-writes or read your writes or RYW)

  - ### Monotonic writes

  - ### Monotonic reads

## Data-centric consistency models

- ### Causal consistency

- ### FIFO consistency (or PRAM consistency)

- ### Cache consistency

- ### Processor consistency

- ### Strong Consistency (or immediate consistency or Linearization or strict consistency or atomic consistency)
  client'a cevap ancak; tüm sunuculara iletildikten ve kaydedildikten sonra gerçekleşir. dolayısı ile en yüksek seviye consistency budur. tüm sistemde kayıtların/işlemlerin sırası tektir/sabittir.

- ### Weak Consistency
  client'a gönderilen cevap en güncel data'yı içermeyebilir. tüm sistemde kayıtların/işlemlerin sırası tutulmaz.

  client'ın eski data alması durumuna "inconsistency window" adı verilmiştir. 

- ### Sequential Consistency
  tüm client'lar aynı zaman aralıklarında aynı datayı okurlar. örneğin; X güncellemesi, replicalara sync ediliyor olsun. 10 replicadan 5'i X güncellemesini alsın. Tam o sırada istek atan client'ların tümü X güncellemesini almalı yada herkes eski halini görmeli. Client'ların bir kısmı X ile bir kısmı eski halini görmemeli. Eğer bu durum sağlanabiliyorsa "Sequential Consistency" var demektir. kaynak: (source-id: 89) "2–1. Sequential Consistency" başlığı.

# Replication models

- ## Passive replication model (or Primary backup)
  tüm client'lar sadece "primary server" denilen sunucuya istek atar. bu sunucu diğer recplica'lara klonlama işlemini gerçekleştirir. sync yhda async yapıp yapmayacağı implementasyona göre değişir. eğer sync backup işlemi yapılıyorsa; client'a çok geç cevap dönülür. bu model'e __pessimistic__ adı verilir. Tersi durumda async bakcup alınır ve clien t'a hızlıca cevap dönülür. BU model'e ise __optimistic (or eager)__ adı verilir. 

  Yukarıdaki tüm paragraf için kaynak: (source-id: 90) Yazar: Leticia Pascual Miret, Master's Degree in Parallel and Distributed Computing, "2.4.1 Passive replication model" başlığı.

- ## Active replication model
  Passive'de tek bir yükümlü sunucu varken (primary server), burada birden fazla olmaktadır. Dolayısı ile, tutarlılığı sağlamak daha zordur. Fakat bu model'in __fault tolerance (or hata töleransı)__ vardır.

  kaynak: (source-id: 90) Yazar: Leticia Pascual Miret, Master's Degree in Parallel and Distributed Computing, "2.4.1 Passive replication model" başlığı.

- ## Semi-passive vs semi-active replication models
  kaynak: (source-id: 90) Yazar: Leticia Pascual Miret, Master's Degree in Parallel and Distributed Computing, "2.4.1 Passive replication model" başlığı.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Horizontal Partitioning (or Yatay Bölümleme)
aynı satırın bütünüyle aynı makinada tutulur. fakat 1 tablonun farklı satırlarının birçok farklı fiziksel makinada bulunabilmesi. örneğin Users tablosu nun ilk 1000 satırı, X fiziksel makinesindeyken, ikinci 1000'lik kısmı (1000-2000 satırları) farklı fiziksel makinada olması durumudur.

# Vertical Partitioning (or Dikey Bölümleme)
X makinasında sadece S1, S2, S3 sutunları X makinesinde, Y makinesinde ise S4, S5, S6 sutunları olması durumudur.

dolayısı ile bu durumda bir tablodan full tüm sutunları her defasında çekiyor isek bu verimsiz bir çözümdür.

# Horizontal + Vertical Partitioning
eğer bu DB yazılımı tarafından destekleniyorsa; 

- A makinasında sadece S1,S2,S3 'ün ilk 1000 satırı vardır.
- B makinasında sadece S1,S2,S3 'ün ilk 1000-2000 satırları vardır.
- C makinasında sadece S4,S5,S6 'ün ilk 1000 satırı vardır.
- D makinasında sadece S4,S5,S6 'ün ilk 1000-2000 satırları vardır.

# partitioning vs sharding
sharding kelime anlamı: parçalama

partitioning kelime anlamı: bölümleme

partitioning aynı DB şeması (veya DB instance'ı) (zaten bu; aynı makine anlamına geliyor) içerisinde bir data'yı (örnek: tabloyu) gruplamak için kullanılır. Bir data'nın gruplanması sadece o gruba özel işlemler yapılabilmesini sağlar. Örneğin; büyük bir tablomuz olsun ve bunu 2 partition'a ayırmış olalım. İlk partition'a özel index yaratabiliriz, yada sadece ilk partition'u drop edebiliriz...

Oysa sharding bir data'yı bölerek, her parçasını ayrı ayrı farklı şemalarda (veya DB instance'larında) (zaten bu farklı makineler anlamına geliyor) tutmak anlamına gelir.

# Horizontal Scaling (or Yatay Ölçeklendirme)
yeni makine/node eklenerek güç arttırılması.

# Vertical Scaling (or Diken Ölçeklendirme)
varolan makinelere CPU,memory, disk gibi kaynaklar eklenerek güç arttırılması. kaynak: (source-id: 93) "Partitioning and Sharding" başlığı, 3üncü paragraf, 1inci cümle.

# scaling
- scale up: adding more resource (RAM, CPU...) to a machines/instance.
- scale down: removing resources (RAM, CPU...) from a machines/instance.
- scale out: adding more machines to cluster or system
- sclae in: removing machines from cluster or system

# Network Partitioning (or Split Brain Syndrome)
Bağımsız cluster'daki node'lar, diğer cluster çökmemesine rağmen çökmüş olarak algılama durumuna verilen isimdir. kaynak: (source-id: 94) 1inci paragraf.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Mongo DB User/Auth

mongo da varsayılan olarak veritabanında hiç kullanıcı yokken herkes erişimi sağlayabilmektedir. bir kullanıcı eklendiğinde artık erişimlerin tümü kısıtlanmıştır.

mongo'da "admin" database'si sistem tarafından kullanılan bir database'dir. bu database'nin içinde kullanıcılar ve rol bilgileri collection'larda tutulur. bu sebeple "admin" databasesi, örneğin robomongo tool'unda "System" klasörü altında gösterilir.

ilk mongo açıldığında "admin" databasesinde bir user yaratılmalıdır. bu user'a "userAdminAnyDatabase" rolü atanmalıdır. bu role ile bu kullanıcı artık yaratılacak her yeni database'ye yeni kullanıcı ekleyebilir hale gelir. bu kullanıcı collection'lara veri ekleme çıkarma gibi işlemler yapamaz. bu rol'de atama işlemini şu komutlarla yapabiliriz:

```js
use admin

var user = {
  "user" : "admin_user",
  "pwd" : "manager",
  roles : [
      {
          "role" : "userAdminAnyDatabase",
          "db" : "admin"
      }
  ]
}

db.createUser(user);

exit
```

şimdi mongo'ya bu yetki ile bağlanıp yeni bir database ve ona bağlı bir user yaratalım:

> mongo admin -u admin_user -p

```js
use test_db

var user = {
  "user" : "test_db_user",
  "pwd" : "123",
  roles : [
      {
          "role" : "readWrite",
          "db" : "test_db"
      }
  ]
}

db.createUser(user);

exit
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# liquibase vs flyway
programatik DB şema yönetimini sağlayan birbirine alternatif framework'lerdir.

Migration gibi işlemlerde, db şema işlemlerinde kullanılabilirler. Her şama değişikliğini detaylı şekilde historical tutarlar ve hata olması durumunda rollback senaryoları tanımlayabilmemizi sağlarlar.

Martin Fowler "Evolutionary database design" isimli bir makale yayımlamıştı. Bu makaledeki gibi database gelişimi istiyorsak bu tarz framework'lerdne yararlanmamız çok verimli olacaktır.

örnek bir liquibase.xml dosyası:

```xml
<?xml version="1.1" encoding="UTF-8" standalone="no"?>
<databaseChangeLog xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                   xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
                   xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.9.xsd">

    <!-- her changeSet sırası ile DB şemasına işlenir.  liquibase kendi tablosunu oluşturur. 
    bu tabloda hangi changeSet'lerimn işlendiği, author'un kim olduğu, hangi date-time'da db'ye işlendiği
    gibi bilgileri tutar.-->
    
    <!-- changeSet'lerde herşey olabilir: DB'ye yeni kayıt (satır) ekleme, 
         yeni tablo oluşturma, tablo silme, tablo şeması güncelleme... -->

    <changeSet author="ahmet" id="changeSetId1">
        <createTable tableName="users">

            <!-- 2 adet sutun birlikte (username ve last_name), bir primary key görevindeler. -->
            <column name="username" type="VARCHAR2(255 CHAR)">
                <constraints nullable="false" primaryKey="true" primaryKeyName="username_primary_key"/>
            </column>

            <column name="last_name" type="NUMBER(19, 0)">
                <constraints nullable="false" primaryKey="true" primaryKeyName="username_primary_key"/>
            </column>

            <column name="CREATED_BY" type="NUMBER(19, 0)"/>
            <column name="CREATED_DATE" type="TIMESTAMP(6)"/>
            <column name="LAST_MODIFIED_BY" type="NUMBER(19, 0)"/>
            <column name="LAST_MODIFIED_DATE" type="TIMESTAMP(6)"/>
        </createTable>
    </changeSet>

    <changeSet author="mehmet" id="changeSetId2">
        <createTable tableName="orders">
            
        </createTable>
    </changeSet>
</databaseChangeLog>
```

Yukarıdaki liquibase.xml dosyasını bu şekilde ilgili DB'de işlem görmesini sağlayabiliriz:

```sh
"/path/to/liquibase" --driver="oracle.jdbc.OracleDriver" --classpath="/path/to/ojdbc7-12.1.0.2.jar" --url='jdbc:oracle:thin:@www.custom-db.com:1521/MY_DB' --username="user" --password="password123" --changeLogFile="liquibase.xml" update
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Oracle Exadata (or Oracle Exadata Database Machine)
sadece oracle db kullanımı için optimize edilmiş, oracle tarafından satılan fiziksel sunuculardır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# varchar vs char vs nvarchar vs nchar

"n" prefixi string'in UNICODE karakterlerinin tümümünü desteklediği anlamına gelir. "n" olmayan string'lerde UNICODE'un sadece en sık kulanılan "plane 0"'ı (başka başlıkta anlatılıyor) desktekleniyor.

- CHAR is fixed-size. char(100), 100 karaketre store etmese bile 100 karaketerlik yer harcar. sürekli bu alanı reserved tutar.
- VARCHAR is variable-size. hücre, sadece karakterler sayısı kadar yer kaplar.

char; varchar'a göre çok daha performans sağlar fakat daha çok yer kaplar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# code first vs database first vs model first
birer database yazılım ilişki kurma yaklaşımlarıdır (or approach).

- ## code first
önce kod yazılır, ardından entity framework yazılımı db'yi oto oluşturur.

- ## database first
önce sql kodları ile db oluşturulur, ardından yazılımcı buna denk gelen modelleri kodda yazar.

- ## model first
genelde IDE'lerde db dizayn araçları ile yapılan bir işlemdir. db'yi bu araçta hazırlarsınız, bu araç hem kod hem de db tarafını otomatik oluşturur. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# obje
veritabanı dünyasında obje; tablo, view, index'lerin (ve daha fazlası fakat herşey değil!) grup ismidir. bu durumda; örneğin USER tablosu bir database instance'sidir.

# Schema (or şema)
1 veritabanında birden fazla şema olabilir. her şema altında birden fazla tablo vardır. Şema aslında tabloların, ilişkilerin ve daha birçok database objesinin tanımıdır.

A user'ı, Y şemasının altındaki tüm objelere erişebilir gibi ayarlamalar kolayca yapılabilir.

bir tablonun ismini yazarken şu şekilde formatlarız: şema_ismi.tablo_ismi

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# In-memory DB

# data grid vs data structure store vs key-value store
grid kelime anlamı: kafes, şebeke

__data grid__; data'nın birçok node'a paylaştırılarak(distributed) yönetilmesini sağlayan sistemlere/mimarilere verilen genel ifadedir.

"data grid" terimi; '__grid computing__'den gelir. kaynak: (source-id: 95) 1inci paragraf.

__in-memory data grid (or IMDG)__ terimi ise isminden de anlaşıldığı gibi RAM'de yönetilen data-grid'lerdir. kaynak: (source-id: 95) "Example Use Cases" başlığı, 4üncü paragraf.

__key-value__ DB'leri sadece bir key'e karşılık herhangi bir tipte veri tutarlar. Fakat __data structure__ db'leri key tarafta list, set, array gibi daha karmaşık veri yapılarını da destekler. dolayısı ile __data structure__ db'leri aynı zamanda key-value veri yapısını da desteklemiş olur. kaynak: (source-id: 97) "What is Redis?" 2inci ve 3üncü paragraf.

# local cache
In-memory DB'lerin önemli özelliklerinden biri de local-cache özelliğidir. Redis gibi data store'ları genelde kalıcı data için diilde, çok kısa vadeli data'ları tutmak için kullanılırız. Bu sebeple genelde kayıt atan uygulama aynı data'yı tekrar okur. Bu sebeple local cache özelliği vardır. local-cache okunan datayı local'de tutar ve her güncellemesini de sunucu ile sync tutar. Bu şekilde tekrar okuması gerekirse direk lokal'den okur. Local-cache policy'leri DB'den DB'ye çok farkedebiliyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Distributed lock
Tüm client'ların update etmesini engellediğimiz data'ları lock'lamamız gerekebilir. Distributed bir sistemde lock yağtığımızda, "Distributed lock" yapmış oluruz. Distributed lock'ların client'lar tarafından evict (serbest bırakılması) gerekir. Sunucuda lock'ların listesi ve statüleri tutulur. Hangi data'nın lock'lanılacağına karışılmaz. Aynı şekilde java'da standart Lock sınıfları da bu şekilde çalışmaktadır. Lock'lanan kod bloğunun ne içerdiği ile ilgilenilmez.

"Distributed transaction" ile "Distributed lock" farklı kavramlardır. "Distributed transaction" için saga veya 2PC(SQL transaction desteği) gibi çözümlere gidebiliriz. "Distributed Lock" ise farklı node'larda duran bir verinin belli bir süre farklı client'lar tarafından okunmaması veya yazılmaması için gerekli özelliktir.

"Distributed" terimi, birden fazla birbirinden bağımsız çalışan node'ların tek bir (global) transaction yürütmesi anlamına gelir.

Client çöker ise ve sunucudaki "lock" bilgisini evict edemezse durumu için, her lock işleminde, genelde, lock için timeout süresi belirtilir. Tanımlanan bu timeout süresi sonrasında sunucu otomatik "lock" bilgisini evict eder/unclock eder.

aşağıdaki tüm açıklamalar için kaynak: (source-id: 98)

Redisson'un lock için sunduğu implementasyonların bazılarına bakalım:

Redisson'un, "RLock" implementasyonlarının tümünde, RLock'ı acquire eden java thread'i ancak lock'ı serbest bırakabilir. Başka thread lock'ı kaldırmak isterse IllegalMonitorStateException fırlatılır. Bu durum standart Java içerisinde gelen "java.util.concurrent.locks.Lock" sınıfılarında da bu şekildedir. Eğer başka client'a bu yetki verilecek ise Lock yerine "Semaphore" kullanılmalıdır.

not: Bir uygulamada birden fazla client olabilir, hatta 1 thread'de de birden fazla bağımsız client olabilir.

Aşağıdaki lock mekanizmalarının desteklenmesi için redis (sunucu) tarafında birçok metadata'nın tutulması gerekebilir.

- Lock

  Klasik lock işlemi yapar.

  ```java
  // redissonClient tüm lock'ların listesini (instance'larını) tutuyor. bu sebeple; getLock metodu ile aynı instance'ı istediğimiz yerden çağrabiliriz.
  RLock lock = redissonClient.getLock("myLock");
  
  lock.lock();
  // or acquire lock and automatically unlock it after 10 seconds
  lock.lock(10, TimeUnit.SECONDS);

  // or wait for lock aquisition up to 100 seconds 
  // and automatically unlock it after 10 seconds
  boolean res = lock.tryLock(100, 10, TimeUnit.SECONDS);

  // do anything you want
  if (res) {
    try {
      // do anything here. redis does cares about what writes here..
    } finally {
        lock.unlock();
    }
  }
  ```

- Fair Lock

  ```java
  RLock lock = redissonClient.getFairLock("myLock");
  ```

  "redisson" (connection) instance'ındaki tüm thread'ler hangi sıra ile lock isteği yolluyorsa, o sıra ile lock'ları acquire edebilecekleri şekilde ayarlanmış lock implementasyonudur. aynı thread'in içindeki lock sırası diil, tüm thread'lerdeki lock sıralaması göz önünde bulundurulur.

- MultiLock

  birden fazla lock'ı grup içine alarak tek bir lock nesnesi üzerinden işlemlere devam edebiliriz.

  ```java
  RLock lock1 = redissonClient1.getLock("lock1");
  RLock lock2 = redissonClient2.getLock("lock2");
  RLock lock3 = redissonClient3.getLock("lock3");

  RLock multiLock = anyRedissonClient.getMultiLock(lock1, lock2, lock3);
  ```

- RedLock

- ReadWriteLock

  Lock mekanizmasının genel ismi bu olarak geçsede; interface olarak buna denk gelir: __org.redisson.api.RReadWriteLock__. RReadWriteLock ise java'daki __java.util.concurrent.locks.ReadWriteLock__ intreface'sinden türer. Sınıf olarakta __org.redisson.RedissonReadWriteLock__ kullanılır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

## Redis
- belirli aralıklarla (isteğe bağlı olarak) verileri dosyaya kaydedebilir.
- tümüyle c ile yazılmıştır. tek thread çalışır.

Redis client'ları:
- lettuce
- Redisson
- Jedis
- spring-data-redis (arkaplanda jedis yada farklı bir implementasyonu kullanır)

Terimler hakkında:
- Redis Lab; redis'in enterprise versiyonunu geliştiren firmanın ismi.
- redis lab'in kendi AWS'lerinde bize hazır sunduğu redis'ler var. bu hizmetin özel adı "Redis Enterprise Essentials" dır.
- "Redis Enterprise Pro" ise redis lab'ın sunduğu AWS entegrasyonudur. Kendi aws account'umuzda kullancağımız redis'lerdir.

yukarıdaki 3 madde için kaynak: (source-id: 99)

Bu sayfada (source-id: 100) hangi özelliğin redis lab veya open source proje tarafından geliştirdiği anlaşılabilir. redis.io olan linkler redis open source projesi tarafından destekleniyor fakat redislabs.com'a yönlendirilen linkler sadece "redis labs" tarafından destekleniyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# in-memory non-RDBMS

| name       | developer  | language | open source |
|------------|------------|----------|-------------|
| Infinispan |            | java     | yes         |
| Hazelcast  | hazelcast  | java     | yes         |
| memcached  |            | c        | yes         |
| redis      | redis labs | c        | yes         |
| Ehcache    |            | java     | yes         |

memcached, redis'e göre daha az özellik içerir. kaynak: (source-id: 101) + (source-id: 102) "Which is better: Redis or Memcached" başlığı.

Redis için çok fazla 3üncü parti eklenti bulunur. Redis zaten çok gelişmiştir ve bu sebeple çok fazla hakimiyet ister. Bu sebeple çok gelişmiş özellikler kullanılmayacak ise memcached tercih edilmelidir.

tümüyle java ile yazılanları özellikle production ortamında jvm'i de yönetmek gerekebilir. Özellikle büyük data'larda heap taştığında, JVM konularına büyük hakimiyet gerektirebilir.

# in-memory RDBMS

| name                 | open source | developer | language |
|----------------------|-------------|-----------|----------|
| h2                   | yes         |           | java     |
| Derby                | yes         | apache    | java     |
| HSQLDB (or HyperSQL) | yes         |           | java     |

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# RDBMS

## mysql vs mariadb
oracle tarafından geliştirilen open source bir DB'dir. ilk geliştirildiğinde oracle'da diildi, fakat oracle satın alınca community mariaDB'yi oluşturdu. MariaDB gerçek bir community ürünüdür ve geliştirme süreçleri bile takio edilebilir durumdadır. Oracle'ın kendi DB'si olduğundan, birçok proje, uzun vadede lisans veya farklı problemlerden kaçındığı için mariaDB kullanamktadır.

mariaDB, resmi olarak "drop-in replacement of MySql" olarak sunulmaktadır. kaynak: (source-id: 429) ilk cümle.

yani mysql yerine hemen geçilebilir durumdadır. Fakat son yıllarda geçiş iş yükü (farklılıklar) gitgide artmaktadır. mysql client'ları mariadb'ye de bağlanabilir, sql syntaxları aynıdır, desteklediği veri tipleri aynıdır...

Her sürüm için farklılıklar ayrı ayrı dökümante edilmiş: (source-id: 103)

## postgresql (or postgres)
performance açısından mariadb ve mysql'e göre övülen açık kaynaklı bir DB.

- unsopported features:

(source-id: 104)

- supported features:

(source-id: 105)

## microsoft sql server (or mssql) vs oracle DB
- genel olarak oracle daha gelişmiş özellikler içeriyor fakat yönetimi daha zor.
- oracle, OS bağımsız çalışırken, mssql sadece ms-windows gibi limitli birkaç OS'ta çalışabiliyor.
- mssql microsoft'un diğer ürünleri ile direk olarak destekleniyor. örneğin "linq"'nın diğer db'lere olan entegrasyonu daha sonradan eklendi.

## DB2
IBM tarafından geliştirilen ilişkisel veritabanı. güncel sürümlerinde no-sql tarzı özelliklerde sunmaya başlamıştır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# serverless DB

## SQLite
sadece bi dosya içinde saklanabilen ilişkisel veritabanı altyapısıdır. sunucu runtime yazılımına ihtiyaç duymaz. çünkü sadece 1 tek dosyadan ibarettir. bu dosyaya erişenler dosyayı okuyup veritabanından neler olduğunu görebilir. aslında sadece bir dosya formatıdır. yazılım veya bir servis değildir.

## Microsoft Access

## LibreOffice Base

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# strong entity vs weak entity

bir tablo (entity) sadece kendi başına bir objeyi ifade edebiliyor (kendi başına yaşayabiliyor / anlam ifade ediyor ise) o tablo güçlüdür. tersi durumda zayıftır. örneğin; "oda" zayıf bir nesnedir. çünkü bina olmadan, oda hiçbir şey ifade etmez. fakat bina tek başına yeterlidir. bina evdende kendi başına yer alabilir.

aslında tam olarak resmi bir tespit etme yöntemi vardır. şu örnekten gidelim:

Customer(customerid, name, surname) --> dışardan tablo referans edilmesine gerek yok. kendi başına yeterli. güçlü.

Adress(addressid, adressName, customerid) --> customerid ile customer verilmesi lazım. adress güçsüz bir varlık.

Adres bir müşteriye ait olmasa; güçlü olacaktı. yani; veritabanına göre gerçek hayattaki nesneler güçlü yada güçsüz olabilir. gerçek hayattan örnek vererek tespit doğru değildir. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# aday anahtar (or candidate key)
join yada benzeri bir sorgu sonucu dönen sonuç tablosunda; bir yada birden sutun, o tablo için private key oluyosa; bu sutunlar aday anahtar demek oluyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# data domain
veritabanlarında data domain; bir sutunun alabileceği değerler kümesini belirtmektedir. örneğin; tc, 10000000 ile 99999999 arasında değer alabilir. is_enabled, true yada false alabilir gibi...

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Normalizasyon
tekrarlanmayı engellemek için best practice'lere uygun veritabanı modeli uygulamak için yapılan işlemlerdir.

# Denormalized
1NF'in dahi karşılanmadığı veritabanı dizaynıdır.

Aşağıdaki örnek veritabanında Adres bilgileri calistigi ofisin adres bilgileridir. Sutun ismi uzun olacağından anlaşılır bir sutun isimi yazılmadı.

> ||| AdresId ||| Name ||| Surname ||| Adres1_İlçe ||| Adres2_İlçe ||| Calistigi_Ofis |||

# 1NF (or 1st normal form)
normal form: model/tip anlamına gelen norm ve form kelimelerinin birleşimidir.

- You can only have one value in a column (virgüllerle aynı sutunda değer olmamalı)
 -You should not create multiple columns for a one to many relationship

> ||| AdresId ||| Name ||| Surname ||| Adres ||| İlçe ||| Calistigi_Ofis |||

Adres2_İl'i eskiden dolu olan satırlar 2 satır olarak ayrı ayrı yazılmak durumunda kalacaklardır.

# 2NF
Her NF, derecesinden düşük NF'leri zaten destekliyor olması gerekiyor.

- (primary key birden fazla sutundan oluşuyor olabilir. bunu gö önünde bulundurarak;) her non-primary sutun; primary sutuna bağlı değilde, sadece 1 parçasına(sutununa) bağlıysa, o parçasına bağlı olduğu sutun ile birlikte farklı bir tabloya alınmalıdır.

Yukarıdaki örnekte primary-key: Name+Surname+Calistigi_Ofis birliktedir. Adres bilgileri sadece Calistigi_Ofis'ya aittir. bu sebeple farklı tabloya taşınırlar.

> ||| Name ||| Surname ||| Calistigi_Ofis |||

> ||| AdresId ||| Adres ||| İlçe ||| Calistigi_Ofis |||

# 3NF

- her non-primary sutun direk olarak sadece primary sutuna bağlı olmalıdır.

Örnekte ilk tablo olmuş 2NF'e uymuş. ikinci tabloda 2nf'e uymuş. bu durumda 3nf'i kontrol etmek gerekmekte. ilk tablo 3 nf'e uymuş. fakat ikinci tablo 3nf'e uymamış. çünkü; ilçe sutunu adresId'ye tam bağımlı değil. zaten bu sebepten tekrarlanabilir veri oluşturuyor. örneğin; ilçe 10 kere tekrar edilebilir o sutunda. ilçe farklı bir tabloya atılmalı.

> ||| Name ||| Surname ||| Calistigi_Ofis |||

> ||| AdresId ||| Adres ||| İlçeId ||| Calistigi_Ofis |||

> ||| İlçeId ||| İlçe |||

# Diğer Form'lar

- Boyce–Codd normal form (or BCNF or 3.5NF)

- 4NF

Fakat en çok ilk üçünden bahsedilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# function vs stored prosedure
fonksiyonlar veritabanında insert, update, delete gibi herhangi bir değişiklik yapacak işlem yapamazlar. bunun sonucu olarak (mantıken); çoğu zaman en az bir parametre alması ve mutlaka bir değer döndürmesi gereklidir.

fakat stored prosedureler veritabanında değişiklik yapabilirler.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Unique Key (or UK) vs Primary Key (or PK)

bir sutun tekil değerler içeriyor ise unique'tir. unique sutunlar null değerler alabilir.

veritabanlarında bir sutunun unique olduğu belirtildiğinde; veritabanı sadece aynı değerlerin kaydedilmesini önleyecektir.

PK ise; veritabanının o sutunu diğer tablolar ile ilişkilendirmek için kullanacağını belirtmek için kullanılır. ilişkilendirme olabilmesi için PK, unique'tir.

Bir taloda Unique sutun birden fazla olabilir. Oysa PK, bir tanedir. PK bazı durumlarda birden fazla sutunu birden kapsamaktadır. Fakat o sutunlar tek başına bir adet PK olarak ele alınır. Yani PK yine bir adettir (fakat birden fazla sutundan oluşur). Bu tarz PK'lara composite (bileşik) sıfatı verilmektedir.

Best practice açısından her tabloda bir primary key olması önerilir.

# surrogate key vs natural key
surrogate kelime anlamı: vekil.

her tablodaki primary key bir bilgiye tekabul etmemesi (surrogate key) best practicedir . örneğin tc (natural key) primary key olmamalıdır. bunun temel 2 sebebi:

- primary key update yapmak zordur (diğer tablolarda aynı anda update gerekir vs) (örneğin kişnini tc'si değişirse, uğdate işlemi zor olabilir)

- privary key'in ömür boyu unique olmayacağı veya hiçbvir durumda null olmayacağının garantisini vermek zordur. bu garanti bugün verilse de yarın bu karar businnes gereği değişebilir. fakat eğer incremental bir ID kullanılsa, businnnes değişikliklerinde primary key'lerde update gerekmeyecek.

Bunun bir dezavantajları:

- sql query'lerinin sürekli olarak primary key'e göre yazılmasını gerektirmektedir. bu sadece manuel yazılan query'lerde diil, programatik query'leri de yoracak. yani performance'ı olumsuz etkileyecek.

- tc örneği üzerinden gidelim. çoğu projede PK index'lenir. PK, sadece tc olsaydı, sadece tc'yi indexleyecektik. fakat surrogate key varsa onunda indexlenmesi gerekecek. bu da db sistemine maliyeti arttıracak.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# primary key generation strategy
performans için önemli bir konu.

```java
@javax.persistence.Id // PK olduğunu JPA'ya bildirir.
@javax.persistence.GeneratedValue(strategy = GenerationType.AUTO) // GeneratedValue, bu field'ın oto-generated value olduğunu tanımlar.
Integer id;
```

GenerationType sınıfının içini incelersek:

```java
package javax.persistence;
/** 
  * Defines the types of primary key generation strategies. 
  *
  */
public enum GenerationType { 
    /**
      * Indicates that the persistence provider must assign 
      * primary keys for the entity using an underlying 
      * database table to ensure uniqueness.
      */
    TABLE, 
    /**
      * Indicates that the persistence provider must assign 
      * primary keys for the entity using a database sequence.
      */
    SEQUENCE, 
    /**
      * Indicates that the persistence provider must assign 
      * primary keys for the entity using a database identity column.
      */
    IDENTITY, 
    /**
      * Indicates that the persistence provider should pick an 
      * appropriate strategy for the particular database. The 
      * <code>AUTO</code> generation strategy may expect a database 
      * resource to exist, or it may attempt to create one. A vendor 
      * may provide documentation on how to create such resources 
      * in the event that it does not support schema generation 
      * or cannot create the schema resource at runtime.
      */
    AUTO
}
```

- AUTO

  GeneratedValue için default "strategy" değerdir.
  
  burada JPA kendisi, hangi GenerationType'ın kullanılacağına karar veriyor. Genelde SEQUENCE seçiliyor.

- IDENTITY

  id değeri entity kayıt edildiğinde DB tarafındna oluşturuluyor. bu sebeple aynı entity'den batch işlemlerinde performance konusunda sıkıntı yaşatıyor, çünkü bir işlem bitmeden, diğer işlemi JPA üstüste yollayamıyor. Burada dikkat: 10 adet liste tek JPA query'sinde DB ye yollanırsa sorun yok. Asıl performans sorunu üstüstü farklı JPA insert query'si yapılırsa oluyor.

- SEQUENCE

  DB'de sequence kavramı var. JPA sequence'den ilgili entity'nin id değerini çekiyor. bu IDENTITY'ye göre daha hızlı. JPA'nın bir kere DB'den sequence'i çekmesi yeterli. Çektiği zaman belli bir dilimi allocate edebiliyor. Bunu da bu şekilde set ediyoruz:

  ```java
  @Id
  @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "sequence1")
  @SequenceGenerator(name = "sequence1", allocationSize = 50)
  private Integer id;
  ```

- TABLE

  JPA'nın kendisi bir tablo oluşturuyor ve bu tabloda sequence'yi tutuyor. Performance için pek tercih edilen yöntem diil. Çünkü JPA'nın Her zaman bu tabloya query atması gerekiyor. Hangi tabloda tuttuğunu entity tarafında belirtmiyoruz. (JPA knfiglerinde belirtiliyor olabilir). Yani biz yine field'ı bu şekilde tanımlıyoruz:

  ```java
  @javax.persistence.Id
  @javax.persistence.GeneratedValue(strategy = GenerationType.TABLE)
  Integer id;
  ```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# sutun indexlemesi
bir sutun indexlendiğinde artık üzerinde daha hızlı querry çalıştırılabilir hale gelir. fakat her update edilişi yavaşlar çünkü indexin de update edilmesi gerekecektir.

```sql
CREATE INDEX my_index_name
ON Persons (LastName)
```

indexi kaldırma işlemi:

```sql
DROP INDEX index_name ON table_name
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# SQL sorguları yaptıkları işlere göre gruplandırılırlar:

DDL (Data Definition Language) --> şemalar üzerinde işlem yapan operatörler: alter, create table gibi

DML (Data Manipulation Language) --> satırlar üzerinde işlem yapmaya yarayan operatörler: SELECT, INSERT, UPDATE gibi

DCL (Data Control Language) --> userların yetkilerini ayarlamak için kullanılan sql operatörleri

TCL (Transaction Control Language) --> Transaction işlemlerinde kullanılan sql operatörleridir: COMMIT, ROLLBACK gibi

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# parsing
DB sunucusu, SQL sorgularını parse edip optimize eder ve execute eder. Bu işleme "__hard parsing__" denir. Oysa aynı sorgunun tekrar tüm bu işlemlere girmesine gerek yok. DB sunucusu, her sql'in optimize edilmiş halini, bellekte tutar. Eğer aynısı gelirse bu sefer "__soft parsing__" yapar ve execute eder.

Oracle db'de büyük küçük harf dahi (örneğin; Select, SELECT) sorgunun farklı olmasına sebep olmaktadır. kaynak: (source-id 106) "Why do bind variables matter for performance?" başlığı.

Buna çözüm olarak sql'lerin elle yazılmaması önerilir. BU eşkilde case-sentitivity sorunu ortadan kalkar. Aynı zamanda 'statement'lara dynamic variable'ları bind ederek'te aynı sql'in farklı değerlerle çalıştırıldığında, hard parsing yapılmamasını sağlamış oluruz. Çünkü; eğer binding yapmazsak; sql aynı fakat içindeki herhangi bir integer farklı ise bile hard parsing yapılır. kaynak: (source-id 106) "Where do bind variables come into this?" başlığı.

Hard parsing ile soft parsing arasında performance olarak büyük fark var. bu kaynakta; (source-id 106) "What's the impact of hard parsing?" başlığındaki örnekte, for loop içerisinde aynı sorgu bind edilerek ve bind edilmeden yollanmış. Bir döngü 4 saniyede tamamlanırken, diğeri 1 buçuk dakikada tamamlanmış.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# mongo db
mongo db'de veri yapıları ve ona denk gelen RMDB karşılıkları aşağıdaki gibidir:

- collection --> tablo
- document -> satır

ilişkiler mondodb'de tutulmamaktadır. fakat bu ilişkiler yazılımsal olarak sağlanabilir.

mongo db de veriler json formatında tutuluyor. json formatı dışında bir tipte değer tutmak gerekirse onu string'e cast edip tutabiliriz. yada database dışında bir yerde tutup, onun URL'sini json string'i olarak saklayabiliriz.

nosql'de standart sql query'ler olmayabilir. örneğin mongodb'de şu şekilde sorular yazılır:

db.users.find( { status: "A", age: { $lt: 30 } } ) gibi sorgu ile sadece tek tablo üzerinde sorgu yapılabilir. $lt değeri aldığı integer değerden daha küçük tüm satırları temsil etmek için kullanılır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# SQL vs OTHERS

#### SQL (or Structured Query Language)
tüm ilişkisel veritabanları için ortak dildir. Tüm sistemlerde çalışabileceği için az özellik içerir.

#### PL/SQL (or Procedural Language/SQL)
Oracle'ın SQL türevi dili.

#### PL/pgSQL
PostgreSQL'ın SQL türevi dili.

#### T-SQL (or Transact-SQL)
Microsoft SQL Server'ın SQL türevi dili.

PL/SQL vs T-SQL -> (source-id: 109) title: "Differences Between Oracle and MS SQL Server".

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# statement
SQL dilindeki her komut (select, update, create, commit ...) ve o komuta yollanan parametreler birlikte 1 statementtir. Her statement noktalı virgül ile ayrılmaktadır. Fakat bazı platformlar noktalı virgül koyulmasını zorunlu kılmaz. yeni satıra geçmek yeterlidir.

1 transaction, sadece 1 statement'ten da oluşuyor olabilir.

sadece 1 statement yolladığımızda, arkaplanda bizim için 1 transaction oluşturuluyor. kaynak: (source-id: 110) "Autocommit transactions" başlığı altında " Each individual statement is a transaction." yazıyor.

# transaction
türkçede kelime anlamı: işlem

multiple statement olmak zorunda diil. tüm sql işlemleri birer transaction'dır ve DB Admin GUI'lere bakarsak "transaction log" (history)'de görürürüz.

# batch (or script)
multiple statement'lar kümesidir. batch, "transaction" gibi atomik olmak zorunda diildir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# BASE
ACID'e alternatif bir özellikler listesidir. Genelde NoSql sistemler bu özelliklere göre çalışır. 3 maddenin kısaltmasıdır:

- __Basically Available__

  sistem sürekli cevap verir (tutarsız data dönse bile)

- __Soft state__

  Sistemdeki veriler yeni input olmasa bile, değişebilir (çünkü diğer veritabanları birbirlerine arkaplanda sync oluyor)

- __Eventual consistency__

  sistem bir süre sonra tutarlı (ilgili query için aynı bilgiyi) bilgi döndürecek hale gelecektir.

# ACID
veritabanı transaction özellikleri (Transaction Properties):

- __Atomicity__: Ya hep ya hiç demektir. Bir transaction içinde bütün işlemler yapılır, ya da biri dahi yapılamıyorsa hiçbiri yapılmaz. rollback özelliğidir. Eğer transaction içinde bir hata olursa sistem en başa dönebilmelidir (yaptıklarını geri alabilmelidir).

- __Consistency (or tutarlılık)__: Yapılan işlemler sonucunda oluşan çıktıların tutarlılığı anlamına gelir. Tutarlılık terimini birçok anlam ifade edebilir. Fakat burdaki anlamı: 

  replica db'ler'deki dataların istenilen şekilde/zamanda (doğru biçimde) klonlanmış olmasıdır. Burada consistency ayarına göre DB hareket edilir. Örneğin; replica db'lere async kayıt isteniyor ise; async, sync kayıt isteniyor ise; o anda diğer klone'lar update olmuş olmalıdır. Buradaki ayar developer'a kalmıştır.
  
  ek not: Consistency sağlanırken; tabiki veritabanındaki ilişkileri (foreign key, primary key) uyuşmazlıkları olmaması, yani istenilen kayıtların istenilen sıra ile kaydedilmiş olması veya daha genel bir tabir ile; verilerin ilişkilerini/yapısını bozacak bir durum olmamalıdır.

  ek not: Consistency'nin birçok farklı biçimleri/türevleri vardır. Bunlar başka başlıkta detaylı şekilde açıklanıyor.

- __Isolation (or izolasyon or yalıtım)__: Transaction gerçekleşirken dışardan müdahaleye izin verilmemelidir. izolasyon seviyelerine göre dğeişiklik gösteren bir özelliktir. örneğin; gerekiyorsa/isteniyorsa kullanılan tablolar or satırlar dışarıdan erişim için bekletilmelidir (lock'lanmalıdır). yada gerekiyorsa/isteniyorsa; dışarıdakiler transaction'ın yazdıklarını okuyabilir, fakat değişiklik yapamaz. izolasyon seviyeleri başka başlıkta detaylı anlatılıyor.

- __Durability (or dayanıklılık)__: işlem client tarafa tamamlandı denildiğinde (commit edildiği onayı geldiğinde), verinin sorunsuzca kaydedildiğini garanti etme özelliğidir. herhangi bir elektrik kesintisinde dahi sistemin kayıt işlemini garanti etmesi gerekir.

# İsolasyon'un olmaması or bazen olması durumunda çıkabilecek problemler:

- __Lost Updates__: Aynı anda birden fazla transaction aynı anda bir veri üzerinde güncelleme yapmak istediği zaman en son işlem yapan transaction ın kaydı geçerli olur. Bu yüzden veri kaybı yaşanır.

- __Dirty Reads__: Bir transaction ın bir veri üzerinde yapmış fakat commit etmemiş olduğu bilgileri diğer transaction tarafından gerçek kayıtmış gibi okuması durumudur. Buna "__read uncommited__" da denir.

- __Non-Repeatable Reads__: Bir transaction bir veriyi okusun ve kendi içinde işleme soksun. Bu transaction commit etmeden başka bir transaction bu veriyi okusun. Daha sonra işlem yapan transaction tekrar veriyi okumak istediğinde veri, aynı veri olmayacağı için sorun yaşanmaktadır.

- __Phantom (hayalet) Reads__: Aynı anda çalışan transaction düşünelim.Bir transaction bir tablodaki verilerin tamamını çeksin ve kendi içindeki işleme soksun.Bu sırada da diğer transaction aynı tabloya veri ekleme işlemi yapsın.Daha sonra ilk transaction tekrar verileri çekmek istediğinde yeni eklenen veriler hayalet veri olarak görünür.

# Isolation levels:
ANSI ve ISO SQL standratlarının belirlediği 4 çeşit izolasyon tipi mevcuttur. Bunlara ek olarak her database farklı seviyeler sunabilir.

Burada sade bir anlatım mevcut: (source-id: 111)

JPA'da aşağıdaki gibi her transaction işlemi için isolasyon seviyesi verebiliriz. Eğer hiç isolasyon seviyesi kullanmazsak, JPA default olarak database'in isolasyon seviyesini kullanmaktadır.

```java
@Transactional(isolation = Isolation.REPEATABLE_READ)
```

İsolayson seviyelerini okumadan önce bu 2 terimi bilmek gerekli:

- # read lock
  eğer bir satır (yada tablo) "read lock" olarak flag'lendiyse, o satır okunabilir fakat yazılamaz(update edilemez).

- # write lock
  eğer bir satır (yada tablo) "write lock" olarak flag'lendiyse, o satır okunamaz veya yazılamaz(update edilemez).

İsolasyon seviyeleri:

- # Read Uncommited (level 0)

  bu level'da bir transaction işlem yaparken yaptığı her değişikilik diğer transaction'lar tarafından görülebilir.

  Aynı zamanda, write-lock'lu dataları dahi okur. kaynak: (source-id: 112) "Arguments" başlığı, "READ UNCOMMITTED" altbaşlığı, ilk cümle.

  - engelleyemeği sorunlar: Dirty + Non-Repeatable + Phantom

- # Read Commited (level 1)

  Diğer transaction'ların ellediği data'lardan bilgi okurken read-lock ve write-lock'u önemser.

  bu level'da bir transaction işlem yaparken kullandığı satırları;

  - eğer okuyorsa, read locked olarak flag'ler
  - eğer güncelliyorsa, write lock olarak flag'ler

  Eğer, read yaptığı SQL parçacığından sonra başka SQL parçacığı ile okuma yapmak istediğinde (when it moves off the current row), o zaman eski okuduğu satırlardaki "read lock" flag'i kaldırılır. Fakat bu durum güncellediği satırlar için geçerli dğeildir. Güncellenen satırlardaki "write lock"'lar transaction sonlanana kadar kalırlar.

  Yukarıdaki paragraftaki "SQL parçacığı"; "each statement" olarak düşünülmelidir. kaynak: (source-id: 112) "Arguments" başlığı, "REPEATABLE READ" altbaşlığı, ikinci paragraf.

  - engellediği sorunlar: Dirty
  - engelleyemeği sorunlar: Non-Repeatable + Phantom

- # Repeatable Read (level 2)

  "Read Commited (level 1)" ile aynıdır. Tek fark: Level 1, read yaptığı tüm böylgeleri transaction sonuna kadar "read locked" olarak işaretler.

  - engellediği sorunlar: Dirty + Non-Repeatable
  - engelleyemeği sorunlar: Phantom

- # Serializable (level 3)

  Repeatable Read (level 2) ile aynıdır. Tek fark şudur:
  
  - level 2; "shared lock" kullanırken,
  - level 3; "Range lock" ile range'leri lock'lar. kaynak: (source-id: 112) "Arguments" başlığı, "SERIALIZABLE" altbaşlığı, 2'inci paragraf ilk cümle.

  Shared lock'ta yeni ilgili data'lar (range içerisine dahil olan data'lar) diğer transaction'lar tarafından modify edilemesede, iligli range arasına yeni satır eklenebilir. Oysa "range lock" ta bu durumda engellenmektedir. kaynak: (source-id: 112) "Arguments" başlığı, "SERIALIZABLE" altbaşlığı, 3üncü madde ve 2inci paragraf 2inci madde.

  - engellediği sorunlar: tümü
  - engelleyemeği sorunlar: yok

# locking mechanism

# usage in JPA
JPA her transaction için hangi lock modu'unu kullanabileceğimizi belirlememize izin veryor. kullanım örnekleri:

```java
// entityManager Find
entityManager.find(Student.class, studentId, LockModeType.OPTIMISTIC);

// Query
Query query = entityManager.createQuery("from Student where id = :id");
query.setParameter("id", studentId);
query.setLockMode(LockModeType.OPTIMISTIC_INCREMENT);
query.getResultList();

// explicit Locking
Student student = entityManager.find(Student.class, id);
entityManager.lock(student, LockModeType.OPTIMISTIC);

// refresh (it updates the lock mode)
Student student = entityManager.find(Student.class, id);
entityManager.refresh(student, LockModeType.READ);

// NamedQuery
@NamedQuery(name="optimisticLock",
  query="SELECT s FROM Student s WHERE s.id LIKE :id",
  lockMode = WRITE)
```

# locking types

Aşağıdaki tüm lock çeşitleri sadece JPA/veritabanı konusunda kullanılmazlar. Genel bilgisayar bilimleri konularıdır.

- # optimistic vs pessimistic
  bu lock çeşitleri, genel bilgisayar biliminde de kullanılan terimlerdir. Optimistic lock'ta lock'lanmış bir satırı, herkes çekebilir fakat herhangi bir thread bunu update etmeye kalktığında, eğer başkası önceden update etmiş ise, hata alır. Yani mutlaka; ancak ve ancak en güncel hali update edilebilir ve ilk update eden kazanır mantığı vardır. Oysa pessimistic lock'ta ilgili satır direk olarak lock'lanır ve kimse hiçbir şekilde o satırın lock'ı kaldırılana kadar ilgili satırı update edemez. Yani ancak ve ancak tek bir thread (lock'layan thread) ilgili satırı update edebilir.

- # optimistic locking
  Entity'mizde (tablomuzda) @Version tagini almış bir sutun olmalıdır. JPA bizim için bu sutunu otomatik yönetir. Her sutun değiştiğinde bu sürüm arttırılır. DB'deki ilgili satırımızın sürümü 5 olsun. Daha sonra bir transaction gelip bu satırı update etmeye kalktığında, eğer transaction verisi sürüm 4 ise OptmisticLockException alacaktır. Ancak 5'incisi sürüme sahip bir transaction o satırı update edebilir.

  Optimistic locking için version'lama yerine farklı yöntemlerde kullanılabilir. örnek versiyon yerine, timestamp te atanabilir. aynı timestamp diilse bizim versiyon diildir kontrolü kurulabilir.

  Optimistic locking tamamen yazılımsal katmandaki logic ile yapılan bir özelliktir. DB'nin desteklemesi gerekmez. dolayısı ile aşağıdaki 2 lock modu'unda da veritabanı seviyesinde lock mekanizması kullanılmaz.

  JPA, Optimistic lock için 2 tür mode sunar:

  - __OPTIMISTIC__ veya __READ__ (enum'lar aynı yere referans eder)

    veri update edildiğinde versiyon numarası yükseltilir.

  - __OPTIMISTIC_FORCE_INCREMENT__ veya __WRITE__ (enum'lar aynı yere referans eder)

    OPTIMISTIC enum'u ile aynı mantıkta çalışıyor, fakat ek olarak; veri okunduğunda dahi versiyon numarasını arttıyor. Bu mode; bir datayı okuduğumuzda onu serbest bırakana kadar bakaları tarafından güncellenememesini sağlar. çok önemli datalar gösterildiğinde bu kullanılabilir.

- # pessimistic locking
  pessimistic kelime anlamı: kötümser

  database'in lock mekanizmasını desteklemesi gerekir. JPA bir satır okunduğunda, o satırı database tarafında lock konumuna geçirir. locklanan satır diğer uygulamalar tarafından okunamaz. 

  JPA'daki çeşitleri:

  - __PESSIMISTIC_READ__

    locklanan entity diğer transaction'lar tarafından okunabilir fakat değiştirilemez. 
    
  - __PESSIMISTIC_WRITE__

    locklanan entity diğer transaction'lar tarafından okunamaz.

  - __PESSIMISTIC_FORCE_INCREMENT__

- # semantic lock
  semantic kelime anlamı: anlamsal

  DB'deki bir kaydı lock'lama yöntemleri kullanmak yerine, o kaydın statüsünü değiştirip, diğer uygulamaların bu statü'ye bakarak (anlamlandırıp), ilgili kaydı güncellemesini bilmesi gerektiği akışlara denir. yani; tamamen uygulama seviyesinde olan; özel bir lock mekanizması olmayan, uygulamamızın businnes logic katmanında birbirlerinin kayıt atmaması gerektiğini ayarlamaktadır.

  örneğin Order'ımız pending statüsündeyse, gün sonu işleminin bu satırı hiçbir şekilde update etmemesi buna örnek verilebilir. Çünkü gün sonu işlemleri ancak ve ancak tamamlanmış siparişler üzerinde çalıştırılabilir.
