############################

############################
# ELK
############################

############################

# ELK (or Elastic Stack)

Elastic + logstash + kibana üçlüsü çoğu zaman birlikte kullanılıyor. bu sebeple bu 3'lü pakete verilen kısaltma. 

Logstash'e her uygulama log'u yollar, Logstash tüm veriyi elastic'e aktarır. Kibana ise elastic'ten okduğu data'ları son kullanıcıya web arayüzünden gösterir.

Bu mimaride Logstash çok yorulur. Çünkü herkes sadece Logstash'e data (log) yollar. Burada yükü dağıtmak için "__Beats__" isimli uygulama sıkça kullanılır. Tüm projemizdeki her uygulama için ayrı ayrı beats ayağa kaldırabilir yada n-adet uygulama için sadece 1 adet beast kaldırabiliriz. Beats sadece aracılık yapar. Logstash'e dataları yollarken, backpressure yeteneği de olduğundan yoğunluk sırasında sistemin dengesini korur. Beats aynı zamanda isterse direk olarak elastic'e de aldığı dataları atabilir. Hatta bazı ek modüller sayesinde basit filtreleme işlemleri de yapabilir. (tüm paragraftaki bilgiler için kaynak: (source-id: 401) )

beats'ler tipine göre farklı executable dosyaları indirme gerektiriyor. örnek: __filebeat__; dosyadan okuma yaparken, __winlogbeat__ ms-windows log sisteminden log'ları takip eder ve ms-windows log'larındaki her değişikliği kendisinin input'u olarak kabul eder.

filebeat için örnek config file:

```yml
filebeat.prospectors:
- input_type: log
  paths:
    - /var/log/httpd/access.log # filebeat'in sürekli okuyacağı dosya

document_type: apache-access # okunacak dosyanın dosya formatı

fields_under_root: true

output.logstash:
  hosts: ["127.0.0.1:5044"] # filebeat hangi ip'deki logstash'e data'ları (log'ları) göndereceği
```

Logstash'in sırası ile 3 farklı fazı vardır:
- input: input'tan dataların okunması
- filter: dataların manipüle edilmesi
- output: dataların farklı bir yere yollanması

logstash için örnek config file:

```groovy
input { // hangi faz için tanımlama yapacağımızı tepede belirtiyoruz
  beats { // beats'ten okuyacağımızı belirtmemiz gerekli.
    port => 5044 // input'un nerden okunacağı
  }
}

// yukarıda "beats" ('ten okumak yerine) yerine şunları kullanabilirdik:

// - file (logstash ile aynı makinede bulunan bir dosyadan okumamızı sağlardı)
// - redis (redisten okumamızı sağlardı)

// input örnekleri için kaynak: (source-id: 402)

filter { // hangi faz için tanımlama yapacağımızı tepede belirtiyoruz

  grok { // logstash ile gömülü gelen bir filter plugin'i
    match => { "message" => "%{IPORHOST:clientip} %{USER:ident} %{USER:auth} \[%{HTTPDATE:time}\] "(?:%{WORD:verb} %{NOTSPACE:request}(?: HTTP/%{NUMBER:httpversion})?|%{DATA:rawrequest})" %{NUMBER:response} (?:%{NUMBER:bytes}|-)" }
  }

  date { // logstash ile gömülü gelen bir filter plugin'i
    match => [ "timestamp" , "dd/MMM/yyyy:HH:mm:ss Z" ]
  }
}

// yukarıda grok eklentisi sayesinde, logstash'e gelen anlamsız log satırı anlamlı hale dönüştürülüyor. log formatımızı grok'a parametre olarak veriyoruz. date eklentisine geldiğimizde ise artık tarih değerimizi log satırından parse etmemize gerek yok. tarihi "timestamp" olarak yeni bir json field'ı olarak kaydediyoruz. artık elastic search'e baktığımızda "timestamp" field'ı istediğimiz formatta görünecektir. ek not: "@timestamp" field'ı logstash tarafından otomatik atılmaktadır. "@timestamp" logsstah'e ne zaman log gelirse o anın tarihi olarak set edilmektedir. 

output { // hangi faz için tanımlama yapacağımızı tepede belirtiyoruz
  elasticsearch { // dataları hangi sunucuya yollacağımıızı bilertmemiz lazım.
     hosts => ["localhost:9200"] // elastic'in ip'si ve portu
  }
}

// yukarıda "elasticsearch" ('e dataları atmak yerine) aşağıdakileri kullanabilirdik:

// - file (logstash ile aynı makinede bulunan bir dosyaya yazmamızı sağlar)
// - graphite (graphite isimli programa dataları yollayabilmemizi sağlar)
// - statsd (aynı makiende bulunan statsd isimli servise data yollayabilmemizi sağlar)

// output örnekleri için kaynak: (source-id: 402)
```

logstash filter'ları için farklı bir örnek: (source-id: 404)

# syslog
Birçok implementasyonu olan fakat rfc3164 ve daha sonrasında rfc5424 ile standartlaştırılmış log formatı ve protokolüdür. syslog standartlaştığından ötürü özel isimdir.

(source-id: 405)

(source-id: 406)

syslog servisleri, 514 portundan dinleme yapar. platformdaki tüm uygulamalar buraya loglarını yollar. Logstash'te input plugini olarak syslog yazılırsa, Logstash 514 portundan dinleme yapmaya başlar. aynı bir syslog deamon'u gibi log'ları dinler ve bunları elastic'e yollar.

# kibana
logstash'in elastic'e kaydettiği logları son kullanıcıya göstermek için web arayüzü sunan bir yazılım.

kibana web-ui'ındaki sekmeler:

- discover: arama yapılmasını sağlıyor.
  discover sekmesindeki alt widget'lar:
  - bir widget'ta "Selected Fields" ve "Available Fields". bunlar arama sonucları ekranında gösterilebilecek sutunları belirtmektedir. örnek: "Available Fields"'de loglarda akan tüm alanlar mevcuttur. örnek: appName, ip, timestamp, message. "Selected Fields"'a "Available Fields"'lardan seçim yaparak alan ekleriz. böylece sadece "Selected Fields"'daki alanlarımız sonuc ekranında görünmüş olur. eğer "Selected Fields" ı boş bırakırsak sonuc ekranında "\_source" sutunu olur ve bu sutunda tüm log bilgileri(alanları) bir json şeklinde gösterilir.
  - bir widget'ta standart olan "Apache Lucene Query Syntax" ile arama yapabilmemizi sağlayan textbox mevcuttur. Lucene arama örneği: "status:200 AND appName:user-service".
  - bir widget'ta filter'lar mevcut. bunlar Lucene stili aramasına ek filtreler eklememizi sağlıyor. Lucene ile de yapılabilecek bir şey fakat filtreler kolay enable disable edilebiliyor. oysa lucene'de bir filtreyi yorum satırı yapmazsınız. silip tekrar yazmamız gerekir.
  
  Ekranda yaptığımız her ayar URL'ye yansır. URL'yi başka tarayıcıya yapıştırdığımızda bu arama aynen açılır. 

- dev tools: json query'leri ile arama yapılmasını sağlıyor. örnek:

```
  GET _search
  {
    "query": {
      "match_all": {}
    }
  }
```

- visualize: grafikler hazırlamamızı sağlıyor. burdan grafik oluşturuyoruz. fakat bu grafikleri direk web-ui'ı açan user'a gösteremiyoruz. bu grafikleri dashboard'a bağlamak zorundayız.

- dashboard: bir filtre yazıyoruz ve visualize'da hazırladığımız her görsel'i buradaki filtreleye bağlıyoruz. örneğin filtremiz 'status:200' olsun. altında da buna bağlı 3 tane grafik bağlamış oluruz. bu dashboard'a "başarılı istekler" adını verelim. birçok dashboardumuz olabilir. artık dashboard sekmesine girip, listeden "başarılı istekler"'i seçen user, karşısında 3 tane grafik görecektir.

# Kibana index pattern
index patterns tell Kibana which Elasticsearch indices you want to explore. An index pattern can match the name of a single index, or include a wildcard (*) to match multiple indices.

For example, Logstash typically creates a series of indices in the format logstash-YYYY.MMM.DD.

# Graylog
Graylog; logstash ve kibana'ya alternatif, ELK'ya göre daha community based bir projedir.

Graylog genelde elasticsearch ve mongo ile kullanılıyor. MongoDB'de genel graylog'un konfig'leri saklanırken, elasticsearch'te log'ların kendileri saklanıyor.

Graylog sunucusuna direk mesajları atabiliriz. Fakat Beats veya Logstash ile de ek modüllerle supportu mevcut.
