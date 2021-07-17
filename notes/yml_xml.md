############################

############################
# YML AND XML
############################

############################

# yaml (or YAML Ain't Markup Language)

boşlukların, satır sonlarının önemli olduğu XML ve JSON'a alternatif bir formattır. .yml veya .yaml uzantıları ile dosyalarda tutulurlar.

json'a göre daha çok özelliğe sahiptir ve okunaklığı daha fazladır.

yaml editor kullanmadan editlemek çok zordur. ve tab karakteri kabul görmemektedir/kullanılmamaktadır.

yaml dökümanı isteğe bağlı olarak --- ilen başlayıp ... ile bitebilir. 

örnek yml:

```yml
# yaml supports comments, json does not

array: 

  - first element of array

  - second element of array

  

# string yazraken tırnak or tırnak koymasakta olabilir

stringObject:

  'key': 'any string here'

  "key2": "any other string here"

  key3  : any other string here

#tipler otomatik algılanır. eger bir integer'ı string algılatmak istiyorsak; o zaman tırnak kullanmak zorundayız.

types:

  - 1

  - "1"

  - true

  - "true"

# yes ve no'lar true false olarak algılanıyor

booleanTypes:

  - no 

  - yes

  - NO 

paragraph: >

  my name

  

  is ahmet

# or sonuna bir tire işareti de atılabilir content: |-

content: |

   my name

   

   is ahmet

# biraz farklı da olsa json tarzı bir formatta da veriler tutulabiliyor

ornekJson: {name: Martin Developer}
```

yukarıdaki yaml'a denk gelen json aşağıdaki gibidir:

```json
{

  "array": [

    "first element of array",

    "second element of array"

  ],

  "stringObject": {

    "key": "any string here",

    "key2": "any other string here",

    "key3": "any other string here"

  },

  "types": [

    1,

    "1",

    true,

    "true"

  ],

  "booleanTypes": [

    false,

    true,

    false

  ],

  "paragraph": "my name\nis ahmet\n",

  "content": "my name\n\nis ahmet\n",

  "ornekJson": {

    "name": "Martin Developer"

  }

}
```

# yaml format standartları

> YAML 1.2 (3rd Edition) - 2009-10-01-  http://yaml.org/spec/1.2/spec.html

> YAML 1.1 (2nd Edition) - 2005-01-18 - http://yaml.org/spec/1.1/

> YAML 1.0 (1st Edition) - 2004-01-29 - http://yaml.org/spec/1.0/

# json format standartları

> March 2017 - RFC 7493 - This document specifies I-JSON, short for "Internet JSON"

> March 2014 - RFC 7159 - draft of "I-JSON"

> March 2013 - RFC 7158 - draft of "I-JSON"

> October 2013 - ECMA-404 - JSON standard at ECMA

> July 2006 - RFC 4627 - first json public doc

Yukarıdaki standartlar az da olsa biribiri arasında fark ediyor. bazı parser/validatorlarda bu bilgi lazım olabilir.

__JSON5, jsonc, Hjson__ json'dan bağımsız fakat ondan türemiş farklı standartlardır.

# xml format standartları
W3C.org'da xml standartları belirlenmiştir. W3C.org da bir spesifikasyon bu süreçlerden geçer:

1. Working Draft (WD)
2. Last Call Working Draft
3. Candidate Recommendation (CR)
4. Proposed Recommendation (PR)
5. W3C Recommendation (REC)

http://www.w3.org/TR/xml/ URL'si her zaman son sürüme otomatik yönlendirir.

> 1.0 (W3C Recommendation of Fifth Edition) - http://www.w3.org/TR/2008/REC-xml-20081126/

> 1.0 (Proposed Edited Recommendation of Fifth Edition) - https://www.w3.org/TR/2008/PER-xml-20080205/

> 1.0 (Fourth Edition)- https://www.w3.org/TR/2006/REC-xml-20060816/

> ...

# xml (or eXtensible Markup Language)

- # terminoloji:

Aşağıdaki tüm satır bir __element__'tir.

```xml
<tag attribute="attribute's value"> tag's value </tag>
```

- # Node
Node terimi resmi olarak xml standratlarında geçmiyor. fakat "node" hep xml'in herhangi bir parçası olarak kullanılıyor. örneğin java'da org.w3c.dom.Element (xml element'i), org.w3c.dom.Document (xml dosyasının tamamı), org.w3c.dom.Attr (element'in attribute'u) gibi sınıfıların tümü org.w3c.dom.Node'dan türemiştir.

- # property vs attribute

"özellik" manasında kullanıldıklarında ingilizce'de de çok yakın anlamlı kelimelerdir. fakat farklı anlamları da vardır. bilişim dünyasında da birbirleri interchangable olarak kullanılırlar.

HTML dünyasında; browser HTML'i parse ederken attribute okur ("xml" standartlarındaki ile aynı anlamda kullanılır). Fakat HTML DOM objesi haline gelen attribute'ler, javascript'in DOM nesnesinden okunmak istendiğinde "property" olarak okunur.

Not: Fakat DOM property'si ile HTML attribute'leri aynı isimde ve tipte oluşturulmazlar. Bu konudan bağımsız (web browser standartları ile ilgili) bir not. örnek: 

```xml
<input id="input" type="checkbox" checked style="color:red">
```

- input.checked --> boolean dönüş yapar.
- input.style --> obje dönüş yapar.

Aynı zamanda DOM objelerinin hala getAttribute isimli fonksiyonu vardır:

```js
input.getAttribute("style") // her zaman string dönüş yapar.
```

Oysa DOM standartlarında input.style'daki "style" bir property olarak adlandırılır.

- # ? karakteri

ilk satırda encoding ve xml-version'u bu şekilde belirtilebilir:

```xml
<?xml version="1.0" encoding="UTF-8"?> 
```

- # XML Namespace

```xml
<table>

  <tr>

    <td>Apples</td>

    <td>Bananas</td>

  </tr>

</table> 

<table>

  <name>African Coffee Table</name>

  <width>80</width>

  <length>120</length>

</table> 
```

yukarıdaki iki farklı xml tek bir xml'de birleştirmiş olalım. fakat isimlendirmeler benzediği/aynı olduğu için sorun olur. bunu çözmek için elemenlerin önüne prefix atılır.

```xml
<h:table>

  <h:tr>

    <h:td>Apples</h:td>

    <h:td>Bananas</h:td>

  </h:tr>

</h:table>

<f:table>

  <f:name>African Coffee Table</f:name>

  <f:width>80</f:width>

  <f:length>120</f:length>

</f:table> 
```

namespacelere isteğe bağlı "xmlns" ile id verilebilir. fakat genelde id yerine o namespace için dökümantasyon url'si yazılır. çünkü url'de genelde unique'tir. örnek:

```xml
<h:table xmlns:h="http://www.w3.org/TR/html4/">

  <h:tr>
```

yada şu şekilde:

```xml
<root xmlns:h="http://www.w3.org/TR/html4/">

   <h:table>
```

# XSL (or Extensible Stylesheet Language)

XML ile ilgili tüm standratların ailesine verilen isimdir. Altında XSLT, XPath gibi standratlar bulunmaktadır.

# XSLT (or XSL Transformations)

XML dökümanını, yine bir XML dosyasına dönüştürmek (farklı bir şema üzerine transfer etmek) için kullanılan XML tabanlı dildir. Yazılımcılar arasında XSL olarak adlandırılır, oysa sadece "XSL" farklı bir kavramdır.

örnek xslt asagidadır. bu xslt'yi xml dköümanını da vererek işletirsek; output olarak bir liste alırız.

xslt:
```xml
<xsl:stylesheet>

  <xsl:output method="text"/>

  <xsl:template match="/">

    Article - <xsl:value-of select="/Article/Title"/>

    Authors: <xsl:apply-templates select="/Article/Authors/Author"/>

  </xsl:template>

  <xsl:template match="Author">

    - <xsl:value-of select="." />

  </xsl:template>

</xsl:stylesheet>
```

xml:

```xml
<Article>

  <Title>My Article</Title>

  <Authors>

    <Author>Mr. Foo</Author>

    <Author>Mr. Bar</Author>

  </Authors>

  <Body>This is my article text.</Body>

</Article>
```

output:

```
Article - My Article

Authors:

- Mr. Foo

- Mr. Bar
```

output olarak aldığımız listenin "Authors" stringinin sağına ve soluna <div> atsaydık, saf liste yerine html çıktısı almış olacaktık.

# XPath

XML dökümanındaki bir verinin yerini gösermek için kullanılan path yapısı. ELimizde XML olsun. İçeirisnden aşağıdaki path'lerle açıklaması yazan bilgiler çekilebilir:

```
/items/philosphy[2] : Philosphy deki ikinci item

/items/*/dictionary : Bütün Sözlükler

/items/*/book[@id="12"]/@title : Id'si 12 olan kitabın title'ı

count(/items/sociology/book) : Sociology kitaplarının sayısı

/items/psychology[last()] : Son psychology kitabı

/items/*/[contains(@title,"Turk")] : İçerisinde Turk geçen bütün maddeler
```

# XQuery

SQL'e benzer şekilde; bir XML dökümanından veri çekebilmek için query dilidir. Örnek:

```xquery
for $x in doc("books.xml")/bookstore/book

where $x/price>30

order by $x/title

return $x/title
```

# XML Schema Definition (or XSD) vs document type definition (or DTD)

ikiside birbirindenbağımsız XML şeması belirtmek için yaratılmış dillerdir. XML içerisindeki elementlerin sırasını dahi belirtebilirsiniz.

# dtd

kurallara uymasını istediğimiz xml dosyasının en üstüne aşağıdaki satırı yerleştirmeliyiz.

dtd dosyası dışardan okunur:

```xml
<!DOCTYPE note SYSTEM "kurallar.dtd">

<note>

  <to>Tove</to>

</note>
```

yada dtd bilgileri xml'in içine gömülür:

```xml
<!DOCTYPE note [

<!ELEMENT note (to,from)>

<!ELEMENT to (#PCDATA)>

<!ELEMENT from (#PCDATA)>

]>

<note>

  <to>Tove</to>

  <from>Ayse</from>

</note>
```

yukarıda 2'inci satırda elementlerin sırası verilmiş. 3. satırda "to" elementinin PCDATA, yani text olacağını belirtmiş.

# xsd

xml dökümanının şemasını referans etmek için:

```xml
<note h:schemaLocation="https://www.w3schools.com note.xsd">

<h:to>Tove</to>
```

xsd dosyasında her zaman root'ta "xs:schema" bulunmak zorunda.

sağ tarafta açıklamaları ile örnek:

(asadaki xsd'yi düzgün okuyabilmek için ekranı büyüt)

```xml
<xs:schema>

<xs:element name="note">    Note isimli bir element olması gerek.

  <xs:complexType>            Bu elementin içinde birden fazla element olacak

    <xs:sequence>             Child elementler xsd'de yazan sıra ile olmalı. sequence yerine all kullanırsak, sıralı olmak zorunda olmazlar.

      <xs:element name="to" type="xs:string"/>        child element olarak "to" isimli element olucak ve degeri string olucak. örnek <to>Ahmet</to>

      <xs:element name="from" type="xs:string"/>      child element olarak "from" isimli element olucak ve degeri string olucak. örnek <from>Ahmet</from>

    </xs:sequence>

  </xs:complexType>

</xs:element>

</xs:schema>
```

-  type="xs:string" yerine birçok farklı tip yazılabilir: Integer, Boolean, Date, negativeInteger, unsignedByte gibi birçok  standart belirlenmiştir.

- <xs:element name="to" type="xs:string" fixed="red"/>  to elementinin içindeki değerin sadece "red" olabilir anlamına geliyor

- fixed="red" yerine default="red" de yazabilir. bu durumda bu değer xml'de belirtilmezse, bir parser tarafından okunduğunda "red" okumasını emreder.

- asagidaki simpleType complex gibi değildir. simple olduğu child elementin olmayacağı anlamına gelir.

```xml
<xs:element name="age">

  <xs:simpleType>

    <xs:restriction base="xs:integer">

      <xs:minInclusive value="0"/>

      <xs:maxInclusive value="120"/>

    </xs:restriction>

  </xs:simpleType>

</xs:element> 
```

restriction için farklı bir örnek:

```xml
<xs:element name="car">

  <xs:simpleType>

    <xs:restriction base="xs:string">

      <xs:enumeration value="Audi"/>

      <xs:enumeration value="Golf"/>

      <xs:enumeration value="BMW"/>

    </xs:restriction>

  </xs:simpleType>

</xs:element> 
```

restriction kendi içinde birçok farklı özellik daha barındırıyor.

xsd'lerde tipleri önceden define edebiliriz. örnek:

```xml
<xs:element name="product" type="prodtype"/>   Define ettik

<xs:complexType name="prodtype">      Burada kullandık

  <xs:attribute name="prodid" type="xs:positiveInteger"/>   Attribute isteğe bağlı (konudan bağımsız bir özellik)

</xs:complexType> 
```

# XML External Entities (or XXE)
XML dosyalarının tepesinde belirtilen dışa kaynakları temsil etmek için kullanılan bir terimdir. B u dış kaynaklar XML'in şemasını belirlemek için kullanılır.

XEE'de belirtilen şema dosyası dışarıda herhangi bir URL'de olduğundan, programımız o şemayı okumak istediğinde güvenlik açığı oluşabilir. Bu sebeple zorunlu diilse şema okumayı iptal etmeliyiz. Önrke java kodu:

```java
import javax.xml.stream.XMLInputFactory;
import javax.xml.stream.XMLStreamException;
import javax.xml.stream.XMLStreamReader;

XMLInputFactory factory = XMLInputFactory.newInstance();

// disable resolving of external DTD entities
factory.setProperty(XMLInputFactory.IS_SUPPORTING_EXTERNAL_ENTITIES, Boolean.FALSE);

// or disallow DTDs entirely
factory.setProperty(XMLInputFactory.SUPPORT_DTD, Boolean.FALSE);

// load xml file
XMLStreamReader xmlStreamReader = factory.createXMLStreamReader(fis);
```

Bunun birçok güvenlik sorununa sebep olabilir:
- hacker, şemayı local dosya olarak gösterirse, uygulama local dosya okunmaya çalışacaktır. local dosya okunamazsa excepiton fırlatacaktır. hacker bu şekilde dosyanın varolup olmadığını anlayabilir.
- hacker, sistemi yavaşlatmak için dışarıdaki büyük bir dosyaya şema referansı verir. Şemayı parse etmek yorucu olacağından sistemi durdurma noktasına getirebilir.
