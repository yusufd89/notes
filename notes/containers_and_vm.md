############################

############################
# CONTAINERS AND VM
############################

############################

# Network drivers

# virtualbox network drivers
(network interface konusu başka başlıkta anlatılıyor.)

virtualbox network ayarlarında network bağdaştırıcısı eklerken birden fazla farklı ayar (driver) mevcuttur. bunlar:

- Not attached: network interface'si oluşturulur fakat internet bağlantısı olmaz.

- NAT

  Burada host ve guest işletim sistemi arasında private virtual bir network oluşturulur. host bir router gibi davranır ve NAT ile istekleri makineden dışarıya çıkarır. guest'in aldığı IP, private network içinden bir IP'dir. Host dışında bu sanal makineye erişmek için port-forwarding yapmak şarttır.

- NAT Network (or NAT Service)

  NAT yapısı ile aynı çalışmaktadır. Sadece NAT yapısında tek bir makine variken (çünkü "NAT" driver sadece 1 makineli private network yaratır) burada komple bir network vardır. Dolayısı ile yine VM'e bağlanan interface bir router gibi davranıp, sanal VM'lerden oluşan bir networku dışarıya NAT ile çıkarmaktadır. Doğal olarak; sanal/private networkte olan VM'ler birbirlerini de görebilmektedirler.

- bridge networking

  host'un bağlı olduğu DHCP'den yeni bir gerçek IP alır. DHCP'den iki tane IP alabilmek için farklı bir cihazmış gibi davrandırtıyor. Bunu yapabilmek için; Virtualbox kendi istekleri için sadece MAC adresi değiştiriyor. bu network çeşidi bazı işletim sistemi ve farklı donanım kartları/teknolojileri için desteklenemiyor (yada yarım destekleniyor yada çok farklı/dolaylı yöntemler uygulanmak zorunda kalınabiliyor).

- Host-only networking

  sanal bir ağ kartı yaratır. bu sanal ağ kartı içerisinde itediğimiz kadar VM'i birbiri ile iletişime geçirebilir. dış dünya ile iletişimde olmazlar. sadece kendi aralarında haberleşiler. istenildiği kadar sanal ağ kartı yaratılıp, VM'ler kendi içinde gruplandırılabilir. sanal ağ kartının yanında, networkte sanal DHCP sunucuda yaratılmaktadır (virtualbox ayarlarından).

- Internal networking

  Host-only networking yöntemi ile apaynıdır. sadece sanal bir kart yaratılmaz. sanal bir kart yaratılmaması; varolan bir fiziksel kartın kullanılmasına sebep olur. Böylece wireshark gibi bir uygulama ile 'Internal networking'e bağlı VM'lerin network trafiğini izleyebiliriz.

- UDP Tunnel Networking

  farklı host'ların ortak network yönetimi yapılabilmesini sağlayan bir driver'dır.

- VDE Networking

  farklı host'ların ortak network yönetimi yapılabilmesini sağlayan bir driver'dır.

Virtualbox ortamında birden fazla ağ bağdaştırıcısı eklenebilir. Dolayısı ile örneğin; bir VM içerisindeki işletim sistemi hem "internal network" ile diğer VM'ler ile haberleşirken, "NAT" bağdaştırıcısı ile internete çıkabilmektedir.

# ("host-only" and "internal networking") vs ("NAT" and "NAT Network")
"host-only" and "internal networking" private network'ten dışarıya virtualbox'un engine'inde olan sanal bir "Switch" cihazı simülasyonu ile çıkarken, "NAT" and "NAT Network" yine virtualbox'un yarattığı sanal bir router ile dışarıya çıkar.

# Docker network drivers

- none

  internet container içerisinde tamamen kapalıdır.

- bridge

  default network type. sanal interface yaratılır. bu interface üzerinden sadece bu bridge bağlı container'lar birbirlerini görür. bu container'lar private bir sub-network içerisindedir.

  bridge'yi router gibi düşünürüz. dolayısı ile bir container'a erişmek için port-forwarding (port exposing) yapmamız şart.

- overlay

  kelime anlamı: kaplama/örtü

  bridge mantığını multi-host üzerinden yapabilmemizi sağlar. yani 2inci bir hosttaki bir container, 1inci hosttaki bir container ile aynı networkteymiş gibi davranabilir.

- host

  container kendi ip'sini almaz. host ile aynı network namespace'sini kullanır. yani container içerisinde çalışan process, host'ta çalışıyormuş gibi düşünebiliriz. bu sebeple "-p" ile yapılan port forwarding'lere ihtiyaç yoktur (ignore edilirler).

- macvlan

  container'a bir mac adresi atar ve host'un networkünde gerçek IP almasını sağlar. bu genelde subnetworking üzerinden işlem yapamayan legacy uygulamalar için kullanılabilir.

  hostun bulunduğu network'ün bilgilerini vermek zorundayız.

  ```sh
  docker network create -d macvlan \
                      --subnet=172.16.86.0/24 \
                      --gateway=172.16.86.1 \
                      -o parent=eth0 pub_net
  ```

  parent olarak ne vereceğimiz çalışma modu'nu belirleyecektir:

  - bridge mode

    direk olarak gerçek fiziksel kartımız üzerinden çalışır. bu sebeple gerçek fiziksel interfacemizi parent'a yazmak zorundayız.

  - 802.1q trunk bridge mode

    sanal yaratılan bir interface üzerinden fiziksel karta bağlanır. böylece host'un interface'sinde olan routing veya filter'lara takılmamış oluruz.

    parent'a "eth0.50" gibi docker engine'in belirttiği şekilde isim vermeliyiz.

- docker plugin'lerinde 3üncü parti network plugin'leri kurup aktif hale getirebiliriz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Sanallaştırma kavramları

# Hypervisor (or virtual machine monitor or VMM)

sanal makine yönetimini yapan yazılımlara verilen gelen isimdir.

hypervisor run edildiği katmana göre 2'ye ayrılır:

#### Type-1 (or native or bare-metal hypervisors)

işletim sisteminin kurulu olmasını gerektirmez. direk donanım ile temasta olan ilk katmanda bulunur. Hypervisor üzerine bir den fazla işletim sistemi kurulur.

Örnek: Microsoft Hyper-V (linux'u da desteklemektedir), Xen, VMware ESXi (or eski adı VMware ESX)

#### Type-2 (or hosted hypervisors)

işletim sistemi üzerine yüklenirler ve sanal makine içindeki uygulamaları host donanımın anlayacağı dile çevirir.

örnek: virtualbox, QEmu (or Quick Emulator)

# Donanım sanallaştırma (or platform sanallaştırma)

kurulan işletim sistemlerine donanımları paylaştırma işlemidir. hypervisor'ler bu paylaştırma işlemini yönetir. hypervisor'ler donanımları paylaştırma işlemlerine göre 3'e bölünürler:

- Tam Sanallaştırma: tamamiyle sanal olarak bir donanım yaratılır ve işletim sistemlerine bu donanım kullandırtılır.

- Para-virtualization: gerçek donanımlar direk olarak işletim sistemlerine bağlanır. sanal donanım hiç yoktur.

- Kısmi Sanallaştırma: para ve tam arasında olan bir mekanizmadır. işletim sistemlerine bazı donanımlar sanal verilirken, bazı donanımlar sanal yaratılıp verilir.

# KVM (or Kernel-based Virtual Machine)

özel bir isimdir. KVM linux modülüdür, hypervisor'dür. işletim sistemi modülü olduğu için type-1 veya 2 olduğu tartışılır. sanal makinede olan işlemleri host'un anlayacağı dile çevirmez. bu sebeple type-1 olarak algılanabilir. fakat çekirdek üzerine kurulu olduğundan type-2 gibi düşünülebilir çünkü tüm guest'ler host makinanın birer process'iymiş gibi çalışmaktadır.

# Parallels Desktop (or Parallels Desktop for Mac)

mac için hypervisor.

# yazılım sanallaştırma

docker gibi uygulamalra verilen genel isimdir. uygulama çalıştırma seviyesinde olur, işletim sistemleri seviyesinde bir kavram değildir.

# intel VT-x vs AMD-v

Sanallaştırma teknolojileri için işlemcilerin yapmış olduğu yeni teknoloji isimleri.

# Nested virtualization

içiçe sanallaştırma yani; sanal makine içinde sanal makine çalıştırmaktır.

# VMware ThinApp

VMware'in uygulaması, yazılım Sanallaştırması yapar. İşletim sisteminde bir uygulamanın sanal olarak yürütülmesini sağlar. Varolan işletim sisteminin dosyalarını elleyemezler.

# Emülator (or öykünücü) vs simulator (or simülatör)

emülatör gerçek sistemi bir sandbox'ta çalıştırıp sunarken, simülatör gerçek sisteme en yakın (benzeri) modeli sandbox'ta sunmaya çalışır. örnekler:

- para-virtualization, emülatör yada simülatör değildir. çünkü donanımı direk olarak yazılıma verir ve üzerindeki sistemler sandbox'ta çalıştırılmaz. sadece işletim sistemleri birbirinden bağımsız (birbirini görme yetkisi olmadan) çalışır. 

- full ve partirial virtualization emülatördür. android sdk'sında gelen android sanal makineleri bu gruba girer. virtualbox bu gruba girer. guest sistemler gerçek setup (örneğin iso) dosyalarından kurulur.

- eğitimlerde kullanılan uçak yada araba oyunları birer simülatördür.

# VirtualBox OSE (or VirtualBox open source edition)

Virtualbox 4üncü sürümden önce kapalı kaynak ve açık kaynaklı sürüm olarak dağıtılıyordu. 4 üncü sürüm ile birlikte ikisi birleştirildi. ve lisans gerektiren ek özellikler; kapalı kaynak eklentiler olarak indirilebiliyor.

# VMware

VMware'in birçok farklı ürünü mevcut. Tüm ürünler kapalı kaynaktır.

# VMware Workstation (or VMware Workstation Pro)

Sanal makina çalıştırıcısıdır. lisans gerektiren versiyon.

# VMware Workstation Player (or VMware Player)

kisisel kullanim için ücretiz sunuluyor. VMware Workstation'dan farklı bir executable olup, eksik özellikler içeriyor.

# VMware Fusion

Mac'in altyapısı farklı olduğundan, mac versiyonu farklı build üretilmiştir.

# Gnome-boxes

gnome projesi altında dağıtılan sanal makina yöneticisi için GUI'dir. Arkaplanda kendi teknolojilerini kullanmaz. Sadece GUI ile sanal makine yönetim (oluşturma, silme, açma...) işlerini kolaylaştırır.

# Virtual Machine Manager (or virt-manager)
Genel bir terim gibi görünsede özel bir uygulama ismi. Gnome-boxes gibi sadece GUI'dir.

# Vagrant

Virtualbox, VMWare gibi uygulamaların içeirisinde olan makinaları, dcoker tarzı yönetimini sağlayabilmemizi sağlayan açık kaynaklı bir komut satırı uygulamasıdır.

Örneğin; Virtualbox üzerinde çalışan Windows-guest içerisinde komut çalıştırmamızı, disikin image'ini hazır indirmemizi, gibi işlemleri kolayca yapabilmemizi sağlar. BUnları yaparken VMWare ile de yapabilmemizi sağladığı için tek bir interface aracılığı ile yönetebilmemzi sağlar.

işletim sistemini hazır bulut imagelerden indirip açar, run edip, bir user tanımlar, bu user'ın içine ssh atar ve ssh komutu ile içine girip istediğimizi çalıştırabilmemizi sağlar.

# chroot
teknoloji bazında alternatifi: __systemd-nspawn__

unix-like sistemlerde bir dizini root olarak belirleyip, o dizin içerisinde bir uygulamayı run etmeye yarayan programdır. run edilen uygulama o dizini root olarak görür ve üst dizinleri kullananamaz. bu durum run edilen uygulamayı hapse atmaya benzetilebilir. fakat pratikte; bir uygulama birçok kütüphaneye, dosyayı kullanır. böyle durumlar için uygulamayı run etmeden önce, istenilen dizinleri, chroot altındaki dizinlere mount etmek gerekir.

bir uygulamayı execute ederken, sanal dizin altında olabilmesini sağlayan bir komuttur. Chroot'un Sanallaştırma gibi bir amacı yoktur.

chrrot ile önce boş bir dizin yaratılır. artık burası koşucak uygulamanın root dizinidir. buralara artık bağımlılıkları da atmak gereklidir. sadece bağımlılıklar diil, posix'te herşey dosya olduğundan stream out in, gibi dosyaları da kaydetmek gereklidir. tüm bir işletim sistemini hazırlamak gereklidir. bu elle zor olduğundan genelde chroot türevi  hazır paket yazılımlardan yararlanılır. yada varolan sistemdeki dizinler direk olarak chroot'un root dizini altındaki yerlere mount edilir. bu şekilde örneğin sistemimizdeki /etc dizinini komple chroot içine bağlamış oluruz.

# container vs VM
container işletim sistemi çekirdeği içermez. vm içerir.

# app container vs system container (or Operating System Container)

  - ## terminoloji
    - app container sadece bir process içerir. system container ise birden fazla process içerir. kaynak: (source-id: 241) "System Containers" başlığı 1inci paragraf.

    - "__System container__" terimi redhat tarafından multiprocess dışında bir anlamda kullanılmaktadır. kaynak: (source-id: 242) "System containers provide a way to containerize services that need to run before the docker daemon is running".

    - __system container__' ile "__Operating System Container__" eş anlamda kullanılır. kaynak: (source-id: 243) 1inci paragraf, ilk cümle.

    - "__Operating System Container__" terimi pek çok kaynakta yer almaz. genelde "__system container__" terimi tercih edilir. "__Operating System Container__" multiprocess içeren container'lardır. kaynak: (source-id: 244) "Operating System Containers" başlığı.

  - ## neden birden fazla process'e ihtiyaç var
    system container'ın birden fazla process içermesinin sebebi; işletim sistemi çekirdeği haricinde tüm dependency'lerini (sadece kütüphane (dosya) değil, process dependency'leri de) kendi container'ı içinde bulundurur. yani birden fazla process içerirler (örnek systemd, SysVinit, Upstart, OpenRC...).

    multiprocess açmaya ihtiyaç olması için örnek process'ler:

    - ssh server 
      
      kaynak: (source-id: 243) 2inmci paragraf.

    - crond 
    
      kaynak: (source-id: 243) 2inmci paragraf.
    
    - syslogd

      kaynak: (source-id: 243) 2inmci paragraf.
    
    - side-car pattern'i uygulayabilmemiz için, birden fazla process aynı container'da çalıştırılabilir.
    
      kaynak: (source-id: 248)

    - eski bir uygulamayı container'da çalıştırmak istediğimizde onun dependency'lerini de çalıştırmak zorunda kalabiliriz (bu madde yukarıdaki syslogd ile aynı şeye denk geliyor)

    özellikle multiprocess içeren container üzerine uzmanlaşmış platformlar: BSD jails, Linux vServer, Solaris Zones, OpenVZ/Virtuozzo, LXC/LXD kaynak: (source-id: 243) son paragraf.

# VM vs container runtine (optionally with container engine)
karşılaştırılmaları doğru diil. biri vm container'ı, diğeri uygulama container'ı.

- VM'in açılması dakikalar alırken, containerruntime saniyeler alır.

- VM fully portable'dır. fakat container runtime diildir. container runtime işletim sistemini sanallaştırmıyor. varolan OS çekirdeğini kullanıyor. bu sebeple başka makinaya atılan container, aşağıdaki durumlarda farklı tepkiler verebilir:

  - OS çekirdeği farklı sürüm ise
  - OS çekirdeği farklı ise
  - çekirdeğin bazı özellikleri aktif ise, başka makinada aynı özellikler aktif olmayabilir (örnek linux kernel module)
  - donanım farklı ise (özellikle donanıma bağlı kodlarda) (bu durum kısmen VM'de de var)

# container runtime
- LXC
- libcontainer
- runc
- crun
- railcar
- katacontainers
- containerd (runc'yi wrap ediyor/kullanıyor.) ("__ctr__" komut satırı client uygulamasıdır.)

yukarıdaki liste için kaynak: (source-id: 244) "Container Runtime" başlığı.

Birçok container runtime "__Open Containers Initiative (or OCI)__" standartlarına uyar. OCI'nin referans implementasyonu runc'dir.

Tüm container runtime'ler, linux'un içinde native gelen "cgroups" ve "Linux namespaces" özelliklerini kullanarak çalışır. Ek olarak SELinux ve AppArmor gibi özelliklerden de sıkça yararlanır.

# Container engines
LXC gibi özelliklerin son kullanıcı tarafından direk kullanılması zordur çünkü alt seviyelidir. Bu yüzden docker ve LXD gbi projeler ortaya çıkmıştır. 

| container engine name | company                           | based on container runtime                                         |
|-----------------------|-----------------------------------|--------------------------------------------------------------------|
| Docker                | Docker Inc                        | Sırası ile bu teknolojiler kullanıldı: 1-LXC 2-libcontainer 3-runc |
| LXD                   | canonical                         | lxc(linux containers) developing by Canonical                      |
| Rkt (or Rocket)       | Red Hat (CoreOS Team)             |                                                                    |
| CRI-O                 | Cloud Native Computing Foundation | runc                                                               |
| Podman                |                                   | runc                                                               |

yukarıdaki liste için kaynak: (source-id: 244) "Container Engine" 1inci paragraf.

# Container Orchestration
container engine'leri wrap eder ve sayı olarak fazla/karmaşık olan systemimizi daha rahat düzenlememizi sağlar.

- kubernetes
- istio (based on kubernetes)
- openshift (based on kubernetes)
- swarm (develop by Docker Inc)
- UCP (or Universal Control Plane) (develop by Docker Inc)
- Mesos (develop by Apache)

yukarıdaki liste için kaynak: (source-id: 244) "Container Orchestration" başlığı son paragraf.

# container runtime vs container engine
aşağıdaki tüm bilgiler buradan kopyalanmıştır: (source-id: 244) "Container Runtime" başlığı ve "Container Engine" başlığı.

The container runtime is responsible for:

- Consuming the container mount point provided by the Container Engine (can also be a plain directory for testing)
- Consuming the container metadata provided by the Container Engine (can be a also be a manually crafted config.json for testing)
- Communicating with the kernel to start containerized processes (clone system call)
- Setting up cgroups
- Setting up SELinux Policy
- Setting up App Armor rules

the container engine is responsible:

- Handling user input
- Handling input over an API often from a Container Orchestrator
- Pulling the Container Images from the Registry Server
- Expanding decompressing and expanding the container image on disk using a Graph Driver (block, or file depending on driver)
- Preparing a container mount point, typically on copy-on-write storage (again block or file depending on driver)
- Preparing the metadata which will be passed to the container Container Runtime to start the Container correctly
  - Using some defaults from the container image (ex.ArchX86)
  - Using user input to override defaults in the container image (ex. CMD, ENTRYPOINT)
  - Using defaults specified by the container image (ex. SECCOM rules)
- Calling the Container Runtime

# podman
Pod Manager'in kısaltmasından özel isim türetilmiştir.

podman; resmi sitesinden "daemonless container engine" olarak geçiyor. çünkü bir engine'e ihtiyacı yok. zira kendisi (sadece client komut satırı uygulaması) linux'un içerisinde gelen teknolojileri kullanıyor. Dolayısı ile ek kurulumda gerektirmiyor.

root yetkisiz de process açabiliyor (tabi kısıtılı özellikler sunarak).

# cgroups (or control groups)
linux üzerinde proseslerin cpu, memory, network gibi kaynaklardan ne kadar öncelikli yararlanabileceği, yada limitli yararlanabilmeleri için yönetimi sağlayan linux çekirdeğinin native özelliğidir.

# Linux namespaces
linux üzerinde proseslerin hangi kaynakları diğer prosesler ile ortak kullanıp kullanamayacağını belirleyen native linux özelliğidir. örneğin;

- Mount: bir grup proses, bir dizini görebilirken diğer hiçbir proses göremeyebilir.

- Network: birden fazla network interface'si (eth, wifi..) birden fazla network namespace'sine bağlanır. network namespace'si iptable gibi rouing ayarlarını içerir.

- IPC: IPC namespaceleri vardır. bir ipc namespace'si içindeki diğer ipc'lere mesaj atamaz.

- PID: process id grubu oluşturuluyor. bu şekilde, X pid namespacesi'sindeki process'ler sadece brbirlerini görebiliyor.

- uts: domain ve host name'leri okurken farklı gruplar yaratabiliyoruz

- User: bir process başlatıldığında o process'in kendini X user'ı ve Y grubu altındaymış gibi sanmasını sağlayabiliyoruz.

- cgroup: bu kısıtlama yapmaya yarayan cgroup özelliği değildir. bu bir namespcace'tir. çalışacak process'in kendini  bir croup kısıtlaması altında olduğunu sanmasını sağlayabiliriz.

bazı kaynaklarda sadece 'namespace' olarak geçer, bu sebeple karışıklığa sebep olabilir, zira 'namespace' kelimesi birçok farklı alanda kullanılmaktadır.

> /proc/<PROCESS_ID>/ns/

dizini altında o process'in tüm namespace'leri ayrı ayrı link dosyalarıdır: 

> /proc/<PROCESS_ID>/ns/ipc

> /proc/<PROCESS_ID>/ns/mnt

İşte bu dosyalar link olduğundan, örneğin X namespace'sine link eder. İşte o proceess'i Y namespace'sine yönlendirirsek o zaman container/sandbox yapmış oluruz. 

# sandbox vs container

conitaner içinde uygulamalar çalıştırabilmek için (yani yeni namepscae'ler yaratabilmek için) root yetkisine ihtiyaç vardır. fakat sandbox için root yetkisine gerek yoktur. örnek docker root yetkisi ister, fakat google chrome sandbox için user yetkisi yeterlidir.

# init process
işletim sistemi servis ve program yönetimi yazılımlarına verilen genel isimdir. sistem başlangıcında ilk başlayan işlemdir. bu sebeple __init process__ olarakta adlandırılırlar. tüm servisler ve process'lerin yönetimini sağlar. OS çekirdeği tarafından başlatılır. kaynak: (source-id: 254) 1inci paragraf.

process id'leri 1'dir.

init process'ler bir OS içerisinde birkaç tane olabilir. bunun için bazı örnek durumlar:
- her container içerisinde init olabilir
- her OS user'ı için ayrı init olabilir. kaynak: kaynak: (source-id: 254) "NOTES" başlığı, 1inci paragraf.

Unix dağıtımlarda ilk geliştirilen init "System V" isim ile dağıtılan dağıtımda kullanılıyordu. Bunun çıkması ile birlikte birçok linux dağıtımı dahi, buna uyumlu init sistemleri ile dağıtılıyordu. herkes kendi init'ini yazıyordu. bu sebeple bu tarz init'ler için "System V style init", "traditional init" gibi terimler kullanılır.

şu anda piyasada birçok init alternatifi mevcut: systemd, upstart...

"init" daha çok sıralı bir açılışa ağırlık verir. örneğin; update hizmeti, log servisine bağlı ise önce log servisinin başlatılması beklenir. hazır olunca update servisi başlar. oysa systemd'de işlemler paralel başlatılır. birbirlerine depend eden istekler beklemeye alınır. işlemler paralel başladığından CPU daha az boşta kalır ve daha hızlı açılış gözlenir.

systemd vs Upstart için komut satırı uygulamaları mevcut. bunların kullanım örnekleri aşağıdadır:

| Operation                          | Upstart Command                   | Systemd command                   |
|------------------------------------|-----------------------------------|-----------------------------------|
| Start service                      | start $job                        | systemctl start $unit             |
| Stop service                       | stop $job                         | systemctl stop $unit              |
| Restart service                    | restart $job                      | systemctl restart $unit           |
| See status of services             | initctl list                      | systemctl status                  |
| Check configuration is valid       | init-checkconf /tmp/foo.conf      | systemd-analyze verify $unitFile  |
| Show job environment               | initctl list-env                  | systemctl show-environment        |
| Set job environment variable       | initctl set-env foo=bar           | systemctl set-environment foo=bar |
| Remove job environment variable    | initctl unset-env foo             | systemctl unset-environment foo   |
| View job log                       | cat /var/log/upstart/$job.log     | sudo journalctl -u $unit          |
| tail -f job log                    | tail -f /var/log/upstart/$job.log | sudo journalctl -u $unit -f       |
| Show relationship between services | initctl2dot                       | systemctl list-dependencies --all |

not: "service" komutu bir shell script dosyasıdır ve init process türünü bilmeden işlem yapabilmemize olanak sağlayan bir wrapperdır.

Systemd servisleri başlatırken hangi servisleri başlatacağına target'lar aracılığı ile karar verir. örneğin sunucumuzda grafik arayüzü hiç kurulmamış ise, daha sonra gui kurarsak ve varsayılan olarak gui servislerinin açılmasını istiyorsak, default target'ı değiştirmeliyiz:

> systemctl set-default graphical.target

otuput:

```
Removed symlink /etc/systemd/system/default.target.
Created symlink from /etc/systemd/system/default.target to /usr/lib/systemd/system/graphical.target.
```

sistemde varolan target'ları görebilmek için:

> systemctl list-units --type=target

# Docker

linux'larda run edilen uygulamaların birbirinden habersiz çalışması, "Linux Containers (or LXC or runC)" isimli yapı ile zaten sağlanmaktadır. yürüyen uygulamalar birbirinden sadece port yada sadece dosya sistemlerini ortak yada bağımsız kullanmaları sağlanabilir. Varolan bu teknolojinin konfigürasyonu zor ve ayrıntılıdır. Docker bu yapıyı değiştirerek (libcontainer isimli proje ile) ve kolaylaştırarak kullanıcıların rahatça izole ortamlarda (container'larda) uygulama yürütebilmesini sağlamaktadır.

# linux dışındaki işletim sistemlerinde docker nasıl çalışıyor

docker sanal makine kurmamakta yada çalıştırmamaktadır. ve "container" yapısı sadece linux'ta vardır. fakat windows ve mac container yapısı desteklememektedir. docker uygulaması windowsa yada mac'e kurulduğunda, çalıştırılacak uygulamalar linux tabanlı olduğu için, docker kendi içinde bir sanal linux makinesi kurmaktadır (docker-machine aracılığı ile kuruyor. "Tiny Core Linux" türevi olan boot2docker isimli işletim sistemini çalıştırıyor). Bu makine üzerinde uygulamaları yürütmektedir. bu işlemleri docker harici bir firma boot2docker isimli uygulama ile yapmaktadır. ve arkaplanda sanal makine kurduğunu da önyüzde göstermemektedir. işletim sistemi boot2docker iken, bunu virtualboxu otomatik kurup yönetem uygulama boot2docker-cli'dir. artık docker-machine komut satırı uygulaması ile docker firması bu işi üstlenmektedir. bu sebeple boot2docker projesi artık geliştirilmiyor.

docker varolan işletim sisteminin çekirdeğini kullandığı için (ortada ikinci işletim sistemi olmadığı için), hypervisor gibi işlemci teknolojilerine bağımlılığı yoktur. en azından linux için bu şekilde. fakat windows ve mac 2016 yılı sonrası sürümleri itibari ile container yapısını desteklemeye başlamıştır. fakat teknik altyapıda donanıma bağımlılık vardır. hyper-v tarzı teknolojilere dayanmaktadırlar.

# Docker Daemon (or docker engine)

Dcoker'ın containerları yönetebilmesini sağlayan yazılımıdır. libcontainer tabanlıdır. bir nevi hypervisor görevi görür.

# docker command line interface

docker uygulamasının bir client'ıdır. docker deamon'a erişir. docker deamon'a CLI'den erişmek zorunlu değildir. API kullanılarak bağımsız client'lar yazılabilir. erişim TCP socketleri ve HTTP istekleri üzerinden yapılabilmektedir.

# docker server vs docker client

her makinede ikisi yada sadece bir tanesi yüklü olabilir. server docker engine'dir. dockerları o makinede koşabilir. client ise user isteklerini docker server'a gönderebilme yeteneğine sahiptir.

# Docker Registery

internette bulunana hazır container repo hizmetlerinin genel adıdır.

# Docker Hub

Docker firmasının sunduğu resmi 'Docker Registery'sinin ismidir.

# Docker-compose

Yaml konfigürasyon dosyasını parametre olarak alır ve bu konfigürasyonlara göre birden fazla docker container'ını ayağa kaldırır. Kolay bir konfigürasyon dosyası olması ile ön plana çıkar. komut satırında bizim uzunca yazacağımız şeyleri kısaltmış olur.

docker-compose configürasyon dosyasının (yml) birçok sürümü vardır. dosyanın içinde en başa version belirtilmelidir. "version:3", "version 3.0" ile aynı anlama gelir. Tüm sürüm listesi buradadır: https://docs.docker.com/compose/compose-file/compose-versioning

"links" özelliği docker compose'da varken, stack'te yoktur. fakat stack'te olan bazı özellikler, docker-compose'da yoktur. 

```yml
links: # aşağıdaki servisler artık hostname üzerinden erişilebilir olur. bu servislerin network'leri mutlaka "links"i koyduğumuz container'ın networkü ile aynı olmalı.
      - db # service_name
      - db:database # service_name:alias
      - redis # service_name
```

# stack

swarm modülünden bağımsızdır. stack docker-compose'un gelişmişidir. swarm özelliği gibi docker-compose'un yapamadığı bir çok özelliği destekler.

v3 yml örnek dosya:

```yml
version: "3"

services:  #service tanımı baska bir başlıkta anlatılıyor

  web:  #docker servisinin adı. daha sonra bu ismi kullanarak docker-compose komutları ile ekrsta işlemler yapabileceğiz

    build: # service imageden değilde, dockerfile'dan oluşturulacaksa bu kısım eklenir

          dockerfile: /my/dir/dockerfile

          args:    # dockerfile içinde args varsa kullanılabilir

              PI = 3

    image: myusername/myrepo:mytag  #bu servis hangi imageden oluşturulacak. eğer bu varsa "build" property'si olmamalı.

    environment: # dockerfile içindekileri override edebilmek için kullanılır

             PROFILE: "docker"

             ANDROID_PATH: "/root/sdk/android"

    hostname: "web_domain_name" #diğer container'lar bu domain name ile bu container'a erişebilecek

    depends_on:  #bu conitanerlar baslamadna bu baslamaz

             - configserver

             - discoveryserver 

    

    deploy: 

      replicas: 5  #bu servise bağlı 5 tane container oluşacak

      resources:

        limits:

          cpus: "0.1"  #her container bu makinedeki tüm cpu'ların max %10'unu harcayabilir.

          memory: 50M  #her container max 50 mb ram harcayabilir

      restart_policy:

        condition: on-failure

      placement:

        constraints: [node.role == manager] # manager tipindeki node'larda bu container çalışacaktır. yada farklı seçenklerde var. 

                                            # örnek: [node.labels.layers == xxx] --> xxx label'ı verilmiş node'larda koşucak. 

    ports:

      - "80:80" #iceriden disariya olan port yönlendirme

    networks:

      - webnet #varolan hangi networke bagli olacak. bu özellik yeni geldi.

networks:

  webnet #bir network ismi
```

# cgroups ve linuxnamespace ayarları

(ne oldukları başka başlıkta anlatılıyor)

her container için ayrı ayrı ayar verilebilir. linuxnamespace'ler docker tarafından otomatik ayarlanıyor. oysa yukarıdaki docker compose örneğinde görüldüğü gibi cgroups'lar user tarafından configüre edilebiliyor (örnek: cpu 0.1 gibi).

# docker swarm

swarm türkçe kelime anlamı: sürü

dockerın içinde gelen bir modüldür. docker'da cluster/scale işlemlerini yapar. instance'ları(container'ları) scale ederek arttıran ve önlerine otomatik load balancer koyabilme yeteneklerine sahiptir. 

# Universal Control Plane (or UCP)

birçok makinadaki docker-daemonlar tek bir noktadaki bu sunucu tarafından Web-GUI ile yönetilebiliyor/monitör edilebiliyor.

# ucp-agent (or ucp node)

2 çeşittir:

- manager: web-ui'ı sunar ve worker'lara komut gönderir.

- worker: docker conitaner'larını çalıştırır.

manager özelliğine sahip bir node'da isterse container çalıştırır fakat bu pek tavsiye edilmez. sadece hızlı test için, deneme amaçlı kurulumlar yapılması için manager'ların container çalıştırması serbest bırakılmıştır.

manager ve worker node'ları aynı sistemde birden fazla olabilir.

# ucp bundle (or ucp client bundle)

ucp panelden download edilir. biz zip dosyasıdır. içinde gerekli anahtarlar ve komut satırı scriptleri bulunur. bu scirptler kullanılarak direk docker yürklü bir makinadan ucp-web-ui-panelindyemiş gibi komut satırından işlem yapılabilmesini sağlar. 

# service

service bir conitaner instance'ı değil. örneğin yukarıda 1 service'e bağlı 5 instance oluşturduk. istersek hemen 10 tane daha ekleyebiliriz. servise yaptığımız ayar o servise bağlı tüm container'lara otomatik yapılmaktadır.

servis tanımımızı güncellediğimiz zaman o service'den türemiş tüm containerlar kapanır ve yeni tanımlama ile tekrar açılırlar.

# service types

Global service: her yeni worker node kelendiğinde bu servislerden birer instance otomatik o workderda açılmaktadır. firewall/antivirüs, monitor-agents gibi uygulamalarımız burada olabilir.

Replicated service:  İlgili servisten kaç adet instance'ın çalışacağına sizin karar verdiğiniz servis tipidir.

# docker machine

ek bir komut satırı uygulaması. bu uygulama ile yeni sanal işletim sistemleri kurabiliyoruz. bu şekilde container desteklemeyen işletim sistemlerinde, kolayca linux sanal makine yaratarak onun üzerinde docker çalıştırmamızı sağlamaktadır. aynı şekilde sadece localde değil, uzak bilgisayarlardaki sanal makineler üzerinde de çalışabilmemizi sağlamaktadır.  

docker machive windows ve linux'ta virtualbox kullanırken, mac'te HyperKit kullanmaktadır.

docker machine driver'ları sayesinde vmware, virtualbox, Microsoft Azure, Amazon Web Services gibi birçok  clodu makina sistemlerine veya sanal makine yöneticilerinde uzaktan işlem yapabiliyoruz.

# docker toolbox

docker engine + docker compose + docker machine + Kitematic uygulamasını bir arada sunan bir setup'tır.

windows ve mac native destek sağladıklarından beri artık bu pakete destek kaldırıldı. windows ve mac'e kurulumlarda "docker for windows (or Docker Desktop for Windows)" veya "docker for mac (or Docker Desktop for Mac)" kurulması öneriliyor.

docker for windows ve mac kubectl ve minikube yazılımını da içinde bulundurmaktadır.

# Kitematic

cross platfrom docker client GUI'sidir.

# docker tooling

Eclipse için docker client eklentisidir. dockerların içine komut yazabilmemizi de sağlıyor.

# docker container vs docker image vs docker file

docker file, docker image'i yaratmak için docker'ın anlayacağı tipte bilgiler/komutlar içeren dosyadır. bu dosya işlenerek (build işlemi) image image yaratılır.

docker image, docker file ile yaratılmış run edilmeye hazır sanal pakettir.

docker image run edildiğinde, docker container olur.

# docker file

örnek docker file:

```docker
FROM ubuntu # Docker container ilk açıldığında, boş bir dosya sistemi oluşturur. Burada bir işletim sistemi kullanmak gerekli. Bu şekilde temel kütüphaneler dosya sisteminde bulunmuş olur.

ARGS PI = 3 # container içinden bu değer okunamaz. komut satırından override edilebilir: "docker build --build-arg PI=4"

ENV ANDROID_HOME /my/dir # yada ENV ANDROID_HOME=/my/dir. Args ile aynı çağrılır. komut satırından override edilebilir: 'docker run -e "ANDROID_HOME=/my/another/dir"'

COPY /source/dir:/dest/dir #container dışındaki bir dizini yada dosyayı container içine kopyalar

ADD /source/dir:/dest/dir # copy ile aynıdır. ekstra olarak ADD; eğer source url ise onu indirir ve eğer source arşiv dosyası ise (tar, zip) onu açıp kopyalar.

RUN echo "hello number $some_variable_name" # yada "hello number ${some_variable_name}".

RUN apt-get install nodejs # sadece "docker build" komutu ile çağrılır. 

CMD ["/usr/bin/node", "/var/www/app.js"] # sadece "docker run" komutu ile çağrılır.

ENTRYPOINT ["/usr/bin/node", "/var/www/app.js1", "/var/www/app.js2"]   # CMD ile aynı görevi görür. tek farkı docker'ı run ederken, ek parametreler alabilir. "docker run myImage /var/www/app.js3" komutu ENTRYPOINT'e 3üncü parametreyi ekleyecetir.
```

# app installation with user password

example: 

> apt-get install wget

This command will ask "yes or no"? The only way to bypass this action is possible by apt-get feature:

> apt-get get "-y" 

parameter and check the user has the privilages to install the wget app. 

# userName/containerName vs containerName vs myhub.mysite.com:8081/myContainerName

Docker file'da her iki formatta da paket indirilebilir. userName olmadan indirilenler docker tarafından resmi olarak tag'lenmiş anlamına gelmektedirler.

"docker registry" açık kaynaklı yazılımları bulunmaktadır. self-hosted şekilde kendimize yaratabiliriz. böyle durumlar için, ip'si verilmiş makineden de image çekebilir.

# host os (or Container OS)

docker deamon'u çalıştıran işletim sistemidir. bu herhangi bir kullandığımız son kullanıcı os'u olabilir. fakat bazı OS'lar sadece docker yürütmek için tasarlanmıştır. içinde gereksiz paketler yoktur.

örnek:
- Snappy Ubuntu Core
- CoreOS (kaynak: (source-id: 256) "Custom operating system" başlığı. )
- RancherOS
- Project Atomic
- Photon

# Snappy Ubuntu Core (or Snappy Ubuntu or Ubuntu Core)

Sadece snap uygulamaları barındıran minimal bir ubuntu türevidir. docker'ın snap paketi olduğundan sadece docker kurulu şekilde kullanılması tercih edilebilir. yada iot cihazlarında tercih edilmektedir.

# Base OS (or base image os)

container içinde koşan işletim sistemidir. FROM komutu ile işletim sistemi baz alınırken, işletim sisteminin minimum olması beklenmektedir. bu durum; hem bellekten kazandırır hemde bağımlılıkların daha iyi belirlenmesini sağlar. buradaki işletim sistemleri tamamen farklı bir dizinde (chroot tarzı) saklanmaktadır. container'da run edilen uygulamalar sadece burayı görebilmektedirler. container içindeki uygulama, host işletim sisteminden sadece linux çekirdeğini ortak kullanmaktadır. onun dışında tüm kaynaklar mount edilen yeni dizin altındadır.

bazen "base os" terimi, "minimal os" terimi yerine yanlış kullanılmaktadır. ikisi farklı şeyler. minimal os, normal destop sistemler içinde olabilir. minimal os, sadece ek paketlerin olmadığı anlamına gelmektedir.

bazen de "container os" terimi "base os" ile karıştırılmaktadır.

linuxta direk sadece işletim sistemi çekirdeği kullanan bir uygulama çalıştırılırsa baseOS'a ihtiyacımız olmaz.

örnek: 
- alpine(özelliği ufak olması)
- ubuntu
- busybox(özelliği ufak olması)
- centos
- fedora
- nanoserver(windows native container'lar için)

# container user

container üzerinde çalışan uygulamalar root kullanıcı ile çalıştırılır. docker, runtime sırasında, root kullanıcısında komut yürütmemize izin verir.

# stop vs remove komutları

iki komutta container'ı durdurmaktadır. fakat remove komutu varolan state'i silmektedir. oysa stop komutu state'i korumaktadır. bu şekilde state istenirse farklı amaçlar için saklanabilir.

# attach vs exec komutu

docker içindeki root user'ına komut satırı üzerinden yönetimini sağlar. attach oldugumuzda yeni bir komut satırı oturumu açılmaz, onun yerine son çalıştırılan komututun çıktılarını görürürüz. eğer yeni bir komut satırı istiyor isek; "docker exec -i -t 878978547 bash command arg1 arg2" ile yeni bir bash açabiliriz. exec komutu en sağda yazan komutu container üzerinde çalıştırmamızı sağlar.

# docker build command

dockerfile'ın image olarak hazır hale getirilmesini sağlar. run edip anında ayağa kalkması için build olması şart. zira build sırasında docker için gerekli dosyalalar internetten indiriliyor.

# docker run command

build edilmiş bir image'yi run etmemize yarar.

-d parametresi eklenince container'ın id'sini döndürüp arkaplanda çalıştırır. -d verilmezse komut satırında işletim sisteminin system.out loglarını basar.

arkaplanda çalışan container'ın system.out çıktılarını "docker log" komutu ile de görebiliriz. 

# docker comit komutu

bu komut ile çalışmakta olan bir image, kopyalanıyor ve yeni bir image yaratılıyor. bu image'nin id'si ekrana basılıyor. image içindeki bilgiler tutulmuş oluyor. örneğin; mysql image'si run edildi, daha sonra üzerine manuel olarak wget kuruldu. bu image kopyalanıp saklanılması isteniyor ise; comit komutundan yararlanılmalıdır. aslında yeni bir isimde klon image oluşturulmuş oluyor. fakat comit yerine dockerfile yaratılması öneriliyor; çünkü image'in nasıl yaratıldığını daha net bilebiliriz.

# layer

container içinde yapılan her işlem yeni bir katman yaratıyor. örneğin layer değişmeden comit yapabilmemiz mümkün diil. çünkü değişen bir dosya olmayacaktır.

# docker diff command

"docker diff containerId" komutu verildiğinde o containerId'nin yaratıldığı image-layer'ı ile şu andaki layer arasındaki dosya sistemindeki farkları listeleyecektir.

# kill vs stop command

container'ların içindeki tüm uygulamalara terminate yada kill siyali gönderiyor. sinyaller başka başlıkta anlatılıyor.

# -p parameter

container'ı run ederken port numarası mappingi yapmak için kullanılır. örneğin;

> docker run -p 80:8080 imageId

BU şekilde host makinenin 80 portuna gelen istekler, docker container içindeki 8080 portuna yönlendirilecektir.

# -v parameter

-p paramtresi ile aynı formata kullanılıyor. fakat dizin bağlamak (mount etmek) için yapılıyor. örnek:

> docker run -v /home/host-user/dir:/home/docker-user/dir imageId

# docker inspect

inspect yanına yazıalna id, herhangi bir kaynağın id'si olabilir. örnek: volume id, image id, container id, network id, stack id gibi.. tüm detaylı json formatında bize döndürür.

# docker --link

docker container'ların birer ip si vardır. bu ip'ler biribirine erişebilmelidirler. bu yüzden host dosyasına dns kaydı otomatik atılabilir. örnek:

> docker run --link myOtherContainerId:aliasOnDnsHostFile imageId

myOtherContainerId ip'si 10.0.0.1 ise; yeni yaratılan container içindeki host dosyasına bakıldığında bu satır görülecektir:

> 10.0.0.1 aliasOnDnsHostFile

# docker hub'a image yollama

docker login komutu ile komut satırından docker'a login olunabilir. daha sonra herhangi bir image'ı push komutu ile docker hub'daki hesabımıza yollayabilir.

# repository vs registry

repository bir docker-image'sinin farklı sürümlerinin barındırıldığı sunucu yazılımıdır. tag ise docker-image'nin sürümüdür. repository kelimesi birçok farklı docker-imagesini barındırıyormuş gibi görünüyor, oysa aynı docker-image'inin farklı sürümlerini barındırıyor. örneğin: repo:jdk tag:8.

registry ise birçok farklı docker-image'sinin bulunduğu sunucu yazılımıdır. örnek "docker hub", docker Inc firmasının resmi registry'sidir ve default olarak docker client'ta tanımlı gelir.

# docker ce

community edition (free)

# docker ee

enterprise edition

# docker edge vs stable

edge is beta version.

# Docker Trusted Registry (or DTR)

locale kurulabilen registry.

# docker collection

docker'ın ucp'sinin vermiş olduğu bir özellik. birçok node UCP'ye bağlı olabilir. her node'da hangi servisi koşacağı stactk-yml dosyalarında bellidir. fakat swarm-yml dosyaları her bilgiyi barındıramıyor. bu sebeple bazı bilgiler sadece ucp içinde kayıtlıdır. örnek:

- hangi volume'nin hangi node'da olacağı

- node'lara atanmış label bilgileri

- stack dosyaları haricinde yaratılmış service'ler

bunların yedeğini alabilmek için gurplama ihtiyacı vardır. işte bu gruplara "collection" denir. collection sadece bu bilgileri değil, tü sistemin bilgileri saklar. örneğin; stack-yml dosyaları da buna dahildir.

her collection, ucp tarafından ayrı ayrı dizinler içerisinde saklanır.

# moby

artık (2017 yılı ile) docker açık kaynaklı proje olarak moby projesi altında dağıtılıyor. moby projesi dockerCE ve EE olarak docker tarafından kapatılıp üzerinde bazı değişiklikler yapıp dağıtılmaktadır. moby projesi ile hedef docker'ı daha modüler hale getirmektir.

# union file system (or unionfs)

docker bu dosya sistemini run edilen container'lar için kullanır. örnek: java kurduk ve uygulamamızı run ettik. java ve ubuntu-os otomatik kurulur. bu 2 container read-only'dir. run ettiğimiz java uygulaması birşeyler kaydetti. bu dosyalar ubuntu-os'un dosyalarını da değiştirmiş olabilir yada ek dosya atayabilir. böyle durumlar için dosya sistemi böyle işliyor: ubuntu-os ve java'nın olduğu bir dosya sistemi read-only (no:1) oluşturuluyor. daha sonra  bir dosya sistemine (no:2) java uygulamamız dosya yazıyor. eğer container içinden bir dosya okumaya kalkarsak; unionfs önce no:2 dosya sistemine bakıyor. eğer bir dosya silme bilgisi yada yeni dosya oluşturulmuş ise bu dosyayı bize dönüyor. eğer hiçbir bilgi bulamaz ise no:1 dosya sistemindeki dosyayı dönüyor. bu sistemde no:2 dosya sistemine no:!'in "branch"'i adı veriliyor. istediğimiz kadar branch oluşturabiliyoruz.

var olan ve container açıldıktan sonra düzenlenen bir dosya branch'e kopyalanır ve editlenir. tabi eğer taşınan bu dosya çok büyükse ilk kopyalama işlemi zaman alacaktır.

unionfs'e birçok alternatif var. bu alternatifleri docker engine'den seçebiliyoruz. bazı dosya sistemleri tüm dosyayı değilde, dosyayı belli bloklara bölüyor ve sadece değişen kısmın bloğunu taşıyor. bu tarz farklı yöntemler mevcut.

unionfs'in değişiklikleri branch'lere kopyalama özelliğine copy-on-write (or cow or implicit sharing or shadowing) deniliyor.

# volume

bir container'a host bilgisyarımızdaki bir dizini mount edebiliriz. buna alternatif olarak sanal bölümler docker tarafından oluşturulabilir. bunlar host makina tarafından okunamazlar. mount ve volume karşılaştırılacak olursa asıl önemli avantaj: volume'ların docker tarafından moutn edilmesi olacaktır. host bilgisyarda motun edeceğimiz dizinin yetkileri, dosya sisteminin desteklenip desteklenmeyeceğini gibi sorunlarla karşılaşabiliriz. oysa volume'larda böyle bir sorun yok.

# docker temizlik

##### dangling images

türkçe kelime anlamı: askıda kalmak

örnek üzerinden direk gidersek. docker içinde jdk indirdik. os olarak fedorayı indirdi. fedora'yı indirince fedora ile "latest" isminde bir layer (image) oluştu. daha sonra jdk layerı oluştu. 1 ay sonra tkrar jdk'yı indirdik. bu sefer içindeki fedora güncellendi. ve yine "latest" tag'i ile. dolayısı ile eski "latest" tagli fedora artık "none" isminde kaydediliyor. bu tarz durumlar bazı layerları askıda bırakıyor. sadece askıda olan layerları temizleyen komut mevcut.

tag vermeden oluşturduğumuz her image dangling'dir.

##### docker system prune

prune türkçe kelime anlamı: budamak.

bu komut sırası ile şu komutları işletiyor:

- docker container prune

- docker image prune

- docker network prune

- docker volume prune

##### docker system prune -a

-a parametresi durmuş tüm kaynakların silinmesini sağlıyor. yani o sırada run edilenler haricindeki tüm kaynaklar siliniyor. hiçbir container run edilmezken çalıştırılırsa tüm kaynaklar silinir.

##### docker container prune

stop olmuş tüm container'ları siler.

##### docker image prune

dangling images'leri siler.

##### docker image prune -a

hiçbir container tarafından kullanılmayan imageleri siler.

##### dangling volume

bir volume conitaner run edildiğinde mount edilir. yani container ile ilişkilendirilir. eğer ilişkisiz bir volume var ise, bu volume dangling'dir. stop olmuş fakat silinmemiş container'lar hala volume'ler ile ilişkilidir.

##### docker volume prune

dangling volume'leri siler. bu komutun "-a" ile bir alternatifi yoktur. çünkü zaten container ile bağlantısı olmayan her volume dangling'dir.

##### docker network prune

volume ile aynı mantıktadır. bu komutun "-a" ile bir alternatifi yoktur. çünkü zaten container ile bağlantısı olmayan her volume dangling'dir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Sanal makinelerde Disk formatlari

```
          native-support      support               açıklama

- VMDK    VMWare              Virtualbox, QEMU/KVM   

- VDI     virtualbox          QEMU/KVM              Genel olarak VDI ve WDMK arasinda önemli farklar mevcut degil.

- raw     QEMU/KVM                                  hiçbir özellik barındırmıyor. sanal diskte ne varsa direk burada binary olarak tutuluyor. format header dahi barındırmıyor. en iyi performans bunda.

- cow     QEMU/KVM                                  QEMU/KVM'nin sunduğu format.

- qcow    QEMU/KVM            VirtualBox            cow'un yeni sürümü.

- qcow2   QEMU/KVM                                  qcow'un yeni sürümü.

- vhdx    Hyper-V             VirtualBox            vhd'nin yeni sürümü. vhd microsoft haricindeki yazılımlara sorun olduğu söyleniyor.

- vhd     Hyper-V             VirtualBox

- cloop   QEMU/KVM                                  özel amaçlı kullanılan bir format.

- qed     QEMU/KVM            VirtualBox            qcow2'nin özellikleri silinerek performans kazandırılmaya çalışılıyor. fakat proje durduruldu.
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# özet karşılaştırma/bilgi: openshift vs istio vs kubernetes vs spring boot
bu karşılaştırmayı yapmak doğru değil. fakat başlıktaki teknolojilerin bazı özellikleri ortak problemi çözmektedirler. tek tablo olarak hızlıca buradan özellik listesini görebiliriz:

- (source-id: 257) "Feature Overlap" başlığındaki şekil.

- (source-id: 258) "Technology Mapping" başlığındaki ilk şekil ve "Best of Both Worlds" başlığındaki ikinci şekil.

# OpenStack
NASA'nın da geliştirmekte olduğu, açık kaynaklı Bulut bilişim altyapı projesidir. bulut bilişim sunan bir firmada olması gereken tüm yazılımlar bu proje altında açık kaynaklı olarak geliştirilmektedir. projede öncelik IaaS'tır.

# OpenShift
Kubernetes'i gömülü olarak kullanan onun üzerine ek özellikler sunanan bir yazılımdır:

- servislerin yönetilmesi
- servislerin discover edilebilmesi
- log takibi
- servislerin birbiri ile konuşması
- dış dünyadan gelen isteklerin balancing edilmesi

OpenShift 'oc' komut satırı uygulaması yada web arayüzünden yönetilmektedir.

Openshift'te her proje, kubernetes'teki namespace'e denk gelmektedir. Diğer daha ufak birimler tamamiyle aynı isimde kullanılır. kaynak: (source-id: 259) "Namespaces" başlığı.

OpenShift'in yönetim paneli için sunduğu web arayüzünde, bir proje içerisinde yeni bir pod ayağa kaldırılmak istendiğinde "namespace" bilgisi ister. burada istenen namespace bilgisi, pod'un çalışacağı namespace değil, openshift'in sunduğu "imagestream" özelliği için kullanılacak namespace bilgisidir.

- ## minishift
komut satırı uygulamasıdır. local'de tek cluster openshift ayağa kaldırır.

- ## OKD (or Origin Community Distribution or old-name:OpenShift Origin)
ücretsiz lisanslı openshift versiyonu.

- ## OpenShift Container Platform (or old-name:OpenShift Enterprise)
OKD'nin lisansı ücretli ve destek alınabilen versiyonudur.

- ## Red Hat OpenShift Online (or RHOO) vs OpenShift Dedicated vs OpenShift.io
Ticari lisanslı sadece bulut makinelerde çalışabilen openshift hizmetleridir.

# Envoy
türkçe kelime anlamı: elçi

L7 proxy'dir ve load balancing gibi ek özellikler barındırır.

# L4 vs L7 proxy
Proxy'ler data iletiminde aracılık yaparlar. aracılık yaparken gelen giden datanın ne olduğu ile ilgilenilirken, L4 proxy'ler OSI katmanlarında 4üncü level seviyesinde data transferlerine manipülasyon yapabilirler. Yani UDP, TCP seviyesinde datayı tanırlar. TCP ile gönderilen datanın ne olduğu ile ilgilenemezler. Oysa L7 proxy'ler en üst seviye OSI katmanında, 7inci katman, application layer'da işlem yapabilirler.

Bazı durumlarda; L7 proxy; OSI 4 katmanında, L4 ise OSI 7 katmanında işlem yapması gerekebilir/yapabilir. Bir proxy yazılımının hangi tipte olduğunu tanımlarken en çok hangi katmandaki işlemlere öncelik verdiği değerlendirilir.

bir L7 proxy aşağıdaki özellikleri sunabilir:

- load balancing

  kendine gelen request'leri, önünde durduğu node'lara paylaştırır

- Health checking

  - Active

    önünde duruğu her node'a sürekli /healchecking gibi bir url ile istek atar. cevap alamazsa, o node'a requestleri yollamaz

  - Passive

    önünde durduğu node'ların client'lara verdiği cevapları inceleler. eğer cevaplarda terslik varsa, o node'u sağlıksız olarak set eder ve ona request yönlendirmez

- Service discovery

  kendini servis discovery'ye tanıtır

- Sticky sessions

  cookie'lere bakarak, kullanıcını aynı session'ı boyunca aynı node'a gitmesini sağlar.

- dos atakarının önüne geçmek için kalkan oluşturur

- rate limiting

  kullanının session'ına göre (state'ine göre) belli bir sürede yapabileceği request sayısı tanımlanır. eğer bu sayıyı geçerse kullanıcının engellenir.

- yönetim paneli

# Proxy türleri

- middle proxy

  klasik proxy sunucularıdır. gelen istekler ve döndürülen cevaplar bu proxy üzerinden geçer.

- Edge proxy

  api gateway olarakta adlandırılırlar.

- Embedded client library

  bir kütüphane olarak node'lara eklenir. bunun dezavantajı dilden bağımsız olamaması. "polyglot (or multilingual)" kütüphaneler yazılması gerekir.

- Sidecar proxy

  kendi başına genelde aynı container içerisinde ayağa kaldırılan proxy'dir.

# Direct server return (or DSR)
bu tarz proxy'ler dönen response'ları kendi üzerlerinden geçirmezler. response'lar direk client'a node tarafından yollanır.

# downstream vs upstream
upstream kelime anlamı: akıntı yönüne karşı.
downstream kelime anlamı: akıntı yönüne doğru.

proxy dünyasında; downstream requesti yollayan, upstream ise cevabı yollayan node'dur.

# Service Mesh
Mesh türkçe kelime anlamı: ağ

mikroservislerin artmasıyla birlikte bu tanım ortaya çıktı. servislerin ağ yönetimi (birbirleri ile haberleşmeleri) sistem büyüdükçe daha zorlaşmaya başlıyor. bu ağı yönetebilmek için birçok çözüm sunuluyor. "Service Mesh" tanımı sıkça karşımıza çıkmaktadır. "service mesh"; ağın yönetimi çözümü için uygulanan altyapılara verilen genel bir terimdir.

sidecar proxy, service discovery, orchestration framework, load balancing, circiut breaker gibi altyapıları içeren çözümler sunulur.

(Sidecar pattern'i başka başlıkta anlatılıyor) Modern servise mesh çözümlerinde sidecar pattern'inden sıkça faydalanılıyor. modern çözümlerde, her pod/container'a bağlı bir sidecar proxy bulunuyor. her gelen giden request buradan geçiyor. o pod/container'a bağlı sidecar security, loggining gibi birçok görevi pod/container'da yüklü olan uygulama yerine yapıyor.

istio sadece "service mesh" yönetimi sunarken, openshift hem orchestration hemde "service mesh" özellikleri sunar.

# Istio
kubernetes içerisinde oluşturduğumuz her pod içinde, istio (otomatik olarak) kendi container'larını açar. bu container'lar ile sidecar proxy pattern'ini baz alarak load balancing, logging gibi birçok servise mesh işlemimizi halleder.

'istioctl' komut satırı uygulaması ile yönetimi sağlar.

# Kubernetes (or abb:K8s)
UCP, docker swarm ve docker compose'a alternatif olan ve daha fazla özelliği içeren açık kaynaklı yazılımdır. kubernetes containerları yönetmek çin kullanılır. container'ların ne ile yönetildiği ile ilgilenmez. yani Kubernetes docker yada rkt ile de çalışabilir. kaldırdığı container'ları istediğimiz herhangi bir container yazılımı ile kaldırabiliriz.

docker UCP'deki özelliklere ek olarak kubernetes'in sundukları:
- cross-application config server barındırır
- cross-application discovery server barındırır
- port yönlendirme yapar, bu şekilde istediğimiz container'ın istediğimiz portuna bağlanabiliriz
- scheduled cronjobs

- ## command line tools

   aşağıdaki tüm komut satırı uygulamaları kubernetes'ten ve birbirlerinden bağımsızdır. sadece istediğimiz paketin binary'sini indirip localde çalıştırabiliriz.

   - ### kubectl
     kubernetes command line tool'udur.

   - ### minikube
     komut satırı uygulamasıdır. localde test amaçlı çalışmalar için geliştirilmiştir. local makinede sanal makina açmakta ve içerisinde tek node'lu kubernetes yürütmektedir.

     eğer local makinede "docker desktop" yüklü ise; sanal makinesizde direk kubernetes yürütebilmektedir çünkü kubernetes tool'ları docker desktop ile yüklü gelmektedir.

     minikube "minikube" isminde bir context oluşturuyor ve kubectl'ye default context olarak set ediyor.

     minikube başlatma:

     ```sh
     minikube start --driver=none
     ```

     Opsiyonel olarak vereceğimiz driverlar aşağıda listelenmiştir. Driver, cluster'ın tümüyle hangi ortama kurulacağını belirliyor.

     - virtualbox

       virtualbox üzerinde yeni vm açıyor ve bunun içine tümüyle kubernetes admin ortamı/cluster'ı kuruyor.

     - hyperv

       virtualbox ile aynı mantıkta çalışıyor.

     - kvm

       virtualbox ile aynı mantıkta çalışıyor.

     - vmware

       virtualbox ile aynı mantıkta çalışıyor.

     - none

       kubernetes admin ortamını ve bunun üzerinde bir cluster'ı local OS'umuza kuruyor. B u pek tavsiye edilen bir yöntem diil. Çünkü varolan OS'umuzdakki dosyalarda değişiklik yapıyor.
       
       Kubernetes cluster'ı ve admin ortamını kuracağımız ortamda hem docker requirement'i vardır hemde container'lar haricinde normal process'lerde çalıştırılır ve OS'un dosyalarına müdahele gerçekleşir. (zaten bunlardan kaçınmak için minikube çıktı ve bu sebeple bu driver tavsiye edilmiyor)
    
     - docker
     
       OS'umuzda bir docker başlatıyor. Bu docker'ın içerisine gerçek bir docker kuruyor ve kubeadm kurulumu yapıyor.

       kaynak: (source-id: 260) Pull request'in başlığında "Kind" kullanıldığı belirtilmiş.

       __KIND__ kubernetes'in docker ortamına kurulması için geliştirilen bir docker-image projedir. KIND, docker içerisine docker kurulumu yapar ve image içerisine kubernetes kurar. kaynak: (source-id: 261) "Deep Dive: KIND - Benjamin Elder & Antonio Ojea" videosunda, 2:08'de slide ekranında docker içerisine neler kurulduğu yazılmış.

   - ### kubeadm
     komut satırı uygulamasıdır. kubernetes'in kendisini update edebilmemizi, cluster oluşturabilmemizi sağlıyor.

- ## components

     - ## Control Plane Components (or Master Components)
       Cluster'daki tüm node'ları ve sistemi yöneten modüllerin tümüdür. Aşağıdaki parçalardan oluşur:

        - ### kube-apiserver
          API'nin sağlanması için gereken module. api olarak servis sunuyor. buraya http isteği olarak yollanan emirleri kubelet'lere yolluyor. kube-apiserver master node içerisindedir.

        - ### etcd
          key-value veritabanıdır. bütün sistemin meta bilgilerinin yönetimi buradan yapılır.
        
        - ### kube-scheduler
          scheduler'ları düzenli olarak çalıştıran modüldür. aynı zamanda yeni oluşturulan POD'ları node'lara atayan modüldür.

        - ### kube-controller-manager
          node'ların ayakta olup olmadığını kontrol eder, açılan pod'ların doğru adet olduğunu kontrol eden... modüldür

        - ### cloud-controller-manager
          kube-controller-manager'in bulut hizmetler (amazon aws gibi) için geliştirilmiş türevidir.

     - ## node components
       node bir VM yada fiziksel makinedir. node components, her node içinde yüklü olan modüllerdir.

        - ### kubelet
          her node'da bir adet yüklüdür. bu yazılım kube-controller-manager'dan emirleri alır ve yerine getirir. o node üzerinde yeni pod'ların ayağa kaldırılması kapatılması gibi işlevleri yerine getiriyor.

        - ### kube-proxy
          her node'da bir adet yüklüdür. "kubernetes servis", "port yönlendirme" gibi networksel işlemlerinin altyapısının her node'da çalışmasını sağlayan yazılımdır. "network proxy" yazılımıdır.

        - ## Container Runtime
          her node'da kurulmuş olması gereken docker yada alternatifi container manager'ı.

- ## addons
     kubernetes'in addon altyapısı mevcuttur. 

     örneğin "Web UI (Dashboard)" bir addon'dur.

- ## namespace, context, cluster

     - ### namespace
       her cluster'da birçok namespace olabilir. her namespace kendi içinde pod ve servisler bulundurur.

       tüm namespace'leri listele:
       > kubectl get namespaces

       yeni namepsace yarat:
       > kubectl create namespace dev

     - ### context
       tüm ayarların bütününe verilen isimdir. örneğin bir context yaratalım:
       > kubectl config set-context minidev --cluster=cluster1 --user=user1 --namespace=namespace1

       switch to context:
       > kubectl config use-context minidev

     - ### cluster
       kubernetes cluster altyapısını destekleyen platformdur. örneğin google cloud, amazon cloud bu yapıyı destekliyor. localden hangi cluster'a gideceğimizi komut satırından belirtmemiz gerekmektedir.

       Bir yazılım projesinin development, test, prod gibi ortamlarının ayrı clusterlara (namespace'lere değil!) kurulması önerilir.

# Kubernetes Objects

- pod
- service
- volume
- namespace
- Controllers
  - ReplicaSet
  - Deployment
  - StatefulSet
  - DaemonSet
  - Job

# pod
kubernetes'in kullandığı en ufak birimdir. içerisinde birden fazla container olabilir.

her pod network'ü ortak kullanıyor. istediği storage namepsacelerini ise ortak kullanabiliyor. pod bir container değil. pod container wrapper'ı. yani pod kendi içinde bir container dizini barındırmıyor. pod örneğin 2 container içeriyorsa, pod 2 container'ı docker ile ayağa kaldırıyor. 2 docker'ı yöneten yapıya pod deniliyor. pod'un kendisni bir container gibi düşünmemek gerekli. çünkü container terimi farklı kapıya çıkıyor. pod bir process olarak düşünülmeli. bu proses diğer açılan 2 docker proces'ini yönetiyor.

pod'a en yakın tanım docker-compose'dur. sadece belirtilen container'ları açmakla/yönetmekle ilgilenir. kendisi bir container değildir.

pod tanımının bulunduğu dosya örneği:

```yml
apiVersion: v1 # in which kubernetes version this file works.
kind: Pod # can be other types like: Service, Pod...
metadata:
  name: multi-container-example
  namespace: test
  labels: 
    app: web # labels are custom key/values. (labels are explained in another topic)
spec:
  containers:
  - name: nginx
    image: nginx:stable-alpine
    resources:
      limits:
        memory: "600Mi" # if it will try to use more memory, this pod will be terminate automatically by kubernetes and will re-create again.
    ports:
    - containerPort: 80 # port which is exported to outside
    volumeMounts:
    - name: html
      mountPath: /usr/share/nginx/html # path which will mount inside container filesystem
  - name: content
    image: alpine:latest
    volumeMounts:
    - name: html
      mountPath: /html # path which will mount inside container filesystem
    command: ["/bin/sh", "-c"]
    args:
      - while true; do
          echo $(date)"<br />" >> /html/index.html;
          sleep 5;
        done
  volumes:
  - name: html # which is the reference name of this volume.
    emptyDir: {} # creates an empty volume.
    
    # alternative of "emptyDir":
    # hostPath:*
    #   path: /data # the full path of the namespace cluster machine

    # other alternatives of "emptyDir": (source-id: 262)
```

context'imizi komut satırından belirledikten sonra pod'umuzu yaratabiliriz:

> kubectl create -f multi-container-example.yaml

Yukarıda 1 pod içinde 2 adet container bulundurulmuştur. Mount şekli docker'dan biraz farklıdır. Mount tanımı container tanımının dışındadır (üst seviyesindedir). bu mounting'e ihtiyacı olan container'lar "mountPath" ile bu tanımı kendileri için kullanabilirler. Yukarıdaki html isimli volume her 2 container tarafından kullanılmış. böyle durumlarda aynı dosyalar 2 container tarafından da görülüp yazılabilmektedir.

Aşağıdaki komut ile varolan pod'ları listeleyebiliriz:

> kubectl get pods --show-labels

Loga bakmak için:

> kubectl logs -f pod-name --tail 200

Eğer bir pod içerisinde birden fazla container varsa, sadece ilgili container'ın loguna bakmak istiyorsak:

> kubectl logs -f pod-name --tail 200 -c container-name

get detail of running pod:

> kubectl describe pod pod-name

delete pod:

> kubectl delete pod pod-name
yada
> kubectl delete -f pod-manifest.yaml

# port-forward
pod manifes yml dosyamızda dışarıya açılacak portu belirtmezsek; sonradan komut satırında şu şekilde portu dışarıya açabiliriz:

> kubectl port-forward pod-name 8081:8080

# CNI (or Container network interface)
host'lar ve container'lar arasındaki network iletişimini sağlayan kubernetes plugin'leridir. isteğe bağlı kullanılırlar. örnek pluginler: calico, flannel, weave net

temel olarak; CNI eklentisi, her makinede bir bridge (eth0, loopback gibi) açıyor. bu bridge üzerinde routing table configürasyonları ile diğer makinedeki container'lara direk olarak, container ip'leri ile istek atabilmemizi sağlıyor.

bu route table'ların birbirlerini görebildiği sanal ağın (ip kümesinin) tümüne __overlay network__ adı veriliyor.

# label and selector

pod veya service yml'mizin başında istediğimiz isimde label'lar kullanabiliriz. bu label'lar sayesinde daha sonra birçok sorgu, update gibi işlemleri belli pod veya servislerimize sağlamış olacağız.

```yml
apiVersion: v1
kind: Pod
metadata:
  name: multi-container-example
  labels:
    app: nginx
    environment: prod
...
...
```

# service
service selector'ler ile belirttiğimiz pod grubuna referans edecek olan sanal yapıdır. örneğin bir servise istek yaparsak aslında ona bağlı pod'lara istek yapmış oluruz gibi...

example yml file:

```yml
apiVersion: v1
kind: Service
metadata:
  name: user-service
  labels:
    run: user-service # the label of this service
spec:
  type: NodePort # can export port for accessing outside of the cluster.
  # alternatives of "type: NodePort":
  # ClusterIP (default) --> does not expose port for accessing the service from outside the world.
  ports:
    - port: 8080 # this is the exported port of this service (only for communication beetween POD's. not outside of the cluster.)
                 # By default and for convenience, the "targetPort" is set to the same value as the "port" field.
      targetPort: 8081 # if any request come to 8080(port), it will redirect on this port of POD
      nodePort: 8083 # the exported port of this service for outside of the cluster. 
                     # By default, Kubernetes will allocate a port from a range (default: 30000-32767)
      protocol: TCP
      name: http-port # this is only a label
    - port: 8090
      targetPort: 8091
      nodePort: 8093
      protocol: TCP
      name: metrics-port # this is only a label
  selector:
    run: user-service-pod-label # this service is in front of all the POD's which have "user-service-pod-label"
```

# deployment
deployment içerisine biçok replica set ve pod barındırabilen bir yapıdır.

yml dosyamızın içerisinde "kind: deployment" yazmamız gereklidir.

# Replica Controller
istediğimiz pod sayısının ayakta kalmasını sağlar.

yml dosyamızın içerisinde "kind: ReplicationController" yazmamız gereklidir.

# Replica set
Replica Controller'ın alternatifidir. temelde aynı görevi görür.

yml dosyamızın içerisinde "kind: ReplicaSet" yazmamız gereklidir.

# desired state vs actual state
her kubernetes objesinin bir 2 state'i vardır. biri yazılımcının istediği durum, diğer ise şu andaki durumudur. örneğin  ReplicaSet ile 100 adet container ayağa kaldırmak istemiş olalım, fakat henüz sadece 50 tanesi ayakta olsun. budurumda "desired state":100, "actual state":50 dir.
