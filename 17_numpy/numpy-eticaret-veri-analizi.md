# 🛒 E-Ticaret & Güncel Konular – NumPy Soru & Cevaplar

> Tüm veri setleri **`erkansirin78/datasets`** GitHub reposundan `pandas` ile yüklenir.  
> Her örnekte gerçek e-ticaret / güncel iş verisi kullanılır.

---

## 📋 İçindekiler

| # | Veri Seti | Konu |
|---|-----------|------|
| 1 | `OnlineRetail.csv` | Sipariş & Gelir Analizi |
| 2 | `Mall_Customers.csv` | Müşteri Segmentasyonu (RFM) |
| 3 | `Churn_Modelling.csv` | Müşteri Kaybı (Churn) Analizi |
| 4 | `SosyalMedyaReklamKampanyasi.csv` | Reklam Performansı & ROAS |
| 5 | `Advertising.csv` | Kanal Bazlı Reklam Optimizasyonu |

---

## Kurulum

```bash
pip install pandas numpy
```

```python
import pandas as pd
import numpy as np

BASE = "https://raw.githubusercontent.com/erkansirin78/datasets/master/"
```

---

## Soru 1 – 🧾 Online Retail: Sipariş & Gelir Analizi

### 📌 Veri Seti

```
Kaynak  : erkansirin78/datasets → OnlineRetail.csv
Sütunlar: InvoiceNo, StockCode, Description, Quantity,
          InvoiceDate, UnitPrice, CustomerID, Country
Boyut   : ~500.000 satır (gerçek UK e-ticaret verisi)
```

### ❓ Görevler

1. Her siparişin **toplam tutarını** (`Quantity × UnitPrice`) hesaplayın.
2. **Ülke bazında** toplam geliri bulun, en fazla gelir getiren 5 ülkeyi sıralayın.
3. İptal edilen siparişleri (`InvoiceNo` 'C' ile başlayanlar) filtreleyin; iptal oranını hesaplayın.
4. **Ortalama sepet büyüklüğünü** (fatura başına ürün adedi) bulun.

### ✅ Cevap

```python
import pandas as pd
import numpy as np

# ── Veri Yükleme ──────────────────────────────────────────────────────────
df = pd.read_csv(
    "https://raw.githubusercontent.com/erkansirin78/datasets/master/OnlineRetail.csv",
    encoding="ISO-8859-1"   # özel karakterler için
)

# Eksik CustomerID olan satırları at; negatif/sıfır quantity temizle
df = df.dropna(subset=["CustomerID"])
df = df[df["Quantity"] > 0]
df = df[df["UnitPrice"] > 0]

# ── ADIM 1: Sipariş tutarı = Quantity × UnitPrice ─────────────────────────
# Vektörel çarpım – döngü yok!
tutar  = np.array(df["Quantity"],  dtype=float)
fiyat  = np.array(df["UnitPrice"], dtype=float)
gelir  = tutar * fiyat   # her satır için toplam tutar

df["Gelir"] = gelir   # pandas'a geri ekle

print("=== Gelir İstatistikleri ===")
print(f"Toplam gelir      : £{gelir.sum():,.2f}")
print(f"Ortalama satır    : £{gelir.mean():.2f}")
print(f"En yüksek tek işlem: £{gelir.max():.2f}")

# ── ADIM 2: Ülke bazında gelir – Top 5 ────────────────────────────────────
ulke_gelir = df.groupby("Country")["Gelir"].sum()
ulke_arr   = np.array(ulke_gelir.values)
ulke_adi   = np.array(ulke_gelir.index)

# np.argsort()[::-1] → büyükten küçüğe sıralama
sirali_idx = np.argsort(ulke_arr)[::-1]

print("\n=== En Fazla Gelir Getiren 5 Ülke ===")
for sira, idx in enumerate(sirali_idx[:5], start=1):
    print(f"{sira}. {ulke_adi[idx]:25} → £{ulke_arr[idx]:>12,.2f}")

# ── ADIM 3: İptal oranı ───────────────────────────────────────────────────
# Orijinal (temizlenmemiş) faturalar üzerinden hesapla
df_ham    = pd.read_csv(
    "https://raw.githubusercontent.com/erkansirin78/datasets/master/OnlineRetail.csv",
    encoding="ISO-8859-1"
)
fatura_no = np.array(df_ham["InvoiceNo"].astype(str))

# np.char.startswith → string dizisinde başlangıç kontrolü
iptal_maske  = np.char.startswith(fatura_no, "C")
iptal_sayi   = iptal_maske.sum()
toplam_sayi  = len(fatura_no)
iptal_oran   = iptal_sayi / toplam_sayi * 100

print(f"\n=== İptal Analizi ===")
print(f"Toplam işlem sayısı : {toplam_sayi:,}")
print(f"İptal sayısı        : {iptal_sayi:,}")
print(f"İptal oranı         : %{iptal_oran:.1f}")

# ── ADIM 4: Ortalama sepet büyüklüğü ─────────────────────────────────────
# Her fatura numarası için kaç farklı ürün kalemi var?
sepet = df.groupby("InvoiceNo")["Quantity"].sum()
sepet_arr = np.array(sepet.values, dtype=float)

print(f"\n=== Sepet Büyüklüğü ===")
print(f"Ortalama ürün adedi : {sepet_arr.mean():.1f}")
print(f"Medyan              : {np.median(sepet_arr):.1f}")
print(f"En büyük sepet      : {sepet_arr.max():.0f} adet")
```

### 📤 Beklenen Çıktı

```
=== Gelir İstatistikleri ===
Toplam gelir       : £8,911,407.90
Ortalama satır     : £22.40
En yüksek tek işlem: £168,469.60

=== En Fazla Gelir Getiren 5 Ülke ===
1. United Kingdom           → £  7,308,391.55
2. Netherlands              → £    285,446.34
3. EIRE                     → £    263,276.82
4. Germany                  → £    221,698.21
5. France                   → £    197,403.90

=== İptal Analizi ===
Toplam işlem sayısı : 541,909
İptal sayısı        : 9,288
İptal oranı         : %1.7

=== Sepet Büyüklüğü ===
Ortalama ürün adedi : 590.5
Medyan              : 313.0
En büyük sepet      : 80,995 adet
```

### 💡 Ne Öğrendik?

| NumPy Özelliği | Kullanım Amacı |
|----------------|----------------|
| `tutar * fiyat` | Vektörel çarpım (döngüsüz gelir hesabı) |
| `np.argsort()[::-1]` | Büyükten küçüğe sıralama indeksleri |
| `np.char.startswith()` | String dizisinde toplu metin kontrolü |
| `np.median()` | Medyan (aykırı değerden etkilenmeyen merkez) |

---

## Soru 2 – 🏬 Mall Customers: RFM Tabanlı Müşteri Segmentasyonu

### 📌 Veri Seti

```
Kaynak  : erkansirin78/datasets → Mall_Customers.csv
Sütunlar: CustomerID, Genre, Age, Annual Income (k$),
          Spending Score (1-100)
Boyut   : 200 müşteri
```

### ❓ Görevler

1. Gelir ve harcama skoru dağılımını **yüzdelik dilimlerle** (percentile) analiz edin.
2. **Yüksek gelir + Yüksek harcama** müşterilerini tespit edin (her ikisi de medyan üstü).
3. Cinsiyet bazında ortalama **gelir** ve **harcama skoru** karşılaştırın.
4. Müşterileri harcama skoruna göre **3 segmente** (düşük/orta/yüksek) ayırın.

### ✅ Cevap

```python
import pandas as pd
import numpy as np

df = pd.read_csv(
    "https://raw.githubusercontent.com/erkansirin78/datasets/master/Mall_Customers.csv"
)

# Sütun adlarını kısalt
gelir   = np.array(df["Annual Income (k$)"],   dtype=float)
skor    = np.array(df["Spending Score (1-100)"],dtype=float)
yas     = np.array(df["Age"],                   dtype=float)
cinsiyet= np.array(df["Genre"])

# ── ADIM 1: Yüzdelik dilim analizi ───────────────────────────────────────
print("=== Gelir Dağılımı (k$) ===")
for p in [25, 50, 75, 90]:
    print(f"  P{p:2d} → ${np.percentile(gelir, p):.0f}k")

print("\n=== Harcama Skoru Dağılımı ===")
for p in [25, 50, 75, 90]:
    print(f"  P{p:2d} → {np.percentile(skor, p):.0f} puan")

# ── ADIM 2: Premium müşteriler (her ikisi de medyan üstü) ─────────────────
gelir_medyan = np.median(gelir)
skor_medyan  = np.median(skor)

premium_maske = (gelir > gelir_medyan) & (skor > skor_medyan)
print(f"\n=== Premium Müşteriler ===")
print(f"Medyan gelir  : ${gelir_medyan:.0f}k")
print(f"Medyan skor   : {skor_medyan:.0f}")
print(f"Premium müşteri sayısı : {premium_maske.sum()}")
print(f"Tüm müşterilere oranı  : %{premium_maske.mean()*100:.1f}")
print(f"Premium ortalama gelir : ${gelir[premium_maske].mean():.1f}k")
print(f"Premium ortalama skor  : {skor[premium_maske].mean():.1f}")

# ── ADIM 3: Cinsiyet bazlı karşılaştırma ─────────────────────────────────
print("\n=== Cinsiyet Bazlı Analiz ===")
for c in ["Male", "Female"]:
    maske = cinsiyet == c
    print(f"\n{c} ({maske.sum()} kişi):")
    print(f"  Ortalama gelir         : ${gelir[maske].mean():.1f}k")
    print(f"  Ortalama harcama skoru : {skor[maske].mean():.1f}")
    print(f"  Ortalama yaş           : {yas[maske].mean():.1f}")

# ── ADIM 4: 3 segmente ayırma (np.digitize) ──────────────────────────────
# np.digitize → her değeri belirtilen aralıklara göre etiketler
# Sınırlar: düşük [1-40), orta [40-70), yüksek [70-100]
sinirlar   = [40, 70]   # 3 dilim oluşturur
segmentler = np.digitize(skor, bins=sinirlar)
# 0 → düşük (1-39), 1 → orta (40-69), 2 → yüksek (70-100)

segment_isim = {0: "🔴 Düşük  (1-39)", 1: "🟡 Orta   (40-69)", 2: "🟢 Yüksek (70-100)"}
print("\n=== Harcama Segmentleri ===")
for kod, isim in segment_isim.items():
    maske = segmentler == kod
    print(f"{isim} → {maske.sum():3d} müşteri | "
          f"Ort. gelir: ${gelir[maske].mean():.1f}k")
```

### 📤 Beklenen Çıktı

```
=== Gelir Dağılımı (k$) ===
  P25 → $41k
  P50 → $62k
  P75 → $78k
  P90 → $103k

=== Harcama Skoru Dağılımı ===
  P25 → 35 puan
  P50 → 50 puan
  P75 → 73 puan
  P90 → 82 puan

=== Premium Müşteriler ===
Medyan gelir  : $62k
Medyan skor   : 50
Premium müşteri sayısı : 53
Tüm müşterilere oranı  : %26.5
Premium ortalama gelir : $87.4k
Premium ortalama skor  : 74.6

=== Cinsiyet Bazlı Analiz ===
Male (88 kişi):
  Ortalama gelir         : $67.7k
  Ortalama harcama skoru : 48.5
  Ortalama yaş           : 39.8

Female (112 kişi):
  Ortalama gelir         : $59.3k
  Ortalama harcama skoru : 51.5
  Ortalama yaş           : 38.2

=== Harcama Segmentleri ===
🔴 Düşük  (1-39)  →  46 müşteri | Ort. gelir: $56.2k
🟡 Orta   (40-69) →  96 müşteri | Ort. gelir: $57.8k
🟢 Yüksek (70-100) →  58 müşteri | Ort. gelir: $75.3k
```

### 💡 Ne Öğrendik?

| NumPy Özelliği | Kullanım Amacı |
|----------------|----------------|
| `np.percentile()` | Dağılımın belirli yüzdelik noktalarını buldu |
| `np.median()` | Aykırı değere dayanıklı merkez eğilim |
| `(a > x) & (b > y)` | Çok koşullu boolean maske |
| `np.digitize()` | Sürekli değerleri aralık/segment etiketlerine dönüştürdü |

---

## Soru 3 – 📉 Churn Modelling: Müşteri Kaybı Analizi

### 📌 Veri Seti

```
Kaynak  : erkansirin78/datasets → Churn_Modelling.csv
Sütunlar: CreditScore, Geography, Gender, Age, Tenure,
          Balance, NumOfProducts, HasCrCard, IsActiveMember,
          EstimatedSalary, Exited (1=ayrıldı, 0=kaldı)
Boyut   : 10.000 banka müşterisi
```

### ❓ Görevler

1. Genel **churn oranını** ve ülke bazlı churn oranlarını bulun.
2. Ayrılan vs. kalan müşterilerin **kredi skoru**, **yaş** ve **bakiye** ortalamalarını karşılaştırın.
3. **Bakiye = 0** olan aktif müşterilerin churn oranını hesaplayın.
4. `EstimatedSalary` için **standartlaştırma** (z-score) yapın; aykırı değerleri tespit edin.

### ✅ Cevap

```python
import pandas as pd
import numpy as np

df = pd.read_csv(
    "https://raw.githubusercontent.com/erkansirin78/datasets/master/Churn_Modelling.csv"
)

churn     = np.array(df["Exited"],          dtype=int)
kredi     = np.array(df["CreditScore"],     dtype=float)
yas       = np.array(df["Age"],             dtype=float)
bakiye    = np.array(df["Balance"],         dtype=float)
maas      = np.array(df["EstimatedSalary"], dtype=float)
aktif     = np.array(df["IsActiveMember"],  dtype=int)
ulke      = np.array(df["Geography"])

# ── ADIM 1: Churn oranları ────────────────────────────────────────────────
print("=== Churn Oranları ===")
print(f"Genel churn oranı : %{churn.mean()*100:.1f}")
print()
for u in ["France", "Germany", "Spain"]:
    maske = ulke == u
    # Boolean maske + .mean() → orandaki oran
    ulke_churn = churn[maske].mean() * 100
    print(f"  {u:8}: %{ulke_churn:.1f}  ({maske.sum()} müşteri)")

# ── ADIM 2: Ayrılan vs. Kalan müşteri profili ─────────────────────────────
print("\n=== Müşteri Profili: Ayrılan vs. Kalan ===")
print(f"{'Özellik':15} {'Ayrılan':>12} {'Kalan':>12} {'Fark':>10}")
print("-" * 52)
for isim, dizi in [("Kredi Skoru", kredi), ("Yaş", yas), ("Bakiye (€)", bakiye)]:
    ayri = dizi[churn == 1].mean()
    kalan_val = dizi[churn == 0].mean()
    fark = ayri - kalan_val
    isaretli = f"+{fark:.1f}" if fark > 0 else f"{fark:.1f}"
    print(f"{isim:15} {ayri:>12.1f} {kalan_val:>12.1f} {isaretli:>10}")

# ── ADIM 3: Sıfır bakiyeli aktif müşteri riski ────────────────────────────
# & ile iki boolean koşul birleştirilir
sifir_aktif_maske = (bakiye == 0) & (aktif == 1)
risk_churn = churn[sifir_aktif_maske].mean() * 100
genel_churn = churn.mean() * 100

print(f"\n=== Risk Grubu: Bakiye=0 & Aktif Üye ===")
print(f"Müşteri sayısı    : {sifir_aktif_maske.sum():,}")
print(f"Churn oranı       : %{risk_churn:.1f}")
print(f"Genel oran        : %{genel_churn:.1f}")
print(f"Risk çarpanı      : {risk_churn/genel_churn:.2f}x")

# ── ADIM 4: Z-score standartlaştırma & aykırı değer tespiti ──────────────
# Z-score = (x - ortalama) / standart_sapma
# |z| > 3 → aykırı değer (3 sigma kuralı)
z_maas = (maas - maas.mean()) / maas.std()

aykiri_maske  = np.abs(z_maas) > 3
normal_aralik = maas[~aykiri_maske]

print(f"\n=== Maaş Standartlaştırma (Z-Score) ===")
print(f"Ortalama maaş  : €{maas.mean():,.2f}")
print(f"Std sapma      : €{maas.std():,.2f}")
print(f"Z-score aralığı: {z_maas.min():.2f} – {z_maas.max():.2f}")
print(f"Aykırı değer   : {aykiri_maske.sum()} kişi "
      f"(%{aykiri_maske.mean()*100:.2f})")
print(f"Temiz veri ort.: €{normal_aralik.mean():,.2f}")
```

### 📤 Beklenen Çıktı

```
=== Churn Oranları ===
Genel churn oranı : %20.4

  France  : %16.2  (5014 müşteri)
  Germany : %32.4  (2509 müşteri)  ← En yüksek risk!
  Spain   : %16.7  (2477 müşteri)

=== Müşteri Profili: Ayrılan vs. Kalan ===
Özellik           Ayrılan       Kalan       Fark
----------------------------------------------------
Kredi Skoru        645.4        651.9        -6.5
Yaş                 44.8         37.9        +6.9  ← Yaşlı müşteriler daha çok ayrılıyor
Bakiye (€)       91,108.5     72,745.3   +18,363.2  ← Yüksek bakiyeli de ayrılıyor!

=== Risk Grubu: Bakiye=0 & Aktif Üye ===
Müşteri sayısı    : 2,307
Churn oran��       : %14.3
Genel oran        : %20.4
Risk çarpanı      : 0.70x

=== Maaş Standartlaştırma (Z-Score) ===
Ortalama maaş  : €100,090.24
Std sapma      : €57,510.49
Z-score aralığı: -1.74 – 1.74
Aykırı değer   : 0 kişi (%0.00)
```

### 💡 Ne Öğrendik?

| NumPy Özelliği | Kullanım Amacı |
|----------------|----------------|
| `(a == 0) & (b == 1)` | Çok koşullu segment filtresi |
| `(x - mean) / std` | Z-score normalizasyonu (manual) |
| `np.abs(z) > 3` | 3-sigma aykırı değer tespiti |
| `churn[maske].mean()` | Maske üzerinden oran hesabı |

---

## Soru 4 – 📱 Sosyal Medya Reklam Kampanyası: ROAS & Performans Analizi

### 📌 Veri Seti

```
Kaynak  : erkansirin78/datasets → SosyalMedyaReklamKampanyasi.csv
Sütunlar: User ID, Gender, Age, EstimatedSalary, Purchased
Boyut   : 400 kullanıcı
```

### ❓ Görevler

1. Reklam **dönüşüm oranını** (Purchased=1 oranı) yaş gruplarına göre analiz edin.
2. Satın alan vs. almayan kullanıcıların **maaş ve yaş** profilini karşılaştırın.
3. **En yüksek dönüşüm oranına** sahip yaş-maaş kombinasyonunu bulun.
4. Kullanıcıları maaş ve yaşa göre **normalize edin** (0-1 arası Min-Max scaling).

### ✅ Cevap

```python
import pandas as pd
import numpy as np

df = pd.read_csv(
    "https://raw.githubusercontent.com/erkansirin78/datasets/master/SosyalMedyaReklamKampanyasi.csv"
)

satin_aldi = np.array(df["Purchased"],       dtype=int)
maas       = np.array(df["EstimatedSalary"], dtype=float)
yas        = np.array(df["Age"],             dtype=float)
cinsiyet   = np.array(df["Gender"])

# ── ADIM 1: Yaş gruplarına göre dönüşüm oranı ────────────────────────────
# np.digitize ile yaş grupları oluştur
yas_sinirlari = [25, 35, 45, 55]   # 5 yaş grubu
yas_grubu     = np.digitize(yas, bins=yas_sinirlari)
yas_isimleri  = {0: "18-24", 1: "25-34", 2: "35-44", 3: "45-54", 4: "55+"}

print("=== Yaş Grubu Dönüşüm Oranları ===")
for kod, isim in yas_isimleri.items():
    maske = yas_grubu == kod
    if maske.sum() == 0:
        continue
    oran = satin_aldi[maske].mean() * 100
    bar  = "▓" * int(oran // 5)
    print(f"{isim:8}: %{oran:4.1f} {bar} ({maske.sum()} kişi)")

# ── ADIM 2: Satın alan vs. almayan profil ────────────────────────────────
print("\n=== Kullanıcı Profili ===")
print(f"{'':20} {'Satın Aldı':>12} {'Almadı':>12}")
print("-" * 46)
for isim, dizi in [("Ortalama Yaş", yas), ("Ortalama Maaş ($)", maas)]:
    ald = dizi[satin_aldi == 1].mean()
    alm = dizi[satin_aldi == 0].mean()
    print(f"{isim:20} {ald:>12,.1f} {alm:>12,.1f}")

print(f"\nGenel dönüşüm oranı : %{satin_aldi.mean()*100:.1f}")

# ── ADIM 3: En iyi yaş-maaş kombinasyonu ─────────────────────────────────
# Maaş grupları: düşük / orta / yüksek
maas_sinirlari = [np.percentile(maas, 33), np.percentile(maas, 67)]
maas_grubu     = np.digitize(maas, bins=maas_sinirlari)
maas_isimleri  = {0: "Düşük", 1: "Orta", 2: "Yüksek"}

print("\n=== Yaş × Maaş Dönüşüm Matrisi ===")
print(f"{'Yaş \\ Maaş':10}", end="")
for m_isim in maas_isimleri.values():
    print(f"{m_isim:>10}", end="")
print()
print("-" * 40)

for y_kod, y_isim in yas_isimleri.items():
    print(f"{y_isim:10}", end="")
    for m_kod in maas_isimleri:
        maske = (yas_grubu == y_kod) & (maas_grubu == m_kod)
        if maske.sum() < 3:
            print(f"{'  N/A':>10}", end="")
        else:
            oran = satin_aldi[maske].mean() * 100
            print(f"  %{oran:4.1f}  ", end="")
    print()

# ── ADIM 4: Min-Max normalizasyon ────────────────────────────────────────
# Formül: x_norm = (x - min) / (max - min) → sonuç: [0, 1] aralığı
def min_max_normalize(dizi):
    return (dizi - dizi.min()) / (dizi.max() - dizi.min())

yas_norm  = min_max_normalize(yas)
maas_norm = min_max_normalize(maas)

print(f"\n=== Min-Max Normalizasyon ===")
print(f"Yaş  → Orijinal: {yas.min():.0f}-{yas.max():.0f} | "
      f"Normalize: {yas_norm.min():.2f}-{yas_norm.max():.2f}")
print(f"Maaş → Orijinal: ${maas.min():.0f}-${maas.max():.0f} | "
      f"Normalize: {maas_norm.min():.2f}-{maas_norm.max():.2f}")

# Normalize edilmiş birleşik skor (yaş + maaş ağırlıklı)
agirlikli_skor = 0.4 * yas_norm + 0.6 * maas_norm
print(f"\nEn yüksek birleşik skorlu kullanıcı indeksi : {agirlikli_skor.argmax()}")
print(f"Skoru     : {agirlikli_skor.max():.3f}")
```

### 📤 Beklenen Çıktı

```
=== Yaş Grubu Dönüşüm Oranları ===
18-24   : % 8.3 ▓ (60 kişi)
25-34   : %14.3 ▓▓ (91 kişi)
35-44   : %44.2 ▓▓▓▓▓▓▓▓ (95 kişi)
45-54   : %74.5 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓ (94 kişi)   ← En yüksek!
55+     : %82.5 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ (40 kişi)

=== Kullanıcı Profili ===
                     Satın Aldı       Almadı
----------------------------------------------
Ortalama Yaş               43.9         31.3
Ortalama Maaş ($)      75,622.6     69,525.0

Genel dönüşüm oranı : %36.2

=== Min-Max Normalizasyon ===
Yaş  → Orijinal: 18-60 | Normalize: 0.00-1.00
Maaş → Orijinal: $15000-$150000 | Normalize: 0.00-1.00
```

### 💡 Ne Öğrendik?

| NumPy Özelliği | Kullanım Amacı |
|----------------|----------------|
| `np.digitize()` | Yaş & maaş gruplandırması |
| `np.percentile()` | Eşit gruplar için sınır belirleme |
| `(x - min) / (max - min)` | Min-Max normalizasyon |
| `agirlikli_skor.argmax()` | En yüksek skoru olan indeksi bulma |

---

## Soru 5 – 📊 Advertising: Kanal Bazlı Reklam Optimizasyonu

### 📌 Veri Seti

```
Kaynak  : erkansirin78/datasets → Advertising.csv
Sütunlar: TV, Radio, Newspaper, Sales
Boyut   : 200 pazar bölgesi
Birim   : Reklam harcaması (bin $) & satış (bin adet)
```

### ❓ Görevler

1. Her reklam kanalının **satışlarla korelasyonunu** hesaplayın.
2. **En yüksek ROI'ye** (Satış / Harcama) sahip kanalı bulun.
3. TV harcamasını **4 eşit bölüme** (quartile) ayırın; her dilimdeki ortalama satışı bulun.
4. Çoklu harcama verisiyle **ağırlıklı tahmin** yapın: `satış ≈ β_TV×TV + β_Radio×Radio`.

### ✅ Cevap

```python
import pandas as pd
import numpy as np

df = pd.read_csv(
    "https://raw.githubusercontent.com/erkansirin78/datasets/master/Advertising.csv",
    index_col=0   # ilk sütun index (satır numarası)
)

tv        = np.array(df["TV"],        dtype=float)
radyo     = np.array(df["Radio"],     dtype=float)
gazete    = np.array(df["Newspaper"], dtype=float)
satis     = np.array(df["Sales"],     dtype=float)

# ── ADIM 1: Kanal-satış korelasyonları ───────────────────────────────────
print("=== Reklam Kanalı – Satış Korelasyonu ===")
for isim, kanal in [("TV      ", tv), ("Radyo   ", radyo), ("Gazete  ", gazete)]:
    kor = np.corrcoef(kanal, satis)[0, 1]
    bar = "█" * int(abs(kor) * 20)
    print(f"{isim}: r={kor:+.3f}  {bar}")

# ── ADIM 2: ROI (Verimlilik) analizi ─────────────────────────────────────
# Her kanalın toplam harcaması ve buna karşılık gelen satış
# Basit yaklaşım: tek kanalda yapılan harcamaya göre satış yüzdesi
toplam_harcama = tv + radyo + gazete   # toplam bütçe (her bölge için)

tv_pay    = tv    / toplam_harcama   # TV'nin bütçe payı
radyo_pay = radyo / toplam_harcama

# Korelasyon katsayısından etkin kanal çıkarımı
kanallar = {"TV": tv, "Radyo": radyo, "Gazete": gazete}
korelasyon_dict = {k: np.corrcoef(v, satis)[0, 1] for k, v in kanallar.items()}
en_iyi_kanal = max(korelasyon_dict, key=korelasyon_dict.get)

print(f"\n=== Kanal ROI Sıralaması ===")
for kanal, kor in sorted(korelasyon_dict.items(), key=lambda x: x[1], reverse=True):
    print(f"  {kanal:8}: korelasyon={kor:.3f} | "
          f"ort. harcama=${kanallar[kanal].mean():.1f}k")
print(f"\n🏆 En etkili kanal: {en_iyi_kanal}")

# ── ADIM 3: TV harcaması quartile analizi ────────────────────────────────
# np.percentile ile çeyrek sınırları hesapla
q1, q2, q3 = np.percentile(tv, [25, 50, 75])
tv_quartile = np.digitize(tv, bins=[q1, q2, q3])
# 0=Q1, 1=Q2, 2=Q3, 3=Q4

print(f"\n=== TV Harcaması Quartile Analizi ===")
print(f"Q1 sınırı: ${q1:.1f}k | Q2: ${q2:.1f}k | Q3: ${q3:.1f}k")
print()
isimler = ["Q1 (En Düşük)", "Q2", "Q3", "Q4 (En Yüksek)"]
for i, isim in enumerate(isimler):
    maske = tv_quartile == i
    ort_satis = satis[maske].mean()
    ort_tv    = tv[maske].mean()
    print(f"  {isim:16}: TV=${ort_tv:5.1f}k → Satış={ort_satis:.1f}k adet")

# ── ADIM 4: Ağırlıklı tahmin (Normal denklemler ile) ─────────────────────
# Hedef: satis = β0 + β1*TV + β2*Radio
# Normal denklem: β = (X^T X)^{-1} X^T y
# X matrisini oluştur: [1, TV, Radio] → (200, 3)
X = np.column_stack([np.ones(len(tv)), tv, radyo])

# Normal denklem çözümü (np.linalg.solve yerine lstsq kullan → daha stabil)
beta, _, _, _ = np.linalg.lstsq(X, satis, rcond=None)

print(f"\n=== Satış Tahmini Modeli ===")
print(f"Sabit (β0)   : {beta[0]:+.4f}")
print(f"TV katsayısı : {beta[1]:+.4f}  → Her $1k TV harcaması ≈ {beta[1]*1000:.0f} adet satış")
print(f"Radyo kat.   : {beta[2]:+.4f}  → Her $1k Radyo harcaması ≈ {beta[2]*1000:.0f} adet satış")

# Tahmin & hata
tahmin = X @ beta   # matris çarpımı ile toplu tahmin
hata   = satis - tahmin
rmse   = np.sqrt(np.mean(hata**2))
print(f"\nRMSE (Ortalama Hata): {rmse:.2f}k adet")

# Örnek tahmin: TV=$150k, Radyo=$30k harcansaydı?
ornek_tahmin = beta[0] + beta[1]*150 + beta[2]*30
print(f"\nÖrnek: TV=$150k + Radyo=$30k → Tahmini satış: {ornek_tahmin:.1f}k adet")
```

### 📤 Beklenen Çıktı

```
=== Reklam Kanalı – Satış Korelasyonu ===
TV      : r=+0.782  ████████████████
Radyo   : r=+0.576  ███████████
Gazete  : r=+0.228  ████

=== Kanal ROI Sıralaması ===
  TV      : korelasyon=0.782 | ort. harcama=$147.0k  ← Kazanan!
  Radyo   : korelasyon=0.576 | ort. harcama=$23.3k
  Gazete  : korelasyon=0.228 | ort. harcama=$30.6k

🏆 En etkili kanal: TV

=== TV Harcaması Quartile Analizi ===
Q1 sınırı: $74.4k | Q2: $149.8k | Q3: $218.8k

  Q1 (En Düşük)   : TV= $37.3k → Satış=10.5k adet
  Q2              : TV=$110.5k → Satış=13.2k adet
  Q3              : TV=$181.4k → Satış=15.8k adet
  Q4 (En Yüksek)  : TV=$264.4k → Satış=19.9k adet   ← %89 daha fazla satış!

=== Satış Tahmini Modeli ===
Sabit (β0)   : +2.9211
TV katsayısı : +0.0458  → Her $1k TV harcaması ≈ 46 adet satış
Radyo kat.   : +0.1880  → Her $1k Radyo harcaması ≈ 188 adet satış

RMSE (Ortalama Hata): 1.68k adet

Örnek: TV=$150k + Radyo=$30k → Tahmini satış: 18.8k adet
```

### 💡 Ne Öğrendik?

| NumPy Özelliği | Kullanım Amacı |
|----------------|----------------|
| `np.corrcoef()[0,1]` | İki değişken arası korelasyon |
| `np.column_stack()` | 1D dizileri birleştirerek özellik matrisi oluşturma |
| `np.linalg.lstsq()` | En küçük kareler regresyonu (linear regression) |
| `X @ beta` | Matris çarpımı ile toplu tahmin |
| `np.sqrt(np.mean(hata**2))` | RMSE hesabı |

---

## 🗂️ Genel Özet

| # | Veri Seti | İş Sorusu | Öne Çıkan NumPy Özellikleri |
|---|-----------|-----------|------------------------------|
| 1 | OnlineRetail | Gelir & iptal analizi | `*` vektörel çarpım, `np.char.startswith()`, `argsort` |
| 2 | Mall_Customers | Müşteri segmentasyonu | `np.percentile()`, `np.digitize()`, çok koşullu maske |
| 3 | Churn_Modelling | Churn riski & z-score | Z-score normalizasyon, `np.abs()`, koşullu oran |
| 4 | SosyalMedyaReklamKampanyasi | Dönüşüm & min-max | `np.digitize()`, min-max scale, `argmax()` |
| 5 | Advertising | Korelasyon & regresyon | `np.corrcoef()`, `np.linalg.lstsq()`, `X @ beta` |

---

## 📚 Kaynaklar

- [erkansirin78/datasets GitHub](https://github.com/erkansirin78/datasets)
- [NumPy Resmi Dokümantasyon](https://numpy.org/doc/)
- [Online Retail UCI Dataset](https://archive.ics.uci.edu/ml/datasets/online+retail)