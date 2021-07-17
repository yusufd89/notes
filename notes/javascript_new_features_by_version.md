############################

############################
# JAVASCRIPT NEW FEATURES BY VERSION
############################

############################

# ES2017 ile gelen bazı yenilikler

- #### async ve await keywordleri

"await" is verb type of "wait" word.

Promise (Ecmascript güncel sürümleri ile gelen nesne) dönen metodları "myMethod.than()" ile çağırmaktansa onları şu şekilde senkron çağırabiliyoruz:

var value = await myMethod();

artık yukarıdaki satır senkron işleyecektir. yukarıdaki satırı içeren metod her zaman async olmak zorunda. yani;

```js
async methodX() {
  ...
  var value = await myMethod();
  ...
  return anything;
}
```

ve artık herhangi bir yerden methodX çağrıldığında, methodX Promise dönecektir ve promise succes'i anything'dir. yani;

```js
methodX().then(  function(value){ 
                           console.log("value" + value); //prints anything
                        }
);
```

yukarıda eğer await metodu error verirse o satır exception throw eder.


- #### Object.values()

```js
const person = { name: 'Fred', age: 87 }
Object.values(person) // ['Fred', 87]
```

Array içinde aynı özellik geçerlidir.

- #### Object.values()

```js
const person = { name: 'Fred', age: 87 }
Object.entries(person) // [['name', 'Fred'], ['age', 87]]
```

Array içinde aynı özellik geçerlidir.

- #### Object.getOwnPropertyDescriptors()

setter işlemimizi ezmiş olalım:

```js
const person1 = {
    set name(newName) {
        console.log(newName)
    }
}
```

artık bu işimizi görmeyecektir:

```js
const person2 = {}
Object.assign(person2, person1)
```

fakat getOwnPropertyDescriptors metodu bize istediklerimizi döndürecektir.

```js
const person3 = {}
Object.defineProperties(person3, Object.getOwnPropertyDescriptors(person1))
```

# ES2016 ile gelen bazı yenilikler

- #### Exponentiation Operator

Math.pow(4, 2) == 4 ** 2

# ES2015 ile gelen bazı yenilikler

- #### Default Parameter Values

```js
function f (x, y = 7) { 

  return x + y;
}
```

- #### class yapıları (extend, constructor desteği ile)

- #### let operatörü (Block-Scoped Variables)

let a=5;

let for gibi döngülerin içerisinde tanımlandığında örnek:

for(let i=0; ...) ...

for dışından okunamaz olur. oysa "var" okunabiliyordu. Aynı durum if içinde geçerli. if içinde let tanımlaması if dışında geçersiz oluyor.

aynı zamanda let ile tanımlanan değerler, aşağıdaki satırlarda tekrar tanımlanamıyor. hata fırlatıyor. oysa var operatöründe aynı değer tekrar tanımlanabiliyordu.

- #### const keyword

Constants kelimesinden geliyor. java'daki final'a denk geliyor.

```js
const a = 2;
```

const'ta "let" ile aynı mantıkta block-scoped variable yaratıyor. yani if, while gibi blokların dışından okunamıyor.

- #### Template literals (or Template strings)

  ` karakteri ile yazılan string'lerde bir çok özellik mevcut. tüm özellikler burada: (source-id: 218) bunlardan bazıları:
  
  - multi-line strings

    ```js
    var myStr = `hello
    world`;
    ```

  - Expression interpolation

    ```js
    var myStr = `first element is: ${a} . but both element total are: ${a + b}`
    ```

- #### String format

```js
var soyad="Aykaç";

var fullName=`Merhaba ${soyad}`;
```

- ### Set liste türü

aynı elemanlar dublicate olmuyor. örnek:

```js
var items=new Set();
items.add(1);
```

- #### Iterators

- #### Maps

key/value tutan liste türü.

- #### WeakMap

Maps ile aynı. sadece enumerable diildir.

- #### is ve isnt operatörü

javadaki instanceOf operatörü ile aynı işi görüyor.

- #### Destructuring Assignment

aynı satırda çoklu değer atama işlemleri sağlanıyor. örnek:

var [a,b] = [9,3];

//eğer sağ tarafta fazladan eleman var ise, sadece sol tarafta istenmeyen eleman yerine boşluk atanabiliyor.

var list = [ 1, 2, 3 ]; 

var [ a, , b ] = list;

- #### sınırsız parametre

```js
function argsTester(...theArgs){

  alert(theArgs.length);
}
```

burada the args aynı tipte olan verileri tutmuyor. tüm objeleri bir dizide tutuyor.

- #### Expression Bodies

```js
odds  = evens.map(v => v + 1) 

pairs = evens.map(v => ({ even: v, odd: v + 1 })) 

nums  = evens.map((v, i) => v + i)
```

sırası ile aşağıdaki satırlara denk gelmektedir:

```js
odds  = evens.map(function (v) { return v + 1; });

pairs = evens.map(function (v) { return { even: v, odd: v + 1 }; });

nums  = evens.map(function (v, i) { return v + i; });
```

- #### parametre birleştirme

var params = [ "hello", true, 7 ]; 

var other = [ 1, 2, ...params ]; // [ 1, 2, "hello", true, 7 ]


- #### parantezsiz metod çağırma işlemi

ajax("google.com")

yerine artık:

ajax "google.com"

yazılabilir.

- #### direct support for octal and binary

```JS
0b111110111 // 503;

0o767 // 503;
```

- #### Property Shorthand

json değerleri sağ taraftaki ile aynı isme sahip ise atama yapmaya gerek kalmıyor.

```js
obj = { 

        x, 

        y };
```

eskiden:

```js
obj = { x: x, 

        y: y

      };
```

- #### module Value Export/Import

```js
//  lib/math.js 
export var pi = 3;

//  someApp.js
import # as math from "lib/math"; 
console.log(math.pi);

//  otherApp.js 
import { pi } from "lib/math"; 
console.log(pi);
```

- #### sınıf içindeki metodlara static operatörü geldi

- #### generators (yield keywordü)

- #### promise nesnesi geldi
