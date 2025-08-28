# Python'da Gömülü Fonksiyonlar – Ders İçeriği

## 1. Giriş

### 1.1 Python'da Fonksiyon Kavramı ve Gömülü Fonksiyonlar
- **Fonksiyonlar**, belirli işleri yapan, tekrar kullanabileceğimiz kod bloklarıdır. Python’da hem kendi yazdığımız hem de dilin bize sunduğu fonksiyonlar bulunur.
- **Gömülü fonksiyonlar** (built-in functions), Python’un standart kütüphanesinde, her zaman hazır gelen ve özel bir modül yüklemeye gerek kalmadan kullanabileceğimiz fonksiyonlardır.
- Bu fonksiyonlar, veri tipleriyle çalışma, giriş/çıkış, matematiksel işlemler, koleksiyon yönetimi, dosya işlemleri, nesne yönetimi gibi çok geniş bir alanda hayatımızı kolaylaştırır.

### 1.2 Gömülü Fonksiyonların Avantajları
- Kodunuzu daha kısa ve okunabilir yapar.
- Hızlıdır, optimize edilmiştir.
- Hata ihtimalini azaltır, güvenilirdir.
- Her yerde kullanılabilir; ek modül gerektirmez.

### 1.3 Sık Kullanılan Gömülü Fonksiyonlar ve Kategorileri
- Veri tipi ve dönüşüm fonksiyonları (`int`, `str`, `float`, `bool`, `list`, `tuple`, `dict`, `set`)
- Koleksiyon ve yineleme fonksiyonları (`len`, `enumerate`, `zip`, `range`, `sorted`, `reversed`)
- Matematiksel işlemler (`abs`, `min`, `max`, `sum`, `round`, `pow`, `divmod`)
- Fonksiyonel programlama (`map`, `filter`, `reduce`, `any`, `all`)
- Nesne ve dosya işlemleri (`type`, `isinstance`, `id`, `dir`, `getattr`, `setattr`, `open`, `help`)
- Diğer yardımcılar (`chr`, `ord`, `bin`, `hex`, `oct`, `eval`, `exec`)

---

## 2. Temel Gömülü Fonksiyonlar

### print(), input()
- Konsola çıktı yazdırmak ve kullanıcıdan veri almak için kullanılır.
  ```python
  print("Merhaba, Python!")
  isim = input("Adınızı girin: ")
  print("Hoş geldiniz,", isim)
  ```

### type(), isinstance()
- Bir değerin tipini görmek ve bir değişkenin belirli bir tipe ait olup olmadığını kontrol etmek için kullanılır.
  ```python
  x = 5
  print(type(x))               # <class 'int'>
  print(isinstance(x, int))    # True
  print(isinstance("a", str))  # True
  ```

### len()
- Dizi, string, liste gibi koleksiyonların eleman sayısını verir.
  ```python
  liste = [1, 2, 3, 4]
  print(len(liste))  # 4
  ```

### str(), int(), float(), bool()
- Tip dönüşümleri sağlar.
  ```python
  s = str(123)
  i = int("456")
  f = float("3.14")
  b = bool(0)    # False
  ```

---

## 3. Koleksiyon ve Yineleme Fonksiyonları

### list(), tuple(), dict(), set()
- Sıralı ve sırasız veri yapılarını oluşturmak için kullanılır.
  ```python
  l = list("abc")         # ['a', 'b', 'c']
  t = tuple([1,2,3])      # (1, 2, 3)
  d = dict(a=1, b=2)      # {'a': 1, 'b': 2}
  s = set([1,2,2,3])      # {1, 2, 3}
  ```

### range(), enumerate(), zip()
- Tekrarlı işlemleri kolaylaştırır, birden fazla dizinin paralel gezilmesini sağlar.
  ```python
  for i in range(5):
      print(i)  # 0,1,2,3,4

  meyveler = ["elma", "armut", "muz"]
  for idx, meyve in enumerate(meyveler, start=1):
      print(idx, meyve)

  isimler = ["Ali", "Ayşe"]
  yaslar = [25, 23]
  for isim, yas in zip(isimler, yaslar):
      print(isim, yas)
  ```

### sorted(), reversed()
- Koleksiyonları sıralama ve ters çevirme işlemlerinde kullanılır.
  ```python
  sayilar = [3, 1, 4]
  print(sorted(sayilar))            # [1, 3, 4]
  print(list(reversed(sayilar)))    # [4, 1, 3]
  ```

#### Alıştırma:
Birden fazla listeyi zip ile birleştirip, sıralanmış şekilde ekrana yazdıran bir fonksiyon yazın.

---

## 4. Matematiksel Fonksiyonlar

### abs(), min(), max(), sum(), round(), pow(), divmod()
- Sayısal işlemleri hızlı ve güvenli şekilde gerçekleştirir.
  ```python
  print(abs(-5))                  # 5
  print(min([3, 2, 1]))           # 1
  print(max([3, 2, 1]))           # 3
  print(sum([1, 2, 3]))           # 6
  print(round(3.14159, 2))        # 3.14
  print(pow(2, 3))                # 8
  print(divmod(17, 5))            # (3, 2)
  ```

#### Alıştırma:
Bir liste içindeki sayıların ortalamasını ve varyansını hesaplayan bir fonksiyon yazın.

---

## 5. Fonksiyonel Programlama Fonksiyonları

### map(), filter(), reduce(), any(), all()
- Fonksiyonları dizilere uygulayarak hızlı veri işleme imkanı sağlar.
  ```python
  sayilar = [1, 2, 3, 4, 5]
  kareler = list(map(lambda x: x**2, sayilar))              # [1, 4, 9, 16, 25]
  tekler = list(filter(lambda x: x % 2 == 1, sayilar))      # [1, 3, 5]
  from functools import reduce
  toplam = reduce(lambda a,b: a+b, sayilar)                 # 15
  print(any([True, False]))                                 # True
  print(all([True, True, False]))                           # False
  ```

#### Alıştırma:
Bir listede bulunan tüm sayıları çift mi diye kontrol eden bir fonksiyon yazın (all ile).

---

## 6. Nesne ve Dosya Fonksiyonları

### id(), dir(), getattr(), setattr(), hasattr()
- Nesne yönetimi ve dinamik işlemler için kullanılır.
  ```python
  x = []
  print(id(x))                 # Nesnenin kimliği
  print(dir(str))              # str nesnesinin öznitelikleri

  class Kedi:
      renk = "siyah"
  k = Kedi()
  print(getattr(k, "renk"))    # "siyah"
  setattr(k, "renk", "beyaz")
  print(k.renk)                # "beyaz"
  print(hasattr(k, "renk"))    # True
  ```

### open(), help()
- Dosya işlemleri ve yardım almak için kullanılır.
  ```python
  with open("dosya.txt", "w") as f:
      f.write("Merhaba")
  help(str)
  ```

#### Alıştırma:
Bir nesnenin özniteliklerini ekrana yazdıran bir fonksiyon yazın.

---

## 7. Diğer Faydalı Fonksiyonlar

### chr(), ord(), bin(), hex(), oct(), eval(), exec()
- Karakter/taban dönüşümleri ve dinamik kod çalıştırma.
  ```python
  print(chr(65))     # 'A'
  print(ord('A'))    # 65
  print(bin(10))     # '0b1010'
  print(hex(10))     # '0xa'
  print(oct(10))     # '0o12'

  kod = "print(5+7)"
  exec(kod)
  ```

#### Alıştırma:
Kullanıcıdan bir sayı alıp, farklı tabanlarda yazdıran bir fonksiyon yazın.

---

## 8. Soru-Cevap ve Uygulama

- Gömülü fonksiyonlarla ilgili örnekler
- Öğrencilerden gelen soruların cevaplanması
- Küçük bir Python projesinde gömülü fonksiyonları kullanmak

---

## 9. Kapanış ve Özet

- Gömülü fonksiyonların önemi ve avantajları tekrar vurgulanır
- Daha ileri seviye için kaynaklar ve öneriler
- [Python Built-in Functions – Resmi Dokümantasyon](https://docs.python.org/3/library/functions.html)

---

