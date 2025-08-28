# Python: Listeler, Demetler ve Liste Metotları – Ders İçeriği

## 1. Giriş

### 1.1 Python’da Veri Yapılarına Genel Bakış
- Python programlama dilinde verileri saklamak ve düzenlemek için çeşitli veri yapılarına ihtiyaç duyulur.
- En yaygın kullanılan veri yapıları: Liste (list), Demet (tuple), Sözlük (dict) ve Küme (set).
- Her veri yapısının kendine özgü avantajları, kullanım alanları ve özellikleri vardır.

### 1.2 Listeler ve Demetler Neden Önemli?
- **Listeler**: Değiştirilebilir, sıralı veri saklama sağlar; birden fazla veri tipini aynı anda tutabilir.
- **Demetler**: Sıralı ama değiştirilemezler; sabit veri veya anahtar olarak kullanmak için idealdir.
- Hem listeler hem de demetler, Python’da veri toplama, sınıflandırma, döngüyle işleme gibi temel işlemler için çok kullanılır.

### 1.3 Kullanım Alanları ve Avantajları
- Listeler: Öğrenci listesi, alışveriş listesi, veri analizi, sonuçlar gibi değişken veri kümeleri için uygundur.
- Demetler: Koordinatlar, sabit ayarlar, veri tabanında bir kaydın anahtarı gibi değişmemesi gereken veriler için kullanılır.
- Her ikisi de hızlı erişim, kolay indeksleme ve birden fazla işlemi destekler.
- Python’un liste metotları sayesinde listeler ile veri ekleme, silme, sıralama ve filtreleme işlemleri kolayca yapılabilir.

---

## 2. Listeler (List) – Tanım ve Temel İşlemler

### 2.1. Liste Oluşturma ve Eleman Ekleme
```python
meyveler = ["elma", "armut", "muz"]
bos_liste = []
karisik = [1, "merhaba", True, 3.14]
```

### 2.2. Liste Elemanlarına Erişim
```python
print(meyveler[0])      # "elma"
print(meyveler[-1])     # "muz"
print(meyveler[1:3])    # ["armut", "muz"]
```

### 2.3. Listeyi Döngüyle Gezmek
```python
for meyve in meyveler:
    print(meyve)
```

### 2.4. Listelerde Değişiklik Yapmak
```python
meyveler[1] = "kiraz"   # ["elma", "kiraz", "muz"]
meyveler.append("portakal")
meyveler.insert(1, "kivi")
```

#### Alıştırma:
Bir listedeki tüm sayıları çiftse "çift", tekse "tek" olarak ekrana yazdıran bir program yazın.

---

## 3. Demetler (Tuple) – Tanım ve Kullanım

### 3.1. Demet Oluşturma
```python
koordinat = (10, 20)
tekli_demet = (5,)  # Virgül zorunlu!
karisik = (1, "ahmet", False)
```

### 3.2. Demete Eleman Erişimi
```python
print(koordinat[0])  # 10
```

### 3.3. Demetlerin Özellikleri
- Değiştirilemez (immutable)
- Hızlı ve güvenli
- Sözlük anahtarı olarak kullanılabilir

### 3.4. Demeti Döngüyle Gezmek
```python
for eleman in karisik:
    print(eleman)
```

#### Alıştırma:
Bir demetin elemanlarını ekrana yazdıran bir fonksiyon yazın.

---

## 4. Liste Metotları – Ayrıntılı İnceleme

### 4.1. append(), insert(), extend()
```python
meyveler.append("çilek")
meyveler.insert(2, "üzüm")
meyveler.extend(["karpuz", "kavun"])
```

### 4.2. remove(), pop(), clear()
```python
meyveler.remove("elma")
meyveler.pop()           # sondaki eleman çıkarılır
meyveler.pop(0)          # belirli indeks çıkarılır
meyveler.clear()         # tüm elemanlar silinir
```

### 4.3. index(), count()
```python
meyveler = ["elma", "muz", "elma", "armut"]
print(meyveler.index("muz"))   # 1
print(meyveler.count("elma"))  # 2
```

### 4.4. sort(), reverse()
```python
sayilar = [5, 1, 7, 3]
sayilar.sort()                 # [1, 3, 5, 7]
sayilar.sort(reverse=True)     # [7, 5, 3, 1]
sayilar.reverse()              # [1, 3, 5, 7] -> [7, 5, 3, 1]
```

### 4.5. copy()
```python
yeni_liste = sayilar.copy()
```

### 4.6. List Comprehension (Liste Üreteci)
```python
kareler = [x**2 for x in range(10)]
```

#### Alıştırma:
Bir listedeki elemanları tersine çeviren, büyükten küçüğe sıralayan ve tekrar edenleri silen bir fonksiyon yazın.

---

## 5. Listeler ve Demetler Arası Dönüşüm

### 5.1. tuple() ve list() Fonksiyonları
```python
t = tuple(meyveler)
l = list(koordinat)
```

#### Alıştırma:
Kullanıcıdan alınan elemanlarla bir liste oluşturup, bunu demete çeviren bir program yazın.

---

## 6. Uygulama ve Proje

- Karmaşık bir veri seti: Sınıf listesi (isim, yaş, not)
- Listeler ve demetler ile temel analizler: En yüksek notu bulma, isimleri sıralama, yaş ortalaması
- Kısa uygulama: Sözlükler ile birlikte liste/demet kullanımı

---

## 7. Soru-Cevap ve Kapanış

- Sık yapılan hatalar ve ipuçları
- Gömülü fonksiyonlar ile liste/demet işlemleri
- Ek kaynaklar ve ileri okuma

---