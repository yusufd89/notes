############################

############################
# ALGORITHM SORT
############################

############################

# Sıralama Algortitlamaları (or Sorting Algorithms)

## natural ordering

İnsanların daha rahat okuyabileceği bir sıralamadır.

traditional sort:

```
img1.png
img10.png
img12.png
img2.png
```

__natural sort__:

```
img1.png
img2.png
img10.png
img12.png
```

natural sorting'in özel karakterlerle, yada büyük küçük harflerle nasıl sıralama yapacağının bir standardı yoktur. Genelde alphanumeric'leri sort etmek için kullanılan bir yöntemdir.

natural sorting'i implemente etmenin birçok yolu var. bir kaynakta sayı ve alfabeye ait olmayan karakterler ignore ediliyordu. aşağıdaki şekilde görüldüğü gibi, her string'i farklı parçalara bölerek sıralama yapmaya çalışıyordu:

```
foo       =>  "foo",  -1
foobar    =>  "foo",  -1,  "bar"
foo13     =>  "foo",  13,
foo13xyz  =>  "foo",  13,  "xyz"
```

"GNU ls" komutunun "version sort" özelliği var. parametre aktif edilip sort edildiğinde, "natural sorting" görevi görüyor.

# lexicographic (or lexicographical order)
matematikte String listelerinin sıralanmasıdır. Bunun birçok çeşidi vardır. Bazıları:
- alphabetical order
- alphanumerical order

## sıralama algoritmalarının özellikleri

- __Stability__

  Gerekmediği sürece (aynı değere sahip elemenların) yer değiştirmemesi.
  
  Sadece sayı değeri tuttuğumuz elemanlarda bunun bir önemi yok. Fakat bu eleman içerisinde farklı nesneye referans ediyor ise (map gibi) o zaman sıranın yer değiştirmemesi gerekmektedir. örnek bir tablomuz olsun:

  ```
  İsim   No
  Ahmet  101
  Ahmet  102
  Ahmet  103
  Mehmet 105
  ```

  Yukarıda "isim" sutunu binary yapıp sıralamak isteyebiliriz. Fakat gereksiz yer değiştirmesini istemeyebiliriz. çünkü öncesinde son kullanıcı tabloyu noya öre sıralamış olabilir.

- __in-place algorithm__

  ekstra bellek ihtiyacı duymadan sıralama yapan algoritmalara denir. Fakat ektra çok ufak bir alan hitiyacı olabilir. örneğin index tutuyorduk, dizinin max elemanını tutuyordur. bunlar ekstra sayılmaz.

  Buna uymayan algoritmalara: __not-in-place (or out-of-place)__ denir.

# Sıralama algoritmaları

- ## Kabarcık Sıralaması (or Baloncuk sıralaması or Bubble Sort)

Diziyi eleman sayısı kadar dolaşır. Her dolaşmada her elemanı sağ taraftaki ile kontrol edip yer değiştirtir.

- ## Seçerek Sıralama (or Selection Sort)

Diziyi sürekli dolaşır. En ufak elemanı geçici bir dizinin başına atar. Daha sonraki dolaşımlarda tekrar en ufak elemanı bulur geçici dizideki 2inci elemana atar.

- ## Hızlı Sıralama Algoritması (or Quick Sort Algorithm)

bir eleman seçilir. bu eleman pivot (türkçe ve ingilizce'de bu şekilde kullanılır) adı verilir. bu elemanın, hangi index'teki eleman seçileceği hakkında birçok farklı görüş mevcuttur.

her pivotun sağ tarafında ondan büyük elemanlar yerleştirilir ve sol tarafında ise küçük elemanlar yerleştirilir. aynı işlem, sağ ve sol taraf içinde yapılacaktır. böyle olunca en ufak parçalara (3 elemana düşünceye kadar) bölündüğünde tekrar birleştirdiklerinde dizi sıralanmış olacaktır.

pivotun sağ ve sol tarafına yerleştirme işlemi şu şekilde yapılır: dizinin ilk ve son elemanı pivot ile karşılaştırılır. eğer ilk-elemen>=pivot>=son-eleman ise ilk-eleman ve son-eleman swap (yer değiştirir) edilir. Daha sonra dizinin baştan ikinci ve sonrdan ikinci elemanı için aynı işlem yapılır. sonra 3üncü... tabi dizinin ortasına gelene kadar.

Buradan sonra dizinin sağ ve sol tarafı ayrı ayrı rekürsiv olarak quick-sort algoritmasına sokulur. Burada ayrı ayrı quick-sort'a atılan arrya'ların referans'larını quick-sort metoduna geçmemiz yeterli. yeni bir liste oluşturup klonalamaya gerek yok.

- ## Birleştirme Sıralaması (or Merge Sort)

Diziyi sürekli ikiye böler. her elemanı kendi içinde 2 şerli şekilde sıralar. Sonra bunları birleştirir. Birleştirirken de elemanların büyüklüklerini değerlendirir.

- ## Yığınlama Sıralaması (or Heap Sort)

öncelikle sıralanması istenen dizi heap ağacı kurallarına uygun şekilde ağaç haline getirilir. heap ağacı hale getirilmesi kısadır. büyük olan üstte ufak olan altında şeklinde dallandırılacaktır. fakat ağaç bir dizi yapısı olmadığından henüz elimizde sıralı bir dizi yoktur. bunu dizi hale getirmek gerekmektedir. heap ağacının en üstündeki en üst sayı olacağından, sonuc kümesine en büyük rakam olarak kaydedilir. daha sonra ağaçın en üstteki node'u silerek ağaç tekrar heapfy işlemine sokulur. bu sefer ağacın en üstündeki değer sonuç kümemizin ikinci en büyük sayısı olmuş olur. bu şekilde tüm ağaç sıfırlandığında sonuç kümemizde sıralanmış bir dizi olacaktır.
