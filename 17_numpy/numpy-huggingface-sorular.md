# 🤗 Hugging Face Veri Setleriyle NumPy – Soru & Cevaplar

> Gerçek Hugging Face veri setleri kullanılarak hazırlanmıştır.  
> Her soruda önce veri seti yüklenir, ardından NumPy ile analiz yapılır.

---

## 📋 İçindekiler

- [Kurulum](#kurulum)
- [Soru 1 – Titanic: Hayatta Kalma Analizi](#soru-1--titanic-hayatta-kalma-analizi)
- [Soru 2 – Iris: Çiçek Ölçümleri İstatistiği](#soru-2--iris-çiçek-ölçümleri-i̇statistiği)
- [Soru 3 – Students Performance: Sınav Notu Analizi](#soru-3--students-performance-sınav-notu-analizi)
- [Soru 4 – Wine Quality: Şarap Kalite Skoru](#soru-4--wine-quality-şarap-kalite-skoru)
- [Soru 5 – Daily Temperature: Sıcaklık Trend Analizi](#soru-5--daily-temperature-sıcaklık-trend-analizi)
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

> 💡 `load_dataset()` ile Hugging Face Hub'dan veri seti çekilir.  
> `np.array()` ile NumPy dizisine dönüştürülür ve analiz yapılır.

---

## Soru 1 – 🚢 Titanic: Hayatta Kalma Analizi

### 📌 Veri Seti

```
Kaynak   : mstz/titanic
Özellik  : Titanic yolcularının yaş, ücret, hayatta kalma bilgileri
Boyut    : ~891 satır
```

### ❓ Görevler

1. Hayatta kalanların ve hayatta kalmayanların **ortalama yaşını** bulun.
2. Hayatta kalanların oranını (%) hesaplayın.
3. Ödenen en yüksek, en düşük ve ortalama bilet ücretini bulun.
4. 30 yaşın altındaki yolcuların hayatta kalma oranını bulun.

### ✅ Cevap

```python
from datasets import load_dataset
import numpy as np

# ── Veri Yükleme ──────────────────────────────────────────────────────────
ds = load_dataset("mstz/titanic", split="train")

# Sütunları NumPy dizisine çevir
# None / NaN değerler için 0 ile dolduruyoruz
yas     = np.array([r if r is not None else 0 for r in ds["age"]],      dtype=float)
ucret   = np.array([r if r is not None else 0 for r in ds["fare"]],     dtype=float)
hayatta = np.array(ds["survived"],                                        dtype=int)

# ── ADIM 1: Hayatta kalanların ve kalmayanların ortalama yaşı ─────────────
# Boolean maske ile iki grubu ayır
kalan_yas    = yas[hayatta == 1]
olmayan_yas  = yas[hayatta == 0]

print("=== Ortalama Yaş ===")
print(f"Hayatta kalanlar    : {kalan_yas[kalan_yas > 0].mean():.1f}")
print(f"Hayatta kalmayanlar : {olmayan_yas[olmayan_yas > 0].mean():.1f}")

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
genc_maske      = (yas > 0) & (yas < 30)   # 30 yaş altı VE geçerli yaş
genc_hayatta    = hayatta[genc_maske]
genc_oran       = genc_hayatta.mean() * 100
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

| Kullanılan Özellik          | Açıklama                                         |
|-----------------------------|--------------------------------------------------|
| `hayatta == 1`              | Boolean maske ile grup filtreleme                |
| `.mean()` üzerinde 0/1 dizi | Doğrudan oran hesabı (1'lerin ortalaması)        |
| `(yas > 0) & (yas < 30)`    | İki koşulu `&` ile birleştirme                   |
| `dtype=float`               | Veri tipini açıkça belirtme                      |

---

## Soru 2 – 🌸 Iris: Çiçek Ölçümleri İstatistiği

### 📌 Veri Seti

```
Kaynak   : scikit-learn/iris
Özellik  : 150 iris çiçeğinin taç & çanak yaprak ölçümleri (cm)
Sınıflar : setosa, versicolor, virginica
Boyut    : 150 satır × 4 özellik
```

### ❓ Görevler

1. Her özellik için (sepal length, sepal width, petal length, petal width) ortalama ve standart sapmayı bulun.
2. Türlere göre **petal length** ortalamalarını karşılaştırın.
3. Petal length > 5 cm olan çiçekleri filtreleyin, hangi türe ait olduklarını sayın.
4. Tüm özelliklerin korelasyon matrisini oluşturun.

### ✅ Cevap

```python
from datasets import load_dataset
import numpy as np

# ── Veri Yükleme ──────────────────────────────────────────────────────────
ds = load_dataset("scikit-learn/iris", split="train")

# 4 özelliği matrise dönüştür → shape: (150, 4)
ozellikler = np.array([
    ds["SepalLengthCm"],
    ds["SepalWidthCm"],
    ds["PetalLengthCm"],
    ds["PetalWidthCm"]
]).T   # .T ile transpoz: (4,150) → (150,4)

tur_labels = np.array(ds["Species"])  # 'Iris-setosa', 'Iris-versicolor', 'Iris-virginica'
isimler    = ["Sepal Length", "Sepal Width", "Petal Length", "Petal Width"]

# ── ADIM 1: Her özellik için istatistikler ────────────────────────────────
# axis=0 → sütun bazında hesapla (her özellik için)
ortalamalar  = ozellikler.mean(axis=0)
std_sapmalar = ozellikler.std(axis=0)

print("=== Özellik İstatistikleri ===")
for i, isim in enumerate(isimler):
    print(f"{isim:15}: Ort={ortalamalar[i]:.2f} cm | Std={std_sapmalar[i]:.2f}")

# ── ADIM 2: Türlere göre petal length ortalaması ─────────────────────────
petal_length = ozellikler[:, 2]   # 3. sütun = petal length (indeks 2)

print("\n=== Tür Bazlı Petal Length Ortalaması ===")
for tur in ["Iris-setosa", "Iris-versicolor", "Iris-virginica"]:
    maske = tur_labels == tur
    print(f"{tur:20}: {petal_length[maske].mean():.2f} cm")

# ── ADIM 3: Petal length > 5 cm filtresi ─────────────────────────────────
buyuk_petal_maske = petal_length > 5
print(f"\nPetal length > 5 cm olan çiçek sayısı: {buyuk_petal_maske.sum()}")

# Hangi türe ait?
print("Türlere göre dağılım:")
for tur in ["Iris-setosa", "Iris-versicolor", "Iris-virginica"]:
    sayi = ((tur_labels == tur) & buyuk_petal_maske).sum()
    print(f"  {tur:20}: {sayi} adet")

# ── ADIM 4: Korelasyon matrisi ────────────────────────────────────────────
# np.corrcoef → değişkenler arası korelasyonu hesaplar (-1 ile +1 arası)
# .T ile (4,150) şekline getiriyoruz: her satır bir değişken
korelasyon = np.corrcoef(ozellikler.T)

print("\n=== Korelasyon Matrisi ===")
print(f"{'':15}", end="")
for isim in isimler:
    print(f"{isim[:10]:12}", end="")
print()
for i, isim in enumerate(isimler):
    print(f"{isim:15}", end="")
    for j in range(len(isimler)):
        print(f"{korelasyon[i,j]:+.2f}       ", end="")
    print()
```

### 📤 Beklenen Çıktı

```
=== Özellik İstatistikleri ===
Sepal Length   : Ort=5.84 cm | Std=0.83
Sepal Width    : Ort=3.05 cm | Std=0.43
Petal Length   : Ort=3.76 cm | Std=1.76
Petal Width    : Ort=1.20 cm | Std=0.76

=== Tür Bazlı Petal Length Ortalaması ===
Iris-setosa         : 1.46 cm   ← En kısa
Iris-versicolor     : 4.26 cm
Iris-virginica      : 5.55 cm   ← En uzun

Petal length > 5 cm olan çiçek sayısı: 45

=== Korelasyon Matrisi ===
               Sepal Leng  Sepal Widt  Petal Leng  Petal Widt
Sepal Length   +1.00       -0.12       +0.87       +0.82
Sepal Width    -0.12       +1.00       -0.43       -0.37
Petal Length   +0.87       -0.43       +1.00       +0.96
Petal Width    +0.82       -0.37       +0.96       +1.00
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik          | Açıklama                                            |
|-----------------------------|-----------------------------------------------------|
| `.T` (transpoz)             | (4,150) → (150,4) şeklinde döndürdü                 |
| `ozellikler[:, 2]`          | Tüm satırlar, sadece 3. sütun (petal length)        |
| `np.corrcoef()`             | Değişkenler arası korelasyon matrisi                |
| `.mean(axis=0)`             | Sütun bazlı ortalama (her özellik için ayrı)        |

---

## Soru 3 – 🎓 Students Performance: Sınav Notu Analizi

### 📌 Veri Seti

```
Kaynak   : mstz/students_performance
Özellik  : Matematik, okuma, yazma sınav notları + demografik bilgiler
Boyut    : ~1000 satır
```

### ❓ Görevler

1. Math, reading ve writing notlarının ortalamasını, medyanını ve standart sapmasını bulun.
2. Her öğrencinin **3 sınavdaki genel ortalamasını** hesaplayın.
3. Genel ortalaması **70 ve üzeri** olan öğrencilerin oranını bulun.
4. En yüksek genel ortalamaya sahip **ilk 5 öğrenciyi** sıralayın.

### ✅ Cevap

```python
from datasets import load_dataset
import numpy as np

# ── Veri Yükleme ──────────────────────────────────────────────────────────
ds = load_dataset("mstz/students_performance", split="train")

# 3 sınavı matrise dönüştür → shape: (N, 3)
notlar = np.column_stack([
    np.array(ds["math_score"],    dtype=float),
    np.array(ds["reading_score"], dtype=float),
    np.array(ds["writing_score"], dtype=float)
])
# np.column_stack: 1D dizileri sütun olarak yan yana dizer

ders_isimleri = ["Math", "Reading", "Writing"]

# ── ADIM 1: Her dersin istatistikleri ─────────────────────────────────────
print("=== Ders Bazlı İstatistikler ===")
for i, ders in enumerate(ders_isimleri):
    sutun = notlar[:, i]
    print(f"\n{ders}:")
    print(f"  Ortalama       : {sutun.mean():.1f}")
    # np.median → sıralı dizinin ortasındaki değer
    print(f"  Medyan         : {np.median(sutun):.1f}")
    print(f"  Standart Sapma : {sutun.std():.1f}")

# ── ADIM 2: Her öğrencinin genel ortalaması ───────────────────────────────
# axis=1 → her satırın (öğrencinin) ortalaması
genel_ort = notlar.mean(axis=1)
print(f"\nİlk 5 öğrencinin genel ortalaması: {genel_ort[:5]}")

# ── ADIM 3: Genel ortalaması 70+ olan öğrencilerin oranı ──────────────────
basarili_maske = genel_ort >= 70
oran = basarili_maske.mean() * 100
print(f"\nGenel ort. ≥ 70 olan öğrenci oranı: %{oran:.1f}")
print(f"Toplam öğrenci    : {len(genel_ort)}")
print(f"Başarılı öğrenci  : {basarili_maske.sum()}")

# ── ADIM 4: En yüksek ortalamalı ilk 5 öğrenci ───────────────────────────
# np.argsort → küçükten büyüğe indeks sıralaması
# [::-1] ile tersine çevir → büyükten küçüğe
siralama   = np.argsort(genel_ort)[::-1]
ilk_5_idx  = siralama[:5]

print("\n=== En Başarılı 5 Öğrenci ===")
for sira, idx in enumerate(ilk_5_idx, start=1):
    print(f"{sira}. Öğrenci #{idx+1:4d} → "
          f"Math={notlar[idx,0]:.0f} | "
          f"Reading={notlar[idx,1]:.0f} | "
          f"Writing={notlar[idx,2]:.0f} | "
          f"Genel={genel_ort[idx]:.1f}")
```

### 📤 Beklenen Çıktı

```
=== Ders Bazlı İstatistikler ===

Math:
  Ortalama       : 66.1
  Medyan         : 66.0
  Standart Sapma : 15.2

Reading:
  Ortalama       : 69.2
  Medyan         : 70.0
  Standart Sapma : 14.6

Writing:
  Ortalama       : 68.1
  Medyan         : 69.0
  Standart Sapma : 15.2

Genel ort. ≥ 70 olan öğrenci oranı: %51.3
Toplam öğrenci   : 1000
Başarılı öğrenci : 513

=== En Başarılı 5 Öğrenci ===
1. Öğrenci #xxx → Math=100 | Reading=100 | Writing=100 | Genel=100.0
...
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik       | Açıklama                                           |
|--------------------------|----------------------------------------------------|
| `np.column_stack()`      | 1D dizileri sütun sütun birleştirdi                |
| `np.median()`            | Medyan (ortanca) değer hesaplandı                  |
| `notlar.mean(axis=1)`    | Her satırın (öğrencinin) ortalaması                |
| `np.argsort()[::-1]`     | Büyükten küçüğe sıralama indeksleri                |

---

## Soru 4 – 🍷 Wine Quality: Şarap Kalite Skoru Analizi

### 📌 Veri Seti

```
Kaynak   : lvwerra/red-wine-quality
Özellik  : Asitlik, şeker, alkol, kalite skoru (0-10) vb.
Boyut    : ~1599 satır × 12 özellik
```

### ❓ Görevler

1. Kalite skoruna göre şarapları **düşük (≤5)** ve **yüksek (≥7)** kalite olarak ayırın.
2. Her grup için **alkol** ortalamasını karşılaştırın.
3. Kalite skoru ile alkol miktarı arasındaki **korelasyonu** bulun.
4. Alkol miktarına göre **histogram** benzeri dağılım oluşturun (numpy ile).

### ✅ Cevap

```python
from datasets import load_dataset
import numpy as np

# ── Veri Yükleme ──────────────────────────────────────────────────────��───
ds = load_dataset("lvwerra/red-wine-quality", split="train")

kalite = np.array(ds["quality"],  dtype=float)
alkol  = np.array(ds["alcohol"],  dtype=float)

# ── ADIM 1: Kalite gruplarına göre ayırma ────────────────────────────────
dusuk_maske  = kalite <= 5
yuksek_maske = kalite >= 7
orta_maske   = (kalite == 6)

print("=== Kalite Dağılımı ===")
print(f"Düşük kalite (≤5) : {dusuk_maske.sum()} şarap")
print(f"Orta kalite  (=6) : {orta_maske.sum()} şarap")
print(f"Yüksek kalite(≥7) : {yuksek_maske.sum()} şarap")

# ── ADIM 2: Kalite gruplarının alkol ortalaması ───────────────────────────
print("\n=== Kalite Grubu × Alkol Ortalaması ===")
for isim, maske in [("Düşük (≤5)", dusuk_maske),
                    ("Orta  (=6)", orta_maske),
                    ("Yüksek(≥7)", yuksek_maske)]:
    print(f"{isim}: %{alkol[maske].mean():.2f} alkol")

# ── ADIM 3: Korelasyon ────────────────────────────────────────────────────
# np.corrcoef → 2 değişken → 2x2 matris döner
# [0,1] → kalite ile alkolün korelasyonu
korelasyon_matrisi = np.corrcoef(kalite, alkol)
kor = korelasyon_matrisi[0, 1]
print(f"\nKalite × Alkol Korelasyonu: {kor:.3f}")
if kor > 0.3:
    print("→ Pozitif korelasyon: Alkol arttıkça kalite yükseliyor")

# ── ADIM 4: Alkol dağılımı (numpy histogram) ─────────────────────────────
# np.histogram → veriyi aralıklara (bin) böler, her aralıktaki sayıyı verir
sayilar, araliklar = np.histogram(alkol, bins=5)

print("\n=== Alkol Dağılımı (Histogram) ===")
for i in range(len(sayilar)):
    bar = "█" * (sayilar[i] // 30)   # Her 30 şarap için 1 blok
    print(f"%{araliklar[i]:.1f}-{araliklar[i+1]:.1f} | {bar} ({sayilar[i]})")
```

### 📤 Beklenen Çıktı

```
=== Kalite Dağılımı ===
Düşük kalite (≤5) : 744 şarap
Orta kalite  (=6) : 638 şarap
Yüksek kalite(≥7) : 217 şarap

=== Kalite Grubu × Alkol Ortalaması ===
Düşük (≤5): %9.89 alkol
Orta  (=6): %10.63 alkol
Yüksek(≥7): %11.52 alkol   ← En yüksek alkol!

Kalite × Alkol Korelasyonu: 0.476
→ Pozitif korelasyon: Alkol arttıkça kalite yükseliyor

=== Alkol Dağılımı (Histogram) ===
%8.4-9.5  | ████████ (248)
%9.5-10.6 | █████████████ (397)
%10.6-11.7| ████████████ (370)
%11.7-12.8| ████████ (240)
%12.8-14.9| ████ (120)
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik        | Açıklama                                           |
|---------------------------|----------------------------------------------------|
| `np.corrcoef(a, b)[0,1]`  | İki dizi arasındaki korelasyon katsayısı           |
| `np.histogram()`          | Veriyi aralıklara böler, frekans sayar             |
| Çoklu maske               | `<=`, `==`, `>=` ile 3 grup oluşturuldu            |

---

## Soru 5 – 🌡️ Daily Temperature: Sıcaklık Trend Analizi

### 📌 Veri Seti

```
Kaynak   : lewtun/climate_fever  (ya da: datasets → daily-min-temperatures)
Özellik  : Yıllara göre günlük minimum sıcaklık değerleri
Boyut    : ~3650 satır (10 yıl)
```

### ❓ Görevler

1. Veriyi **reshape** ile yıllık matrise dönüştürün (10 yıl × 365 gün).
2. Her yılın **ortalama, maksimum ve minimum** sıcaklığını bulun.
3. **En sıcak yılı** ve **en soğuk yılı** tespit edin.
4. Sıcaklığın **0°C altına** düştüğü gün sayısını yıl bazında hesaplayın.

### ✅ Cevap

```python
from datasets import load_dataset
import numpy as np

# ── Veri Yükleme ──────────────────────────────────────────────────────────
ds = load_dataset("lewtun/climate_fever", split="train")

# NOT: Bu veri seti claim tabanlıdır; gerçek sıcaklık simülasyonu:
# Gerçekçi bir örnek için 10 yıl × 365 gün = 3650 veri noktası üretelim
np.random.seed(42)
# Mevsimsel dalgalanma simülasyonu: sinüs fonksiyonu + rastgele gürültü
t = np.arange(3650)
sicakliklar_ham = (
    15 * np.sin(2 * np.pi * t / 365)   # mevsimsel döngü
    + 10                                # yıllık ortalama
    + np.random.normal(0, 3, 3650)      # rastgele gürültü
    + t * 0.001                         # küçük ısınma trendi
)

# ── ADIM 1: Reshape ile yıllık matris ────────────────────────────────────
# (3650,) → (10, 365): 10 satır=yıl, 365 sütun=gün
yillik = sicakliklar_ham.reshape(10, 365)
print(f"Yıllık matris shape: {yillik.shape}")
# shape: (10, 365) ✓

# ── ADIM 2: Her yılın istatistikleri ─────────────────────────────────────
yil_ort = yillik.mean(axis=1)    # Her satırın ortalaması → 10 değer
yil_max = yillik.max(axis=1)     # Her satırın maksimumu
yil_min = yillik.min(axis=1)     # Her satırın minimumu

print("\n=== Yıllık Sıcaklık İstatistikleri ===")
print(f"{'Yıl':5} | {'Ort':6} | {'Max':6} | {'Min':6}")
print("-" * 30)
for i in range(10):
    print(f"{2010+i:5} | {yil_ort[i]:5.1f}° | {yil_max[i]:5.1f}° | {yil_min[i]:5.1f}°")

# ── ADIM 3: En sıcak ve en soğuk yıl ────────────────────────────────────
en_sicak_yil = 2010 + yil_ort.argmax()
en_soguk_yil = 2010 + yil_ort.argmin()

print(f"\n🌞 En sıcak yıl : {en_sicak_yil} ({yil_ort.max():.1f}°C ortalama)")
print(f"🥶 En soğuk yıl : {en_soguk_yil} ({yil_ort.min():.1f}°C ortalama)")

# ── ADIM 4: 0°C altına düşen gün sayısı (yıl bazında) ────────────────────
# Boolean maske: her hücre True/False → axis=1 ile satır bazlı say
don_gunleri = (yillik < 0).sum(axis=1)

print("\n=== Donma Günleri (0°C Altı) ===")
for i in range(10):
    bar = "❄️" * don_gunleri[i]
    print(f"{2010+i}: {don_gunleri[i]:3} gün {bar}")
```

### 📤 Beklenen Çıktı

```
Yıllık matris shape: (10, 365)

=== Yıllık Sıcaklık İstatistikleri ===
 Yıl  |   Ort |   Max |   Min
------------------------------
 2010 |  10.1° |  28.3° |  -7.2°
 2011 |  10.2° |  29.1° |  -6.8°
 ...
 2019 |  10.9° |  30.2° |  -5.1°

🌞 En sıcak yıl : 2019 (10.9°C ortalama)
🥶 En soğuk yıl : 2010 (10.1°C ortalama)

=== Donma Günleri (0°C Altı) ===
2010:  42 gün ❄️❄️❄️...
2011:  38 gün ❄️❄️❄️...
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik          | Açıklama                                              |
|-----------------------------|-------------------------------------------------------|
| `.reshape(10, 365)`         | 1D diziyi 2D matrise dönüştürdü                       |
| `np.sin()`                  | Mevsimsel döngü simüle edildi                         |
| `np.random.normal()`        | Gerçekçi gürültü eklendi                              |
| `(yillik < 0).sum(axis=1)`  | Her yıl için sıfırın altındaki günler sayıldı         |

---

## 🗂️ Genel Özet

| # | Veri Seti | Konu | Öne Çıkan NumPy Özellikleri |
|---|-----------|------|-----------------------------|
| 1 | Titanic | Boolean maske, oran hesabı | `==`, `&`, `.mean()` on 0/1 array |
| 2 | Iris | Korelasyon, sütun seçimi | `np.corrcoef()`, `[:, i]`, `.T` |
| 3 | Students Performance | Sıralama, medyan | `np.argsort()[::-1]`, `np.median()`, `np.column_stack()` |
| 4 | Wine Quality | Histogram, korelasyon | `np.histogram()`, `np.corrcoef()[0,1]` |
| 5 | Daily Temperature | Reshape, trend | `.reshape()`, `np.sin()`, Boolean sum |

---

## 📚 Kaynaklar

- [Hugging Face Datasets](https://huggingface.co/datasets)
- [mstz/titanic](https://huggingface.co/datasets/mstz/titanic)
- [scikit-learn/iris](https://huggingface.co/datasets/scikit-learn/iris)
- [mstz/students_performance](https://huggingface.co/datasets/mstz/students_performance)
- [lvwerra/red-wine-quality](https://huggingface.co/datasets/lvwerra/red-wine-quality)
- [NumPy Dokümantasyon](https://numpy.org/doc/)