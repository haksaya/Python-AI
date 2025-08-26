# Python'da Gömülü Fonksiyonlar – Ders İçeriği

## 1. Giriş

- Python’da fonksiyon kavramı ve gömülü fonksiyonların tanımı
- Gömülü fonksiyonların avantajları
- [Resmi Python Built-in Functions Listesi](https://docs.python.org/3/library/functions.html)

---

## 2. Temel Gömülü Fonksiyonlar

### print(), input()
- **print():** Konsola veri yazdırmak için kullanılır.
  ```python
  print("Merhaba, Python!")
  ```
- **input():** Kullanıcıdan veri almak için kullanılır.
  ```python
  isim = input("Adınızı girin: ")
  print("Merhaba,", isim)
  ```

### type(), len(), str(), int(), float(), bool()
- **type():** Bir değişkenin tipini gösterir.
  ```python
  x = 5
  print(type(x))  # <class 'int'>
  ```
- **len():** Bir koleksiyonun eleman sayısını verir.
  ```python
  meyveler = ["elma", "armut", "kiraz"]
  print(len(meyveler))  # 3
  ```
- **str(), int(), float(), bool():** Tip dönüşümleri sağlar.
  ```python
  s = str(123)
  i = int("456")
  f = float("3.14")
  b = bool(0)  # False
  ```

### range(), enumerate()
- **range():** Belirtilen aralıkta sayılar üretir.
  ```python
  for i in range(5):
      print(i)
  ```
- **enumerate():** İndeksli döngü oluşturmada kullanılır.
  ```python
  for i, meyve in enumerate(meyveler):
      print(i, meyve)
  ```

#### Alıştırma:
Kullanıcıdan alınan sayıların ortalamasını hesaplayan bir program yazın.

---

## 3. Veri Yapısı Fonksiyonları

### list(), tuple(), dict(), set()
- **list():** Liste oluşturur.
  ```python
  l = list("abc")  # ['a', 'b', 'c']
  ```
- **tuple():** Demet oluşturur.
  ```python
  t = tuple([1,2,3])
  ```
- **dict():** Sözlük oluşturur.
  ```python
  d = dict(a=1, b=2)
  ```
- **set():** Küme oluşturur.
  ```python
  s = set([1,2,2,3])
  ```

### sorted(), reversed(), zip()
- **sorted():** Sıralama yapar.
  ```python
  sayilar = [3, 1, 4]
  print(sorted(sayilar))  # [1, 3, 4]
  ```
- **reversed():** Elemanları tersine çevirir.
  ```python
  print(list(reversed(sayilar)))
  ```
- **zip():** Birden fazla diziyi birleştirir.
  ```python
  isimler = ["Ali", "Ayşe"]
  yaslar = [25, 23]
  for isim, yas in zip(isimler, yaslar):
      print(isim, yas)
  ```

#### Alıştırma:
Birden fazla listeyi zip ile birleştirip, sıralanmış şekilde ekrana yazdıran bir fonksiyon yazın.

---

## 4. Matematiksel Fonksiyonlar

### abs(), min(), max(), sum(), pow(), round(), divmod()
- **abs():** Mutlak değer döndürür.
  ```python
  print(abs(-5))  # 5
  ```
- **min(), max():** En küçük/en büyük değeri döndürür.
  ```python
  print(min([3, 2, 1]))  # 1
  print(max([3, 2, 1]))  # 3
  ```
- **sum():** Toplamı döndürür.
  ```python
  print(sum([1, 2, 3]))  # 6
  ```
- **pow():** Üs alma işlemi.
  ```python
  print(pow(2, 3))  # 8
  ```
- **round():** Yuvarlama işlemi.
  ```python
  print(round(3.14159, 2))  # 3.14
  ```
- **divmod():** Bölüm ve kalanı tuple olarak döndürür.
  ```python
  print(divmod(17, 5))  # (3, 2)
  ```

#### Alıştırma:
Bir liste içindeki sayıların ortalamasını ve varyansını hesaplayan bir fonksiyon yazın.

---

## 5. Fonksiyonel Programlama Fonksiyonları

### map(), filter(), reduce(), any(), all()
- **map():** Fonksiyonu listedeki tüm elemanlara uygular.
  ```python
  sayilar = [1, 2, 3]
  kareler = list(map(lambda x: x**2, sayilar))
  ```
- **filter():** Şarta uyan elemanları seçer.
  ```python
  tekler = list(filter(lambda x: x % 2 == 1, sayilar))
  ```
- **reduce():** Birleştirerek tek değer elde eder.
  ```python
  from functools import reduce
  toplam = reduce(lambda a,b: a+b, sayilar)
  ```
- **any(), all():** Herhangi biri/Hepsi doğru mu?
  ```python
  print(any([True, False, False]))  # True
  print(all([True, True, False]))   # False
  ```

#### Alıştırma:
Bir listede bulunan tüm sayıları çift mi diye kontrol eden bir fonksiyon yazın (all ile).

---

## 6. Nesne ve Dosya Fonksiyonları

### isinstance(), id(), dir(), getattr(), setattr(), hasattr()
- **isinstance():** Tip kontrolü.
  ```python
  print(isinstance(5, int))  # True
  ```
- **id():** Nesne kimliği.
  ```python
  x = []
  print(id(x))
  ```
- **dir():** Öznitelik listesi.
  ```python
  print(dir(str))
  ```
- **getattr(), setattr(), hasattr():** Dinamik öznitelik işlemleri.
  ```python
  class Kedi:
      renk = "siyah"
  k = Kedi()
  print(getattr(k, "renk"))
  setattr(k, "renk", "beyaz")
  print(k.renk)
  print(hasattr(k, "renk"))  # True
  ```

### open(), help()
- **open():** Dosya açmak için kullanılır.
  ```python
  with open("dosya.txt", "w") as f:
      f.write("Merhaba")
  ```
- **help():** Yardım almak için kullanılır.
  ```python
  help(str)
  ```

#### Alıştırma:
Bir nesnenin özniteliklerini ekrana yazdıran bir fonksiyon yazın.

---

## 7. Diğer Faydalı Fonksiyonlar

### chr(), ord(), bin(), hex(), oct(), eval(), exec()
- **chr(), ord():** Karakter ve ASCII dönüşümü.
  ```python
  print(chr(65))  # 'A'
  print(ord('A')) # 65
  ```
- **bin(), hex(), oct():** Sayı taban dönüşümleri.
  ```python
  print(bin(10))  # '0b1010'
  print(hex(10))  # '0xa'
  print(oct(10))  # '0o12'
  ```
- **eval(), exec():** Dinamik kod çalıştırma (dikkatli kullanın!).
  ```python
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

- Gömülü fonksiyonların önemi
- Daha ileri seviye için kaynaklar
- [Resmi Python Documentation](https://docs.python.org/3/library/functions.html)

---
