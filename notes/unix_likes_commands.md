############################

############################
# UNIX LIKES COMMANDS
############################

############################

# bazı komut satırı uygulamaları + shell buildin'ler

## which

farklı path'lerde aynı isimde birçok dosya olabilir. örneğin; "which vlc" bize hangi dizindeki vlc'yi execute edeceğini gösterir.

## where

paramatre aldığımı komutun nerelerde olduğunu listeler. which tek bir dizin dönerken, where birden fazla dönebilir.

## echo

parametre aldığı string'i stdout'a yollar.

echo -e "hello \n \a" 'da bulunan -e parametresi stdout'a yollanacak string parametresindeki \n ve \a nın özel karakterler olduğunun algılanmasını sağlar. yani; \n satır sonu \a ise beep sesi çıkaracaktır. özel karakterlerin tüm listesi:

```
\a      alert (bell)
\b      backspace
\c      suppress further output
\e      escape character
\f      form feed
\n      new line
\r      carriage return
\t      horizontal tab
\v      vertical tab
\\      backslash
\0nnn   the character whose ASCII code is NNN (octal).  NNN can be 0 to 3 octal digits
\xHH    the eight-bit character whose value is HH (hexadecimal).  HH can be one or two hex digits
```

-n paramtresi echo komutunun sonuna satır sonu karakteri eklemesini sağlar.

echo çoğu sistemde built-in komut'tur. -n ve -e parametreleri çoğu komut satırı interpreterında default olarak zaten echo komutuna yollanır.

-E parametresi, escape karakteri --> \ ile belirtilen string'lerin özel karakterler olarak algılanmamasını sağlar.

## printf

parametre aldığı string'i stdout'a yollar. echo'ya göre ektra bazı özellikleri vardır.

## pwd

(Print Working Directory) Bulunduğunuz dizinin ismini verir.

## hostname

Makinanın ismini verir.

## whoami

(Who Am I?) Sisteme giriş yaparken yazdığınız kullanıcı isminizi verir.

## uptime

Makinanın ne kadar süredir açık olduğu bilgisini verir.

## cd abc

(Change Directory) abc path'ine gider. cd bir komut satırı uygulaması değildir. komut satırı uygulamasının bir özelliğidir.

## mkdir abc

(Make Directory) bulunduğu dizinde abc isminde klasör oluşturur

## grep xyz abc

abc dosyasındaki, xyz string'inin oldugu satırları dondurur

## ls

bulunduğu dizindeki dosyaları listeler

## top

çalışmakta olan process'lerin detaylı listesi

## history

komut satırında daha önce verilen komutların listesini çıkartır.

## cat dosya.txt

prints the file

## nano file.txt

basit text editor

## vim

__vi__ editoründen esinlenerek yapıldığı için bu ismi almıştır.

__gvim__; gtk penceresi içine gömülmüş bir terminalde vim çalıştırılmaktadır. ek olarak toolbar butonları bazı komutları yerine getirmk amaçlı sunmaktadır. bu tarz birçok vim forku mevcuttur.

__vim-gnome__ ve __vim-gtk__ farklı bağımlılıklarla derlenen iki benzer fakat gvim tarzı forklardır.

__vim-tiny__ vim'i tüm özelliklerini barındırmayan bir forkudur. komut satırından __vi__ yada __vim.tiny__ olarak çağrılır. ubuntu ve türevlerinde bu paket yürklü gelmektedir. 

vim'in birçok modu var:
- insert mode
- normal mode
- visual mode

vim'in hangi modda olduunu en aşağıdaki panelde yazmaktadır. vim ilk açıldığında insert modda başlar. insert modda klavyeden girilenler, dosyayı düzenlemek için kullanılır.

ESC tuşu ile normal moda geçiş yapılır.

Normal mod'dayken de sağa sola gidilebilir. bunun için sağa sol yerine, h j k l tuşları (or farklı tuşlar konfigüre edilebilir) kullanılabilir.

normal mod'da, 4 karakter sağa gidilecek ise; 4 ardından da "l" karakterine basılır.

notmal mod'da sırası ile c,4,l tuşlarına basıldığında ise 4 karater sağa gider, ardından da otomatik insert moda geçeriz. c karakteri bunu yapar.

normal mod'dayken insert mode'a geçiş yapmak için i tuşuna bsmalıyız. eğer a tuşuna basarsak bizi insert tuşuna alır fakat imleci bulunan karakterin sağına atar.

normal moddayken komut girebiliriz. bunun için normal moddayken yada insertt mod'dayken : tuşuna basmalıyız. ardından da komutumuzu gireriz. örnek:

> :q

vim'i kapatır.

> :q!

değişiklikleri kaydetmeden kapatır

> :wq

değişiklikleri kaydederek çıkar.

> :w

sadece değişiklikleri kaydeder. vim'i kapatmaz.

visual mode'a geçiş yapabilmek için v tuşuna basılmalıdır. v tuşuna basıldıktan sonra karakter grubu seçimi yapabiliriz. burada hem mouse supportu var, hemde yine ghjk karakterleri ile sağa sola gidip seçim yapabiliyoruz. 4 ardından da "l" tuşuna basarsak, 4 karakter sağa doğru seçim yapılmış olur gibi...

## neovim

komut satırından __nvim__ ile çağrılır. vim forkudur. çok gelişmiş özelliklere sahiptir.

## emacs

bu terim; genişletilebilir komut satırı text editörlerine verilene genel bir isimdir. tek başına bir uygulama değildir. mutlaka kendini emacs olarak belirten bir türevini kurmak gereklidir. "GNU Emacs", "XEmacs (or old-name:Lucid EMacs)", or "remacs" kullanılmalıdır.

komut satırından "emacs" diye çağrıldığında sistemde yüklü olan bir emacs editorü (yukarıda yazanlardan biri) çağrılır.

emacs, vim'e göre çok daha gelişmiş bir yapıya sahiptir. fakat vim'e göre konfigürasyonu daha zordur.

## more dosya.txt

prints the file. fakat ek olarak komut satırı ekrana sığmayan kısımları boşluk tuşuna basarak devamlı parça parça okumamıza olanak verir.

## head dosya.txt

print some of first lines of file.

## tail dosya.txt

prints some of last lines of file.

## head -n 5 dosya.txt

prints the first 5 lines

## tail -n 25 dosya.txt

prints the last 5 lines

## ls | grep abc

(| işareti kendinden önceki komutun çıktısını sonrakine girdi olarak aktarır.)
grep komutu; ls'nin output'unda sadece "abc" içeren satırları döndürür.

## ls | more

ekrana sığacak şekilde dosya isimlerini listeler. sığmayanları boşluk tuşuna basarak görebiliriz.

## less

more ile aynı görevi görüyor. less daha eski yılların bir projesi.

## netstat

socket listeleme programı

## nc
açılımı: netcat. 

komut satırı uygulaması ile bir porttan direk tcp soketi açılaması, oradan data atılıp alınması gibi hızlı network işlemleri yapmamızı sağlıyor.

## cat

dosya okuma, dosyayı başka bir dosyanın sonuna direk ekleme gibi işlemler sağlar

## ln

- kısayol oluşturur.
- "ln -s" parametresi symbolic link (or soft link) oluşturur.
- "-s" parametresi geçilmezse hard link oluşturur.
- posix'teki dosya sistemleri her 2 türkdeki link çeşididini de destekler.
- soft link, dosyanın path'ine işaret ediyor. dolayısı ile; link ettiğimiz dosyanın adı/path'i değişirse, linkimiz artık çalışmaz hale gelir. 
- hard link ise; dosyanın içeriğine direk link ediyor. dosya ismi değişirse, linkimiz hala doğru yere referans etmeye devam eder.

  (dosyanın içeriği ile dosyanın adresi farklı göstergelerdir)

## man
 
   man vlc

   aldığı ilk parametre farklı bir programdır. ilgili programın manuel page'sini gösteriyor.

   posix'lerde her uygulama kurulduğunda manuel dosyalarını /usr/share/man/tr/i386 (or /usr/local/man) gibi dizininlere atar. bu dizinler OS'tan OS'a değişiklik göstermektedir.

   man programı bu dizinleri kurcalar ve bize ilgili programın manuel'ini gösterir.

   manuel dosyalarında şu şekilde bir tanım görürüz:

   > command [ A ] file ...

   - A burada köşeli parantez içinde olduğu için opsiyonel parametre olduğunu temsil eder.
   
   - file ise zorunlu bir parametredir.

   - üç okta ondan bir önceki parametreden sonsuz adet alabildiğini belirtir. yani file1'in yanına; file2, file3 şeklinde dilediğimiz kadar dosya atabiliriz.

   ## section

   man sadece komutların doc'larını diil, system call gibi birçok fonksiyonunda doc'unu göstermektedir. bunlar bazı kategorilere ayrılmış durumda. kategori listesi bu şekilde:

   - 1 - User commands (Programs)
         
     Those commands that can be executed by the user from within a shell.
 
   - 2 - System calls
     
     Those functions which wrap operations performed by the kernel.
 
   - 3 - Library calls
     
     All library functions excluding the system call wrappers (Most of the libc functions).
 
   - 4 - Special files (devices)
     
     Files found in /dev which allow to access to devices through the kernel.
 
   - 5 - File formats and configuration files
     
     Describes various human-readable file formats and configuration files.
 
   - 6 - Games
     
     Games and funny little programs available on the system.
 
   - 7 - Overview, conventions, and miscellaneous
 
     Overviews or descriptions of various topics, conventions and protocols, character set  standards, the standard filesystem layout, and miscellaneous other things.
 
   - 8 - System management commands
   
     Commands like mount(8), many of which only root can execute.

   örnek:

   "man 1 read" komutu read komutunun doc'unu gösterecektir. fakat "man 2 read" read system call'unun doc'unu gösterecektir.

   örnek2:

   (source-id: 314) sayfası bize read'in system call'unun doc'unu gösteriyor.

## httpie

   wget ve curl'a alternatif modern bir komut satırı http client uygulaması. modern uygulamaların strest testlerinde dahi kullanılabilir. komut satırından "http" olarak çağrılmaktadır.

## http-prompt

   httpie kullanan fakat komut satırında otomatik tamamlama sunan bir komut satırı uygulamasıdır. interaktif çalışır. komtu satırına "http-prompt" yazıldığında interaktif moda geçer.

## ldd

   List Dynamic Dependencies'in kısaltmasıdır.

   "ldd executable" komutu ile "lib.so" dosyasının link ettiği diğer bağımlılıklarını görüyoruz. bu şekilde programa tanıtacağımız lib dosyasının sistemimizde ihtiyaç duyduğu bağımlılıkları görebiliriz.

## update-alternatives

   /etc/alternatives/ ve /var/lib/alternatives/ dizinlerini düzenler. bu dizinde her amaç için (örnek x-www-browser, editor) hangi programın işletim sisteminde varsayılan olarak açılacağı bilgisi vardır. örneğin /etc/alternatives/java bir symbolic link'tir ve java'nın executable dosyasına link eder.

## dd

dd komutu cp ile yapılabilecek herşeyi yapar fakat ekstrasında bazı ek özellikler sunar. sunduğu özellikler özellikle disklere (partititonlara) yazıp okumayı kolaylaştırmaktadır. partitionlar ve diskler linuxta birer dosya olduğu için "cp" komutu ile de aynı işler yapılabilir. fakat dd bu iş için biçilmiş kaftandır.

iso formatı partition bilgilerini de tutmaktadır. bir red-hat linux iso'sunu direk dd ile çok basit şekilde bir device'a (usb'ye) aktarabiliriz. artık bu usb bootable bir OS olacaktır.

## basename

> basename '/home/user/Desktop/todo.txt'

dosya adını, örnekte; 'todo.txt'yi output'a yazar.

## dirname

> dirname '/home/user/Desktop/todo.txt'

dosya path'ini, örnekte; ''/home/user/Desktop'u output'a yazar.

## 7z
- __7-zip__ windows için dağıtılan official paketin ismidir.
- __p7zip__ 7-zip geliştiricilerinden bağımsız sunulan ve sadece POSIX'ler için geliştirilen paketin ismidir. p7zip, 7-zip'nin resmi sitesinde referans olarak gösterilmektedir.
- 7-zip'in içerisinde birçok binary vardır:
  - "__7z__" (binary/executable dosya) kendisiyle aynı dizinde olması beklenen windows'ta 7z.dll'i (linux'ta 7z.so'yu) kullanılır. __7z.dll (linux'ta 7z.so)__ asıl işi yaparken (7z engine), __7z__ binary'si sadece komut satırı API'si sunar. 7zip'in GUI'si, 7z'yi değil, 7z.dll/7z.so'yu kullanır.
  - __7zG__ ve __7zFM__ binary'leri sadece ms-windows için GUI sunmaktadır.
  - 7z.sfx - SFX module (Windows version)'dür
  - 7zCon.sfx - SFX module (Console version)'dür (7za.dll'i kullanır)
  - 7za.exe - standalone console version of 7-Zip. sadece console API'si sunmaktadır.
  - 7za.dll - library for working with 7z archives (no other dependency needed for this executable)
  - 7zxa.dll - library for extracting from 7z archives (no other dependency needed for this executable)
- "7-Zip Extra" paketi, 7-zip geliştiricilerinin dağıttığı sadece 7za'yı içeren pakettir. GUI içermez vs sadece ms-windows için çalışır.

## awk

girdi olarak multiline bir string alır ve her satırını ekrana nasıl basacağını parametre olarak alır.

örnek:

İlgili dosyanın her satırını ekrana basar:

> awk '{print $0}' myfile

- $0 for the whole line.
- $1 for the first field.
- $2 for the second field.
- ...

Her satır; "RS" yani; "input-record separator" ile birbirinden ayrılıyor. Her satır içindeki field'lar ise; "FS" yani;"the input-field separator" birbirinden ayrılıyor. Bu ayraçları override edebiliriz.

örnek:

> ss --all --processes --tcp --udp | awk -F ' ' '{print $1"\t"$2"\t"$5"\t"$6"\t"$7}'

## pushd ve popd

cd'ye alternatif komut satırı uygulamalarıdır. cd'ye göre akışta ince detaylar farketmektedir. fakat "cd" built-in oluğundan bu davranışları kesin olarak standarda dökmek yanlıştır. internette bir kaynağa göre davranışlar şu şekilde farketmektedir:

kaynak: (source-id: 315) "Adaephon" answer.

```
cd somedir
    change directory to somedir
    save the original directory in OLDPWD
    set PWD="somedir"
    replace top element of the directory stack (as shown by dirs) with somedir (the number of elements on the stack does not change).
cd -:
    change directory to $OLDPWD
    swap values of PWD and OLDPWD
    modify the top element of the directory stack to reflect (the new) PWD
pushd somedir:
    change directory to somedir
    save original directory in OLDPWD
    set PWD="somedir"
    push somedir onto the directory stack (extending it by one element)
popd:
    save original directory in OLDPWD
    remove first element of the directory stack
    change directory to the new top element of the directory stack
    set PWD to the new top element of the directory stack
```

# alias

komut satırı dünyasında alias bir komutun yerine kullanılan keyword'dür. örneğin;

> alias clr="clear"

komutu ile artık istediğimiz zaman "clr" komutu ile "clear" komutunu çalıştırmış oluruz.

> unalias clr

komutu ile alias silinir.

