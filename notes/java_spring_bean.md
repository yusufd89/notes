############################

############################
# JAVA SPRING BEAN
############################

############################

# Spring Bean

- ## Spring IoC container
DI için gereklidir. 2 çeşittir: Bean Factory vs ApplicationContext. ApplicationContext daha gelişmiş özellikler içerir.

  - ### ApplicationContext

    ```java
    ApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");

    HelloWorld objA = (HelloWorld) context.getBean("helloWorld");
    ```

  - ### ClassPathXmlApplicationContext
    classhpath içindeki dizini istiyor

  - ### FileSystemXmlApplicationContext
    full path istiyor

  - ### WebXmlApplicationContext
    tüm uygulamadaki xml'leri load ediyor

  - ### AnnotationConfigApplicationContext
    parametre olarak bir class istiyor. bu sınıfın içinde configürasyonlar oluyor.

  Spring bean'i dışında kalan sınıflar (bean olmayan sınıflar, normal sınıflar) içerisinde bean çeken annotation'lar kullanılamaz. hata alınmasa bile null gelir değerler. örneğin; @autowired ile normal bir sınıfta bir bean sınıfını inject ettik. bu sınıf runtime'da null olur. bean'ler ancak bean'ler tarafından çağrılabilir. yada yukarıdaki gibi context.getBean() metodu ile çağrılabilir.

  Runtime sırasında aynı java uygulamasında birden fazla ApplicationContext olabilir. dolayısı ile context.getBean() metodu ile hangi ApplicationContext'i aldığımıza dikkat etmeliyiz. fakat best practice'lere göre context'e bu şekilde erişmek pek önerilmez.

- ## BeanFactory
ApplicationContext'e alternatif bir kütüphanedir. spring-beans modülü içinde gelir. ApplicationContext, BeanFactory'den daha gelişmiştir ve BeanFactory'nin tüm özelliklerini zaten içerir. BeanFactory daha sadedir. bu sebeple mobil gibi uygulamalarda tercih edilebilir.

- ## Bean Scopes
  - ## singleton
  tüm applicationContext'te tek bir instance olmasını sağlıyor

  - ## prototype
  each injection initializes new object

  - ## request
  each HTTP request. only exist for Web applications.

  - ## session
  each HTTP session. only exist for Web applications.

  - ## global-session
  portletler için session bazlı bean oluşmasını sağlıyor. bu bean normal servlet'ler için kullanılırsa, "session" bean ile aynı mantıkta çalışacaktır.

  - ## websocket
  websocketlerin bağlantısı açık kaldıkça aynı bean sürekli açık kalır

  - ## application
  ServletContext hayat döngüsü boyunca varolan singleton bir obje. bir applicaionContext içerisinde birden fazla ServletContext olabilir.

  Yukarıdaki hazır scope'lar dışında custom scope'ta yaratılabilir.

  bean'lerin ne scope olursa olsun initialize ve destroy sırasında çağrılacak metodları olabilir. bu metodlar beans.xml dosyasında belirtilmek zorundadır.

- ## Bean hayat döngüsü
  sırası ile:

  - bean'e propertieleri set edilir

  - BeanNameAware.setBeanName(String name)

  - BeanFactoryAware.setBeanFactory(BeanFactory beanFactory)

  - ApplicationContextAware.setApplicationContext

  - @PostConstruct yada BeanPostProcessor.postProcessBeforeInitialization()

  - InitializingBean.afterPropertiesSet()

  - a user defined bean init method

  - BeanPostProcessor.postProcessAfterInitialization()

  - bean hazır durumda

  - DisposableBean.destroy()

  - a user defined ben destroy method

  bir örnek üzerinden gidelim:

  X Bean'imizin hayat döngüsüne bir metod ekleyelim: X bean BeanFactoryAware'i implemente eder ve setBeanFactory metodunu override ederse, setBeanFactory otomatik olarak çalışır. aksi durumda bu event atlanır.
  BeanFactoryAware'yi ilgili bean (X) implemente etmeyip aşağıdaki gibi kullanabiliriz. fakat böyle durumlarda aşağıdaki metod tüm bean'ler için çalıştırılmaktadır.

```java
public class MyBeanFactory implements BeanFactoryAware {
 
    private BeanFactory beanFactory;
 
    @Override
    public void setBeanFactory(BeanFactory beanFactory) throws BeansException {
        this.beanFactory = beanFactory;
    }
 
    public void getMyBeanName() {
        MyBeanName myBeanName = beanFactory.getBean(MyBeanName.class);
        System.out.println(beanFactory.isSingleton("myCustomBeanName"));
    }
}
```

- ## bean property

xml tanımı yapılır:

```xml
<bean id="person" class="com.ornek.bean.Person">
      <property name="message1" value="Ahmet" />
</bean>
```

java tarafında artık bean hazırdır. message1 değeri otomatik javaee/spring tarafından doldurulacatır:

```java
public class Person {
   private String message1;
}
```

Yukarıdaki xml tanımını yapmasaydık, java kodumuzun içine annotation atmak zorundaydık.

- ## bean init method

benzer şekilde destroy metodu da belilenebiliyor

```xml
<bean id="myBean" class="..." init-method="myInıtMethod"/>
```

- ## @PostConstruct and @PreDestroy Annotations

JavaEE Annotations standardıdır. bu sebeple annotationlar javax.annotation.\* içerisindedir. bean'lerde initialize ve destroy sirasinda calisacak metodlarun üzerine konulur. beans.xml'de belirtilmemişse, bu annotationlar kullanılabilir.
