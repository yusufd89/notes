############################

############################
# DATABASE CASSANDRA
############################

############################

# cassandra
cassandra yazılımı, apache foundation tarafından ücretsiz ve açık kaynaklı olarak sunulmaktadır. __DataStax__ firması apache'nin repo'sunu base alarak; "__DataStax Enterprise (or DSE)__" isminde ürün sunmaktadır. __DataStax__ hem ücretli hem ücretsiz versiyon içermektedir. __DataStax__ sadece ek özellikler sunar ve teknik support verir. bu linkte ikisinin farkları açıklanmaktadır: (source-id: 123)

cassandra Java'da yazıldığı için runtime'da JVM'e ihtiyaç duyar.

- cluster içindeki node'lar arasında master-slave ilişkisi yoktur. onun yerine __ring design__ söz konusudur. Bu durum "No Single Point of Failure" olmasını sağlamaktadır. her node isteklere cevap verebilecek tasarımdadır.
- cassandra cluster yapısı içerisinde "ring design" ile haberleştiği için "cluster" terimi yerine "ring" terimi de kullanılmaktadır.
- multi data center supportu default olarak vardır. yani; wan üzerinden dahi, aynı cluster'a bağlı cassandra node'ları birbiri arasında paylaşım yapabilir. bunun için ek bir servise ihtiyaç yoktur. bu özellik cassandra sunucularında default gelir.
- client cluster içerisindeki herhangi bir node'a istek yapabilir. Client'ın attığı isteği ilk alan node'a __coordinator (or koordinatör)__ ismi verilir. eğer bu istek query isteği ise; return data'sı kordinatörde yok ise; kordinatör arkaplanda bu datayı diğer node'lara sorarak dönüş yapar. eğer istek kaydetme isteği ise; coordinatör fiziksel olarak o data'yı kaydedecek olan node'lara isteği yollar.
- __Ayarlanabilir Veri Tutarlılığı Seviyesi (or Consistency Levels)__: Veri tutarlılığı seviyesi, okuma isteğinin kaç sunucudan veri alarak cevaplanacağını ve yazma isteğinin kaç sunucuya veri yazıldıktan sonra istemciye "tamamlandı" olarak dönüleceğini belirler. Örneğin kopya sayısı 10 olan bir kümeye gelen yazma isteğinin tutarlılık seviyesi 3 ise, gelen veri 3 sunucuya yazıldıktan sonra (kalan 7 sunucuya kopyalama devam ederken)  istemciye "tamamlandı" olarak dönülecektir. Cassandra veritabanında veri tutarlılığı seviyesi küme ve sorgu bazında ayarlanabilir.
- eğer client data manipülasyonu yapacak istek yollarsa sırası ile şunlar işletilir:
  - Cassandra node'u gelen isteği fiziksel bellekte olan "commit log"'a kaydeder
  - client'a "commited" mesajını döner
  - data'yı __Memtable__ denilen hızlı hafızadaki bölgeye taşır
  - data'yı olması gereken yere taşır. yani sorting'e göre olması gerektiği yere taşır. En son taşınan bölgeye __SSTable__ adı verilir.
- Okuma işlemlerinde ise önce node'daki Memtable'a bakılır, eğer yok ise SSTable'a bakılır. kaynak: (source-id: 124) 1inci paragraf.

# insert into vs update
"insert into" işlemi if not exist özelliği içermiyor ve varsa aynı id'li data'yı override ediyor. Bu durumda "insert into" ile "update" aynı görevi görüyor. fakat ikisi arasında ufak farklılıklar var. buradaki gibi: (source-id: 125) answer of billbaird at "May 16 '14 at 23:04". Stackoverflow'da billbaird'in bahsettiği konunun bug olmadığını gösteren kaynak: (source-id: 126)

cassandra "lock" mekanizmasını desteklemez. (oysa bu durum distributed sistemlerde bu önemli bir gereksinimdir.)

Client cassandra'ya bir kayıt isteği attığında cassandra hızlı dönüş yapabilmek için önce commit log'a yazar ve client'a dönüş yapar (bu konu başka başlıkta detaylı anlatılıyor). işte performance avantajı burda. commit log'daki data daha sonra gerekli yere fiziksel olarak taşınır. Burada ince bir nokta var: Commit log'a sadece kayıt atılabiliyor. İşte bu sebeple cassandra'da update ve insert işlemi aynı şeye denk geliyor. Aynı sebepten, cassandra "lock" mekanizması da destekleyemiyor. Çünkü commit log'a herhangi bir client bir bilgi atabilir. commit log hiçbir kontrol içermiyor. Bu sebeple çok hızlı. Eğer kontroller gelirse performance kaybı olur. Bu durumda farklı DB server'ları kullanmamız daha avantajlı olur. Cassandra zaten generic purpose bir DB değil. Bazı durumlarda kullanmak gerekiyor.

Cassandra read-before-write'tan kaçınır. kaynak: (source-id: 127) ilk 2 paragraf.

Cassandra ek olarak istisna durumlar için "if not exist" gibi özellikleri  lightweight transactions (or LWT) isimli bir özellik ike destekliyor fakat bu pek önerilmiyor. kaynak: (source-id: 127) 2inci paragraf.

# SSTables
cassandranın yazma hıznın yüksek olmasının sebeplerden biridir. SSTables'lar birer fiziksel dosyadır. her dosya immutable'dır. yani; dosyanın içeriğini update edilmez. memtable direk olarak SSTable olarak fiziksel olarak saklanır. (source-id: 129) kaynak: title: "Storing data on disk in SSTables", 1st paragraph.

Bu sebeple cassandra'da silme veya update işlemi gerçekten fiziksel kaydı silmez/değiştirmez. Silme veya update işlemi de yeni bir row'dur(kayıttır). update edilen kayıt (row) okunacağı zaman her zaman en sonki kayıt okunur.

SSTables'ların sayısı arttırkça, cassandra arkaplanda işe yaramayan row'ları (kayıtları) ignore eder/siler ve hala kullanılması gereken kayıtları yeni SSTable'lara merge eder. Bu işleme "compaction" denir.

Silme işleminde, silmek için atılan yeni kayıt'a tombstone (mezar taşı) adı verilir. Tombstone ile işaretlenen kayıtlar compaction ile sinir ve beraberinde tombstone'larda silinir.

# cassandra vs mongdoDB
Burada birçok detay farklılık çıkabilir. Fakat tüm sebepler aşağıdaki temel farklılıkalrın sonucunda ortaya çıkmaktadır:

- # cluster yapısı
mongoDB'de auto-election özelliği var. Tek bir mongodb instance'ı isteklere cevap döner (master node). Diğer node'lar (slave node'lar) arkaplanda güncel data'lara sync olur. Eğer master node çökerse, auto-election devreye girer ve diğer node'lerden biri master olur. Burada ortalama 12 saniye zaman kaybı yaşanacaktır fakat isteğe bağlı olarak bu arada read-query'lerine cevap verilebilir. kaynak: (source-id: 130). Bazı kaynaklarda bu sürenin ortalama 1 dk olduğu yazar. kaynak: (source-id: 131) "Data Availability" başlığı. Oysa cassandra'da master-slave ilişkisi yoktur. her node eşit miktarda data'yı fiziksel olarak barındırır (tabi bazı data'lar yine bu node'lar arasında yedekli şekilde barındırılır). gelen isteğe cevap verecek data yok ise; diğer node'a istek yönlendirilir. Eğer isteği alan node çökerse, diğer node'lar isteğe cevap zaten veriyor durumdadır. Auto-election gibi bir sürece ihtiyaç yok.

MongoDB'de slave node'lar (eğer istenirse/ayarlanırsa) read isteklerine cevap verebildiği için read'ler açısından cassandra ve mongodb aynı performansı sergiliyor diyebiliriz. Fakat iş yazmaya geldiğinde cassandra çok daha üstün performance sergiliyor. Çünkü mongo'da sadece master node yazma işlerini hallederken, cassandra'da tüm node'lar bu görevi aynı anda üstleniyor.

- # join queries
Cassandra'nın yapısı gereği SQL dilindeki join gibi özellikler çalışmamaktadır. Aynı zamanda where ile sorgu her sutun için yapılamamaktadır. Bu sebeple sorgularda kısıtlamalar yaşanmaktadır. Benzer sebeplerden her sutuna index'te atılamamaktadır. (Aslında bu paragrafta belirtilenler cassandra ile de yapılabilir, fakat eğer yapılırsa cassandra kullanmanın hiçbir manası kalmaz.). Oysa mongo-db zaten nested dökümanlarla çalıştığı için onlar içerisinde gelişmiş sorgular yapabilmemizi destekliyor.

- # scheme
Cassandra'da tablo yapısı (şeması) önceden belli/sabit iken, mongo db'de böyle bir limit yoktur. mongo-db'de şama opsiyonel'dir.

Hatta mongodb'de bir field farklı kayıtlarda farklı tipte (int, string...) olabilir. kaynak: (source-id: 132) title: "Flexible Schema", 1inci madde.

- # nested objects
mongo-db'de, içiçe (nested) json objeler tutulabilir. Oysa cassandra'da böyle bir imkan yoktur. Cassandra'da içiçe bilgi yerine, aynı tabloda farklı sutunlara yazmak gerekiyor. Örneğin:

mongo db:

```
order : {
  order_id: "99",
  order_date : "01 01 2012"
  user : {
    user_id: "123",
    user_name: "ahmet"
    user_surname: "karaoglu"
  }
}
```

cassandra db:

```
order : {
  order_id: "99",
  order_date : "01 01 2012"
  user_id: "123",
  user_name: "ahmet"
  user_surname: "karaoglu"
}
```

Cassandra'da daha sonradan "collection" yapıları geldi.

collection'lar bir field'ın içinde map, list tutabilmemizi sağlıyor. fakat gerçek bir sutun gibi çalışılmasını sağlamıyor. limitasyonlar var. kaynak: (source-id: 133) Frozen olan collection'larda, frozen olan tüm collection update edilirken, tüm bilgiler güncelleniyor. frozen data'lar binary data olarak saklanıyor. Frozen olan collection'larda limitasyonlar çok daha fazla.

MongoDB terminolojisinde tek döküman içinde olan diğer (nested / içiçe) dökümanlara __embedded document__ adı verilir. ve Embedded dökümanlar native olarak mongo-db tarafından desteklenir. Embedded kullanmak işlemleri hızlandırır fakat data dublication'ı arttırır. Onun yerine reference (mongo db terminolojisinmde DEBRef) kullanılabilir fakat o zaman query'ler yavaşlar fakat dublication azalır. Aynı durum cassandra için de vardır. Fakat cassandra nested veya reference'ları native olarak desteklemez. Onun yerine Cassandra'yı kullanan yazılımın bunu manuel yapması gerekir.

# cassandra veri yapısı
- __Keyspace__, relational-db'deki şemaya veya veritabanına denk gelmektedir. en üst seviyeli db kavramıdır.
- __column family__, relational-db'deki tabloya denk gelmektedir. java'da şu objede tutulur:

  > Map<RowKey, SortedMap<ColumnKey, ColumnValue>>

  > Map<ParitionKey, SortedMap<ColumnKey, ColumnValue>> (daha ilerde ne oldukları anlatılıyor) kaynak: (source-id: 134) "Column family" başlığı.

  Her satır RowKey ile temsil edilir. Her satır'da birden fazla column-key ve her column-key'e denk gelen value vardır.

  Aslında bakıldığında relational-db'de de aynı şekilde data'yı temsil edebiliriz: her satırın mutlaka bir id'si olsun. her satırda, bir sutuna karşılık gelen bir değer vardır. (bu konu başka başlıkta anlatılıyor: "column family")

- __colum key (or column name)__ relational-db'deki sutun ismine denk gelmektedir. her column key'e karşılık gelen bir de __column value__ vardır.

- __Cassandra Query Language (or CQL)__ dili ile query atılır. sql'e çok benzerdir. __Cassandra query language shell (or cqlsh)__ komut satırı uygulaması ile bu query'ler atılabilir. CQL'de hala 'table' gibi terimler kullanılıyor. cqlsh, shell/bat script'idir fakat kendi içerisinde python'u çağırır.

# cassandra java client example

```xml
<dependency>
    <groupId>com.datastax.cassandra</groupId>
    <artifactId>cassandra-driver-core</artifactId>
    <version>3.1.0</version>
</dependency>
```

```java
public class CassandraConnector {
 
    private Cluster cluster;
 
    private Session session;
 
    public void connect(String node, Integer port) {
        Builder b = Cluster.builder().addContactPoint(node);
        if (port != null) {
            b.withPort(port);
        }
        cluster = b.build();
 
        session = cluster.connect();
    }
 
    public Session getSession() {
        return this.session;
    }
 
    public void close() {
        session.close();
        cluster.close();
    }
}
```

Keyspace yaratan bir metod yazalım:

```java
public void createKeyspace(String keyspaceName) {

  String queryStr = "CREATE KEYSPACE IF NOT EXISTS " + keyspaceName + 
                    "WITH replication = {'class':'SimpleStrategy','replication_factor':'2'};";

  session.execute(queryStr);
}
```

Dikkat edilirse her keyspace için ayrı ayrı replica sayısını verebiliyoruz. Eğer replica vermezsek; 1 satır 1 node'da yer alır. Fakat o tablonun her satırı aynı node'da olmak zorunda diildir. Cassanra node'ları her satırı kendi arasında paylaşmaktadır. Eğer tablonun recplica sayısını 2 yaparsak, her satır mutlaka 2 node'da olacaktır.

Yukarıdakinden daha farklı stratejiler mevcut. Örneğin; "NetworkTopologyStrategy". (başka başlıkta anlatılıyor)

Check all keyspace list:

```java
ResultSet result = session.execute("SELECT * FROM system_schema.keyspaces;");

List<String> allKeyspaceList = result.all()
```

Create a column family query

```sql
CREATE TABLE IF NOT EXISTS books
(
  id uuid PRIMARY KEY,
  title text,
  subject text
);
```

# database design patterns (mostly used on Cassandra)

- # one table per query pattern (or one-table-per-query pattern) vs query-first approach (or query-driven modelling)
Aralarında farklılıklar var. Cassandra kullanırken çoğu zaman "one table per query pattern" yaparız fakat bu en optimum çözümü bulduğumuz anlamına gelmez. en optimum çözüm 'query first approach'tur.

table per query pattern'i açıklamak gerekirse: selectByTitle sorgumuz için özel bir tablomuz olsun: "booksByTitle". Durum böyle olunca duplicate data'larımız tüm veritabanında çoğalıyor. fakat bu durum cassandra'da okumada performans artışı sağlanıyor. Artık her yeni kayıt işlemlerimizde bir 'book' ve 'booksByTitle'a ekleme yapmamız gerekecek.

query first approach; ise farklıdır. buradaki fark; query first approach'ta bazen çok benzer query'leri aynı tabloya atabilmemizdir. Sadece where koşulu değişebilir... çünkü  bazı durumlarda önceliği düşük sorgular için dublica data olmamasını hza terchi edebiliriz. Böyle durumlarda primary key birden fazla sutuna olur.

Ek not: Cassandra'da tablo isimlendirmeleri şu şekilde olmalı: user_by_name, users_by_id, reservations_by_user_id..

- # time series pattern
activity log olarak düşünebileceğimiz tablolardır. "money_transaction" tablosu buna en temel örneklerden biridir. blockhain mantığı gibi silinen data olmaması gerekir.

- # wide partition pattern (or wide row pattern)
ilişkili data'ların aynı partition'da tutulup, bu şekilde tek bir sorgu ile hızlı çağrılması pattern'idir.

# Chebotko notation
Artem Chebotko'nun geliştirdiği Cassandra için tablo gösteriminde kullanılan notasyondur. temelde şu şekildedir:

```
Q1 (Find User by name)
        ↓
*************************           *************************
*     users_by_name     *           * users_by_school_name  *
*************************           *************************
* user_name          K  *           * school_name        K  *
* user_last_name     C↑ *           * school_city        C↑ *
* user_id            C↓ *           * school_level          *
* user_address          *  --> Q2   *************************
* school_name           *     (Find 
*************************      school by name)
```

Q1 ve Q2 application flow'una göre sırası ile yapılacak isteklerdir.

Yukarıdaki tablo notasyonuna göre joinleme kısmı application client tarafında yapılması beklenir.

K primary key'i temsil eder.

C↑ clustering key'i temsil eder. ASC sorting yapar.

# partitioning key vs clustering key

Simple bir tablo yaratmaya bakalım:

```sql
create table simple_table (
    TC_NO int PRIMARY KEY, -- partitioning key: TC_NO
    TELEFON int 
);
```

Şimdi ise __composite key (or compound key or bileşik anahtar)__ olan tablo yaratalım:

```sql
create table table1 (
      TC_NO int,
      TELEFON int,
      DOGUM_YILI int,
      PRIMARY KEY(TC_NO, TELEFON) -- partitioning key: TC_NO, Clustering Key: TELEFON
);
```

PRIMARY KEY parantezinin içindeki ilk kısım __partitioning key__'dir. Where koşulları ile data çekerken bu key şarttır. Çünkü cassandra node'ları artık partititoning key'e göre dışardan aramaya hizmet vermektedir. 

Örneğin TC'si 0-999 arasındaki satırlar node1'de, 1000-1999 arası satırlar node2'de bulunuyor. Her node toplamda eşit sayıda satırları barındırıyor. Bu şekilde denge sağlanmış oluyor. Cassandra bir satıra ait tüm primary key'lerin birlikte hash'ini alır ve buna göre node'lara dağıtır. Hash çıktısı standart olduğundan (belli boyutta uzunluğu, çıktıdaki olabilecek karakterler kümesi/çeşitliliği...), her node'a dağıtma işlemini kümeleyip/mapping yapabilir. (cassandra hash algoritması olarak non-kriptografic hash metodları kullanılır) kaynak: (source-id: 134) "Partition key" başlığı 3üncü paragraf. + kaynak: (source-id: 136) "Node, Start range, End range" içeren tablo.

Primary key 2 kısımdan oluşur. ilk kısım partition key, ikinci kısım __clustering key__ olarak değerlendirilir. partition key birden fazla olduğunda parantez içerisine alınmalıdır. clusterin key'lere göre sorting yapabiliriz anlamına gelir. her satır clustering key'lere göre fiziksel olarak sorting yapılarak tutulur. Örneğin TC'si 0-999 arasındaki satırlar node1'de olsun. node1 içerisinde fiziksel olarak TELEFON numarasına göre sorting yapılmış şekilde tüm satırlar tutulur.

Diğer örnekler:

```sql
create table table2 (
      TC_NO int,
      TELEFON int,
      DOGUM_YILI int,
      OLUM_YILI int,
      PRIMARY KEY((TC_NO, TELEFON), DOGUM_YILI) -- partitioning key: TC_NO ve TELEFON, Clustering Key: DOGUM_YILI
);
```

```sql
create table table3 (
      TC_NO int,
      TELEFON int,
      DOGUM_YILI int,
      OLUM_YILI int,
      PRIMARY KEY(TC_NO, TELEFON, DOGUM_YILI) -- partitioning key: TC_NO, Clustering Key: TELEFON ve DOGUM_YILI
);
```

Where koşullarında partition key'deki tüm elemanları girmek zorunludur. Yani table2'de TC_NO ve TELEFON (ikisi ile birlikte) ile where sorgusu yapmak zorundayız. table2 için örnek vermeye devam edersek; Where koşuluna, ek olarak; DOGUM_YILI da kullanılabilir. fakat zorunlu değildir. DOGUM_YILI sortlandığı için hızlı dönüş sağlayacaktır. kaynak: (source-id: 134) "A note about querying clustered composite keys" altında "valid queries" örnekleri.

# blob
cassandra'nın byte array data tipidir. Java'da bu data mapping yapıldığında ByteBuffer olarak tutulmalıdır. kaynak: (source-id: 138)

# Cassandra write consistency levels

Aşağıdaki tüm bilgiler için kaynak: (source-id: 139) Aynı linkte 'read consistency'ler yazmaktadır.

Güncel casssandra'da, consistency level CQL komutunda verilemiyor. CQL'deki "WITH CONSISTENCY" kullanımdan kaldırıldı. consistency level programatik olarak driver seviyesinde, yada sunucu tarafta cluster veya data-center seviyesinde yada per-operation basis (for example insert or update) seviyesinde ayarlanabiliyor.

| Level        | Description                                                                                                                                                                                                                                                                                                        | Usage                                                                                                                                                                                                                                                                                                                                          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ALL          | A write must be written to the commit log and memtable on all replica nodes in the cluster for that partition key.                                                                                                                                                                                                 | Provides the highest consistency and the lowest availability of any other level.                                                                                                                                                                                                                                                               |
| EACH_QUORUM  | Strong consistency. A write must be written to the commit log and memtable on a quorum of replica nodes in all data center.                                                                                                                                                                                        | Used in multiple data center clusters to strictly maintain consistency at the same level in each data center. For example, choose this level if you want a read to fail when a data center is down and the QUORUM cannot be reached on that data center.                                                                                       |
| QUORUM       | A write must be written to the commit log and memtable on a quorum of replica nodes.                                                                                                                                                                                                                               | Provides strong consistency if you can tolerate some level of failure.                                                                                                                                                                                                                                                                         |
| LOCAL_QUORUM | Strong consistency. A write must be written to the commit log and memtable on a quorum of replica nodes in the same data center as thecoordinator node. Avoids latency of inter-data center communication.                                                                                                         | Used in multiple data center clusters with a rack-aware replica placement strategy, such as NetworkTopologyStrategy, and a properly configured snitch. Use to maintain consistency locally (within the single data center). Can be used with SimpleStrategy.                                                                                   |
| ONE          | A write must be written to the commit log and memtable of at least one replica node.                                                                                                                                                                                                                               | Satisfies the needs of most users because consistency requirements are not stringent.                                                                                                                                                                                                                                                          |
| TWO          | A write must be written to the commit log and memtable of at least two replica nodes.                                                                                                                                                                                                                              | Similar to ONE.                                                                                                                                                                                                                                                                                                                                |
| THREE        | A write must be written to the commit log and memtable of at least three replica nodes.                                                                                                                                                                                                                            | Similar to TWO.                                                                                                                                                                                                                                                                                                                                |
| LOCAL_ONE    | A write must be sent to, and successfully acknowledged by, at least one replica node in the local data center.                                                                                                                                                                                                     | In a multiple data center clusters, a consistency level of ONE is often desirable, but cross-DC traffic is not. LOCAL_ONE accomplishes this. For security and quality reasons, you can use this consistency level in an offline datacenter to prevent automatic connection to online nodes in other data centers if an offline node goes down. |
| ANY          | A write must be written to at least one node. If all replica nodes for the given partition key are down, the write can still succeed after a hinted handoff has been written. If all replica nodes are down at write time, an ANY write is not readable until the replica nodes for that partition have recovered. | Provides low latency and a guarantee that a write never fails. Delivers the lowest consistency and highest availability.                                                                                                                                                                                                                       |
| SERIAL       | Achieves linearizable consistency for lightweight transactions by preventing unconditional updates.                                                                                                                                                                                                                | You cannot configure this level as a normal consistency level, configured at the driver level using the consistency level field. You configure this level using the serial consistency field as part of the native protocol operation. See failure scenarios.                                                                                  |
| LOCAL_SERIAL | Same as SERIAL but confined to the data center. A write must be written conditionally to the commit log and memtable on a quorum of replica nodes in the same data center.                                                                                                                                         | Same as SERIAL. Used for disaster recovery. See failure scenarios.                                                                                                                                                                                                                                                                             |

## quorum
kelime anlamı: yeterli çoğunluk

Bu değer şu şekilde hesaplanıyor: (sum_of_replication_factors / 2) + 1
