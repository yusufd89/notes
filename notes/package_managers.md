############################

############################
# PACKAGE MANAGERS
############################

############################

# Homebrew
Sadece macOS için yapılan açık kaynaklı paket yöneticisi projesinin ismi. komut satırından __"brew"__ olarak kullanılmaktadır.

Linux ve ms-windows için aynı temele dayanan yazılım paralelden ayrı geliştiriliyordu (linux için olan Linuxbrew projesiydi). daha sonra bu projelerin tümü birleştirildi.

Homebrew, nix ile çok benzer yapıdadır. fakat nix, özellikle sürüm yönetimi konusunda çok daha gelişmiştir.

## formulae
formulae paket kurulumu için gerekli tanımlamaları içeren metindir. Homebrew tarafından kullanılır.

# Cask
Homebrew eklentisidir. GUI kullanan uygulamaların yönetimini sağlamaktadır.

ilk başlarda Homebrew'den bağımsız geliştiriliyordu. daha sonra Homebrew altında ortak geliştirmeye başlandı.

Cask sadece macOS'ta desteklenmektedir (yıl 2019).

# Flatpak (or old-name:xdg-app)

flatpak, sadece unix tabanlı sistemler için geliştirilmiştir. user-yetkisinin yeterli olduğu sandbox teknolojisine dayanıyor (teknoloji adı: Bubblewrap). 

# Bubblewrap vs firejail vs sandstorm

linux'ta user-namespace teknolojisi genişletilerek root yetkisi olmadan sandbox içinde uygulama çalıştırmaya yarayan birbirlerine alternatif teknolojilerdir.

# Filesystem in USErspace (or FUSE)
root yetkisi olmadan process'in kendi görebildiği dizinini, root dizinlerine mount edebilmesini sağlıyor. desteklediği OS resmi olarak sadece Linux ve BSD. Fakat 3üncü parti fork'lar Mac (OSXFUSE-macFUSE) içinde çalışmasını sağlamaktadır.

# AppImage (or old-name:klik or old-name:PortableLinuxApps)
tüm dependency'ler tek bir dosya içinde tutuluyor. hiçbir paket yöneticine ihtiyaç barındırmıyor. direk executable'ın yürütülmesi yeterli oluyor. FUSE tarzı altyapı kullanarak çalışıyor.

# nix

nix sistemden bağımsız çalışan paketleme sisteminin ismidir. her uygulama root dizininde store olarak isimlendirilen bir dizinde saklanıyor. her user ise kendi path'inde istediği kısayolları ekliyor. nix bir paket yöneticisidir.

nix, mac'te de native olarak çalışıyor. nix namespace teknolojilerini, build sırasında veya nix daemon veya nix komut satırı uygulaması ile işlem yaparken kullanıyor. fakat kurulumdan sonra uygulamalar namespace teknolojileri ile çalışmıyor. bu sebeple firejail gibi uygulamalar nix ile entegre çalışabilirken, snap ile çalışmamaktadır.

snap ve flatpak ise cgroup, namespace gibi teknolojilerden direk olarak yararlanıyor. kaynak: (source-id: 267) 2nd paragraph.

# NixOS

tüm uygulamaların nix paketleme yöntemi ile yönetildiği linux tabanlı işletim sistemi.

# Guix 

Nix'in sadece açık kaynaklı paketleri kabul eden türevi.

# nix komutlar
> nix-env -qaP | grep -i vlc

search ignoring case. the list is not same as official web site. her satır bir uygulamayı gösteriyor. ilk sutun program için "attribute name" ikinci ise "package name".

> nix-env -i vlc

install vlc by package name. install komutunun parametresi regex'tir. bu sebeple sadecd "vlc" dediğimizde "vlc" regex'ine uyan tek bir sonuç var ise, o paketi yükler.

> nix-env -iA vlc

install vlc by attribute name

> nix-env -q

list all installed pagakes

> nix-env -e vlc

removes the package

> --arg config '{ allowUnfree = true; }'

bu parametre install ve update package komutlarına geçilebilir. böylece lisanslı paketlerde indirilmeye açık olur.

> nix-channel --update nixpkgs
> nix-env -u '*'

update nix packages.

> nix-collect-garbage -d
when you remove a package with -e, it only removes the symbolic links from user profile. to remove completly the packages from "nix store" use above command.

(with -d parameter we remove also the rollback (old generation) packages)

# remove nix
- If you dont use nix daemon, stop it.

- it is enough to remove the path variables of nix from current OS user. the path file is auto added by nix-installer here:

  $HOME/.profile

  remove this line:

  > if [ -e /home/user_name/.nix-profile/etc/profile.d/nix.sh ]; then . /home/user_name/.nix-profile/etc/profile.d/nix.sh; fi # added by Nix installer

- Also run this command (optionally): "sudo rm -r /nix"

- Also (optionally - because they are only folders) "rm $HOME/.nix-channels $HOME/.nix-profile $HOME/.nix-defexpr"

# wrapped vs unwrapped nix packages

ornegin firefox'un her iki prefix ile de paketi mevcut. wrapped olanı eklentilerin/patch'lerin kurulu oldugu pakettir. unwrapped ise saf halidir.

# firejail
bazı komutlar:

(diğer komutlar burada https://firejail.wordpress.com/features-3/man-firejail-profile/)

vlc komutunun sağında kalan her paraetre vlc'ye geçilir
> firejail vlc -file /videos/video.mp4

interneti devre dışı bırakmak için:
> firejail --net=none vlc

X'i farklı bir ekrandaymış gibi açar. bu sebeple firefoxu sanal bir penceredeymiş gibi görürürüz. açılan uygulama sistemden ekran görüntüsü alamayacaktır.
> firejail --x11 vlc

/root ve /home/user dizinleri artık tamamen boştur/sanaldır.
> firejail --private vlc

/home/user dizini artık /path1'dir.
> firejail --private=/path1 vlc

geçici oluşturulan /home/user dizinine path1'deki tüm dosyalar kopyalanır. sandbox kapandığında geçici olan home dizini silinir ve /path1 eskisi gibi kalır.
> firejail --private-home=/path1 vlc
> firejail --private-home=/path1/file1 vlc # sadece file1 geçici home dizinine kopyalanır

iki adet dns algılatırız
> firejail --dns=8.8.8.8 --dns=8.8.4.4 firefox

local network adreslerine erişememesi önceden hazır gelen nolocal.net dosyası
> firejail --netfilter=/etc/firejail/nolocal.net firefox

ip (ifconfig yerine kullanılıyor) komutunu sanal olarak bir network'e atadık. network bilgilerini (örnek mac adres) rastgele firejail tarafından üretiliyor. ip'yi elle verdiğimizi için rastgele üretilmedi. bu sanal network'un bağlı olduğu dış network eth1'dir. eth1 o sıra bilgisayarımızda ayakta olmalıdır.
> firejail --net=eth1 --ip=192.168.0.10 ip -c a

profil dosyasında komut satırında geçeceğimizi bir çok parametreyi bulundurabiliyoruz. bu şekilde komutlarımız daha kısa oluyor ve aynı profil dosyasını birçok  uygulama için kullanabiliyoruz.

eğer --noprofile parametresini vermezsek default olarak aynı executable isminde bir dosyayı firejail'in profilleri tuttuğu dizinde arar. eğer aynı isimde profil dosyası bulursa o profil dosyasını aktif eder.

--noprofile parametresi geçilmezse aynı zamanda şu da olur: default olarak bazı profiller otomatik devreye alınıyor. bu profil dosyaları okunduunda komut satırına log atılıyor.

> firejail --profile=/file.profile vlc

# Guix System Distribution (or GuixSD)

Guix paket yöneticisi içeren işletim sistemi.

# portableapps.com

sadece windows için uygulamaların portable hale getirildiği projedir. portable uygulamayı çalıştırmak için paket yöneticisine ihtiyaç yoktur.

# snap

container içinde masaüstü/sunucu uygulamaların çalıştırılmasını sağlıyor.

# snappy

snap app manager

# Snapcraft

"snap formatı"'na uygun uygulama paketlemek için gerekli tool.

# snap commands

- snap find vlc --> finds apps on market

- snap install vlc

- snap install --beta vlc 

- snap install --devmode vlc --> snap uygulamasının bazı dizinleri (örnek /etc/) okumaya yetkisi yoktur. bunu aşmak için tüm dizinlere yetki veriyoruz. 

- snap remove vlc

- snap list --all -> lists installed apps

- snap refresh vlc --> updates vlc

- snap disable vlc --> vlc'yi silinmiş gibi yapar fakat dosyaları kalır. eğer arkaplan servisi varsa önce onu stop eder. enable'da ise servisi varsa başlatır.

- snap services start docker --> servisi başlatır. her snap app'te servis olmak zorunda değil. arkaplanda sürekli açık duran sistem servisleri snap tarafından destekleniyor. posix'lerde loglar /var/log dizini altında saklanırlar. snap'in servislerinin log'ları da buraya düşmektedir.

# containerized apps HOME folder

Tüm uygulamalar normalde $HOME idizini içerisine tüm config dosyalarını kaydederler. Fakat containerized app'lerde farklı durum vardır:

- snap: /home/<user_name>/snap/<snap_app_name>/<app_version>/

- portableapps.com: portableappname/Data/ dizinini kullanıyor.

- appimage: executable dosya ile aynı dizinde ve aynı isimde suffixi ".home" olan dizini kullanıyor. eğer yok ise normal sistemdeki $HOME dizinini kullanıyor.

- nix: normal uygulamalar gibi sistemdeki $HOME dizinini kullanıyor.

- flatpak: normal uygulamalar gibi sistemdeki $HOME dizinini kullanıyor.

- docker: container içindeki /root dizinini kullanıyor. 

snap uygulamaları home dizininde şöyle seçenkerlerde sunuyor:

- /home/<user_name>/snap/<snap_app_name>/<app_version>/ --> burası app_version sürümü için home dizini

- /home/<user_name>/snap/<snap_app_name>/common/ --> tüm sürümler için rtak olan home dizini

- /home/<user_name>/snap/<snap_app_name>/current/ --> bu bir link. yüklü olan (enable olan) sürümün home dizinine link ediyor.

Snap uygulamaları home dizini gibi işletim sistemi root dizinini altında /var/snap/ dizininde de her uygulama için read-write yetki olacak şekilde dizin yapısı kurmuş durumda. burası tüm OS user'ları için ortak config'leri barındırıyor.

# containerized apps dizin yapısı

- portableapps.com: /<APP-NAME\>/App/

- appimage: kendisi zaten tek bir (portable) dosya.

- docker: o anda docker runtime'ı, dizinleri contaner'a mount ediyor.

- nix: işletim sistemi root dizini altında tek bir dizinde tüm dosyaları toplanmış durumda:

```
--/nix/

------/store/

------------/<HASH_OF_THIS_FILE_OR_DIR>-<PACKAGE_NAME>-<APP_VERSION>/ --> Burası dizin de olabilir sadece bir dosyada. her dependency içinde kendi dependency'lerini barındırmıyor. tüm dependency'ler de nix/sotree/ içinde.

------/var/

----------/profiles/

-------------------/<PROFILE_NAME_1>/

-------------------/<PROFILE_NAME_2>/

------------------------------------/bin/
```

Her user bir profil'e bağlanır. Her profil ise kendi içinde, nix-store'da yüklü olan aynı uygulamanın farklı sürümlerine bağlanır. Bu sürümlerin komut satırı executable'ları /<PROFILE_NAME_2>/bin/ içinde yer alıyorlar.

Dolayısı ile OS içinde yeni bir user'ın $PATH'ine /<PROFILE_NAME_2>/bin/ dizinini eklemek yeterlidir. artık tüm uygulamalar kullanılabilir olur.

$HOME/.nix-profile --> bu dizin buraya link ediyor: /nix/var/nix/profiles/<PROFILE_NAME_X>

- snap

işletim sistemi root içerisinde birçok dosyayı barındırıyor. fakat ekstradan işletim sistemi ile entegreli çalıştığından her tarafta sembolik linkler ve config dosyaları da barındırıyor.

```
--/snap/

-------/bin/ >-> executables of installed apps

-------/<APP_NAME>/

------------------/<VERSION>/

------------------/current/ ->link to enabled version
```

# nix vs docker

- nix namespace'leri kullanmaz. programlar normal masaüstü uygulaması gibi açılır. nix ile açılan uygulamada namespace'leri ayırmak istersek önüne firejail gibi uygulamalar kullanmamız gereklidir.

- nix herhangi bir package install ederken programı baştan local'de build eder ve mount-namespace'lerinden ve cgroups'tan yararlanır. onun dışında özel bir namespace teknolojisini kullanmaz.

- nix desktop uygulamalarda da kullanılabilmasi daha kolaydır.

- nix tamamen portable bir dizindedir. isteğe bağlı runtime servisi (daemon) açılabilir.

- nix update/değişiklik sonrası rollback işlemleri kolaydır. çünkü grupça tüm paketleri rollback yapabilir. git'teki gibi geri ileri alınabilir. docker'da bunu yapabilmek için docker'ın önünde kubernetes gibi yazılımlar kullanmak gerekir.

- dockerfile'de "apt-get update" işlemi yapıldığında paket indirme işleminin hangi paketleri indirdiği net değildir. oysa nix'te çok fazla paket detayına tek tek inilebilir. hem versiyon hemde sha hem de her paket için ayrı ayrı repo verilebilir.

- nixos sayesinde kernel modülü gerketiren uygulamalarda çalıştırılabilir. örnek virtualbox nixOS'ta sorunsuz çalışır.

# (appimage or chown) vs firejail vs snap vs container
container tüm kaynakları ilgili process için yeni yaratır. Sadece istediğimiz kaynakları process'in görmesini sağlarız (ayarlamamaız gerekir).

appimage ve chown sadece başlatılan process'in mount edilen root dizinini değiştirir ("mnt namespace" teknolojisinden yararlanır). diğer tüm kaynaklar OS'taki diğer process ile aynıdır.

snap ise bazı kaynakların (yarı yarıya diyebiliriz) yeni yaratılmasını sağlayarak process'i yürütür.

firejail ise varolan process'i hiçbir yeni kaynak yaratmadan başlatır fakat çok basitleştirilmiş komut satırı parametreleri ile yeni namespace'ler (kaynaklar) yaratabilmemizi sağlar.
