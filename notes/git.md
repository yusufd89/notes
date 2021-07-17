############################

############################
# GIT
############################

############################

# GIT SCM (or Git Source control management or Git Sürüm Kontrol Sistemi)

# Git vs SVN (or Subversion)
temel fark git'in dağıtık (or Distributed) bir yapıya sahip olmasıdır. bunun sonucu olarak; herkes kendi local repo'suna sahiptir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# git flow vs trunk based development
trunk kelime anlamı: gövde, ana hat, ana yol

git flow developmentta; bir develop branch'i olur. her developer buradan bir branch oluşturur ve ilgili geliştirmesi tamamlandığında develop branch'ine merge eder. develop branchinin stabil olduğu bir noktadan master'a merge olunur. master release'lerin bulunduğu branch'tir.

trunk based'de ise; herkes master üzerinde çalışır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# git Credentials
git Credential bilgilerini birçok farklı yerde tutabilir. kullanılan OS'a göre defualt bir değeri vardır. biz bunu elle bu şekilde değiştirebiliriz:

```sh
git config --global credential.helper cache # cache moduna geçirdik
```

Mode'lar:

- default: does not store anywhere 
- cache: çok kısa bir süreliğine (default: 15 dk) ram'de tutar. bunun için arkada git daemon'u çalışır.
- store: txt formatında $HOME dizini içinde bir dosyada saklar (default: $HOME/.git-credentials)
- MacOS'ta isek default olarak macos un yüklü getirdiği osxkeychain uygulamasında saklar.
- __wincred__, windows için git içinde yüklü gelen default mode'dur. microsoft'un "__Windows Credential Store__"'a datayı saklamasını iletir.
- ms-windows'ta iken git'Ten bağımsız geliştirilen "__Git Credential Manager for Windows (or GCM)__" uygulamasını kurarabiliriz. bu uygulama microsoft'un "__Windows Credential Store__"'a datayı saklamasını iletir. GCM; artık geliştirilmeyen '__Windows Credential Store for Git (git-credential-winstore)__'un bir forkudur.

ek not: mac ve ms-windows OS olarak kendi içinde genel key yönetimi için GUI sunmaktadır.

gitconfig dosyası aşağıdaki dosyalardan okunur:

- Your machine's system .gitconfig file. (örnek: C:\Program Files (x86)\Git\etc\gitconfig)

- Your user .gitconfig file located at ~/.gitconfig.

- A second user-specific configuration file located at $XDG_CONFIG_HOME/git/config or $HOME/.config/git/config.

- The local repository's configuration file .git/config.

Sadece sistem config dosyasının içeriğini bu şekilde listeleyebiliriz:

```sh
git config --system --list
```

örnek sistem dosyası:

```
[http]
    sslBackend = openssl
    sslCAInfo = C:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt
[credential]
    helper = manager
```
 
örnek "git config --system --list" çıktısı:

```
http.sslbackend=openssl
http.sslcainfo=C:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt
credential.helper=manager
```

Tüm config'lerin dosya bazlı listelenmesi için:

```sh
git config --list --show-origin
```

örnek çıktı:

```
file:"C:\\ProgramData/Git/config"       core.symlinks=false

file:"C:\\ProgramData/Git/config"       core.autocrlf=true

file:"C:\\ProgramData/Git/config"       core.fscache=true

file:"C:\\ProgramData/Git/config"       color.diff=auto

file:"C:\\ProgramData/Git/config"       color.status=auto

file:"C:\\ProgramData/Git/config"       color.branch=auto

file:"C:\\ProgramData/Git/config"       color.interactive=true

file:"C:\\ProgramData/Git/config"       help.format=html

file:"C:\\ProgramData/Git/config"       rebase.autosquash=true

file:C:/Program Files/Git/mingw64/etc/gitconfig http.sslbackend=openssl

file:C:/Program Files/Git/mingw64/etc/gitconfig http.sslcainfo=C:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt

file:C:/Program Files/Git/mingw64/etc/gitconfig credential.helper=manager

file:C:/Users/user-name/.gitconfig        user.name=user-name

file:C:/Users/user-name/.gitconfig        user.email=user-name@my-domaim.com

file:C:/Users/user-name/.gitconfig        user.password=my-password

file:C:/Users/user-name/.gitconfig        credential.helper=store
```

Benzer şekilde dosya bazlı değilde, scope bazlı (global, sistem...) listelemek için bu komut gereklidir:

```sh
git config -l --show-scope  # --show-scope parametresi git 2.26 sonrasında gelmiştir
```

örnek çıktı:

```
global  user.global=true

global  user.override=global

global  include.path=$INCLUDE_DIR/absolute.include

global  user.absolute=include

local   user.local=true

local   user.override=local

local   include.path=../include/relative.include

local   user.relative=include
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Git workspace structure

git workspace'si içerisinde 3 tane alan vardır:

- Git klasörü

  ".git" isimli dizindir. Git'in üstverileri (metadata) ve nesne veritabanını depoladığı yerdir. Bu, Git'in en önemli parçasıdır ve bir yazılım havuzunu bir bilgisayardan bir başkasına klonladığınızda kopyalanan şeydir.

- Çalışma klasörü

  projenin bir sürümünden yapılan tek bir seçmedir. Bu dosyalar Git klasöründeki sıkıştırılmış veritabanından çıkartılıp sizin kullanımınız için sabit diske yerleştirilir.

- Hazırlık alanı (staging area)

  genellikle ".git" klasörünüzde bulunan ve bir sonraki kayıt işlemine hangi değişikliklerin dahil olacağını tutan sade bir dosyadır. Buna bazen "indeks" dendiği de olur, ama "hazırlık alanı" ifadesi giderek daha standart hale geliyor.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# State

dosyaların bulunabileceği 2 farklı state vardır:

- __Tracked__

  öncedeki comitlerde db'de olan yada hiçbir committe olmayıp şu anda "tracked" state'ine manuel olarak alınmış dosyadır.

  Kendi içinde 3 çeşit durumda olabilir:

  - __Kaydedilmiş (or staged)__: verinin güvenli biçimde veritabanında depolanmış olduğu anlamına gelir.

  - __Değiştirilmiş (or modified)__: dosyayı değiştirmiş olduğunuz fakat henüz veritabanına kaydetmediğiniz anlamına gelir.

  - __Hazırlanmış (or unmodified)__: değiştirilmiş bir dosyayı bir sonraki kayıt işleminde bellek kopyasına alınmak üzere işaretlediğiniz anlamına gelir.

- __Untracked__

  önceki comitlerde bu dosya yoktur.

State'ler arası değişim aksiyonlara göre şu şekildedir:

```
                                              TRACKED
                           ______________________|________________________
                          |                      |                        |
UNTRACKED              Unmodified              Modified                Staged

    o--------------------->>  add file  >>--------------------------------o
 
                            o--->>  edit file  >>--o

                                                   o-->>  stage file  >>--o

    o--<<  remove file  <<--o

                            o--------------<<  commit file  <<------------o
```

Yuakarıdaki şekilde "stage file" işlemi için komut satırından "git add myFile1" komutu veriliyor. "git add" komutu multi-purpose'dur. çünkü UNTRACKED dosyayı da Staged duruma getiriyor.

Yuakrıdaki şekildeki terimler git status çıktısı ile birebir aynı olmayabiliyor. örnek "git status" çıktısı:

```
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md
```

Yukarıdaki çıktıda; "modified:   CONTRIBUTING.md", "Changes to be committed" altında, yani; staged durumunda. fakat modifiye edilmiş bir dosya olduğu için "modified" olarak yazılmış. oysa staged durumunda.

CONTRIBUTING.md'yi elle staged duruma aldık. Eğerki (comit atmadan veya hiçbir aksiyon almadan) tekrar aynı dosyayı editlersek, "git status" çıktımız şu şekilde olacaktır:

```
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```

"git diff" ile tüm değişiklikleri, "git diff --staged (or git diff --cached)" ile de sadece stage'de olan değişiklikleri satır satır detaylı şekilde görebiliriz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Commands

yeni bir git çalışma alanı yaratmak için:

> git init

komutu kullanılır. bulunduğunuz dizinde bir repo yaratır.

fakat varolan bir repoyu klonlamak için:

> git clone git://github.com/schacon/grit.git

komutu kullanılır. git:// yerine farklı protokollerde desteklenir.

bir dosyayı çalışma alanından silmek için:

> git rm myFile

eğer dosya değiştirilmiş ve indexe eklenmiş (kayda hazırlanmış) ise:

> git rm -f

komut ile zorla silmek zorundasınız.

> git log

komutu ile tarihçe görüntülenebilir. her değişikliği bir satırda görmek istiyorsak:

> git log --pretty=oneline

örnek çıktı:

```
ca82a6dff817ec66f44342007202690a93763949 Change version number
085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7 Remove unnecessary test
a11bef06a3f659402fe7563abf99ad00de2209e6 Initial commit
```

Eğer istediğimiz formatta her comiti görmek istiyorsak:

> git log --pretty=format:"%h - %an, %ar : %s"

örnek çıktı:

```
ca82a6d - Scott Chacon, 6 years ago : Change version number
085bb3b - Scott Chacon, 6 years ago : Remove unnecessary test
a11bef0 - Scott Chacon, 6 years ago : Initial commit
```

aşağıdaki komut, son yapılan comit üzerine yeni değişiklikler var ise onları da o comite eklemek için kullanılır:

> git commit -m 'Initial commit'

> git add "forgotten_file"

> git commit --amend

(ammend kelime anlamı: iyileştirmek)

daha önce bahsedilen silme işlemlerinde, dosya çalışma alanından da tamamen siliniyordu. oysa dosyayı silmeden, sadece kayıt alanına eklenmiş ise sadece kayıt alanından kaldırmak için:

> git reset HEAD myfile.txt

komutu kullanılır. bu şekilde dosya tracked olmaya devam eder fakat kayda atılmamış olur.

bir dosya değişmiş durumda fakat kayıt alanına eklenmemiş ise; dosyayı resetlemek yani değiştirilmemiş hale getirebilmek için:

> git checkout -- myfile.txt

komutu çalıştırılır.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# remote

local repo ile çalışmaya benzer olarak, local repoyu uzak (remote) repo'lar ile işlemede tabi tutabilir. remote için pull yada push gibi işlemler yapılır.

__origin__ Git'in klonlamanın yapıldığı sunucuya verdiği öntanımlı addır.

bu komut ile origin adresi görüntülenir:

> git remote -v

bu komut birden fazla remote görüntüleyebilir. çünkü birden fazla remote olabilir. push ve pull için ayrı repo'larda olabilir. örneğin bir yerden çekip başka bir yere push yapıyor olabiliriz.

bu komut ile yeni uçbirimler eklenebilir:

> git remote add [kisa_ad] [url]

> git fetch origin

komutu o anda olduğumuz brenç'le ilişkili uzaktaki tüm değişiklikleri local git veritabanına çeker fakat çalışma alanı üzerinde değişikleri yapmaz. çalışma alanı ile birleştirme işlemi için pull komutu kullanılır. çünkü "pull"; hem fetch, hemde rebase işlemini yapacaktır.

fetch komutu eğer remote verilmemişse (yukarıdaki örnekte "origin"), default olarak ilgili branch ile ilişkilendirilmiş remote branch'ten fetch yapar. o da yok ise default olarak 'origin'den çeker.

fetch komutunun "-all" parametresi tüm remote'lardan fetch işlemini yapar. fetch işlemi branch bazlı değildir.

> git push origin master

yukarıdaki komut ile local repoda comit'lenmiş değişiklikler remote'a yollanır. eğer biz yollamadan önce biri değişiklik yollamış ise, bizim değişiklik reddedilecektir. önce eski değişiklikleri alıp, local ile rebase olup, bu şekilde comitlememiz ve daha sonra push etmemiz gerekmektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# tag

etiket (tag) git logları üzerinde görülebilirliği arttırmak amaçlı (sürüm tutma gibi) bilgisini saklamak için kullanılır.

"git push" işlemi tag'leri remote'a yollamaz. tag'leri ayrı komut ile yollamak gerekir. yada hepsini birden yollamak için özel parametre geçilmelidir:

> git push origin --tags

2 çeşit tag vardır:

- lightweight

  sadece comit'in referansına bir label atmak için kullanılır. örnek tag atma:

  > git tag "alpha"

- annotated

  birer git objesidir ve gelişmiş özellikler içerir.

  örnek annotated tag atma:

  > git tag -a v1.4 -m "alpha"

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# branch

Bir commit atıldığında git stage'dekiherşeyi snapshotunu ağaç şekline tutar. Dolayısı ile git'in veritabanı temelde 'series of snapshot'tır. örnek bir commit (ve onun ağacı):

```
                                                     (object id:40) 
                                                      _____________ 
                                                     |BLOB          |
                                                     |public class  |
                                                     |function util |
                                                     |retun null    |
                                                      ------------- 

  (object id:98)      (object id:99)                 (object id:40) 
 ________________      ________________________       ______________ 
|COMMIT          |    |TREE                    |     |BLOB          |
|tree      99    |--->|tree      40  Util.java |---> |public class  |
|author    ahmet |    |blob      41  Main.java |     |function Main |
|commiter  ahmet |    |commiter  42  Print.java|     |retun null    |
|parent    97    |     ------------------------       --------------
-----------------
                                                     (object id:42) 
                                                      _____________ 
                                                     |BLOB          |
                                                     |public class  |
                                                     |function Print|
                                                     |retun null    |
                                                      ------------- 

```

Her branch, yukarıdaki gibi bir commit objesinin ID'sine fererans etmektedir.

"master" isimli branch'in diğer branch'lerdne hiçbir farkı yoktur.

yeni bir dal (branch) yaratmak için: 

> git branch b1

varolan bir dala geçmek için:

> git checkout b1

master ve test dalımız olsun. test masterdan yeni dallanmış ve sadece ek 1 değişiklik içeriyor olsun. test dalımızdaki değişiklikleri master dalına almak için bu 2 brench'i birleştirmek gerekiyor.

önce master dalımıza geçiş yapalım:

> git checkout master

> git git merge test

burada "fast forward (hızlı ileri alma)" yapmılmıştır. çünkü test masterdan türemiştir.

gitte brenç birleştirme yada başka bir birleştirme işleminde aynı dosyalar düzenlenmiş ise conflict durumu söz konusu olur. böyle bir durumda işlem devam edemez. yarıda kalır. merge edilecek dosya "git status" komutu ile "unmerged" olarak görülür. git, bu dosyaların içine uyuşmazlıkları gösteren standart formatlarda işaretler koyar. örnek:

```
<<<<<<< HEAD:index.html

<div> Hello </div>

======

<div> Hello World</div>

>>>>>>> my_branch:index.html
```

Yukarıda "Head" yazan bulunduğumuz branch'i temsil ediyor. ======= işaretinin üstü HEAD branch'inde olan metin iken, ======= aşağısı my_branch brench'indedir.

ilgili dosya (conflict olan dosya) üzerinde değişiklikleri manuel yaparız. daha sonra ilgili dosyayı "git add index.html" kayda hazır hale getiririz. daha sonrada kayıttakileri komitleyerek birleştirme işlemini tamamlamış oluruz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# gitignore
.gitignore dosyaların comitlenip comitlenemeyeceğine karar veriyor.

bazen bazı dosyalar gitignore listesinde olmasına rağmen comitlenebilir dosyalar listesinde yer alabilmektedir. bunun sebebi; o dosya/dosyaların "tracked" olmasıdır. o dosyaları önce "untracked" statüsüne geçirilmesi gerekmektedir.

bir dosyayı untracked yapmak için:

> git rm --cache /dir/file.txt

gitignore %100 regex kurallarına uymuyor. 

bazı örnekler:

```
# ignore all .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in any directory named build
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# git for windows
git resmi sitesinde (source-id: 430) download'larda görülen resmi olmayan bir git forkudur.

bu repo'da geliştirilmektedir: (source-id: 431)

official git paketi; windows için build edildiğinde "git bash" gibi programlarda yüklenmektedir. zaten windows için çıkılan build arkaplanda shell bağımlılıkları vardır. çünkü "git" windows için tasarlanmamıştır. "git for windows" ise, resmi git'in bu kısımlarını ortadan kaldırmaya çalışır. çözüm olarak windows için git'in sadece POSIX uyumlu kısımlarını tekrar native olarak yazmaktadırlar.

git-bash.exe bu proje ile yüklü gelir. Git tümüyle C'de yazılmamıştır. Bir kısmı shell ve Perl içermektedir. Bu kısımlar tekrardan yazılması (ve yeni güncellemelerin desteklenmesi) büyük maliyet olduğundan bu kısmı kapatmak için git-bash.exe ile birlikte gelmektedir. kaynak: (source-id: 140) 2inci paragraf.

git-bash.exe eskiden msys için özel üretilen bir fok'u (__msysGit__) ile gelirken daha sonra msys2'tye geçilmiştir. kaynak: (source-id: 140) 3üncü paragraf.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# git değişiklikleri nasıl tutar

git değişiklikleri dosya olarak tutar. sadece değişiklik olan textleri ve satır numaralarını değil.

komut satırından yapılan her aksiyonu veritabanına kaydeder. bu şekilde her şey geri alınabilir ve kaybolmaz.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Git reset çeşitleri

A bir comit noktası olmak üzere;

> git reset --soft A

A noktasına HEAD'ı çeker. Fakat A'dan sonra yapılmış tüm komitlerdeki dosyaları staged olarak atar (ready to commit).

> git reset --mixed A (or git reset A)

A noktasına HEAD'ı çeker. Fakat A'dan sonra yapılmış tüm komitlerdeki dosyaları değiştirilmiş hale getirir. yani son kullancı önce u dosyaları staged yapıp öyle comitleyebilir.

> git reset --hard A

A noktasına HEAD'ı çeker. A'dan sonra yapılmış tüm comitteki dosyalar yok olur.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# rebase vs merge

ikiside farklı branchleri birleştirmek için kullanılan komutlardır. 

- rebase

  iki branchi rebase ile birleştirirsek; bir branchteki her komiti tek tek diğerinin sonuna eklemiş oluruz. 
  
- merge

  merge işlemi ise tüm değişiklikleri birden tek komitte birleştirmemizi sağlar.

"rebase" ve "merge" işlemi (komutu); o anda bulunan branch üzerinde değişiklik yaptırır. diğer branchlere hiç dokunmaz.

"pull" işlemi; "fetch from upstream" ve "rebase" işlemlerine denk gelir. burada "rebase" işlemi; local branch ile remote branchi rebase etmektedir.

remote branchler olmak zorunda değildir. kişi kendi içinde tek local-repo ile de geliştirme yapıp comitleyebilir. comitler local repoya atılır. "push to upstream" yapıldığında (eğer remote anında onay vermiyorsa, örneğin arada gerrit var ise), eclipse'de remote kısmında hala remote-branch'in geride kaldığı(comiti almadığı) görülür. yani aslında biz eclipse'te çalışırken sadece local branchlerimizde oynama yapabiliyoruz. remote tüm branchler sadece birer yansımadır. 

# fast forward merge vs no-fast forward merge

- "fast forward" merge işleminin bir özelliğidir.
- git default olarak fast-forward merge yapmaya çalışır. "--no-ff" parametresi geçilerek bu durum engellenebilir. 
- Fast forward merge'de rebase'deki gibi tüm comitler zincirleme olarak eklenir.
- "no-fast forward" da ise tüm comitler tek bir merge comiti olarak görünür.
- "squash", "no-fast forward" tamamen aynıdır. tek fark: squash'te gir merge yapıldığını bilmezken, "no-fast forward" da, git; merge olduğunu bilir.

örnek git log:

```
* (b1) c3
* c2
* (b2) c1
```

b2 branch'indeyken şu komutları verirsek:

```sh
git merge --no-ff --no-commit b1
# b1 deki tüm değişiklikleri master'da staging'e alır ve commit mesajını hazır tutar. 

git commit -m "c4"
# comit mesajında; b1'deki her comit mesajı ayrı ayrı birleştirilmiş şekilde yer alır. fakat biz bu komut ile birlikte commit mesajını ezmiş olduk.
```

git log şu şekilde olacaktır:

```
* (b2) c4
|\
| \
|  * (b1) c3
|  * c2
| /
|/
* c1
```

farklı bir örnek ile ilerleyelim:

örnek git log:

```
* (b1) c3
* c2
* (b2) c1
```

b2 branch'indeyken şu komutları verirsek:

```sh
git merge --no-commit b1 # --no-ff olmadığı için bu durumda fast forward merge olacak
# b1 deki tüm değişiklikleri master'da staging'e alır ve commit mesajını hazır tutar. 

git commit -m "c4"
# comit mesajında; b1'deki her comit mesajı ayrı ayrı birleştirilmiş şekilde yer alır. fakat biz bu komut ile birlikte commit mesajını ezmiş olduk.
```

git log şu şekilde olacaktır:

```
* (b1) (b2) c3
* c2
* c1
```

# rebase
rebase işleminin merge'e göre ekstra yetenekleri vardır. örnek:

git logumuz bu olsun:

```
* (b1) c102
* c101
|
|  * (b2) c201
|  * c200
|  | 
|  |      * (b3) c301
|  |      * c300
|  |     / 
|  |    /
|  |   /
|  |  /
|  | /
|  * c999
| /
|/
* c100
```

> git rebase --onto b1 b2 b3

Yukarıdaki komut b1 branch'ine b3'teki her komiti tek tek inject eder. fakat b2'de olan ara komit var ise onları almaz. yani c999'u almayacak. son durum şu şekilde olacaktır:

```
* (b3) c301
* c300
* (b1) c102
* c101
|
|  * (b2) c201
|  * c200
|  | 
|  * c999
| /
|/
* c100
```

# strategies
merge işlemi fast forward değilse "-s" ile birçok strateji parametresi alabilir:

- recursive
- resolve
- octopus
- ours
- subtree

Her stratejinin ise kendine özgü parametreleri vardır. bunları komut satırında "-X" parametresinin yanında giriyoruz. örneğin recursive'in kabul ettiği bazı parametreler:

- ours
- theirs
- ignore-space-change

# ours
hem -X hemde -s ile yollanabilir ve ikisinin işlevi farklıdır.

> git merge -X ours b2

b2 branch'ini merge eder fakat eğer herhangi bir dosyada conflict olursa sadece current branch'i doğru olarak kabul eder.

> git merge -s ours b2

"-X ours" ile aynı işlevi görür. Ek olarak; b2'den curent-branch'te olmayan bir dosya gelirse o zaman o dosyayı kabul etmez. sonuç olarak bakıldığında "-s ours" current-branch'te hiçbir değişiklik olmamasını sağlar. bu komut git'e merge işlemi olduğunu bildirmek için yapılır.

# squash
kelime anlamı: ezmek

merge işlemine geçilen özel bir parametredir.

örnek git log:

```
* (b1) c3
* c2
* (b2) c1
```

b2 branch'indeyken şu komutları verirsek:

```sh
git merge --squash b1
# b1 deki tüm değişiklikleri master'da staging'e alır ve commit mesajını hazır tutar. 

git commit -m "c4"
# comit mesajında; b1'deki her comit mesajı ayrı ayrı birleştirilmiş şekilde yer alır. fakat biz bu komut ile birlikte commit mesajını ezmiş olduk.
```

git log şu şekilde olacaktır:

```
* (b2) c4
|
|  * (b1) c3
|  * c2
| /
|/
* c1
```

Dikkat edilirse git merge yapıldığı gilgisini tutmuyor.

"--no-squash" parametresi ile squash yapılmamasını sağlayabiliriz.

# --continue

> git merge --continue

şeklinde merge'e parametre olarak geçilir.

merge işlemi yapıldığında conflict olursa, git; conflict'leri gidermemizi bekler. o sıra merging moduna girer. artık user merge'u abort etmeli yada mergü conflict'leri tammalayıp sonlandırmalıdır.

--continue parametresi git komutuna pass edildiğinde, git merging modundan sonlanma moduna girer. (merge işlemini tamamlamak için devam etmiş olur. "continue" terimi buradan geliyor.)

Git --continue işlemi sonrası genelde komit atılır. bu sebeple git 2.12.0 ile git commit artık --continue parametresi ile aynı işi görmektedir. kaynak: (source-id: 142) change log'da şu şekilde yazmaktadır: "git merge --continue" has been added as a synonym to "git commit" to conclude a merge that has stopped due to conflicts.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# hook

türkçe kelime anlamı: çengel, tuzak.

./.git/hooks içerisinde birçok script dosyası mevcut. bu scriptler her git event'i ile birlikte çağrılmaktadır. eğer scripler commit'te bir terslik olduğuna karar verirlerse, event'i yarıda kesebiliyorlar. örneğin pre-commit script'i eslint hatalarına bakabilir. eğer eslint hatası varsa comite izin vermez.

geçici bunu aşmak istiyorsak komut satırından;

--no-verify

parametresi her git komutunun sonuna eklenebilir. yada  pre-commit scriptinin içeriği elle silinebilir.

hook scriptleri client side'da olduğu için yazılımcı tarafından silinebilir veya esgeçilebilir. bu sebeple sunucu tarafta da hook yapılabilir.

hook scriptleri birer scritptin language ile yazılmış dosyalardır. internetten rastgele örnek bir pre-comit hook'una dosyasının tepsine bakıldığında #!bin/bash veya php gibi tanımlar görürür. git bu script'e parametre geçer ve exit code'una bakarak işlemin kesilip kesilmeyeceğine karar verir.

örneğin; projemizdeki .git/hooks/commit-msg.sample doyası örnek bir sciprt içerir. bu devrede diildir. devreye almak için bu dosyanın sonundaki .sample'ı silmemiz gerekir. bu örnek shell script'i ile yazılmıştır. biz bu dosyanın içerğini tümü ile silip nodejs ile çalışmasını sağlayabiliriz. "commit-msg" dosyası git tarafından, commit mesajı girildikten hemen sonra execute edilir. örnek bir commit-msg dosyası:

```js
#!/usr/bin/env node

var COMMIT_MSG_MIN_LENGTH = 50;

console.log("");
console.log("commit-msg hook started");
console.log("");

const fs = require('fs');
const commitMessage = fs.readFileSync(process.argv[2], 'utf8').trim();

const childProcessExec = require('child_process').exec;
const util = require('util');
const exec = util.promisify(childProcessExec);

checkBranchNameAndMessage();

function errorHook(erroMsg){
  console.log("");
  console.log("error detail: " + erroMsg);
  console.log("");
  process.exit(1);
}

async function checkBranchNameAndMessage(){
  const allBranches = await exec('git branch');
  currentBranch = allBranches.stdout.split('\n').find(b => b.charAt(0) === '*').trim().substring(2);
  
  console.log("");
  console.log("currentBranch:" + currentBranch);
  console.log("commit message: " + commitMessage);
  console.log("");

  if(commitMessage){
    if(commitMessage.length > COMMIT_MSG_MIN_LENGTH){
       
    }else {
      errorHook("commit message length is less then " + COMMIT_MSG_MIN_LENGTH);
    }
  } else {
    errorHook("commit message is not defined!");
  }
  
}
```

Yukarıdaki kod nodejs üzerinde çalışacaktır.
- process.argv environment'ten değer çekebilmemizi sağlıyor.
- process.exit exit code'umuzun istersek 0 dan farklı olmasını sağlıyor ve commit işlemini yarıda kesiyor
- hook dizininde npm yada nomedule olmamasına rağmen, "require('fs');" yapabiliyoruz. bunun sebebi nodejs'in runtime'da bazı module'leri default olarak inject etmesidir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# branch değiştirme

branch değiştirince; staged'de duran veya unstaged'de duran dosyalara hiçbir şey olmaz. oldukları yerde kalmaya devam ederler.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Tracking Branches
git push ve pull komutlarının ek parametreye ihtiyaç duyulmadan çalışmasını sağlar. her branch'in takip ettiği branch'ler vardır. her brnach'in "tracking branch"i olabilir. dolayısı ile push ve pull direk tracking branch üzerinden çalışır.

örnek:

```sh
git checkout --track origin/fix1

# output:
# Branch fix1 set up to track remote branch refs/remotes/origin/fix1.
# Switched to a new branch "fix1"
```

Localde farklı isimde branch istiyorsak:

```sh
git checkout -b fix1_local origin/fix1

# output:
# Branch sf set up to track remote branch refs/remotes/origin/fix1.
# Switched to a new branch "fix1_local"
```

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# stash

türkçe kelime anlamı: güvenli bir yere gizlemek, saklamak.

stagede olan yada olmayan dosyaları (comitlenmemiş dosyaları) yedek alabiliriz. stashteki bu dosyaları istediğimiz zaman istediğimiz branch'e apply edebiliriz.

birden fazla stash'imiz olabilir. tümünü şu şekilde listeleyebiliriz:

```sh
git stash list

# output:
# stash@{0}: WIP on master: 049d078 Create index file
# stash@{1}: WIP on master: c264051 Revert "Add file_size"
# stash@{2}: WIP on master: 21d80a5 Add number to log
```

stage'de olan değişikliklerimizi şu şekilde stash'e alabiliriz:

> git stash

başka branch'e geçip yada aynı branch'te istediğimiz zaman apply edebiliriz:

> git stash apply stash@{2}

Eğer en son yarattığımız (en güncel) stashi apply etmek istiyorsak hiçbir şey belirtmemize gerek yok:

> git stash apply

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# comit id

sha-1'dir ve unique'tir. "git log" komutu ile git history'yi hashleriyle birlikte görebiliriz.

spesifik bir komite bakmak istersek "git show 09fsaa" ile hash'in sadece birkaç karakterini girmemiz yeterli oluyor.

"git rev-parse master" komutu ile master branchindeki en son komitin hash'ini döndürmekteyiz.

# refs

references'in kısaltmasıdır. ref'ler comit'lerin birer referansıdır. alias gibi düşünülebilir. ref'ler basit doayalar şeklinde tutulur. ".git/refs" dizini içerisindedirler.

örneğin;

.git/refs/remotes/origin/master dosyasında sadece bir satır yazar ve bu satırda remote'un bulunduğu head (muhtemelen son komitin) komitin id'si (hash'i - sha1) vardır.

.git/refs/heads/master dosyasıda benzer şekilde local repo'daki son komitimizin hash'ini tutar.

.git/refs/remotes/origin dosyasında "ref: refs/remotes/origin/master" yazmaktadır. bu satır farklı bir yere referans sağlanmaktadır.

"git show master" komutu master dosyamızdaki comit-id yi alır ve bize o komit hakkında detayları gösterir. bu komut yerine bu komutu da yazabilirdik:

"git show refs/heads/master"

# Refspecs

reference spesifications'ın kısaltmasıdır.

git, push komutunda hangi referansın hangi referans ile ilişkilendirileceğinini tutmak zorundadır. formatı: 

> source:destination

şeklindedir. örneğin;

> git push origin master:refs/heads/qa-master

yukarıdaki komuttta; "refs/heads/qa-master" remote makinadaki dizindir.

Refspecs formatında opsiyonel "+" (artı) işareti gelebilir. bu uzak masaüstüne non-fast-forward update yapmasını istediğini söylemek içindir.

# delete remote branch

asagidaki komutta source olmadığı için boştur ve uzaktaki makinada "remote-branch-name" isimli breanch'i siler.

> git push origin :remote-branch-name

git'in güncel versiyonlarında remote branch'i silmek için ek komut gelmiştir:

> git push origin --delete remote-branch-name

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# Reflog

git'te herşey burda loglanmaktadır. silinen branchler dahi buradan geri getirilebilir.

Fakat git, aralıklarla erişilmeyecek objeleri silmektedir. bu sebeple %100 herşeyin sürekli geri getirilebilir olduğunu söylemek mümkün diil. kaynak: (source-id: 143) "Redo after undo “local”" başlığındaki ikinci madde.

tüm değişiklikleri listeleme:

>  git reflog show --all

Sadece HEAD'imizde olan her değişikliği listemeleme:

```sh
git reflog # default olarak şuna denk geliyor: git reflog show HEAD

# OUTPUT:
# eff544f HEAD@{0}: commit: migrate existing content
# bf871fd HEAD@{1}: commit: Add Git Reflog outline
# 9a4491f HEAD@{2}: checkout: moving from master to git_reflog
# 9a4491f HEAD@{3}: checkout: moving from Git_Config to master
# 39b159a HEAD@{4}: commit: expand on git context
# 9b3aa71 HEAD@{5}: commit: more color clarification
# f34388b HEAD@{6}: commit: expand on color support
# 9962aed HEAD@{7}: commit: a git editor -> the Git editor
```

If you want to restore the project’s history as it was at that moment in time use:

```sh
git reset --hard <SHA>
```

If you want to recreate one or more files in your working directory as they were at that moment in time, without altering history use:

```sh
git checkout <SHA> -- <filename> 
```

Yukarıdaki iki örnek komut için kaynak: (source-id: 143) "Redo after undo “local”" başlığındaki son paragraf.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# pull request (or PR)

sadece github'da kullanılan bir terim değildir. genel bir ibaredir. git altyapısında da kısmen barındırılan bir özelliktir.

- ### git altyapısında bulunan pull request

  feature_1_branch push'larız. daha sonra:

  ```sh
  git request-pull master_branch https://git/project1 feature_1_branch
  ```

  Artık upstream'de bulunan review/mail sistemi otomatik herkese email atacaktır. bu işlem sadece bildirim için kullanılır. yetkili kişilerin özel bir pull işlemi için imkan yoktur.

- ### github için "pull request" ve gitlab için "merge request"
  github'daki pull request'in, GitLab'deki karşılığıdır. tamamen aynı mantıkta çalışırlar.

  X branch'ini Y ranchinden oluşturarak geliştirmeye başlarız. geliştirmemiz tamamlanınca Y yi push'larız. Daha sonra gitlab/github arayüzüne girer, oradan X ve Y branchlerini belirterek merge request açarız. Yani Y'deki komitleri X'e merge etmeleri için yetkilililere bildirim yollarız. yetkilililer onaylarsa bu kod otomatik yine gitlab/github arayüzündenmerge edilir.

  gitlb/github arayüzü kullanmak istemiyorsak gitlab/gihub command line tool'u bulmamız gerekir.

  yukarıda anlatıldığı gibi github bir branch'ten pull request yaratabilmemize izin veriyor. ek olarak github, for oluşturduğumuz projeden de upstream'e pull request atabilmemize izin vermektedir.

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# fork

sadece github'a özgü bir terimdir. bir projeyi klonlama işlemidir. fakat bu klonlama işlemi sunucu tarafta otomatik yapılır. bir github projesini local makinamıza kopyaladığımızda ise klon yapmış oluruz.

# upstream vs origin
upstream kelime anlamı: akıntı yönüne karşı.

ikiside birer "remote" alias'ıdır. bir projeyi klonlayıp, klonladığımız projeyi tekrar locale klonladığımızda; upstream ilk/orjinal projenin remote'udur. origin ise arada olan remote'tur. 

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

• • • • • • • • • • • • • • • • • • • • • • • •

# git patch

Bulunduğumuz branch ile "masterX" arasındaki diff'i alarak bir dosyaya ("PATCH1.patch" dosyasına) patch yazılıyor:

```sh
git format-patch "masterX" --stdout > "PATCH1.patch"
```

Bu diff'i başka bir makinede apply etmemiz gerekir:

```sh
git apply "PATCH1.patch"
```

Apply etmeden önce hangi değişikliklerin apply edileceğini komut satırından görmek istiyorsak:

```sh
git apply --stat "PATCH1.patch"
```

# author vs committer
author kodu yazan kişi, commiter o kodu git veritabanına kaydeden kişidir. patch dosyasi ile birine bir şey attığımızda; o patch'i hazırlayan kişi author, patch'i karşıdaki kişi comitlerse, o kişi commiter oluyor.
