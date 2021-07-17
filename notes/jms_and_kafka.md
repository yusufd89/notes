############################

############################
# JMS AND KAFKA
############################

############################

# Messaging System
  iki farklı şekilde yapılabilir:

  - Point to Point

    örnek: bir web browser'ın sunucuya yolladığı ajax isteği

  - Publish-Subscribe

    örnek: apache kafka, MQTT

# apache kafka
Apache tarafından geliştirilen açık kaynaklı projedir. Confluent firması, 'apache kafka'nın üzerine kurulu ek özellikler sunar ve resmi olarak support hizmeti verir.

kafka açık kaynaklı bir broker'dır. publisher'lar buraya mesaj bırakır, consumer'lar ise buradan üye oldukları topic'lere göre mesajları okurlar.

Kafka'ya gelen mesajlar kafka sunucusunda __segment file__ olarak isimlendirilen dosyalara kaydedilir. bu şekilde data'lar sadece RAM'de kalmaz. fakat dosyaya kaydetme sıklığı sistemi yavaşlatır. kafka sunucu config'lerindeki log.flush.interval.messages, log.flush.interval.ms gibi config'ler segment dosyaları için ayarlar sunar. Bu dosyalardaki kayıtları silmek içinse log.retention.hours, log.retention.bytes gibi seçenekler sunulur.

Kafka, zookeeper sunucusuna ihtiyaç duyar. bu sebeple zookeeper kullanılması zorunludur. zookeeper temel olarak şu görevler için data tutar:
- leader ve follower bilgisilerini tutmak için
- cluster içindeki hangi node'ların ayakta olup olmadığını tutar
- hangi topic'ler var, ve hangi topicler hangi broker'larda, hangi partition'lar var
- Quotas - how much data is each client allowed to read and write
- ACLs - who is allowed to read and write to which topic (old high level consumer) - Which consumer groups exist, who are their members and what is the latest offset each group got from each partition.

kafkanın producer ve consumer'lar için java api'si vardır. 

/kafka/bin/ dizini içerisinde consumer, ve publisher client'ları gibi hızlıca komut satırından işlem yapabilmemiz için hazır script'ler mevcuttur. örnekler:

```sh
# önce sunucumuzu başlatalım:
/bin/kafka-server-start.sh config/server.properties

/bin/kafka-topics.sh --zookeeper localhost:2181 --delete --topic demo

/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic sampleTopic

/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic sampleTopic
```

Dikkat edilirse topic silme, yaratma gibi işlemler için zookeeper soket bilgisini yollamak zorundayız. çünkü burada istek kafka broker'ına değil, zooker'a yapılıyor. oysa message produce ve consume komutlarında zookeeper bilgisi geçilmiyor. orada broker bilgisi geçiliyor, çünkü istek kafka broker'ına yapılıyor.

Kafka script'ine bakılırsa: (source-id: 372), bu sınıfı çağırdığı görülür: (source-id: 373). Scala sınıfı içinde görüldüğü üzere org.I0Itec.zkclient.ZkClient sınıfı; yani Zookeeper client'ı ile Zookeeper'a istek yapılıyor.

Kafka client API'leri topic listeleme gibi metodlar sunuyor:

Kaynak: (source-id: 374)

topic listeleme API'sinin kullanımı:

```java
KafkaConsumer<String, String> consumer = new KafkaConsumer<String, String>(props);
topics = consumer.listTopics();
```

Kafka kendi içinde zookepeer'a giderek topic delete, create gibi işlemler yapabilir. Bu API kümesi, Admin işlemleri olarak geçmektedir. kaynak: (source-id: 375) "Running from JAR" başlığı, 2inci paragraf + (source-id: 376)

Consumer ve producer java API'lerine örnek:

- producer

```java
Properties props = new Properties();
props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9990,localhost:9991");//kafka servers which are on the same cluster
props.put(ProducerConfig.CLIENT_ID_CONFIG, "client99");
props.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, LongSerializer.class.getName()); // record'un key'ini serialize ederken kullanılacak sınıf
props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());// record'un value'sunu serialize ederken kullanılacak sınıf
props.put(ProducerConfig.PARTITIONER_CLASS_CONFIG, CustomPartitioner.class.getName()); // asagida anlatiliyor
// other props may come here...

Producer<String, String> producer = new KafkaProducer<String, String>(props);

//we create a message here
final ProducerRecord<Long, String> record = new ProducerRecord<>("my-topic", "my-key", "my-value");

//we send the message
RecordMetadata metadata = producer.send(record).get();

print("record sent to partition: " + metadata.partition() );
print("record sent to offset: " + metadata.offset() );
```

- consumer

```java
KafkaConsumer<String, String> consumer = new KafkaConsumer<String, String>(props);

//we should subscribe to get a message form that topic
consumer.subscribe("my-topic")

ConsumerRecords<String, String> records = consumer.poll(100); // 100 is the time in milliseconds consumer will wait if no record is found at broker.

while(true){
    //we loop one by one for all messages from that topic
    for (ConsumerRecord<String, String> record : records){
            
            //we got the message
            print(record.offset(), record.key(), record.value());

    }

    consumer.commitAsync(); // or 'commitSync' to block the thread
}

consumer.close();

```

# CustomPartitioner

CustomPartitioner bir record yolladığımızda, onu yolamadan önce çağrılan bir metod içerir. bu metodu sonucunda bir sayı döner. bu sayı,o record'un gideceği partition'dur. eğer bir topic bir den fazla partition'da ise, o zaman bu metodu kullanmak durumundayız. bu metodun içine yazılacak logic tamamen developer'a kalmıştır. örnek:

```java
import java.util.Map;
import org.apache.kafka.clients.producer.Partitioner;
import org.apache.kafka.common.Cluster;

public class CustomPartitioner implements Partitioner{

  private static final int PARTITION_COUNT=50;

  @Override
  public void configure(Map<String, ?> configs) {
  }

  @Override
  public int partition(String topic, Object key, byte[] keyBytes, Object value, byte[] valueBytes, Cluster cluster) {

    //custom any logic here...
    Integer keyInt=Integer.parseInt(key.toString());
    return keyInt % PARTITION_COUNT;
  }

  @Override
  public void close() {
  }
}
```

Görüldüğü üzere her partition'un ID'si bir integer'dır. Zaten TopicPartition'un instance'ı; topic ismi ve partition id'si ile yaratılır:
    
> TopicPartition(String topic, int partition) 

kaynak: (source-id: 377)

# committing an offset
"committing an offset" means that consumer client got the message. that means that spesific record(message) is "consumed". Kafka’da default kendi içerisinde offset'leri tuttuğu bir topic vardır. Kafka, offsetlerin (record'ların) consume edilip edilmediğini bu topic içerisine attığı kayıtlardan takip eder. kaynak: (source-id: 378) "Atomic multi-partition writes" başlığı, 3üncü paragraf.

- # record
    yollanan her mesaj terminolojide __record__ olarak geçer. her record key-value şeklindedir. kafka her record'un okunması sırasını garanti eder.

- # Broker
    her apache kafka node'una denir.

- # kafka cluster
    birçok broker'ın bir arada çalıştığı ortama denir.

- # partition
    - her broker'da birden fazla partition olabilir.
    - bir topic biden fazla partition'da yer alabilir.
    - her topic mutlaka en az 1 partition'da yer almalıdır.

    bir partition'da sadece 1 farklı topic olabileceğinden, partition id'leri topic bazından unique olarak düşünmeliyiz. Yani; "important-topic" isimli topicin 1 id'li partitionu ile, "warnings-topic" isimli topic'in 1 id'li partition'u farklı partition'lardır.

    partition'lar kuyruk gibi düşünülebilir. bir kuyruktaki mesajı hem topic, hemde partition numarası ile çekebiliriz. kaynak: (source-id: 379) "KafkaConsumer" başlığı 3üncü kod bloğu örneği.

    Yukarıdaki örnek python'da yazılmış, fakat Java client'ta da aynı obje mevcut. TopicPartition objesi; topic ismi ve partition id'si ile instance'ı yaratılır:
    
    > TopicPartition(String topic, int partition) 

    kaynak: (source-id: 377)

- # offset
    offset bilişimde: the distance to an element within a data object

    mesajın o partition'daki pozisyonudur. bu değer hiç değişmez.

- # replication factor
    her partition'un kaç adet broker'da klonlanacağını belirtebiliyoruz. mesajımızı X node'unun A partition'una gönderelim. X node'u mesajı aldığında diğer node'ların ilgili partition'larına yollar. bu şekilde bir makinemiz down olduğunda, diğer makineler mesajı saklamaya ve dağıtmaya devam edecektir.

    her partition için __leader__ ve __follower (or in-sync replicas or ISR)__ broker'lar vardır. follower'lar (ilgili partition için) sadece data'nın klonlanmasında görevlidirler. aynı zamanda leader çökerse follower'lardan biri leader olarak devreye girmektedir. kaynak: (source-id: 381) "Replication: Kafka Partition Leaders, Followers, and ISRs." başlığı. + Diğer kaynak: (source-id: 382) "What is Replication?" başlığı "Leader for a partition:" ile başlayan 7inci paragraf.

    X partition'a bir mesaj atıldı. Bu mesaj X partition'un liderine yollanmamış olsun. O zaman bu isteği alan node, ilgili mesajı o partition'un liderine forward eder. kaynak: (source-id: 383) "Kafka topic partition" başlığı 5inci paragraf.

    bir topic yaratma örneği:

    > /bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

    Bu komutta:
    
    - replication-factor parametresinde, bu topic ve ona bağlı partition'ın kaç adet node(broker)'da tutulacağını belirttik.
    - partitions ile bu topic'e bağlı kaç farklı partition olması gerektiğini belirlemiş olduk
    - zookeeper parametresi başka yerde anlatılıyor (bu konu için önemsiz bilgi)

- # commited record
    - record is commited only if all follower's are got the record successfully. kaynak: (source-id: 381) "Kafka Architecture: Kafka Replication – Replicating to Partition 0" başlığı, 1inci paragraf.
    - Client mesajın commit edilip edilmediğini API aracılığı ile bilebiliyor. kaynak: (source-id: 385) "KAFKA REPLICATION: 0 TO 60 IN 1 MINUTE" başlığı , 3üncü paragrafın ilk cümlesi.
    - Consumer'lar sadece commit edilmiş record'ları okuyabiliyor. kaynak: (source-id: 381) "Kafka Architecture: Kafka Replication – Replicating to Partition 0" başlığı, 1inci paragraf.

- # acknowledgment (or ACK)
  producer (client) tarafında ayarlanan bir parametredir. bu parametre şu değerleri alabilir:
  - 0: client isteği atar. isteğin bir yere ulaşıp ulaşmadığı ile hiç ilgilenmez.
  - 1: client sadece leader'ın isteği aldığından emin olana kadar bekler. hata alırsa tekrar istek atar.
  - all: o partition için tüm follower'ların bu record'u aldığından emin olana kadar bekler. hata alırsa tekrar istek atar.

  kaynak: (source-id: 387) " Apache Kafka ack-value" başlığı.

# message queuing vs publish-subscribe
  kafka 2 tip'te mesaj yollama işlemini yapabiliyor. publish-subscribe'da tüm consumer'lara mesaj giderken, queuing modunda sadece 1 adet consumer mesajı okuyabiliyor. kaynak: (source-id: 388) "Kafka as a Messaging System" başlığı ilk paragraf.

# Kafdrop
kafka için açık kaynaklı GUI monitoring uygulaması. Kafdrop kafka API'sini kullanarak web arayüzde monitor ettiği bilgileri gösteriyor. Sadece temel özellikleri içeriyor. 

# MirrorMaker
Kafka default'ta (tek başına) multi DC hizmeti mevcut diil. Bunun için kafka sunucusundan bağımsız yazılımlardan yararlanmak gerekiyor. Bunlar biride MirrorMaker.

MirrorMaker kafkalardan bağımsız olarak ayağa kaldırılıyor. Ayağa kaldırırken tüm DC'lerdeki her kafkanın ip-port bilgileri config ile MirrorMaker'e veriliyor. Aynı zamanda MirrorMaker'a, hangi kafkalardaki topiclerin hangi kafkalara sync olacağı gibi bilgiler veriliyor. BU bilgiler doğrultusunda MirrorMaker consumer ve producer olarak davranıp, DC'ler arasında bu kafkaları sync etmeye çalışıyor.

'Confluent' firmasının geliştirdiği 'Replicator', 'MirrorMaker'a alternatiftir.

# kafka connect
kafka'dan bağımsız çalışan bir instance'dır. 2 farklı connector'ü vardır:
- __Source connector__

  farklı bağımsız sistemlerden (örneğin veritabanlarından), data okur ve bunları kafka'da topic'lere kaydeder. örnek: postre-sql'deki bir tablodaki her dğeişikliğin, kafka'da topic altında event'lerde görmek isteyebiliriz.

  Kafka connect, değişikliğkleri okuyacağı sistemin connector'üne ihtiyaç duyar. örnek "mysql connector jar"'ını path'e eklemek zorundayız. YUada "debezium" gibi aracı uygulamalar kullanmak durumundayız.

- __Sink connector__

  source'nin tersine, kafka topic'lerindeki data'ların bağımsız bir sisteme kaydedilmesini sağlar. örnek: her kafka'daki data'nın elastic-serach'e kaydedilmesini isteyebiliriz.

# kafka vs rabbitmq
kafka streaming platform olarak geçer, rabbitmq ise messaging broker'dır. asıl fark şurdadır: kafka kuyruğu silmez. client kuyrukta nerde olduğunu (index'i) kendi tutmak zorundadır. bu onu "consumer-centric" yapar. bu sebeple streaming platform olarak kullanılır. çünkü her client istediği gibi geçmişe ileriye gidebilir, yani stream edebilir. rabbitmq da ise push vardır. rabbitmq mesajları karşıya push'lar. eski mesjaları client göremez. rabbitmq'daki bu çalışma modeline "__smart-broker / dumb consumer__" denir.

rabbitmq mesajları persist edebilir fakat bunların çekilmiş client'lar tarafından tekrar çekilebilmesini sağlayamaz.

rabbitmq mesajların consumer'lara ulaşıp ulaşmadığını garanti edebilir (retry yapabilir).

# message queue vs message broker
message broker yazılımı, message queue'ların management'ini sağlar. kaynak: (source-id: 389) title: "What is a message broker?", 4th paragraph.

- enqueue
  
  fiildir. sıraya almak.

  verb. add item to queue.

- dequeue

  fiildir. kuyruktan çıkarmak.

# event bus için yazılımlar (broker'lar)
  - Apache Kafka

  - JMS (or Java Messaging Service)

    JMS API, JavaEE'nin bir API spesifikasyonu. Runtime'da bir implementasyon kullanmak zorundayız. Bu implementasyonlara __JMS provider__ (broker) deniyor. JMS client'lar, JMS provider'a bağlanarak çalışır. JMS client destekleyen provider'lardan bazıları (bu liste normal JMS olmayan client'lar tarafından da message-queue olarak kullanılabilir):

    - Apache ActiveMQ

      "Artemis" kod adı ile ActiveMQ projesi paralelden geliştiriliyor. Artemis stabil olduğunda eski proje (artemis'in başlaması ile artık "Classic" olarak adlandırılıyor) sonlandırılacak.

    - Open Message Queue (or OpenMQ or Open MQ)

      Oracle tarafından geliştirilen, GlassFish içerisinde default olarak geliyor. İstenirse standalone da kullanılabiliyor.

    - OpenJMS

    - Oracle Advanced Queuing (or AQ)

    - IBM MQ (or old-name:MQSeries or old-name:WebSphere MQ)

    - Rabbit mq (Pivotal Software tarafından geliştiriliyor)
