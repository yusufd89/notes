############################

############################
# ALGORITHMS DATA STRUCTURES
############################

############################

# Java Collections
Türeme sırası aşağıdaki gibidir.

Iterable -> interface

Collections -> interface (extends Iterable)

List -> interface (extends Collection)

ArrayList -> Class (extends List)

Burada temel sınıflar tek bir şemada gösterilmiştir: (source-id: 408)

# LinkedList vs ArrayList
List'ten türemiş bir diğer sınıf LinkedList'tir. ArrayList ile ortak arayüzü kullandıklarından kullanım farkı yoktur, fakat algoritmaları gereği hız ve bellek kullanımları farklıdır. LinkedList üzerinde her eleman bir sonraki elemanın referansını tutar. bu sebeple araya eklenene değerler hızlıca eklenip silinebilir. oysa ArrayList'te araya ekleme ve silmeler çok maliyetlidir.

# Iterator
Iterator'dan türetilen sınıflar Iterator instance'ı dönen bir metod içerir. Bu metoddan dönen değerler for-each döngüsü ile dönüldüğünde değerler silinebilir hale gelir. Aksi halde; iteratorsız, direk collection'ı dönersek ve döngü içerisinde eleman silersek, collection algoritma yapısı gereği hata alırız. Collection yapıları; objeleri tutmak için belli algoritmalar kullanır.

# Map
Hash ile işlem yapan collection'ların (Set, hash-map...) işleyişmantığı, "hashcode" başlığında detaylı anlatılmaktadır.

Map interface'si hiçbir yerden türememiştir. Map<Class1, Class2> şeklinde tanımlanır. Her class1 çeşidinde bir objeye karşılık, class2 çeşidinde bir obje vardır. Key-value şeklinde tutar. Map'te tüm value'ları almak ve tüm key'leri almak için bir metod vardır. Bu metodlar'dan dönen değerler kullanılarak for döngüleri yapılabilir.

Map sınıfından türetilmiş sınıfllar aynı interfaceden türedikleri için ortak özellikler sunarlar. fakat algortimaları gereği hızları ve döngü esnasında verdiği değerlerin sıraları farklıdır.

- __HashMap__: döngü sırasında hangi elemanı vereceğinin garantisi yoktur.

- __TreeMap__: döngü sırasında elemanları sırası ile verir. burada sıra aşağıdakilerden istediğimiz yöntem ile belirlenir:

  - java.lang.Comparable

    bu interfaceden türeyen class'lar compareto metodunu implemente etmek zorundadır. treemap bu metodlardan yararlanarak sort edebilir.
  
    java dünyası; bu interface'nin, sınıflar için "natural order" yaptığı terimini kullanmaktadır.

  - java.util.Comparator
  
    bu interface'yi türettiğimiz class'ta "int compare(object1, object2)" metodu implemente edilmelidir. return olan integer değeri öncelik değeridir.
    
    Bu metod dto'ların içinde değildir. external bir class olarak compare işlemini gerçekleştirmemizi sağlar.

- __LinkedHashMap__: map.put(object) metodunun işlediği sıra ile döngü sırasında elemanlar iterate edilir.

- __IdentityHashMap__: HashMap ile aynı mantıktadır. HashMap eşitlikleri int dönen hashCode() metodu ile kontrol ederken, IdentityHashMap == ile kontrol eder (instance referans kontrolü).

# SortedMap
Map'ten türemiş bir interface'tir. TreeMap gibi sıranın önemli olduğu Map'ler bu interface'den kullanılır.

# HashTable
__HashMap__ datastructure'nin ikinci ismidir. Bu java dünmyasın dışında da bu şekilde kullanılır. java dünyasında tek farkı şudur: Java'da "java.util.Hashtable" sınıfı thread-safe'dir, "java.util.HashMap" ise diildir.

bir çeşit veri yapısıdır. bir tablo düşünelim. her satırı bir dizi'de tutmak yerine, her satırın primary değerleri ile hash'ini alıp, hash'ini index olarak kullanabliriz.

hash table'larda arama işlemi çok hızlıdır. listeye bir data eklemek array'e göre daha uzundur çünkü hash alma işlemi gerektirir. 

# EnumMap
"Key" tarafında sadece enum değerleri kabul etmektedir.

# Set
Set, Collectiondan türemiştir. Set içerisinde dublicate nesne olamaz.

- __HashSet__

  Set'ten türemiştir. Arkada hash-map tutar. her elemanı hash değeri ile bu hash-map'e atar. sıra yine set'te olduğu gibi garanti diildir.

- __LinkedHashSet__

  HashSet'ten türemiştir. Tek farkları HashSet'e göre iterasyon sırasının tutumasıdır (insertation order'ı saklar).

- __TreeSet__

  Set'ten türemiştir. temel farkı compareTo() metodu ile iterasyon sırasını saklar.

# unmodifiable collections
List<Character> immutablelist = Collections.unmodifiableList(list);

bu şekilde varolan bir listeyi editlenemeyecek bir liste olarak kopyasını oluşturuyoruz. Bu kopya listede add(obj) gibi metodlar hala mevcuttur. fakat liste elemanlarında editleme yapılmak istendiğinde unsupportedoperationexception fırlatılmaktadır. bu sınıf genelde bir yere listeyi göndermek fakat değişiklik yapılmasının riskli olduğu düşünüldüğü durumlarda kullanılmaktadır.

# Veri yapıları

# Linked List (or bağlı liste) vs Double Linked List vs Circle Linked List (or Dairesel bağlı liste)

Linked List sadece bir sonraki elemanın adresini içeriyorken, double linked list bir önceki elemanında adresini içeriyor. performans açısından avantaj sağlarken bellekten zarar etmektedir.

Dairesel Linked List ise son elemanı listenin başındaki elemana referans etmektedir. Dairesel Linked List'ler isteğe bağlı double olabilirler.

# Stack (or yığın or yığıt or çıkın)

Nesne ekleme ve çıkarmalarının sadece en üstten (top) yapıldığı veri yapısına denir. LIFO mantığı işler.

en üstteki elemanlara bu işlemler yapılabilir. push ile eleman eklenir, pop ile eleman çıkarılır. peek (or top) fonksiyonu ile ise, en üstteki eleman okunur (fakat listeden silinmez/kaldırılmaz).

# Kuyruk (or queue)

FIFO mantığında çalışır. Kuyruğun ara elemanlarına erişim yoktur. Son'a eklenir (enqueue) yada ilk eleman çıkarılır (dequeue).

- __PriorityQueue__ java da olan, yine java'daki 'Queue'dan türemiş bir sınıftır. Bu sınıf genel veri yapılarında __priority queue__ olarak adlandırılır.  Bu sınıfta kuyruk "compare" metoduna göre sıralanır. Dolayısı ile her eklenen yeni eleman kuyruğa compare metodundan dönen sıraya göre karar verildiği sıraya girer. 

# graph

Node'lar birbirlerine istedikleri gibi (döngüsel dahi) bağlanabilir. bi node 10 tane node'a, aynı graph'ta bir node, sadece 1 noda'a bağlı olabilir. 

bellekte tutulurken 2 şekilde tutulabilir:

- __komşuluk matrisi (or adjacency matrix)__: çok yer kaplar. fakat komşuluk tespit etme kısa sürer.

```
   A B C

A  0 1 0

B  1 1 1 

C  0 1 1
```

- __komşuluk listesi (or adjacency list)__: az yer kaplar. fakat komşuluk tespiti yavaştır. veri yapısı oluşturmak daha komplekstir.

```
A -> B

B -> C -> D
```

# ağaç (or tree)
bir çeşit graph'tır (fakat her graph bir ağaç diildir).

bir node'a gitmek ulaşabilmek için sadece 1 farklı yol olmalıdır. bazı tanımlar:

__Yaprak (or Leaf)__: Çocuğu olmayan düğümdür

__Kardeş (or Sibling)__: Ebeveyni aynı olan düğümlerdir.

__Ata (or Ancestor)__: Bir d düğümünün ataları, d'den köke olan yol üzerindeki tüm düğümlerdir.

__Ayrıt (or edge)__: düğümler arası ilişkiye verilen isimdir.

__descendant (or torunlarıdır)__: bir düğümünü çocuklarına bağlı tüm alt düğümlerdir.

__level (or düzey or seviye)__: bir düğümün köke olan uzaklığıdır.

__height (or yükseklik)__: herhangi bir x node'unun yüksekliği, torunları arasında ona en uzak olan yaprağa olan uzaklığıdır.

__derinlik (or depth)__: bir ağacın derinliği ona en uzak olan yapara olan uzaklıktır.

## ağaç çeşitleri

   - ### Binary Tree (or İkili Ağaç)
   
     İkili ağaçta bir düğümün __sol çocuk__ ve __sağ çocuk__ olmak üzere en fazla iki çocuğu olabilir

   - ### Full Binary Tree

     bir binary tree çeşididir. her düğümün aynı seviyede derinliği olmalıdır ve her düğümün mutlaka 2 çocuğu vardır. ağaç dengeli çizildiğinde her taraftan aynı boyutta görünür. örnek:

     ```
           4 
          / \
         /   \
        2     5 
       / \   / \
      1   3 4   6
     ```

   - ### Complete Binary Tree

     binary tree türevidir. yapraklar arasındaki deirnlik farkı en fazla 1'dir. her eklenen düğüm sol'dan sağa doğru eklenir. 1 derinlik bitmeden diğerine geçilmez. örnekler:

     ```
           4 
          / \
         /   \
        2     5 
       / \   / \
      1   3 4   

      
           4 
          / \
         /   \
        2     5 
       / \   / \
      1       
     
     ```

   - ### Height Balanced Binary Tree

     Her düğümünü sol alt ağacının yüksekliği ile sağ alt ağacının yüksekliği ile farkı en fazla 1'dir. örnekler:

     ```
           4 
          / \
         /   \
        2     5 
       / \   / \
      1   3     6

                        4 
                       / \
                      /   \
                     /     \
                    /       \
                  2           5 
                /   \       /   \
                                 6

                        1 
                       / \
                      /   \
                     /     \
                    /       \
                  1           1 
                /   \       /   \
               1                 1

                        1 
                       / \
                      /   \
                     /     \
                    /       \
                  1           1 
                /   \       /   \
               1           1     
                          /     
                          1
     ```

   - ### Yığın Ağacı (or Heap tree or öbek or binary heap)

     bir binary tree türevidir. her düğüm, tüm alt düğümlerinden büyük olan ağaçtır.

     herhangi bir ağacı, "yığın ağacı" kuralların uygun hale getirmek için yapılan işlemlere __yığınlamak (or heapify)__ denir.

   - ### İkili Arama Ağacı (or Binary Search Tree)

     binary tree çeşididir. her düğümün sol çocuğu sağ çocuğundan büyük olan ağaçtır. babanın alttakilerden büyük olup olmaması önemli diildir.

## ağaç içinde gezinme

   - Pre-order Traversal (root-left-right)
        - Kökü ziyaret et
        - Sol alt ağacı dolaş
        - Sağ alt ağacı dolaş
   - In-order Traversal (left-root-right)
        - Sol alt ağacı dolaş
        - Kökü ziyaret et
        - Sağ alt ağacı dolaş
   - Post-order Traversal (left-right-root)
        - Sol alt ağacı dolaş
        - Sağ alt ağacı dolaş
        - Kökü ziyaret et
    Level-order Traversal (Breadth-first)
        - Kökü ziyaret et
        - Soldan sağa ağacı dolaş

    örnekte incelersek:

    ```
                        F 
                       / \
                      /   \
                     /     \
                    /       \
                  B          G 
                /   \         \
               A     D         I
                    / \       /
                   C   E     H
    ```

    Pre-order   : F, B, A, D, C, E, G, I, H

    In-order    : A, B, C, D, E, F, G, H, I

    Post-order  : A, C, E, D, B, H, I, G, F

    Level-order : F, B, G, A, D, I, C, E, H

# Expression Tree (or İfade Ağaçları)

```
                        + 
                       / \
                      /   \
                     /     \
                    /       \
                   *         7
                 /   \
                +     c
               / \
              a   b
```

```
infix   : (a+b)*c + 7 (in-order-traversal uygulandığında bu sonuç elde edilir)

prefix  : +*+abc7     (Pre-order traversal)

postfix : ab+c*7+     (post-order traversal)
```

# Infix vs Prefix vs Postfix

Aritmetik işlemler 3*8+9 gibi derleyiciler tarafından çözümlenirken  bir sıralamaya koyulmaktadırlar. Infix vs Prefix vs Postfix, bu sıralama (notasyon) gösterimlerine verilen 3 alternatiftir. Bazı notasyonlara göre önce işaretler yer almaktadır gibi… Notasyonları gerçekleştirirken ve çözümlerken veri yapılarından yararlanılır.

# infix

matematiksel hesaplamalar (örnek: 3+(2*4) ) insanın okuyabileceği türden yazıldıklarında infix formatındadırlar. derleyiciler bu hespalamaları yapabilmek için bunları  bir formata çevirir. bunlardan bazı formatlar: Prefix notasyonu (or polish notation), Postfix notasyonu (or RPN or reverse polish notation). Bu iki örnek notasyonda da paranteze ihtiyaç yoktur.
