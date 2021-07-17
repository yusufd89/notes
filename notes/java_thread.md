############################

############################
# JAVA THREAD
############################

############################

# java thread
thread kelime anlamı: 1. iplik, 2. konu

# thread oluşturma
iki şekilde thread yaratılabilir:

1- Runnable interfacesi implemente edilerek 

2- thread sınıfı extend edilerek

örnek:

```java
class ImplementsRunnable implements Runnable {

   //runnable sadece run metodunu içerir.

   private int counter = 0;

   public void run() {

         counter++;

         System.out.println("ImplementsRunnable : Counter : " + counter);
   }
 }

 class ExtendsThread extends Thread {

   private int counter = 0;

   public void run() {

         counter++;

         System.out.println("ExtendsThread : Counter : " + counter);
   }
 }
```

hangisini kullanmak gerekli:

- runnable kullanılırsa; ImplementsRunnable sınıfımız isterse başka sınıflardan extend edebilir. fakat ExtendsThread zaten extend hakkını kullandığı için tekrar extend edemez (java kuralı)

- runnable'den implemente etmiş sınıfta başlatılan her thread "private int counter" değerini ortak kullanır.

ImplementsRunnable direk çağrılamaz. Thread içine atılmalıdır.

```java
Thread t1 = new Thread(new ImplementsRunnable());
t1.start();

Thread t2 = new Thread(new ImplementsRunnable());
t2.start();
```

yukarıda t1 ve t2 aynı "counter" değeri kullanır.

# void run vs void start
run metodu çağrıldığında yeni bir paralel thread yaratılmaz. fakat satrt metodu run metodunu thread yaratarak çağırır.

start metodu aynı sınıf için 2 kere çağrılırsa IllegalThreadStateException fırlatır.

# void sleep(long)
milisecond cinsinden parametre alır ve ilgili thread'i o kadar bekletir.

# void join()
örnek:

```java
t1.join();
a++;
```

t1 thredi sonlanmadan a++ çalışmayacaktır.

# void join(long)

örnek:

```java
t1.join(3000);
a++;
```

t1 ölürse a++ çalışır, yada 3 saniye içinde ölmezse a++ çalışır. 

# static Thread currentThread()
bu metod o anda çalışmakta olan thread'in instance'ını dönüyor. static bir metod olmasına rağmen o anda bu metodu çağran thread'in bilgisini alabiliyor. 

# getName setname
thread sınıfına isteğe bağlı isim atanabiliyor.

# setDaemon geDdaemon
boolean bir parametre alır. normalde java tüm thread'ler sonlanmadan JVM'i kapatmaz. daemon thread'lar bu kurala dahil diildir. daemon thread'ler sorgulanmadan JVM kapanabilir. 


# Executors
Birçok thread'i yönetebilmemizi sağlayan bir yapıdır.

ExecutorService executor = Executors.newFixedThreadPool(5);//onceden 5 thread açık tutuluyor. hızlı baslangıc icin.

```java
for (int i = 0; i < 10; i++) {  

   MyRunnableImpl runnable = new MyRunnableImpl(i);  
   executor.execute(runnable);  
}

executor.shutdown(); 

while (!executor.isTerminated()) {  

     //wait
}  

System.out.println("Finished all threads");  
```

# ThreadGroup

```java
ThreadGroup tg1 = new ThreadGroup("Group A");   

Thread t1 = new Thread(tg1,new MyRunnable(),"one");     

Thread t2 = new Thread(tg1,new MyRunnable(),"two");   
```

artık grupandıklarından dolayı tümüne aynı işlemi uygulamayabiliriz:

```java
Thread.currentThread().getThreadGroup().interrupt();
```

# synchronized
bu java keyword'ü metodun imzasına koyulduğunda o metod aynı anda en fazla 1 thread tarafından çalıştırılabilir olur. diğer threadler beklemeye alınır.

bu keyword ile isterske sadece belli bir kod bloğunuda kilitleyebiliriz:

```java
public void anyMethod() {

    //some code here

    synchronized (objRef) {

        //some code here

    }

    //some code here
}
```

yukarıdaki synchronized bir metod değil. özel bir syntax. burada objRef bu kod bloğunun o andaki thread için bekletilip bekletilmeyeceğine karar veriyor.

JVM, her aynı objRef'nin o kısma girmesine engel oluyor. yani "X" değerinde objRef olan iki thread varsa, aynı anda bu bloğa giremezler. 

objRef aynı zamanda "class" tipinde de değer alıyor. Örneğin Person.class. Eğer buparametre verilirse, Person'dan oluşmuş bütün thread'ler buraya girmek için sırada bekleyecektir.

# Collections.synchronizedMap()
Collections.synchronizedMap() ve ConcurrentHashMap iki farklı thread-safe sunan alternatiflerdir. Çünkü standart java HashMap thread-safe diildir.

on ConcurrentHashMap:
- read operations are non-blocking
- write operations take a lock on a particular segment or bucket. The default bucket or concurrency level is 16, which means 16 threads can write at any instant after taking a lock on a segment or bucket.

# thread safe
bu terim tüm programla dilleri için geçerlidir. bir metod aynı anda istenildiği kadar thread tarafından çağrılıyor ve sorunsuz çalışıyor ise o metod thread safe'tir. bir sınıf thread safe ise o sınıfın içindeki tüm public metodlar thread safe anlamına gelir.

çağrılan metod; dışarıdaki kaynaklardan yararlanıyorsa ve özel olarak threadlocal, mutual exclusion, synchronized gibi çözümler kullanmamış ise; çağrılan metod, thread local değildir. mutual exclusion, synchronized gibi çözümler kullanılırsa bu sefer bu metodu çok thread aynı anda kullandığında sistem yavaşlayacaktır. bu sebeple daha verimli çözümler tavsiye edilir.

örnek:

StringBuilder thread safe diildir. Bu durumda;

```java
private StringBuilder sb = new StringBuilder("abc");

public void addProperty(String name, String value) {
   
      sb.append(name).append('=').append(value);
}
```

Bu şekilde çağırırsak konuş yanlış yapma olasılığı vardır:

```
Thread1: addProperty("a", "b");
Thread2: addProperty("c", "d");
Thread3: addProperty("e", "f");
```

# threadlocal
javada bir sınıftır. aşağıdaki örnekte basit şekilde kullanımı mevcut. ThreadLocal her thread için yeni bir nesne yaratmaktadır. nesneyi yaratmak için initialValue() metodunu çağırır.

```java
public class Foo
{
    private final ThreadLocal<SimpleDateFormat> formatter = new ThreadLocal<SimpleDateFormat>(){

        @Override
        protected SimpleDateFormat initialValue()
        {
            return new SimpleDateFormat("yyyyMMdd HHmm");
        }
    };

    public String formatIt(Date date)
    {
        return formatter.get().format(date);
    }
}
```

# wait notify
Javanın obje sınıfına ait metodlarıdır. wait ile o thread artık bekleme durumuna girer. taki başka biri o thread üzerinde notify metodunu çağırana kadar.
