############################

############################
# DATABASE NOSQL TERMINOLOGY
############################

############################

# NoSQL (or Not Only SQL) vs Relational Database Management System (or RDBMS or İlişkisel veri tabanı yönetim sistemi)
nosql; foreign key olmadan kullanılan veritabanlarına optimize edilmiştir. Oysa relational-db'lerde foreign key tutmaya göre optinize edilmiştir. eğer tutulmayacaksa zaten nosql kullanmak daha mantıklı olacaktır.

nosql db forign-key gibi ilişkilerin olmayacağı anlamına gelmez. nosql bir veritabanında foreign key de olabilir. örnek: mongodb'deki "DBRef" özelliği.

Nosql veritabanları kendi içlerinde çok farklı mantıklarda çalışabilmektedirler. kimisinde bir özellik yok iken, diğerinde mevcut olabilir. işleyiş, data tutma biçimleri çok çok farklı olabiliyor.

nosql şema olmadığı anlamına gelmiyor. şema kontrolü istenirse application seviyesidne veya veritabanı seviyesinde yapılabilir (her nosql veritabanı şema kontrolü özelliği desteklemek zorunda diildir).

("partitioning vs sharding" konusu farklı yerde anlatılıyor.) Nosql db'lerde ilişkiler yapılması mantıksız olduğu için kullanılmaz. bu sebeple bu avantajları sağlar:
- ilişki yerine datanın kendisi ilişkilerle birlikte atomik olarak tutulduğu için, bir tablodaki data'lar farklı DB instance'larında çok kolay tutulabiliyor. Yani; nosql, RDBMS'e göre sharding konusunda çok büyük kolaylıklar sağlıyor.
- ilişkiler olmadığı için şemalarda değişiklik yapmak RDBMS'e göre çok kolaydır.

# nosql database tipleri

- # Document-Oriented store
Her nesneyi (id'si olan bir nesneyi) ayrı birer (tek) döküman gibi saklar. örnek sistemler: MongoDB

- # Key-Value store
Bilgiler bir anahtar ve karşılığında bir değer şeklinde saklanıyor. genelde çok fazla işlem ama ufak verileri saklamak için kullanılan sistemlerde kullanılıyor (örneğin; caching).

key-value sistemler farklı veri yapıları (hash-map gibi) da içerebilir, yada verilerin (value'ların) tipini (int, string...)'de yönetebilir.

örnek sistemler: Hbase, Cassandra, Riak, Berkeley DB, Redis

- # Graph store
Kayıtlar, graph(structure çeşidi) ile ilişkilendirilmiş şekilde tutulmaktadır. bu ilişkiler, relational database'lerdeki ilişkilerle aynıdır fakat foreign key tarzı kavramlar yoktur.

sosyal network ağı gibi bilgilerin tutulmasında kullanılırlar. ahmet'in like'ladıkları, ahmetin dislike'ladığı, ahmetin arkadaşları...

örnek sistemler: Neo4J, Giraph

- # others (which includes "column" word)
bu gruba giren örnek sistemler: Bigtable, HBase, Hypertable, Cassandra, Sybase IQ, C-Store, Vertica, VectorWise, MonetDB, ParAccel, Infobright.

burada terminoloji karmaşası söz konusudur. Bu kaynakta yorumları da dahil olmak üzere çok verimli bilgiler mevcut: (source-id: 407)

"column" içeren no-sql terimleri aşağıda açıklanmıştır:

  - # column-oriented
    bu terim RDBMS dünyasında farklı amaçla kullanılan bir terimdir.

  - # wide-column store (or extensible record store)
    __wide-column__ sistem; her cell (hücre)'nin value'su için farklı sürüm değerleri saklar. time-series pattern'i de buradan gelir. Bu sebeple; __wide-column__ store'lar  "__three-dimensional structure__ (bazen "__multi-dimensional__" denir)" olarak, documen-based store'lar ise "two-dimensional structure" olarak nitelendirilirler.

  - # column-store
    column-store bir sutun'a ait (belli range'lerdeki veya tüm) dataların fiziksel olarak ardarda kayıtlı olduğu sistemlerdir. daha doğrusu; her hücrenin hangi satıra ait olduğu bilgisinin direk olarak store'a yazılmayan sistemlerdir. bu tarz sistemlerde bir hücrenin hangi satır'a ait olduğunu farklı hesaplamalarla bulabiliriz. column-store fiziksel olarak data'yı bu şekilde kaydeder:

    ```
    (ID) 1, 2, 3, 4, 5, 6
    (First Name) Joe, Jack, Jill, James, Jamie, Justin
    (Last Name) Smith, Williams, Davis, Miller, Wilson, Taylor
    (Phone) 555-1234, 555-5668, 555-5432, NULL, 555-6527, 555-8247
    (Email) jsmith@gmail.com, jwilliams@gmail.com, NULL, jmiller@yahoo.com, NULL, jtaylor@aol.com
    ```

    Örneğin Cassandra column-store diildir. zaten resmi github sayfasında "partitioned row-store" olduğu yazar. çünkü eğer bir hücreye erişmek istiyorsak; cassandra, önce row-key'i buluyor, sonra column-name'ini buluyor.

  - # column family
    column family database'de, RDBMS'teki tablo column-family'ye denk gelmektedir. developer'ın sorgudan döndürmek istediği her sutun için farklı tablo yapması gerekir/beklenir. (not: "one-table-per-query pattern" buradan gelir). bu sebeple "tablo" yerine "column-family" terimi kullanılır. yani 1 tablo, bir column grubuna denk gelir. "family" suffix'i buradan gelir. family suffix'i; bir nevi multi-column, yada column-group terimlerine denk gelir.
    
    table ile column-family karşılaştırıldığında, fiziksel olarak data tutuş biçiminin farketmemesini bekleriz. fakat ikisi arasında şu farklar söz konusu:
    - kavramsal/logical farklılık
    - veriye erişimde, genelde farklı öncelikler tercih edildiği için, data'nın tutuş biçimi structural olarak farklı optimize ediliyor. örneğin column-family mantığında (genelde) data fiziksel olarak sorted oluyor. tablo ile karşılaştırıldığında, bu gibi optimizasyonlar/farklılıkar söz konusu oluyor. 

    cassandra dünyasında eskiden column-family terimi kullanılırdı. fakat daha CQL'e geçiş ile "tablo" terimi kullanılmaya başlandı. fakat cassandra hala column-family bir database'dir.

Yukarıdaki no-sql tiplerine bakıldığında, aslında, herhangi bir db ile kaydettiğimiz ve çektiğimiz bilgiyi diğeri ile de yapabiliriz. örneğin; Document tabanlı sistemdeki kaydı, Key-Value ile de tutabiliriz. fakat seçimimizi datamızı nasıl çekeceğimize (nerelere sorgu atıp çekmek isteyeceğimize), nasıl kaydedeceğimize göre karar vermeliyiz.

örnek:

ilişkisel veritabanı gibi data kaydedecek isek, fakat ilişkiye ihtiyacımız yok ise, Document tabanlı database bu iş için uygun. çünkü ilerdeki zamanlarda her data sutunu'na göre sorgu atmak isteyebiliriz. oysa bu data'yı Key-Value database'de saklıyor olsaydık, sorgularımızda büyük problem yaşardık. çünkü Key-Value database value'da ne olduğu ile pek ilgilenmez. Key-Value genelde value'su tek bir değer olan datalar için uygundur. bu şekilde daha hızlı okuma ve yazma yapabiliriz. Hatta bu sebepten genelde RAM üzerinde çalışırlar.

Document tabanlı sistemlerde her döküman genelde json veya türevleri formatında saklanır.
