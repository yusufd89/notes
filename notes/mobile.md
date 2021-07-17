############################

############################
# MOBILE
############################

############################

# SIM Application Toolkit (or STK)

SIM kartın servis sağlayıcısı tarafından akıllı telefonlara otomatik yüklenen bir yazılımdır. bu uygulama ile müşteri bazı işlemleri gerçekleştirebilir. örneğin türkiyedeki servis sağlayıcılar buradan haber alma servislerini aktifleştirebilmemiz sağlayan grafik arayüzü sunmaktadırlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Dalvik Virtual Machine (DVM)

android altyapısında gömülü olan JVM türevidir.

Android için kodlar .dex uzantılı "Dalvik executable" dosyasına çevrilir. DVM bu dosyaları okur ve işletir. jvm için .class dosyası neyse, dalvik için .dex dosyasıda odur. fakat bir dex dosyası içinde tüm bytecode'ları birden barındırır. .dex dosyası ".exe"'ye denkdir.

Google, JIT ile çalışan DVM yerine artık, AOT çalışan "Android Runtime (ART)"'ı geliştirmeye başlamıştır. Android 4.4 ile birlikte her iki runtime çeşidi de kullanılabilmektedir.

Android NDK (or Native Development Kit) ile bytecode'a çevrilmeden direk makina kodunun işletebildiği kodlar yazılabilmektedir. Uygulamalar daha hızlı çalışabilmektedir. fakat portabilite daha düşüktür.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# AAR

android için jar dosyası düşünülebilir. jar'dan farklı layout gibi resource dosyalarını da barındırmasıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

resmi olarak android dünyası için iki çeşit modul vardır:

- app module

  - Phone & Tablet Module

  - Wear OS Module

  - Android TV Module

  - Glass Module

- library module

  - jar

  - AAR

module'ler içindeki libs dizini private uzaktan indirilen jar'ları kapsamaktadır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# App components

Android dünyasında bir app birçok çeşit tipte dışarıya kendini açabilir. bunlar:

- activity
  
  son kullanıcıya açılacak olan GUI'nin temel sınıfıdır. activity sınıfından türemelidir.

- service
  
  JobScheduler veya Service sınıfından türemesi gereklidir. sürekli arkaplanda işlem yapar. dışarıya bilgi alıp verecek bir API'leri olmaz. dışarıya kapalıdırlar.

- broadcast receiver

  service gibidir fakat arkaplanda isteklere cevap vermek için bekler. istekler gelmezse işlem yapmaz. IPC gibi düşünülebilir.

- content provider

  sistemde kayıtlı dosyaların direk olarak paylaşılmasını sağlar. istediğimiz dosyaları sadece kendi uygulamamızla, istediklerimizide herkesle paylaşabiliriz.

dikkat edilirse listene "app" yok. app sadece bir serviste olabilir. app apk'ya denktir. yukarıdaki listede farklı kavramlar var.

# Intent
türkçe kelime anlamı: amaç

bir app component'inden diğer bir app componet'ine geçilen paramtre nesnesidir. örnek kod:

```java
Intent intent = new Intent(AlarmClock.ACTION_SET_ALARM) # app componentte alınacak aksiyon

.putExtra(AlarmClock.EXTRA_MESSAGE, 3)  # app compoentte bu aksiyon için gerekli dataları yolluyoruz.

.putExtra(AlarmClock.EXTRA_HOUR, 4)

.putExtra(AlarmClock.EXTRA_MINUTES, 0);

startActivity(intent);
```

başka bir örnek:

```java
Intent downloadIntent = new Intent(this, DownloadService.class); # this olunca DownloadService'i bizim uygulamamızdan buluyor

downloadIntent.setData(fileUrl);

startService(downloadIntent);
```

# resources

src ile aynı dizindeki "res" dizinidedir. her resource gruplandırılmıştır.

- /drawable

  resim dosyaları

- /layout

  gui için özel xml dosyaları

- /menu

  context menu, sub menu, options menu gibi yerler için gerekli xml dosyaları

- /values

  hardcode string'lerimiz

- /xml

  varsa kullandığımız xml dosyalarımız

- /font

yukarıdakiler dışında birçok standart dizin var. eğer kendi grubumuzu oluşturacaksak, istersek ekstrasında şunu yapabiliriz:

cihazın özelliği aşağıdaki klasöre denk ise o dizindekiler okunur. eğer denk olan klasörde aranan resource yoksa default klasör okunur.

- /myResouces

  default directory

- /myResouces-hdpi

  bu örnekteki filtre: Screen pixel density (dpi)

- /myResouces-en-large-round

  çok çeşit filtre var. bu örnekteki: language-Screen size-Round screen

# assets

res ile aynı dizin seviyesindedir. assets hiçbir özellik sunmaz. özelliksiz bir dizindir. oysa "res" dizinini birçok özelliği vardır. yukarıdaki gibi cihaz özelliğine göre ilgili kaynağı açar. benzer şekilde her resource'nin otomatik bir id'si yaratılır. bu id ile onu hardcode çekebiliriz.

örneğin /res/values/strings.xml'imizde bu olabilir:

```xml
<resources>

    <string name="hello">Hello</string> #bu java kodundan R.string.hello olarak çağrılabilir.

    <string name="hi">@string/hello</string> #yukarıdaki satıra işaret ediyor

</resources>
```

Yukarıda R (java) sınıfı IDE tarafından otomatik oluşturuluyor.

Ekran bilgileri android cihazlarada bazen runtime'da değişebiliyor. bu gibi durumlarda zaten android activity'yi yeniden oluşturuyor. o yüzden yazılımcı birşey yapmasına gerek kalmıyor.

android sırası ile açık olan activity'nin onSaveInstanceState(), onDestroy(), onCreate() metodlarını çağrıyor.

# activity hayat döngüsü

- ilk açılış sırasına göre:

  - onCreate

  - onStart

  - onResume

    Burada aktiviti son kullanııya açılmış oluyor

- diğer eventler

  - onPause
  
    Kullanıcı bu activity'yi kapatmadan bir popup'a bakarsa, bildirime bakarsa, telefon ekranı kapanırsa ki durumlarda bu metod çağılır. eğer tekrar activitiy'ye focuslanılırsa OnResume çağrılır. burada tek istisna Dialog'dur. dialogda bu metod çağrılmaz.

  - onStop
  
    başka aktivity'ye geçilirse çağrılır. eğer tekrar activity'mize dönülürse sırası ile onRestart, onStart, onResume çağrılır.

  - onDestroy
   
    activity kapatılırsa

# android'in Application hayat döngüsü

Applcation'dan extend ettiğimiz bir sınıfta uygulamamızın kurulduğundan silinmesine kadar olan süreç içindeki bazı eventleri yakalayabiliriz.

# feature

uygulamanın kullandığı donanımsal özellikler manifest dosyasına girilmektedir. required ise eğer o cihazda bu özellik yoksa kurulum gerçekleşmeyecektir. required diilse manifest'e yazmak zorunlu diil, fakat yazmakta fayda olabilir.

```xml
<uses-feature android:name="android.hardware.camera" android:required="false" />
```

# permission

sistemsel yetki istiyorsan "uses-permission" ile manifest dsyasına girilmelidir. örnek:

```xml
<uses-permission android:name="android.permission.INTERNET" /> 
```

başka app componentlerden yararlanacaksak bunun yetkisini "permission" ile istemeliyiz. örnek:

```xml
<permission android:name="com.example.project.DEBIT_ACCT" />
```

android gizlilik için önemsiz yetkileri son kullanıcıya hiçbir zaman bildirmemektedir. 

android 6+ sürümlerde artık marketten kurulumlarda hiçbir şey son kullanıcıya bildirilmemektedir. artık run-time sırasında java kodu ile yetki isteği yapılmaktadır.

# support versions

- min sdk

  en düşük desteklenen android sürümü

- target sdk

  spesifik bir örnekten gidersek; android 6 ile permissionExcepiton'lar geldi. biz bu sınıfı IDE'de görmek istiyorsak; target sdk'yı min 6 tutmalıyız.

- compile sdk

  sadece derleme aşamasında kullanılacak sdk versiyonu. genelde target'a eşittir. yada daha güncel derleyici ile kullanmak isteyebiliriz diye yükseltebilir. çünkü güncel compile sdk'ları kullanırsak, bi ihtimal apk'mız daha güncel android'ler ile daha uyumlu çalışabilir. çünkü güncel api'ler ufak değişiklikler isteyerek bizim sürüm yükseltmeden daha güncel android sürümlerine destek verebilmemizi sağlayacaktır.

- buildToolsVersion

  bu ise sdk içinde gelen toll'un versiyon numarasıdır.

bu kurala uyulmak zorundadır: min <= target <= compile 

buid.gradle ve manifest dosyasında da aynı versiyon definition'ları mevcut. android manifest'teki proje bazlı IDE'nin ayarları set edebilmesi için ayarlanmıştır. gradle varken, gradle her zaman manifest'leri override eder.

# app identifiers

android manifest'teki "package" ve build gradle'da "applicationId" birbirinden bağımsız.

applicationId son kullancı tarafından görülebiliyor ve kolayca değiştirilebiliyor. fakat manifest'teki packgeName'i son kullanıcı göremiyor ve değiştirmek için proje yapısında birçok değişikliği pararlene yapmayı gerektiriyor. fakat applicaitonId değiştirilirse, google play uygulamayı farklı olarak tanımlıyor.

build gradle'da:

```java
android {

    defaultConfig {

        applicationId "com.example.myapp"

    }

    flavorDimensions "api", "mode" #bizim belirlediğimiz kelimeler

    productFlavors {

        free {

            dimension "mode" #yukarıda belirlediğimiz kelimelerden biri

            applicationIdSuffix ".free"

        }

        pro {

            dimension "mode"

            applicationIdSuffix ".pro"
        }

        minApi23 {

            dimension "api"

            minSdkVersion 23

            versionCode 20000  + android.defaultConfig.versionCode

            versionNameSuffix "-minApi23"

        }

        minApi21 {

           dimension "api"

           minSdkVersion 21

           versionCode 10000  + android.defaultConfig.versionCode

           versionNameSuffix "-minApi21"
        }
    }

    buildTypes {
        debug {
            applicationIdSuffix ".debug"
        }

        release {
            applicationIdSuffix ".release"
        }
    }
}
```

build tiplerine göre applicationID mizi değiştirebiliriz. şöyle bir app id'miz olabilir:

> com.example.myapp.free.minApi21.debug

eğer applicationId'miz yoksa android-sdk derlemsinde packageName applicationId olarak alınır.

res dosyalarının otomatik oluşturulduğu R sınıfı IDE tarafından packageName paket ismi altında oluşturuluyor. bu sebeple paket ismi değişince R'yi import eden sınıflarımızın import satırlarını da değiştirmemiz gerekiyor.

SDK apk build işlemini tamamladığında packageName'i en son adımda applcaitonId ile değiştiriyor. apk'nın içine bakıldığında bu görülebilir. 

# manifest

örnek:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"

    package="com.albarakaapp"

    android:versionCode="1"  #son kullanıcıya gösterilmez. her defasında 1 arttırmak gerekir.

    android:versionName="1.0"> #son kullaıcıya gösterilir. her defasında 1 arttırmak iyidir.

    <uses-permission android:name="android.permission.INTERNET"/>

    <permission android:name="com.albarakaapp.permission.C2D_MESSAGE"/>

    <application android:name=".MainApplication" android:allowBackup="true" android:label="@string/app_name" android:icon="@mipmap/ic_launcher" android:theme="@style/AppTheme">

        <activity android:name=".SplashActivity" android:theme="@style/AppTheme" >

            <intent-filter>

                <action android:name="android.intent.action.MAIN"/>

                <category android:name="android.intent.category.LAUNCHER"/>

            </intent-filter>

        </activity>

        <activity android:name=".MainActivity" android:theme="@style/AppTheme" android:label="@string/app_name" android:configChanges="keyboard|keyboardHidden|orientation|screenSize" android:windowSoftInputMode="adjustResize" android:exported="true"/>

        <meta-data android:name="com.google.android.geo.API_KEY" android:value="AIzaSyCtSShMdfDn-RlPE5cgEVdl1QnTmVWNNnU"/>

        <receiver

            android:name="com.pushnotification.GcmBroadcastReceiver"

            android:permission="com.google.android.c2dm.permission.SEND" >

            <intent-filter>

                <action android:name="com.google.android.c2dm.intent.RECEIVE" />

                <category android:name="your.package.name" />

            </intent-filter>

        </receiver>

        <service

            android:name="com.pushnotification.GcmIntentService"

            android:exported="false" >

            <intent-filter>

                <action android:name="com.google.android.c2dm.intent.RECEIVE" />

            </intent-filter>

        </service>

        <provider

            android:name="android.support.v4.content.FileProvider"

            android:authorities="com.albarakaapp.provider"

            android:grantUriPermissions="true"

            android:exported="false">

            <meta-data

                android:name="android.support.FILE_PROVIDER_PATHS"

                android:resource="@xml/filepaths" />

        </provider>

    </application>

</manifest>
```

Her library-module ve app-module'de manifest olabilir. bu durumda final apk'da bunların birleştirilir. birleştirme işlemi temel olarak, manifestteki tüm verilerin birleştirilmesinden meydana gelir. eğer aynı önem seviyesindeki module'lerde aynı xml tag'inini farklı value'leri var ise; conflict meydana gelir. fakat daha önemli module'de farklı veri varsa önemli olan module'ün bilisi alınır.

önem seviyesi şu şekilde: library < app < 'app built variant'

"app build variant" build.gradle'da belirtilen debug, release, minApi21, demo, free kombinasyonları'dır. buradaki özellikler manifest'tekileri override eder. en yüksek öncelik bunlardadır.

# proguard

apk'nın boyutunu düşürme özellikleri içeriyor. build.gradle'da;

- minifyEnabled

  true yapıldığında proguard özelliği apk içindeki java kodu sınıf/metod isimlerini kısaltıyor ve çağrılmayanları siliyor.

- shrinkResources

  kullanılmayan resource dosyalarını siliyor.

proguard için rule dosyasına bazı rule'lar atanabiliyor. örneğin; bir sınıfın proguard tarafından ignore edebiliriz. yada @Keep metodumuzu ignore etmek istediğimiz sınıfın tepesine atabiliriz. çünkü bazı sınfıları reflection kullanarak çağrıyoruz.

# Multidex

(dex dosyası başka başlıkta anlatılıyor)

android sisteminde dex dosyasının içinde 65bin metoddan fazla sayıda metod bulundurulamıyor. Multidex özelliği apk içindeki class.dex dosyaımızı parçalara bölüyor: classes1.dex, classes2.dex. 

Pre-dexing: java bytecode'un android bytecode'una(.dex'e) çevrilme işlemidir.

bazı library'lerimiz pre-dexing'i desteklemiyor ise; bu library'yi ignore etmeden multidex özelliğinden yararlanamayız.

multidex özelliği için compile dependency'mize Multidex jarını eklemeliyiz. fakat android %+ ile birlikte artık dependency olarak eklememize gerek yok. direk olarak anroid runtime birçok dex dosyasını apk içinden otomatik buluyor.

# UI thread vs main thread

UI thread activity lifecycle'sinde çalışan thread'lerdir. bu thread içerisinde GUI'de değişiklik yapan kodlar çağrılabilir. faat diğer thread'lerimizde GUI işlemi yapamayız. eğer yapmak zorunda kalırsak aşağıdaki kod ile yapabiliriz:

```java
activity_instance.runOnUiThread(new Runnable() {

            @Override

            public void run() {

                // do GUI operations

            }
});
```

Android dünyası için; "UI thread", "main thread" ile eş anlamlıdır.

onClick eventlerimiz'de UI thread sayılmaktadır.

# AsyncTask

Javadaki THread sınıfı andoid UI thread ile etkileşimde değildir. bu sebeple UI işlemlerini zorlaştırır. Android içindeki jvm'de AsyncTask isimli class vardır. bu sınıf android UI thread ile etkileşimli thread açabiliriz. bu şekilde UI işlemleri de yapabiliriz. 

# Android process vs thread

android dünyasında her uygulamadaki her servis ve önyüz aynı process'in altında  thread'lerdenmeydana gelir. fakat geliştirici isterse manifesstte bunların ayrılması için özel bir config yapabiliyor. ayırmamızın avantajı şu olur: eğer bir process memory azlığı sebebi ile OS tarafından kill edilirse, diğer işlemlerimiz devam edebiliyo kalacaktır.

# Toast

türkçe kelime anlamı: Kızarmış ekmek

Android ekranında çıkan native popup objesinin özel ismidir. GUI işlemi olarak sayılır bu sebeple UI thread'de ekrana basılabilir.

```java
Context context = getApplicationContext();

CharSequence text = "Hello toast!";

int duration = Toast.LENGTH_SHORT;

Toast toast = Toast.makeText(context, text, duration);

toast.show();
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Kotlin

JVM/Dalvik üzerinde çalışabilen (yani bytecode'a çevrilebilen) ve Javascript'e çevrilebilen bir programlama dilidir.

2016'da piyasaya tanıtıldı.

Google Android için bu dili resmi olarak desteklemektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Appium

Açık kaynaklı mobil platformlar için test yazılımıdır. Yazılım selenium ile aynı mantıkta çalışıyor. Java ve diğer programlama dili client'ları selenium'dan extend ederek geliştirilmiştir. Aynı selenium'daki gibi driver.findBYId("loginButton").click(); gibi çalışmaktadır.

Selenium sunucusu yerine appium sunucusu mevcuttur. Bu sunucu, appium'da nodejs için module olarak yazılmıştır.

Selenium türemesi olduğu için hybrit uygulamaları da kolayca test edebilmek için kullanılabilir.

# appium-desktop

standartalone bir uygulamadır. içinde embeeded appium sunucusu çalıştırabilmektedir. istenirse de zaten varolan appium sunucusuna ip:port üzerinden bağlanabilmektedir. appium-dekstop uygulaması emulator ekran görüntüsünü gösterip, ekrandaki elementleri inspect edebilmemizi ve inspect ederek seçtiğimiz elementler üzerinde selenium komutları çalıştırmamızı sağlamaktadır. örneğin bi buton seçip tıklamamızı sağlıyor. bu işlemleri appium-desktop uygulması üzerinden yaptığımız için her adımımızı kaydediyor ve selenium java kodu ortaya çıkarıyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Apple paket çıkma

### Sertifika işlemleri

- 1inci adım: "sertifika"

bu sertifika çeşididinin özel bir ismi yoktur.
son kullanma tarihi vardır.
Geliştirici için developer ve Distribution sertifikalarının ikiside gerekli olabilir:

  - Developer sertifikası
  
   uygulamanın test paketi dağıtmasına izin veren sertifika çeşididir.

  - Distribution sertifikası
  
    app store üzerinden dağıtımı için gerekli sertifika çeşididir.

bu sertifkları alabilmesi için kendi kişisel bilgisayarından key üretmesi ve bu key ile request yapması gerekmektedir. request'i yaptığında artık Distribution veya developer sertifikası generate edilmiş olacaktır. bu sertifikayı indirip sisteme tanıtması gerekmektedir.

- 2ici adım: "devices"

burada kullanacak cihazların UDID'leri gerekmektedir. buranın sonunda bir sertifika üretilmez. sadece web arayüzünden yapılan ir tanımlamadır.

- 3üncü adım: "app IDs"

sertifika değildir. sadece web arayüzünden yapılan ir tanımlamadır. oluşturacağımız app id uygulamaya özel olabileceği gibi, genel olarak tüm uygulamalarımızda kullanabileceğimiz şekilde de oluşturulabilir. Ama uygulamaya özel oluşturmadığımız provizyon dosyalarıyla, push notification gibi özellikleri uygulamalarımızda kullanamayız. genel kullanım için app-id yaratılacak ise; bundle-id'ye "com.mycompany.\*" gibi yıldız içeren bir string gelmelidir.

- son adım: "provizyon sertifikası (or team provisioning profile)"

bu sertifikada iki çeşittir: developer veya Distribution. Yukarıdaki tüm adımlardaki bilgilerin kombinasyonları sonucunda bir provizyon sertifikası üretilebilir. bu dosyayı geliştirici kendi kişisel mac'ine tanıtmalıdır.

### Test sistemi

- Test Flight

test ettirmek artık eskisine nazaran daha kolay bir hale getiririldi. yeni sistemin adı test flight'tır.

- ipa

ipa formatı ios için kurulum paketi uzantısıdır.

- test kullanıcı kümesi
  - internal testing
  
    itunes connect hesabı olan veyetki verilmiş kişilerdir.
  
  - external testing
  
    email ile apple hesabı ilişkilendirilmiş kullanıcılara davetiye gönderilir. sadece bu kullanıcılar ipa dosyasını kurabilir. bu kullanıcılar apple telefonlarına test flight uygulamasını kuruyor. orası bir app market gibi çalışıyor. kullanıcıya izin verilmiş tüm test uygulamalarını oradan kurabilip update edebiliyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# windows mobile vs windows phone

windows phone, artık windows mobile olarak isimlendiriliyor. yıllara göre çıkan sürümler aşağıdadır:

- Windows phone 7 sürümü - 2010
- Windows Phone 8 sürümü - 2012
- Windows Phone 8.1 sürümü - 2014
- Windows 10 Mobile sürümü - 2015

windows 10 mobile projesi resmi olarak sonlandırılmıştır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# .nomedia

Android bu dosyayı gördüğü klasörlerdeki media dosyalarını (video, resim...), "galeri" gibi son kullanıcı için geliştirilmiş uygulamalarda göstermemektedir. Örneğin; thumbnail dosyalarının bulunduğu bir dizinde bu dosya olmalıdır. Bu dosyanın içi boştur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Android SDK

Android SDK tamamen kurulumsuz ve IDE'den bağımsızdır.

sadece sdk indirildiğinde

> sdk_root/tools/android.bat sdk

yada

> sdk_root/tools/android.bat avd

komutları ile GUI'ler başlatılabiliyordu. fakat güncel sürümlerde (2017 sonrası) artık sadece komut satırından kullanılabilmektedir. Bu sebeple Google'nin sitesinde SDK tek başına "command line tools" ismi ile geçmektedir. Google "Android Studio" içerisinde GUI barındırmaktadır.

# sdk package details

#### SDK Platform sekmesindekiler:

- google play ürünleri emulatorde birebir aynı davranıyor. çoğu google uygulaması ilk girişte hesap istiyor.

- "google APIs" prefixi içerenler

  google services'in bazı kütüphanelerini de içeriyor.

- "google play" prefixi içerenler

  hem google API's pefixi içerenleri hemde google play uygulamasını yüklü getiriyor.

- images'lerden biri seçilmezse emulatör başlatılamaz.

- INTEL Atom  vs ARM EABI

  intel Atom olanlar intel masaüstü işlemcilerde daha hızlı çalışıyor. oysa ARM EABI her komutu simüle ediyor. bu sebeple arm çok yavaş kalıyor.

- Android SDK Platform

  kütüphanenin jarlarını indiriyor. jar'ların kodlarına bazen bakmak istenebilir. bu durumda ilgili sürümün "sources for android" paketi indirilmelidir. 

#### SDK Tools sekmesindekiler:

- Android SDK Build-Tools

  derleme/apk üretme işlemleri için gerekli paket.

- Android SDK Platform-Tools

  adb komut satırı uygulamaısnı içeriyor.

- Android SDK Tools

  sdk-manager + AVD (or android virtual devices) manager + debugging tools gibi andorid geliştiricisinin ihtiyaç duyduğu tool'ları barındırıyor.

- Android Emulator

- diğeleri...

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Phonegap vs cordova vs ionic

cordova; npm ile kurulabilen, nodejs üzerinde çalışan hibrit mobil uygulaması oluşturmaya yarayan komut satırı tool'udur.

phonegap ise bu tool üzerine kurulan ve ek hizmetler sunan bir framework'tür. cordova'ya göre ek özellikler:

- mobil uygulamaları bulutta paketleyen yapı

- daha zengin komut satırı uygulaması ile proje ayarlamaları daha kolaylaştırıldı

- komut satırı uygulamasına ek olarak GUI içeren biryazılım. bu şekilde uygulamalar kolayca testte (preview) edilebiliyor.

- Test süreçlerini kısaltmak için geliştirme ortamı dependency'lerin daha az olduğu bir işletim sistmeinde test işlemleri kolay ve hızlı bir şekilde yapılabiliyor.

ionic ise yine cordova temelli, phonegap'e benzer ek seçenekler sunan bir tool. cordova'ya göre ek özelliklerin bazıları şunlardır:

- bulutta derleme işlemleri

- hazır notification servisleri

- programlama bilmeden uygulama yapma imkanı

- native UI veren bir hali hazırda temalara sahip olması

- uygulamaların marketten onay almadan, kısmı güncelleme yapabilmeleri

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Airplane mode (or uçak modu or aeroplane mode or flight mode or offline mode)
neyin açık neyin kapalı olacağı, işletim sistemleri/donanımlar ve bunların sürümleri arasında hala farklılıklar var.

Bluetooth, telephony, WiFi, nfc, radio gps disable bırakılıyor. fakat kullanıcı hala airplane mod'dayken zayıf iletişim yollarının bazılarını açabiliyor: nfc, Bluetooth

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Mobil işletim sistemleri

```
Name       Open-source  Kernel    development status   companies supported

Palm OS        no       linux       discontinued          palm

WebOS          yes      linux       discontinued          HP, LG, Palm

MeeGo          yes      linux       discontinued          nokia

Symbian        no        -          discontinued          nokia

Bada           no        -          discontinued          samsung

Firefox OS     yes      linux       discontinued          mozilla

FireOS         no       android     continue              amazon (kindle e-reader cihazları için)

BlackBerry     no       unix-like   continue              BlackBerry (or old-name:Research In Motion or old-name:RIM)

Tizen          yes      linux       continue              samsung

Ubuntu Touch   yes      linux       continue              Canonical

Sailfish       yes      linux       continue
```

- Tizen Şu anda en popüler Samsung Galaxy Gear cihazlarda kullanılıyor. Windows manager olarak, Enlightenment windows manager projesi altında geliştirilen, Enlightenment Foundation Libraries (or EFL) kullanmaktadır.

# Cyanogen OS vs CyanogenMod
"Cyanogen Inc" bu projeyi yürüten firmanın adı. CyanogenMod açık kaynaklı projenin ismi iken, firmalara resmi olarak dağıtılan ticari işletim sisteminin adı Cyanogen OS'dir. AOSP CyanogenMod, Cyanogen OS "Google Android"'e denk gelmektedir.

# Bazı Custom Rom'lar

```
name                         development status    note

OmniROM                      discontinued          sadece açık kaynkalı proje

replicant                    discontinued          sadece açık kaynkalı proje

Paranoid Android             continue              sadece açık kaynkalı proje

CyanogenMod                  discontinued

MUIU                         continue              çok fazla kapalı kaynak kod içeriyor.

Android Open Kang Project    continue              sadece açık kaynaklı kodlar içeriyor.

LineageOS                    continue              CyanogenMod projesi iptal edince community buna forkladı
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# F-Droid

sadece açık kaynaklı uygulamaları barındıran (Google Play'e alternatif) market uygulaması.

# Kies

Samsung'un kendi cihazları için itunes alternatifi uygulamadır. sadece mac ve windows'a yüklenebilmektedir. data backup, photo management, os update gibi birçok işlem yapabilmemizi sağlar.

# ClockworkMod (or CWM or CWMR) Recovery

açık kaynaklı android'ler için geliştirilmiş bir recovery yazılımıdır. yüklendiği zaman, telefondaki stock recovery yazılımın yerine geçmekte ve stock'takine göre bir çok ek özellik sunmaktadır. CWM; SD karttaki zip dosyalarından, cihaza ROM yükleyebilmektedir.

# Team Win Recovery Project (or TWRP)

açık kaynaklı CWM alternatifi (GUI içeren) bir yazılımdır.

# PhilZ Touch

Recovery uygulamasıdır. artık geliştirilmemektedir.

# Heimdall

cross platform çalışabilen, açık kaynaklı Odin alternatifidir. odin'de olduğu gibi sadece samsung cihazlar için çalışmaktadır.

# jailbreaking

sadece ios işletim sistemleri için geçerli olan bir kelime. ios sisteminde root haklarını ele geçirmeye işlemidir. jailbreaking genel bir terimdir. jailbreaking için birçok açık yada kapalı kaynak kod tool vardır.

# AOSP (or Android Open Source Project)

Google'ın android projesinin genel adıdır.

# Boot ROM code (or boot rom)

BIOS/UEFI'ye denk gelmektedir.

Mobil cihazlarda bootloader'ın bulunduğu kısım önceden belirlidir. BU sebeple "Boot ROM code" direk olarak cihazın sürücüsündeki Bootloader'ı çalıştırmaktadır.

# android bootloader

android bootloader şu 3ünü açabilir: recovery (örnek: ClockworkMod), system (işletim sistemini açar), radio (cihazın antenini kontrol etmek amaçlı bir arayüzdür).

Cihaz açıldığında bootloader açılır, fakat bootloader genelde neyi açayım diye arayüzden sormaz. genelde tuş kombinasyonları ile bu 3 seçenekten (bazen daha fazlası olabiliyor) biri seçilmiş oluyor. Örneğin samsung'larda; home+volu-up+power tuşu, bootloader'ı açar ve recovery'yi run etmesini seçer. sadece power tuşu; bootloader'ı açar ve linux'u (android'i) run etmesini seçer.

Diskin /boot bölümünde bootloader dosyaları yer alır.

Qualcomm'un Boot Loader ismi LK (Little Kernel)'dir.

# rom

rom işletim sistemini içeren fiziksel parçanın (disk) içindeki yazılımsal bölüme (partition) verilen isimdir. ROM'un bulunduğu parçaya (diske) normal hdd gibi yazılamadığından, oraya yazılma işlemi "flash" olarak adlandırılmaktadır.

mobil/tablet'ler birer gömülü cihaz olduğundan, içindeki yazılım (burada android oluyor) firmware olarak adlandırılırlar. yani; custom rom yüklediğimizde; ROM'a yeni firmware yüklemiş (flash'lamış) oluruz. diğer bir değiş ile; rom'a yeni rom yüklemiş oluruz. fakat halk arasında bu tabirler farklı kelimelerle anlatılıyor.

ROM içerisinde android'den kalan kısım, "internal storage" olarak son kullanıcı tarafından kullanılmaktadır.

# rooting

android cihazlarda rootlama işlemi admin yetkilerini ele alma olarak adlandırılır. custom rom yükleme  anlama gelmektedir.

# ADB (or Android Debug Bridge)

ADB, erişilen cihazda (wifi, yada usb takılı iken) Android açıkken işlem yapmamızı sağlayan komut satırı uygulamasıdır.

ADB, Android SDK içerisinde gelmektedir.

ADB'ye cevap vermesi için Android işletim sistemi runtime'ında özel bir process olmalıdır. Bazı farklı mode'larda (işletim sistemi açılmamış mode'lar recovery, bootloader gibi), ADB'nin tüm komutlarına olmasada kısmen komutlarını destekleyen yazılımlar çalıştırılıyor. Bu şekilde kısmen ADB komutları çalıştırılabiliyor.

# Fastboot

ADB ile aynı mantıktadır. Fakat asıl amacı; Android çalışmıyorkenki komutları cihazda çalıştırmaktadır. Cihaz fast-boot mode'da çalışıyor denildiğinde, o andaki mode (recovery, bootloader gibi) fastboot komutlarını destekliyor anlamına gelir.

# Odin

Samsung cihazlara ROM flash'lamak için geliştirilmiş kapalı kaynak bir windows uygulamasıdır.

# download mode (or Odin mode)

o andaki mode (recovery, bootloader gibi) Odin uygulamasının komutlarını destekliyor anlamına gelir.

# yalp store

Açık kaynaklı android uygulamasıdır. "Google play services" kurulu olmayan cihazda marketten uygulama indirmeye yarıyor. google hesabı uygulamaya veriliyor. uygulama markete bağlanıp apk'yı indiriyor ve kurulumu son kullanıcıya açıyor.

# Open GAPPS

Google'ın uygulamaları (Gmail, youtube gibi) kapalı kaynaktır ve AOSP'ye dahil edilmez. lisans sebebi ile bazı custom rom'larla (google ile anlaşma yapılmadığı sürece) yüklü gelemez. Açık kaynak community, tüm google uygulamalarını paketleyerek dağıtmaktadır. Bu dağıtılan hazır paketler GAPP diye adlandırırlar. GAPPS paket'inin neler içerdiği burada detaylı yazmaktadır: https://github.com/opengapps/opengapps/wiki/Package-Comparison Bu sayfadan AOSP projesinde hangi uygulamaların dahil olup olmadığı anlaşılamaz. çünkü bazı uygulamalar AOSP içerisinde de vardır. Fakat chromium/chrome gibi dağıtılır. örneğin; keyboard. "AOSP Keyboard" vardır, bide "Google Keyboard".

GAPPS Paket farklılıkları:

- ARM - 64/32 - Intel mimarilerinin kombinasyonları farklı kurulum paketinde.

- Her android sürümü için uygun/ paket dağıtılıyor.

- Yukarıdakilerin kombinasyonu ile dağıtılan paketler:

  - Pico: google uygulamalarının android'de çalışabilmesi için şart olan arkaplan uygulamaları vardır. sadece bunlar yükleniyor. en ufak paket budur.

  - Nano: pico + some apps

  - Micro: Nano + some apps

  - Mini: Micro + some apps

  - Full:  Mini + some apps

  - Stock: nexus telefonlardaki uygulamalar

  - Super: stock + Kalan diğer tüm uygulamalar

  - TVStock: android tvler için ilgili tüm uygulamalar

  - Aroma: "Stock" paketi ile aynı paketleri içeriyor. sadece bir arayüz ile nelerin kurulacağını son kullanıcıya bırakıyor.

# gapps google paketlerini nerden buluyor

google'ın ürünleri kapalı kaynak ve birçoğu markette dahi yayınlanmıyor. Open GAPPS paketleri elde etmek için şu yolu izliyor: google resmi sitesinde nexus ve pixel cihazlar için android'i komple image olarak indirmeye sunuyor. simulatorde ve normal cihaza kurabilmek amaçlı. Open GAPPS bunu simülatorde açık, telefona root yetkilerini açık, apk'ları çekiyor.

# Google Play Services

GAPPS'in tüm paketlerinde olan uygulama. bu uygulama sadece arkaplanda çalışır ve diğer tüm google uygulamaları için zorunludur. Public API'leri mevcuttur. Bunları dışardan farklı uygulamalar kullanabilir. Bu API'lere depend olan uygulamalar google ürünü içermeyen custom rom'larda çalışmayacaktır. Bu sebeple bazı açık kaynaklı uygulamalar (örneğin; microG (or old-name:NOGAPPS)), bazı google API'leri ile aynı paket ismi (java paket isimleri aynı) içeriyor ve aynı API'leri aynı isimlerle alternatif işlem yaparak sağlıyor. Fakat henüz (2017) piyasada bu API'leri karşılayacak stabil uygulamalar mevcut değildir. Bu API'lerin bazıları; location hizmetleri (açık kaynaklılar bu API'yi Apple, Mozilla Location gibi servislere bağlıyor), notification sistemi, google hesabı aracılığı ile OAuth, google analitics, google maps'ten harita ve görüntü hizmetleri almak (açık kaynaklılar bunu openstreetmaps'e bağlıyor).

# com.google.android.googlequicksearchbox

google arama uygulamasının paket id'si. ismi sadece "Google" olarak markette dağıtılmaktadır. bazı kaynaklarda "google app" yada "google app (search)" olarak geçkemktedir.

# Android launcher

windows ve ios'ta henüz bulunmayan ana ekran yöneticisidir. masaüstü işletim sistemlerinde masaüstü yöneticisinin mobildeki karşılığı olarak düşünülebilir. bu yazılım diğer android uygulamaları gibi basitçe kurulabilmekte ve varsayılan olarak belirlenen uygulama ana ekranda açılmaktadır. yüzlerce launcher vardır. aşağıdaki listenin tümü google marketten indirip herhangi bir telefona kurulabiliyor:

- google now launcher (or tr:google asistan launcher)
  
  com.google.android.launcher paket id'li launcher. 

- pixel launcher

  com.google.android.apps.nexuslauncher id'li google'ın pixel serisi telefonlar için geliştirdiği alternatif launcher.

- Samsung TouchWiz Home (or yeni ismi: Samsung Experience)

  com.sec.android.app.launcher paket id'li lanuncher. samsung cihazlarında yüklü geliyor.

- com.benny.openlauncher

  a community launcher

- Facebook Home

  artık geliştirilmeyen facebook'un sosyal medya entegreli launcher'ı.

- Trebuchet

  cyanogenmod launcher (LineageOS projesi ile aynı isimde devam ediyor)

# google now (or tr:Google Asistan)

"google now" siri'ye alternatif bir özelliktir. uygulama diildir, çünkü tek başına kullanılamaz. bu sebeple; googlequicksearchbox içerisinde bulunuyor. 

com.google.android.launcher'in içinde direk bu özellik gelmiyor, fakat com.google.android.launcher, googlequicksearchbox'e bağımlı. benzer şekilde com.google.android.apps.nexuslauncher'da googlequicksearchbox'a bağımlı.

# Google Home

paket id'si: com.google.android.apps.chromecast.app

google'ın speak donanım ürünü. bu cihazı kontrol edebilmek için android ve ios için uygulama mevcut. android'deki uygulamanın adı "google Home". Bu uygulama ek olarak chromecast içinde bazı özellikler içeriyor.

# widget

her android launcher'ın widget desteği yoktur.

# com.google.android.apps.messaging

google'ın sms, mms uygulaması'nın paket id'si. bu uygulama aynı networktekilerin haberleşmesini sağlayan ek özellikler de içeriyor.

# com.android.mms

AOSP'ye dahil olan sms ve mms uygulaması.

# com.android.documentsui

bir uygulamanın file manager ile dosya seçtimek istemesiyle açılacak olan pencere için gerekli uygulamanın paket id'si. uygulama ismi sadece "Files" diye geçiyor.

# com.android.settings

settings uygulamasının id'si.

# paket id'leri

com.android.* : AOSP projesi içine dhail olan açık kaynaklı uygulamalar.

com.sec.* : samsung'un uygulamaları

com.google.android.# : google'nin kapalı kaynak uygulamaları

# Xposed Framework

Açık kaynkalı bu proje, rootlu android'lerde değişiklik yapmayı sağlıyor. bu şekilde custom rom kurmadan sadece root yetkisini alarakta birçok cusotm romda olan özelliği kullanabiliyoruz. ahtta custom rom kurup ondan olmayan bir özelliği de kullanabiliriz. framework hiçbir yetenek içermiyor. her yetenek onu kullnanan modülleri yüklediğimizde geliyor. framework sistemin dosyalarını değiştirmiyor, sadece RAM üzerinde değişiklik yapıyor. bu sebeple modüllerdenbiri sisteme zarar verirse, çok rahatlıkla devre dışı bırakılabiliyor.

# android one

google donanım geliştiricileri (dağıtıcılar) ile anlaşıyor. dağıtıcılara marketting desteği sağlıyor. telefonun dizaynı konusunda onara destek oluyor. aynı zamanda ve en önemlisi dağıtıcıya android OS un kurulması çin teknik destek sağlıyor. bazı telefon modlleri "android one" projesi kapsamında bu şekilde piyasaya sürülüyor. amaç dağıtıcının maliyetini düşürmek ve piyasada ucuz android sunmak. google bu şekilde kendi pazarını da arttıyor. bu telefonlarda stock android yüklü geliyor.

# nexus

android yüklü mobil/tablet cihazlar serisinin ismidir. "android one" projesine alternatiftir. fakat burada google işin daha büyük bir kısmını üstlenir ve daha yüksek fiyatlı telefonlar için çalışmalar yapılmaktadır.

# Nexus One

ilk çıkarılan nexus cihazının modeli.

# pixel

android yüklü mobil/tablet cihazlar serisinin ismidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# android version history

| name               | version number | linux kernel version         | release date       | api level |
|--------------------|----------------|------------------------------|--------------------|-----------|
| Astroid            | 1.0            | 2.1                          | September 23, 2008 | 1         |
| Petit Four         | 1.1            | 2.6                          | February 9, 2009   | 2         |
| Cupcake            | 1.5            | 2.6.27                       | April 27, 2009     | 3         |
| Donut              | 1.6            | 2.6.29                       | September 15, 2009 | 4         |
| Eclair             | 2.0 – 2.1      | 2.6.29                       | October 26, 2009   | 5 – 7     |
| Froyo              | 2.2 – 2.2.3    | 2.6.32                       | May 20, 2010       | 8         |
| Gingerbread        | 2.3 – 2.3.7    | 2.6.35                       | December 6, 2010   | 9 – 10    |
| Honeycomb          | 3.0 – 3.2.6    | 2.6.36                       | February 22, 2011  | 11 – 13   |
| Ice Cream Sandwich | 4.0 – 4.0.4    | 3.0.1                        | October 18, 2011   | 14 – 15   |
| Jelly Bean         | 4.1 – 4.3.1    | 3.0.31 - 3.4.39              | July 9, 2012       | 16 – 18   |
| KitKat             | 4.4 – 4.4.4    | 3.10                         | October 31, 2013   | 19 – 20   |
| Lollipop           | 5.0 – 5.1.1    | 3.16                         | November 12, 2014  | 21 – 22   |
| Marshmallow        | 6.0 – 6.0.1    | 3.18                         | October 5, 2015    | 23        |
| Nougat             | 7.0 – 7.1.2    | 4.4                          | August 22, 2016    | 24 – 25   |
| Oreo               | 8.0 – 8.1      | 4.10                         | August 21, 2017    | 26 – 27   |
| Pie                | 9.0            | 4.4.107, 4.9.84, and 4.14.42 | August 6, 2018     | 28        |
| Q                  | 10.0           |                              | September 3, 2019  | 29        |
|                    | 11             |                              | September 8, 2020  | 30        |

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# WebView

# Android için webview

Android activity içerisinde buttonview, textview kullanırmış gibi webviewda kullanımı aynıdır:

```java
WebView myWebView = (WebView) findViewById(R.id.webview);

WebSettings webSettings = myWebView.getSettings();

webSettings.setJavaScriptEnabled(true);
```

Eğer tüm sayfayı kaplaması isteniyor ise activity'nin full screen olması, varsa webview'ın borderları kapatılmalı ve webview'ın bulunduğu layout tüm sayfayı kaplamalıdır. bu şekilde bir tarayıcıymış gibi kullanılabilir.

# Android üzerinde custom component

Android platformu hem fully hemde basic olarak 2 farklı çeşit custom element (android'de view) yaratmamıza olanak sunuyor. basit custom element, hali hazırda varolan bir elementin sınıfını extend ederek, metotlarını override ederek, yada yeni metod ekleyerek, yeni element yaratmamıza olanak sağlıyor. Fully custom elementlerde ise, çizim gibi metodları da kullanıp tümüyle sıfırdan yeni bir element yaratmamıza izin veriyor.

# Android System Webview

paket id: com.google.android.webview

Android artık webview'ı ayrı bir apk olarak marketten sunmakta (çoğu telefonda default yüklü gelmektedir). google chrome tarayıcısının yüklü olması ile alakasız bir durum. Android eskiden, default tarayıcısının kodlarına dayalı bir webview kullanıyordu. 5. sürüm ve sonrasında Chromium (chrome) tabanlı bir webview'a geçildi. sistemde birden fazla webview olabilir. yazılımcılar webview kullanmak istediklerinde import ettikleri kütüphane'ye göre hangi webview'a erişeceklerine karar verirler. chrome öncesi olan webview kütüphanesi: com.android.webview

# WebChromeClient vs WebViewClient

"Android Webview"ın içinde olan/kullanılan iki variable'dır. bunlar dışarıda set edilebilir şekilde ayarlanmışlardır. WebChromeClient içerdiği metodlar, ilgili webview'ın loading bar, alert/popup, page title, favicons gibi HTML DOM'u dışında kalan işlerin eventlerinde çağrılırlar. WebViewClient ise; HTML DOM eventlerinde çağrılırlar. örneğin; sayfa yüklendiğinde, safya url'ye istek yaptığında gibi...

# firefox based webview

Firefox'un webview'ı için stabil bir çalışma yok.

# cordova web view

CordovaWebView custom bir webview'dır ve eklentiler ile bilgi alışverişi yapabilecek şekilde tasarlanmıştır. İşletim sistemindeki default webview'dan extends edilip özellikler eklenmiştir.

# Android default browser

"com.android.browser" paket id'si ile kullanılan browser'dır. resmi olarak özel bir ismi olmadığı için "stock browser", "android browser", "webkit bundled browser" gibi isimlerle anılmaktadır.

# Google Chrome (paket id: com.android.chrome) varken neden hala android default tarayıcısı yüklü geliştiriliyor?

- android 4.4 sonrası nexus serili telefonlarda google chrome tarayıcısı default gelmektedir. fakat diğer donanım firmaları google ürünlerine bağımlılık yaratmak istemediğinden chrome'u yüklü sunmamaktadırlar.

- uygulamaların webview'ları buna bağlı olduğundan, chrome yüklü gelirse uygulamaların çalışması da riskli olacağından kimse chrome yüklü getirmiyor.

- "Android default browser" daha hafif olduğunda bazı üreticiler kötü donanımlarında hala bu tarayıcıyı kullanmaktadır.

- donanım firmaları lisansı gereği default tarafıcıya pach ekleyebilirken, chrome'a ekleyemiyorlar. bu sebeple default tarayıcı yüklü getiriliyor.

# Apple WebView

Apple üzerinde custom webview kullanma olanağı yok. Apple'ın kendi webview'ı (yeni adı:WKWebView, old-name:UIWebView) kullanılmalıdır.

# Crosswalk

Proje cordova projesinden türemiştir. Birçok ek özellik sunar. Temel özelliği android'lerde chromium tarayıcısına dayalı webview yaratıp, uygulamamının apk'sına gömmeleri ve her android cihazda aynı kalmasıdır. fakat android 5'ten sonra, android default webview chrome ‘a dayalı olacağı için, crosswalk projesinin bu avantajı ortadan kalkmıştır.

avantajları ise;

- hala chrome webview'ın android'lerde dafeult yüklü gelmemesi

- chrome sürümünün her android sistmeinde değişik olması. crosswalk, kendi içinde kütüphane olarak barındırıyor webvieweı. yazılımcı fix olarak bir sürüm seçebiliyor.

# Android Custom Tabs

Android uygulaması içerisinde yeni bir tarayıcı penceresi açmadan kullanıcıya tarayıcı kullandırıtılır. Tüm ekranı kaplaması şarttır. Fakat tarayıcı özelleştirilebilir. Önceden menüleri ve işlevleri set edilebilir gibi. Eğer işletim sisteminde o anda google chrome tarayıcısı kurulu değil ise; uygulama yeni bir pnecerede default tarayıcıyı açacaktır.

# Safari View Controller

Android Custom Tabs'ın Apple'daki versiyonu.

# Apple üzerinde diğer tarayıcılar

Apple üzerinde yüklenen tarayıcılar apple politikası sebebi ile apple tarayıcısının rendering mekanizmasını kullanmak zorundadır.

# cordova-plugin-inappbrowser Eklentisi

Bu eklenti ile; bir url, kullanılan webview'da yada sistemin default tarayıcısını açarak gidilmesini sağlıyor. Aynı zamanda ek olarak şu özelliği de sunuyor: yeni bir dialog (popup dialog'daki dialog altyapısı ile ufak bir blok) içinde; geri, ileri, dur butonları ve  bir de webview elementi olan layout yaratıyor (java kodu ile) yaratıyor. bu dışarıdan bakıldığında Android Custom Tabs ve Safari View Controller'a çok benziyor. bu dialog içerisinde bir web sitesi açılmasını sağlıyor.

# samsung internet

paket id: com.sec.android.app.sbrowser

samsung kendi telefonlarında 2017 öncesi stock android browser'ı yüklü getiriyordu. 2017 ve sonrasında chromium tabanlı kendi tarayıcısnı yüklü getirdi ve marketten indirmeye açtı.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

Android partitions:

- /boot

  cihaz başlatıldığında başlayan bölüm.

- /system

  android işletim sisteminin bulunduğu bölüm. ek olarak sadece stock uygulamalar buradadır. stock uygulamalar şuralarda olabilir /system/app, /system/priv-app.

- /recovery

  alternatif bot bölümüdür.

- /data/app

  user'ın kurduğu apk içindeki dosyalar buradadır. fabrika ayarlarına dönüldüğünde bu dizin silinir.

- /data/data/package_name

  her uygulama için private internal storage. android artık sd-card'lara da data atabilmemizi sağlıyor. bu durumda datalar şurada oluyor: /sd-card-dir/Android/data/package_name

  $HOME dizini her uygulama için farklıdır ve bu dizindeki kendi private alanını gösterir. çünkü android'de her app bir kullanıcıya aittir.

  private internal storage her uygulama silindiğinde otomatik siliniyor fakat external ve internal storage'deki dosyalar silinmiyor.

  Eğer bir uygulamayı silersek otomatik olarak /sd-card-dir/Android/data/package_name'de siliniyor. bu sebeple silinmemesini istediğimiz dosyaları /sd-card-dir dizinine taşımalıyız. 

- /cache
  
  android'in cache için ayrılına kısmıdır. wipe etmekte hiç zarar olmaz. "Internal cache" olarak geçer. uygulamalar private olarak buraya dosya atabilir. buraya geçici dosyalar atılmalıdır. silindiğinde son kullanıcıya boş yer kalmış olur. bu tarz dataları (örneğin "video önbelleği") gibi buraya atmak gerekir.

- /misc

  cihazın sistemsel dosyalarını içermektedir. buradaki dosyalar cihazın işleyişini etkileyebilir.

- /sdcard

  sd kart alanıdır. bazı cihazlar internal ve external sd kart sunmaktadır. bu gibi durumlarda internal sd kart /sdcard alanında mount edilir. external'lar ise /sdcard/sd yada /sdcard2 gibi alanlarda mount edilir. fakat bu mount pointler cihazdan cihaza değişiklik gösterebilmektedir.

- /sd-ext

  bazı rom'lar /data alanı sığmaması durumu için, herhangi bir başka bölümü /data klasörü olarak kullanabilir. bu yeni ek alan /sd-ext alanıdır.

not: her cihaz ve sürüm kombinasyonu farklı dizinleri  amaçla kullanabilir. bu sebeple kesin bir standart yoktur. örneğin; /mnt/sdcard/ dizini bazı telefonlarda telefonun kendi hafızasına kısayol olarak set edilmiş.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Push Notifications

bir uygulama tüm mobil sistemlerde istediği anda kod akışından son kullanıcıya "notification" gösterebilir. "push notification"lar ise bu durumdan farklıdır.

# Push notification işleyişi:

push notification için işletim sistemi sunucuları devreye girer:

- androidler; google cloud messaging (or GCM or yeni adı: Firebase Cloud Messaging)

- ioslar; Apple Push Notification Service (or APNS)

- windows'lar (masaüstü ve mobil); Windows Push Notification Service (or WNS)

Mobil uygulama açıldığı zaman, kendi işletim sistemi ile temasa geçerek push notification sistemine o uygulama için register olur. işletim sistemi, uygulamaya bir register-id verir. mobil uygulama, bu register-id'yi, mobil uygulamanın özel olarak yazması gereken sunucuya gönderir. sunucu artık o mobil uggulama kullanıcısına bir mesaj (push notification) göndermek itediğinde; direk olarak işletim sistmei sunucusuna (apns, wpns gibi) register-id ile birlikte yollayacağı mesja bilgisini gönderir. işletim sistemi sunucusu bu mesajı mobil uygulamaya yollar.

# Amazon Simple Notification Service (or SNS)

Amazon firmasının, Amazon Web Services (AWS) isimli hizmet gruplarından bir tanesidir. Bazı mobil işletim sistemleri için push hizmeti sunmaktadır. Tek bir API ile tüm desteklenen platformlara mobil bildirim gönderilebilmektedir. Sadece push değil, aynı zamanda sms ve email de gönderebiliyor. SNS varolan mobil işletim sisteminin push mekanizmasından yararlanıyor. Sadece bu sistmein önüne bir katman yazılmış durumda. BU şekilde tek bir API ile tüm platformlara bildirim gönderebiliyor. Yani API üzerinden bir mesaj gönderdiğimizde, SNS bu mesajı APNS, WNS gibi API'lere yönlendiriyor.

# Push notification bulut hizmetleri yerine MQTT kullanımı

MQTT açık kaynaklı standartlaşmış bir protokoldür. MQTT, Facebook messenger gibi uygulamalarca tercih edilmektedir. MQTT için bazı sebepler:

- Mobil işletim sisteminin bulut hizmetleri her zaman ayakta olmayabiliyor

- Mobil işletim sisteminin bulut hizmetleri yapılan notification sayısına limit koyabiliyor (or ek ücret talep edebiliyor)

- mobil işletim sistemi bulut servisi her zaman cihaza mesajı çok geç gönderebiliyor (özellikle anlık mesaj uygulamaları için büyük sıkıntı)

- mobil işletim sistemi bulut hizmeti custom rom'larda yüklü olmayabiliyor

- mqtt daha hafif ve hızlı çalışabiliyor (zira direk soketten bilgiyi gönderiyor. diğer türlü bizim sunucu, mobil bulut hizmetine, mobil bulut hizmeti de cihaza iletimi yapıyor)

# apple'da mqtt kullanma

apple mobil os'larında backgroud processlere izin vermiyor. dolayısı ile; push yerine mqtt kullanmak imkansız. apple yeni sürümlerinde sadece mesjalaşma uygulamalarına yada bazı  kriterlere göre arkaplan processlerine izin vermektedir. bazı kısıtlamalar olsada kullanılabilmektedir.

# MQTT (or Message Queuing Telemetry Transport)

Açık kaynaklı bir protokoldür. bu protokol ile birçok cihaz birbirine toplu mesaj alıp verebilmektedir. Protokol şu şekilde işliyor:

- client, sunucuya bir başlığa (topic) subscribe olmak istediğini söyler.

- artık herhangi bir client bu topic altında bir mesaj bıraktığı zaman, bu sunuya bu topic için kaydolmuş herkese(tüm client'lara) mesaj gider.

- ## topics

başlık standardı zorun değildir. fakat best practice'lere göre şu şekilde kullanılır:

- örnek: 30 numaralı apartmanın, 2inci katındaki oturma salonun sıcaklığındaki değişiklikleri takip etmek için kaydolunacak başlık: 

  > "30/2/oturma/sicaklik"

- yukarıdaki örnekte tüm katlar için değişiklikleri izlemek isteseydik: (single level wildcard)

  > "30/+/oturma/sicaklik"

- yukarıdaki örnekte 2inci kat için tüm odaların tüm sensörlerindeki değişiklikleri izlemek isteseydik: (multi level wildcard)

  > "30/2/#"

- $ kakarteri

  $ karakteri ile başlayan topicler sistem topicleridir. fakat bunlar için belirlenmiş bir standart yoktur. bazı sunucular bu bilgileri client'larla paylaşırken bazıları paylaşmıyor. ama tüm sunucular bu topiclere clientların mesaj bırakmasını engelliyor.

- ## QoS

Mesaj gönderen tarafındaki her mesajın iletim kalitesini (logic'ini) belirlenir.

- QoS 0

  - disconected olmuş clientlara mesaj iletilmez.

  - "fire and forget" mantığı vardır. sunucu bu mesjaı tutmaz. anında herkese iletir ve unutur. bazı sunucular bunu da tutarlar (belli bir süre).

  - her açıdan çok hafiftir.

- QoS 1

  - Mesaj kesin iletilir

  - Mesaj birden fazla kez iletilebilir. bunun sebebi iletildimi kontollerinin sunucu tarafında detaylı yapılmamasıdır.

- QoS 2

  - Mesaj kesin iletilir

  - Mesaj tek sefer iletilir

  - Maksimum trafik harcar

# Paho

açık kaynaklı Client API for MQTT. API, java başta olmak üzere birçok major dil için yazılmıştır. javascript API'si TCP ile sunucuya bağlanamıyor. Bu sebeple javascript websocket'ten yararlanılıyor.

# Mosquitto

açık kaynaklı MQTT sunucusudur. mqtt protokolünde sunucu iletişim için bir aracı olduğu için bu tarz tüm mimarilerde ingilizcede "broker" olarak isimlendirilir. ingilizce "broker" türkçede komisyoncu (or eş anlamlı:simsar) anlamına geliyor. fakat türkçe sözlüklerde "broker" kelimesi mevcut. broker türkçe sözlükte: 'borsa komisyoncusu' olarak geçiyor.

# mqtt-spy

MQTT desktop client app (test amaçlı kullanılır).

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Device Unique Id

aşağıdaki bilgiler güncel versiyon sistemlere göre yazılmıştır. eski versiyonlarda farklı id alma yöntemleri bulunabilir fakat yenilerinde deprecated olmuşlardır.

- ## ios

    - uygulama kendi bir sertifika keychain oluşturarak sisteme kaydedebilir. bunu uygulama, daha sonra tekrar sisteme kurulduğunda okuyabilir. fakat sistem ayarlarına resetlenen bir cihazda bu bilgi yokolacaktır.

    - Identifier for Vendor (IDFV): aynı geliştirici şirket kendi uygulamaları için aynı cihazı görebilir. örneğin facebook ve facebok messenger ortak bir IDFV deeğerini aynı user için görmektedirler.

    - adid (advertisement id): sadece sistem resette ve kullanıcı isteği ile resetleniyor.

    ```
            factory-reset  user-manuel

    keychain      changes      same

    adid          changes      changes

    vendor        changes      same

    openUDID      changes      same
    ```

- ## Android

    - Hat takılamayan cihazlarda IMEI bulunmadığından IMEI numarası tercih edilmemelidir.

    - öneri olarak kullanıcının google hesabına bakılması öneriliyor. Zira kullanıcı telefonu başkasına vermiş olabilir. bu sebeple uygulamalar için önemli olan cihaz değil, cihazı kulllanan kullanıcı olmalıdır.

    - mac adres kullanma yöntemi: android cihazda wifi yada Bluetooth donanımı olmayabilir , olsada bazı donanımlar mac adres döndürecek şekilde tasarlanmayabilir.

    - GSF Android-ID: is generated by the Google Services Framework (GSF). google uygulamaları yüklü olan cihazlarda vardır. fabrika ayarlarında resetlenir.

    - Device Build Fingerprint: OS'un seri numarası/user agent'ı.

    - Google Advertising ID (GAID): kullanıcın istediği zaman resetlenyebileceği unique değerdir.

    - TelephonyManager.getSimSerialNumber(): sim karta bağlı değişen bir değer ve sadece SIM kart varsa geçerli

    - seri numarası android.os.Build.SERIAL: fabrika ayarına dönüşte resetlenmez.

    - TelephonyManager.getDeviceId() fabrika ayarlarına dönüldüğünde bu değer değişmektedir.

    - SSAID (or Android ID) : Secure.getString(getContentResolver(), Secure.ANDROID_ID)); fabrika ayarlarına dönüldüğünde bu değer resetlenmektedir.

- ## desktop operation systems

    Genel olarak uygulamalar bağlı olan donanım'ların ayrı ayrı seri numaralarını kullanarak unique bir bilgi oluşturmaya çalışırlar. genel olarak piyasadaki işletim sistemleri, üzerinde çalışan uygulamalara kendini tanıtmak için tekil bir id vermektedir. fakat yazılımlar genelde HDD seri numarası tercih eder, çünkü işletim sistemi ve kullanıcı bilgilerinin olduğu alan oraya bağlıdır. dolayısı ile o değişmediği sürece, makine sadece güncellenmiş gibi varsayılmaktadır.

    örnek linux'ta /etc/machine-id dosyası bir unique id barındırır. bu değer donanım güncellemelerinde değişmez.

