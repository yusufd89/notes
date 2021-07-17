############################

############################
# JAVASCRIPT
############################

############################

# javascript promise
promise keywordü daha çok kullanılsada farklı kütüphaneler, yada programlama dilleri farklı isimlerde kullanmaktadır: Future, delay, deferred...

Javascript'te parametre olarak fonksiyon geçilebilmektedir. bu şekilde error, success gibi event'lerde o callabck'lerimiz çağrılmaktadırlar. fakat promise ile; parametre geçmek yerine, promise bize bir nesne (promise nesnesi) döner. biz bu promise nesnesinin success fail gibi metodlarına ilgili callback metodlarımızı ona yollarız. daha sonra promise metodumuzu run ederiz. aslında farklı yöntemlerle yapılabilecek bir iş. fakat promise yöntemi okunabilirliği arttırmaktadır, standart olmasını sağlamaktadır ve eğer dilin native Promise kütüphanesinden yararlanıyorsak, asenkron thread işlemi yapabilmemizi sağlamaktadır.

promise aslında programlama dilinden bağımsız bir best practice'dir.

ecmascript 6 ile Promise nesnesi native olarak gelmiştir. daha önceki ecmascript sürümlerinde Promise 3üncü parti kütüphanelerle yapılmaktaydı. güncel ecmascript promise kullanımı şu şekildedir:

```js
const myPromise = new Promise((resolve, reject) => {

  // this function here called "executor".

  // do any asyncron operation here:
  setTimeout(() => {
    resolve('foo');
  }, 300);

  // if we will call "resolve" here those will be ignored.
  // "resolve" method works only once. 
});

myPromise
  .then(handleResolvedA, handleRejectedA)
  .then(handleResolvedB, handleRejectedB)
  .then(handleResolvedC, handleRejectedC)
  .finally(finallyHandler);

// if we have only 1 reject-handler:
myPromise
  .then(handleResolvedA)
  .then(handleResolvedB)
  .then(handleResolvedC)
  .catch(handleRejectedAny)
  .finally(finallyHandler);
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# "use strict"
bu satır ile javascript dilinin derlenmesi daha detaylı ve daha temiz olmasını sağlar. bazı örnekler:

- "var" olamadan global değerler yaratılmasını engeller.

- throws exception on Assignment to a non-writable global:

```js
var undefined = 5; // throws a TypeError
var Infinity = 5; // throws a TypeError
```

"use strict" olmasaydı yukarıdkai satırlar hata fırlatmayacak fakat variable simleri özel oldukları için bu isimde variable da oluşmayacaktı.

- throws exception on Assignment to a non-writable propertyç
```js
var obj1 = {};
Object.defineProperty(obj1, 'x', { value: 42, writable: false });
obj1.x = 9; // throws a TypeError
```

- throws exception on Assignment to a getter-only property
```js
var obj2 = { get x() { return 17; } };
obj2.x = 5; // throws a TypeError
```

"use strict" satırı bir metodun içine yazılırsa sadece metod için geçerli olmaktadır. eğer globale yazılırsa tüm sistemi etkiler.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# variable defining sytax

```js
var var1 = "hello", var2, var3 = 99;
```

equals:

```js
var var1 = "hello";
var var2;
var var3 = 99;
```

# multi equal character on same line

```js
var a = b = c;
a = b = c;
z = a = b = c;
```

Yukarıdaki örnekte sırası ile: "b = c", "a = b" çalıştırılıyor. en sondaki örnekte ek olarak; en sonda "z = a" çalıştırılıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Web Hypertext Application Technology Working Group (or WHATWG)
https://github.com/whatwg reposunda geliştirilen web standartlarını dökümante edilen bir web projesi geliştiren topluluktur. __World Wide Web Consortium (or W3C)__'ten farklı bir topluluktır fakat birlikte çalışmaları vardır. Yayınladıkları eski dökümanlarda ufak farklılıklara rastlayabiliriz. Fakat daha sonrasında bu farklılıklar kapatıldı.

# fetch

Web tarayıcılarında uzun zamandır detskelenen yeni API. Promise tarzı çalışması en büyük avantajıdır. örnek kullanım:

```js
fetch('send-ajax-data.php')

    .then(data => console.log(data))

    .catch(error => console.log('Error:' + error));
```

ES7 async/await example:

```js
async function doAjax() {
    try {
        const res = await fetch('send-ajax-data.php');
        const data = await res.text();
        console.log(data);
    } catch (error) {
        console.log('Error:' + error);
    }
}

doAjax();
```

Fect API spesifikasyonu burada: (source-id: 303)

Eski tarayıcılar için core Javascript polyfill kütüphanesi: https://github.com/github/fetch (whatwg-fetch isimli npm paketi). Fetch polyfill kendi içinde var XMLHttpRequest()'i wrap eder. Kaynak: (source-id: 304)

Fetch, jQuery.ajax()’den bazı farklılıklar var. bu linkte farklılıklar yazmaktadır: (source-id: 305)

example codes for fetch:

```js
var metaDatas = {
    method: 'post',
    headers: {
      "Content-type": "application/x-www-form-urlencoded; charset=UTF-8"
    },
    body: 'foo=bar&lorem=ipsum'
  };

fetch('./api/some.json', metaDatas)
  .then(
    function(response) {
      if (response.status !== 200) {
        console.log('Looks like there was a problem. Status Code: ' + response.status);
        return;
      }

      // read some headers:
      console.log(response.headers.get('Content-Type'));
      console.log(response.headers.get('Date'));

      // read some metadata:
      console.log(response.status);
      console.log(response.statusText);
      console.log(response.type);
      console.log(response.url);

      // json() is a stream.
      // response.status, headers are coming first from the TCP connection. they are ready inside this function, otherwise fetch will call "catch".
      // but the payload is coming after header and status. payload can be very long. so we call it with stream. 
      // kaynak: (source-id: 306) sayfanın sonundaki android emülatörlü animasyonda 8 saniyelik download'un nasıl stream edildiği gösteriliyor.
      response.json().then(function(data) {
        console.log(data);
      });
    }
  )
  .catch(function(err) {
    console.log('Fetch Error ' + err);
  });
```

another example:

```js
// instead of response.json() we can call the reader (which is a stream-reader)
const reader = response.body.getReader();

// infinite loop while the body is downloading
while(true) {
  // done is true for the last chunk
  // value is Uint8Array of the chunk bytes
  const {done, value} = await reader.read();

  if (done) {
    break;
  }

  console.log(`Received ${value.length} bytes`)
}
```

another example:

```js
function status(response) {
  if (response.status >= 200 && response.status < 300) {
    return Promise.resolve(response)
  } else {
    return Promise.reject(new Error(response.statusText))
  }
}

function json(response) {
  return response.json()
}

fetch('users.json')
  .then(status) // yukarıdaki status metodu oto çağrılıyor ve response parametresi oto geçiliyor
  .then(json) // yukarıdaki status metodu oto çağrılıyor ve response parametresi oto geçiliyor

  // burada istediğimiz kadar then kullanabiliriz. her then metodunda return ettiğimiz her obje, diğer then'e parametre olarak geçecektir.

  .then(function(data) {
    console.log('Request succeeded with JSON response', data);
  }).catch(function(error) {
    console.log('Request failed', error);
  });
```

# Axios
- browser'da XMLHttpRequest'i wrap eden, nodejs'te "http" objesi ((source-id: 307) ) ile çalışan açık kaynaklı javascript http client. kaynak: (source-id: 308) "Features" başlığı 1 ve 2inci madde.
- fetch-api ile yapılacak birçok şeyi daha kolay şekilde yapabilmemizi sağlıyor.
- fetch-api'ye göre yapılamayan bazı özellikleri de var (örnek upload'da progress'ler adım adım takip edilemiyor).

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# immutable.js

```js
const { Map } = require('immutable')

const map1 = Map({ a: 1, b: 2, c: 3 })

const map2 = map1.set('b', 50)

map1.get('b') + " vs. " + map2.get('b') // 2 vs. 50
```

Yukarıdaki Map sınıfı, js'in default bir sınıfı diil. tamamen immutable'a özel bir sınıftır. yani aşağıdaki gibi bir obje diildir:

```js
var myArr = { a: 1, b: 2, c: 3 };
```

# immer.js

```js
import produce from "immer"

const baseState = [
    {
        todo: "Learn typescript",
        done: true
    },
    {
        todo: "Try immer",
        done: false
    }
]

const nextState = produce(baseState, draftState => {
    draftState.push({todo: "Tweet about it"})
    draftState[1].done = true
})
```

at the end baseState will be untouched. dikkat edilirse; immutable.js'teki gibi native olmayan JS class'ı kullanılmamış. sadece draftState native olmayan bir JS class'ıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# vanilla-js
vanilla js bir kütüphane/framework'tür. fakat içi boş(kod olmayan) bir js projesidir: (source-id: 309) . Bu proje, herkesin çok fazla gereksiz js kütüphanesi kullanmasına tepki olarak oluşturulmuştur.

vanilla-js, saf js kodu ile yazılmış projelere takma isim olarak kullanılmaktadır.

"vanilla" teriminin sık kullanılması ile birlikte artık herkes her framework/uygulamaya "vanilla" takma ismini prefix olarak koymaktadır. o uygulamayı yada framework'ü eklenti olmadan/saf hali ile kullandığını belirtmek için kullanılır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Polyfill
bu terimin türkçesi yoktur.

sadece web development'ında kullanılan bir terimdir. eğer bir kod parçası, web tarayıcının desteklemediği bir özelliği çalıştırabilmemizi sağlıyorsa, o kod parçasına Polyfill denir.

# Shim
tüm programlama dünyasında kullanılan bir terimdir. eğer bir kod parçası, bizim yazdığımız API metodunun önünü intercept edip başka bir metoda yönlendiriyorsa, o kod parçasına shim denir. shim'ler genelde geriye uyumluluk için kullanılırlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# cross-env
https://www.npmjs.com/package/cross-env sitesinde dağıtılan node modülüdür. bu modül ile npm scriptlerinde çağrılan komutlara environment variable'ları geçebilmemizi sağlamaktadır. bu özellik normalde de npm tarafından desteklenir, fakat cross-env, bunu OS'tan bağımsız bir syntax ile yapabilmemizi sağlar.

örnek usage:

```json
// package.json file
{
  "scripts": {
    "build": "cross-env NODE_ENV=production webpack --config build/webpack.config.js"
  }
}
```

cross-env isimli node modül 2 adet komut export eder: cross-env ve cross-env-shell. cross-env komuta parametre geçilen komut variable'ı okuyabilir. fakat ikinci komut bu variable'ı okuyamaz. iki veya daha fazla komut üstüste çağrılacak ise cross-env-shell kullanılması şarttır. cross-env-shell için örnek:

```json
{
  "scripts": {
    "greet": "cross-env-shell XXX=111 YYY=222 \"echo $XXX && echo $YYY\""
  }
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# flow
flow.org sitesinde dağıtılan js için type desteği getiren bir typechecker'dır.

örnek JS kodu:

```js
let num: number = 1 + 2;

//fonksiyon örneği:
function square(n: number): number {
  return n * n;
}

square("2"); // hem derleyici hata verir, hemde IDE olan flow eklentimiz (or lint içindeki flow eklentimiz) hata verir.

// sol tarafta bir nesneye referansı atanmadan yazılan örnekler:
(1234: number);
("hi": string);
(true: boolean);
([1, 2]: Array<number>);
({ prop: "value" }: Object);
(function method() {}: Function);

```

Flow tipleri JS syntax'ında yoktur. bu sebeple derleyicimizde de ayar yapmamız gerekecektir.

- configs:
  - JS dosyanın flow'a göre algılanması için "// @flow" satırının, JS dosyanın bir yerinde olması gerekmektedir.
  - projenin root'unda .flowconfig dosyası olmalıdır. bu dosya için ignore/include edilecek dizinler gibi ayarlar bulunuyor

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# javascript performans avantajı nereden kaynaklı?

javascript tek thread çalışır. thread içerisinde çağrılan paralel gibi görünen threadler'in (setTimeout, ajax gibi) callback'leri aslında asıl thread bittikten sonra çalıştırılır. örneğin ajax işlemine callback parametresi geçtik. ajax işlemi browser'a verilir ve asıl thread bitmeden javascript o callback'i ajax sonuc dönmüşse dahi çalıştırmaz.

ecmascript thread mekanizmasında zorunlu standartlar getirmemiştir. dolayısı ile ecmascript'in javascript harici diğer implementasyonları tek thread olmak zorunda değildir.

thread kavramı process thread'i olarak algılanmamalıdır. javascript motoru multi-thread'dir. javascript'in çağırdığı ajax işlemi multithread olabilir. fakat javascript'in kod seviyesinde tek thread olarak işletilir.

# Event loop
JavaScript'in concurrency model'i __event loop__'a dayanır. Tüm işlemler (event'ler) bir queue'da bekletilir. Hepsi sıra ile tek thread'de execute edilir. Bu mekanizmaya __event loop__ denir.

# sunucudaki performans üstünlüğü

javascript tek thread olmasına rağmen daha hızlı çalışır. servletlere istek gelir. servlete gelen istek databaseye gider. database'den işlemin dönüş yapması 5 saniye olsun. bu 5 saniye boyunca 1 thread beklemede durmaktadır (blocking-IO). java'da database işlemini thread yapsak ve asagidaki gibi olsa main thread devam eder ve databse işlemi threadde çalışır.


```java
//class definition on server side
class ThreadX extends Thread {

     run(){
           aLongDatabaseOperation();
           System.out.println("3");
     }
}


//servlet code start

System.out.println("1");
t = new ThreadX();
t.run();
System.out.println("2");

//servlet end
```

yukarıdaki kod bloğunda hala javascript daha hızlı olacaktır. günümüzde 1 cpu max 8 cpu'lu olabiliyor. bu durumda; thread'in database işelmini beklemesi demek, cpu'yu da boşuna bekletmesi demek. aynı zamanda thread memory'si demektir. CPU aynı anda birçok işlem yapabilseydi javascript bu kadar performanslı olmayacaktı. js yukarıdaki gibi bir işlemde main thread'i bitiriyor. yani ekrana 1 ve 2 print ediliyor. eğer veritabanı işlemi bitmiş ise; js hemen ekrana 3 basıyor. fakat database işlemi bitmemişse; servlete gelen diğer isteklere cevap vermeye devam ediyor.

# performans comparison: single-thread non-blocking I/O vs multithread blocking-IO

yukarıdaki servlet örneği alsında bu karşılaştırmanın bir spesifik örneği oldu. sistemden sisteme bu kaşrılaştırmanın olumlu ve olumsuz yanları olabilir. fakat servlet'lerde sunucuya 1000 istek geldi diyelim. 10000 thread açılacak java'da. oysa javascriptte 1 thread olacak. javascript motoru tabi arkaplnada çok thread açıyor. fakat açılan thread'ler hiç blocklanmadıkları için hemen kapanıyorlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# moment.js

tarih/saat işlemlerini kolaylaştıran javascript kütüphanesi. bazı özellikler:

- tarihi formatlayıp gösterme
- bir tarihi verip şu andan ne kadar eski olduğunu gösterme
- toplama çıkarma 

# moment-timezone.js

- timezone bilgilerini içeren moment eklentisi. bir datetime bilgisi, istenilen timezone'a çevrilebilmesi sağlanıyor.

- moment-timezone ile convert işlemi yapabilmek için bağımlılıklarımız şunlardır:

  - moment.js: core kütüphane

  - moment-timezone.js: timezonu çevirme api'si için

  - moment-timezone-with-data.js: convert işlemini yapan js içerisinde her ülkenin timezone bilgisi kodları ve saatleri ile birlikte yok. o yüzden bu dosyaya da ihtiyacımız var. dosyanın isminden de anlaşıldığı gibi bu dosyanın içinde zaten moment-timezone.js vardır. her ülkenin yıllara göre timezone'u değişmektedir. bu sebeple bu data yıllara göre tutulmaktadır. bu sebeple kütüphanenin dosya büyüklüğü artmaktadır. Buna çözüm olarak farklı paketler sunulmaktadır:

    - moment-timezone-with-data-2012-2022.js

      son 10 yılın datası ile gelen paket.

    - moment-timezone-with-data-1970-2030.js

      1970 ile 2030 arasındaki data'lar ile gelen paket.

    - moment-timezone-with-data.js

      tüm yılları içeren paket.

    Moment-js-with-data bu data'ları buradan topluyor ve kütüphanenin içine gömüyor: (source-id: 310) kaynak: (source-id: 311) "mj1856" commented on Jul 27, 2016. 1inci paragraf.

# other JS date/time libraries
momentjs projesi ek geliştirmler yapılmayacak statüye geçmiştir. kendi resmi sitesinde diğer önerilerle ilgili güzel bir yazı var: (source-id: 312) title: "Recommendations".

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# numeral.js

sayısal işlemleri kolaylaştıran javascript kütüphanesi. bazı özellikler:

- istenilen formatta para bimiri, byte birimi formatlayarak gösterebilme

- 1inci, 2inci gibi çıktıları verebilme

- üs sayılarını formatlayabilme 1e+2 gibi

- basit matematik işlemleri yapabilme

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# nodejs

## express

nodejs için sunucu yazılmasını kolaylaştıran framework'tür, npm modülüdür. özellikle rest controller işini yapması ile ön plana çıkar.

## REPL

Read Eval Print Loop işlevini gören nodejs içinde gelen komut satırı uygulamasıdır. sadece "node" komutu komut satırına yazıldığında komut satırı yeni bir satıra geçer ve son kullanıcıdan javascrpt girişi bekler. buraya yazılan javascript'ler o anda işletilir. 

REPL genel bir karamdır. Örneğin Java 9 ile de REPL gelmiştir.

# yarn vs bower
npm'e alternatif nodejs için paket yöneticisileri.

# Gulp vs Grunt
nodejs modülleridir. bunlar sayesinde projemizde minify, auto-watch and auto-deploy gibi işlemlerimizi tasklar tanımlayarak yapabiliyoruz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# how to use common static string variables

javascript kütüphanelerinin soruce code'una bakıldığında stringler hardcode girilmiş olarak görülebilir. bunun sebebi minify edilirken, yada minify edilmeden prod ortamına hazırlanırken, kodun daha hızlı çalışabilmesi için stringlerin gömülmesidir. 

örneğin; momentjs'te

> moment().add(1, 'month');

buraya gönderilen stringlerin common bir yerde tutulması tavsiye edilir.

momentjs geliştirme ortamında bu code'lar hardcode değildir. prod'a paketlenirken hardcode girilir.

yani; CommonStrings diye bir sınıf isteyerek yaratılmıyor. çünkü momentjs'te moment().add(1, CommonStrings.MONTH); kodu yerine momentjs'te moment().add(1, "month"); daha hızlı çalışmaktadır. dev ortamında CommonStrings varken canlı javascript kodlarında CommonStrings kullanılmamaktadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# javascript core ile obje klonlama

Ecmascript güncel versiyonları ile gelen aşağıdaki ile yapılabilir:

```js
var newObject = { ...oldObject, {} };
```

Syntax yazılımcılar arasında "object spread" deniliyor. (spread kelime anlamı: yayılmış). 3 noktaya (...) "spread operatörü" denir.

Yukarıda oldObject array veya obje olabilir. her türlü js otomatik iterate ediyor.

Aşağıdaki işlem sperad operatörü ile yapılan işlem ile aynı işi yapmaktadır:

```js
var newObject = Object.assign(oldObject);
```

assign metodu sonsuz parametre alıyor. tüm parametreleri tek objede topluyor. 

Tek farkı şudur: Object.assign setter(newValue) kullanarak yeni objeye değerleri atıyor. yani setter metodu tetikleniyor. fakat spread direk nesneyi property atayarak oluşturuyor.

# Jquery ile obje klonlama

- Shallow copy

Shallow türkçe kelime anlamı: yüzeysel

```js
var newObject = jQuery.extend({}, oldObject);
```

shallow copy yeni obje yaratıyor. eski objenin en üstteki property'lerini geziyor. bu property'leri literal tipte ise; variablelelerini kopyalıyor. eğer property'ler obje ise referansları ile kopyalıyor. alt elementlere girmiyor.

- Deep copy

```js
var newObject = jQuery.extend(true, {}, oldObject);
```

Deep copy'de tüm alt elementler dahi geziliyor ve tüm değerler variable olarak yeni objeye kopyalanıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# rest operator
burada kullanılan "..." (üç nokta) rest operatörü olarak adlandırılır. fonksiyonlara sınırsız parametre yollanabilmesini sağlar.

```js
function f(x, y, ...arr1) {
  
  // arr1 is simple javascript array.
}

// calling above method
f("a", "b", 1, 2, 3, 4);
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# watchman
facebook'un geliştirdiği bir yazılım. bir dosya dizini veriliyor, bu dosya dizinlerini sürekli takip ediyor eğer bir değişiklik olursa, önceden belirlenen komutları tetikliyor.

executable dosyası, ek olarak fb-watchman ismi ile nodejs paketi olarak dağıtılıyor. böylece javascipt api'si ile de kullanılabiliyor.

genelde web uygulamarında developement yaparken bu uygulamadan çok yararlanılıyor. live-reloading işlemi yapılması sağlanıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# modernizr
bu js libary'si ile hangi teknolojilerin tarayıcıda varolup olmadığı kontrol edilebiliyor. asagidaki örnekteki gibi tüm teknolojiler tek bir variable'da kontrol edilebiliyor. örnek:

```js
if(modernizr.cookies){

  //cookies enabled
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Javascript scope
The "global" scope is the outermost scope. It is accessible from any inner/local scope. global scope on web browser is accesible via "window" object. on other javascript engines can be different.

```js
this.window === window.window // true
this === window // true
```


fonksiyonların kendi scope'u vardır. new olmazsa yukarıdakinin "this"'i ile fonksiyon içindeki this eşit olur. fakat aynı this'i kullandıkları aynı scope'ta oldukları anlamına gelmiyor. aşağıdaki örnek bu durumu açıklıyor:

```js
// function tanımlama. burada execute edilmiyor.
function run() {
  // "run" function scope
  var message = 'hello';
  console.log(message);
  console.log(this === window);
}

run(); // burada execute ediliyor.
// prints:
// "hello"
// true

console.log(message); // throws ReferenceError

new run(); // burada execute ediliyor.
// prints:
// "hello"
// false
```

__lexical scoping (or static scoping)__ closure konusunda anlatılmıştır.

# closure (or lexical closure or function closure)

closure türkçe kelime anlamı: kapatma

```js
var add = function () { // function-1

    var counterVAR = 5;
    counter = 5;
    this.counterTHIS = 5;
    let counterLET = 5;
    const counterCONST = 5;

    return function () { // function-2
        counterVAR += 1;
        counter += 1;
        counterTHIS += 1;
        counterLET += 1;
        // const variables can not be changed! they are read-only.
        // (that rule is not about "scopes".)
        // counterCONST += 1;

        console.log("INNER- counterVAR: " + counterVAR);
        console.log("INNER- counter: " + counter);
        console.log("INNER- counterTHIS: " + counterTHIS);
        console.log("INNER- counterLET: " + counterLET);
        console.log("INNER- counterCONST: " + counterCONST);
    }
};

console.log(typeof add); // function (which is "function-1")

var addFunc = add();

console.log(typeof addFunc); // function (which is "function-2")

addFunc();
addFunc();
// new addFunc(); --> ile çalıştırılacak fonksiyonun scope'unu değiştiriyoruz, ama function-2 scope'unda kullanılan bir variable yok. o yüzden aşağıdaki sonuçlar değişmeyecekti.

console.log(typeof addFunc()); // undefined. because function-2 does not have areturn value.

// counterVAR is undefined on this scope
// var addFunc = new add(); --> yapsaydık yine de aynı şekilde olacaktı.
try {
console.log("counterVAR:" + counterVAR); // throws undefined exception
} catch(e) { console.log("counterVAR is undefined"); }

// counter, en üst seviye "this" olan "window" objesinin scope'undadır.
// var addFunc = new add(); --> yapsaydık yine de aynı şekilde olacaktı.
console.log("counter:" + counter); // prints 8

// counterTHIS add function'umuzu "window" scope'unda run ettiğimiz için "counter" ile aynı seviyede tanımlanmıştır.
// var addFunc = new add(); --> yapsaydık, zaten addFunc() hata verecekti.
// Bu kısım özellikle önemli!
// new operatörü kullanmazsak this=window oluyor.
// new operatörü kullanırsak this=windows olmuyor. yeni bir "this" oluyor. fakat bu durumda inner scope'lar buraya erişemiyor.
console.log("counterTHIS:" + counterTHIS); // prints 8

// counterLET is undefined on this scope
// var addFunc = new add(); --> yapsaydık yine de aynı şekilde olacaktı.
try {
console.log("counterLET:" + counterLET); // throws undefined exception
} catch(e) { console.log("counterLET is undefined"); }
```

closure ile API'lerin private metodlar ve değerler içerebilmesi sağlanmaktadır.

resmi olarak closure'un ne olduğu net diil. bazıları: return edilen metod'un önceki metoddaki variable'lara hala erişebilme tekniğine "Closure" denirken, bazıları ise return edilen fonksiyona closure adını veriyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Javascript language

# null vs undefined
farklıdır. undefined hiç değer almamış anlamına gelir. örneğin;

```js
var a1;

var a2 = null;

typeof a1; //prints undefined

typeof a9; //prints undefined. a9 is not even typed before.

typeof a2; //prints null;
```

# data types
- javascriptte number, boolean ve string birer primitive type'tır.

- fonksiyonlar (aşağıda detaylı anlatım var), typeof operatörü ile bakıldığında "fonksiyon" döndürürler. bu tipte olmalarının sebebi daha hiç new instance'ı ile oluşturulmamış olmasıdır.

- diğer data tiplerinin tümü (null dahil) objedir. array'ler objeden türemiş birer objedir. dolayısı ile objedir.

# Accessing Object Properties
- objectName.propertyName

- objectName["propertyName"]

# global vs local variable
local değerler metodların sadece içinden erişilebilir. oysa global değerler türm program tarafından erişilebilir. bir metod içerisinde "var" ile variable tabımlaması yapılmadan bir dataya değer atanırsa; o değer otomatik olarak global olarak tanımlanır. fakat böyle bir şeyin yapılması kesinlikle tavsiye edilmez.

# === vs ==
- == karşışaltırılan değerlerin eşit olup olmadığına (valueOf() metodu ile) bakarken, === ek olarak tiplerinde eşit olup olmadığına bakar.

- zorunlu kalmadıkça == kontrolü yapmamak gerekli. mantığı biliyor olsakta, başkasının okumasını zorlaştırıyoruz.

- === kontrolü daha doğal ve basit. javascript bilgisi dahi gerektirmiyor. tek istisna NaN'da oluyor. NaN === NaN -> false dönüyor.

- == için kurallar sırasıyla işletilmelidir:

  1- aynı tiptelerse === karşılaştırması yapılıyor. farklı tipler için aşağıdaki kurallar geçerlidir:

  2- null ve undefined eşittir

  3- sayı ve string karşılaştırılınca string önce sayıya çevrilir. js içinde Number(string) metodu mevcut.

  4- en az bir operand boolean ise; true->1, false->0'ya çevirir ve tüm kuralları tekrar işletir.

  5- obje karşısında string yada number varsa, obje.valueOF çağrılır ve kuraller tekrar işletilir.

  6- diğer tüm durumlar false döner

# NaN
__Not-A-Number__ anlamına gelmektedir. isNaN gibi metodlar bazen beklenmedik sonuçlar verebilir. örneğin " " değeri 0 a eşit sayıldığından isNaN false döner.

NaN bilgisayar bilimlerinde bir sayıdır. örneğin 0/0 tanımlanamaz ve bu sebeple NaN döndürmelidir. bu sebeple javascriptte typeof ile bakarsak; NaN, "number" tipindedir. 

JS beklenmedik sonuçlar dönebilmektedir. birçok alışılmadık durumları buradan inceleyebiliriz: jsfuck.com 

# debugger; keyword
bu keywordü içeren satırlar debug modda olan IDE tarafından durdurulurlar.

# Regular expressions
objeden türemişlerdir. javascriptte özel syntaxı vardır. tırnak içerisine almaya gerek yoktur.

# object (or nesne or tr:obje) vs instance
instance kelime anlamı: 1. örnek 2. hal/durum

"class", programlama dillerinde "nesne" tanımlayabilmek için gerekli bir tiptir. "User" eğer class tipindeyse nesnedir. User bir interface'de olabilirdi.

Instance ise bellekte ayrı yeri olan klon nesnedir.

bu başlıkta ve bu notlarda, obje ve nesne terimlerini kullanırken doğru olmasına hiç dikkat edilmedi. ikiside birbiri yerine kullanılmıştır.

# javascript function vs javascript class
javascript'te class yoktur (javascript'te class ecmascript 6 ile geldi). JS, sınıf olmamasına rağmen nesne tabanlı bir dildir. "nesne" yerine "prototip" kavramı vardır.

asagidaki person fonksiyonu bize objeyi döndürmek için kullanılan fonksiyondur. nesne döndürdüğü için constructor da denir. (hatta nesne döndürdüğü için class'ta denir fakat bu doğru diildir).

```js
function person(first) {

    this.firstName = first;

    this.lastName = null;

    this.changeLastName = function (name) {

        this.lastName = name;
    };
}

var myFather = new person("John"); // (inside "person" function) "this" (scope) is a new scope. 
print(myFather.firstName);
print(typeof myFather); // object

var myMother = person("Esra"); // (inside "person" function) "this" (scope) is the current "window" object.
print(myMother); //prints undefined. If we had "return "ahmet" on last line of person function, myMother would be "ahmet".
print(window.firstName);//prints Esra.
```

ecmascript'in güncel standartlarında class'lar vardır. fakat geriye uyumluluk adına herkes tarafından kullanılması tercih edilmeyebiliyor. örnek:

```js
class User {
  constructor(name) { this.name = name; }
  sayHi() { alert(this.name); }
}

alert(typeof User); // function (yeni sürüm js'teki "class" olmasına rağmen)
```

Yeni sürüm JS class'ları ile, eski sürüm JS function'ları tamamiyle aynı şeylerdir. 'Class' yapısı arkaplanda aynı işlevi bizim için yerine getirmektedir, yani syntactical sugar'dır. kaynak: (source-id: 313) title: "Defining a class", writes: "JavaScript classes, introduced in ECMAScript 2015, are primarily syntactical sugar over JavaScript's existing prototype-based inheritance. The class syntax does not introduce a new object-oriented inheritance model to JavaScript.".

Eski tip Function'larda extend işlemi yapılamaz. Function'un türettiği objede extend yapılabilir ("javascript object" başlığında anlatılıyor). Oysa yeni JS'teki class'larda extend işlemi java'daki syntax gibi yapılır.

# javascript object

Asagidaki (nesne2) tanımlama ile fonksiyonsuz bir şekilde obje türetmiş oluyoruz.

```js
var nesne2 = {

    Ad: 'Melih',

    Soyad: 'Orhan',

    AdSoyad: function () {

        return this.Ad + ' ' + this.Soyad
    }
}
```

Aşağıdaki şekilde inheritance yapabiliriz:

```js
// 2'inci parametrede descriptor'lar yollanıyor (başka başlıkta anlatılıyor).

var obj1 = Object.create(nesne2, { 
     
    prop1: {
      writable: true,
      configurable: true,
      value: 'value1'
    },
    
    prop2: {
      writable: true,
      configurable: true,
      value: 'value2'
    },
    
});
```

Yukarıda nesne2 yerine "Object.prototype" yazarsak boş objeden türetmiş oluruz.

# descriptor
her property'nin descriptor'ları vardır. bir obje içine bir property eklediğimizde js'in aşağıdaki metodunu kullanabiliriz. bu metod üzerinden gidersek descriptor'ları daha iyi anlayabiliriz.

```js
Object.defineProperty(obj, prop, descriptor)
```

örnek:

```js
Object.defineProperty(myObject, 'myInteger', {
  value: 99, //myInteger'nin değeri
  writable: true, // myInteger = 1; ile değiştirilip değiştirilemeyeceği
  enumerable: true, // for-loop ile dönüldüğünde bu değerin de döngüye girip girmeyeceği
  configurable: true, // property'nin silinip silinmeyeceği veya tipinin değiştirilip değiştirilmeyeceği
  get: function() { return val; },
  set: function(newValue) { val = newValue; }
});
```

Artık myObject.myInteger bize 99 u verecektir.

Dikkat edilirse defineProperty'nin aldığı tüm json elementine "descriptor" deniliyor. yani her biri birer descriptor değil. (bazen karışıkığa sebep olabiliyor. o yüzden bu cümleyi not aldım).

ES2017 ile getOwnPropertyDescriptors metodu gelmiştir (başka yerde anlatılıyor).

# own-property
bir nesnenin süper variable'ları bu kümeye dahil değildir. __hasOwnProperty("propertyToCheck")__ ile sorgulayabiliriz.

# fonksiyon ve obje içinde gelen property ve metodlar

#### fonksiyon properties:

- __length__

  fonksiyon kaç parametreli olduğunu tutar.

  ```js
  function func2(a, b) {}
  console.log(func2.length);
  // output: 2
  ```

- __arguments__

  (deprecated or not standart) fonksiyon çağrılınca ona yollanan argümanlar dizi olarak tutulur. bu argümanlar bu property'de tutulur.

- __arity__

  (deprecated or not standart) length ile aynı görevi görür. fakat length standartlarda oldugundan length kullanılmalıdır.

- __caller__

  (deprecated or not standart) fonksiyon o anda çağıran fonksiyon referansı.

- __display name__

  (deprecated or not standart) default olarak metodun kendi ismidir, fakat developer bunu istediği gibi ezebilir.

- __name__

  fonksiyon adının string halini tutar.

- __prototype__

  tipi json objesidir. array değildir. js objesi olduğundan saf js syntax'ında olduğu gibi buraya bir çok değer atayabiliriz:

  > myFunction.prototype.newProp = 99;
  
  prototype objesi, ilgili fonksiyondan üretilecek veya daha önceden üretilmiş her instance'a "__\_\_proto\_\___" property'si referans geçilir. bu sebeple buraya atadığımız her değer diğer eski ve yeni yaratılacak her instance'ın \_\_proto\_\_'sunda vardır.
  
  Aynı zamanda önceden veya sonradan oluşturulan instance'lara prop olarak kopyalanır. örnek:

  ```js
  myFunction.prototype.newProp = 99;

  instanceOfFunc.newProp; // 99

  instanceOfFunc.__proto__.newProp; // 99 

  instanceOfFunc.prototype; // objelerin prototype2ı olmaz. sadece function'ların prototype'ı vardır.
  ```

  prototype ile yeni prop eklemek çok kolaydır. fakat varolan prop'u güncellemek daha karmaşıktır. zira instance'ı üretmek için kullanılan constructor, zaten prop'u override edecektir. Bu durumu aşağıdaki önekten anlayabiliriz:

  ```js
  let f = function () {
    this.a = 1;
    this.b = 2;
  }
  let o = new f();

  f.prototype.b = 3;
  f.prototype.c = 4;
  // do not set the prototype f.prototype = {b:3,c:4}; this will break the prototype chain. because prototype has also super prototype.

  // o.__proto__ ---> has properties b and c
  // o.__proto__.__proto__ --> is Object.prototype
  // o.__proto__.__proto__.__proto__ --> is null.

  console.log(o.b); // 2
  // Is there a 'b' own property on o? Yes, and its value is 2.
  // The prototype also has a 'b' property, but it's not visited.
  // This is called Property Shadowing.
  ```

#### fonksiyon metods:

- __call(thisArg, arg1, arg2 ...)__

  ilgili fonksiyonu execute eder. args ile execute ederken göndereceğimiz parametreleri bir dizide göndeririz. thisArgs ise, fonksiyonun içindeki "this" scope'unu ezmek için kullanırız.

- __apply(thisArg, args)__

  "call" ile aynı görevi görür. sadece parametre alışı farklıdır. args bir dizi olmak zorundadır.

- __bind(thisArg, arg1, arg2 ...)__

  "call" ile aynı görevi görür. tek farkı; "bind", metodu execute etmez. ona parametreleri geçer. metod farklı satırda execute edilebilir. eğer argümanlar(args1, args2...) yollanmazsa; fonksiyon bir sonraki kod bloklarında execute edildiğinde de verilebilir. bind metodunda args'ler verilirse; ilerde execute ederken vermek gerekmez.

- __isGenerator()__

  (deprecated or not standart) fonksiyon içerisinde "yield" keywordu bulunup bulunmadığını döndürür. (yield başka başlıkta anlatılıyor)

- __toSource()__

  (deprecated or not standart) fonksiyon içindeki kod bloğunu string olarak döndürür.

- __toString()__

  toSource() ile aynı görevi görür. fakat tostring daha standarttır.

#### objelerin içerdiği fonksiyonlar:

- __valueOf()__

  o objenin primitive değerini döndürmelidir. == işaretinin yaptığı karşılaştırma için kullanılır. bu sebeple unique bir primitive döndürmelidir. valueOf() metodu objenin tipinden bağımsız bir eşitlik kontrolüdür. (başka başlıkta == vs === anlatılıyor)

  istisna olarak bir array'in valuof'u array'in kendisini döner.

  eğer valueof, developer tarafından hiç override edilmediyse json objesi döner. bu json objesinde ne olduğuna örnek üzerinden bakarsak:

  ```js
  function person(first) {

      this.firstName = first;

      this.lastName = null;

      this.changeLastName = function (name) {

          this.lastName = name;
      };
  }

  var myFather = new person("John");

  print(myFather.firstName);
  // output:
  // {
  //   firstName: John,
  //   lastName: null,
  //   changeLastName = function (name) {
  //         this.lastName = name;
  //   },
  //   __proto__: {}
  // }
  ```

# accessor property
Özel bir syntax'tır. "get a()" satırı, "object.a" dediğimizde döndürülecek degeri belirler. benzer şekilde "set a(v)" satırı, onu set ettiğimizde çalıştırılacak metodu çalıştırır. örnek:

```js
var o = {

  n: 1,

  get a(){ return this.n; },

  set a(v){ this.n = v*v; }
};

o.a // prints 1

o.a = 4;  //set ettğimiz satır

o.a // prints 16
```

# js'te bir syntax örneği

```js
(  function(name) {
              console.log("hello " + name)
}) ("ahmet")
```

Burada, "name" parametresi alan anonim bir fonksiyon tanımlanıyor. Bu fonksiyonu oluşturuyoruz (parantez içerisinde) ve hemen yanında metod çağırdığımızda yaptığımız gibi parantez içinde parametrelerini veriyoruz ve anonim fonksiyonu execute ediyoruz. sonuç olarak console'da "hello ahmet" çıktısını alıyoruz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# amd (Asynchronous Module Definition) vs commonjs
js dosyaları yazıldığında ve daha sonra kullanılabilir hale getirilmesi için belli bir formatta yazılması gerekmektedir. bu formatların standartlarıdır.

amd ve commonjs en çok tercih edilen standartlardır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# require.js
javascript kütüphanesi. sadece ilgili js modüllerinin yüklenmesini sağlamaktadır. yüklenen modüllerin bağımlılıkları varsa onları da otomatik yüklemektedir.

requirejs(['app/main']); ile istediğimiz modülün yüklenmesini sağlıyoruz.

modül tanımlamasını şu şekilde yapıyoruz:

```js
define("alpha", ["credits","products"], function(credits,products) {

        //my module code is here

});
```

bağımlılık olmadığı durumlarda define ikinci aldığı dizi parametresini hiç almayabilir. alpha ise bu tanımlayacağımız modülün id'si. biri dependency ile bu id ile cagrıyor bizim modülü.

require("myLib") ile bize "myLib" id'li kütüphaneyi dönüyor. bu objeyi kullanarak; içiden bir metod çağrabiliriz:

require("myLib").myMethod();

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# libary oluştuturken genelde yapılan tanımlamalar:

```js
if (typeof define === 'function' && define['amd']) {

     define(['jquery'], factory);

} else {

// other codes here
```

Burada "factory" takip edilirse; API'nin (libnarynin) olduğu kodu olduğu görülür.

"define" bir fonksiyon mu diye kontrol edilmiş. "define" requeire.js'in modül tanıtlatmak için public sunduğu bir metod'dur. eğer bu varsa require.js vardır demek oluyor. require.js var ise; define['amd'] ile define içerisinde amd desteğinini olup olmadığına bakılır.

ek not:

```js
define['amd'] = define.amd // true
```

eğer AMD support var ise if bloğuna giriliyor. require.js ile yeni bir modül yaratıyor. 'jquery' dependency'sini alacak şekilde yeni modülümüz tanımlanıyor. else durumlarda require.js yokken yapılacaklar yazılıyor.

- örnek

```js
(function (global) {

    'use strict';

    var MyModule = function () {

      /* Your awesome module logic here… */

    };
    
    // …and here

    MyModule.foo = 'bar';

    // AMD support

    if (typeof define === 'function' && define.amd) {

        define(function () { return MyModule; });

    // CommonJS and Node.js module support.

    } else if (typeof exports !== 'undefined') {

        // Support Node.js specific `module.exports` (which can be a function)

        if (typeof module !== 'undefined' && module.exports) {

            exports = module.exports = MyModule;

        }

        // But always support CommonJS module 1.1.1 spec (`exports` cannot be a function)

        exports.MyModule = MyModule;

    } else {

        //eger amd, nodejs, commonjs yoksa window.mymodule ile erişilebilmesi için bu işlem yapılıyor.

        global.MyModule = MyModule;
    }
})(this);
```

sondaki this ile windows objesi yakalanmış oluyor. kendini execute eden metod "global" paramteresi ile this'i (window'u) alıyor.

Kütüphaneler kendini parantez içine alııp execute ediyor. Eğer bunu yapmazlarsa "var" oluşturdukları her variable global scope'ta tanıımlanır. Bu da diğer lib'lerdeki variable'lerle çakışmasına sebep olabilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# web page lifecycle

- #### events

  - > $(document).ready( func );

    readystate interactive olduğunda bu metodu jquery çalıştırmaktadır. (readystate asagida anlatiliyor)

  - > document.addEventListener("DOMContentLoaded", func);

    executes when HTML-Document is loaded and DOM is ready to run any javascript safely.

    it waits to execute all internal inline javascripts (script tags) and also external src javascript documents. only exeption is "async" and "defer" attributes of external scripts.

    browser'ların autofill-form(otomatik form tamamlmama) DOMContentLoaded eventini beklemektedir.

    DOMContentLoaded eğer sayfa yüklendikten sonra handler'a set edilirse hiçbir zaman execute edilmez.

  - > $(window).load( func ); yada window.onload = func;

    iframelerin içi yüklendiğinde, resimler tamamen indirildiğinde bu metod çağrılır

  - > window.onunload = func;

    kullanıcı sekmeyi kapattığı zaman

  - > window.onbeforeunload = func;

    kullanıcı sekmeyi kapatmak istediği zaman. burada tek seçeneğimiz string döndürmek:

    ```js
    window.onbeforeunload = function() {

        return "There are unsaved changes. Leave now?";
    };
    ```

    bu stringi tarayıcı bir dialog'da gösteriyor ve evet hayır sçeneğini sunuyor. eveti seçerse sekme kapatılıyor. hayırı seçerse kapatılmıyor.


- #### readystate

DOMContentLoaded sadece readystate loading durumundayken handlera attach edilebilir.

```js
if (document.readyState == 'loading') {

  document.addEventListener('DOMContentLoaded', func);
}
```

doument readyState's:

> "loading" – the document is loading.

> "interactive" – the document was fully read.

> "complete" – the document was fully read and all resources (like images) are loaded too.

readyste'in değiştiği event'i de yakalayabiliriz:

```js
document.addEventListener('readystatechange', func );
```

- #### eventler ile gili notlar
  - asagidaki iki metod aynı şeyi yapar:

    - $(window).load( func );

    - $(window).on('load', func )

    Yukarıdaki load metodu document'te alabilir, button da alabilir.

  - asagdaki iki code ayni anlama geliyor. jquery sık kullanıldığı için bu şekilde ayarlamis.

    - $( document ).ready( func );

    - $( func );

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# $ prefix on variables
javascript kodlarında çoğu zaman jquery'nin namespae'i olan $ işareti görülür. bunun sebebi oluşturulan variable'ın jqueryden dönen bir değeri tuttuğunu belli etmekttir. örneğin;

var a = 3;
var $myObject = $("#email");

buna benzer bir durum birçok diğer kütüphaneyi kullanan programcıların yaptığı görülebilir. örneğin; underscore js kullananlar   
\_myVariable diye adlandırırlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# namespace

javascript'te en global değerler namespace olarak kullanılır. örneğin bir kütüphane eklediğimizde kendini buraya bir tanımlama yaparak ekler. bu şekilde herkes buradan onu çağırır. bu sebeple javascriptte buradaki değerler namespace dendir.

genelde bu tanımlama ile init yapılır:

var MAYAPPLICATION = MYAPPLICATION || {};

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# yield keyword

yield türkçe kelime anlamı: esneme.

fonksiyona kalındığı yerden devam edilebilmesini sağlar. yield return eder, fakat bir "Generator" objesi döndürür. "function \*" ibaresindeki yıldız işareti fonksiyonun bir generator objesi döndürdüğünü temsil eder. örnek:

```js
function* foo(x) {

    while (true) {

        x = x # 2;
        yield x;
    }
}

var g = foo(2);

g.next(); // -> 4

g.next(); // -> 8

g.next(); // -> 16
```

# yield*
yield içindekileri bir üstteki metodun generator'ı ile birleştirmek istersek yield# kullanırız. örnek:

```js
function* g1() {

  yield 2;

  yield 3;

  yield 4;
}

function* g2() {

  yield 1;

  yield* g1();

  yield 5;
}

var iterator = g2();

console.log(iterator.next()); // {value: 1, done: false}

console.log(iterator.next()); // {value: 2, done: false}

console.log(iterator.next()); // {value: 3, done: false}

console.log(iterator.next()); // {value: 4, done: false}

console.log(iterator.next()); // {value: 5, done: false}

console.log(iterator.next()); // {value: undefined, done: true}
```

# yield ile hiçbir şey döndürülmediğinde ne olur?
yield keywordunun yanında hiçbir şey olmadığında, örnek:

```js
function* g1() {

  yield;
}
```

iterator şunu döner: {value: undefined, done: true};

# generator nasıl done=true olduğunu anlıyor?
eğer yield'dan sonra herhangi bir kod satırı var ise; done:false oluyor.

# var iterator = g2();
g2 bir genrator donen obje ise; "var iterator" atık genrator objesidir ve "g2()" kodunda parentez açılmasına rağmen; hiçbir kod execute edilmez. g2'nin ilk satırları dahi ancak iterator.next() dediğimiz zaman çağrılır.

# yield kullanılan fonksiyonlarda return keywordü
return de iterator next metodunda yield gibi değer dönüdürür. yield ile apaynı davranışı sergiler. fakat her zaman done:true'dur. bundan sonra itetrator devam etmez. tek fark budur.

return değeri aşağıdaki gibi değer atama görevi görmektedir.

```js
function# g1() {

  yield 2;
  return 3;
}

function# g2() {

  yield 1;
  var a = yield# g1();
  console.log(a);
  yield 4;
}

var iterator = g2();

console.log(iterator.next()); // {value: 1, done: false}

console.log(iterator.next()); // {value: 2, done: false}

console.log(iterator.next()); // {value: 3, done: false}

3 //console.log(a) çıktısı

console.log(iterator.next()); // {value: 4, done: false}

console.log(iterator.next()); // {value: undefined, done: true}
```

Yukarıda "var a = yield# g1();" daki satırda # karakteri hiç kullanılmasaydı:

var a = yield g1();

a değerine hiçbir değer atanmayacaktı. generator'ımız;

{value: 2, done: false}

yerine;

{value: Generator, done: false} 

dönecekti. ve a değeri undefined olacağından console.log undefined basacaktı. fakat; next(); 'e yollayacağımız ilk parametre a'ya atanıyor olacaktı. aşağıda direk örnekle gidelim:

var a = yield g1(); satırını işleten next() metodundan sonraki next() metoduna paramtre geçseydik: next(99); o zaman "var a" değerimiz 99 olacaktı.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# noConflict metodları
javascriptte namespaceler diğer dillerdeki gibi düzenli yönetilemeyebiliyor. karışıklık olmaması için her kütüphane en tepede noConflict isimli bir metod tanımlıyor. örneğin jquery'de bu metod şunu yapıyor.

```js
var j = jQuery.noConflict();
j( "div p" ).hide();
$( "content" ).style.display = "none";
```

Yukarıda noConflict metoduna true parametresi geçilseydi artık 3 üncü satırda $ işareti de kullanılamaz hale gelecekti. noConflict(true)'yu, $ işaretini başka bir kütüphane kullanıyor ise yapabiliriz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# arrays

- #### obje'den türemiştir.

var cars = ["Saab", "Volvo", "BMW"];

var cars = new Array("Saab", "Volvo", "BMW");//array fonksiyonu.

new Array tercih edilmemeli, çünkü yanlış anlaşılma olabilir. zira constructor tek parametre ve sayı alınca boş array oluşturuyor:

new Array(20); //20'lik bir dizi oluştu. bazıları bunu 1 elemanlı bir dizi olduğunu düşünebilir.

- #### erişmek için:

> cars[1];

javascript'te arrrayler birer objedir. aslıda her dizi elemanı bir property'dir. sadece access'i farklıdır. bunun sebebi:

herhangi bir objede 0 veya 1 isimli property'ye şu şekilde erişebiliyoruz:

> myArr["0"]

yada

> myArr[0]

Sayı vererek eriştiğimizde aslında; javascript interpreter'ı onu string'e çeviriyor. Bu sebeple myArr["0"] değeri myArr[0] ile aynı şeyi veriyor.

Yani bu erişim arraylere özgü bir durum değildir. arraylarin içindeki metodlar otomatik propertieleri sayısal cinsten tutmaktadır. örneğin "jquery objesi" (konu başka başlıkta anlatılıyor) array dönmüyor fakat liste içinden bir elemana erişmek istediğimizde; yine index ile erişebiliyoruz.

- #### array'in hazır metodları:

- cars.length;

- cars.sort(); default sorts alphabetically.

  sort; isteğe bağlı olarak bir parametre olarak fonksiyon alıyor. örnek:

  cars.sort(function(a, b){

    return (b - a);
  });

  negatif deger dönerse a, b den küçük demektir. tüm dizinin elemanları birbiri ile karşılaştırıyor.

- fruits.pop(); //removes last element

- fruits.push("Kiwi"); //adds element to last index and return the last new index

- fruits.shift(); // removes first element

- fruits.unshift("Lemon"); // adds element to first index

- fruits.splice(2, 4, "Lemon", "Kiwi"); //2'inci elemandan itibaren, 4 tane eleman siliyor (silinen elemanların indexleri: 3,4,5,6) + 2'inci indexten itibaren sağ tarafta olan bütün argümanları; "lemon" ve "kiwi"'yi diziye ekliyor ekliyor. örnek:

   var fruits = ["1", "2", "3", "4"];

   fruits.splice(2, 0, "x", "y");

   prints(fruits); // prints 1,2,x,y,3,4

- arr1.concat(arr2, arr3);

  sırası ile birleştiriyor. sonsuz parametre kabul ediyor.

- fruits.slice(1,3); returns new array from 1-3 index

# For loop comparison table

| how to call                                                      | change scope/context | iterate over objects | how to break                              | access all array list | change orjinal variable | iterate over empty slots |
|------------------------------------------------------------------|----------------------|----------------------|-------------------------------------------|-----------------------|-------------------------|--------------------------|
| lodash.forEach(arr,   function( index, val )); (or)  lodash.each | false                | true                 | return  false/null/undefined  on callback | false                 | true (read NOT-A)       | true                     |
| jQuery.each( arr,  function( index, val ));                      | false                | true                 | return false/null/undefined on callback   | false                 | true (read NOT-A)       | true                     |
| for(val in arr) { ... }                                          | true                 | true                 | break keyword                             | true                  | true                    | false                    |
| for(i=0; i<arr.length; i++) { ... }                              | true                 | false                | break keyword                             | true                  | true                    | true                     |
| underscore.each(arr,function(val, index, arr),context)           | true                 | true                 | not possible                              | true                  | true (read NOT-A)       | true                     |
| underscore.every(arr,function(val, index, arr),context)          | true                 | true                 | return false/null/undefined on callback   | true                  | true (read NOT-A)       | true                     |
| arr.forEach(function(val, index, arr), context);                 | true                 | false                | not possible                              | true                  | true (read NOT-A)       | false                    |

NOT-A:

orjinal elemanı callback'e geçiyor. dolayısı ile değişkenler burada değiştirilebilirler. fakat genel javascript kuralları gereği bilinmesi gerekenler var. callback metodu yeni bir fonksiyon olacağı için geçilen değerler 2 durumda değiştirilemezler:

1- eğer yeni bir obje ataması yapılırsa (çünkü yeni objenin referansı farklı. orjinal  obje'nin içeriği değiştirilmemiş olacak. ve orjinal dizi; referansla elemanları tutuyor.

2- değiştirilen eleman bir primitive (string, int...) ise. çünkü primitive'ler metodlara atanırken sadece değerleri geçer (referansları değil).

Bu iki durum için geçici olarak "access all array list" kuralı true ise; orjinal objenin içindeki referans manuel değiştirilir.


- #### Tablo hakkında

- lodash.forEachRight ve lodash.eachRight aynı metodlardır. lodash.each ile aynı özelliklere sahipler. tek farkı liste elemanlarının sırasını tersten dönmesidir.

- "iterate over empty slots" kuralı:

   boş slotlar (hiç atanmamış değerler) için callback çağrılıyor dönmüyor.

   örnek:
   
   ```js
   var a = ['a0'];

   a[3] = 'a3';

   a[4] = undefined;

   a[5] = null;
   ```

   sadece a[1] ve a[2] boş. bunlar için for loop callbak çağrılması.

   eğer boş olup olmadığı kütüphane içinde kontrol ediliyorsa bu yavaşlığa sebep olmaktadır.

- "iterate over object" kuralı:

   eğer list bir js objesi ise, yine döngü çalışıyor ve her property'si dönmeye başlıyor. 

   method'un aldıgı parametreler'in anlamı değişiyor:

   list array ise; (value, index)

   list obje ise; (value, key)

- elle for döngüsünün yazılması ( for(i++) şeklinde ) diğer tüm döngülerden çok daha performanslı çalışmaktadır.

- $.each() metodu ile $(selector).each() aynı değildir. $(selector).each() bir jquery objesinin içerisinde dönmeye yarıyor.

- çoğu kütüphanenin "map" metodları da vardır. bu metodlar for metodları ile aynı parametreleri alır. map metodları callback metodlarından return edilen her elemanı yeni bir diziye atara. bu yeni diziyi de map metodu return eder. map metodunun temel felesefesi budur. for yerine map yada map yerine for kullanmak anti-pattern'dir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# ecmascript vs javascript vs jscript vs ActionScript
javascript ve jscript vs ActionScript; birer ecmascript implementasyonudur. buna rağmen, bazı implementasyonlar kendilerince spesifikasyon dışı ek özellikler içerebilirler.

# CoffeeScript vs typescript
javascript'e çevrilen bir programlama dilleridir.

# source-to-source compiler (or transcompiler or transpiler)
Bir dil, derlenmeden önce başka bir dile çevrilebilir. Bu işlemi yapan çeviriciye transpiler denir.

# typescript version history

aşaıdaki sürümler arasında minor versiyonlarda mevcuttur.

| version | release date      | important changes                                                                                                                                      |
|---------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1.1     | 6 October 2014    | performance improvements                                                                                                                               |
| 1.3     | 12 November 2014  | protected modifier, tuple types                                                                                                                        |
| 1.4     | 20 January 2015   | union types, let and const declarations, template strings, type guards, type aliases                                                                   |
| 1.5     | 20 July 2015      | ES6 modules, namespace keyword, for..of support, decorators                                                                                            |
| 1.6     | 16 September 2015 | JSX support, intersection types, local type declarations, abstract classes and methods, user-defined type guard functions                              |
| 1.7     | 30 November 2015  | async and await support,                                                                                                                               |
| 1.8     | 22 February 2016  | constraints generics, control flow analysis errors, string literal types, allowJs                                                                      |
| 2.0     | 22 September 2016 | null- and undefined-aware types, control flow based type analysis, discriminated union types, never type, readonly keyword, type of this for functions |
| 2.1     | 8 November 2016   | keyof and lookup types, mapped types, object spread and rest,                                                                                          |
| 2.2     | 22 February 2017  | mix-in classes, object type,                                                                                                                           |
| 2.3     | 27 April 2017     | async iteration, generic parameter defaults, strict option                                                                                             |
| 2.4     | 27 June 2017      | dynamic import expressions, string enums, improved inference for generics, strict contravariance for callback parameters                               |
| 2.5     | 31 August 2017    | optional catch clause variables                                                                                                                        |
| 2.6     | 31 October 2017   | strict function types                                                                                                                                  |
| 2.7     | 31 January 2018   | constant-named properties, fixed length tuples                                                                                                         |
| 2.8     | 27 March 2018     | conditional types, improved keyof with intersection types                                                                                              |
| 2.9     | 14 May 2018       | support for symbols and numeric literals in keyof and mapped object types                                                                              |
| 3.0     | 30 July 2018      | project references, extracting and spreading parameter lists with tuples                                                                               |
| 3.1     | 27 September 2018 | mappable tuple and array types                                                                                                                         |
| 3.2     | 30 November 2018  | stricter checking for bind, call, and apply                                                                                                            |
| 3.3     | 31 January 2019   | relaxed rules on methods of union types, incremental builds for composite projects                                                                     |
| 3.4     | 29 March 2019     | faster incremental builds, type inference from generic functions, readonly modifier for arrays, const assertions, type-checking globalThis             |
| 3.5     | 29 May 2019       | faster incremental builds, omit helper type, improved excess property checks in union types, smarter union type checking                               |
| 3.6     | 28 August 2019    | Stricter generators, more accurate array spread, better unicode support for identifiers                                                                |

# ECMAScript
ECMA-262 ve ISO/IEC 16262 standartları ie oluşturulan betik dilidir.

# ECMAScript (or ES) version history

| Name                                               | Date Puplished |
|----------------------------------------------------|----------------|
| ES5                                                | 2009           |
| ES5.1                                              | 2011           |
| ECMAScript 2015 (or ES2015 or ECMAScript 6 or ES6) | 2015           |
| ECMAScript 2016 (or ES2016 or ECMAScript 7 or ES7) | 2016           |
| ECMAScript 2017 (or ES2017 or ECMAScript 8 or ES8) | 2017           |
| ECMAScript 2018 (or ES2018 or ECMAScript 9 or ES9) | 2018           |

"ES.Next" ECMAScript'in br sonraki versiyonunu belirten özel bir takma addır.

Ecmascript ile javascript'in versiyonları aynıdır. Çünkü ecmascript'in referans implementasyonu javascript'tir.

Typescript'in herhangi bir sürümü, istenilenilen javascript'in herhangi bir sürümüne çevrilebilir. ancak istisna olarak bazı özellikler javascript'te hiç desteklenmiyor olabilir. böyle durumlarda, js tarafında sürüm yükseltmek gerekebilir.

# ecmascript implementasyonları standardize edilirken, her sürüm kendi içinde belli sürümlere ayrılır.

| sürüm kodu | sürüm adı | açıklama                                          |
|------------|-----------|---------------------------------------------------|
| stage-0    | Strawman  | just an idea, possible Babel plugin               |
| stage-1    | Proposal  | this is worth working on                          |
| stage-2    | Draft     | initial spec                                      |
| stage-3    | Candidate | complete spec and initial browser implementations |
| stage-4    | Finished  | will be added to the next yearly release          |

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Browser Object Model (or BOM)

html tarayıcılarının javascript'e ekledikleri javascript objeleridir. bu objeler nodejs gibi ortamlarda olmuyorlar.


## window

genel bir objedir. js'te global tanımlanan her değer buraya bağlanmaktadır. örnek metod:

> window.close()

## window.screen

fiziksel ekranla ilgili bilgiler içeren javascript objesidir. örnek:

> screen.width

> screen.height

## window.location

url ile ilgili metodlar buradadır.

> window.location.href 

## window.history

> history.back();

## window.navigator

tarayıcının user agent bilgilerini barındırır.

## document.cookie

cookie metodları buradadır.

## document

windows.document ile de aynı objeye erişilebiliyor. DOM ile ilgili metodlar buradadır. örnek:

> document.appendChild(element);

> document.write(text);

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# jquery object (or jQuery collection object)

$( 'li' ); metodundan dönen obje, jquery objesi olarak adlandırılır. bu adlandırma jquery'nin kendi içinde belirlediği bir standartdır. yazılımcıların birbiri arasında anlaşabilmesi için konulan özel bir isimdir. javascript'te herşey ( $, JQuery dahi ) birer obje olduğundan "javascript objesi" ile isim karışıklığı yaşanabilmektedir.

jquery object, array objesi ile benzer property'ler içeriyor fakat Array yada Array'den türemiş bir obje değildir.

Örnek kullanımlar:

```js
var listItems = $( 'li' );
var rawListItem = listItems[0]; // or listItems.get( 0 );
$( '<p>Hello!</p>' ); //creates new element

//search inside a spesific block
var paragraph = $( 'p' );
$( 'a', paragraph );
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# javascript executes code in 3 phases

1- First, the engine walks through the code, looks for function declarations and hoists them (moves them to the top)

2- it hoists variable declarations

3- finally it runs the "normalized" code.

example:

```js
function bar() {

        return foo; // foo degerinin tanımı yok.

        foo = 10; //foo degerinin hala tanımı yok.

        function foo() {} //foo degerinini tanımlaması burda. yukarıda eksikti. bu sebeple kodun en başına alınacak.

        var foo = 11; //foo degerinin artik tanımlanması var. "var" keyword'üne artık gerek yok.
}
```

"normalized" code:

```js
function bar() {

    function foo() {} 

    return foo; //kod execute edildiğinde kod bu kısımda sonlanacaktır. aşağıdaki kodlar unused'tir.

    foo = 10;

    foo = 11;
}
```
