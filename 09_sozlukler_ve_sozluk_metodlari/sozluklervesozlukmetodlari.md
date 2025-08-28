# Python'da Sözlükler ve Sözlük Metotları – Ders İçeriği

## 1. Giriş

### 1.1 Sözlük nedir? Neden kullanılır?
- **Sözlük (dictionary)**, Python’da veriyi anahtar–değer (key-value) çiftleriyle saklayan bir veri yapısıdır.
- Listenin aksine, elemanlara indeksle değil, anahtar ile erişilir.
- Sözlükler, hızlı veri erişimi ve organize veri saklama için kullanılır. Bir kişinin bilgileri, ürün katalogları, ayarlar gibi birçok yerde tercih edilir.

### 1.2 Anahtar–değer (key-value) kavramı
- Sözlüklerde her eleman bir anahtar ve ona karşılık gelen bir değerden oluşur.
- Anahtarlar benzersiz (unique) ve değiştirilemez (immutable) olmalıdır. Genellikle string, sayı veya tuple tipindedir.
- Değerler her türlü veri tipi olabilir; sayı, string, liste, hatta başka bir sözlük.

### 1.3 Sözlüklerin avantajları ve kullanım alanları
- **Avantajları:**
    - Hızlı arama ve güncelleme (hash tabanlı erişim)
    - Esnek veri tipi desteği
    - Dinamik olarak büyüyebilir
    - Anahtarlar aracılığıyla anlamlı veri erişimi
- **Kullanım alanları:**
    - Veritabanı kayıtları, JSON veri yapıları
    - Konfigürasyon ve ayar dosyaları
    - Sözlükler, anahtar ile hızlı veri arama gerektiren tüm uygulamalarda kullanılır

---

## 2. Sözlük Oluşturma ve Temel İşlemler

### 2.1. Sözlük Oluşturma
```python
bos_sozluk = {}
ogrenci = {"ad": "Ali", "yas": 21, "okul": "YTÜ"}
notlar = dict(math=90, fizik=85)
```

### 2.2. Elemanlara Erişim
```python
print(ogrenci["ad"])
print(ogrenci.get("yas"))
```

### 2.3. Eleman Ekleme ve Güncelleme
```python
ogrenci["sinif"] = 3
ogrenci["yas"] = 22
```

### 2.4. Eleman Silme
```python
del ogrenci["okul"]
yas = ogrenci.pop("yas")
```

#### Alıştırma:
Kullanıcıdan alınan anahtar–değer ikilileriyle bir sözlük oluşturup, anahtar ile arama yapan bir program yazın.

---

## 3. Sözlüklerde Döngü ve Arama

### 3.1. Anahtar, Değer ve Elemanlar
```python
print(ogrenci.keys())     # dict_keys(['ad', 'sinif'])
print(ogrenci.values())   # dict_values(['Ali', 3])
print(ogrenci.items())    # dict_items([('ad', 'Ali'), ('sinif', 3)])
```

### 3.2. Sözlükte Döngü
```python
for anahtar in ogrenci:
    print(anahtar, ogrenci[anahtar])

for anahtar, deger in ogrenci.items():
    print(f"{anahtar}: {deger}")
```

### 3.3. Anahtar Kontrolü
```python
print("ad" in ogrenci)       # True
print("soyad" not in ogrenci) # True
```

#### Alıştırma:
Bir sözlükte sadece belirli anahtarlara sahip değerleri ekrana yazdıran fonksiyon yazın.

---

## 4. Sözlük Metotları

### 4.1. get(), setdefault()
```python
# get(): Anahtar yoksa None veya varsayılan döner
print(ogrenci.get("soyad", "Bilinmiyor"))

# setdefault(): Anahtar yoksa ekler, varsa mevcut değeri döner
ogrenci.setdefault("soyad", "Yılmaz")
```

### 4.2. update()
```python
ekstra = {"şehir": "İstanbul", "burslu": True}
ogrenci.update(ekstra)
```

### 4.3. pop(), popitem()
```python
yas = ogrenci.pop("yas", None)
anahtar, deger = ogrenci.popitem()  # Son eklenen anahtarı siler
```

### 4.4. clear(), copy()
```python
kopya = ogrenci.copy()
ogrenci.clear()  # Tüm elemanları siler
```

#### Alıştırma:
Bir sözlüğün kopyasını oluşturup, kopyada bir değer değiştirip orijinal sözlüğün değişmediğini gösteren bir program yazın.

---

## 5. Sözlüklerde İleri Düzey Kullanım

### 5.1. Sözlükle List, Tuple ve Set Kullanımı
```python
# Anahtarlar tuple olabilir
koordinatlar = {(0,0): "başlangıç", (1,1): "hedef"}

# Değerler liste veya başka sözlük olabilir
siniflar = {"9A": ["Ali", "Ayşe"], "9B": ["Veli", "Can"]}
```

### 5.2. Sözlükten Listeye Dönüştürme
```python
anahtarlar = list(ogrenci.keys())
degerler = list(ogrenci.values())
```

### 5.3. Sözlükle List Comprehension
```python
meyveler = ["elma", "armut", "kiraz"]
fiyatlar = [5, 7, 10]
sozluk = {meyve: fiyat for meyve, fiyat in zip(meyveler, fiyatlar)}
```

#### Alıştırma:
Bir listenin elemanlarını anahtar, eleman uzunluğunu değer olarak içeren bir sözlük oluşturan fonksiyon yazın.

---

## 6. Sözlüklerde Hatalar ve İpuçları

- Sözlükte olmayan anahtara erişim hatası (`KeyError`)
- get() ile güvenli erişim
- Anahtarların değiştirilemez (immutable) tipler olması gerektiği
- Sözlüklerin sıralı olmadığını (Python 3.7 ve sonrası eklenme sırası korunur)
- Büyük veri kümelerinde sözlük performansı

#### Alıştırma:
Sözlükte olmayan bir anahtara erişim hatasını try/except ile yöneten bir örnek yazın.

---

## 7. Uygulama ve Mini Proje

- Öğrenci not sözlükleri ile ortalama ve en yüksek notu bulma
- Metin içindeki kelimelerin sıklığını sayan fonksiyon
- Sözlükleri kullanarak basit adres defteri uygulaması

---

## 8. Soru-Cevap ve Kapanış

- Sık yapılan hatalar ve ipuçları
- Sözlük metotları ile ilgili ileri uygulama örnekleri
- Ek kaynaklar ve ileri okuma

---
