
############################

############################
# JAVASCRIPT REACT
############################

############################

# reactJS

MVC mimarisindeki V katmanını karşılayan js kütüphanesidir. çünkü React'ın yaptığı; React.createElement(); yapıp render edilecek view'ı döndürmektir. Businnes logic'in içerde yapılıp yapılmadığı developer'ın kendisine kalmıştır.

React bir framework değildir. React fonksiyonel componentleri sadece render edilecek objeyi döndürecek şekilde tasarlanmıştır. react bu sebeple bir framework değildir.

- # jsx

Jsx dosya uzantısıdır. developer kodları tarayıcıya atmadan, bir transpiller aracılığı ile kodları js'e çevirir. developer web tarayıcısından debug ettiğinde js dosyası görür. jsx, direk olarak ecmascript implementasyonu değildir. fakat ek kurallar içererek bazı kolay okunabilirlik, hızlı yazılabilirlik gibi özellikler kazandırmaktadır. jsx sadece react için yazılmış bir syntax değildir. fakat ilk reactjs ile çıktığından her tarafta bu şekilde anılır. piyasada "react" syntax'ı denildiğinde jsx uzantısı kastedilir. oysa bu algı yanlıştır.

react örnek kodları minimum ecmascript 6 (güncel) sürümünü kullanır. fakat istenirse eski sürüm js'ler ile de react kütüphanesi çağrılıp kullanılabilir. react kodları incelenirken javascript'teki class gibi birçok yeni yapı görülebilmektedir.

Örnek bir jsx dosyası:

```jsx
var Sayac = React.createClass({

  artir: function () {

        var a = 3;
   },

  render: function () {

    return (

         <div>
          <View style={styles.progressCircleContainer}>
              <Progress.Circle size={50} indeterminate thickness={10} />
          </View>
        </div>
    }
})
```

Yukarıdaki kod tarayıcıda transpiller'dan geçtikten sonra aynı kalır; sadece render'ın içi şu şeklde döner:

```js
return React.createElement(

        "div",

        null,

        React.createElement(

             View,

             { style: styles.progressCircleContainer },

             React.createElement(Progress.Circle, { size: 50, indeterminate: true, thickness: 10 })
        )
```

jsx syntax örnekleri:

```jsx
const element = <h1>Hello, {name}</h1>;

// yada

const element = (<h1>Hello, {name}</h1>);


// yukarıdaki elementi aşağıya yollayabiliriz:
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

```jsx
const element = (
  // bunun içerisi js'tir. fakat tek satırlıktır. bu sebeple noktalı virgül ile birkaç satır yazamayız.
  // bu js'inm içerisine yazılan kod return edilir ve direk ekranda output olarak gösterilir.
  <h1>
    
    Hello, {formatName(user)}
  </h1>
);

// Genel javascript bilgimize bakarsak;
if(user && user.lastName){ // if içerisinden string dönmektedir fakat bu condition'a sokulduğunda "true" olarak dönüş yapar.
  console.log(user && user.lastName); // if condition'unun içerisindeki ile birebir aynı kod var. burası da string dönüyor. fakat condition içerisinde olmadığından dolayı string kalmaya devam ediyor.
}

// multine line javascript yazılamıyor fakat aynı satırda olduğu için ve/veya gibi işlemler kullanabiliriz. örnek:
const element = (
  <h1>
     Hello, {user && formatName(user)}
  </h1>);

// aynı javascript syntax'ını xml element'lerine prop eklerken de uyguluyoruz:
const element = <img src={user.avatarUrl}></img>;
```

```jsx
// escmascript'in güncel sürümlerinde gelen string içinde dinamik değer kullanmada aynı şekilde jsx'te de beklendiği gibi (değişiklik olmadan) kullanılabilir:
const element = (
  <h1>
     {`hello ${user.name}`}
  </h1>);

// eski sürüm javascript'ler ile yukarıdakini bu şekilde yazabiliriz:
const element = (
  <h1>
     {"hello " + user.name}
  </h1>);
```

# react temel mimari

AngularJs'te olduğu gibi tüm değişkenlerin değişip değişmediğini kütüphanenin kendisi hep kontrol etmiyor. SetState() metodunu yazılımcının çağırması bekleniyor. Bu sebeple performans açısından avantaj sağlanıyor.

React componentlerinde (view'da) bir değişiklik olduğunda, react komple component'i tekrar render ediyor. Burada performans sorunu ortaya çıkıyor. Fakat bunu çözmek için virtual-Dom mekanizması devreye giriyor. React sanal-dom üzerinde değişiklikleri render ediyor ve gerçek dom'a sadece değişiklikleri aktarıyor (buradaki sürece verilen özel isim: __Reconciliation (or Uyumlaştırma)__)

Sayfa render edilirken state değişikliği yapılmaması gerekiyor.

State deişikliklerinde zaten render metodu çalışacağı için sayfa yeniden yeni değerlere göre değişecektir. dolayısı ile yazılımcı update kodlarını yazmaktan kurtulacaktır. angular-js'te two-way binding olduğundan ekrandaki değişkenler otomatik güncellenir, fakat businnes logic isteyen kodlar işlenmez. sadece variable'ler güncellenir. angular-js'te de sayfa initialize olurken herşeyi parametreki alırsa, orda da güncelleme için kod yazmak gerkemez, fakat bu durumda o projede zaten react kullanılması daha mantıklı olacaktır. çünkü react bu feslefe üzerine kuruludur.

__Fiber__ react'ın 16'ıncı versiyonu ile gelen Reconciliation motorudur.

- # page navigation
reactJS'te geçişler single page'dir. web tarayıcısında farklı bir sayfaya gidilmez. fakat rect-native'de bazı routing kütüphaneleri tek activity kullanırken, bazıları her sayfayı farklı activity'lere yönlendirebilir.

React'ta temel olarak routing aşağıdaki şekilde çalışır. About, Users, Home componentleri bulunan sayfaya göre render ediliyor yada edilmiyor. bir routing gerçekleştiğinde tüm sayfa değil sadece Switch'in içi değişiyor.

```jsx
// bu örnek temel mantığı göstermek için yazılmıştır. react-router-dom ile yazılmıştır.
<Router>
    <div>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
          <li>
            <Link to="/users">Users</Link>
          </li>
        </ul>
      </nav>

      <Switch>
        <Route path="/about">
          <About />
        </Route>
        <Route path="/users">
          <Users />
        </Route>
        <Route path="/">
          <Home />
        </Route>
      </Switch>
    </div>
</Router>
```

 - ## react-router
   routing yapmak için bir kütüphanedir. eğer react-native kullanıyorsak react-router-native paketini de eklmememiz şarttır. eğer html geliştiriyorsak; react-router-dom eklememiz şarttır.

   DOM ve native paketlerinde aynı interface'ler ile API sunar.
   
   3 ve 4üncü sürümler arasında önemli değişiklikler var.

   örnek kullanım:

   ```jsx
   import {
    BrowserRouter,
    Switch,
    Route,
    Link
   } from "react-router-dom";

   <BrowserRouter>
      <div>
        <nav>
          <ul>
            <li>
              { /* we can use also <a href> here */ }
              <Link to="/">Home</Link> 
            </li>
            <li>
              <Link to="/about">About</Link>
            </li>
            <li>
              <Link to="/users">Users</Link>
            </li>
          </ul>
        </nav>

        {/* switch is optional component. 
            If we use Switch, only first match will render.
            If we don't use it, then react will render all components
            which match. example: 
            if the url is "/about/company" it will render both "/about" and "/about/company".
        */}
        <Switch>

          <Route path="/about">
            <About />
          </Route>
          
          <Route path="/users"> { /* or only: <Route path="/users" component="Users"> */ }
            <Users />
          </Route>

          { /* below render is not different from component.
            it allows us to create nline functions.
            this feature called "dynamic routing". it is different then "static routing".
            because dynamic routing allow developers to decide which component will render on runtime. */ }
          <Route
                path={`${match.path}/:name`}
                render={({ match }) => (
                  <div>
                    {" "}
                    <h3> {match.params.name} </h3>
                  </div>
                )}
          />

          <Route path="/">
            <Home />
          </Route>

        </Switch>

        { /*
        istersek buraya yukarıdaki ile aynı path'e sahip route tanılmayabiliriz. aynı path olduğundan ikiside render olacaktır.
        <Route path="/users">
            <Users />
        </Route> 
        */ }

        { /*
        hatta buraya ikinci bir switch daha koyup altına birçok route koyabiliriz:
        <Switch>
          <Route path="/users">
              <Users />
          </Route> 
        </Switch>
        */ }

      </div>
   </BrowserRouter>

   {/* sadece Users componenti içinde nested routing yapalım */}
   function Users() {

      let match = useRouteMatch(); // import from "react-router-dom"

      return (
        <div>
          <h2>Users</h2>

          <ul>
            <li>
              <Link to={`${match.url}/details`}>
                Details of user
              </Link>
            </li>
            <li>
              <Link to={`${match.url}/main_details`}>
                Main details of user
              </Link>
            </li>
          </ul>

          {/* here is nested routing */}
          <Switch>
            <Route path={`${match.path}/:userId`}>
              <UserPhoto />
            </Route>
            <Route path={match.path}>{/* default page */}
              <h3>Please select a link</h3>
            </Route>
          </Switch>
        </div>
      );
   }
   ```

   Auth, sidebar, nesting gibi en temel örnekler çok basit şekilde burada hazırlanmıştır: (source-id: 219)

 - ## react-router-redux (or old-name:redux-simple-router)
   tekrar deprecated oldu, artık __connected-react-router__ paketi kullanılıyor.

   react-router'ı wrap ediyor. bu kullanımı opsiyonel olan bir js kütüphanesidir. redux state'ine otomatik olarak:
   - url
   - url'ile geçilen path parametreleri
   
   gibi birçok history meta bilgisi ekliyor. bu şekilde developement/debug işlerimizi çok kolaylaştırabiliyoruz.

   __routerMiddleware__ connected-react-router'ın middleware'idir. kullanılması zorunlu diildir. fakat dispatcher'ın push gibi history işlemleri yapabilmemiz için şarttır. eğer bu olmazsa sadece linkler ile gidilebilir. routerMiddleware initialize olurken parametre olarak history (history.js değil! history başka başlıkta anlatılıyor) kütüphanesini istemektedir.

   connected-react-router, redux state'ini değiştirdiği için, state'deki değişikliklerimizi belirleyen reducer'larımıza kütüphanenin reducer'ını eklememiz şarttır:

   ```js
   // reducers.js
   import { combineReducers } from 'redux'
   import { connectRouter } from 'connected-react-router'

   const createRootReducer = (history) => combineReducers({
      router: connectRouter(history),
      ... // rest of your reducers
   })
   export default createRootReducer
   ```

   Resmi github sayfaındaki FAQ'da güzel notlar var: (source-id: 220)

 - ## react-native-router-flux
   
   TODO bu kısımı tümüyle gözden geçir !!

   sadece react-native için alternatif routing kütüphanesidir. react-navigation için farklı bir API sunmaktadır. Bu sebeple kod sadece javascript'ten ibarettir.

 - ## react-navigation vs react-native-navigation
   ikiside sadece react-native için routing kütüphanaleridir.

   react-navigation kodunun çoğu javascript iken, react-native-navigation'ın çoğu kodu native dillerle yazılmıştır.

   - ### react-navigation

        ```js

         // App.js

         import { createStackNavigator } from "react-navigation";

         import Home from "./scenes/Home";
         import PushedView from "./scenes/PushedView";

         export default createStackNavigator({
            Home: {
                screen: Home,
                navigationOptions: {
                    title: "Home"
                }
            },
            PushedView: {
                screen: PushedView
            }
         });

        ```

        ```js
        // scenes/Home.js

        type Props = {
            navigation: Object
        };

        export default class Home extends Component<Props> {

            goToPushedView = () => {
                this.props.navigation.navigate("PushedView");
            };

            render() {
                return (
                    <View>
                        <Button
                            onPress={this.goToPushedView}
                            title={"Push something"}
                        />
                    </View>
                );
            }
        }
        
        ```

        Yukarıda this.props.navigation.navigate yerine this.props.navigation.push kullanılırsa, aynı sayfalara tekrar gidilmesi sağlanabilir. Aynı sayfalara tekrar gidince aynı activity'den yeni bir tane daha oluşturulmuş olur.

   - ### react-native-navigation
     1 ve 2inci sürümleri arasında çok büyük farklılıklar var.

 - ## NavigatorIOS
   sadece ios için çalışan bir routing kütüphanesi. desteği kaldırıldı.

 - ## createStackNavigator vs createSwitchNavigator
   react-navigation'ın (sadece native için geliştirilen routing kütüphanesi) fonksiyonlarıdır.

   createSwitchNavigator Authentication süreçleri gibi (örnek login olma) geri tuşunun olmayacağı ve her defasında yeni açılan sayfanın eskisini yoketmesi ile çalışan sayfalarda kullanılır. kullanıcı geri gidememelidir.

   createStackNavigator ise geri tuşuna basıldığında bir önceki sayfaya gidilen cinsten routing yapmamızı sağlayan metoddur.

   bu metodlara sayfalarımızı (component) ve config'lerimiz geçeriz.

  - ## history

    history.js (https://github.com/browserstate/history.js/) ile bir bağlantısı yoktur.

    https://github.com/ReactTraining/history reposunda geliştirilen pakettir.

    redux ve react-native'den tamamen bağımsız bir js kütüphanesidir. fakat react-router bu kütüphaneden yararlanarak çalışır.

    normal koşullarda web tarayıcısı history'yi tutar. "history" paketi ise js motoru üzerinde history'nin tutulmasını sağlar ve bize history change listener, change history gibi birçok metodun bulunduğu API sunar.

    aşağıdaki import'lar yapılarak history kullanılabilir olur:

    html 5 destekleyen tarayıcılar (diez olmadan history değişiklikleri sağlar):

    > createBrowserHistory

    react-native gibi js motorunun web tarayıcılar tarafından yönetilmediği platformlar için:

    > createMemoryHistory

    html5 olmayan tarayıcılar (diez işareti ile kullanımı sağlar):

    > createHashHistory

    HashHistory'nin BrowserHistory'ye göre avantajı kopyalanabilir linkler üretmektedir. Örneğin; BrowserHistory kullanıyor olalım. /"user/detail" sayfamız olsun. Bu sayfaya react uygulamamızdan yönlenince (html-5 standartları gereği) sunucuya HTTP GET isteği yapmaz. Lokalde (browser'da) bir history oluşturur. "HTML 5 yenilikler" başlığında bu konu anlatılıyor. Fakat; son kullanıcı url'den kopyalayıp bu linke gitmeye çalışırsa, web tarayıcısı sunucuya HTTP-GET isteği atacaktır. Dolayısı ile sunucuda buna karşılık bir controller olması şarttır. react-boilerplate projesinde ayağa kalkan nodej server'ı default olarak bunu yapıyor: gelen herhangi bir isteğe karşılık index.js'i döndürüyor. Tabi bu yüklenince otomatik uygulama iligli path'e routing yapıyor.

    örnek kod:
    
    ```js
    import createHistory from "history/createBrowserHistory";

    const history = createHistory();
    // Get the current location.
    const location = history.location;
    ```

  - ## react-history
    "history" paketi için react component wrapper'ıdır. örnek kod:

    ```xml
    <History>
            {({ history, action, location }) => (

              <p>
                The current URL is {location.pathname}
              </p>
            )}
    </History>
    ```

# setState()
aldığı ilk parametre bir json objesidir. bu obje state'e ekleniyor, var olan değerler varsa update ediliyor. ikinci parametre ise opsiyonel callback metodu.

setState metodu asenkrondur. bu sebeple, setState'e yolladığımız callback metodumuzunda hiçbir zaman senkron çalışmayacağını unutmamak gerekli. js tek thread çalıştırılıyor. dolayısı ile thread'imiz, yani setState'i çağıran metodumuz bitmeden, callback metodumuz da çağrılmayacak. 

Component'in içindeki this.props ve this.state değerleri setState metodu tetiklenip, render işlemi bittikten sonra güncellenir.

dolayısı ile bazı durumlarda; aşağıdakinin yerine:

```js
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

bunu yapmak isteyebiliriz:

```js
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

Bu bize; render tamamlanmış olmasa da, en son çağrılan setState'in state değerini verecektir.

aynı zamanda react setState işlemlerini kuyruğa alıp sıra ile işlemez. onun yerine hepsini birleştirir öyle render'ı çalıştırır.

```js
handleIncrement = () => {
  this.setState({ count: this.state.count + 1 })
  this.setState({ count: this.state.count + 1 })
  this.setState({ count: this.state.count + 1 })
}

handleDecrement = () => {
  this.setState({ count: this.state.count - 1 })
  this.setState({ count: this.state.count - 1 })
  this.setState({ count: this.state.count - 1 })
}
```

Yukarıdaki handleIncrement metodundaki kod'daki state buna eşittir:

```js
Object.assign(  
  {},
  { count: this.state.count + 1 },
  { count: this.state.count + 1 },
  { count: this.state.count + 1 },
)
```

Dolayısı ile bu şekilde yapmalıyız:

```js
handleIncrement = () => {
  this.setState((prevState) => ({ count: prevState.count + 1 }))
  this.setState((prevState) => ({ count: prevState.count + 1 }))
  this.setState((prevState) => ({ count: prevState.count + 1 }))
}
```

# forceUpdate()
render metodunun çalışmasını sağlıyor. child componentlerinde update olmasını sağlıyor. bu metodun kullanılması önerilmiyor. zaten state yada props değiştiğinde render otomatik çağrılıyor. bu sebeple bu metoda gerek yok. faat bazen class yada dışardaki farklı static değerler render içinde kullanılıyorsa (ki bu hiç önerilmiyor) forceUpdate metoduna ihtiyaç olmaktadır.

# component objesi metodları (lifecycle)

- #### sayfa render olurken bir component'in sırası ile aşağıdaki metodları çağrılır:

  > constructor

    burada setstate metodu çalışmaz. this.state = {...} state değişkenşni direk değiştiririz.

  > componentWillMount
  
  bu metod tamamlanmadan render çalıştırılmaz. bu sebeple burada çalıştırılan setstate() işlemleri re-render işlemini tetiklemez. componentWillMount içinde çalıştırılan async metodlar bu kurala dahil diildir.

  > render( )
  
  pure bir metod olmalı aynı state'e karşılık hep aynı şeyi döndürmeli.

  > componentDidMount
  
  ajax call'ların burada yapılması önerilir. burada setstate işlemi re-render'ı tetikler.

- #### Bir componentin state'inin yada props'unun değişmesiyle tekrardan render edilmesi sonucu çağrılan methodlardır:

  > componentWillReceiveProps( nextProps )
  
  metodun icinde nextProps vs this.props karşılaştırması yapabiliriz

  > shouldComponentUpdate( nextProps, nextState )
  
  eger false dondurursek buradan sonra hicbir metod cağrılmaz

  > componentWillUpdate( nextProps, nextState) )
  
  setState işlemi burada yapılmamalı. eğer şart ise bir önceki metodlar tercih edilmeli.

  > render( )

  (yukarıda açıklandı)

  > componentDidUpdate( )
  
  ajax işlemleri burada olmalı



- #### Komponent yok edilirken çalıştırılacak metod:

  > componentWillUnmount()
  
  obje destroy olduğunda tetikleniyor



# prop vs state

props; properties'in kısaltmasından gelir.

componentlerde hem prop hemde state isimli json'lar vardır. ikisinden biri değiştiğinde render tekrardan çağrılır. bu sebeple bu iki json, ancak setState() gibi metodlarla değiştirilmelidir. çünkü react ancak bu şekilde render'ı çağıracaktır. state.myValue=9; değişikliğini react bilemez, ve render'ı çağıramayacaktır.

prop bir üst componentten aktarılan event ve variable'lardır. state ise component'in tamamen kendi içinde tuttuğu variable'lardır. propslar mantıken değiştirilmemelidir. state ler ise; değiştiğinde sayfanın render'ının çalışması gerektiği verileri içermelidir. değiştiğinde sayfa render edilmeyecekse, component class'ının variable'ı tanımlanmalıdır.

bir component prop'ların nereden geldiğini hiç bilmez. componenti çağıran component ona datayı kendi state'indne or redux'ın stateinden atmış olabilir. aşağıdan yukarıya data geçilemez (tek istisna: prop ile component'e onEventChange metodu yollarız. ve değişikliği bu metod aracılığı ile manuel isteyebiliriz). bu duruma __yukarıdan-aşağıya (or tek yönlü or top-down or unidirectional) veri akışı (or data flow)__ denir.

# defaultProps

```js
class CustomButton extends React.Component {
  // ...
}

CustomButton.defaultProps = {

  color: 'blue'
};
```

undefined property'leri için kendini koruyan kod yaratıyor. null prop'lar hala null kalmaya devam eder.

# props.children

```js
export default class Panel extends React.Component {

  render() {

    return (

      <div>

        <div className="panel-header">{this.props.title}</div>

        <div className="panel-body">{this.props.children}</div>

      </div>
    );
  }
}
```

Yukarıdaki component tanımlandıktan sonra aşağıdaki gibi kullanılabilir:

```xml
<Panel title="Browse for movies">

  <div>Movie stuff...</div>

  <div>Movie stuff...</div>

  <div>Movie stuff...</div>

</Panel>
```

# propType

asagidaki gibi proptan geçilecek parametrelerin tipi belirleyebiliriz.

```js
class MyComponent extends React.Component {
     ...
}

MyComponent.propTypes = {

  myValue1: PropTypes.array, //yada PropTypes.array.isRequired

  myValue2: PropTypes.bool,

  myValue3: PropTypes.instanceOf(ClassName),

  myValue4: PropTypes.oneOf(['potato', 'turkey'])
}
```

react'ın eski versioyonlarında propsTypes yerine contextTypes kullanılıyordu.

# controlled vs uncontrolled component

A controlled component accepts its current "value" as a prop + callback to change that value. example contolled component:


```jsx
<input value={someValue} onChange={handleChange} />
```

Uncontrolled component:

```jsx
<input onChange={handleChange} />
```

Uncontrolled olan versiyonda two-way binding olmayacak.

controlled component daha çok react'a uygun tarzda yazılmış oluyor.

react event'leri component'in kensininde define etmiş şekilde sayfayı render etmiyor. react arkaplanda her event'i tutuyor ve yönetiyor.  örneğin yukarıdaki örneklerde onChange event'lerini direk html inputumuz içerisinde göremeyiz.

react'ın DOM'u kendisinin yönetmesinden sebep; beklenmedik durumlarla karşılaşabiliriz. örnek:

```jsx
<input
    inputType="text"
    value="try to change this"
/>
```

Yukarıdaki input son kullanıcı tarafından değiştirilemez olur. çünkü react "value" değerini sabitlemiştir. input'a onChnage event'i koysak tetiklenecektir. fakat değer yine değişmeyecektir.

controlled olup olmadığı "value" keyword'ü ile karar veriliyor. tabi component'in onchange tarzı metodu da olmalıdır. onchange'in keywordü önemli diil.

"value" keywordü bazı html objelerinde olmadığı için react render ederken onlara özel olarak ek alanlar/çözümler yaratılmıştır. örnekler:
- input type "text" için; "defaultValue" ile value değeri atayabilmemizi sağlamaktadır.
- textarea'nın normalde (html standartlarında) value değeri yoktur. içerisindeki metin textarea etiketinin dışına yazılır. fakat react'ta value kullanılabilirdir.

react'ın kendi DOMlistener'ları vardır. her event'i, native tarayıcı eventlerinden önce react okur, yada sonra yazılımcının yazdığı fonksiyonlara yollar. Yazılımcının yazdığı metodlara event geldiğinde SyntheticEvent gelir. bu even normal event'i wrap etmiş bir objedir. Eğer tarayıcının event'ine ihtiyacımız var ise, gelen event objesinin içindeki nativeEvent isimli "DOMEvent" objesi kullanılabilir.

React event dönüşlerini de hemen tarayıcıya iletmez. arada yine react metodu olacağı için bazı beklenmedik durumlar ile karşılaşabiliriz. örnek: event metodlarımızdan false döndürmek olay yayılımını (propagation'ı) durdurmayacaktır. bu sebeple stopPropagation() gibi fonksiyonları kullanmamız gerekir. 

# componentwillmount mı? componentdidmount mı? ajax call için uygun?

willmount'ta ajax call yapılabilir. fakat öneri didmount'ta yaılmasıdır. çünkü: 

- client side için sebep: asenkron bir isteğin (örnek ajax call) ne zaman dönüş yapacağı belirsizdir ve değişkendir. biz kodumuzu geliştirirken render metodunu 2 türlü test etmeliyiz: response-data boşken (daha dolmamış) ve doluyken. fakat eğer testlerimiz/kod geliştirmemiz sırasında ajax calları erken dönüş yapıyorsa; biz response-data boşken (daha dolmamış) durumunu test edememiş olabiliriz. buna ihtimal bırakmamak için ajax calları didmount'ta yapmalıyız.

piyasada yazılımcılar; render işlemi başlamadan requesti yapayım düşüncesindeler. böylece render ederken request gitmiş olur diye düşünülüyor.

- server side için sebep: jsp gibi, react ta istenirse suncuda derlenip client tarafa atılabilir. sunucu tarafta derlendiğinde componentwillmount metodu hayat döngüsünde çalıştırılmaz. bu sebeple ajax callarımızı componentdidmount'de çalıştırmalıyız.

# container vs component

component react sınıfıdır. bu sınıftan türetip tekrar kullanılabilir componentlerimizi oluştururuz. cointainer (or container component) ise resmi olmayan bir tanımdır. best practice'lere göre container;

- direk GUI objeleri render etmemeli. container'ın render kısmında, componentler GUI objelerini render etmeli.

- cointainerlar redux/store'lara bağlantı kurup componentlere basmaları gereken bilgileri ve handle metodlarını prop olarak vermelidir.

container'lar sayfa veya sayfanın bölümleri (footer, widget gibi) componentlere denir. componentler ise; textboxlar, buttonlar, textler olarak kullanılır.

yine resmi olmayan tanımlarda; cointainer olmayan componentlere "__Dumb (or çöp yığını) component__" veya "__presentational (or sunumsal) component__" adı verilmektedir.

conitaner'lar "__smart component__" olarakta adlandırılırlar. bazıları container'lara "screen" demeyi de tercih edebiliyor. fakat screen, footer componentlerini kapsamamaktadır. bu sebeple screen demek pek doğru olmayacaktır (bu biraz da projenin yapısına bağlı).

# Higher-Order Components (or HOC)
bu bir pattern'dir.

```jsx
const EnhancedComponent = higherOrderComponent(WrappedComponent);
```

a higher-order component is a function that takes a component and returns a new component.

component'lere prop geçeriz. bu prop'lar ile component'i şekillendirebiliriz. fakat bu prop'lardan bir taneside component de olabilir. yani component'i component'e prop olarak geçebiliriz. bu şekilde component direk olarak component'in bir bölgesinde bizim parametre'de geçtiğimiz component'i gösterebilir/render edebilir. Yani; HOC, component parametresi alan component'lerdir. Fakat pattern'de bunu component diilde fonksiyon olarak yapmamız önerilir.

# fonksiyon call bindings

Metodları çağrırıken metodların içindeki "this" değerinin undefined olmaması için doğru context'in bind edilmesi gerekmektedir. Çünkü JSX'teki html objeleri bizim JS class'ı (component class'ımız oluyor) içindeki fonksiyonu çağırdığında this değeri o sıra js'teki genel context olacaktır. Oysa biz o fonksiyona; JS class'ımızın context'ini geçmek istiyoruz ki; class içerisindedki state'i props'u kullanabilelim. örnek doğru yöntem:

```jsx
class MyComponent extends React.Component {

  constructor(props) {
    ...
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    // eger yukarıda gerçek context'i bind etmezsek bu değer bizim istediğimiz değer olmayacak. (peki hangi değer olacak. bu ayrı bir araştırma konusu.)
    this.setState(...
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

Hiç bind işlemi yapılmaz bu yapılabilir:

```jsx
<button onClick={(e) => this.handleClick(e)}>
  Click me
</button>
```

Fakat bunun 2 dezavantajı var: (kaynak: (source-id: 221) "Passing Arguments to Event Handlers" başlığından hemen önceki cümle )
- her render işleminde bu metod yeni anonim metod generate edecektir
- bu metod html-button'a diilde bir React component'ine (örnek MyButtonComponent) prop olarak aktarılsaydı, her render edilişinde yeni anonim metod geleceği için,  MyButtonComponent tekrardan render edilecekti.

# Fonksiyonel bileşen (or functional component) vs class component (or sınıf bileşen) 

fonksiyonel:

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

aynı işi göre sınıf bileşeni:

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

# React.PureComponent
React.Component'e ile neredeyse tamamen aynıdır. çok ufak farkları vardır. daha hafiftir/performanslıdır.

# Errors
Exception değildir. js'te veya jsx'lerde olan hataları yakalamak için kullanılır. 

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Bir sonraki render'da son çare arayüzünü göstermek için
    // state'i güncelleyin.
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // Hatanızı bir hata bildirimi servisine de yollayabilirsiniz.
    logErrorToMyService(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // İstediğiniz herhangi bir son çare arayüzünü render edebilirsiniz.
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}
```

bu component'imizi bu şekilde kullanabiliriz:

```jsx
<ErrorBoundary>
    <MyWidget />
</ErrorBoundary>
```

Yukarıda ErrorBoundary, sadece child component'lerde hata olursa hatayı catch edebilecektir.

React 16'dan itibaren, bir hata sınırı tarafından yakalanmamış hatalar, tüm React bileşen ağacının devreden çıkmasına neden olacaktır. Bunun sebebi:

- Messenger gibi bir üründe hatalı bir arayüzün görünür kalması, birinin yanlış kişiye mesaj göndermesine neden olabilir.
- bir ödeme uygulamasında yanlış miktarın görüntülenmesi, hiçbir şey görünmemesinden daha kötüdür.

# hook
react 16.8'den gelen bir özelliktir. kullanımı opsiyoneldir. funcitonal componentlere benzer ve ek özellikler sunar. hook, bazı fonksiyonlar sunar. bu fonksiyonlar bazı eventlerde devreye girerler. yani fonksiyonel component'lere ek özellik katarlar. dolayısı ile normal component'lerde kullanılamazlar. direk örnek üzerinden gidersek:

```jsx
import React, { useState } from 'react';

function Example() {
  // "useState" metodu 2 parametre dönüyor:
  //   1- variable'ı tutan değer
  //   2- variable'ı set eden fonksiyon
  // örneğimizde;
  // "count" diyeceğimiz yeni bir state değişkeni tanımlayın
  // "count"'un ilk değeri 0.
  // setCount set ediyor olsun.
  const [count, setCount] = useState(0);

  // bu kod bloğu örneğinde kullanmadığımız, diğer örnek state'lerimiz:
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

setCount fosnkiyonu setState gibi merge işlemi ile uğraşmaz. direk olarak tüm objeyi/state'i replace eder.

"useEffect" componentDidMount + componentDidUpdate + componentWillUnmount metodlarının tek bir metod'da toplanması olarak düşünülebilir. useeffect hem sayfa ilk init olduğunda ve daha sonraki her render işleminde çalışır. örnek:

```js
import React, { useState, useEffect } from 'react';

function Example() {
  
  // some code here (from below example)

  useEffect(() => {
    
    document.title = `You clicked ${count} times`;
  });

  // some code here (from below example)
}

```

useEffect fonksiyonunda return ettiğimiz fonksiyon var ise, component remove olduğunda o fonksiyon çalıştırılır. burada kaynakları serbest bıraktığımız kodlar yazılmalıdır. örnek:


```js
import React, { useState, useEffect } from 'react';

function Example() {

  useEffect(() => {
    
    // any code here

    return () => { 
        // clear resources here! 
    }
  });

}

```

useEffect fonksiyonuna ikinci parametre olarak variable geçebiliriz. bu varible'lar değiştiğinde otomatik olarak useEffect çalışacakır. normalde useEffect sadece componentDidMount + componentDidUpdate + componentWillUnmount'da çalışacaktır. fakat ek olarak bir değer veridğimizde o değerler değiştiğinde de useEffect çalışır.

# custom hook
kendi hook'umuzu yaratabliriz. direk örnek üzerinden gdelim:

```jsx
import React, { useState, useEffect } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log(`The count is ${count}`);
  });

  return (
    <div>
      <p>Count is {count}</p>
      <button
        onClick={() => {
          setCount(count + 1);
        }}
      >
        increase
      </button>
    </div>
  );
}
```

Yukarıda useEffect her renderda çalışır.

eğer bunu yazarsak useEffect sadece bir kere component mount olduğunda çalışacaktır:

```js
useEffect(() => {
    console.log(`The count is ${count}`);
}, []);
```

eğer bunu yaparsak sadece "name" değiştiğinde useEffect çalışacktır:

```js
useEffect(() => {
    console.log(`The count is ${count}`);
}, [name]);
```

Şimdi gelelim custom hook'lara. useEffect sadece çağrıldığı componentin (fonksiyonel coomponentin) render'ını takip eder. dolayısı ile dış dünyadan izoledir. bu şekilde state tutan ve kendince render olan fonksiyonlar yaratabiliriz. bunara hook denir. kendi hook'larımızı "__use__" prefixi ile yazmamız önerilmektedir.

örnek bir custom hook'u inceleyelim:

```jsx
import React from "react";

// "useUserCollection" bizim custom hook'umuz.
// "useUserCollection" MyComponent içerisinde çağrılıyor. bu sebeple buradaki tüm kodlar sanki MyComponent içindeymişçesine çalışacaktır.
// örneğin useUserCollection içindeki useEffect, MyComponent her render olduğunda çalışacaktır.
const useUserCollection = () => {
  const [filter, setFilter] = React.useState("");
  const [userCollection, setUserCollection] = React.useState([]);

  const loadUsers = () => {
    fetch(`https://jsonplaceholder.typicode.com/users?name_like=${filter}`)
      .then(response => response.json())
      .then(json => setUserCollection(json));
  };

  React.useEffect(() => {
    // bu blok MyComponent her render olduğunda çalışacaktır.
    console.log("useEffect of useUserCollection");
  });

  return { userCollection, loadUsers, filter, setFilter };
};

export const MyComponent = () => {
  // useUserCollection custom hook'umuz bize birden fazla obje döndürüyor.
  const { userCollection, loadUsers, filter, setFilter } = useUserCollection();

  // burası componentimizdeki custom businnes logic
  React.useEffect(() => {
    loadUsers();
  }, [filter]);

  return (
    <div>
      <input value={filter} onChange={e => setFilter(e.target.value)} />
      <ul>
        {userCollection.map((user, index) => (
          <li key={index}>{user.name}</li>
        ))}
      </ul>
    </div>
  );
};
```

# react-helmet
node modülüdür. Helmet component'ini sunar. Helmet componenti içinde render edilen html objeleri, header'a koyulurlar (eğer zaten önceden header'da aynı etiketler var ise onları override eder).

örnek:

```jsx
import React from "react";
import {Helmet} from "react-helmet";

class Application extends React.Component {
  render () {
    return (
        <div className="application">
            <Helmet>
                <meta charSet="utf-8" />
                <title>My Title</title>
                <link rel="canonical" href="http://mysite.com/example" />
            </Helmet>
            
            ..
            <input type="text" defaultValue="hello world">
            ..
        </div>
    );
  }
};
```

# ReactNative

Mobil platformlar için geliştirilmiş bir framewowk'tür. Bu çatıda react-js syntax'ı ile (sınıfların isimleri aynı örnek: component) javascript kodları, react-native modülü sayesinde mobil işletim sistemlerinin native kodlarına çevrilmektedir. cordova gibi yapılarda webview üzerinde çalışan arayüz, react-native'de native arayüzde çalışmaktadır.

cordova ile aynı şekilde parse işlemi yapılmaktadır. resource dosyalarında bulunan jsx dosyaları, runtime sırasında native arayüze çevrilmektedir. native componentlerin çevrilmesi az da olsa bir süre almaktadır. bu açıdan bakıldığında cordova ile bir fark yoktur. fakat daha sonra native componentler, webview'dakilerden daha hızlı çalışmaya devam etmektedirler. işte cordovaya göre performans açısından avantaj sağladığı nokta budur.

# JavaScriptCore

jsx'lerin parse işlemi JavaScriptCore ile yapılmaktadır. JavaScriptCore react-native içerisinde gelmekte ve uygulamanın runtime'ına eklenmektedir. JavaScriptCore ile çalışan uygulama native modül geldikçe native tarafta işlem yapmaktadır. örneğin; bir json objesi, yada bir integer native tarafta tutulmamaktadır. ancak ve ancak native modül ihtiyacı (kod satırı native modülü çağrıyorsa) native tarafta işlem gerçekleştirilmektedir. tüm işlemler javascript'te yapılmaktadır + render edilen sayfalar native modüller çağrarak UI render ederler. fakat o native UI'ların eventleri tekrar javascript core'da işlem yaparlar. örneğin onppres'teki i++ kodu javascript'te çalıştırılır.

google-chrome ile debug edilen native uygulama daki JavaScriptCore google-chrome'un içindekidir. google-chrome ile android içerisinde debug edilen uygulama websocker aracılığı ile haberleşmektedir.

# Reconciliation (or uyumlaştırma)
React altyapısı arkaplanda tüm sayfayı render etmez. sadece gerekli alanları render eder. böylece performance artışı sağlar. burada bir hespalama yapılması gereklidir. hangi objelerin update olup olmayacağı algoritmasına Reconciliation denir.

react; __virtual dom (or VDOM)__ oluşturur ve VDOM ile gerçek DOM'u karşılaştırarak Reconciliation yapar.

# Virtual DOM for react native

react native'de html dom'u olmadığından nasıl çalışıyor? react-core içerisindeki yapıda virtual dom görevini gören sistem çok esnek tasarlanmış. programlama dilinden bağımsız. dolayısı ile render'dan return edilen değerler ile varolan view karşılaştırılıyor. bu kaşrılaştırma sonucu sadece değişen kısımlar, o andaki sayfaya uygulanabiliyor.

# react activity

react uygulaması bir activity'dir. manifestte belirttiğimiz (or ana sayfamızı yapmak zorunda diiliz) main-activity'miz ReactActivity'den türemiş bir activity olmalıdır. uygulama bunu çağırdığında react o activity için devreye girecektir.

React yapısı gereği activity dışında android'in Application hayat döngüsünde de bir kaç setupu vardır. Hatta Application'a ek olarak ReactApplication'dan da ekstend işlemi yapmalıyız. (android'in Application hayat döngüsü başka başlıkta anlatılıyor)

# native koda erişme

reat-native'de hem native koddan js'e hemde tersi mümkündür. fakat erişim işlemi asenkrondur.

# native-base

react-native gui elementlerinden extend edip kullanmamızı sağlayan react-native için geliştirilmiş bir modülüdür. yani bir katman daha eklenerek daha fazla nitelik kazandırılmaya çalışılıyor. aynı jsp->jsf katmanları gibi. native-base özellikle yeni event'ler/nitelikler değilde; hem ios hemde android'de kendi platformlarına göre daha oturaklı komponent yaratmak için tema(theme) felsefesinde geliştirilmektedir. 

# react-devtools

bu isim ile web tarayıcıları için eklenti mevcut. bu eklenti tarayıcıya kurulduğunda, tarayıcının developer tool'una ek bir sekme geliyor. bu şekilde sadece react-js debug'ı kolaylaşıyor. normalde sadece web tarayıcısı debug için yeterlidir. fakat bu eklenti inspect element işini COmponent bazlı yapıyor/gösteriyor ve her elemente geçilen prop'ları gösteriyor.

react-devtools ismi aynı olsa da bağımsız bir npm modülüdür. electron tabanlı bu npm modülü, react-devtools eklentini barındırıyor.

# react-native-debugger

react-devtools tabanlı bir debugger. ektra bazı özellikler içeriyor. örnek redux support.

# hot reload vs live reload

live reload'da proje js dosyalarında herhangi bir değişiklik olduğunda emulatordeki uygulamamız otomatik komple restart olur ve state'ini kaybeder.

hot reload'da ise uygulama restart olmaz ve state'ini kaybetmez. fakat değişiklikler RAM'de çalışan uygulamaya yansır. dolayısı ile değişikliği görebilmemiz için ilgili javascript kod bloğunun tekrar işletilmesi yeterli olacaktır.

yukarıdakiler sadece js dosyaları için geçerlidir. diğer dosyalar için uygulamayı tekrardan komple run etmek gerekir.

# npm start -- --reset-cache

sadece "npm start" yaptığımızda js dosyaları bundle halinde hazır hale getirilir ve http üzerinden sunuma açılır. js dosyalarında bir değişiklik olduğunda ise bu bundle baştan sona işlenmez sadece değişiklik olan kısım hemen bundle'de güncellenir. npm start komutu iptal edilip tekrar çalıtırıldığında npm tekrar bundle'yi üretmez. eskisini kullanır. fakat "-- --reset-cache" komutu ile bundle tekrardan sıfırdan üretilir.

"npm start", nodejs sunucusu ayağa kaldırıyor ve aşağıdaki gibi public URL'leri dışarıya açıyor:

http://localhost:8081/index.ios.bundle  //bundle js'i komple veriyor

http://localhost:8081/index.android.bundle

http://localhost:8081/debugger-ui.html //buradaki sayfada webWorker (javascript thread teknolojisi) kullanılıyor. Bu sayfa packager (npm start ile başlatılan uygulama) tarafından sağlanıyor. packager WebSocket teknolojisi ile  ile haberleşiyor.

emulatorde yada cihazda uygulamamızı başlattığımızda, emülatör gidip kodları http://localhost:8081/index.ios.bundle'dan çekmesi gerekir. packager'ın ip:port bilgisini mobil cihazımızın "react dev menu"sünde set etmemiz gerekir.

emülator/cihaz ve debugger(örnek: web tarayıcısı) uygulamaları nodejs sunucusuna; yani "npm start" ile başlattığımız packager'a bağlanıyorlar. artık ikisi(debugger ve emulatör) packager'i proxy olarak kullanarak haberleşiyor. eğer haberleşme başlar ise; web tarayıcısıda index.android.bundle dosyasını kendine packager'dan indiriyor. artık javascript dosyası emulatoröden diil, web tarayıcısının kendisinde koşmaya başlıyor.

# metro bundler
react-native'in bundle hazırlamasını yarayan ve npm modülüdür. "npm start" yaptığımızda bu çalışır.

# ref
ref her componente daha hızlı erişebilmemizi sağlayan bir fonksiyonalite sağlar. react'ta eskiden şu şekilde kullanım vardı:

tanımlama kodu:

> ref="myInput"

erişim için kod:

> this.refs.myInput

Daha sonra bu şekilde kullanım önerilmeye başlanmıştır:

tanımlama kodu:

> ref={(input) => { textInput = input; }}

erişim için kod:

>  this.textInput


# react için bazı best practice'ler/notlar

- bir component çok fazla prop almaya başladığında çok fazla özellşemeye başlamış anlamına gelir. bir süre sonra, her prop için if blokları component içinde artar. bu da karmaşıklığın artmasına sebep olur. bu sebeple; belli bir süre component'ler klonlanarak/kopyalanarak ayrı bir component haline getirilir. çünkü çok özelliştirme abartılırsa, yeni bir component olması gerektiği anlamına gelmektedir.

- bir liste elemanları için birer obje oluşturduğumuzda, listenin eleman sayısına göre/index'e göre key kullanmamamız şarttır. hatalı kullanıma örnek:

```jsx
const todoItems = todos.map((todo, index) =>
  // Bunu yalnızca öğelerinizin sabit ID'leri yoksa yapın
  <li key={index}>
    {todo.text}
  </li>
);
```

key=index yerine key=todo.id kullanmalıyız. çünkü listeye daha sonradan yeni bir eleman eklenirse, liste indexe göre hazırlandığı için hatalar meydana gelecektir. kaynak: (source-id: 222)

"key" react için özel bir keyword'dür. key random da atanmamalıdır. çakışma olursa hata olacaktır. id veya key her zaman atamak zorunda değiliz, fakat listeye elemen eklenecekse, çıkarılacaksa (yani re-render) edilecek ise mutlaka key olmalıdır.

- react componentleri birbirinden extend etmemeleri (class extends yöntemi) önerilir. onun yerine birbirini kapsayan (composite) componentler tercih edilmelidir. önerilen kullanım aşağıdaki gibidir:

```jsx
<MyCustomComponent> <AnotherComponent> ... </AnotherComponent> </MyCustomComponent>
```

"composition over inheritance" başlığında anlatıldığı gibi bu durum react içinde geçerlidir. varolan data sadece proplardan ve kendi state'mizden gelmelidir. diğer datalar bizi ilgilendirmemelidir. eğer react component'lerimiz inheritance olursa, super class'tan gelecek objelerinde variable'larına göre kod yazmamız gerekir.

dikkat edilirse redux kullanırken mapToProps ile redux store'undan ihtiyacımız olan değerleri prop olarak kendi komponent'imize bağlarız. dolayısı ile redux'ın store'u react'tan bağımsız bir yapı olmasına rağmen, props aracılığı ile component içine çektik. böylece focus'umuz sadece props ve state değerleri olmuştur. komplekliği azaltmış oluyoruz.

- tüm hibrit uygulamalarda olduğu gibi Native tarafın UI Thread'i ile Javascript moturunun thread'i farklı olduğundan bu ikisinin haberleşmesi de çok yavaştır. özellikle döngü içinde her seferinde native kod çağırmak çok maliyetlidir.

- react setState içerisinde === kontrolü ile değişiklik olup olmadığına bakar.  eğer değişiklik varsa sadece değişikliğin paramtre olarak yollandığı komponentleri render eder. sebeple bussines logic'ler render içinden kaldırılıp, render metodu içindekiler komponentlere bölünerek, bussinnes logicler oralara taşınmalıdır. bu şekilde istatistiksel olarak daha az kod işlenecektir. zira belki o komponent hiç tekrardan render edilmeyecek ve businnes logic kısmı dahi çalıştırılmayacaktır. fakat businnes logic component dışında olsaydı render metodunun başlaması ila çalıştırılıyor olacaktı.

   örnek;

   ```
   render(){
     if(state.hesaplar == true){
          <div> state.accounts </div>
     }
   } 
   ```

   re-render edildi. if kontrolü yapıldı. oysa hesaplar değerinde hiç değişiklik yoktu. o zaman aşağıdakini yazmak daha mantıklı olacaktır:

   ```
   render(){
      <HesaplarKOmponent value={state.hesaplar} accounts={state.accounts}/>
   } 
   ```

- state'i bir value'ya atayıp değiştirip sonrada o value'yu state'e set etmek yanlış. aşağıdaki örnek yanlış:
   ```
   var x = this.state.x;

   x.z.push("foo"); // z is a list

   this.setState({x:x});
   ```

   burada olabilecek sorunlar: 

     - react setState metodunu işletirken state'i değişmemiş sanabilir. çünkü içini biz zaten değiştirdik (o anda ilgili tüm componentShouldUpdate gibi metodları incelemek gerekir) 

     - paralel bir thread state'i kullanıyor/değiştiriyor olabilir. state'i elle değiştirmemiz bir çakışmaya yol açabilir.

  bu sebeple bunun yerine Object.assign kullanıp obje klonlanmalıdır. listeler içinse [].catcat([ newElement1, newElement2 ]) kullanmalıyız.

- React render veya içindeki farklı bir component'i render edip etmeyeceğine karar vermek için deep comparison yapıyor. yukarıdaki notta state'i elle değiştirmekten bahsettik. eğer elle değiştirseydik ve hemen ardından setstate çağırsaydık bu bizim zaten dezavantajımıza olabilirdi. çünkü Immutability react'ta çoğu zaman avantaj sağlıyor. çünkü genelde state'in içinden bir eleman değiştirildiğinde zaten component'in render olması gerekecek. fakat react önce statein tümünü dolaşarak buna karar veriyor. fakat react dolaşırken, daha az dolaşmasını sağlamalıyız. bu sebeple en tepedeki bir objenin klonunu o obje yerine yerleştirdiğimizde, react direk olarak en tepeden kontrol etmeye başlayacağı için değişikliği görecek ve render işlemine hemen başlayacak. yani react framework'ünün compare işlemini kısaltmış olacağız. tabi bu her zaman geçerli olan bir durum diil. örneğin; 

   state = {x, y} olsun. render metodunuzun içinde sadece Y'yi kullanan 100 adet component olsun. 1 adet componentte Y içindeki A değerini kullansın. sadece A yı değiştirmek istersek, object assaign ile Y'yi komple yeni obje olarak clonlayacağımızı için 100+1=101 adet component tekrar render olacaktır. oysa sadece Y.A yı değiştirseydik, sadece 1 komponent render olacaktır. yani object assaign her zaman avantaj sağlamayabilir. 

- loading bar

  paraleleden işlem yapılırken loading bar gösterilir.

  ```jsx
  render(){

   if(state.loading){

      <LoadingBar>

   } else {

      <SCREEN>
   }
  }
  ```

  yerine;

  ```jsx
  render(){
      <LoadingBar hidden=state.loading>
      <SCREEN>
  }
  ```

  yapılmalıdır. çünkü state.loading değiştiğinde sadece zaten render olmuş bir bar hide edilecektir. diğer türlü state.loading değiştiğinde tüm sayfa render edilecek.

- render metodu içinde businnes logic hiç olmamalı. render'ın görevi sadece sayfayı oluşturmaktır. logic'lerle ilgilenmek farklı bir görev.

- render metodu içinde anonim metod olmamalı. çünkü render'ın sürekli çağrılacağı düşünülerek uygulama tasarlanmalı. anonim metodlar runtime sırasında oluştururlur. bu da zaman kaybı yaratır. anonim metod yerine; önceden bir kere metod oluşturulmalı ve o metod kullanılmalıdır.

  aslında bu kural genel olarak herşey için geçerli fakat genelde her taraftaki anonim metodları sabit metod olarak ayarlamak kodun daha kötü okunmasına sebep oluyor. buna normal koşullarda tölerans gösterebiliyoruz. fakar render metodu sürekli çalışacağı için burada bu konuda tölerans göstermemek gerekiyor.

# "react-native link" komutu
/root/node_modules/ dizini altında native pltaform bağımlı kütüphanaler olabilir. burada bulunan kütüphanelerin /root/ios/ ve /root/android/ altındaki projelere import edilebilmesi için bu komut kullanılır. istenirse komutsuz manuel de import yapılabilir.

# react-native-cli vs react-native
react-native-cli komut satırından react-native projesi oluşturma gibi komtuları yerien getirmek için yapılmış, ilgili projenin dependency'lerinde olmak zorunda olmayan bir node modülüdür.

react-native ise react-native'in runtime'da çalıştırması gereken bir node modülüdür.

# react vs react-dom vs react-native
react-native çıkmadan önce sadece reactj vardı. reactjs, react paketi ile dağıtılıyordu. react-native çıkışı ile birlikte "react" paketi her platform için "react-core" paket oldu. web development yapanlar react-dom'u, mobile geliştiricileri is react-native'i de package.json'a eklemelidirler.

# RNPM (or react native package manager)
eskiden kullanılan fakat artık react kütüphanesinin içine entegre edilen node modülüdür. komut satırından paket kurulumları, link işlemlerini yapabilmemizi sağlıyordu.

# react dizin yapısı

- / - root dizini

- /android - gradle root projesi. burası android studio için proje dizini. eclipse için workspace dizini.

- /android/settings.gradle - burada npm içindeki modullerin native java kodlarının dizinleri mevcut. bu şekilde her proje IDE tarafından workspace'te görülebilir olacaktır. bu sebeple android studio açıldığında bir sürü proje görünmektedir.

- /android/app - android studio için android modül dizini. eclipse için android proje dizini.

- /android/app/build.gradle - dependencies kısmında compile('com.facebook.react') ile jar'lar direk gradle networkünden indirilmektedir. yine dependencies kısmında "compile project(':react-native-code-push')" satırları mevcut. bu projeler bi üst dizindeki settings.gradle'da workspace'e tanıtılmıştı.

- /android/app/src/main/java - java kodları

- /android/app/src/main/AndroidManifest.xml

- /android/app/build/.../index.android.bundle - bütün /app dizinindeki js dosyaları burada tek dosya haline getiriliyor ve apk içine taşınıyor. android runtime'da bu dosyayı okuyor. 

- /ios

- /app - react javascript kodları ve kaynak dosyaları

- /index.android.js - android projesinde başlayacak olan ilk sayfa (yeni react init'le gelmiyor)

- /index.ios.js - ios projesinde başlayacak olan ilk sayfa (yeni react init'le gelmiyor)

- /index.js - ilk açılacak dosya

- /package.json - libs

- /node_modules - npm yöneticisinin dosyaları

# create-react-app

https://github.com/facebook/create-react-app reposundan dağıtılan, bir reactjs projesi oluşturup ayağa kaldırmamızı yarayan node-modülüdür. proje ilk kurulduğunda sadece 3 bağımlılık vardır:

```json
//package.json file
"dependencies": {
  "react": "^16.11.0",
  "react-dom": "^16.11.0",
  "react-scripts": "3.2.0"
},
"scripts": {
  "start": "react-scripts start",
  "build": "react-scripts build",
  "test": "react-scripts test",
  "eject": "react-scripts eject"
},
```

react-scripts modülü diğer tüm işleyişi halledecek script'lerimizi içerir: node server'ı kaldırabilir ve dışarıya projemizi web tarayıcısı üzerinden açabilir, projedeki değişiklikleri otomatik takip edip hot reloading yapabilir, ES kodlarını eski sürümlere göre build eder, productione ve dev ortamlarına göre derleme yapabilir...

# https://github.com/react-boilerplate/react-boilerplate
bu boilerplate hem create-react-app'in yaptığını yapıyor, hemde proje içindeki dosyaları da oluşturuyor. yani; her component, container, redux ve saga, i18n için gerekli tüm dosyaları da oluşturuyor.
