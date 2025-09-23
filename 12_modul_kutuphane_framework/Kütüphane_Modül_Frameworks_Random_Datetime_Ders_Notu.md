# Kütüphane, Modül, Frameworks Kavramları, Random ve Datetime Kütüphanesi ile Uygulamalar

---

## 1. Giriş: Kütüphane, Modül, Framework Nedir?

### 1.1. Modül Nedir?
- Python’da bir dosya (`.py`) içindeki kodların bir bütün olarak kullanılabilmesi için modül olarak adlandırılır.
- Örnek:
    ```python
    # math.py (bir modül)
    def topla(a, b):
        return a + b
    ```

### 1.2. Kütüphane (Library) Nedir?
- Birden fazla modülün bir araya gelmesiyle oluşan, belirli bir amaca yönelik işlevleri barındıran yapılardır.
- Örnek: `math`, `random`, `datetime`, `os` gibi Python kütüphaneleri.

### 1.3. Framework Nedir?
- Belirli bir yazılım geliştirme sürecini kolaylaştıran, kapsamlı ve kuralları olan yapılardır.
- Kodun iskeletini oluşturur, geliştirici eksik parçaları ekler.
- Örnek: Django (web), Flask (web), Tensorflow (AI).

---

## 2. Random Kütüphanesi

### 2.1. Random Kütüphanesinin Temelleri
- Rastgele sayı üretmeyi sağlar.
- Dahili bir kütüphanedir, kuruluma gerek yoktur.
- Kütüphane kullanımı:
    ```python
    import random
    ```

### 2.2. Temel Fonksiyonlar ve Kullanımları

#### 2.2.1. random.random()
- 0.0 ile 1.0 arasında rastgele bir ondalık sayı üretir.
    ```python
    import random
    print(random.random()) # 0.0 <= x < 1.0
    ```

#### 2.2.2. random.randint(a, b)
- a ile b (her ikisi dahil) arasında bir tamsayı üretir.
    ```python
    print(random.randint(1, 10)) # 1 ile 10 arasında bir tam sayı
    ```

#### 2.2.3. random.uniform(a, b)
- a ile b arasında ondalıklı sayı üretir.
    ```python
    print(random.uniform(1, 5)) # 1.0 <= x < 5.0
    ```

#### 2.2.4. random.choice(seq)
- Bir liste, demet, string gibi sıralı veri tiplerinden rastgele bir eleman seçer.
    ```python
    meyveler = ["elma", "armut", "muz"]
    print(random.choice(meyveler))
    ```

#### 2.2.5. random.choices(seq, k=n)
- Sıralı yapıdan k adet rastgele seçim yapar (tekrar olabilir).
    ```python
    print(random.choices(meyveler, k=2))
    ```

#### 2.2.6. random.sample(seq, k=n)
- Sıralı yapıdan k adet benzersiz rastgele eleman seçer.
    ```python
    print(random.sample(meyveler, k=2))
    ```

#### 2.2.7. random.shuffle(seq)
- Bir listeyi yerinde rastgele karıştırır.
    ```python
    sayilar = [1, 2, 3, 4, 5]
    random.shuffle(sayilar)
    print(sayilar)
    ```

### 2.3. Uygulamalar ve Örnekler

#### 2.3.1. Zar Atma Simülasyonu
```python
for i in range(5):
    print("Zar sonucu:", random.randint(1, 6))
```

#### 2.3.2. Şifre Üretici
```python
karakterler = "abcdefghijklmnopqrstuvwxyz0123456789"
sifre = ""
for i in range(8):
    sifre += random.choice(karakterler)
print("Oluşturulan Şifre:", sifre)
```

#### 2.3.3. Öğrenci Listesinden Rastgele Kişi Seçimi
```python
ogrenciler = ["Ali", "Veli", "Ayşe", "Fatma"]
print("Bugün tahtaya çıkacak kişi:", random.choice(ogrenciler))
```

#### 2.3.4. Sınıfı Gruplara Ayırma
```python
ogrenciler = ["Ali", "Veli", "Ayşe", "Fatma", "Zeynep", "Mehmet"]
random.shuffle(ogrenciler)
grup1 = ogrenciler[:3]
grup2 = ogrenciler[3:]
print("Grup 1:", grup1)
print("Grup 2:", grup2)
```

---

## 3. Datetime Kütüphanesi

### 3.1. Datetime Kütüphanesinin Temelleri
- Tarih ve saat işlemleri için kullanılır.
- Dahili bir kütüphanedir.

    ```python
    import datetime
    ```

### 3.2. Temel Fonksiyonlar ve Kullanımları

#### 3.2.1. Şimdiki Tarih ve Saat
```python
simdi = datetime.datetime.now()
print("Şu an:", simdi)
```

#### 3.2.2. Sadece Tarih veya Saat
```python
tarih = datetime.date.today()
print("Bugünün tarihi:", tarih)

saat = datetime.datetime.now().time()
print("Şu anki saat:", saat)
```

#### 3.2.3. Belirli Bir Tarih ve Saat Oluşturma
```python
ozel_tarih = datetime.datetime(2025, 1, 1, 10, 0, 0)
print("Belirli tarih:", ozel_tarih)
```

#### 3.2.4. Tarih ve Saat Formatlama
```python
simdi = datetime.datetime.now()
print(simdi.strftime("%d/%m/%Y %H:%M:%S")) # 23/09/2025 14:30:45
```
- Sık kullanılan formatlar:
  - `%d` : gün
  - `%m` : ay
  - `%Y` : yıl
  - `%H` : saat (24 saat)
  - `%M` : dakika
  - `%S` : saniye

#### 3.2.5. Tarihler Arası Fark Hesaplama
```python
t1 = datetime.datetime(2025, 9, 1)
t2 = datetime.datetime(2025, 9, 23)
fark = t2 - t1
print("Gün farkı:", fark.days)
```

#### 3.2.6. Saat ve Dakika Ekleme/Çıkarma (timedelta)
```python
from datetime import timedelta

simdi = datetime.datetime.now()
yeni_zaman = simdi + timedelta(days=5)
print("5 gün sonrası:", yeni_zaman)
```

### 3.3. Uygulamalar ve Örnekler

#### 3.3.1. Doğum Tarihinden Yaş Hesaplama
```python
dogum_tarihi = datetime.datetime(2000, 4, 15)
bugun = datetime.datetime.now()
yas = bugun.year - dogum_tarihi.year
if (bugun.month, bugun.day) < (dogum_tarihi.month, dogum_tarihi.day):
    yas -= 1
print("Yaşınız:", yas)
```

#### 3.3.2. Basit Geri Sayım (Countdown)
```python
import time

hedef = datetime.datetime.now() + timedelta(seconds=10)
while datetime.datetime.now() < hedef:
    kalan = hedef - datetime.datetime.now()
    print("Kalan saniye:", kalan.seconds, end="\r")
    time.sleep(1)
print("Süre doldu!")
```

#### 3.3.3. Rastgele Tarih Üretimi
```python
def rastgele_tarih(baslangic, bitis):
    baslangic_zaman = baslangic.timestamp()
    bitis_zaman = bitis.timestamp()
    rastgele_zaman = random.uniform(baslangic_zaman, bitis_zaman)
    return datetime.datetime.fromtimestamp(rastgele_zaman)

baslangic = datetime.datetime(2020, 1, 1)
bitis = datetime.datetime(2025, 1, 1)
print("Rastgele tarih:", rastgele_tarih(baslangic, bitis))
```

---

## 4. Random ve Datetime ile Mini Proje: Çekiliş Programı

### 4.1. Çekilişe Katılanları ve Tarihleri Listeleme

```python
katilanlar = ["Ali", "Veli", "Ayşe", "Fatma", "Mehmet"]
cekilis_tarihi = datetime.datetime(2025, 10, 1, 20, 0, 0)

print("Çekilişe katılanlar:")
for kisi in katilanlar:
    print("-", kisi)
print("Çekiliş tarihi:", cekilis_tarihi.strftime("%d/%m/%Y %H:%M"))
```

### 4.2. Çekiliş Sonucunu Belirleme

```python
if datetime.datetime.now() >= cekilis_tarihi:
    kazanan = random.choice(katilanlar)
    print("Kazanan:", kazanan)
else:
    kalan = cekilis_tarihi - datetime.datetime.now()
    print("Çekilişe kalan süre:", kalan)
```

---

## 5. Ödev ve Alıştırmalar

1. 1-100 arasında rastgele 10 sayı üretip, bunların ortalamasını bulunuz.
2. Kullanıcıdan doğum tarihi alın, yaşını ekrana yazdırınız.
3. Bir listeyi rastgele karıştırıp ilk 3 elemanını ekrana yazdırınız.
4. Bir tarih girildiğinde, bugüne kaç gün kaldığını hesaplayan programı yazınız.
5. Rastgele 5 haneli bir şifre üreten program yazınız.

---

Bu ders notları ile hem temel kavramları hem de Random ve Datetime kütüphanelerini bol örnekle uygulamalı olarak öğrenmiş olacaksınız.