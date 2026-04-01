# 🐍 NumPy – Gerçek Hayat ve Yazılım Geliştirme Süreçlerinden 5 Soru & Cevap

> Bu döküman, NumPy kütüphanesini gerçek hayat ve yazılım geliştirme senaryolarıyla pekiştirmek için hazırlanmıştır.  
> Her soru; senaryo, adım adım açıklamalı kod, beklenen çıktı ve özet tablosu içerir.

---

## 📋 İçindekiler

- [Soru 1 – Market Sepeti Analizi](#soru-1--market-sepeti-analizi)
- [Soru 2 – Yazılım Ekibi Performans Takibi](#soru-2--yazılım-ekibi-performans-takibi)
- [Soru 3 – Sunucu Sıcaklık İzleme Sistemi](#soru-3--sunucu-sıcaklık-i̇zleme-sistemi)
- [Soru 4 – A/B Test Sonuçlarını Analiz Etme](#soru-4--ab-test-sonuçlarını-analiz-etme)
- [Soru 5 – Öğrenci Not Sistemi ve Harf Notu Dönüşümü](#soru-5--öğrenci-not-sistemi-ve-harf-notu-dönüşümü)
- [Genel Özet Tablosu](#genel-özet-tablosu)

---

## Soru 1 – 🛒 Market Sepeti Analizi

### 📌 Senaryo

Bir market uygulaması geliştiriyorsunuz. Müşterinin sepetinde şu ürünler var:

| Ürün    | Fiyat (TL) | Adet |
|---------|-----------|------|
| Süt     | 35        | 2    |
| Ekmek   | 10        | 3    |
| Yumurta | 45        | 1    |
| Peynir  | 80        | 1    |
| Su      | 8         | 4    |

### ❓ Görevler

1. Her ürünün toplam tutarını (fiyat × adet) hesaplayın.
2. Sepet toplamını bulun.
3. 30 TL ve üzeri toplam tutarlı ürünleri filtreleyin.
4. Tüm ürünlere **%10 indirim** uygulayın, yeni sepet toplamını hesaplayın.

### ✅ Cevap

```python
import numpy as np

# Ürün fiyatları ve adetleri iki ayrı vektörde tutulur
fiyatlar = np.array([35, 10, 45, 80, 8])   # Her ürünün birim fiyatı
adetler  = np.array([2,  3,  1,  1,  4])   # Her ürünün adedi

# ── ADIM 1: Her ürünün toplam tutarı ──────────────────────────────────────
# Vektörel çarpım: aynı indeksteki elemanlar çarpılır, döngüye gerek yok
tutarlar = fiyatlar * adetler
print("Her ürünün toplam tutarı (TL):", tutarlar)

# ── ADIM 2: Sepet toplamı ─────────────────────────────────────────────────
sepet_toplam = tutarlar.sum()
print("Sepet toplamı:", sepet_toplam, "TL")

# ── ADIM 3: 30 TL ve üzeri tutarlı ürünler (Boolean Maskeleme) ────────────
# Her tutarı 30 ile karşılaştırıyoruz → True/False dizisi oluşur
maske = tutarlar >= 30
print("Pahalı ürünlerin tutarları:", tutarlar[maske])

# ── ADIM 4: %10 indirim uygula ────────────────────────────────────────────
# Her elemandan %10 düşürmek için 0.90 ile çarpmak yeterli
indirimli_tutarlar = tutarlar * 0.90
print("İndirimli tutarlar:", indirimli_tutarlar)

indirimli_toplam = indirimli_tutarlar.sum()
print("İndirimli sepet toplamı:", indirimli_toplam, "TL")
```

### 📤 Beklenen Çıktı

```
Her ürünün toplam tutarı (TL): [70 30 45 80 32]
Sepet toplamı: 257 TL
Pahalı ürünlerin tutarları: [70 30 45 80 32]
İndirimli tutarlar: [63.  27.  40.5 72.  28.8]
İndirimli sepet toplamı: 231.3 TL
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik   | Açıklama                                        |
|----------------------|-------------------------------------------------|
| `fiyatlar * adetler` | Vektörel çarpım, iki dizi eleman eleman çarpıldı |
| `.sum()`             | Tüm elemanların toplamı                         |
| `tutarlar >= 30`     | Boolean maske oluşturdu                         |
| `tutarlar[maske]`    | Sadece koşulu sağlayanları getirdi              |
| `tutarlar * 0.90`    | Tüm elemanlara aynı anda indirim uygulandı      |

---

## Soru 2 – 👩‍💻 Yazılım Ekibi Performans Takibi

### 📌 Senaryo

Bir yazılım şirketinde 4 geliştirici 3 sprint boyunca görev tamamladı:

| Geliştirici | Sprint 1 | Sprint 2 | Sprint 3 |
|-------------|---------|---------|---------|
| Ali         | 8       | 10      | 7       |
| Ayşe        | 12      | 9       | 11      |
| Mehmet      | 6       | 8       | 9       |
| Zeynep      | 10      | 12      | 14      |

### ❓ Görevler

1. Her geliştiricinin toplam ve ortalama görev sayısını bulun.
2. Her sprintteki takım toplamını bulun.
3. En çok görevi kim tamamladı?
4. En verimli sprint hangisiydi?

### ✅ Cevap

```python
import numpy as np

# 2D matris: satırlar = geliştiriciler, sütunlar = sprintler → shape (4, 3)
performans = np.array([
    [8,  10,  7],   # Ali
    [12,  9, 11],   # Ayşe
    [6,   8,  9],   # Mehmet
    [10, 12, 14]    # Zeynep
])

gelistiriciler = ["Ali", "Ayşe", "Mehmet", "Zeynep"]
sprintler      = ["Sprint 1", "Sprint 2", "Sprint 3"]

# ── ADIM 1: Her geliştiricinin toplamı ve ortalaması ──────────────────────
# axis=1 → satır boyunca işlem yap (her satırı kendi içinde topla)
kisi_toplam   = performans.sum(axis=1)
kisi_ortalama = performans.mean(axis=1)

print("=== Geliştirici Bazlı ===")
for i, isim in enumerate(gelistiriciler):
    print(f"{isim:8}: Toplam={kisi_toplam[i]}, Ortalama={kisi_ortalama[i]:.1f}")

# ── ADIM 2: Sprint bazlı takım toplamları ────────────────────────────────
# axis=0 → sütun boyunca işlem yap (her sütunu kendi içinde topla)
sprint_toplam = performans.sum(axis=0)

print("\n=== Sprint Bazlı Takım Toplamları ===")
for i, sprint in enumerate(sprintler):
    print(f"{sprint}: {sprint_toplam[i]} görev")

# ── ADIM 3: En çok görevi kim tamamladı? ─────────────────────────────────
# argmax() → en büyük değerin indeksini verir
en_cok_index = kisi_toplam.argmax()
print(f"\nEn verimli geliştirici : {gelistiriciler[en_cok_index]}")
print(f"Toplam görev           : {kisi_toplam[en_cok_index]}")

# ── ADIM 4: En verimli sprint ─────────────────────────────────────────────
en_verimli_sprint_index = sprint_toplam.argmax()
print(f"\nEn verimli sprint         : {sprintler[en_verimli_sprint_index]}")
print(f"Toplam tamamlanan görev   : {sprint_toplam[en_verimli_sprint_index]}")
```

### 📤 Beklenen Çıktı

```
=== Geliştirici Bazlı ===
Ali     : Toplam=25, Ortalama=8.3
Ayşe    : Toplam=32, Ortalama=10.7
Mehmet  : Toplam=23, Ortalama=7.7
Zeynep  : Toplam=36, Ortalama=12.0

=== Sprint Bazlı Takım Toplamları ===
Sprint 1: 36 görev
Sprint 2: 39 görev
Sprint 3: 41 görev

En verimli geliştirici : Zeynep
Toplam görev           : 36

En verimli sprint         : Sprint 3
Toplam tamamlanan görev   : 41
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik    | Açıklama                                           |
|-----------------------|----------------------------------------------------|
| `np.array([[...]])`   | 2D matris oluşturuldu                              |
| `.sum(axis=1)`        | Her satırı kendi içinde topladı (kişi bazlı)       |
| `.sum(axis=0)`        | Her sütunu kendi içinde topladı (sprint bazlı)     |
| `.argmax()`           | En büyük değerin indeksini döndürdü                |
| `.mean(axis=1)`       | Her satırın ortalamasını aldı                      |

---

## Soru 3 – 🌡️ Sunucu Sıcaklık İzleme Sistemi

### 📌 Senaryo

Bir veri merkezinde 5 sunucunun 7 günlük sıcaklık değerleri (°C):

| Sunucu   | Pzt | Sal | Çar | Per | Cum | Cmt | Paz |
|----------|-----|-----|-----|-----|-----|-----|-----|
| Sunucu 1 | 65  | 67  | 70  | 68  | 72  | 66  | 64  |
| Sunucu 2 | 55  | 58  | 60  | 57  | 61  | 59  | 56  |
| Sunucu 3 | 78  | 80  | 85  | 82  | 88  | 79  | 77  |
| Sunucu 4 | 60  | 62  | 65  | 63  | 66  | 61  | 59  |
| Sunucu 5 | 70  | 73  | 75  | 72  | 76  | 71  | 69  |

### ❓ Görevler

1. Her sunucunun haftalık ortalama sıcaklığını bulun.
2. 75°C üzeri sıcaklıkları **"tehlikeli"** olarak işaretleyin (kaç tane var?).
3. En sıcak sunucuyu ve en sıcak günü bulun.
4. Tüm sunuculardaki günlük ortalama sıcaklığı hesaplayın.

### ✅ Cevap

```python
import numpy as np

# 5 sunucu, 7 günlük sıcaklık verisi → shape: (5, 7)
sicakliklar = np.array([
    [65, 67, 70, 68, 72, 66, 64],  # Sunucu 1
    [55, 58, 60, 57, 61, 59, 56],  # Sunucu 2
    [78, 80, 85, 82, 88, 79, 77],  # Sunucu 3
    [60, 62, 65, 63, 66, 61, 59],  # Sunucu 4
    [70, 73, 75, 72, 76, 71, 69]   # Sunucu 5
])

gunler    = ["Pzt", "Sal", "Çar", "Per", "Cum", "Cmt", "Paz"]
sunucular = ["Sunucu 1", "Sunucu 2", "Sunucu 3", "Sunucu 4", "Sunucu 5"]

# ── ADIM 1: Her sunucunun haftalık ortalaması ─────────────────────────────
# axis=1 → her satırın (sunucunun) ortalamasını al
sunucu_ort = sicakliklar.mean(axis=1)
print("=== Haftalık Ortalama Sıcaklıklar ===")
for i, sunucu in enumerate(sunucular):
    print(f"{sunucu}: {sunucu_ort[i]:.1f} °C")

# ── ADIM 2: 75°C üzeri tehlikeli sıcaklıklar ─────────────────────────────
# Boolean maske → True olan yerleri say
tehlikeli_maske = sicakliklar > 75
print(f"\nTehlikeli ölçüm sayısı : {tehlikeli_maske.sum()}")
print("Tehlikeli sıcaklıklar  :", sicakliklar[tehlikeli_maske])

# ── ADIM 3: En sıcak sunucu ve en sıcak gün ──────────────────────────────
sunucu_max = sicakliklar.max(axis=1)
en_sicak_sunucu_idx = sunucu_max.argmax()
print(f"\nEn sıcak sunucu  : {sunucular[en_sicak_sunucu_idx]}")
print(f"Maksimum sıcaklık: {sunucu_max[en_sicak_sunucu_idx]} °C")

gun_max = sicakliklar.max(axis=0)
en_sicak_gun_idx = gun_max.argmax()
print(f"\nEn sıcak gün              : {gunler[en_sicak_gun_idx]}")
print(f"O günkü en yüksek sıcaklık: {gun_max[en_sicak_gun_idx]} °C")

# ── ADIM 4: Günlük ortalama (tüm sunucuların ortalaması) ─────────────────
# axis=0 → her sütunun (günün) ortalamasını al
gunluk_ort = sicakliklar.mean(axis=0)
print("\n=== Günlük Ortalama Sıcaklıklar ===")
for i, gun in enumerate(gunler):
    print(f"{gun}: {gunluk_ort[i]:.1f} °C")
```

### 📤 Beklenen Çıktı

```
=== Haftalık Ortalama Sıcaklıklar ===
Sunucu 1: 67.4 °C
Sunucu 2: 58.0 °C
Sunucu 3: 81.3 °C
Sunucu 4: 62.3 °C
Sunucu 5: 72.3 °C

Tehlikeli ��lçüm sayısı : 7
Tehlikeli sıcaklıklar  : [78 80 85 82 88 79 77]

En sıcak sunucu  : Sunucu 3
Maksimum sıcaklık: 88 °C

En sıcak gün              : Cum
O günkü en yüksek sıcaklık: 88 °C
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik       | Açıklama                                        |
|--------------------------|-------------------------------------------------|
| `sicakliklar > 75`       | Her eleman için koşul kontrolü yapıldı          |
| `tehlikeli_maske.sum()`  | True değerleri sayıldı (True=1, False=0)        |
| `.max(axis=1)`           | Her satırın (sunucunun) en büyüğü               |
| `.max(axis=0)`           | Her sütunun (günün) en büyüğü                   |

---

## Soru 4 – 📊 A/B Test Sonuçlarını Analiz Etme

### 📌 Senaryo

Bir e-ticaret sitesinde iki farklı buton rengi test edildi.  
10 günlük tıklanma oranları (%):

| Grup         | G1  | G2  | G3  | G4  | G5  | G6  | G7  | G8  | G9  | G10 |
|--------------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| A (Mavi)     | 3.2 | 3.5 | 3.1 | 3.8 | 3.6 | 3.3 | 3.7 | 3.4 | 3.9 | 3.2 |
| B (Kırmızı)  | 3.8 | 4.1 | 3.9 | 4.3 | 4.0 | 3.7 | 4.2 | 3.8 | 4.5 | 4.1 |

### ❓ Görevler

1. Her grubun ortalamasını, standart sapmasını ve maksimumunu bulun.
2. B grubunun A grubuna göre her gün kaç puan daha iyi olduğunu hesaplayın.
3. Hangi günlerde B grubu **%0.5'ten fazla** fark attı?
4. İki grubun ortalama farkını **yüzde olarak** hesaplayın.

### ✅ Cevap

```python
import numpy as np

# İki farklı test grubunun günlük tıklanma oranları (%)
A = np.array([3.2, 3.5, 3.1, 3.8, 3.6, 3.3, 3.7, 3.4, 3.9, 3.2])
B = np.array([3.8, 4.1, 3.9, 4.3, 4.0, 3.7, 4.2, 3.8, 4.5, 4.1])

gunler = [f"Gün {i+1}" for i in range(10)]

# ── ADIM 1: Her grubun istatistikleri ────────────────────────────────────
print("=== Grup İstatistikleri ===")
for isim, grup in [("A (Mavi)", A), ("B (Kırmızı)", B)]:
    print(f"\n{isim}:")
    print(f"  Ortalama       : {grup.mean():.2f}%")
    # std() → standart sapma: verinin ortalamadan ne kadar saptığını gösterir
    print(f"  Standart Sapma : {grup.std():.3f}")
    print(f"  Maksimum       : {grup.max():.1f}%")
    print(f"  Minimum        : {grup.min():.1f}%")

# ── ADIM 2: Günlük fark (B - A) ──────────────────────────────────────────
# Vektörel çıkarma: aynı indeksteki elemanlar çıkarılır
fark = B - A
print("\n=== Günlük Farklar (B - A) ===")
for i, gun in enumerate(gunler):
    print(f"{gun}: +{fark[i]:.1f} puan")

# ── ADIM 3: B'nin 0.5 puandan fazla öne çıktığı günler ───────────────────
buyuk_fark_maske = fark > 0.5
print(f"\nB'nin 0.5'ten fazla öne geçtiği gün sayısı: {buyuk_fark_maske.sum()}")
print("O günler:")
# np.where() → True olan indeksleri döndürür
for idx in np.where(buyuk_fark_maske)[0]:
    print(f"  {gunler[idx]}: fark = {fark[idx]:.1f} puan")

# ── ADIM 4: Ortalama yüzde fark ──────────────────────────────────────────
yuzde_fark = ((B.mean() - A.mean()) / A.mean()) * 100
print(f"\nB grubu, A grubuna göre ortalamada %{yuzde_fark:.1f} daha iyi performans gösterdi.")
```

### 📤 Beklenen Çıktı

```
=== Grup İstatistikleri ===

A (Mavi):
  Ortalama       : 3.47%
  Standart Sapma : 0.252
  Maksimum       : 3.90%
  Minimum        : 3.10%

B (Kırmızı):
  Ortalama       : 4.04%
  Standart Sapma : 0.228
  Maksimum       : 4.50%
  Minimum        : 3.70%

=== Günlük Farklar (B - A) ===
Gün 1 : +0.6 puan
Gün 2 : +0.6 puan
...

B'nin 0.5'ten fazla öne geçtiği gün sayısı: 7

B grubu, A grubuna göre ortalamada %16.4 daha iyi performans gösterdi.
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik     | Açıklama                                     |
|------------------------|----------------------------------------------|
| `.std()`               | Standart sapma hesaplandı                    |
| `B - A`                | İki vektörün eleman bazlı farkı              |
| `np.where(maske)[0]`   | Koşulu sağlayan indeksler bulundu            |
| Yüzde hesabı           | Skaler işlem tüm diziye uygulandı            |

---

## Soru 5 – 🎓 Öğrenci Not Sistemi ve Harf Notu Dönüşümü

### 📌 Senaryo

6 öğrencinin 4 sınavdaki puanları ve sınav ağırlıkları:

| Sınav  | Ağırlık |
|--------|---------|
| Vize 1 | %20     |
| Vize 2 | %25     |
| Proje  | %25     |
| Final  | %30     |

| Öğrenci | Vize 1 | Vize 2 | Proje | Final |
|---------|--------|--------|-------|-------|
| Ali     | 70     | 75     | 80    | 65    |
| Ayşe    | 90     | 85     | 92    | 88    |
| Mehmet  | 55     | 60     | 58    | 50    |
| Zeynep  | 80     | 78     | 85    | 90    |
| Fatma   | 65     | 70     | 72    | 68    |
| Can     | 45     | 50     | 48    | 40    |

**Harf notu skalası:** AA ≥ 85 | BA ≥ 75 | BB ≥ 65 | CB ≥ 55 | FF < 55

### ❓ Görevler

1. Her öğrencinin **ağırlıklı ortalama** notunu hesaplayın.
2. Notlara göre **harf notu** verin.
3. Dersi **geçenleri** (≥ 55) ve **kalanları** listeleyin.
4. Sınıf ortalamasını ve en yüksek notu bulun.

### ✅ Cevap

```python
import numpy as np

# Her satır bir öğrenci, her sütun bir sınav → shape: (6, 4)
notlar = np.array([
    [70, 75, 80, 65],   # Ali
    [90, 85, 92, 88],   # Ayşe
    [55, 60, 58, 50],   # Mehmet
    [80, 78, 85, 90],   # Zeynep
    [65, 70, 72, 68],   # Fatma
    [45, 50, 48, 40]    # Can
])

ogrenciler = ["Ali", "Ayşe", "Mehmet", "Zeynep", "Fatma", "Can"]

# Ağırlıklar (toplamları 1.0 olmalı: 0.20+0.25+0.25+0.30 = 1.0)
agirliklar = np.array([0.20, 0.25, 0.25, 0.30])

# ── ADIM 1: Ağırlıklı ortalama ────────────────────────────────────────────
# @ (matris çarpımı): shape (6,4) @ (4,) → (6,)
# Her öğrencinin notu ağırlıklarla çarpılıp toplanır
agirlikli_ort = notlar @ agirliklar

print("=== Ağırlıklı Ortalama Notlar ===")
for i, isim in enumerate(ogrenciler):
    print(f"{isim:8}: {agirlikli_ort[i]:.1f}")

# ── ADIM 2: Harf notu belirleme ───────────────────────────────────────────
# np.select: birden fazla koşulu sırayla kontrol eder
kosullar = [
    agirlikli_ort >= 85,
    agirlikli_ort >= 75,
    agirlikli_ort >= 65,
    agirlikli_ort >= 55
]
harf_listesi = ["AA", "BA", "BB", "CB"]

# np.select(koşullar, değerler, default= hiçbiri sağlanmazsa ne dönsün)
harf_notlari = np.select(kosullar, harf_listesi, default="FF")

print("\n=== Harf Notları ===")
for i, isim in enumerate(ogrenciler):
    print(f"{isim:8}: {agirlikli_ort[i]:.1f} → {harf_notlari[i]}")

# ── ADIM 3: Geçenler ve kalanlar ─────────────────────────────────────────
gecti_maske = agirlikli_ort >= 55

print(f"\n✅ Dersi geçenler ({gecti_maske.sum()} kişi):")
for i in np.where(gecti_maske)[0]:
    print(f"   {ogrenciler[i]} ({agirlikli_ort[i]:.1f})")

print(f"\n❌ Dersten kalanlar ({(~gecti_maske).sum()} kişi):")
# ~ operatörü Boolean maskeyi tersine çevirir
for i in np.where(~gecti_maske)[0]:
    print(f"   {ogrenciler[i]} ({agirlikli_ort[i]:.1f})")

# ── ADIM 4: Sınıf istatistikleri ─────────────────────────────────────────
print(f"\n📊 Sınıf Ortalaması : {agirlikli_ort.mean():.1f}")
print(f"🏆 En Yüksek Not   : {agirlikli_ort.max():.1f} ({ogrenciler[agirlikli_ort.argmax()]})")
print(f"📉 En Düşük Not    : {agirlikli_ort.min():.1f} ({ogrenciler[agirlikli_ort.argmin()]})")
```

### 📤 Beklenen Çıktı

```
=== Ağırlıklı Ortalama Notlar ===
Ali     : 72.8
Ayşe    : 88.8
Mehmet  : 56.3
Zeynep  : 83.9
Fatma   : 69.0
Can     : 45.8

=== Harf Notları ===
Ali     : 72.8 → BA
Ayşe    : 88.8 → AA
Mehmet  : 56.3 → CB
Zeynep  : 83.9 → BA
Fatma   : 69.0 → BB
Can     : 45.8 → FF

✅ Dersi geçenler (5 kişi):
   Ali    (72.8)
   Ayşe   (88.8)
   Mehmet (56.3)
   Zeynep (83.9)
   Fatma  (69.0)

❌ Dersten kalanlar (1 kişi):
   Can (45.8)

📊 Sınıf Ortalaması : 69.5
🏆 En Yüksek Not   : 88.8 (Ayşe)
📉 En Düşük Not    : 45.8 (Can)
```

### 💡 Ne Öğrendik?

| Kullanılan Özellik      | Açıklama                                           |
|-------------------------|----------------------------------------------------|
| `notlar @ agirliklar`   | Matris-vektör çarpımı ile ağırlıklı ortalama       |
| `np.select()`           | Çoklu koşul → birden fazla değer atama             |
| `~gecti_maske`          | Boolean maskeyi tersine çevirdi                    |
| `.argmin()`             | En küçük değerin indeksini verdi                   |

---

## 🗂️ Genel Özet Tablosu

| # | Soru | Konu | Kullanılan NumPy Özellikleri |
|---|------|------|------------------------------|
| 1 | Market Sepeti | Vektörel işlemler, filtreleme | `*`, `.sum()`, Boolean maske |
| 2 | Yazılım Ekibi | 2D matris, axis kullanımı | `.sum(axis)`, `.mean(axis)`, `.argmax()` |
| 3 | Sunucu Sıcaklık | Boolean maske sayma | `.sum()` üzerinde True sayma, `axis` |
| 4 | A/B Test | İstatistik, fark analizi | `.std()`, `np.where()`, vektör çıkarma |
| 5 | Not Sistemi | Matris çarpımı, çoklu koşul | `@` operatörü, `np.select()`, `~` |

---

## 📚 Kaynaklar

- [NumPy Resmi Dokümantasyon](https://numpy.org/doc/)
- [NumPy Yeni Başlayanlar Rehberi](https://numpy.org/doc/stable/user/absolute_beginners.html)
- [NumPy Cheat Sheet](https://numpy.org/doc/stable/user/quickstart.html)
