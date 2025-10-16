# PYTHON İLE NESNE TABANLI PROGRAMLAMA (OOP) – Ders İçeriği

Bu dersle, Python ile Nesne Tabanlı Programlama (OOP) kavramlarının temellerini açıklamalar ve bol örneklerle öğreneceksiniz.

---

## 1. Nesne Tabanlı Programlama (OOP) Nedir?

- OOP: Programları nesneler ve bu nesnelerin etkileşimleri üzerinden tasarlama yöntemidir.
- Nesne (Object): Veri (özellik/alan) ve bu veriler üzerinde işlem yapan fonksiyonları (metot) bir arada tutan yapı.
- Sınıf (Class): Nesne oluşturmak için bir şablondur.
- OOP'nin ana kavramları: Sınıf, Nesne, Miras (Inheritance), Kapsülleme (Encapsulation), Polimorfizm (Çok Biçimlilik).

**Gündelik Hayattan OOP Örneği:**
- Araba bir sınıftır. Tek tek arabalar ise nesnelerdir. Her arabanın rengi, markası (özellik), çalıştırma gibi fonksiyonları (metot) vardır.

---

## 2. Neden OOP’ye İhtiyaç Duyulur?

- Büyük ve karmaşık projelerde kodun düzenli, sürdürülebilir ve tekrar kullanılabilir olması istenir.
- OOP ile:
  - Kod tekrarını azaltırız.
  - Modülerlik ve ölçeklenebilirlik sağlanır.
  - Gerçek hayattaki kavram ve ilişkiler yazılıma daha doğal aktarılır.

**Küçük Örnek:**
```python
# Fonksiyonel yaklaşımda:
araba1_marka = "Toyota"
araba1_renk = "Kırmızı"
araba2_marka = "Ford"
araba2_renk = "Mavi"
# OOP ile:
class Araba:
    pass
```
---

## 3. Sınıf ve Nesneler

### Sınıf Oluşturma

```python
class Araba:
    pass  # Şimdilik boş, sonra dolduracağız
```

### Nesne Oluşturma

```python
araba1 = Araba()
araba2 = Araba()
print(type(araba1))  # <class '__main__.Araba'>
```

### Özellik (Attribute) Tanımlama

```python
class Araba:
    renk = "Kırmızı"

araba1 = Araba()
araba2 = Araba()
araba2.renk = "Mavi"
print(araba1.renk)  # Kırmızı
print(araba2.renk)  # Mavi
```

### Nesne Özellikleri ve Sınıf Özellikleri

```python
class Araba:
    tip = "Otomobil"  # Sınıf özelliği

    def __init__(self, marka, renk):
        self.marka = marka    # Nesne özelliği
        self.renk = renk

araba1 = Araba("Renault", "Beyaz")
print(araba1.marka, araba1.renk, araba1.tip)  # Renault Beyaz Otomobil
```

**Alıştırma:**  
Kendi `Ogrenci` sınıfınızı oluşturun, isim ve numara özellikleri ile iki nesne üretin.

---

## 4. Metot Oluşturma

### Metot Nedir?

- Sınıf içinde tanımlanan fonksiyonlardır.
- İlk parametreleri genellikle `self` olur.

```python
class Araba:
    def calistir(self):
        print("Araba çalıştı.")

araba = Araba()
araba.calistir()
```

### Özelliklere Metot İçinden Erişim

```python
class Araba:
    def __init__(self, marka, renk):
        self.marka = marka
        self.renk = renk
    
    def bilgi_goster(self):
        print(f"{self.marka} {self.renk} bir arabadır.")

araba = Araba("Opel", "Siyah")
araba.bilgi_goster()  # Opel Siyah bir arabadır.
```

**Alıştırma:**  
Bir `Kare` sınıfı yazın, kenar uzunluğu parametre olsun ve alanını döndüren bir metot ekleyin.

---

## 5. Yapıcı Metotlar (Constructor)

- Python’da `__init__` özel metot ile nesne ilk oluşurken başlangıç değerleri atanır.

```python
class Kisi:
    def __init__(self, isim, yas):
        self.isim = isim
        self.yas = yas

kisi1 = Kisi("Ayşe", 25)
print(kisi1.isim, kisi1.yas)
```

### Varsayılan Parametreler

```python
class Calisan:
    def __init__(self, isim, maas=5000):
        self.isim = isim
        self.maas = maas

c1 = Calisan("Ali")
c2 = Calisan("Zeynep", 7000)
print(c1.isim, c1.maas)
print(c2.isim, c2.maas)
```

**Alıştırma:**  
Bir `Urun` sınıfı yazın, adı ve fiyatı parametre olarak alsın. Nesne oluşturulunca bu değerleri ekrana yazdıran bir metot olsun.

---

## 6. Miras Alma (Inheritance)

- Bir sınıf başka bir sınıfın özelliklerini ve metotlarını devralabilir.
- Kod tekrarını azaltır, genişletilebilirlik sağlar.

```python
class Hayvan:
    def ses_cikar(self):
        print("Hayvan bir ses çıkardı.")

class Kedi(Hayvan):
    def ses_cikar(self):
        print("Miyav!")

class Kopek(Hayvan):
    def ses_cikar(self):
        print("Hav hav!")

kedi = Kedi()
kopek = Kopek()
kedi.ses_cikar()   # Miyav!
kopek.ses_cikar()  # Hav hav!
```

### Miras Alırken Üst Sınıfın Metotlarını Kullanmak

```python
class Calisan:
    def __init__(self, isim):
        self.isim = isim

    def bilgileri_goster(self):
        print(f"Adı: {self.isim}")

class Yonetici(Calisan):
    def __init__(self, isim, departman):
        super().__init__(isim)  # Üst sınıfın __init__’ini çağırır
        self.departman = departman

    def bilgileri_goster(self):
        super().bilgileri_goster()
        print(f"Departman: {self.departman}")

y = Yonetici("Fatma", "Pazarlama")
y.bilgileri_goster()
```

**Alıştırma:**  
Bir `Arac` sınıfından `Bisiklet` ve `Motor` sınıflarını türetin. Her biri kendine özgü bir metot içersin.

---

## 7. Kapsülleme (Encapsulation)

- Nesne verilerini dışarıdan koruma, doğrudan erişimi engelleme.
- Python’da değişken başına `_` (korumalı) veya `__` (özel/gizli) ekleyerek yapılır.

```python
class BankaHesabi:
    def __init__(self, isim, bakiye):
        self.isim = isim
        self.__bakiye = bakiye  # Gizli (private) değişken

    def bakiye_goster(self):
        print(f"{self.isim} bakiyesi: {self.__bakiye} TL")

    def para_yatir(self, miktar):
        if miktar > 0:
            self.__bakiye += miktar

    def para_cek(self, miktar):
        if 0 < miktar <= self.__bakiye:
            self.__bakiye -= miktar

hesap = BankaHesabi("Ali", 1000)
hesap.bakiye_goster()
hesap.para_yatir(500)
hesap.para_cek(300)
hesap.bakiye_goster()
# print(hesap.__bakiye)  # AttributeError!
```

### Getter ve Setter Metotları

```python
class Kisi:
    def __init__(self, isim):
        self.__isim = isim

    def get_isim(self):
        return self.__isim

    def set_isim(self, yeni_isim):
        if isinstance(yeni_isim, str):
            self.__isim = yeni_isim

kisi = Kisi("Zeynep")
print(kisi.get_isim())
kisi.set_isim("Ayşe")
print(kisi.get_isim())
```

**Alıştırma:**  
Bir `Ogrenci` sınıfı yazın; not bilgisini gizli yapın ve not bilgisini sadece getter ile gösterin.

---

## 8. Kapanış ve Ekstra

### Polimorfizm (Kısa Bilgi)

- Aynı isimli metotların farklı sınıflarda farklı işler yapabilmesidir.

```python
class Hayvan:
    def ses_cikar(self):
        print("Ses yok")

class Kedi(Hayvan):
    def ses_cikar(self):
        print("Miyav")

class Kopek(Hayvan):
    def ses_cikar(self):
        print("Hav hav")

hayvanlar = [Kedi(), Kopek(), Hayvan()]
for h in hayvanlar:
    h.ses_cikar()
```

### Alıştırmalar ve Mini Proje Önerisi

- Kendi basit öğrenci, çalışan, banka hesabı, araç gibi OOP örneklerinizi yazın.
- Mini Proje: Bir kitaplık yönetimi sınıfı yazın. Kitap ekle, sil, listele gibi metotlar içersin. Kitaplar nesne olarak tutulmalı.

### Kaynaklar ve İleri Okuma

- Python OOP resmi dökümantasyon: https://docs.python.org/3/tutorial/classes.html
- Python OOP örnek projeler, SOLID prensipleri, design patterns.

---

**Not:** Her bölümde bol örnek ve mini uygulama önerileriyle kendi başınıza pratik yapmanız teşvik edilir.