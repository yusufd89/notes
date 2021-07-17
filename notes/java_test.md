############################

############################
# JAVA TEST
############################

############################

# RestTemplate 
asagidaki gibi kullanımı olan rest client'tır. spring-web modülü içinde gelir.

```java
RestTemplate restTemplate = new RestTemplate();

People people = restTemplate.getForObject("http://google.com/people", People.class);

log.info(people.toString());
```

# TestRestTemplate
Bu sınıf RestTemplate'ten extend etmez fakat RestTemplate'i private olarak kendi içinde bulundurur. neredeyse tüm metodları RestTemplate'teki metodları direk çağırır. yani RestTemplate'i wrap eder. fakat ekstradan testleri kolaylaştırmak amaçlı bazı metodlar içerir. örnek: 

- basic auth için password ve username'i veririz, artık her istekte bunları header'da yollar.

- Constructor with HttpClientOption sunuyor. böylece options'ları constructor'da geçebiliyoruz.

Aynı zamanda TestRestTemplate exception fırlatmaz. onun yerine bazı noktalarda Assert metodları kullanır yada kod çalışmaya devam eder. böylece testlerimizde try-catch bloklarımızın sayısı azalır.

TestRestTemplate kesinlikle sadece test'ler için kullanılmalıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# java'da assert kavramı

türkçe kelime anlamı: öne sürmek, idda etmek.

assert programlama dünyasında kullanılan genel bir mantıktır. assert java'da anahtar bir kelimedir. bu yüzden bir metod gibi kullanışı (syntax'ı) yoktur. java 1.4 ile gelmiştir. örnek kullanımı şu şekildedir: asssert( 3 == myNumber ); eger kod runtime sırasında bu satıra geldiyse ve condition false ise; satır AssertionError fırlatacaktır. eger condition true ise; kod hicbir sey yokmus gibi devam edecektir.

assert syntax'ı 2 şkilde kullanılır:

> assert ( 3 == myNumber) : "error: number is not 3" ;

ve

> assert ( 3 == myNumber);

condition sağlanmaz ise sağ taraftaki blok toString'e çevrilir ve AssertionError içerisine yazılır.

java da bir uygulama başlatırken assert keywordlu satırlar devre dışıdır. yani hiç çalıştırılmaz. bunu enable etmek için java uygulamasına en başta parametre geçmek gerekli. istege baglı olarak assertleri sadece belirli paketlerde enable yapabilir.

# assert kütüphaneleri

bazı kütüphaneler (junit gibi) assert metodları sunmaktadır. bu metodlar bildiğimiz java sınıflarıdır. özel bir syntax olma durumu söz konusu değillerdir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# JUnit
test sınıfları verilecek aşağıdaki şekilde çağrılabilir:

```java
JUnitCore junit = new JUnitCore();
Result result = junit.run(testClasses);
```

Fakat IDE'lerdeki junit eklentisi @test annotation'ları içeren metodların sınıflarını otomatik olarak çağırmaktadır.

# junit 4 vs 5
5 inci sürüm ile büyük değişiklikler oldu.

# modülerlik
junit 5, 3 temel parçadan oluşuyor:
- JUnit Platform: API (programatik çağrılabilşmesi için interface'ler(API'ler) burada)
- JUnit Jupiter: API implementasyonu. sadece junit5 annotation'larını çağrıyor.
- JUnit Vintage: JUnit 3 and JUnit 4 kodlarını çalıştırabilmek için gerekli API implementasyonu.

Her implementeasyon (jupiter, vintage...), "Platform" modülündeki "TestEngine" class'ını implemente eder. kaynak: (source-id: 181)

# launcher
JUnit 5 ile; Launcher kavramı geldi. "Launcher" programatik olarak testleri class'larda arayabiliyor, filtreleyebiliyor ve yürütebiliyor. Launcher'ın programatik olarak çağrılıyor dedik, işte bu API; "JUnit Platform Launcher API" olarak isimlendiriliyor ve artifact-id'si: "junit-platform-launcher".

# junit 4 integration to 5
eğer runtime'da junit-vintage-engine varsa; junit-4 annotation'ları otomatik olarak launcher tarafından bulunur ve execute edilir. hiçbir ek ayara gerek yoktur. kaynak: (source-id: 182) "3.1. Running JUnit 4 Tests on the JUnit Platform" başlığı.

Eğer junit4'ten tamamen geçilmek isteniyor ise buradakiler yapılmalıdır: kaynak: (source-id: 182) "3.2. Migration Tips" başlığı.

# TestEngine
JUnit 5 ile gelen bir kavramdır. Şu anda iki farklı TestEngine var:
- junit-jupiter-engine
- junit-vintage-engine

Her test engine implementasyonu "junit-platform-engine" paketindeki interface'leri implemente etmelidir.

## annotations
| purpose of annotation                                 | junit 4      | junit 5      |
|------------------------------------------------------|--------------|--------------|
| Declare a test method                                | @Test        | @Test        |
| Execute before all test methods in the current class | @BeforeClass | @BeforeAll   |
| Execute after all test methods in the current class  | @AfterClass  | @AfterAll    |
| Execute before each test method                      | @Before      | @BeforeEach  |
| Execute after each test method                       | @After       | @AfterEach   |
| Disable a test method / class                        | @Ignore      | @Disabled    |
| Test factory for dynamic tests                       | NA           | @TestFactory |
| Nested tests                                         | NA           | @Nested      |
| Tagging and filtering                                | @Category    | @Tag         |
| Register custom extensions                           | NA           | @ExtendWith  | 

## min java
Junit 4 min java 5 isterken, junit 5, min java 8 istemektedir.

## test suite'ler

junit 4:

```java
import org.junit.runner.RunWith;
import org.junit.runners.Suite;
 
@RunWith(Suite.class)
@Suite.SuiteClasses({
        ExceptionTest.class,
        TimeoutTest.class
})
public class JUnit4Example
{
}
```

junit 5:

```java
import org.junit.platform.runner.JUnitPlatform;
import org.junit.platform.suite.api.SelectPackages;
import org.junit.runner.RunWith;
 
@RunWith(JUnitPlatform.class)
@SelectPackages("ExceptionTest.class", "TimeoutTest.class")
public class JUnit5Example
{
}
```

# junit 5 örnek kod

```java
junit 5 örnek test:

import org.junit.jupiter.api.AfterAll;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Disabled;
import org.junit.jupiter.api.Tag;
import org.junit.jupiter.api.Test;
 
import com.howtodoinjava.junit5.examples.Calculator;
 
public class AppTest {
     
    @BeforeAll
    static void setup(){
        System.out.println("@BeforeAll executed");
    }
     
    @BeforeEach
    void setupThis(){
        System.out.println("@BeforeEach executed");
    }
     
    @Tag("DEV")
    @Test
    void testCalcOne()
    {
        System.out.println("======TEST ONE EXECUTED=======");
        Assertions.assertEquals( 4 , Calculator.add(2, 2));
    }
     
    @Tag("PROD")
    @Disabled
    @Test
    void testCalcTwo()
    {
        System.out.println("======TEST TWO EXECUTED=======");
        Assertions.assertEquals( 6 , Calculator.add(2, 4));
    }
     
    @AfterEach
    void tearThis(){
        System.out.println("@AfterEach executed");
    }
     
    @AfterAll
    static void tear(){
        System.out.println("@AfterAll executed");
    }
}
```

```java
@RunWith(JUnitPlatform.class)
@SelectPackages("com.test.examples") //yada @SelectClasses( com.test.examples.ClassA.class )
@IncludePackages("com.test.example.packageB")
@ExcludeTags("PROD")
public class JUnit5TestSuiteExample
{
}
```

# JBehave

Java için BDD test sürecini işletmek için gerekli kütüphane. Temel olarak öncelikle; test için yapılacak işlemler story dosyalarına belirli formatlarda yazılıyor. Daha sonra Java içerisinde bu dosyalardaki her satıra (işleme) tekabül eden Java metodları yazılıyor. Örneğin;

story dosyasının bir satırında:

Sayfa "google.com" ‘dayken "lütfen aranacak kelimeyi yazın" yazacak.

java sınıfında:

```java
@When(Sayfa $URL ‘dayken $PRINTED_TEXT yazacak.)
public void checkWhatSiteHasPrinted(String URL, String PRINTED_TEXT){

     //do the test here
}
```

Daha sonra JBehave configürasyonları (çıktı rapor türü formatı gibi) yapılır. JBehave daha sonra story'leri run eder ve rapor çıktılarını istenilen dizine oluşturur.

JBehave kendi içinde JUnit'e depend eder. JBehave kendi içinde JUnit testlerini çağırır. Bu çağrılan junit-test story dosyalarını okur ve bunları işletir.

# testcontainers
birçok programlama dili için açık kaynaklı test kütüphanesidir. container'ları programatik ayağa kaldırmamızı sağlar. bu şekilde temel amaç test'lerden önce ilgili testin, container içinde koşmasını sağlamaktır.

isteğe bağlı; junit ile entegreli çalışabilir. bunun çin ekstra lib eklemek gerekli: group-id:org.testcontainers package-id:junit-jupiter.

```java
@Testcontainers
class MyTestcontainersTests {

     // will be shared between test methods
    @Container
    private static final MySQLContainer MY_SQL_CONTAINER = new MySQLContainer();

     // will be started before and stopped after each test method
    @Container
    private PostgreSQLContainer postgresqlContainer = new PostgreSQLContainer()
                                                              .withDatabaseName("foo")
                                                              .withUsername("foo")
                                                              .withPassword("secret");

    @Test
    void test() {
  
        String mySqlUrl = MySQLContainer.getJdbcUrl();

        assertTrue(MY_SQL_CONTAINER.isRunning());
        assertTrue(postgresqlContainer.isRunning());
    }
}
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# spring test

# @RunWith(SpringJUnit4ClassRunner.class)
JUnit spring'in özellikleri ile açılmalıdır. aksi durumda spring özellikleri çalışmaz (yani injection'lar, bean'ler özelliklerini kaybeder. normal sınıf olarak kullanımda kalırlar.). SpringRunner.class parametresi de SpringJUnit4ClassRunner'a referans ettiği için tamamiyle aynı işi görüyor.

Bunun yerine junit 5 ile artık "@ExtendWith" kullanıyoruz. Fakat geriye uyumluluk için @RunWith hala kullanılabiliyor.

# @ContextConfiguration(locations = {...})
ApplicationContext'in belirlenmesi için yapılıyor. parametre olarak xml dosyasının path'i verilebilir, yada @Configuration sınıfı/sınıfları verilebilir. Her @Configuration içerisinde @ComponentScan yapıp, sadece ayağa kaldıracağımız bean'lerin paket isimlerini verebiliriz. Böylece tüm spring uygulaması ayağa kalkmaz.

# @SpringBootTest
Eğer Junt testi içinde @Configuration kullanılmamışsa, "/src/main/* (test olmayan paketler)" arasında @SpringBootConfiguration arar ve spring context'i ayağa kaldırır. böylece bean'ler test süresince kullanılabilir olur.

SpringJUnit4ClassRunner (veya SpringRunner) sadece bean özelliklerini açar, fakat application context'te bean olmadığından pek bir işe yarayamaz. bu sebeple SpringRunner ve SpringBootTest genelde birlikte kullanılır.

@SpringBootApplication içerisinde zaten @EnableAutoConfiguration vardır.

@SpringBootTest default olarak tek başına spring server'ı (wen ortamı kısmını) ayağa kaldırmaz. kaynak: (source-id: 184) "25.3. Testing Spring Boot Applications" başlığı.

Web ortamı oluşturmak için @SpringBootTest'e parametre geçmek gerekli:

```java
@SpringBootTest(args = "--app.test=one")
```

@SpringBootTest, webEnvironment parametresi alabilir:

```java
@SpringBootTest(webEnvironment.MOCK)
```

webEnvironment aşağıdaki değerleri sunmaktadır:

- # MOCK (Default)
    ApplicationContext'i kaldırır fakat mock bir web environment'i oluşturur. yani gerçek bir server ayağa kalkmaz. Mock controller'lar olacağı için @AutoConfigureMockMvc (reactive olamayan server'lara bağlanmak için) yada @AutoConfigureWebTestClient (reactive olan server'lara bağlanmak için) gibi annotation'larla kullanılması önerilir.

    eğer claspath'te web dependency'leri yok ise; normal ApplicationContext'i init eder.

- # RANDOM_PORT
    Gerçek server'ı uygulamayı ayağa kaldırır. Rastegele bir port ile dışarıya açar.

- # DEFINED_PORT
    Gerçek server'ı uygulamayı ayağa kaldırır. port default port yada application.yml'de verilen porttur.

- # NONE
    ApplicationContext'i hiç web ortamlarını ignore ederek ayağa kaldırır.

If your test is @Transactional, it rolls back the transaction at the end of each test method by default. However, if you are using RANDOM_PORT or DEFINED_PORT which provides a real servlet environment, the HTTP client and server run in separate threads and, for that reason, they are separate transactions. Any transaction initiated on the server does not roll back in this case. 

# @WebMvcTest
@WebMvcTest aşağıdaki iki annotation'u devreye sokar: 

  - __@AutoConfigureWebMvc__

    sadece @Controller'ları ayağa kaldıracak şekilde spring context'i ayağa kaldırır. bu şekilde testlerin başlama hızı daha yüksektir. çünkü sistemin sadece bir kısmı ayağa kalkar.

  - __@AutoConfigureMockMvc__

    MockMvc bean'ini inject edebilmemiz sağlar. web slicing testingde server ayaa kalkmaz. dolayısı ile controller'lar normal-standart yntemlerle çağrılamaz. ancak bu işi "MockMvc" objesi yapabilir. MockMvc artık client api'mizdir.

Yukarıdaki iki annotation bilgilerinden yola çıkarak şunu söyleyebiliriz: eğer testlerimize @AutoConfigureWebMvc ve @SpringBootTest yazarsak (@AutoConfigureWebMvc yazılmamışsa) server full ayağa kalkar ve yine testlerimiz mockmvc ile yapabiliriz.

sadece 1 adet controller'ı ayağa kaldırmak için:

```java
@WebMvcTest(HomeController.class)
```

@WebMvcTest test örneği:

```java
@RunWith(SpringRunner.class)
@WebMvcTest(UserVehicleController.class)
public class UserVehicleControllerTests {

    @Autowired
    private MockMvc mvc;

    @MockBean // package: org.springframework.boot.test.mock.mockito
    private UserVehicleService userVehicleService;

    @Test
    public void testExample() throws Exception {
        given(this.userVehicleService.getVehicleDetails("sboot"))
                .willReturn(new VehicleDetails("Honda", "Civic"));
        this.mvc.perform(get("/sboot/vehicle").accept(MediaType.TEXT_PLAIN))
                .andExpect(status().isOk()).andExpect(content().string("Honda Civic"));
    }
}
```

bu tarz testlere "__slicing test__ (slice kelime anlamı: dilim)" denir. çünkü sadece sistemin bir kısmı kaldırırılır ve o kısımlar test edilir. bu test tipi, unit test'in bir türevidir.

slicing test için spring boot'ta bu annotation'lar sunulmaktadır:

__@WebMvcTest__ - for testing the controller layer
__@JsonTest__ - for testing the JSON marshalling and unmarshalling
__@DataJpaTest__ - for testing the repository layer
__@RestClientTests__ - for testing REST clients

# @DataJpaTest
full auto-configuration yapmayıp, sadece JPA ortamını ayağa kaldırıyor.

her test metodu sonrası işlemler geri alınır.

repo testleri entity ilişkilerinin doğru kurulup kurulmadığının ve özel yazılan query'lerin düzgün çalışıp çalışmadığını görebilmek için yapılır.

```java
@RunWith(SpringRunner.class)
@DataJpaTest
public class CityRepositoryTest {

    @Autowired
    private CityRepository repository;

    @Test
    public void should_find_all_customers() {

        Iterable<City> cities = repository.findAll();

        assertThat(cities).hasSize(10);
    }
}
```

@DataJpaTest, __TestEntityManager__ autowired edilebilmesini sağlar. TestEntityManager, EntityManager'i wrap etmez. ona alternatiftir. test için uygun olan metodları barındırır ve bazı EntityManager metodlarını barındırmaz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# mockito
java kitaplığıdır
- metodlardan istediğimiz değerler dönmesini sağlamaktadır
- bunun yanında bir metoda kaç kez girildiğini tespit edebilmekte
- bir metod hangi parametre ile çağrıldığını görebilmekteyiz

# @Mock
mockito annotation'udur. İlgili nesnenin instance'sını oluşturmaz. onun yerine mock bir obje oluşturur.

asagidaki kullanım:

```java
@Mock
MyService myservice;
```

Bununla ayni işi görmektedir:

```java
MyService myservice = Mockito.mock(MyService.class);
```

Eğer annotation kullanılırsa tüm testlerden önce, annotation'un bulunduğu sınıfta asagidaki komutun bir kerelik çalıştırılması şarttır:

```java
MockitoAnnotations.initMocks(this);
```

Mockito, sadece mock olan instance'ların return değerlerini değiştirebilir. yani "new Person()" diyerek oluşturduğumuz bir sınıfın "run()" metodunu çağırdığımızda return değerini değiştiremez.

# @InjectMocks
Test edeceğimiz sınıfı @InjectMocks ile instance'ını oluştururuz. fakat test edeceğimiz sınıfın içindeki dependency'leri @Mock ile aynı test-class'ında tanımlarız. örnek:

```java
public class ApplicationTest 
{
    @InjectMocks
    MyService myService;

    // "aClassInsideMyService" MyService içerisinde kullanılan bir sınıf olsun.
    @Mock
    AClassInsideMyService aClassInsideMyService;
    
    // aynı şekilde "anotherClassInsideMyService" MyService içerisinde kullanılan bir sınıf olsun.
    @Mock
    AnotherClassInsideMyService anotherClassInsideMyService;
     
    @Test
    public void validateTest()
    {
        boolean saved = myService.save("hello");
        assertEquals(true, saved);
    }
}
```

# org.springframework.boot.test.mock.mockito.MockBean
spring içinde gelen bir annotation'dur. sadece mockito kütüphanesi için geliştirilmiştir. mock'lamak istediğimiz componentler bu anotasyonla inject etmeliyiz. spring bean'i olduğu için bu annotation şarttır. eğer mockito içindeki @Mock annotation'ını kullanırsak normal bir class olarak instance yaratmış oluruz.

MockBean'de bir bean instance'ı singleton ise; o zaman o bean'i mock edersek, tüm yazılım sürecinde o bean'i mock etmiş oluruz. yani junit test case'imizde o bean'i çağırmadıysak bile, onu çağıracak olan farklı thread'de bu durumdan etkilenmiş olacaktır. 

# @ExtendWith(MockitoExtension.class)
MockitoJUnitRunner ile aynı görevi görmektedir.

Junit 5 ile artık junit'e extension yazılabiliyor. Mockito'nun MockitoExtension'u bir junit 5 extension'udur. onu devreye almak için aşağıdaki gibi annotation'a eklemek gerekiyor:

```java
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.junit.jupiter.MockitoExtension;

@ExtendWith(MockitoExtension.class)
class MyServiceTest {
  // tests
}
```

İkinci extension ise:

```java
import org.junit.jupiter.api.extension.ExtendWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit.jupiter.SpringExtension;

@ExtendWith(SpringExtension.class)
@ContextConfiguration(classes = {ConfigClass1.class, ConfigClass2.class})
public class UserTest {
  // tests
}
```

SpringExtension, junit 5 ile spring'i aktif etmeyi (yani bean'leri autowire edebilmemizi) sağlıyor. @ContextConfiguration ile spring'in hangi bean'leri ayağa kaldıracağımızı veriyoruz.

# @Rule
JUnit 5 ile gelen bir özelliktir. Extension gibi rule'larda junit akışına özellik katar. MockitoExtension kullanmak istemediğimizde, onun yerine aşağıdaki rule'u aktif etmemiz yeterli olacaktır:

```java
import org.junit.Rule;
import org.mockito.junit.MockitoJUnit;
import org.mockito.junit.MockitoRule;
 
public class ExampleTest {
 
    @Rule
    public MockitoRule rule = MockitoJUnit.rule();
 
    // tests
}
```

# @MockitoJUnitRunner
JUnit'in "runner" özeliği var. runner'lar junit test akışını değiştirebilirler ve junite özellik ekleyebilirler. birçok çeşit runner var. MockitoJUnitRunner bunlardan bir tanesi. MockitoJUnitRunner, @Mock gibi annotation'ların initialize edilmesini sağlıyor. bunu enable etmek için:

```java
import org.mockito.junit.MockitoJUnitRunner;
 
@RunWith(MockitoJUnitRunner.class)
public class ExampleTest {
    // tests
}
```

Mockito 2.2.20 öncesi "org.mockito.runners.MockitoJUnitRunner" sınıfı kullanılırken, bu sınıf artık "org.mockito.junit.MockitoJUnitRunner" olarak belirlendi. junit için geliştirilen sınıflar "org.mockito.junit.*" altına taşındı.

# stubbing
kelime anlamı: ağaç sökmek, saplamak

```java
public Student {

   public Solution solveProblem( Problem problem, int maxTime ){
        // any code here
   }
}
```

olsun. asagidaki kod ile fake data döndürebiliriz:

```java
Solution fakeSolution = new Solution();

fakeSolution.setSolution("Fake solution");

// stubbing the "solveProblem" method
Mockito.when( student.solveProblem( Mockito.any(Problem.class), Mockito.anyInt() ) ).thenReturn(fakeSolution);
```

Yukarıda "student" bir mock instance olmalıdır. yani "new Student()" ile yaratılmış bir sınıf olamaz. mock(Student.class) olmalıdır.

Mockito bir proxy instance'ı yaratıyor. örnek olarak yukarıdaki student'i mock'layalım:

```java
Student student1 = mock(Student.class);
```

student1 artık bir mock sınıftır. 

Mockito proxy based bir kütüphanedir. Proxy olarak araya girer ve bir metod çağrılmadan önce ve sonra işlem yapabilir.

Mock'lama kütüphaneleri genel olarak 2'ye ayrılıyor:
- proxy based (example libs: mockito, EasyMock, jMock)
- bytecode manipulation (example libs: PowerMock)

# Mock vs Spy
Mockito ile mocklanan instance'lar tamamen fake'tir. örnek:

```java
Student student1 = mock(Student.class);
```

student1'den herhangi bir metod gerçekten çağrılmaz. Fakat spy'da öyle diildir. Spy gerçek instance'ın her metodunun önüne ve sonuna metodlar koyabilmemizi sağlar ve arada gerçek metod da çağrılır. örnek:

```java
List list = new LinkedList();
List spy = spy(list);
when(spy).get(0).thenReturn(anyObjectHere);
assertEquals(anyObjectHere, spy.get(0)); // burada gerçek liste elemenı çekilmeye çalışacağından ArrayIndexOutOfBoundException tarzı bir mesaj alırız.
```

Spy'a bazı yerlerde __partial mock__ da denilir.

# Stubbing consecutive calls (iterator-style stubbing)

```java
when(mock.someMethod("1"))
   .thenThrow(new RuntimeException())
   .thenReturn("hello");

//First call: throws runtime exception:
mock.someMethod("1");

//Second call: prints "hello"
System.out.println(mock.someMethod("1"));

//Any consecutive call: prints "hello" as well (last stubbing wins).
System.out.println(mock.someMethod("1"));
```

Farklı bir örnek:

```java
when(mock.someMethod("a"))
   .thenReturn("1")
   .thenReturn("2")
   .thenReturn("3");

// yada yukarıdaki aynı şu şekilde de yazılabilir:
when(mock.someMethod("a"))
   .thenReturn("1", "2", "3")
```

# ArgumentCaptor
bir metoda geçilmiş parametreleri yakalayabilmemizi saglar. örnek:

```java
ArgumentCaptor<Problem> argumentCaptor = ArgumentCaptor.forClass(Problem.class);

Mockito.verify(student).solveProblem(argumentCaptor.capture());

//here do your tests which invokes solveProblem method

//end of the test check the variables passed to solveProblem method

if( argumentCaptor.getValue().getProblemDetails() == "2 + 2 = ?" ){

     //test success

} else {

    throw Exception("Test failed");
}
```

# verify
Asagidaki kod solve problem metodunun 1 kere çağrılıp çağrılmadığını kontrol ediyor.

```java
Mockito.verify(student, new Mockito.Times(1)).solveProblem( any(Problem.class), anyInt());
```

# doAnswer

```java
// normalde AtomicBoolean kullanmaya gerek yok. fakat aşağıda anonym fonksiyon içerisinden bu boolean'ın çağrılması gerekiyor. bu sebeple AtomicBoolean şart.
AtomicBoolean methodInvoked = new AtomicBoolean(false);

doAnswer(invocation -> {

    Message m1 = (Message) (invocation.getArguments()[0]);

    if (methodInvoked.get()) {
        return "message already sent";
    } else {
        methodInvoked.set(true);
        someObject.httpMessageSend(m1);
        return "message sent"
    }
}).when(client).sendMessage(Mockito.any()); // or any "Message" class
```

# answer

```java
when(client.sendMessage(Mockito.any()).thenAnswer(
    new Answer() {
        public Object answer(InvocationOnMock invocation) {
              
              Message m1 = (Message) (invocation.getArguments()[0]);

              if (methodInvoked.get()) {
                  return "message already sent";
              } else {
                  methodInvoked.set(true);
                  someObject.httpMessageSend(m1);
                  return "message sent"
              }
}});
```

# thenReturn vs doReturn vs doAnswer

- thenReturn sadece dönüş parametresini değiştirebiliyor.

- doReturn'de type yoktur. bu sebeple runtime sırasında dönüşün tipine karışmaz. bu önceden bilinmeyen sınıflar/metodlar (örneğin runtime'da yüklenen pluginler) gibi sistemleri test etmek için idealdir. bu nadir bir durum olduğundan; genelde doReturn yerine thenReturn kullanılır. doReturn örneği:

  ```java
  doReturn(true).when(user).getName()); // normalde name string döner, fakat doReturn ile true döndürdük.
  ```

  Fakat doReturn; spy instance'larda gerçek metodun çağrılmasını engeller. bu şekilde spy'larda gerçek metodun çağrılmasını engellemiş oluruz. örnek:

  ```java
  List list = new LinkedList();
  List spyList = spy(list);

  // at this line of code, the real method is calling.
  // this line throws IndexOutOfBoundsException (because the list is yet empty)
  when(spyList.get(0)).thenReturn("foo");

  // You have to use doReturn() for stubbing.
  // if you check below code, you will see that we pass only 'spyList' object as parameter. we don't call the real 'get' method. for that reason doReturn-when and when-thenReturn and some other Mockito methods have different order.
  doReturn("foo").when(spyList).get(0);
  ```

- doAnswer'ın aldığı Answer class'ının answer metodu, mock edilen metoda gelen parametreleri de okuyabilmemizi ve dönüşünü ona göre değiştrebilmemizi sağlıyor.
