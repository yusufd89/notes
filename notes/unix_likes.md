############################

############################
# UNIX-LIKES
############################

############################

# freedesktop.org (or X Desktop Group or XDG)
X window system üzerindeki uygulamalara katkıda bulunan ticari olmayan topluluğun ismidir. Gnome, KDE gibi projelerin büyük destekçilerindendir.

# XDG Base Directory Specification
XDG'nin hangi dizinlerde hangi dataların olacağı standartıdır.

OS üzerinde o anda $HOME user'ı gibi belli standartlar ile dizinler belirlenmiştir. Bu standartlara uyulmak zorunda değildir, fakat standart olduğu için birçok yazlım bu dizinleri tercih eder. örneğin;

$XDG_CONFIG_HOME, çoğunlukla HOME/.config'i işaret eder ve bu dizin sadece ayarları tutar. oysa $XDG_DATA_HOME, çoğunlukla $HOME/.local/share/ i işaret eder ve sadece dataları tutar: örneğin;
- image thumbnails
- email programı/client düşünelim. emaillerimiz "data" da tutulurken, email config ayarlarımız "config" dizininde tutulur.

gibi. bu dizin standartlar sayesinde;

- son kullanıcı ayarlarını bir makinadan diğerine daha rahat taşıyabilir
- son kullanıcı yada sistem enviroment değişkenini değiştirerek confg'lerin başka yerdeymiş gibi gözükmesini sağlayabilir
- HOME dizini gereksiz şişmez. Bazı developer'lar home dizinine gizli dosya tutarak bu maddenin aşılabileceğini söylüyor, fakat birçok kişi (özellikle linux kullanıcıları) gizli dosyaları sürekli görüntülüyor.

$XDG_CONFIG_DIRS bir dizin listesi tutar. $XDG_CONFIG_HOME'a ek olarak hangi dizinlerde config dosyalarını bulabileceğimizi tutar. örnek: /etc/xdg:$HOME/xdg

Specification eğer $XDG_CONFIG_HOME gibi değerler boş ise; default değerleri de belirtmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Window System

İşletim sisteminde GUI (Input Ouput - keyboard, mouse vs dahil) pencerelerin yönetimini sağlayan sistemdir. Tüm sistemi temsil eder. Hangi pencere açık, statüleri ve meta bilgileri burada tutulur. (Aşağıda anlatılan hem sunucu hem client tarafının tümünü temsil eder)

# X Window System (or X)
Piyasada en çok 11'inci sürüm kullnıldığından X11 olarakta isimlendirilmektedir.

Bir Window System'dır.

# Display Server (or Window Server)

Display Server bir sunucudur. Display server pencere meta bilgilerini tutar. Bunları, window manager ile birlikte window system'ın client tarafına sunar. client tarafı birden fazla olabilir. Zira uzaktan aynı makineye bağlanan ve kullanan birileri olabilir. Burada pencerelerin GUI'lerinin dekorasyonu ve işlevlerini window manager sunmaktadır. Sunucu ve client aralarında Telnet kullanarak haberleşirler.

X client her açtığımız uygulama'dır. Bu uygulamalar yetkileri dahilinde diğer uygulamaları görebilirler (ekran görüntüleri alabilir gibi).

Firejail'in x11 sandboxing özelliği firejail'in çalıştırıldığı bilgisyarda yeni bir x-server açıyor. bu x-server bu iki bağımsız yazılmdan biri olabilir: Xpra and Xephyr. RUn eidlmesi istenen GUI uygulamasının client'ı bu sunucuya bağlanıyor.

# X.Org Server

X Window System için sunucu tarafıdır (başka alternatiflerde piyasada mevcuttur). Bazı kaynaklarda kısaltılarak "X server" olarak kullanılıyor. Fakat "X Server" iki anlama da gelebilir: "X.Org Server" kısaltması, yada "X Window System" için sunucu tarafı. "X Window System" için birden fazla sunucu tarafı implementasyonu (yazılımı) olduğu için karışıklığa sebep olabilir.

# mac os display server
__Quartz Compositor__ is the display server and compositing window manager.

X11'den forklanan __XQuartz__ yazılımı, X11 uyumluluğunu sağlamak için kullkanılan yazılımdır.

# $HOME/.Xauthority dosyası

Bu dosya home'a sahip olan user'ın "x.org server"'a eriştiğinde kullandığı session'ın Authentication token'ını saklar. eğer bu dosyaya yazma yetkisi yok ise o user görüntüyü alamaz. bu sebeple sudo ile açılan komutlarda bu sorun yaşanabiliyordu. yine bu sebeple gksudo komutu geliştirildi. 

# Xresources
varsayılan olarak ~/.Xresources veya ~/.Xdefaults dizinindeki tutulan property'lerdir. bu property'ler her program için spesifik yada genel olarak tüm pencerelerin yapısı (rengi, textlerin fontu...) hakkında bilgiler tutar.

# Mir vs Wayland

X çok eski bir altyapıya sahiptir. Bu sebeple X'e alternatif açık kaynaklı projeler geliştirilmiştir.

X'te compositor opsiyonel bir yetenekti. Oysa wayland'da zorunlu bir özelliktir. wayland'da compositor'ün ayrı modül olması mantığı yoktur. display server ve compositor tek bir modül haline getirildi.

# Window Manager

Windows System üzerinde pencerelerin yönetimi (işlevlerini belirleyen: minimize, maximize, always on top, dekorasyonu gibi) sağlayan yazılımdır.

windows manager'ların kurulum paketlerinde gömülü ek uygulamalar ile geldiklerinde neredeyse bir masaüstü yöneticisi(gnome) gibi hizmet verebilmektedirler.

tiplerine göre 4'e ayrılırlar.

- Compositing Window Manager (or compositor)

  - pencereler birbirleri üzerine binebilirler (bu durum overlapping olarak adlandırılır)
  - ek olarak transparan yapabilme gibi birçok özelliğe sahiptirler çünkü her pencere objesini manipüle edebilirler.

  örnekler:

  Compton, sway, Compiz, KWin, Metacity, Mutter, Xfwm, Enlightenment, Xcompmgr, Gala, Muffin

- Stacking (or floating)

  - pencereler birbirleri üzerine binebilirler 
  - pencereleri manipüle etme gibi bir durumları yoktur.

  örnekler:

  2bwm, aewm, AfterStep, amiwm, Blackbox, cwm, Fluxbox, FVWM, IceWM, JWM, Matchbox, mwm, Openbox, Sawfish, twm, Window Maker, eggwm, evilwm, Flwm

- Tiling

  - pencereler birbirleri üzerine binemezler.

  örnekler:

  i3, Ion, ratpoison, wmii, StumpWM, larswm, Qtile, Herbstluftwm, Bspwm, EXWM, howm, Notion, Ratpoison, subtle, sway, way-cooler, WMFS, WMFS2

- dynamic tilling (or dynamic)

  Tiling ve Stacking arasında geçiş yapabilen mod'ları mevcuttur.
 
  örnekler:

  - dwm: 2000 satırı geçmeyen sadece C ile yazılmış kod olacak şekilde tasarlanmaktadır. sadece temel görevleri yerine getirmek için tasarlanmıştır.

  - awesome: dwm türevidir. 2000 satırlık kod limiti bu fork'da aşılmıştır. aynı zamanda lua kullanır.

  - spectrwm, xmonad, catwm, echinus, FrankenWM, Qtile, wmii

# Client-side decoration (or CSD)
windows manager normalde X server'ın görevidir. fakat CSD ile client'lar da artık kendi pencere yapılarını oluşturabiliyor.

bu sistemin tersine __Server-Side Decoration (or SSD)__ denir.

# Masaüstü yöneticisi (or desktop manager)

EN üst seviyeli GUI ortamıdır. Masaüstlerinde sunulacak özellikleri (widget, notification system, simge panelleri, ayarlar sunan yazılımlar, hazır gelen yazılımlar gibi) belirlerler.

Bazı Windows Manager'lar desktop manager olmadan kullanılabilir. Fakat sadece windows system tek başına (window manager olmadan) son kullanıcı için bir işe yaramaz.

# desktop manager'lar:

- budgie: gnome 2'inci sürüme benzer, sıfırdan yazılmış

- KDE Plasma: en gelişmiş DM olma yolundadır

- Gnome: genel olarak kde'ye göre daha hafiftir

- Xfce: genel olarak gnome'a göre daha hafiftir

- LXDE: xfce'ye alternatiftir

- MATE: Gnome'un 2'inci sürümünden devam eden bir akımdır.

- Cinnamon: Gnome'un 3'üncü sürümünden devam eden bir akımdır. gnome shell'e alternatiftir. gnome için kabuktur.

- LXQt: LXDE'nin qt tabanlı türevidir.

- Budgie

- Sugar: cocuklar icin tasarlanan arayüzde çok kısıtılı seçenek sunan masaüstüdür

- Moksha: Enlightment projesinden türemiş, masaüstü yönetici olmaya odaklanmış bir projedir.

- lumina: hafif olmayı amaçlar

- Pantheon: elementary OS için yaratılan proje

- manokwari: gnome üzerine kurulu shell (unity gibi)

- Deepin DE (or DDE)

# KDE Plasma vs KDE

KDE, projenin genel ismidir. KDE; "Plasma masaüstü yöneticisi", "KDE uygulamaları"" ve "KDE kütüphaneleri (frameworks)"" üçlüsünden oluşur. Sonuçta asıl amaç; masaüstü ortamı sunmak olduğu için; KDE; "K Desktop Environment" kelimelerinin kısaltmasından oluşmaktadır.

# KDE Neon

Ubuntu LTS bazlı KDE yüklü gelen, KDE takımı tarafından geliştirilen OS. Kubuntu LTS varken nedenböyle bir OS geliştiriliyor? Çünkü Ubuntu LTS versiynlarında stabilite gereği hiçbir uygulama (masaüstü ymneticiside dahil) her zaman güncellenmez. Güncellensede genelde sadece güvenlik paketleri güncellenir. KDE takımı ise sadece kendi repolarını update edecek şekilde ayarlamıştır Neon içerisinde.

# GNOME Shell vs Unity

Gnome 3 üzerine inşa edilmiş farklı masaüstü yöneticileridir. Unity, Ubuntu tarafından geliştirilmekte, Gnome Shell ise, Gnome takımı tarafından geliştirilmektedir. Bu yüzden gnome-shell, gnome projesinin varsayılan (or referans) masaüstü olmaktadır. Gnome Shell'in eklenti altyapısı mevcuttur.

Gnome, 3'üncü sürümüne kadar tek başına bir masaüstü yöneticisi olarak paketlenip sunulmaktaydı. 3'üncü sürümü ile artık her topluluk/şirket bunun üzerine ek bir kabuk yazarak dağıtmak durumunda kalıyorlar (gnome shell, unity, cinnamnamon gibi).

Bazı işletim sistemleri, gnome 3'ü hala sade (eski haline benzer) olarak gösterebilmektedirler. bunun birkaç yöntemi var:

1- GNOME Flashback (or GNOME Fallback): gnome 3 ile eski görüntüyü sağlamak için bazı modüller devre dışı bırakılıyor ve shell'dekinden farklı bir window manager kullanılıyor. + eski panel kullanılıyor.

2- GNOME Classic (or GNOME Classic (no effects)):  gnome 3.8 sürümü ile resmi olarak; birden fazla eklenti ile eklentiler ile eski görünümü gnome shell üzerine verebiliyor.

Gnome 2'den 3e geçiş sürecinde oturum açma ekranlarında işletim sistemleri kendilerince isimlendirme kullandıkları için karışıklığa sebep olmaktadırlar.

# Ubuntu Gnome

Ubuntu'nun türevi. Masaüstü yöneticisi olarak sadece "Gnome Shell" yüklü gelmektedir.

Ubuntu 18.04 ile artık varsayılan masaüstü Gnome Shell'dir. Ekstra birkaç eklenti yüklü gelmektedir (örnek kısayol panel eklentisi). Bu sebeple Ubuntu Gnome projesine ihtiyaç kalmamış ve proje sonlanmıştır.

# Display manager (or login manager)

işletim sistemi login ekranında çıkan yazılımdır. masaüstü yöneticisin yada sadece pencere yöneticisini başlatmak için görevlidir. komut satırı yada GUI tabanlı olabilirler.

- Console

  - CDM
  - Console TDM
  - Ly
  - nodm

- Graphic

  - Entrance - An EFL based display manager
  - GDM - The GNOME display manager.
  - LightDM - A cross-desktop display manager, can use various front-ends written in any toolkit.
  - LXDM - The LXDE display manager. Can be used independent of the LXDE desktop environment.
  - MDM - used in Linux Mint, a fork of GDM 2.
  - SDDM - The QML-based display manager and successor to KDE4's kdm; recommended for Plasma 5 and LXQt.
  - SLiM - Lightweight and elegant graphical login solution. (discontinued)
  - XDM - The X display manager with support for XDMCP, and host chooser.

# X display manager

Sadece X session'u başlatan yazılımdır (display manager'dır).

# GTK (or old-name:GIMP Toolkit or old-name:GTK+) vs Qt vs Java Swing vs Java AWT

Widget toolkit'lerdir. Penrecelerdeki butonların ve diğer nesnelerin nasıl olacağına ve event'lere karar veren kütüphanelerdir. Window manager ekrana bir pencere açtığında bu kütüphanelerden yararlanır. Doğal olarak; default olarak her window manager'ın yanında bir widget toolkit olmalıdır. Bazı uygulamalar kendi içerisinde widget toolkitleri gömerler (java ile yazılmış bir uygulamanın swing'i kendi içerisinde bulundurması gibi, GIMP'in GTK'yı bulundurması gibi). Böyle durumlarda windows manager o uygulamayı, uygulamanın kendi widget toolkit'i ile açmak zorunda kalır. böyle durumlarda ekranda bazen sıkıntılar yola açabilir. çünkü her pencerede, bir çeşit toolkit aynı anda çalışıyor olur. bir yazılım, esnek tasarlanmış ise birden fazla toolkit ile başlatılabilir.

# Qt

açık kaynaklı bu proje, ağırlıklı olarak C++ üzerinden, QT widget'ları ile uygulama yazılmasını sağlar. Qt projesi, sadece widget toolkit değildir. Aynı zamanda bir IDE (pencere tasarlama modülü içeren) sunmaktadır. QT, sadece GUI için değil, aynı zamanda C++ için veritabanı, matematik gibi bir çok işlevi yerine getiren API'lerde sunmaktadır. Diğer diller C++ kodunu çağırarak yada C++ kodu diğer dilleri çağırarak runtime sırasında çağırarak yada derleme sırasında c++/qt binary'lerini kullanarak işlemleri yapmaktadırlar.

# Remote desktop using X

X sunucuları uzaktan bağlanılmak için gerekli altyapıya sahiptir. X sunucusuna birden fazla client aynı anda istek yapabilir. AYnı kullanıcı oturumu içerisinde dahi birden fazla client istek yapıp cevap alabilir. X sunucularından gelen bu istekleri uzak makinada X client karşılamak zorundadır. X client MS Windowsta olmadığı için uzak makine orada yapılamaz. Fakat Apple cihazlar için apple'ın kütüphane esnekliği ile open source X11 client'ı mevcuttur. Apple makinede x client kurulu ise uzak masaüstü yapılabilir. X org sadece masaüstünü kople değil, uygulama penceresi bazında da uzağa yansıtma yapabilir. Uzak masaüstü kendi masaüstünde uygulama açarmış gibi uygulamayı kullanabilir.

SSH üzerinden uzak masaüstü rahatlıkla yapılabilir. Komut satırından SSH ile username ile login olduktan sonra, komut satırından örneğin firefox yazılır ise, firefox ssh yapılan makinede açılacaktır.

X11'in bu özelliğini kullanmayan diğer uzak bağlantı uygulamaları (örneğin teamviewer), sadece ekranın yada bir bölümünün ekran görüntüsünü çekerek uzak makinaya aktarırlar. Oysa X11'deki olay direk olarak native bir çalışma sergilemektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# apparmor vs selinux
birbirlerine alternatif __Linux kernel security module (or LSM)__'leridir. dosyalara erişimi kısıtlarlar.

"Subject vs Principal vs User" başlığında da anlatıldığı gibi; her security context'inde:

- obje; erişilecek kaynaktır. LSM için: dosya ve dizin.
- subject; objeye erişmek isteyen process'tir. LSM için: OS üzerinde çalışan yazılımlar.

# discretionary access control (or DAC) vs mandatory access control (or MAC)
discretionary kelime anlamı: isteğe bağlı

mandatory kelime anlamı: zorunlu

apparmor ve selinux yüklü olmayan *nix sistemlerde, standart *nix dosya koruması vardır. bu koruma DAC grubuna girer. çünkü DAC dosya sahibinin erişimi isteğe bağlı kısıtlayabildiği kontrol mekanizmalarına denir.

MAC ise; sistem admini tarafından verilen kurallar ile kısıtlama getirilen güvenlik mekanizmalarına denir.

Bu durumda apparmor vs selinux MAC grubundadır. Fakat ek olarak DAC yetenekleri de sunarlar.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# dns ve host ayarları

/etc/resolv.conf dosyasında dns tanımları vardır:

nameserver 8.8.8.8
nameserver 8.8.4.4

Bu dosya birçok yazılım tarafından aynı anda editlemekte ve okunmaktadır. okuyanlar arasında "resolver" uygulaması da vardır.

Herkesin paralel okuması veya buraya yazılması durumuna çözüm getirmek için "resolvconf" yazılımı geliştirildi. diğer tüm uygulamalar (vpn client, network manager...) her dns değişiminde "resolvconf" uygulamasına bilgi göndermesi beklenir. Fakat "resolvconf" yazılımı sonradan geliştirildi. hala onu tanımayan başka yazılımlar var ve bu sebeple "resolvconf" her zaman tam olarak başarıyı sağlayamıyor.

Son kullanıcı resolv.conf dosyasını editlememeli. /etc/network/interfaces dosyasını editlemelidir.

örnek:

```
dns-nameservers 12.34.56.78 12.34.56.79
```

network manager (root olarak çalışan yazılım ve önyüz uygulamaları (önyüz uygulamarına örnek: nmcli, nmtui) asagidaki dns ayarlarını kendice override eder:
- dhcp ayarlarındaki dns'leri
- resolv.conf'taki dns'leri
- /etc/dhcp/dhclient.conf'teki dns'leri

NetworkManager GUI'den son kullanıcının belirlediği ayarları buraya kaydeder:

> /etc/NetworkManager/system-connections/name-of-connection

örnek:

> "/etc/NetworkManager/system-connections/Wired connection 1".

dosya içeriği örneği:

```
[802-3-ethernet]
duplex=full
mac-address=XX:XX:XX:XX:XX:XX

[connection]
id=Wired connection 1
uuid=xxx-xxxxxx-xxxxxx-xxxxxx-xxx
type=802-3-ethernet
timestamp=1385213042

[ipv6]
method=auto

[ipv4]
method=auto
dns=208.67.222.222;
ignore-auto-dns=true
```

Artık tüm network manager gui'leri doğru bilgiyi gösterecektir.

# /etc/hosts

default örnek dosya içeriği:

```
cat /etc/hosts
127.0.0.1	localhost
127.0.1.1	machibe-id

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouter
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# ubuntu-restricted-extras

bu paket ubuntu repolarında duruyor fakat lisans sebepleri gereği ile default yüklü getirilemiyor. içerisinde şunları barındırıyor:

- adobe flash player

- mp3 codec ve diğer codec'ler

- microsoft TrueType core fontları

- icedtea plugin

- unrar

# repositories
Ubuntu'da 4 ana repository var:

| repository name | open source | supported by canonical |
|-----------------|-------------|------------------------|
| main            | yes         | yes                    |
| universe        | yes         | no                     |
| Restricted      | no          | yes                    |
| Multiverse      | no/yes      | no                     |

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# root of linux distros

- debian (deb based)

  - SteamOS (gnome masaüstü de yüklü geliyor. bu şekilde normal linux uygulamaları da çalıştırılıyor.)

  - Raspbian (Raspberry üzerinde çalışması için tasarlanmış. lxde yüklü.)

  - mxLinux (sadece desktop sürümü olan. içerisinde son kullanıcı birçok için paket yüklü geliyor. bu sebeple çok kolay kulanımı var. xfce masaüstünü kullandığı içinde hafif.)

  - kali (or old-name:BackTrack) (güvenlik testleri için geliştirilmiş tool'lar içeriyor)

  - tails (or The Amnesic Incognito Live System) (tüm bağlantılar tor üzerinden yapılır ve gizliliği amaçlar)

  - pardus (tübitak tarafından geliştiriliyor. eskiden pisi paket yöneticisi kullanırdı fakat daha sonradan deb'e geçti.)

  - KNOPPIX (temel amacı live cd ile çalışmak. çok hafif.)

  - ubuntu

    - mint

    - elementary (sadece masaüstü sürümü mevcut. son kullanıcı için kolaylatırılmış ayarlar barındırıyor.)

    - deepin

    - zorin

    - ubuntu studio (ubuntu'nun multimedia uygulamaları yüklü gelen türevi)

- fedora (rpm based)

  - Mandrake

  - Red Hat Enterprise Linux (or RHEL) (ticari)

    - centOS (or Community Enterprise Operating System) (community yönetiyor. RHEL'den hiçbir farkı yok. RHEL gibi bir ticari OS'u temel aldığı için üstünede paketler free olunca herkes tarafından özellikle tercih sebebi oluyor.)

    - Oracle Linux (ticari)

    - scientific Linux (akademik çalışmalarda kullanılması için tasarlandı. 2019'da geliştirmesi durduruldu ve CentOS'a geçip ona destek verecekleri açıklandı.)

- arch (Pacman paket yöneticisi). sistem kurulumunda sadece ihtiyaç olan paketleri seçtirebilmesi konusunda çok çok esnek.

  - Manjaro

- Gentoo (package manager: Portage) arch gibi sistemin paketlerine kadar kullanıcnın kendisi kuruyor. arch'a göre daha fazla teknik bilgi gerektiriyor.

  - Sabayon

- opensuse (rpm based)

  - SUSE. enterprise.

- PCLinuxOS (end user friendly. sadece masaüstü versiyonu mevcut. RPM based.) 

- Mandriva (or old-name:Mandrake) (rpm based)
  
  - mageia

  - OpenMandriva

- Puppy (liveCD ile çalışabilmek için çok hafif tasarlanmıştır)

- Slackware

- nixOS (nix package manager as default)

- Alpine (package manager: apk (or Alpine Package Keeper) )

- solus (paket yöneticisi: eopkg (pisi türevidir)) (sadece son kullanıcı için masaüstü sürümü mevcuttur.)

distrowatch.com'dan bir OS'un detay sayfasına bakıldığında, temel yazılımlar için (browser, office...) yüklü olan güncel paket sürümleri gibi tüm detaylar dahi bulunmaktadır.

distrotest.net sitesi gerçek makinaya tarayıcı üzerinden vnc ile kullanma imkanı sağlıyor.

# ReactOS
microsoft windows dosyalarını yürütebiliyor ve ona benziyor. linux tabanlı bir OS değildir. sıfırdan yazılmış bir OS çekirdeği kullanılıyor.

# ubuntu netboot
ubuntu türevi değildir. ubuntu'nun standart iso'sundan farklı olarak GUI ve birçok paketi yüklü getirmez. son kullanıcılar arasında "minimal iso" yada "mini.iso" olarakta adlandırılır. bu iso ubuntu repo'larına kurulum sırasında bağlanarak indirme yapar. tabi güncel paket kuracağı için update işlemine gerek kalmaz.

Ubuntu 18.04 ile standart iso ile kurulum sırasında yeni bir seçenek sunuyor: "minimal installation". bu seçenek yukarıdakinden tamamen bağımsızdır. bu standart masaüstü bileşenlerini ve utility'lerin kurulmasını fakat vlc, libreoffice, oyunlar gibi ekstra paketlerin kurulmamasını sağlıyor. normal installation ile arasındaki fark (kurulmayan tam paket listesi) (source-id: 442)

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# package-managers

# Portage

paket yönetim sistemidir. komut satırı uygulaması: __emerge__'dür.

# dnf (or Dandified YUM) vs yum (or "Yellowdog Updater, Modified")

rpm (or Redhat Package Manager) paket yönetim sisteminin komut satırı uygulamalarıdır. dnf yum'un türevidir. fedora'nın birçok türevinden kullanılıyor.

# yum groupinstall vs yum install

yum paketleri grup halinde barındırabiliyor. örneğin "graphic user interface" isimli bir grup varsa, bu grubun içinde gui için gerekli tüm paketler mevcuttur. tek komut ile tümünü kurabiliyoruz.

# zypper

rpm paket yöneticisi. Suse tarafından kullanılıyor. __ZYpp (or libzypp)__ paket yöneticisinin ismi, onu yöneten komut satırı uygulamasının ismi: __zypper__.

# deb paket yönetim sistemi

# apt-get

debian paket yöneticisi için komut satırı uygulamasıdır. "sudo apt-get install chat"

# apt-cache

debian paket yöneticisinin source-list'i ile ilgili işlemlerin yapılmasını sağlayan komut satırı uygulaması. örnek: "sudo apt-cache search chat"

# apt

apt son kulanıcı için geliştirilmiş daha basitleştirilmiş hem apt-cache hemde apt-get komutlarını basitleştirip farklı bir arayüzde sunuyor.

# purge vs remove

apt-get'e geçilen iki parametrede uygulamayı silmemizi sağlar. purge ise configuration dosyalarını da siler. burada bahsi geçen config dosyaları /home içindeki dosyalar değil. bahsi geçen config'ler /etc içindeki konfiglerdir ( /etc: config files for all users. example /etc/appname/ ).

purge seçeneği "synaptic package manager"'de "Tamamen kaldır" seçeneğine tekabül ediyor.

# autoremove vs remove

remove yerine autoremove kullanılırsa, silinen ilgili paketin yüklemiş olduğu ve diğer paketler tarafından kullanılmayan dependency'ler(paketler) de sistemden silinir. genelde bu paketler çok ufak olduğunda tekrar ihtiyaç olması ihtimaline karşı pek kimse autoremove kullanmıyor.

# apt-get update

Paket listelerini güncellemek. liste /etc/apt/sources.list (text bazlı dosya) dosyasındadır.

# apt-get upgrade

kurulu paketleri günceller.

# apt-get dist-upgrade

işletim sistemini günceller. 

# upgrade vs dist-upgrade

sources.list dosyasına baktığımızda içinde bu tarz url görebiliriz: "http://archive.ubuntu.com/ubuntu xenial-security". dikkat edilirse; xenial (ubuntunun bir sürümünün ismi) yazıyor. işte "upgrade" komutu run edildiğinde xenial için desteklenen en son sürüm vlc, firefox ve diğer paketler kuruluyor. yani vlc'nin en son sürümü kurulacak diye bir durum söz konusu diildir. fakat "dist-upgrade" sources.list dosyasının bu url'lerini de günceller. işte işletim sistemi yükseltme farkı budur. işletim sistemi de paketler topluluğudur. bu bakış açısı ile "xenial" kelimesi sources.list'te olmasaydı tüm sistem sürekli yükselirdi.

# apt-get clean

/var/cache/apt/archives/ içinde bulunan .deb uzantılı dosyaları siler. ".deb" dosyaları tekrar kurulma ihtimaline karşı hazır tutulur.

# apt-cache search paket_adı 

programı aramak

# apt-cache show paket_adı

program hakkında bilgi almak

# repository

sources.list dosyasındaki her url bir repository'dir. repository paketlerin dışarıdan indirilmesi için açılan sunucudur.

# ppa (or Personal Package Archive)

paketlerin dışarıdan indirilmesi için açılan Launchpad sunucularıdır. bir ppa sunucusunda birden fazla paket çeşidi indirilebilir. sadece bir paket olmak zorunda diildir.

apt-add-repository ppa:group-name/sub-name ile ppa kurulabilir. eklenen ppa source.list'e eklenmez. ppa farklı bir yerde tutulur: "/etc/apt/sources.list.d" dizininde dosyalar halinde tutulurlar. 

# dpkg
deb dosyaları üzerinde direk işlem yapabilmemizi sağlayan komut satırı uygulamasıdır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# kernel (or çekirdek)

"işletim sistemi" ve "işletim sistemi çekirdeği" farklı kavramlardır. işletim sisteminin çekirdeği değişebilir, fakat kendisi aynı isimde sürüm çıkarmaya devam edebilir.

# UNIX

işletim sistemi çekirdeğidir.

# Darwin

Apple çok eskiden UNIX işletim sistemi kullanıyordu. Daha sonra lisans sorunları sebebi ile BSD çekirdeğini kullanmaya başladı. BSD'den türettikleri işletim sistemi çekirdeğine Darwin adı verildi.

# BSD (or Berkeley Software Distribution)

İşletim sistemi çekirdeğidir. UNIX'ten çatallanmıştır.

# Linux

Linux, UNIX çekirdeğinden çatallanmamıştır.

# Solaris (or old-name:SunOS)

İşletim sistemi ve kernel ile aynı isimde dağıtılmaktadır. çekirdeği, UNIX'ten çatallanmıştır.

# Unix-like operating system (or UN*X or \*nix)

BSD, Linux, Unix ve türevlerini kapsayan işletim sistemi ailesidir. Resmi bir UNIX Spesifikasyonu var, fakat sertifikayı almamış bir çok Unix-like sistemlerde mevcuttur.

# POSIX (or Portable Operating System Interface for Unix)

IEEE (or Institute of Electrical and Electronics Engineers) tarafından belirlenen, tüm işletim sistemlerinde geçerli olabilecek bir standartlar ailesidir. Resmi olarak sertifika almamış bir çok POSIX destekli (or kısmen POSIX destekli) işletim sistemleri vardır. Tüm standartları sağlamayan fakat kısmen standartlara uyan işletim sistemleri vardır. Bunların arasında MS Windows, BSD ve Linux vardır. Solaris ve MacOS, tamamiyle POSIX desteklidir.

POSIX standartları temelde şunlara benzer: İşletim sistmei üzerinde çalışan yazılımların birbirleri arasında yollayabildikleri sinyallarin tipleri, işletim sisteminin process ve thread yönetimi, tarih ve zamanlama konularında standartlar, desteklenen encoding'ler vs...

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# .desktop dosyaları
Birçok linux dağıtımında ".desktop" uzantılı dosyalar mevcuttur. Bunlar normal birer text dosyasıdır. Run edildiklerinde, içindeki bilgilere göre bir komut çalıştırırlar. örnek .desktop dosyası içeriği:

```ini
[Desktop Entry]

Version=1.0

Type=Application

Name=Firefox

Comment=Internet Web Browser

Exec=/usr/bin/firefox.bin

Icon=firefox.jpeg
```

Desktop dosyalarının executable yetkisi varsa; dosya yöneticisi ekranda gösterirken .desktop uzantısını gizler. onun yerine "name" değerini ekranda gösterir. Executable yetkisi olmayan dosyalarda hala ".desktop" uzantısı görülür. 

# Link dosyaları
Unix-like'ların tümünde standarttır. Link dosyaları o dizindeyken orjinal dosyanın tüm özelliklerini döndürürler. Örneğin link'in boyutu 60 mb olabilir. Çünkü Link sadece orjinal dosyanın referansını tutarak, o dizindeymişçesine davranmasını sağlayabilir.

Link dosya sisteminin bir özelliğidir. Oysa desktop file manager'in bir özelliğidir.

# "open with" kısayolları
nautilus'teki "open with" seçenekleri birer desktop dosyalarıdır. /usr/share/applications, /home/user-name/.local/share/applications gibi birçok dizin içerisinde bulunurlar. gnome masaüstü initialize olurken bütün bu dizinleri gezer ve bu kısayolları menüde gösterir. kısayolların içinki "exec" komutuna %U "open with" parametresi ile birlikte açılacak dosyanın aresini gönderir. örneğin scapcraft uygulamaları portable'dır. fakat sistemde yüklü gibi gözükmelerini sağlamak için bir dizinde bütün snap uygulamalaırın desktop dosyaları bulundurur. işletim sistemine kurulmuş olan snap, bu dizini file manager'ların config dosyalarına ekler. artık nautilus her başladığında bu dizini de tarayacaktır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# wine (or Wine İs Not Emulator)
windows executable dosyalarının unix-like'larda yürütmeye çalışan yazılım.

wine ile çalıştırılan bir executable, sistem çağrısı yaptığında çalıştırdığı metod, posix'te denk gelen en yakın metoddur. bu sebeple wine %100 stabil çalışamamaktadır. çünkü sistem çağrıları metodları, windowsun sistem çağrı metodları ile %100 aynı şekilde çalışamamaktadırlar.

wine yukarıdaki sebepten bir emülatör değildir. emülatör olsaydı, sistem çağrıları metodları windows'unki ile birebir aynı şekilde implemente edilmeleri gerekecekti.

örneğin android emülatörleri cpu işlemlerini masaüstü pc'de geçekleştirdiğinde birebir cpu çevrimi yapmaktadır.

wine; aynı windows 7'nin, "windows vista uyumluluk modu" mantığı ile çalışmaktadır.

# playonlinux
wine ile windows programı yüklendikten sonra, yüklenen proramın düzgün çalışabilmesi için windows'a denk gelen dizinlere dll atmak gibi birçok ek işlev gerekebiliyor. bu işlevler her program için toplanmış ve çözümleri internette aık kaynak olarak paylaşılmaktadır. playonlinux uygulaması bunları son kullanıcıya otomatik yapıyor.

mac ve BSD için ayrı fork'lar üretilmiştir: PlayOnMac and PlayOnBSD.

# CrossOver
playonlinux ile aynı görevi yapan ticari bir yazılımdır.

# dll (or Dynamic-link library)
microsoft'un shared-library konsepti için implementasyonudur. dll dosyaları ms-windows için portable kütüphanelerdir. bunun içindeki metodlar herhangi bir programlama dili ile windows üzerinde çalıştırılabilir.

# library path

çalıştırığımız program, kütüphaneleri tararken, taradığı dizinler arasına yeni bir dizin eklemek istersek bu path parametresinden yararlanabiliriz:

```sh
export LD_LIBRARY_PATH="/list/of/library/paths:/another/path"
./program
```

bu bilinen/standart bir path değeri olduğundan her sistem bunu okur.

java'da özel olarak ikinci bir yöntemde sunulmuştur:

```sh
java -Djava.library.path=/path/to/my/dll -cp /my/classpath/goes/here MainClass
```

Linux'ta c/c++'ta iki tip shared object vardır.

- Dynamically linked shared object libraries
  - genelde .so uzantılı dosyalardır. __Shared Object__'in kısatmasıdır.
  - bu dosyalar runtime sırasında ilgili program tarafından okunur.
- Static libraries
  - genelde .a uzantılı dosyalardır.
  - derleme sırasında ilgili programın içine gömülürler.
  - gcc komutu ile bir derlemeye örnek verelim:
    > gcc src-file.c -lm -lpthread
    
    -l prefix'inden sonra "m" ve "pthread" gelmektedir. Bu 2 dosya static lib olarak baul edilir. derleme sırasında tüm sistemde "lib" prefixi ile aranırlar. örnek bulunan dosyalar: 
    - /usr/lib/libm.a
    - /usr/lib/libpthread.a
  - "a" uzantısı archive tiriminin kısaltmasından gelmektedir. a dosyası "ar (archiver'ın kısaltması)" komut satırı uygulaması ile oluşturulur. ".a" dosyası birçok farklı dosyanın birleşimidir. örnek:
    > ar rcs libclass.a class1.o class2.o class3.o

    "libclass.a" dosyası birçok .o dosyasının birleşimidir.

    ar komutu genelde sadece derlemelerde kullanılır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Filesystem Hierarchy Standard (FHS)
POSIX'ler için dizin standarttır. asagida bazı dizinler verilmiştir. iligli olanlar gruplandırıldı.

__

/dev device files. everthing is file on linux konusu. example: hdd partitions.

/Proc is a special virtual directory like /dev. Baska başlıkta detaylı anlatılıyor.

__

/media mounted removable devices (cd-rom, usb)

/mnt temporary mounted volumes (mounted iso)

/cdrom cd-rom mount point. it is not linux standart. because linux use /media.

/misc automatic mounted device , like archive files (like .iso), or mounted remote filesystems

__

/lib shared libraries /lib32 /lib64 gibi dizinler olabilir. çünkü aynı isimde executable'lar aynı sistemde olabilir. bu dizinde aynı zamanda kernel-modülleri de vardır.
bazı OS'larda /lib /usr/lib'e linklenmiş durumdadır. bu tarz linklemeler birçok dizin için yapılmaktadır.

/usr apps own files.

/sbin system-binary'den gelmektedir. Utilities used for system administration (and other root-only commands). mostly recovering, booting, repairing things...

/bin command line based executable apps

/usr/bin commands for end user, GUI apps 

/usr/sbin sistem açıldıktan sonra kullanılabilecek yönetimsel komutlar  buradadır. boot, recover, repair için olmayan fakat yönetimsel komutlar bu dizindedir.

/usr/local/sbin kullanıcı tarafından yüklenen sistemsel uygulamalar

/opt optional'dan gelmektedir. 3rd addons, or other system optional softwares.

__

/var app data for all users except config files (because config files are stored on /etc). the files inside tese directory are grouped like: log files (/var/log), crash dumps (/var/crash), files which are sent to printer (/var/spool), 

/etc config files for all users. example /etc/appname/.

/home/username user spesific home folder

/root root user's home folder

__

(others - gruplanamayanlar)

/lost+found hata durumlarında bazı dosyalar dosya sisteminde yok olabiliyorlar. fakat bu dosyalar tekrar kurtarılabilmeleri için eğer yapılabiliyorlarsa bu dizin altında linkleniyorlar.

/srv data to be served by the system for protocols such as, ftp, www

/tmp temporary files for all apps.

/boot boot files (example: grub)

# MacOS dizin yapısı
MacOS'ta POSIX'lerdeki gibi bir yapı vardır. Bazı istisnalar şunlardır:

/Applications --> uygulamaların ve kendi datalarının tutulduğu dizindir. her uygulama kendi isminde bir klasörde tutulur.

/Users --> linux'taki /home dizinidir. sadece ismi farklıdır.

/Volumes --> mount edilen tüm bölümler buradadır.

/var/root --> linuxtaki /root dizini.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# linux üzerinde yetki
linux üzerinde dosyalar üzerindeki haklar kullanıcı, grup ve diğerleri olarak 3 grupta belirlenebilmektedir. 

bir dosya için permission tanımlaması yaparken sadece owner, grup ve others olarak yapılabilir. bu sebepten eğer bir dosyaya, 2 farklı grubun hakkı olması isteniyorsa, yeni grup yaratılıp, o gruba yetki atanmalıdır.

1 kullanıcı birden fazla gruba mensup olabilir.

chown; owner değiştirme, chmod ise permission değiştirme için unix'lerde kullanılan komut satırı uygulamalarıdır. örnek:

> chmod 730 myfile.txt

yada farklı bir formatta yetkiler sırası ile verilir:

> chmod rwx-wx--- file.txt

Yukarıdaki ilk 4'lü (rwx-) dosyanın owner'ı için geçerli permissionlardır. ikinci dötlü ise dosyanın grubundaki user'lara uygulanacak permissionlardır. Son dörtlü ise "others" için geçerli olacak yetkilerdir.

"ls -la" komutu ile buldunduğumuz dizindeki dosyaları yetkileri ile beraber görebiliriz.

chmod'un aldığı sayısal parametre'ye unix'lerde "mode" olarak isimlendirilmektedir. mode şu şekilde belirlenir:

4 "read",

2 "write",

1 "execute"

0 "no permission"

her biri owner, grup, other için yanyana koyulur. aşağıdaki örnekler aynı anlama gelir:

> chmod u=rwx,g=rx,o=r myfile

> chmod 754 myfile

> chmod rwxr-xr-- myfile

Bazı mode'ların sembolik tanımlamaları da vardır. örnek: 

- a+wx

  777 ile aynı anlama gelir.

- a-wx

  r--r--r-- ile aynı anlama gelir

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# superuser
- linux işletim sisteminde hiç kısıtlaması olmayan kullanıcıdır.
- UID (user identifier) sıfırdır.
- bu kullanıcının ismi genelde 'root' olarak koyulur fakat bu bir zorunluluk diildir.
- dolayısı ile; terminolojik olarak root ve superuser aynı şey diildir.

# su (komut)
'substitute (vekil) user' ve 'switch user'ın kısaltmalarından gelmektedir. 'super user' ın kısaltması değildir. çünkü user switch yapmamızı sağlar ve o user ile komut çalıştırabilmemizi sağlar.

"su" komutu, kullanıcı logout/login yapmadan komut satırından diğer kullanıcılara geçiş yapmamıza yarar. "su -c" komutu ile sadece o vereceğimiz komutu run etmemizi sağlar.

başka kullanıcı ile işlem yaparken "exit" komutu ile eski kullanıcıya dönüş yapabiliriz.

sadece 'su -' komutu o anda root user'ı olmamızı sağlar. 'su abc' komutu ise; abc kullanıcısı olmamızı sağlar.

# 'sudo abc' ( kısaltması)
"SuperUser Do" kısaltmasından gelmektedir.

"abc" komutunu başka kullanıcı yetkileri ile (kullanıcı ile değil!) işletmemiz sağlar. sudo komutunun geliştirildiği ilk zamanlar sadece superuser yetkileri ile işlem yapılması sağlanıyordu. bu sebeple ismi "SuperUser Do" kısaltmasıdır. fakat daha sonra herhangi bir kullanıcı yetkileri ile işlem yapabilmek için tasarlanmıştır. default olarak superuser yetkileri ile işlem yapılabilmesini sağlar.

sudo komutunu çalıştıran kullanıcının, sudo çalıştırmaya yetki verilmiş olmalıdır (sudoers dosyası aşağıda anlatılıyor). komut çalıştırılırken sorulacak şifre o andaki user'ın şifresidir.

ubuntu, komut satırını kapatıp açana kadar yada belirli bir süreliğine tekrar şifresiz sudo komutu üzerinden komut yürütmemize izin verir. bu 2 özellik sudo'nun özelliğidir.

"sudo -i" ile sürekli olarak root yetkileri ile işlem yapmamızı sağlar.

sudo komutunun plugin altyapısı mevcuttur. kaynak: (source-id: 10) "Description" başlığı 2inci paragraf. bu sebeple her sistemdeki davranışları, OS'un plugin kurallarına göre değişkenlik gösterebilir.

# gksudo command
gksudo komutu $HOME dizinini /root olarak ayarlıyor. bu şekilde çalışan komut satırı uygulamasının config dosyaları kendini /root altına atıyor. oysa sudo ile çalıştırılsaydı config dosyaları /home/current-user-name altında root yetkileriyle dosyalarda bulunuyor olacaktı. yetki sorunları meydana gelecekti. Aynı zamanda (özellikle) X oturumu dosyalarında da yetkilendirme sorunu olabiliyor. Bu sebeple grafik arayüzü uygulamalarını ilgilendiren bir konu. BU sebeple gnome 'gksudo', KDE uygulamaları ise 'kdesudo' komutunu kullanıyor.

# Ubuntu root user 
Ubuntu'da varsayılan olarak root kullanıcı ile giriş yapılmıyor. fakat kulanıcının root yetkileri mevcut. /etc/sudoers dosyasında hangi kullnıcıların kendi oturum şifrelerini bildiği takdirde root yetkileri ile komut çalıştırabileceklerini gösteriyor. işte sudo burada devreye giriyor. root kullanıcımızın bir şifresi olmamasına rağmen root yetkileri ile işlem yaptık. bu sudo komutunun bir özelliğidir. oysa ubuntuda "su" komutunu veridğimizde root kullanıcısı şifresi sorar, ubuntu'da (varsayılan olarak) root kullanıcı şifresi olmadığından root'a hiçbir zaman geçiş yapamayız. su genelde çoğu linux sisteminde kullanılan bir komut iken; sudo bazı dağıtımlarda kullanılır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Terminal (or uçbirim)
kelime anlamı:

1. Otobüs, uçak vb. taşıtların yolcularını ilk aldığı veya son bıraktığı yer.
2. Bir veri iletişim ortamında veri giriş çıkışını sağlayan donanım birimi veya donanım birimleri topluluğu.

text input/output environment. Bir sistemin yönetilebilmesi için giriş ve çıkışları olan parçadır/modüldür.

# Konsol (or console)
türkçe sözlükte: "işletmen uçbirimi" olarak belirtilmiştir. yani bir terminal'dir. fakat işletmen, yani operatör (Bilgisayar vb. teknik aletleri işleten kimse) için geliştirilmiş bir terminaldir.

# Sanal konsol
İşletim sistemlerindeki komut satırı uygulamaları birer "sanal konsol"dur. komutu yazan yazılımcı/programcı için geliştirilmiş konsol.

# Video oyun konsolu
Digital ortamda oyun oynayabilmek için tasarlanmış konsoldur.

# shell (or kabuk)
shell, işletim sisteminde son kullanıcı için, işletim sistemine erişmesi için sunulan arayüzüdür. Bu arayüz Gnome, KDE olabilirken, sadece komut satırı masaüstleri yada sadece komut satırı uygulamasıda bir "kabuk"'tur. çünkü işletim sistemine erişmemiz için bir arayüz sunarlar.

# unix shell
bu terim; *nix sistemlerde, komut satırı yorumlayıcıları kapsar.

# Shell Command Language (or sh or Bourne shell)
programming language + __"command line interpreter"__ ( dili yorumlayan yazılım) described by the POSIX standards. bir spesifikasyondur. implementasyon değildir.

"command line interface" ile "command line interpreter" kısaltmaları aynıdır. fakat ikisi farklı kavramlardır.

# bash (or Bourne-Again SHell)
Bir "sh" implementasyonudur. 

Geliştirildikten sonra sh standartlarınında dışına çıkmıştır. isteğe bağlı sh uyumlu modda çalışabilir. "sh uyumlu mod"da çalıştığında hem bash hemde sh özelliklerini barındıracak şekilde script'leri run eder.

Bash'in pazar payı yüksek olduğundan; Çoğu unix-like sistemde /bin/sh uygulaması çalıştırıldığında, aslında bash çalıştırılır. /bin/sh sadece bir sembolik bir linktir (kısayol). bin/sh sadece bash'i değil, sistemde tanımlı olan default sh implementasyonunu çağırır.

# Z shell (or Zsh)
sh implementasyonudur.

# diğer shell'ler
fish, dash, Xiki Shell (or xsh), KornShell...

MacOs bash kullanmaktadır. Güncel sürümlerinde (ortalam yıl: 2019) zsh ile bilikte gelmektedir.

# fish
fish is not posix comptible or shell compatible. fakat çok daha sonra geliştirilmesi başlandığı için çok güncel teknolojieri baz alıyor. GPL lisanslı. Herkes genel olrak çok başarılı buluyor fakat shell uyumlu olmaması sebebi ile hiçbir OS default yüklü getirmemektedir.

# Oh My Zsh
sadece zsh için konfigürasyonlar community tarafından bu proje altında dağıtılmaktadır. bu konfigürasyonlar ile interpreter olan zsh, son kullanıcı için çok daha fazla yeteneğe sahip oluyor. bu özellikler terminal'den bağımsızdır.

oh-my-zsh bilgisayara kurulduğunda istenirse root izinli bir dizinine, yada istenirse de $HOME/.oh-my-zsh/ dizinine kuruluyor. burada birçok script mevcut. Bu script'lerin devreye girebilmesi için de $HOME/.zshrc dosyasında (bu dosya zsh tarafından execute ediliyor) bir referans (basit bir script çağırma sarırı) mevcut. yani oh-my-zsh tamamiyle taşınabilir durumda. $HOME/.oh-my-zsh/ dışında hiçbir yere kurulum yapılmıyor. $HOME/.oh-my-zsh/ dizini bir setup'tan değil, "git" aracılığı ile çekiliyor.

# Terminal Emulator (or CLI or command line interface)
shell yada alternatiflerini kullanabilmemiz için GUI yazılımlarıdır.  

"Terminal" unix-like dünyasında bir device dosyasıdır. Bu dosyaya yazma işini "Gnome terminal" gibi yazılımlarla; yani "terminal emulator"'larla yaparız.

Terminal Emulator içerisine komutlar yazdığımızdan, "Terminal Emulator"a eş anlamlı olarak CLI de kullanılmaktadır.

unix ve benzeri sistemlerde herşey dosyadır ve terminalde bir dosyadır. bir komutun çıktısı ve girdisi dosyadan okunacak şekilde basittir. Oysa powershell bir script dilidir. üst seviyeli API aracılığı ile linuxta yapılabilen birçok şeye imkan sunar.

# piyasadaki bazı terminal emulatörler

| name                              | notes                                                                                                                                                                                                                                   |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| xterm                             | ilk olarak X windows manager ile uyumlu çalışabilmesi için tasarlandığından "x" prefixi takılmıştır.                                                                                                                                    |
| UXTerm                            | xterm'in bazı karakter seti desteği eklenmiş paketinin ismidir.                                                                                                                                                                         |
| GNOME Terminal                    | Gnome desktop projesinin bir parçası olan terminal yazılımıdır. Uygulama açıldığında GUI'deki title'ı sadece "terminal"'dir. fakat bu son kullanıcıya kolay olması amaçlı bu şekilde tasarlanmıştır. orjinal ismi "gnome terminal"'dir. |
| Terminator                        | java ile yazılmış açık kaynaklı bir terminal yazılımıdır.                                                                                                                                                                               |
| macOS için terminal               | MacOs içerisinde gömülü gelen terminal yazılımının özel bir ismi yoktur. direk olarak "terminal" olarak isimlendirilmektedir.                                                                                                           |
| iterm                             | sadece macOS için geliştirilen terminal yazılımıdır. proje uzun zamandır güncellenmediğinden __iterm2__ isimli proje hayata geçirilmiştir.                                                                                              |
| Guake                             | gnome için masaüstünde panelden açılabilen komut satırı yazılımıdır.                                                                                                                                                                    |
| Konsole                           | KDE projesinin parçası olan komut satırı yazılımıdır.                                                                                                                                                                                   |
| Terminology                       | enlightment masaüstü projesi içinde gelen terminal yazılımıdır.                                                                                                                                                                         |
| upterm (or old-name:Black Screen) | web altyapısı üzerine kuruludur. sonlanmıştır (yıl 2019).                                                                                                                                                                               |
| hyper (or old-name:HyperTerm)     | web altyapısı üzerine kuruludur. hyper uygulaması, HyperTerminal ile karıştırılmamalıdır. HyperTerminal microsoft windows için çok farklı amaçta geliştirilmiş bir yazılımın ismidir.                                                   |
| tilix                             |                                                                                                                                                                                                                                         |
| terminus                          |                                                                                                                                                                                                                                         |
| alacritty                         |                                                                                                                                                                                                                                         |
| putty                             | ssh, için tasarlanmıştır. uzak masaüstündeki shell'i interpreter olarak kullanır. mintty projesi buradan birçok alıntı kod içermektedir.                                                                                                |
| KiTTY                             | putty projesinin forkudur.                                                                                                                                                                                                              |
| mintty                            | aşağıdaki başlıklarda açıklanmıştır                                                                                                                                                                                                     |
| tilda                             |                                                                                                                                                                                                                                         |
| SecureCRT                         | ticari                                                                                                                                                                                                                                  |
# microsoft windows

- ## PowerShell
  command line intepreter'dır. (tabi yürüttüğü script dili de yenilendi. cmd.exe'den farklı dil kullanıyor.)

- ## Windows Terminal
  kodadı: Cascadia
  
  microsoft'un 2019'da geliştirmeye sıfırdan başladığı, açık kaynaklı, sadece terminal emulator.

- ## Windows Console
  terminal emulator'dır. açılan GUI ekranıdır. powershell ve cmd default'ta bununla açılır. kaynak: (source-id: 11) "Microsoft’s Big Bet – Windows NT" başlığı, son paragraf.

- ## command.com
  command line intepreter'dır.

  __MS-DOS command interpreter__ olarak ta anılır çünkü MS-DOS tabanlı sistemlerde bu kullanılıyordu. kaynak: (source-id: 12) 10'uncu sayfa, "Command shell overview" başlığı, ilk paragraf.

  .bat uzantılı dosyaları yürütür.

- ## cmd.exe (or Command prompt)
  command line intepreter'dır.

  terminolojik olarak; "Command prompt" ile aynı anlamdalar. (source-id: 11) "Microsoft’s Big Bet – Windows NT" başlığı, son paragraf.

  .CMD uzantılı dosyaları yürütür. fakat ".bat" ile geriye uyumludur. kaynak: kaynak: (source-id: 14) "Also, Cmd != MS-DOS!" başlığı, 7'inci madde.

  MS-windows NT sürümlerinde fault olarak CMD'.exe'ye geçiş yapmıştır. kaynak: (source-id: 14) "Also, Cmd != MS-DOS!" başlığı, 6'ıncı madde.

- ## Windows Console Host (or Console Windows Host)
  conhost.exe'ile yürütülen yazılımdır.

  windows 7 ile gelmiştir. kaynak: (source-id: 16) "So, what’s inside the Windows Console?" başlığı.

  windows 7 öncesi conhost yerine "ClientServer Runtime System Service (or CSRSS)" kullanılıyordu. 

  cmd ve powershell ve diğer komut satırı uygulamaları buraya attach olarak çalışırlar. buna zorunlu diiller. 3üncü parti conhost alternatif'leri mevcutur.

  conhost'un sunduğu api "Console API"'dir. Bu api'yi kullanabilmek için "Console Driver (ConDrv)"'a ihtiyacımız var.

# Komut satırı olarak terminal emülatörler

Bu tarz emülatörler menubar border içermezler ve farklı emulatör içerisinden de çağrılabilirler. Komut satırından çağrıldıklarında aynı satırda kendisi başlamış olur. Özellikle desktop manager/window manager olmayan ekranlarda kullanılmak üzere tasarlanmışlardır.

- Linux console
- GNU Screen
- Minicom
- tmux

# xterm türevleri
xterm açık kaynaklıdır. onu fork eden birçok proje geliştirilmiştir:

liste için kaynak: (source-id: 17) "What versions are available?" başlığı.

- ansi_xterm
- color_xterm
- cxterm (Chinese)
- hanterm (Korean)
- mxterm
- nxterm
- kterm (Japanese)
- xterm (forked by "X Consortium")

Ekranda renkleri gösteren katman terminal emulator'dır. interpreter karakterleri output olarak verir gerisine karışmaz. aldığı outputlarda escape karakterlerin ne olup olmadığı terminal emulator'ın standartlarına bağlıdır. bu standartlara __escape sequences__ denir. örnek sequence: __DEC VT220__. kaynak: (source-id: 18) "DESCRIPTION" başlığının sondan birinci paragrafın son cümlesi.

Bazı kaynaklarda __escape sequences__ için protokol terimi de kullanılmaktadır. Bir terminal emulatör manual sayfasında hangi protokolleri desteklediğini yazar. Bazen desteklediği protokollerde "xterm" görebiliriz. Bu; xterm'in desteklediği protokolleri desteklemektedir, anlamında kullanılır.

"Terminal emulator" terimi de "terminal emulation"dan gelir. çünkü VT220 birer terminal cihazlarıdır (__Digital Equipment Corporation (or DEC)__ tarafından geliştirilmiştir). Onların sequence'lerini komut satırı GUI yazılımımız desteklediği için, GUI yazılımımıza terminal emulator denir.

Genelde "$TERM=xterm-*" olan terminaller xterm'in desteklediği escape sequences'ları dinliyor anlamına gelir. Fakat bu kuralı tüm terminal'ler doğru şekilde uygulamıyor. kaynak: (source-id: 17) "What versions are available?" başlığında ortada olan 3 maddelik paragraf.

Bazı terminaller birden fazla sequence'yi destekliyor. örnek "gnome terminal". kaynak: (source-id: 18) "DESCRIPTION" başlığının son 3 paragrafı.

En başta belirtidliği gibi: Ekranda renkleri gösteren katman terminal emulator'dır. fakat echo ve printf gibi komutlar (or herhangi bir çıktı üreten komutlar), escape characterini dışarıya yansıtıp yansıtmayacağı önemlidir. çünkü yansıtıp yansıtmayağına göre, terminal emülatör onun renkli olup kontrol etmektedir. bu sebeple bazen komutun or shell'in nasıl davrandığı da renklendirmek için önemli olabiliyor.

# Cygwin vs MinGW (or Minimalist GNU for Windows)

açık kaynaklı bazı linux komut satırı uygulamaları, windows için tekrar derlenerek windows tarafında kullanılabilmektedirler. Fakat sadece POSIX uyumlu API'ler çağrıldığında sorun olacaktır. Buna çözüm olarak; Cygwin bu API'lerin yerini tutan windows karşılığındaki adaptor/emulator'lar içermektedir. Cygwin, bir dll dosyasıdır ve POSIX için gerekli tüm API'lere denk gelen windows API'lerini çağırır.

MinGW de ise böyle bir katman yoktur. MinGW direk windows için çalışan native uygulamalar paketidir. normalde; GCC sadece linux'a derlemek için tasarlanmıştır. Oysa MinGW; di̇rek olarak gcc'nin wi̇ndows'ta çalışacak exe dosyasını üretmiştir. bunu yapabilmek için GCC'nin kodlarında gerekli değişiklikleri yapmaktadırlar. MinGW aynı zamanda birçok POSIX uygulamasını da sadece windows'ta çalıştırabilecek şekilde kodlarını dğeiştirip, windows için derleyip hazır şekilde sunmaktadır.

Cygwin ile wine'ın mantığı tamamiyle farklıdır. wine direk windows executable'larını, linux'ta çalıştırırken, Cygwin linux executable'ı çalıştırmaz. Cygwin, UNIX executable'larının Cygwin/windows için derlenmiş hallerini çalıştırır. çalıştırıken ek olarak bir dll aracılığı ile, bazı API isteklerinin önüne geçer.

# MSYS
Minimal SYStem'ın kısaltmasıdır.

MinGW ile derleme yapmayı kolaylaştırmak için ek geliştirilen bir altyapıdır. MSYS bir unix programının windows ortamında derlenebilmesi için gerekli tüm tool'ları barındırır. örnek:
- make
- gawk
- grep
- bash (sadece interpreter, terminal GUI uygulamasını barındırmaz)

kaynak: (source-id: 21) 1 ve 2inci paragraf.

# MSYS vs MSYS2
MSYS2, MSYS'den bağımsız geliştirilen çalışmadır. fork değildir. aynı amacı güttüğü için bu şekilde isim verilmiş.

MSYS2 kendi içerisinde pacman paket yöneticisini yüklü getirir.

MSYS ve MSYS2, birer Cygwin forkudur. kaynak: (source-id: 22) 3 vs 6'ıncı paragraf.

"git for windows" başlığında __git-bash__, __msysGit__ hakkında bilgiler mevcut.

# mintty
windows için açık kaynaklı terminal emulator'dır. ms-windows'un komut satırı ile hiçbir bağlantısı yoktur. aşağıdaki paketler opsiyonel olarak mintty ile entegreli çalışabilir:
- MSYS
- MSYS2
- cygwin

# termux
- android için açık kaynaklı terminal emulator'dır.
- android işletim sistemi biraz farklı bir dizin yapısı kullandığı için apt-get ile kurulan komut satırı uygulamaları bu terminalde düzgün şekilde çalışamayabiliyor. benzer şekilde bu uygulama root olmayan cihazlarda çalışmak üzere tasarlandı. bu sebeple apt ile kurulan uygulamalar storage'ye kuruluyor. dolayısı ile komut satırı uygulamaları bu sebepten düzgün çalışamıyorlar. çünkü normalde o uygulamalar root yetkisi ile sistem kurulucak şekilde tasarlanmıştır. kurulum yöntemi farklı olunca, çalışmasında da sorunlar olabiliyor.
- android üzerinde her uygulamanın kendi user'ı var. bu uygulamaya sandbox yaptırmayı kolaylaştırıyor. uygulama bir yetki istediğinde, aslında kullanıcıya yetki veriliyor. her app'in bir user olmasının birbirinin dosyalarına erişememelerini de sağlıyor. bu sebeple; termux üzerinde çalıştırdığımız her komutta bunu değerlendirmemiz gerekiyor.

# CTRL+ALT+F1
Linux'ta GUI masaüstü ekranı açıkken buna basıldığında, tüm ekranda konsol ekranı açılır. arkaplanda varsayılan olarak 6 adet ekran açıktır. 7inci ekran GUI'nin kendisini (X or wayland) açmış olan session'dır.

CTRL+ALT+F1 ile ilk konsole ekranı açılırken, CTRL+ALT+F2 ile ikincisini açabiliriz.

Eğer GUI ekranında diilsek, yani konsol'daysak, ALT+FX ilx X'inci session'a geçebiliriz. ALT+→ ve ALT+← ile bir önceki veya bir sonraki session'lara gidebiliriz.

# Windows Subsystem for Linux (or WSL)
- 1.0 ve 2.0 sürümleri arasında çok büyük farklar var.
- Tüm WSL sürümleri sadece 64 bit windows'larda ve 64 bit linux executable'larını yürütebiliyor.
- Tüm WSL sürümleri linux GUI uygulamalarını desteklemeyecek şekilde tasarlanmıştır.
- WSL 2 direk özel bir VM içerisinde çalışıyor. Linux executable'ları çalıştırılmak istendiğinde direk olarak çekirdekte çalıştırılıyor. Oysa WSL 1.0'da istek intepret ediliyor ve eğer varsa POSIX system call'ları emüle ediliyordu. kaynak: (source-id: 23) "Full System Call Compatibility" başlığı, 1inci paragraf.
- WSL 2'de optimize edilmiş özel bir linux kernel'i ile geldiği için boot-time ve performance sorunları çok düşük. kaynak: (source-id: 23) "A quick explanation of the architectural changes in WSL 2" başlığı, 1inci paragraf.
- wsl komut satırı uygulaması ile linux komutları CMD üzerinden de çağrılabilmektedir. örnek:

  > wsl echo hello

  kaynak: (source-id: 25) "Run Linux tools from a Windows command line" başlığı.

- WSL'in linux shell'i üzerinden windows uygulamalaır da çağrılabilir:

  > ipconfig.exe | grep IPv4

  kaynak: (source-id: 25) "Run Windows tools from Linux" başlığı.

- WSL içindeki linux ile Windows user'ları birbirlerinden tamamen bağımsız.
- windows dosyalarına WSL içerisinden bu şekilde erişiyoruz: "/mnt/c/Program Files"
- Windows'tan WSL dosyalarına erişmek için:

  > \\\wsl$\ubuntu
  
  > \\\wsl$\distro-name

  direk olarak bu değeri path olarak kullanabiliriz. WSL içerisinde gömülü file server geliyor. Windows ise client tarafta bu file server'ı dinliyor. Bu sebeple WSL kapalı ike içindeki dosyalara erişemeyiz.

  Aynı zamanda bu durumun bilinen önemli bug'ları var: https://devblogs.microsoft.com/commandline/whats-new-for-wsl-in-windows-10-version-1903/ "Known issues" başlığı.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# komut satırı path değişkenleri

işletim sistemi aşağıdaki dosyaların içindeki komutları sırası ile işletir.

/etc/profile  --> her login sonrası (tüm user'lar için) çalıştırır.

~/.profile -> her login sonrası bu home klasörünün sahibi olan user için bu dosyadaki komutlar çalıştırılır.

~/.bashrc  --> shell uygulaması başlatıldığında, ilk olarak bu dosyanın içindeki komutları sırası ile çalıştırılır. örneğin 'bash' komutunu çalıştırdığımızda buradaki kodlar tekrar çalıştırılır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# builtin (internal) command
bu komutlar birer program diildir. bu komutlar terminal emulator'ların sunduğu bir özellik değildir. bu komutlar interpreter'ın (bash, zsh gibi) sunduğu keyword'lerdir/özelliklerdir. örneğin "which echo" yazdığımızda sonuç alamayız. çünkü echo bir builtin command'dır.

Bazı terminal'ler yada OS'ler shell builtin'leri ile aynı isimde programlar eklerler. bu durumda override eden (ki muhtemelen shell override edemeyecek) program çalışacaktır. Dolayısı ile komutlara aynı parametre yollasak bile farklı ortamlarda farklı sonuçlar alabiliriz.

"bash-builtins" komutu bize bash'in internal komutlarını listeler. bu liste aşağıdaki gibidir:

alias, bg, bind, break, builtin, case, cd, command, compgen, complete, continue, declare, dirs, disown, echo, enable, eval, exec,  exit,  export,  fc,  fg,  getopts, hash, help, history, if, jobs, kill, let, local, logout, popd, printf, pushd, pwd, read,  readonly,  return,  set,  shift,  shopt,  source, suspend,  test,  times,  trap,  type, typeset, ulimit, umask, unalias, unset, until, wait, while

isimleri ilginç fakat bunlarda builtin'dir:

```sh
:
```

```sh
exit 0 # (saglikli) donus yapan bos bir uygulamadır
```

```sh
.
```

source ile aynı görevi görür. parametre olarak source edilecek dosyayı alır.

```sh
[
```

çoğu yazılımcı bunu syntax sanar oysa değildir. __"test"__ komutu ile aynı görevi görür.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

## sourcing script vs executing script

"source ./file.sh" vs "./file.sh"

ikiside file'ı aynı şekilde işletir. fark şudur: source dosyayı current-process'te (current-shell'de) execute eder. bu sebeple file'ın değiştireceği her variable tüm shell akışı boyunca kalıcı olur. oysa "./file.sh" yeni bir sub-shell (sub-process) açılır ve file'ın oluşturduğu hiçbir variable/fonksiyon shell'de kalıcı olmaz.

source komutu yerine bu şekilde de kullanım aynı görevi görecektir:

> . command

noktalı gösterim yerine source kullanmak daha best-practice'dir. çünkü "source" bir komut satırı uygulamasıdır. komut satırı olunca daha portable oluyor. çünkü built-in'ler her ortama göre değişebiliyor. bazı ortamlarda "." kullanılmıyor. örneğin fish'in güncel versiyonlarında "." kullanılmıyor. kaynak: (source-id: 27) 5'inci paragraf.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# komut satırı uygulamalarının help/manuel açıklamaları
"man pwd" ile pwd'nin manuel dosyasını ekrana bastırırız. her manuel'de SYNOPSIS (türkçe kelime anlamı: özet) başlığı vardır. Bu başlıkta komut satırının parametrelerinin nasıl yollanacağı açıklanır.

SYNOPSIS'in %100 bir standartdı yok. birçok firma kendi standardını resmi sitesinden yayınlıyor. fakat her uygulama bunlara uymuyor ve firmalar arası ufak farklar mevcut. örnek bir SYNOPSIS standartları standardı: (source-id: 441)

örnek SYNOPSIS ve anlamları:

```sh
command [options] <file1> [<dir1>]... param {a|b|c}
```

- "options" başlığındaki parametrelerden birini alacak anlamına gelir.
- options'taki [] işareti, bu alanın (options alanının) opsiyonel olduğunu gösterir. yani yollanması zorunlu diildir.
- file1 zorunlu bir alandır. çünkü [] içinde diil.
- file1 <> içine alınmış çünkü bir değeri ifade ediyor.
- dir1 opsiyoneldir ve ... birden fazla parametre yanyana olabilir anlamını kazandırır.
- "param" <> içine alınmamış. çünkü bir değeri ifade etmiyor. harcode bir string. yani son kullanıcı buraya sadece "param" yollayabilir.
- {a|b|c} a veya b veya c parametresi alır. bazı standartlarda {} yerine () kullanılır. c'nin altı çizli olsaydı c default değer (yani son kullanıcı o parametreyi yollamazsa) alınacak değer anlamına gelir.

- kalın yazılmış kelimeler:
  - <> alınmayan (sabit/hardcode string'leri)
  - komutun kendisi

- italik yazılan kelimeler:
  - <> içerisine alınan değerlerdir

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# coreutils
açık kaynaklı c ile yazılmış, hiçbir dependency gerektirmeyen en temel komut satırı uygulamalar grubudur. tümü bir git repository'sinde düzenli olarak geliştirilir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

## tty
TeleTYpewriter'ın kısaltmasıdır. stdout'a, stdin (stream) dosyasının full path'ini döner.

__eng:teleprinter (or teletypewriter or teletype or TTY or tr:telem)__ bir metnin uzağa gönderilemsine yarayan, elektromanyetik cihaz. 

örnek; "tty" komutu çıktımız "/dev/pts/0" olsun. aynı komut satırında "read my_variable" komutunu verirsek, komut satırı stdin'den bizim bir değer girmemiz ve bu değeri ekrana basıp aynı zamanda my_variable'a atayacaktır. read komutu bu işi görür. biz hiçbir değer girmezsek ve farklı bir terminal session'ında "echo hello > /dev/pts/0" yazarsak, diğer session'daki read komutuna "hello" string'i gider.

her açtığımız terminal session'ı (ssh olsun, local terminallerimiz olsun) hepsi farklı stdin'e sahiptir. bu sebeple her açtığımız terminal'de tty değerleri genelde bu şekilde ilerler: /dev/pts/0, /dev/pts/1, /dev/pts/2

burada basit bir anlatım var: (source-id: 28) "Enter, the Pseudo Terminal (PTY)" başlığı.

## pseudoterminal master (or PTM) vs pseudoterminal slave (or PTS)
terminal interpreter'lar (ssh, xterm, gnome terminal...) bir terminal session'ı açtıklarında bir pts ve ptm dosyası oluştururlar. bunlar device dosyalarıdır.

terminolojik olarak bakıldığında; terminal interpreter'lara __pseudoterminal (or pty or pseudo-tty or pseudotty)__ denir.
