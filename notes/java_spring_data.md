############################

############################
# JAVA SPRING DATA
############################

############################

# persistence

## spring data
en üst modülün ismi "Spring Data"'dır. Spring data bir interface'dir. Bunun birçok implementasyonu mevcut. Örnek implementasyonlar:
- Spring Data JPA
- Spring Data MongoDB
- Spring Data JDBC
- Spring Data LDAP
- Spring Data Redis
- Spring Data for Apache Cassandra

'Spring Data' implementasyonları Spring tarafından geliştirilmez. Spring implementasyonları sadece JPA gibi API'lerin önüne bir API daha koyar. böylece; relational database'lere erişmek istediğimizde; JPA veya alternatifi bir framework ile erişmek istediğimizde tümüne aynı API'lerden erişebilmemizi sağlar.

spring-data-commons; ortak annotation'ları vs barındıran jar'dır. Fakat ortak olmayan annotation'larda mevcut. örneğin; MongoDB için @Entity yerine @Document yazmak gerekli.

## spring jta
JavaEE'nn kullandığı Java Transaction API (or JTA)'yı kullanır. Yine Spring data da olduğu gibi önüne wrapper atarak bir API sunar. Dolayısı ile bir JTA implementasyonuna ihtiyacımız var:

- Atomikos
- Narayana
- Java Open Transaction Manager (or JOTM)
- JBoss TS (javaEE sunucusundan bağımsız çalışabilmektedir)
- Bitronix Transaction Manager (or BTM)

Yada Java EE managed bir Transaction Manager kullanabiliriz. Bunun için uygulamamızın Java EE sunucu üzerinde kaldırmak zorundayız. Sprig embeeded web server ile geldiğinde de, embeeded java web server'ın sunduğu JTA'yı kullanabiliriz.

JTA birden fazla DB'nin de transactional çalışmasını sağlamaktadır. yani bir işlem diğer DB'ye kaydedilemediyse, ilk db'ye de kaydetmeyecektir.

JTA 2 amaçla kullanılabilir:
- JMS: Broker'a mesaj gitmesi, onun karşı taraf tarafından okunduğunu ve karşı tarafından çalıştırığı metodun başarılı şekilde tamamalandığından emin olunması
- DB: DB datalarının gerektiğinden bir den fazla DB'ye tümüyle kaydedilebilmesinden emin olunması

kaynak: (source-id: 279) 2 inci paragraf.

Spring PlatformTransactionManager sınıfı ile transaction yapısını desteklemektedir. @Transactional annotation'unu bir metodun tepesine yazdığımızında, spring application-context içerisinde PlatformTransactionManager implementasyonu (bean) arayacaktır. Eğer manuel bean tanımlatmak istiyorsak şunu yapmalıyız:

```java
@Bean
 public PlatformTransactionManager platformTransactionManager(){ 
    return new JtaTransactionManager();
}
```

PlatformTransactionManager class hiyerarşisi şu şekildedir:

```
- PlatformTransactionManager
-- HibernateTransactionManager
-- JTATransactionManager
-- JMSTransactionManager
-- JPATransactionManager
-- WebLogicJtaTransactionManager
```

kaynak: (source-id: 280)

## distributed transaction
'__Global transaction__' terimi XA protokolü dökümanında 'distributed transaction'ın kendisine verilen isimdir. global transaction her yerde kullanılan bir terim diildir. XA dökümanında, karışıklığı engellemek için bu şekilde kullanıldığı belirtilmiş. kaynak: (source-id: 281) "Distributed Transaction Processing:Reference Model", Version 3, title: "2.1 Transaction Definitions", subtitle: "Global Transaction" and "Distributed Transaction".

'local transaction' terimi XA protokolü dökümanında hiç kullanılmamıştır.

global transaction'lar birden fazla bağımsız kaynak üzerinde çalışırken transaction sağlayan yapılardır. global transaction'lar için üçüncü parti bir servisin kaynakları kontrol ediyor olması gerekmektedir. ancak global transactionlar ile 2PC yapılabilmektedir. 2PC nin olması için üçüncü parti servisin DB gibi kaynaklarla iletişimde olması gerekiyor. Bu iletişim için kullanılan protokollerden bir tanesi XA'dır. kaynak: (source-id: 279) 3 üncü paragraf.

__X/Open (or Open Group for Unix Systems)__ birçok kuruluş tarafından desteklenen ortak bir camiadır. XA protokolü, X/Open tarafından geliştirilmiştir. bu dökümanında spesifikasyon tanımlanmıştır: (source-id: 283) Dökümanın dağıtım sayfası: (source-id: 284)

Dökümandaki bazı tanımlar:
- __Application Program__: transaction'ın adımlarını tanımlayan program.
- __Resource Manager__: DB, file-system, printer service gibi paylaşılacak kaynağı paylaşan yazılımdır.
- __Transaction Manager__: transaction'ın ne durumda olduğunu monitör eden, gerektiğinde rollback alması için ilgili RM'lere protokol üzerinden haber verel yazılımdır.

"Transaction"; aynı resource-manager'de yapılan, rollback edilebilir atomik işlemi kapsamaktadır. Oysa "Distributed transaction"; farklı resource manager'lerinde olduğu data'lar üzerinde yapılan, rollback edilebilir atomik işlemleri kapsamaktadır.

Dökümanda 11.inci sayfada "Interface Overview" başlığında belirtildiği gibi XA, DB ile transaction manager arasındaki protokoldür. Bu sebeple DB tarafından desteklenmesi zorunludur.

## JPQL Queries vs native queries
JPQL JPA'nın kendi query syntaxıdır. örnek: 'SELECT c FROM Country c'. Native query ise sql sunucusunda çalıştırılacak sql'in kendisidir. JPA API'leri ikisini de çalıştırmamıza izin verir.

## named query tanımlama:
native yada JPQL querie'lerini bir isim ile tutup çağırabiliriz. örnek:

```java
@Entity
@Table(name = "country", schema="my_db")
@NamedQueries({

    @NamedQuery(name="Country.findAll",

                query="SELECT c FROM Country c"),

    @NamedQuery(name="Country.findByName",

                query="SELECT c FROM Country c WHERE c.name = :name"),

}) 

public class Country {

    @Id
    @Column(name = "id")
    @GeneratedValue(strategy = GenerationType.SEQUENCE)
    private Long id;
}
```

Artık yazılımımızın herhangi bir yerinden şu kod ile named query kullanabiliriz:

```java
@PersistenceContext
public EntityManager em;

customers = em.createNamedQuery("findAllCustomersWithName")

        .setParameter("custName", "Smith")

        .getResultList()
```

# EntityManager/EntityManagerFactory vs Session/SessionFactory
Session hibernate spesific sınıftır. EntityManager ise JPA spesific'tir. EntityManager arkaplanda hibernate'in Session'ını zaten kullanmaktadır.

EntityManager'dan Session instance'ımızı elde edebiliriz:

```java
Session session = entityManager.unwrap(Session.class);
```

# entity manager types

Basically JPA specification defines two types of entity managers:
 
- Application-Managed (__LocalEntityManagerFactoryBean__ kullanılır)

  Application Managed entity manager means "Entity Managers are created and managed by merely the application ( i.e. our code )" .
 
- Container Managed (__LocalContainerEntityManagerFactoryBean__ kullanılır)

  Container Managed entinty manager means "Etity Managers are created and managed by merely the J2EE container ( i.e. our code doesn't directly manages instead entity managers are created and managed by container, and our code gets EM's through some way like using JNDI ).
 
# JPA Konfigürasyon
 
- ## Uygulama Tarafından Yönetilen EntityManager Konfigürasyonu
 
jpa-application-managed.xml:
 
```xml
<bean id="entityManagerFactory"
      class="org.springframework.orm.jpa.LocalEntityManagerFactoryBean">
 
         <property name="persistenceUnitName"
                   value="rentAcar-application-managed" />
</bean>
```

persistence.xml:
 
```xml
<persistence
    version="1.0"
    xmlns="http://java.sun.com/xml/ns/persistence"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://java.sun.com/xml/ns/persistencehttp://java.sun.com/xml/ns/persistence/persistence_1_0.xsd">
    
        <persistence-unit name="rentAcar" />
        <persistence-unit name="rentAcar-application-managed">
            <class>com.kurumsaljava.spring.Car</class>
            <class>com.kurumsaljava.spring.Customer</class>
            <class>com.kurumsaljava.spring.Rental</class>
            <properties>
                <property name="hibernate.connection.url" value="jdbc:hsqldb:mem:spring-playground" />
                <property name="hibernate.connection.driver_class" value="org.hsqldb.jdbcDriver" />
                <property name="hibernate.dialect" value="org.hibernate.dialect.HSQLDialect" />
                <property name="hibernate.connection.username" value="sa" />
                <property name="hibernate.connection.password" value="" />
                <property name="hibernate.hbm2ddl.auto" value="create" />
                <property name="hibernate.show_sql" value="true" />
                <property name="hibernate.format_sql" value="true" />
                <property name="hibernate.hbm2ddl.show" value="true" />
            </properties>
        </persistence-unit>
</persistence>
```

örnek bir işlem:
 
```java
public static void main(String[] argv) {   
    ApplicationContext context = new ClassPathXmlApplicationContext("jpa-application-managed.xml");
    EntityManagerFactory factory = (EntityManagerFactory) context.getBean("entityManagerFactory");
    EntityManager manager = factory.createEntityManager();
    EntityTransaction transaction = manager.getTransaction();
    transaction.begin();
    List result = manager.createQuery("select c.name from Customer c").getResultList();
    System.out.println(result.size());   
    transaction.commit();  
    manager.close();  
    factory.close();
}
```
 
- ## Uygulama Sunucusu Tarafından Yönetilen EntityManager Konfigürasyonu
 
jpa-container-managed.xml:
 
```xml
<bean id="entityManagerFactory"    
      class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
         
          <property name="jpaVendorAdapter">
                   <bean class="org.springframework.orm.jpa.vendor.HibernateJpaVendorAdapter"/>
          </property>
         
          <property name="jpaProperties">
                  <props>
                    <prop key="hibernate.show_sql">true</prop>
                    <prop key="hibernate.format_sql">true</prop>
                    <prop key="hibernate.hbm2ddl.auto">create</prop>
                    <prop key="hibernate.hbm2ddl.show">true</prop>
                  </props>
          </property>
         
          <property name="dataSource" ref="dataSource" />
</bean>
```

# Repository
türkçe kelime anlamı: depo, ambar

```java
public interface MyRepository extends CrudRepository<Person, Long> {

  Person save(Person p);

  Optional<Person> findById(Long primaryKey);

  Iterable<Person> findAll();

  long count(); 

  void delete(Person p);

  boolean existsById(Long primaryKey);
}
```

Yukarıdaki metodlar default implemente edilmiş durumdalar. çağrıldıklarında veritabanında işlem yapacaklardır. isteğe bağlı ekstra metodlar yazılabilir. o zaman interface değil class yapılmalıdır. fakat metod body2si yazılmayacak ise (yani hep query'ler ile çalışılacak ise) sadece interface yapılıp metod imlazarı yeterli olacaktır.

Super'den sub-interface'ye doğru:

- Repository -> hiçbir metod içermiyor.

- CrudRepository -> count, delete, existbyid, findall, save gibi metodlar içeriyor

- PagingAndSortingRepository --> pagination için metod içeriyor.

bunlardan türemiş birçok implementasyon mevcut.

# @NoRepositoryBean
ilgili sınıfın instance'ının repository olmadığını işaretler. örneğin baseRepository sınıflarımızda bu annotation'ı kullanabiliriz. örnek 2: PagingAndSortingRepository bu annotation'ı içeriyor.

# enabling jpa on project
```java
@EnableJpaRepositories(basePackages = "com.acme.repositories.jpa")

@EnableMongoRepositories(basePackages = "com.acme.repositories.mongo")

interface Configuration { }
```

# @Modifying
repository'lerde her eğer manuel bir query yazıyor isek ve db'yi güncelliyorsak, o zaman bu annotation'u o metodumuzun tepesine eklememiz şarttır. bunsuzda çalışır kod, fakat sağlıklı olmaz. jpa buna göre güncelleme olup olmadığını biliyor ve buna göre arkaplandaki davranışlarını belirliyor (örnek cache güncelleme gibi...)

```java
@Query("UPDATE my_table SET name = ahmet"
        + " WHERE id = :id")
@Modifying
int increaseValue(@Param("id") Long id);
```

# relations
(önce güçlü zayıf tablo başlığı okunmalı)

customer-order tablosunda ilişkilere bakalım. customer güçlü, order güçsüz tablodur. çünkü order'da customer-id olmak zorundadır. yoksa o order bi anlam ifade etmez.

normalde nesneye dayalı dillerde, Customer objesi içerisinde List<Order> olmalıdır. fakat databasede buna gerek yok. yukarıdaki satırdan çıkan sonuç bu.

entity customer:

```java
@OneToMany(mappedBy="customer") //order class'ının private 'customer' property'sidir
private List<Order> order;
```

entity order:

```java
@ManyToOne
@JoinColumn(name="customer_id") //order tablosundaki 'customer_id' sutununun adı
private Customer customer;
```

# JoinColumn vs mappedBy
mappedby ile jpa'ya ilişkinin sutnunun (foregin key'in) karşı objede olduğunu belirtiyoruz. mappedby belirtildiğinde ilgili tablomuzda foreign key olmamasına rağmen, java objesinde sanal olarak varmış gibi davranabilmemiz sağlanabiliyor. örneğin yukarıdaki örnekte; customer içinde herhangi bir foreign key olmamasına rağmen getOrder yapabileceğiz.

oysa JoinColumn ile order tablosunun customer_id diye databasede bir sutun içerdiğini belirtiyoruz.

# crosstable (or jointable)
sadece tablo ilişkilerinin tutulduğu tabloya verilen isimdir. one-to-one yada many-to-one ilişkilerde pek tercih edilmiyor. çünkü yeni tablo yaratmak yerine, varolalan tablolara bir foreign key ekleniyor. fakat many-to-many ilişkilerde kullanılması şart. ismi genelde ilişkilendirilen iki tablonun birleşimidir. örnek: customer_order.

# @jointable
kullanımı:

```java
@Entity
public class A {

    private Long id;

    @ManyToOne
    @JoinTable(
       name = "A_B", 

       joinColumns = @JoinColumn(name = "B_ID"), 

       inverseJoinColumns = @JoinColumn(name = "A_ID")
    )
    private B b;
}
```

# FetchType
@ManyToOne(fetch = FetchType.LAZY) şeklinde kullanılır. Lazy sadece get methodu çağrılınca databaseden nesneyi çağırır, EAGER ise her zaman direk databaseden okunmuş halde objeyi getirir. one-to-one ve many-to-one ilişki default olarak EAGER iken, many-to-many ilişki default'ta LAZY'dir.

# CascadeType
@OneToMany(cascade=CascadeType.ALL) şeklinde kullanılır. örneğin order yaratıyoruz fakat customer_id foreign key'inin null olmaması gerekiyor. dolayısı ile önce customer yaratılmış olmalı. bu sebeple iki tabloya birden kayıt atarken önce customer daha sonra order'a yazmasını istiyoruz JPA'dan. örnek:

```java
Student student = new Student();

student.setName("Ahmet");

student.getHomeAddress().setStreet("Esentepe");

entityManager.persist(student);
```

Yukarısı CascadeType belirtmediysek hata verecektir. çünkü adres objesi student içinde tanımlı diil. bunu şu şekilde çözebiliriz:

```java
@OneToOne(cascade = CascadeType.PERSIST)

private Address homeAddress = new Address();
```

CascadeType'lar:

- PERSIST : Nesne persist edilirse alt nesne de persist edilir

- MERGE : Nesne merge edilirse alt nesne de merge edilir

- REMOVE : Nesne silinirse bağlı alt nesne de silinir

- REFRESH : Nesne yenilenirse bağlı alt nesne de yenilenir

- ALL : Tüm işlemler birlikte yapılır

multiple kullanım mevcuttur:

```java
@OneToOne(cascade = { CascadeType.PERSIST, CascadeType.MERGE })
```

# bi-directional (or bidirectional) vs in-directional (or indirectional)
onetomany yada manytomany yada onetoone tek yönlü yada çift yönlü olabilir. örneğin; onetoone ilişki yaptık fakat 2 objenin sadece 1 tanesine foreign key koyduk. java objesinden (entity içinde) de tanımlama yapmadık. dolayısı ile runtime sırasında sadece birinden diğerine gidiş olabilecek. dolaylı yoldan erişim yapılır fakat bidirectional ve indirectional terimleri direk erişim olup olmadığı ile ilgili bir durumdur.

# transaction
bir metodun tepesine @Transactional annotation'u atılırsa o metodun içindeki işlemerde yapılan database işlemleri atomic olur. eğer hata çıkarsa otomatik olarak sql'ler geri alınır. aslında geri alınmasından ziyade yapılan database işlemleri database'de işlenmiyor. 

@Transaction opsiyonel olarak şu parametreleri alabilir:

```java
@Transactional(rollbackFor = MyException.class, 
               propagation = Propagation.REQUIRED,
               timeout = 35)
```

- rollbackFor

  sadece belirtilen excepiton(lar) için rollback yapılacağıdır. default'ta herhangi bir java excepiton'ında SQL'ler rollback edilir. 
  
  eğer bu property'de belirtilenlerden farklı bir excepiton alınırsa, oraya kadarki SQL'ler comit edilir.

- timeout

  eğer bu süre geçerse rollback edilir

- readOnly

  ilgili transaction bloğunun sadece read-only işlem yaptığının bilgisini transaction manager'a yollar.

  transaction manager bunu runtime'da optimizasyon için kullanabilir.

  eğer "true" verilmişse; transaction manager fail vermek zorunda değil. bu transaction manager'a kalmış bir durum. kaynak: (source-id: 285)

- propagation

  türkçe kelime anlamı: yayılma
  
  @transactional bir metod içinde farklı bir @transactional bean'in metodu çağrılabilir. o zaman bu yeni metod'daki işlemlerin bağımsız mı yoksa, bir önceki transaction'a bağlı mı olacağına propagation özelliği ile karar veriliyor. propagation'ın alabileceği bazı değerler:

  - REQUIRED
    
    default değerdir. Aktif bir Transaction yoksa yeni bir transaction açar. Aktif varsa buna katılır.

  - REQUIRES_NEW

    Aktif bir transaction işlemi varsa bunu bekletir (Suspend) Yeni bir tane açarak kendi işini hallettikten sonra bu transaction işlemini kaldığı yerden devam ettirir. 2 transaction birbirinden bağımsızdır.

  - NOT_SUPPORTED

    Transaction varsa suspend edilir servis metodu Transactionsız çalıştırılır.

  - NEVER

    Transaction varsa Exception fırlatır.

  - MANDATORY

    Transaction yoksa exception fırlatır

  - SUPPORTS

    önceden açılmış transaction varsa; onu kullanır. yoksa transaction'suz işlem yapar.

  - NESTED
    
    Aktif bir Transaction yoksa yeni bir transaction açar. Aktif varsa buna katılır. Bu kısım aynı REQUIRED gibidir. sadece ek olarak metod bağlangıcında bir "savepoint" yaratır. ve eğer hata alınırsa bu savepoint'e dönülür.

@Transactional decleratif çözüm. Programatik çözüm için:

PlatformTransactionManager sınıfından yararlanılır. Bu sınıf ile:

```java
DefaultTransactionDefinition def = new DefaultTransactionDefinition();
TransactionStatus status = txManager.getTransaction(def);
try {
  // execute your business logic SQL operations here
}
catch (MyException ex) {
  txManager.rollback(status);
  throw ex;
}
txManager.commit(status);

```

# application.properties dosyasındaki örnek datasource tanımı

bu tanım jpa sadece jdbc kullanılacakken, 

```yml
mydabatabase:

  datasource:

    url: jdbc:sqlserver://ip:1433;databaseName=mydb

    username: usr

    password: 123

    driver-class-name: com.microsoft.sqlserver.jdbc.SQLServerDriver

    testOnConnect: true -> her db connection'ı oluşturulduğunda öncesinde yapılan kontroldür

    testWhileIdle: true -> bir connection'dan kimse bir süredir işlem yapmadıysa, bağlantı üzerinden validationQuery çağırılır.

    logValidationErrors: true -> validationQuery yapıldığında alınacak olan hataların loglanıp loglanlanmayacağı

    validationQuery: "SELECT 1" -> yukarıdaki eventlerde (testOnConnect, testWhileIdle...) çağrılıcak sql sorgusu

```
