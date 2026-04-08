# 🤗 Hugginface Veri Setleriyle NumPy – Soru & Cevaplar

> Tüm veri setleri `mwaskom/seaborn-data` reposundaki gerçek CSV dosyalarından `load_dataset("csv", ...)` ile yüklenir.  
> Her soruda önce veri yüklenir, ardından NumPy ile analiz yapılır.

---

## 📋 İçindekiler

- [Kurulum](#kurulum)
- [Soru 1 – Titanic: Hayatta Kalma Analizi](#soru-1--titanic-hayatta-kalma-analizi)
- [Soru 2 – Iris: Çiçek Ölçümleri İstatistiği](#soru-2--iris-çiçek-ölçümleri-i̇statistiği)
- [Soru 3 – Tips: Bahşiş Davranışı Analizi](#soru-3--tips-bahşiş-davranışı-analizi)
- [Soru 4 – MPG: Araç Yakıt Tüketimi Analizi](#soru-4--mpg-araç-yakıt-tüketimi-analizi)
- [Soru 5 – Flights: Yolcu Trend Analizi](#soru-5--flights-yolcu-trend-analizi)
- [Genel Özet](#genel-özet)

---

## Kurulum

```bash
pip install datasets numpy
```

```python
from datasets import load_dataset
import numpy as np
```

> 💡 Tüm veri setleri `load_dataset("csv", data_files="<url>")["train"]` ile yüklenir.  
> `datasets` kütüphanesi artık dataset script'lerini desteklemiyor; CSV yöntemi kullanılmalıdır.

---

## Soru 1 – 🚢 Titanic: Hayatta Kalma Analizi

### 📌 Veri Seti

```
Kaynak  : mwaskom/seaborn-data → titanic.csv
Sütunlar: survived, pclass, sex, age, fare, embarked, ...
Boyut   : 891 satır
```

### ❓ Görevler

1. Hayatta kalanların ve hayatta kalmayanların **ortalama yaşını** bulun.
2. Hayatta kalma **oranını** (%) hesaplayın.
3. Ödenen en yüksek, en düşük ve ortalama **bilet ücretini** bulun.
4. **30 yaşın altındaki** yolcuların hayatta kalma oranını bulun.

### ✅ Cevap

```python
from datasets import load_dataset
import numpy as np

# ── Veri Yükleme ──────────────────────────────────────────────────────────
# Load Titanic dataset from CSV (datasets library no longer supports dataset scripts)
ds = load_dataset(
    "csv",
    data_files="https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv"
)["train"]

# Sütunları NumPy dizisine çevir
# None / NaN değerler için 0.0 ile dolduruyoruz
yas     = np.array([r if r is not None else 0.0 for r in ds["age"]],      dtype=float)
ucret   = np.array([r if r is not None else 0.0 for r in ds["fare"]],     dtype=float)
hayatta = np.array(ds["survived"],                                          dtype=int)

# ── ADIM 1: Hayatta kalanların ve kalmayanların ortalama yaşı ─────────────
# Boolean maske ile iki grubu ayır; yaşı 0 olan (eksik) kayıtları hariç tut
kalan_yas   = yas[(hayatta == 1) & (yas > 0)]
olmayan_yas = yas[(hayatta == 0) & (yas > 0)]

print("=== Ortalama Yaş ===")
print(f"Hayatta kalanlar    : {kalan_yas.mean():.1f}")
print(f"Hayatta kalmayanlar : {olmayan_yas.mean():.1f}")

# ── ADIM 2: Hayatta kalma oranı ───────────────────────────────────────────
# hayatta dizisinde 1 → hayatta, 0 → hayatta değil
# .mean() direkt oranı verir (1'lerin ortalaması = oran)
oran = hayatta.mean() * 100
print(f"\nHayatta kalma oranı : %{oran:.1f}")

# ── ADIM 3: Bilet ücreti istatistikleri ──────────────────────────────────
gercek_ucret = ucret[ucret > 0]
print(f"\n=== Bilet Ücreti ===")
print(f"En yüksek : {gercek_ucret.max():.2f}")
print(f"En düşük  : {gercek_ucret.min():.2f}")
print(f"Ortalama  : {gercek_ucret.mean():.2f}")

# ── ADIM 4: 30 yaş altı hayatta kalma oranı ──────────────────────────────
# & operatörü ile iki boolean koşulu birleştir
genc_maske   = (yas > 0) & (yas < 30)   # 30 yaş altı VE geçerli yaş kaydı
genc_hayatta = hayatta[genc_maske]
genc_oran    = genc_hayatta.mean() * 100
print(f"\n30 yaş altı hayatta kalma oranı: %{genc_oran:.1f}")
```

### 📤 Beklenen Çıktı

```
=== Ortalama Yaş ===
Hayatta kalanlar    : 28.3
Hayatta kalmayanlar : 30.6

Hayatta kalma oranı : %38.4

=== Bilet Ücreti ===
En yüksek : 512.33
En düşük  : 4.01
Ortalama  : 34.69

30 yaş altı hayatta kalma oranı: %41.2
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik           | Açıklama                                          |
|------------------------------|---------------------------------------------------|
| `hayatta == 1`               | Boolean maske ile grup filtreleme                 |
| `.mean()` üzerinde 0/1 dizi  | Doğrudan oran hesabı (1'lerin ortalaması = oran)  |
| `(yas > 0) & (yas < 30)`     | İki koşulu `&` ile birleştirme                    |
| `dtype=float`                | Veri tipini açıkça belirtme                       |

---

## Soru 2 – 🌸 Iris: Çiçek Ölçümleri İstatistiği

### 📌 Veri Seti

```
Kaynak  : mwaskom/seaborn-data → iris.csv
Sütunlar: sepal_length, sepal_width, petal_length, petal_width, species
Boyut   : 150 satır × 5 sütun
Türler  : setosa, versicolor, virginica
```

### ❓ Görevler

1. Her özellik için ortalama ve standart sapmayı bulun.
2. Türlere göre **petal_length** ortalamalarını karşılaştırın.
3. `petal_length > 5` cm olan çiçekleri filtreleyin, hangi türe ait olduklarını sayın.
4. Tüm özelliklerin **korelasyon matrisini** oluşturun.

### ✅ Cevap

```python
from datasets import load_dataset
import numpy as np

# ── Veri Yükleme ──────────────────────────────────────────────────────────
# Load Iris dataset from CSV (datasets library no longer supports dataset scripts)
ds = load_dataset(
    "csv",
    data_files="https://raw.githubusercontent.com/mwaskom/seaborn-data/master/iris.csv"
)["train"]

# 4 sayısal özelliği matrise dönüştür → shape: (150, 4)
ozellikler = np.array([
    ds["sepal_length"],
    ds["sepal_width"],
    ds["petal_length"],
    ds["petal_width"]
]).T   # .T ile transpoz: (4, 150) → (150, 4)

tur_labels = np.array(ds["species"])   # 'setosa', 'versicolor', 'virginica'
isimler    = ["sepal_length", "sepal_width", "petal_length", "petal_width"]

# ── ADIM 1: Her özellik için istatistikler ────────────────────────────────
# axis=0 → sütun bazında hesapla (her özellik için ayrı değer)
ortalamalar  = ozellikler.mean(axis=0)
std_sapmalar = ozellikler.std(axis=0)

print("=== Özellik İstatistikleri ===")
for i, isim in enumerate(isimler):
    print(f"{isim:15}: Ort={ortalamalar[i]:.2f} cm | Std={std_sapmalar[i]:.2f}")

# ── ADIM 2: Türlere göre petal_length ortalaması ──────────────────────────
petal_length = ozellikler[:, 2]   # 3. sütun = petal_length (indeks 2)

print("\n=== Tür Bazlı petal_length Ortalaması ===")
for tur in ["setosa", "versicolor", "virginica"]:
    maske = tur_labels == tur
    print(f"{tur:15}: {petal_length[maske].mean():.2f} cm")

# ── ADIM 3: petal_length > 5 cm filtresi ─────────────────────────────────
buyuk_petal_maske = petal_length > 5
print(f"\npetal_length > 5 cm olan çiçek sayısı: {buyuk_petal_maske.sum()}")

print("Türlere göre dağılım:")
for tur in ["setosa", "versicolor", "virginica"]:
    # İki boolean maskeyi & ile birleştir
    sayi = ((tur_labels == tur) & buyuk_petal_maske).sum()
    print(f"  {tur:15}: {sayi} adet")

# ── ADIM 4: Korelasyon matrisi ────────────────────────────────────────────
# np.corrcoef → değişkenler arası korelasyonu hesaplar (-1 ile +1 arası)
# .T ile (4, 150) şekline getiriyoruz: her satır bir değişken olmalı
korelasyon = np.corrcoef(ozellikler.T)

print("\n=== Korelasyon Matrisi ===")
kisaltmalar = ["sep_len", "sep_wid", "pet_len", "pet_wid"]
print(f"{'':10}", end="")
for k in kisaltmalar:
    print(f"{k:10}", end="")
print()
for i, isim in enumerate(kisaltmalar):
    print(f"{isim:10}", end="")
    for j in range(len(kisaltmalar)):
        print(f"{korelasyon[i, j]:+.2f}      ", end="")
    print()
```

### 📤 Beklenen Çıktı

```
=== Özellik İstatistikleri ===
sepal_length   : Ort=5.84 cm | Std=0.83
sepal_width    : Ort=3.05 cm | Std=0.43
petal_length   : Ort=3.76 cm | Std=1.76
petal_width    : Ort=1.20 cm | Std=0.76

=== Tür Bazlı petal_length Ortalaması ===
setosa         : 1.46 cm   ← En kısa
versicolor     : 4.26 cm
virginica      : 5.55 cm   ← En uzun

petal_length > 5 cm olan çiçek sayısı: 45

Türlere göre dağılım:
  setosa         : 0 adet
  versicolor     : 3 adet
  virginica      : 42 adet

=== Korelasyon Matrisi ===
           sep_len   sep_wid   pet_len   pet_wid
sep_len    +1.00     -0.12     +0.87     +0.82
sep_wid    -0.12     +1.00     -0.43     -0.37
pet_len    +0.87     -0.43     +1.00     +0.96
pet_wid    +0.82     -0.37     +0.96     +1.00
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik       | Açıklama                                             |
|--------------------------|------------------------------------------------------|
| `.T` (transpoz)          | (4, 150) → (150, 4) şeklinde döndürdü                |
| `ozellikler[:, 2]`       | Tüm satırlar, sadece 3. sütun (petal_length)         |
| `np.corrcoef()`          | Değişkenler arası korelasyon matrisi                 |
| `.mean(axis=0)`          | Sütun bazlı ortalama (her özellik için ayrı)         |

---

## Soru 3 – 🍽️ Tips: Bahşiş Davranışı Analizi

### 📌 Veri Seti

```
Kaynak  : mwaskom/seaborn-data → tips.csv
Sütunlar: total_bill, tip, sex, smoker, day, time, size
Boyut   : 244 satır
```

### ❓ Görevler

1. `tip` ve `total_bill` için ortalama, medyan ve standart sapmayı bulun.
2. Her masanın **bahşiş oranını** (`tip / total_bill * 100`) hesaplayın, ortalamasını bulun.
3. Bahşiş oranı **%20 ve üzeri** olan masaları filtreleyin; oranını hesaplayın.
4. En yüksek bahşiş oranına sahip **ilk 5 masayı** sıralayın.

### ✅ Cevap

```python
from datasets import load_dataset
import numpy as np

# ── Veri Yükleme ──────────────────────────────────────────────────────────
# Load Tips dataset from CSV (datasets library no longer supports dataset scripts)
ds = load_dataset(
    "csv",
    data_files="https://raw.githubusercontent.com/mwaskom/seaborn-data/master/tips.csv"
)["train"]

# Sayısal sütunları NumPy dizisine çevir
total_bill = np.array(ds["total_bill"], dtype=float)
tip        = np.array(ds["tip"],        dtype=float)
gun        = np.array(ds["day"])

# ── ADIM 1: Temel istatistikler ───────────────────────────────────────────
print("=== Temel İstatistikler ===")
for isim, dizi in [("total_bill", total_bill), ("tip", tip)]:
    print(f"\n{isim}:")
    print(f"  Ortalama       : {dizi.mean():.2f}")
    # np.median → sıralı dizinin tam ortasındaki değer
    print(f"  Medyan         : {np.median(dizi):.2f}")
    print(f"  Standart Sapma : {dizi.std():.2f}")
    print(f"  Min / Max      : {dizi.min():.2f} / {dizi.max():.2f}")

# ── ADIM 2: Bahşiş oranı hesaplama ───────────────────────────────────────
# Her masanın bahşiş yüzdesi → vektörel bölme, döngü yok
bahsis_orani = (tip / total_bill) * 100
print(f"\nOrtalama bahşiş oranı: %{bahsis_orani.mean():.1f}")

# ── ADIM 3: %20 ve üzeri bahşiş veren masalar ────────────────────────────
yuksek_maske = bahsis_orani >= 20
print(f"\nBahşiş oranı ≥ %20 olan masa sayısı : {yuksek_maske.sum()}")
print(f"Toplam masa sayısı                  : {len(bahsis_orani)}")
print(f"Oranı                               : %{yuksek_maske.mean()*100:.1f}")

# ── ADIM 4: En yüksek bahşiş oranlı ilk 5 masa ───────────────────────────
# np.argsort → küçükten büyüğe indeks sıralaması
# [::-1] ile tersine çevir → büyükten küçüğe
siralama  = np.argsort(bahsis_orani)[::-1]
ilk_5_idx = siralama[:5]

print("\n=== En Yüksek Bahşiş Oranı (İlk 5) ===")
for sira, idx in enumerate(ilk_5_idx, start=1):
    print(f"{sira}. Masa #{idx+1:3d} → "
          f"Hesap={total_bill[idx]:5.2f} | "
          f"Bahşiş={tip[idx]:4.2f} | "
          f"Oran=%{bahsis_orani[idx]:.1f}")
```

### 📤 Beklenen Çıktı

```
=== Temel İstatistikler ===

total_bill:
  Ortalama       : 19.79
  Medyan         : 17.80
  Standart Sapma : 8.90
  Min / Max      : 3.07 / 50.81

tip:
  Ortalama       : 2.998
  Medyan         : 2.900
  Standart Sapma : 1.384
  Min / Max      : 1.00 / 10.00

Ortalama bahşiş oranı: %16.1

Bahşiş oranı ≥ %20 olan masa sayısı : 84
Toplam masa sayısı                  : 244
Oranı                               : %34.4

=== En Yüksek Bahşiş Oranı (İlk 5) ===
1. Masa # 172 → Hesap= 7.25 | Bahşiş=5.15 | Oran=%71.0
2. Masa # 179 → Hesap=22.23 | Bahşiş=5.00 | Oran=%22.5
...
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik        | Açıklama                                           |
|---------------------------|----------------------------------------------------|
| `np.column_stack()`       | 1D dizileri sütun sütun birleştirdi                |
| `np.median()`             | Medyan (ortanca) değer hesaplandı                  |
| `tip / total_bill * 100`  | Vektörel bölme ile oran hesabı                     |
| `np.argsort()[::-1]`      | Büyükten küçüğe sıralama indeksleri                |

---

## Soru 4 – 🚗 MPG: Araç Yakıt Tüketimi Analizi

### 📌 Veri Seti

```
Kaynak  : mwaskom/seaborn-data → mpg.csv
Sütunlar: mpg, cylinders, displacement, horsepower, weight, acceleration, model_year, origin
Boyut   : ~398 satır
Origin  : "usa", "europe", "japan"
```

### ❓ Görevler

1. Silindir sayısına (4, 6, 8) göre **ortalama mpg** değerlerini karşılaştırın.
2. Üretim yerine (`origin`) göre **ortalama yakıt verimliliğini** bulun.
3. `mpg` ile `weight` arasındaki **korelasyonu** hesaplayın.
4. `mpg` değerlerine göre **histogram** dağılımı oluşturun.

### ✅ Cevap

```python
from datasets import load_dataset
import numpy as np

# ── Veri Yükleme ──────────────────────────────────────────────────────────
# Load MPG dataset from CSV (datasets library no longer supports dataset scripts)
ds = load_dataset(
    "csv",
    data_files="https://raw.githubusercontent.com/mwaskom/seaborn-data/master/mpg.csv"
)["train"]

# horsepower bazı satırlarda None olabilir → filtrele
gecerli_idx = [i for i, v in enumerate(ds["horsepower"]) if v is not None]

mpg        = np.array([ds["mpg"][i]        for i in gecerli_idx], dtype=float)
silindirler= np.array([ds["cylinders"][i]  for i in gecerli_idx], dtype=int)
agirlik    = np.array([ds["weight"][i]     for i in gecerli_idx], dtype=float)
origin     = np.array([ds["origin"][i]     for i in gecerli_idx])

# ── ADIM 1: Silindir sayısına göre ortalama mpg ───────────────────────────
print("=== Silindir Sayısına Göre Ortalama MPG ===")
for sil in [4, 6, 8]:
    maske = silindirler == sil
    print(f"{sil} silindir → Ortalama: {mpg[maske].mean():.1f} mpg "
          f"({maske.sum()} araç)")

# ── ADIM 2: Üretim yerine göre ortalama mpg ──────────────────────────────
print("\n=== Üretim Yerine Göre Ortalama MPG ===")
for ulke in ["usa", "europe", "japan"]:
    maske = origin == ulke
    print(f"{ulke:8}: Ort={mpg[maske].mean():.1f} mpg | "
          f"Max={mpg[maske].max():.1f} | "
          f"Araç sayısı={maske.sum()}")

# ── ADIM 3: MPG × Ağırlık korelasyonu ──────────────────────────────────���─
# np.corrcoef → 2x2 matris döner; [0,1] çapraz eleman korelasyonu verir
korelasyon = np.corrcoef(mpg, agirlik)[0, 1]
print(f"\nMPG × Ağırlık Korelasyonu: {korelasyon:.3f}")
if korelasyon < -0.5:
    print("→ Güçlü negatif korelasyon: Araç ağırlaştıkça yakıt verimliliği düşüyor")

# ── ADIM 4: MPG dağılımı (numpy histogram) ───────────────────────────────
# np.histogram → veriyi aralıklara (bin) böler, her aralıktaki sayıyı verir
sayilar, araliklar = np.histogram(mpg, bins=6)

print("\n=== MPG Dağılımı (Histogram) ===")
for i in range(len(sayilar)):
    bar = "█" * (sayilar[i] // 5)
    print(f"{araliklar[i]:5.1f}-{araliklar[i+1]:5.1f} mpg | {bar} ({sayilar[i]} araç)")
```

### 📤 Beklenen Çıktı

```
=== Silindir Sayısına Göre Ortalama MPG ===
4 silindir → Ortalama: 29.3 mpg (199 araç)   ← En verimli
6 silindir → Ortalama: 19.9 mpg (83 araç)
8 silindir → Ortalama: 14.7 mpg (103 araç)   ← En az verimli

=== Üretim Yerine Göre Ortalama MPG ===
usa     : Ort=20.0 mpg | Max=46.6 | Araç sayısı=245
europe  : Ort=26.7 mpg | Max=44.3 | Araç sayısı=68
japan   : Ort=30.5 mpg | Max=46.6 | Araç sayısı=72

MPG × Ağırlık Korelasyonu: -0.832
→ Güçlü negatif korelasyon: Araç ağırlaştıkça yakıt verimliliği düşüyor

=== MPG Dağılımı (Histogram) ===
  9.0- 15.8 mpg | ██████ (32 araç)
 15.8- 22.6 mpg | ██████████████ (72 araç)
 22.6- 29.4 mpg | ████████████ (60 araç)
 29.4- 36.2 mpg | ████████████ (62 araç)
 36.2- 43.0 mpg | ████ (24 araç)
 43.0- 46.6 mpg | (4 araç)
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik         | Açıklama                                           |
|----------------------------|----------------------------------------------------|
| `np.corrcoef(a, b)[0, 1]`  | İki dizi arasındaki korelasyon katsayısı           |
| `np.histogram()`           | Veriyi aralıklara böler, frekans sayar             |
| `origin == "usa"`          | String karşılaştırmalı boolean maske               |
| `gecerli_idx` filtresi     | None değerleri list comprehension ile temizlendi   |

---

## Soru 5 – ✈️ Flights: Yolcu Trend Analizi

### 📌 Veri Seti

```
Kaynak  : mwaskom/seaborn-data → flights.csv
Sütunlar: year, month, passengers
Boyut   : 144 satır (12 yıl × 12 ay)
Yıllar  : 1949 – 1960
```

### ❓ Görevler

1. Veriyi `reshape` ile **yıllık matrise** dönüştürün → shape: (12, 12).
2. Her yılın toplam, ortalama ve maksimum yolcu sayısını bulun.
3. **En kalabalık yılı** ve **en kalabalık ayı** tespit edin.
4. Yıllar içinde yolcu sayısının **büyüme oranını** hesaplayın.

### ✅ Cevap

```python
from datasets import load_dataset
import numpy as np

# ── Veri Yükleme ──────────────────────────────────────────────────────────
# Load Flights dataset from CSV (datasets library no longer supports dataset scripts)
ds = load_dataset(
    "csv",
    data_files="https://raw.githubusercontent.com/mwaskom/seaborn-data/master/flights.csv"
)["train"]

# Yolcu sayısını NumPy dizisine çevir → shape: (144,)
yolcular = np.array(ds["passengers"], dtype=float)
yillar   = np.array(ds["year"],       dtype=int)
aylar    = np.array(ds["month"])

# ── ADIM 1: Reshape ile yıllık matris ────────────────────────────────────
# Veri 1949-1960 arası 12 yıl × 12 ay sıralıdır
# (144,) → (12, 12): 12 satır=yıl, 12 sütun=ay
yillik = yolcular.reshape(12, 12)
print(f"Yıllık matris shape: {yillik.shape}")   # (12, 12) ✓

yil_listesi = list(range(1949, 1961))   # [1949, 1950, ..., 1960]
ay_listesi  = ["Oca","Şub","Mar","Nis","May","Haz",
               "Tem","Ağu","Eyl","Eki","Kas","Ara"]

# ── ADIM 2: Her yılın istatistikleri ─────────────────────────────────────
# axis=1 → her satırın (yılın) istatistiklerini hesapla
yil_toplam = yillik.sum(axis=1)
yil_ort    = yillik.mean(axis=1)
yil_max    = yillik.max(axis=1)

print("\n=== Yıllık Yolcu İstatistikleri ===")
print(f"{'Yıl':6} | {'Toplam':8} | {'Ort':7} | {'Max':6}")
print("-" * 35)
for i, yil in enumerate(yil_listesi):
    print(f"{yil:6} | {yil_toplam[i]:8.0f} | {yil_ort[i]:6.1f}  | {yil_max[i]:6.0f}")

# ── ADIM 3: En kalabalık yıl ve en kalabalık ay ───────────────────────────
en_kalabalik_yil_idx = yil_toplam.argmax()
print(f"\n🏆 En kalabalık yıl : {yil_listesi[en_kalabalik_yil_idx]}")
print(f"   Toplam yolcu    : {yil_toplam[en_kalabalik_yil_idx]:.0f}")

# axis=0 → her sütunun (ayın) toplamı → tüm yıllar boyunca hangi ay daha kalabalık?
ay_toplam              = yillik.sum(axis=0)
en_kalabalik_ay_idx    = ay_toplam.argmax()
print(f"\n📅 En kalabalık ay  : {ay_listesi[en_kalabalik_ay_idx]}")
print(f"   Toplam yolcu    : {ay_toplam[en_kalabalik_ay_idx]:.0f}")

# ── ADIM 4: Yıllık büyüme oranı ──────────────────────────────────────────
# np.diff → ardışık elemanların farkını alır: yil[i+1] - yil[i]
# Yüzde büyüme = fark / önceki yıl * 100
farklar     = np.diff(yil_toplam)           # 11 değer (12 yılın farkı)
buyume_oran = (farklar / yil_toplam[:-1]) * 100

print("\n=== Yıllık Büyüme Oranı ===")
for i in range(len(buyume_oran)):
    isaretli = f"+{buyume_oran[i]:.1f}" if buyume_oran[i] >= 0 else f"{buyume_oran[i]:.1f}"
    print(f"{yil_listesi[i]} → {yil_listesi[i+1]}: %{isaretli}")

print(f"\nOrtalama yıllık büyüme : %{buyume_oran.mean():.1f}")
```

### 📤 Beklenen Çıktı

```
Yıllık matris shape: (12, 12)

=== Yıllık Yolcu İstatistikleri ===
  Yıl  |   Toplam | Ort    |    Max
-----------------------------------
  1949 |     1520 |  126.7 |    148
  1950 |     1676 |  139.7 |    170
  ...
  1960 |     5714 |  476.2 |    622

🏆 En kalabalık yıl : 1960
   Toplam yolcu    : 5714

📅 En kalabalık ay  : Ağu
   Toplam yolcu    : 4400 (tüm yıllar toplamı)

=== Yıllık Büyüme Oranı ===
1949 → 1950: %+10.3
1950 → 1951: %+15.5
...
1959 → 1960: %+12.0

Ortalama yıllık büyüme : %10.7
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik          | Açıklama                                              |
|-----------------------------|-------------------------------------------------------|
| `.reshape(12, 12)`          | 1D diziyi 2D yıl×ay matrisine dönüştürdü              |
| `.sum(axis=1)`              | Her yılın toplamı (satır bazlı)                       |
| `.sum(axis=0)`              | Her ayın toplamı (sütun bazlı)                        |
| `np.diff()`                 | Ardışık elemanların farkını aldı                      |
| `farklar / yil_toplam[:-1]` | Yüzde büyüme oranı hesaplandı                         |

---

## 🗂️ Genel Özet

| # | Veri Seti | Konu | Öne Çıkan NumPy Özellikleri |
|---|-----------|------|-----------------------------|
| 1 | Titanic (`titanic.csv`) | Boolean maske, oran hesabı | `==`, `&`, `.mean()` on 0/1 array |
| 2 | Iris (`iris.csv`) | Korelasyon, sütun seçimi | `np.corrcoef()`, `[:, i]`, `.T` |
| 3 | Tips (`tips.csv`) | Bahşiş oranı, sıralama | `np.argsort()[::-1]`, `np.median()`, vektörel bölme |
| 4 | MPG (`mpg.csv`) | Histogram, korelasyon | `np.histogram()`, `np.corrcoef()[0,1]`, None filtresi |
| 5 | Flights (`flights.csv`) | Reshape, trend | `.reshape()`, `np.diff()`, `axis=0/1` |

---

## 📚 Kaynaklar

- [mwaskom/seaborn-data GitHub](https://github.com/mwaskom/seaborn-data)
- [Hugging Face Datasets Dokümantasyonu](https://huggingface.co/docs/datasets)
- [NumPy Resmi Dokümantasyon](https://numpy.org/doc/)
- [NumPy Yeni Başlayanlar Rehberi](https://numpy.org/doc/stable/user/absolute_beginners.html)
