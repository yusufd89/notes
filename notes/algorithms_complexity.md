############################

############################
# ALGORITHMS COMPLEXITY
############################

############################

# Analysis of algorithms

## algoritma karmaşıklığı (or algorithm Complexity)
__time Complexity__ ve __space Complexity__ (bellek kullanımı) gibi faktörlerin değerlendirmeleridir.

- __O (or Büyük O or Big-Oh or Big-O or Big O)__

  __worst-case analysis (or En kötü durum analizi)__ için kullanılan notasyondur.

  en kötü durum için algoritmanın içinde if/else ile ayrılan kısımlarda en yavaş olan kısım seçilir.

- __Θ (or Big Theta)__

  __average-case analysis (or ortalama durum analizi)__ için kullanılan notasyondur.

  ortalama durum analizini yapmanın bir standardı yoktur. bu yüzdne biraz daha zordur. çünkü input olarak ne verileceğinin bir standardı yoktur. örneğin; bir dizi de sıralı arama yapılıyor ise, ortalama durum analizi yaparken dizinin orta elemenı verilir.

- __Ω (or big Omega)__

  __best-case analysis (or En iyi durum analizi)__ için kullanılan notasyondur.

- __küçük-omega (or little-omega or ω)__ ve __küçük-o (or little-o)__

  en iyi ve en kötü durumların kısmen tolere edilmiş analizleridir.

Not-1: big-O ve ve küçük-o'da bulunan O ve o simgeleri birbirirnin küçük ve büyük halleridir. Fakat bu O simgesi, ingizlice alfabesindeki O harfine denk değildir. Hafif italik olarak yazılan özel bir karakter/semböldür (akademide "Landau symbol" olarak geçer). kaynak: (source-id: 418) title: "More information".

Not-2: Hesaplamalar yapılırken, asimptotik üst sınır ve alt sınırlar kullanılır. (asimptot'lar başka başlıkta anlatılıyor)

## örnek notasyon gösterimi

f(x) = 6x^4 + 9x^4 + 80 = O(x^4) = Θ(x)

olarak ifade edilir. Bu gösterime göre; "O" bir fonksiyon değildir, sadece bir gösterimdir.

## büyüme oranları

1 < logn < n < n*logn < n^2 < 2^n < n!

| n      | (constant) 1 | (logarithmic) logn | (logarithmic) log_2 n | (linear) n | (logarithmic) N-log-n | (quadratic) n^2 | (cubic) n^3 | (exponential) 2^n |
|--------|--------------|--------------------|-----------------------|------------|-----------------------|-----------------|-------------|-------------------|
| 1      | 1            | 0                  | 0                     | 1          | 0                     | 1               | 1           | 2                 |
| 2      | 1            | 0.3                | 1                     | 2          | 0.6                   | 4               | 8           | 4                 |
| 3      | 1            | 0.4                | 1.5                   | 3          | 1.4                   | 9               | 27          | 8                 |
| 10     | 1            | 1                  | 3                     | 10         | 10                    | 100             | 1E+03       | 1024              |
| 100    | 1            | 2                  | 7                     | 100        | 200                   | 1E+04           | 1E+06       | 1E+30             |
| 1000   | 1            | 3                  | 10                    | 1E+03      | 3E+03                 | 1E+06           | 1E+09       | 1E+301            |
| 10000  | 1            | 4                  | 13                    | 1E+04      | 4E+04                 | 1E+08           | 1E+12       | too big!          |
| 100000 | 1            | 5                  | 17                    | 1E+05      | 5E+05                 | 1E+10           | 1E+15       | too big!          |
| 1E+6   | 1            | 6                  | 20                    | 1E+06      | 6E+06                 | 1E+12           | 1E+018      | too big!          |
| 1E+7   | 1            | 7                  | 23                    | 1E+07      | 7E+07                 | 1E+14           | 1E+021      | too big!          |
| 1E+8   | 1            | 8                  | 27                    | 1E+08      | 8E+08                 | 1E+016          | 1E+024      | too big!          |
| 1E+11  | 1            | 11                 | 37                    | 1E+11      | 1E+12                 | 1E+022          | 1E+033      | too big!          |
| 1E+25  | 1            | 25                 | 83                    | 1E+025     | 3E+26                 | 1E+050          | 1E+075      | too big!          |

# Space Complexity

- example:

O(n)

```java
int sum(int n) {
  if (n <= 0) {
    return 0;
  }
  return n + sum(n-1);
}
```

- example:

O(1)

```java
int pairSumSequence(int n) {
  int sum = 0j
  for (int i = 0j i < nj i++) {
    sum += pairSum(i, i + l)j
  }
  return sum;
}

int pairSum(int a, int b) {
  return a + b;
}
```

# kodun time complexity hesaplanması

```java

// O(1)
print(hello)

// O(n)
for ( i = 0; i < n; i++) {
    print(hello)
}

// O(n2)
for ( i = 0; i < n; i++) {
    for ( i = 0; i < n; i++) {
        print(hello)
    }
}

// O(logn)
// k en fazla kaç kere içeri girdiğimiz olsun
// 2^k > n (her iterasyonda i'nin değeri: 2⁰, 2¹,2²,…2^k)
for ( i = 0; i < n; i=i*2) {
    print(hello)
}
```

Yukarıdaki kodun toplamı:
> O(1) + O(n) + O(n2) + O(logn) = 1 + n + n2 + logn = O(n2 + logn) = O(logn)

Yukarıdaki notasyonda O'nun içindeki değerler, hesaplamamızdaki hassasiyete kalmıştır. Eğer hassas hespalama yapılacak ise, yada düşük seviyelerdeki n değerleri için çalışılacaksa, hassasiyeti arttırıp O(n + n2 + logn) de yazabilirdik.

O(n2) = 0(n3) eşitliği de doğrudur. Fakat üst limiti en düşük tutmak daha yakın değerler verecektir.

# logn nereden geliyor?
- binary search algortimasından yola çıkalım. 16 adetlik bir dizimiz olsun ve worst case'e yakalanalım.
- elemanı bulamadığımız her adımda diziyi ikiye bölüyoruz.
- en kötü durumda 4 kere diziyi bölmemiz yetecek.
- bu durumda 16'yı dört kere 4'e bölüyoruz: 16 * (1/2)^4 = 1
- şimdi bu denklemi n elemanlı dizi için genelleyelim: n * (1/2)^k = 1.
- bu denklemde k benim kaç kere döngüye gireceğimin sayısı. biz bu sayıyı arıyoruz. bu sebeple denklemi çözersek;

  > k = log_2 n (log 2 tabanında n)

- log_2 n asimptotu logn olduğundan binary search için karmaşıklık O(logn)'dir.

# kod hesaplamalarına farklı örnekler
farklı bir örnek:

```java
int n=100;
int i=1;
int j=1;

while(s<=n){
  i++;
  s=s+i;
  doSomething();
}
```

| Iteration | value of i | value of s=s+i |
|-----------|------------|----------------|
| 1         | 1          | 1+1            |
| 2         | 2          | 1+1+2          |
| 3         | 3          | 1+1+2+3        |
| 4         | 4          | 1+1+2+3+4      |
| .         | .          | .              |
| .         | .          | .              |
| k         | k          | 1+1+2+3+4+..+k |

"k" kaç kere içeri girdiğimizin değeri olsun. k'yı bilmiyoruz.

```
1+1+2+3+4+..+k > n --> bu durumda loop'ta çıkılacaktır. denklemin sol tarafını matematikteki en temel formül ile tekrar yazarsak:
k(k+1)/2 > n (Bu sıkça kullanılan matematik formülüdür)
k^2 + k > n
k'yı ignore ederiz çünkü k^2 yanında bir önemi neredeyse yok.
k^2 > n
k > √n
```

farklı bir örnek:

```java
int n=100;

for(int i=1; i*i<=n; i++){
  doSomething();
}
```

| Iteration | value of i |
|-----------|------------|
| 1         | 1          |
| 2         | 2          |
| 3         | 3          |
| 4         | 4          |
| .         | .          |
| .         | .          |
| k         | k          |

```
"k" döngüye kaç kez grdiğimiz olsun. biz bu sayıyı bilmek istiyoruz.
yuakrıdaki tablodan da görüldüğü gibi k=i'dir.
i*i > n olduğunda da döngünün sonlanacağını biliyoruz.
i > √n
i'nin max değeri (döngü sonundaki değeri) bize kaç kez döngüye girdiğimizi verecektir.
```

farklı bir örnek:

n'inci fibonacci'yi hesaplayan programı inceleyelim:

```java
fibonacci(int n){
  if(n<1){
    return 1;
  } else {
    return fibonacci(n-1) * fibonacci(n-2);
  }
}
```

Hız 2^n'dir. ağaç olarak çizdiğimizide her bir fibonaççi daha atladığımızda işlem sayısının 2'nin üssel değeri olarak arttığını görürüz. Ağaç benzeri farklı bir gösterim de buda olabilir:

```
F(6)                 f(6)                 <--  1=2^0
F(5)                f(5) f(4)             <--  2=2^1
F(4)            f(4) f(3)  f(3) f(2)      <--  4=2^2
F(3)                ****                  <--  8=2^3
F(2)              ********                <-- 16=2^4
F(1)          ****************            <-- 32=2^5
F(0)  ********************************    <-- 64=2^6
```

farklı bir örnek:

```java
f(int n){
  if(n<1){
    return 1;
  } else {
    return f(n-1) * f(n-1);
  }
}
```

```
F(6)                 f(6)                 <--  1=2^0
F(5)                f(5) f(5)             <--  2=2^1
F(4)            f(4) f(4)  f(4) f(4)      <--  4=2^2
F(3)                ****                  <--  8=2^3
F(2)              ********                <-- 16=2^4
F(1)          ****************            <-- 32=2^5
F(0)  ********************************    <-- 64=2^6
```

Hız 2^n'dir.

# ArrayList calculation of "insert" method - space and time complexity
ArrayList'in nasıl implemente edildiği çok önemli tabi. fakat optimum/genelde uygulanan implementasyonları düşünerek hesaplama yapalım.

ArrayList kendi içinde native array tutar. native array'ler bazı dillerde (c gibi) dinamik yönetilebilir (not: aslında c'de dinamik array yok, fakat pointer'lar ile bu yapılabilir). bazı dillerde (java gibi) ise dinamik array yoktur. bu yazıda dilin dinamik array destekleyemediğine göre complexity hesaplayacağız.

the insert method should add a new element to native-aray which is storing inside ArrayList. we had accept that the programming language does not support dynamic arrays. Therefore insert method must create a new clone array of existing array with currentArraySize+1 element. The clone element will be created with time and space O(n) complexity.

But most of ArrayList implementations double the capacity only when the array-size is power of 2. So, O(n) (explained above) is only occurs when the arrays-size is power of 2: 1, 2, 4, 8, 16... On the other cases nsert method takes O(1) both for space and time complexity.

- worst-case is O(n)
- best-case is O(1)

Now let's have a look to spesific point: What happens when we add n elements to ArrayList?

Until we came to X, we have should have passed those:

1 + 2 + 4 + ... + X = X + X/2 + X/4 ... 1 = roughly 2X

X insertions take O(2X) time and space complexity. But the __amortized time__ is O(1) because mostly O(1) will occur.

