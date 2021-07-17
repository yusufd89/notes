############################

############################
# C BUILD PHASES
############################

############################

# fazlar (or phases)
- preprocess
  
  derleme öncesi çalışır. başka başlıkta anlatılan keywordlerin (ifdef gibi) çalıştığı aşamadır. bu fazın çıktısı yine source koddur. fakat bir kısmı ifdef gibi tanımlar sebbei ile silinmiştir.

- compile

  kod, makinenin anlayacağı dile çevriliyor. bu faz sonucunda __object code (or object file)__ elde edilir.

  genelde __.o__ uzantılıdır. c'den türemiş bazı dillerde __.obj__ olarakta kullanılır.
  
  object code'da diğer kütüphaneler henüz linklenmediği için düzgün çalışamaz.

- link

  kütüphanelerin birleştirildiği/linklendiği fazdır. artık object code'umuz executable olmuştur. 

# file formats
interface'ler ".h" (__header file__ (türkçede "__üst bilgi dosyası__" olarak çevirlir)) uzantılı, diğer tüm kodlar ".cpp" uzantılı text dosyalarında saklanması önerilir. bazı repo'larda c++ header'ları c header'ları ile karışmasın diye ".hpp" uzantılı kaydedilir.

C'de de bu şekildedir. header dosyasında fonksiyon defination'larımız durur. fonksiyonların implementasyon kodları .h dosyasında olmamalıdır. fakat olursa yine çalışır. fakat best practice değildir. ".h" dosyalarının implementasyonları ".c" dosyalarında olmalıdır. ".c" dosyaları compiler'ın kendisinde tanımlanmış olmalıdır (.c dosyası ile .h dosyası aynı isimde olma gibi bir zorunluluk yoktur). yoksa derleyici düzgün derleme yapamaz. standart olarak compiler'lar default birçok kütüphaneyi kendi içine barındırır.

# "iosstream" vs "iosstream.h"
farklı dosyalardır. c++ ilk çıtkığında "iosstream.h" kullanılıyordu. fakat namespace verilmemişti. daha sonrada std namespace'i altına taşındığıklarında eski kodlar etkilenmesin diye "iosstream" isimli kütüphane (dosya) altında dağıtılmaya başlandı.

# dll
dll dosyaları hem header (export edilen fonksiyonların bilgisi) hemde de implementasyonları barındıran dosyalardır. dll dosyasını C veya C++ 'tan kullanabilmek için, dll'e tekabül eden (c veya c++ için uygun formatta olan) header dosyasına ihtiyacımız vardır. Bu header dosyalarını build sırasında bulundurmak zorundayız, yoksa kodumuz compile etmez. Fakat runtime sırasında implementasyonumuz OS tarafından bize verilmelidir. Dll dosyaları portable olduklarından onları exe içerisine gömüpte kullanabiliriz.
