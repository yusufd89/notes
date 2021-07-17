############################

############################
# GRADLE
############################

############################

# gradle

groovy syntax'ı ile build script yazmaya yarıyor (groovy syntax'ı başka başıkta anlatılmıştır). sadece jvm tabanlı projeler için değil, programlama dilinden bağımsızdır. şu anda çoğu eklentisi java tabanlı prjeler için yazdılığı için öyle bir algı oluşuştur.

# kotlin
gradle groovy'nin yanında kotlin syntax'ını da destekliyor. dosyanın kotlinle yazıldığını belirtmek için her gradle dosyasının sonuna kts eklemek gerekiyor. örnek:

> build.gradle.kts

# files

  - # build.gradle

  tüm işleyişin belirlendiği dosya

  - # gradle.properties

  properties formatında dosyasıdır. key-value şeklinde build.gradle tarafına parametre geçmek için kullanılır.

  - # settings.gradle

  tüm sub-modüller için geçerli olan key-value şeklindeki property'leri ve işleyişin de belirlenebebileceği dosyadır. sub-modüller içeren projede sadece 1 tane (root projede) olması gerekir alt projelerde olmamalıdır.

# lifecycle

  - initialization phase

    butada gradle sadece submodüllerin varolup olmadıklarını kontrol ediyor.

  - configuration phase
  
    __Gradle builds a Directed Acyclic Graph (DAG)__ algoritması kullanarak tasklarda döngü olup olmadığını temsil ediyor.

  - execution phase

    tüm build tasklarının çalıştırıldığı fazdır. ilk 2 faz IDE eklentileri tarafından default çağrılırken, bu fazın çağrılması için bir komut gerçekmektedir.

# tasks

gradle'da fazlar aslında basit yapıdadır. gradle tasklar üzerine kuruludur. task başka taskları çağırır. hangi taskların olacağına plugin'ler karar verir. java-plugin'i, bazı istisnalar dışında maven ile aynı isimlere sahip tasklar tanımlamıştır. bu şekilde maven'a alışmış geliştiriciler, gradle'daki taskları da çağırabilir.

build.gradle içinde;

```groovy
task hello {
   doLast {
      println 'tutorialspoint'
   }
}
```

taskımızı şu şekilde run ediyoruz:

> gradle –q hello

yada 

> gradlew hello

gradlewrapper otomatik olarak task çağırmaktadır.

"gradlew --help" ile "gradlew help" ayrı komutlardır.

eclipse'te gradle eklentisi varsa "gradle tasks" view'ı tüm gradle tasklarını listelemektedir. gradle taskları önce proje bazlı gruplandırılmakta daha alt seviyede ise 'task grup'ları bazında listelenmektedir. tasklarımızı gruplandırmak istersek; örnek hello taskımızı bir grup altına alalım:

build.gradle dosyamızın içine bunu eklememiz yeterli:

```groovy
hello.group = MY_GROUP_NAME
```

Gradle'da hiçbir eklenti yoksa "Help" ve grubu altında bir kaç task varsayılan olarak tanımlı gelir. bunlar gradle executable'ın içine gömülmüş tasklardır:

- build setup (task grup)

  - init (task)

    boş bir gradle proje oluşturur. bulunduğumuz dizinde, gradle.build dosyası vs oluşturur...

  - wrapper (task)

    gradle wrapper dosyalarını bulunduğumuz dizinde oluşturur.

- help (task group)

  - tasks (task)

    Displays the tasks runnable from root project

  - help

    displays help

  - (and others)
  
# task dependsOn

```groovy
task task4(dependsOn: [task1, task3]) << {

   println 'building task4'
}
```

artık task4 koştuğunda önce task1 sonra task3 koşacaktır. task1 task2 koşmuşsa (başka task tarafından) o zaman tekrar koşmaz.

# :my-sub-project1:myTask

bu şekilde altprojedeki bir taskı çağırmış oluyoruz. örnek komut:

> gradle :order-microservice:compile

yada asağıdaki aynı taskı çalıştırmaktadır:

> gradle order-microservice:compile

# defaultTasks

defaultTasks'lar eğer task ismi komut satırında hiç verilmemiş ise koşacak tasklardır. örnek:

```groovy
defaultTasks 'clean', 'run'

task clean {
    doLast {
        println 'Default Cleaning!'
    }
}

task run {
    doLast {
        println 'Default Running!'
    }
}

task other {
    doLast {
        println "I'm not a default task!"
    }
}
```

> grdale -q

komutu sadece clean ve run tasklarını çağıracaktır.

# java plugin

```groovy
apply plugin: 'java'

repositories {

   mavenCentral()
}

dependencies {

   compile group: 'org.hibernate', name: 'hibernate-core', version: '3.6.7.Final'

   testCompile group: 'junit', name: 'junit', version: '4.+'

}
```

# java plugin dependency types

- Compile
- Runtime
- Test Compile
- Test Runtime

# sourceSet

java plugin'inin sunduğu bir konsepttir. sourceSet; birlikte derlenecek resource ve java kodlarının bulunduğu dizinledir. örneğin default tanımlı main sourceSet'i:

```groovy
sourceSets {

    main {

        java {

            srcDirs = ['src/main/java']

        }

        resources {

            srcDirs = ['src/main/resources']

        }

    }

}
```

gibi test source set'i de bulunur. isteğe bağlı ek source set'ler belirlenebilir. örnek: "integration-test" soruceSet gibi.
