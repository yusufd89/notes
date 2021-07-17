############################

############################
# JAVA PERSISTANCE
############################

############################

# ORM (or Object to Relational Mapping)

ORM programlama dilinden bağımsız, veritabanı objelerinin programlamada haritalanmasının (mapping) genel ismidir.

# Persistence (or süreklilik)

Bilişim dünyasında persistence, bir işlemin sürekliliğinin sağlanması kastedilir. işlemin sürekliliği olabilmesi için state'in (data'nın) bir yere kaydedilmesi gerekir.

# JPA (or Java Persistence API)

java için ORM spesifikasyonudur.

# eclipselink (or old-name:toplink) vs Hibernate vs openJPA

Birer JPA implementasyonudur.

# @javax.persistence.Entity vs @org.hibernate.annotations.Entity
javax kullanırsak runtime sırasında implementasyon arar ve onu çağırır. hibernate olan direk kendini çağırır. hibernate ne kadar javax ile aynı görevi görse de, javax'ta olmayan ekstra proprty'ler sunuyor.

# Entity Framework
microsoft'un ORM frameworkü'nün özel ismidir.

# JDBC (or Java Database Connectivity) vs JPA

JDBC, java için database spec'idir. (driver olmadan bir işe yaramaz.) JPA kendi içinde JDBC kullanır. JDBC databaseye bağlanan ve üzerinde işlem yapmaya yarayan API'dir. Her database bunun implementasyonlarını (driver'larını) yapar (mysql, oracle...). Bunun üzerine ORM yeteneğini katarak JPA ortaya çıkmıştır.

# ODBC (or Open Database Connectivity)
JDBC'ye alternatiftir. Dilden bağımsız geliştirilmiş bir API'dir.

# ojdbc
oracle database'sinin jdbc driver'ıdır.

# ODM (or Object Document Mapping)

ORM relational databaseler için mapping yaparken, ODM sadece nosql'ler (relation olmayan databaseler) içindir.

# database Dialect vs database Driver

dialect türkçe anlamı: lehçe

Driver bir databaseye giderken soket üzerinden kullandığı erişimi sağlayan yazılımdır. örneğin bir sql komutunu şu IP'li database'de çalıştır dediğimizde bu işi halleder.

Dialect ise SQL türevi (ve o türevin versiyonudur). SQL dilinin birçok türevi ve versiyonu çıkmıştır. bazı database'ler birçok farklı SQL türevine ve versiyonuna destek verir. işte bu durumlar için Dialect özelliğini kullanırız.

bir spring uygulamasını jpa ile ayağa kaldırırken, hem dialect hemde driver vermemiz gerekir. eğer dialect vermezsek default dialect'i kullanacaktır.

# sql2o
açık kaynaklı Java kütüphanesinin ismi. bu kütüphane ile aşdağıkigibi resultSet'lerle uğraşmadan query atabiliyoruz. Hibernate'ten ortalama 5 kat daha hızlı.

```java
public List<Customer> fetchCustomers(customerId) {
  try (Connection con = sql2o.open()) {
    final String query =
        "SELECT id, name, address " +
        "FROM customers WHERE id = :customerId";

    return con.createQuery(query)
        .addParameter("customerId", customerId)
        .executeAndFetch(Customer.class);
  }
}
```

# HikariCP
JDBC için connection pool kütüphanesidir. Buraya bakılırsa: (source-id: 397) "What does correctness and reliability mean?" başlığı. Connecion poool yönetiminin ne gibi yetenekleri olduğu görülmektedir.

# connection pool-size
HDD'lerde cihaz yavaşlığından kaynaklı bloklanma vardı. Fakat SSD'lerde blocklanma daha az çünkü SSD cihaz hızlı cevap dönüyor. SSD'ler hızlı olduğundan yazılımcılar direk olarak güçlü makine psikolojisi ile pool sayısını arttırıyor, oysa; bloklanma az olduğundan CPU'nun ve diğer tüm cihazların thread switch maliyetini düşürmenin avantajlı olduğu görülmektedir.

ortalama connection pool sayısı database çalıştıran makinanın şu özelliklerinden hesaplanır:

connections = (cpu_core_count * 2) + effective_spindle_count

Hyperthreading aktif ise bile HT sayısı ile değil, gerçek fiziksel core cpu sayısı referans alınmalıdır.

yukarıdaki tüm bilgiler için kaynak: (source-id: 398)

spindle; HDD'nin okuma kafasını temsil eder. Birden fazla HDDmiz olsun. bu HDD'lerdeki kayıtların tümü tek bir DB instance'ını (sunucusunu) oluştursun. Bu durumda HDD sayımız, spindle count'a eşit olur. Eğer her HDD'mizi paralelden 2 kafa okuyor olsaydı o zaman; spindlle HDD adetinin 2 katı olacaktı.

Yukarıda 1 DB sunucusundan bahsedildi. 10 pool sunucu tarafından ayarlanmış olsun. Eğer sadece 1 instance uygulama bu sunucuya istek yapıyor ise; client taraftaki ayara max ve min pool count 10 verilebilir.

yukarıdaki bahsi geçen pool sayısı sadece 1 db ve 1 app bu db'de işlem yaparsa geçerlidir. diğer durumlarda farklı connnection pool sayısı ile çalışmak daha verimli olabilir. kaynak: (source-id: 399) "brettwooldridge" comment on November 20, 2017.

# mybatis (or old-name:ibatis)
ibatis sonlandırıldı ve isim değişikliği ile mybatis ile geliştirilmelerine devam edildi.

mybatis veritabanı işlemleri yapmaya yarayan java kütüphanesi. SQL sonuçlarını java objelerine mapping yapabildiği için ORM aracıdır. fakat JPA implementasyonu diildir.

mybatis çok gelişmiştir:
- lazyload desteği var
- annotation desteği var
- mapping desteği var (orm)
- xml ile önceden query'ler tanımlanıp çağrıldığı gibi, runtime'da da query'ler dinamik yaratılabilmektedir.

örnek bir işlem:

```java
Reader reader = Resources.getResourceAsReader("SqlMapConfig.xml");
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(reader);		
SqlSession session = sqlSessionFactory.openSession(); 

session.delete("Student.deleteById", 2); // "Student.deleteById" query is declared on xml
session.commit();
session.close();
System.out.println("Record deleted successfully");
```

# jdbc driver types
jdbc'nin çalışma prensiplerini belirlemektedir. client tarafta URL girilirken type belirtilir. örnek oracle-JDBC url girerken şunu gireriz:

> jdbc:oracle:oci:@myhost:1521:inst1

burada "oci" oracle'ın belirlediği bir keyworddür. "oci", type-2'ye referans etmektedir.

- Type 1 driver – JDBC-ODBC bridge

- Type 2 driver – Native-API driver

  client atrafın direk database sunucusunun native client protokolünü kullanır. native protokolü desteklemek için saf java kullanılmayabilir. native client sistemde yüklü bir arkaplan servisi dahi kullanablir. bu tipin taşınabilirliği azdır.

- Type 3 driver – Network-Protocol driver (middleware driver)

- Type 4 driver – Database-Protocol driver/Thin Driver(Pure Java driver)

  ojdbc'de "thin" olarak geçmektedir. bu tipte bağlantılar %100 java kodu kullanır. db sunucusu ile java soketi açıp haberleşirler. %100 java olduklarından her tarafta kullanılabilirler.

# oracle DB version history

i, g, c keyword'leri tamamane rastgele verilmiştir. teknik anlamda hiçbir önemi yok.

| full name and version         | initial verson of serries | latest version of serries |
|-------------------------------|---------------------------|---------------------------|
| Oracle 7.2                    | 7.2.0                     |                           |
| Oracle 7.3                    | 7.3.0                     | 7.3.4                     |
| Oracle8 Database              | 8.0.3                     | 8.0.6                     |
| Oracle8i Database             | 8.1.5.0                   | 8.1.7.4                   |
| Oracle9i Database             | 9.0.1.0                   | 9.0.1.5                   |
| Oracle9i Database Release 2   | 9.2.0.1                   | 9.2.0.8                   |
| Oracle Database 10g Release 1 | 10.1.0.2                  | 10.1.0.5                  |
| Oracle Database 10g Release 2 | 10.2.0.1                  | 10.2.0.5                  |
| Oracle Database 11g Release 1 | 11.1.0.6                  | 11.1.0.7                  |
| Oracle Database 11g Release 2 | 11.2.0.1                  | 11.2.0.4                  |
| Oracle Database 12c Release 1 | 12.1.0.1                  | 12.1.0.2                  |
| Oracle Database 12c Release 2 | 12.2.0.1                  |                           |
| Oracle Database 18c           | 18.1.0                    |                           |
| Oracle Database 19c           | 19.0.0                    |                           |

Oracle OJDBC, jdk, jdbc spesifikasyonu sürümleri uyumu için burada resmi compability matrix table'lar mevcut:

(source-id: 400)

# jdbc url form examples

with username pass:

> jdbc:oracle:thin:ahmet/12345@//myhost:1521/mydb

without username pass:

> jdbc:oracle:oci:@myhost:1521:inst1

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# jdbc

```java
PreparedStatement ps = null;
try {
   String SQL = "Update Employees SET age = ? WHERE id = ?";
   ps = conn.prepareStatement(SQL);
   . . .
}
catch (SQLException e) {
   . . .
}
finally {
   pstmt.close();
}
```

Her açılan jdbc connection'ı için birçok statemen tanımlanabilir. statement'lerin birçok türevi vardır. statement objelerimizi bir kere oluşturduktan sonra dilediğimiz kadar üstüste aynı connection'da çağırabiliriz. statementler (tipine göre) gerektiğinde db-side caching'de kullanmaktadır. statement tipleri:

- Statement

```java
Statement stmt = con.createStatement();

stmt.executeUpdate("CREATE TABLE STUDENT(ID NUMBER NOT NULL, NAME VARCHAR)");
```

- PreparedStatement

```java
PreparedStatement pstmt = con.prepareStatement("update STUDENT set NAME = ? where ID = ?");
pstmt.setString(1, "ahmet");
pstmt.setInt(2, 111); 
pstmt.executeUpdate();
```

- CallableStatement

store prosedurleri çağırmak için kullanılır.

```java
CallableStatement cstmt = con.prepareCall("{call anyProcedure(?, ?, ?)}");
//Use cstmt.setter() methods to pass IN parameters
cstmt.execute();
```
