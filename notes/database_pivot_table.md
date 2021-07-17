############################

############################
# DATABASE PIVOT TABLE
############################

############################

# pivot table

pivot türçe anlamları: en önemli nokta, püf nokta, çark etmek, eksen üzerinde dönmek.

pivot olarak belirlediğimiz sutuna ait satırları, sutun haline çevirip oluşturduğumuz tabloya pivot tablosu denir.

en basit örnekle ilerleyelim:

- bir siparis tablomuz var.

- Bir müsterinin verdigi her bir siparis bir satirda gösteriliyor.

- Her müsteri için son 6 aylik siparis bilgilerini görmek istiyoruz.


> ||| SiparisID ||| MusteriAdSoyad ||| UrunAdi ||| Tutar ||| Donem |||

tablomuz olsun.

pivot tablomuzu oluşturursak;

```sql
SELECT *

FROM (

      SELECT 

       MusteriAdSoyad

      ,Donem

      ,sum(Tutar) as ToplamTutar  

      FROM Siparis

      group by MusteriAdSoyad ,Donem

     ) as gTablo

PIVOT

(

  SUM(ToplamTutar)

  FOR Donem IN ([200911],[200912],[201001])

)

AS p
```

Tablomuz şöyle olacaktır:

> ||| MusteriAdSoyad ||| 200911 ||| 200912 |||

MS Excel gibi uygulamalarda da pivot tablosu yapabilmek için fonksiyonlar hazır sunulmaktadır.
