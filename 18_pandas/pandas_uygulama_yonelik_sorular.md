# 🐼 Pandas Pratik Soru-Cevap

> Tüm sorular `erkansirin78/datasets` reposundaki gerçek veri setleri ile hazırlanmıştır.

---

## Soru 1 — Banka Müşteri Verisi: Temel Keşif ve Filtreleme

> 📁 Veri seti: `Churn_Modelling.csv`

Aşağıdaki görevleri sırasıyla yapın:

1. `Churn_Modelling.csv` dosyasını okuyun, kaç satır ve sütun içerdiğini yazdırın.
2. Veri setinde **eksik değer** var mı? Sütun bazında kontrol edin.
3. **Almanya'da** yaşayan ve **bankadan ayrılmış** (`Exited == 1`) müşterileri filtreleyin.
4. Bu müşterilerin ortalama `CreditScore` ve ortalama `Balance` değerini hesaplayın.
5. Sonuçları yorumlayın.

---

### ✅ Cevap 1

```python
import pandas as pd

# 1. Veriyi oku ve boyutunu gör
df = pd.read_csv("Churn_Modelling.csv")
print("Satır x Sütun:", df.shape)

# 2. Eksik değer kontrolü
print("\nEksik değer sayıları:")
print(df.isnull().sum())
# → Tüm sütunlar 0 döner, veri seti temizdir

# 3. Almanya'da yaşayan ve ayrılmış müşterileri filtrele
alman_ayrilanlar = df[(df["Geography"] == "Germany") & (df["Exited"] == 1)]
print(f"\nAlmanya'da bankadan ayrılan müşteri sayısı: {len(alman_ayrilanlar)}")

# 4. Ortalama CreditScore ve Balance
print(f"Ortalama Kredi Skoru : {alman_ayrilanlar['CreditScore'].mean():.1f}")
print(f"Ortalama Bakiye      : {alman_ayrilanlar['Balance'].mean():,.2f} $")
```

**Açıklamalar:**

| Satır | Ne yapıyor? |
|---|---|
| `pd.read_csv(...)` | Dosyayı okuyup DataFrame oluşturur |
| `.shape` | `(satır, sütun)` döner |
| `.isnull().sum()` | Sütun başına eksik değer sayısını verir |
| `(koşul1) & (koşul2)` | İki koşulu aynı anda uygulamak için `&` kullanılır; `and` yazmak hata verir |
| `.mean()` | Sayısal sütunun ortalamasını hesaplar |

**Yorum:** Almanya'dan ayrılan müşterilerin kredi skoru ve bakiyesini görmek, hangi profildeki müşterilerin riski yüksek olduğunu anlamaya yardımcı olur. Bu, bankacılıkta *churn tahmini* için kritik bir ilk adımdır.

---

## Soru 2 — Reklam Harcamaları: Yeni Sütun ve Gruplama

> 📁 Veri seti: `Advertising.csv`

Aşağıdaki görevleri sırasıyla yapın:

1. `Advertising.csv` dosyasını okuyun ve ilk 5 satırı görüntüleyin.
2. `TV`, `Radio` ve `Newspaper` sütunlarını toplayarak her kampanya için `ToplamHarcama` adında yeni bir sütun oluşturun.
3. `ToplamHarcama` değerine göre her kampanyayı `"Düşük"` (< 100), `"Orta"` (100–300), `"Yüksek"` (> 300) olarak etiketleyin ve `Butce` adında yeni bir sütuna kaydedin.
4. `Butce` kategorisine göre gruplama yaparak her grubun **ortalama satış** (`Sales`) değerini hesaplayın.

---

### ✅ Cevap 2

```python
import pandas as pd

# 1. Veriyi oku
df = pd.read_csv("Advertising.csv")
print(df.head())

# 2. Toplam harcama sütunu oluştur
df["ToplamHarcama"] = df["TV"] + df["Radio"] + df["Newspaper"]

# 3. Bütçe kategorisi ekle
def butce_kategori(toplam):
    if toplam < 100:
        return "Düşük"
    elif toplam <= 300:
        return "Orta"
    else:
        return "Yüksek"

df["Butce"] = df["ToplamHarcama"].apply(butce_kategori)

print("\nYeni sütunlar eklendi (ilk 5 satır):")
print(df[["TV", "Radio", "Newspaper", "ToplamHarcama", "Butce", "Sales"]].head())

# 4. Bütçe kategorisine göre ortalama satış
print("\nKategoriye göre ortalama satış:")
print(df.groupby("Butce")["Sales"].mean().round(2))
```

**Açıklamalar:**

| Satır | Ne yapıyor? |
|---|---|
| `df["A"] + df["B"] + df["C"]` | Sütunları satır satır toplar; döngüye gerek yoktur |
| `.apply(fonksiyon)` | Her hücreye verilen fonksiyonu uygular |
| `def` ile tanımlı fonksiyon | Birden fazla koşul içerdiğinden `lambda` yerine ayrı fonksiyon daha okunabilirdir |
| `.groupby("Butce")["Sales"].mean()` | Butce değerine göre gruplar, her grup için Sales ortalamasını alır |

**Yorum:** Yüksek bütçeli kampanyaların ortalama satışı gerçekten daha mı yüksek? Gruplama bunu tek satırda gösterir.

---

## Soru 3 — Restoran Bahşiş Verisi: Pivot Tablo ve Özet İstatistik

> 📁 Veri seti: `tips.csv`

Aşağıdaki görevleri sırasıyla yapın:

1. `tips.csv` dosyasını okuyun ve sayısal sütunların özet istatistiklerini (`describe`) görüntüleyin.
2. Gün (`day`) ve cinsiyet (`sex`) bazında ortalama bahşiş miktarını gösteren bir **pivot tablo** oluşturun.
3. Pivot tabloya bakarak en yüksek ortalama bahşişin hangi gün ve cinsiyette verildiğini bulun.
4. `total_bill` sütunu için **IQR yöntemiyle** aykırı değerleri tespit edin ve kaç adet olduğunu yazdırın.

---

### ✅ Cevap 3

```python
import pandas as pd

# 1. Veriyi oku, özet istatistikler
df = pd.read_csv("tips.csv")
print("=== Özet İstatistikler ===")
print(df.describe().round(2))

# 2. Pivot tablo: gün x cinsiyet bazında ortalama bahşiş
pivot = df.pivot_table(
    values="tip",
    index="day",
    columns="sex",
    aggfunc="mean"
).round(2)
print("\n=== Pivot Tablo: Ort. Bahşiş (Gün x Cinsiyet) ===")
print(pivot)

# 3. En yüksek kombinasyonu bul
max_deger = pivot.stack().idxmax()
print(f"\nEn yüksek ortalama bahşiş: Gün={max_deger[0]}, Cinsiyet={max_deger[1]}")

# 4. IQR yöntemi ile aykırı değer tespiti
Q1 = df["total_bill"].quantile(0.25)
Q3 = df["total_bill"].quantile(0.75)
IQR = Q3 - Q1
alt = Q1 - 1.5 * IQR
ust = Q3 + 1.5 * IQR

aykirilar = df[(df["total_bill"] < alt) | (df["total_bill"] > ust)]
print(f"\nIQR Sınırları: [{alt:.2f}, {ust:.2f}]")
print(f"Aykırı değer sayısı: {len(aykirilar)}")
print(aykirilar[["total_bill", "tip", "day"]])
```

**Açıklamalar:**

| Satır | Ne yapıyor? |
|---|---|
| `.describe()` | count, mean, std, min, %25, %50, %75, max değerlerini tek seferde gösterir |
| `pivot_table(values, index, columns, aggfunc)` | Excel'deki PivotTable'ın karşılığıdır |
| `.stack()` | Çok sütunlu tabloyu tek sütuna indirgeyerek `idxmax()` kullanmayı mümkün kılar |
| IQR yöntemi | `Q1 - 1.5×IQR` ile `Q3 + 1.5×IQR` dışında kalan değerler aykırı kabul edilir |

**Yorum:** Pivot tablo, çok boyutlu karşılaştırmayı tek bakışta anlaşılır hale getirir. IQR aykırı değer tespiti, veri temizlemenin en yaygın kullanılan yöntemlerinden biridir.

---

## Soru 4 — Alışveriş Merkezi Müşterileri: Veri Birleştirme ve String İşlemi

> 📁 Veri seti: `Mall_Customers.csv`

Aşağıdaki görevleri sırasıyla yapın:

1. `Mall_Customers.csv` dosyasını okuyun.
2. `Gender` sütunundaki `"Male"` ve `"Female"` değerlerini `str.replace()` ile Türkçeleştirin: `"Erkek"` ve `"Kadın"`.
3. Aşağıdaki kampanya tablosuyla `pd.merge()` kullanarak birleştirin (`left join`):

```python
import pandas as pd

kampanya = pd.DataFrame({
    "CustomerID": [1, 5, 10, 20, 50, 100],
    "Kampanya": ["Yaz İndirimi", "Hoş Geldin", "VIP", "Sadakat", "Flash Sale", "Gold Üye"]
})
```

4. Kampanyası olmayan müşteri sayısını yazdırın.
5. Kampanyası olan müşterilerin ortalama `SpendingScore` değerini hesaplayın.

---

### ✅ Cevap 4

```python
import pandas as pd

# 1. Veriyi oku
df = pd.read_csv("Mall_Customers.csv")

# 2. Gender sütununu Türkçeleştir
df["Cinsiyet"] = df["Gender"].str.replace("Male", "Erkek").str.replace("Female", "Kadın")
print("Cinsiyet değerleri:", df["Cinsiyet"].unique())

# 3. Kampanya tablosu
kampanya = pd.DataFrame({
    "CustomerID": [1, 5, 10, 20, 50, 100],
    "Kampanya": ["Yaz İndirimi", "Hoş Geldin", "VIP", "Sadakat", "Flash Sale", "Gold Üye"]
})

# Left join: tüm müşteriler korunur, kampanyası olmayanlar NaN alır
birlesik = pd.merge(df, kampanya, on="CustomerID", how="left")
print("\nBirleşik veri (ilk 5):")
print(birlesik[["CustomerID", "Cinsiyet", "SpendingScore", "Kampanya"]].head())

# 4. Kampanyası olmayan müşteri sayısı
kampanyasiz = birlesik["Kampanya"].isnull().sum()
print(f"\nKampanyası olmayan müşteri sayısı: {kampanyasiz}")

# 5. Kampanyası olan müşterilerin ort. harcama puanı
kampanyali = birlesik[birlesik["Kampanya"].notnull()]
print(f"Kampanyalı müşterilerin ort. SpendingScore: {kampanyali['SpendingScore'].mean():.1f}")
```

**Açıklamalar:**

| Satır | Ne yapıyor? |
|---|---|
| `.str.replace("eski", "yeni")` | Sütundaki tüm hücrelerde metni değiştirir; döngü yazmaya gerek yoktur |
| `.str.replace(...).str.replace(...)` | Zincirleme (chaining) ile birden fazla değişiklik tek satırda yapılabilir |
| `pd.merge(..., how="left")` | Sol tablonun tüm satırlarını korur; sağda eşleşme yoksa `NaN` yazar |
| `.isnull().sum()` | Kaç satırın `NaN` olduğunu sayar — kampanyası olmayan müşterileri bulmak için kullanılır |
| `.notnull()` | `NaN` olmayanları filtreler |

**Yorum:** `left join`, ana tablonuzu kaybetmeden ek bilgi eklemenin en güvenli yoludur. Gerçek hayatta CRM, kampanya ve satış tablolarını bu şekilde birleştirirsiniz.

---

## Soru 5 — Iris Veri Seti: GroupBy, Yeni Sütun ve Dosyaya Kayıt

> 📁 Veri seti: `iris.csv`

Aşağıdaki görevleri sırasıyla yapın:

1. `iris.csv` dosyasını okuyun ve kaç farklı tür (`Species`) içerdiğini bulun.
2. Tür bazında `SepalLengthCm` ve `PetalLengthCm` sütunlarının **ortalama, min ve max** değerlerini tek bir `groupby + agg` işlemiyle hesaplayın.
3. Her çiçeğin `SepalLengthCm / SepalWidthCm` oranını hesaplayıp `SepalOran` adında yeni bir sütun olarak ekleyin.
4. `SepalOran` değeri **2.0'dan büyük** olan çiçekleri filtreleyin.
5. Bu filtrelenmiş veriyi `iris_genis_taç.csv` adıyla kaydedin ve kaydedilen dosyayı geri okuyarak kaç satır içerdiğini doğrulayın.

---

### ✅ Cevap 5

```python
import pandas as pd

# 1. Veriyi oku, tür sayısını bul
df = pd.read_csv("iris.csv")
print("Benzersiz türler:", df["Species"].unique())
print("Tür sayısı:", df["Species"].nunique())

# 2. Tür bazında çoklu istatistik
ozet = df.groupby("Species").agg(
    SL_Ort=("SepalLengthCm", "mean"),
    SL_Min=("SepalLengthCm", "min"),
    SL_Max=("SepalLengthCm", "max"),
    PL_Ort=("PetalLengthCm", "mean"),
    PL_Min=("PetalLengthCm", "min"),
    PL_Max=("PetalLengthCm", "max")
).round(2)
print("\n=== Tür Bazında Özet ===")
print(ozet)

# 3. Sepal oran sütunu ekle
df["SepalOran"] = (df["SepalLengthCm"] / df["SepalWidthCm"]).round(2)
print("\nSepalOran sütunu eklendi (ilk 5):")
print(df[["SepalLengthCm", "SepalWidthCm", "SepalOran", "Species"]].head())

# 4. Oranı 2.0'dan büyük olanları filtrele
genis_tac = df[df["SepalOran"] > 2.0]
print(f"\nSepalOran > 2.0 olan çiçek sayısı: {len(genis_tac)}")
print("Tür dağılımı:")
print(genis_tac["Species"].value_counts())

# 5. Kaydet ve doğrula
genis_tac.to_csv("iris_genis_tac.csv", index=False)
print("\n✅ Dosya kaydedildi: iris_genis_tac.csv")

dogrulama = pd.read_csv("iris_genis_tac.csv")
print(f"Kaydedilen dosyadaki satır sayısı: {len(dogrulama)}")
```

**Açıklamalar:**

| Satır | Ne yapıyor? |
|---|---|
| `.nunique()` | Sütundaki benzersiz değer sayısını verir |
| `groupby().agg(ad=(sütun, fonksiyon))` | Gruplama ve çoklu istatistiği tek seferde hesaplar; sonuç sütunlarına özel isim verilir |
| `df["A"] / df["B"]` | İki sütunu eleman bazında böler; döngü gerekmez |
| `to_csv("dosya.csv", index=False)` | `index=False` yazılmazsa Pandas satır numaralarını ekstra sütun olarak kaydeder |
| Kayıt + geri okuma | Dosyanın doğru kaydedildiğini kontrol etmek için iyi bir alışkanlıktır |

**Yorum:** `SepalOran > 2.0` koşulu daha "uzun ama ince" çanak yapraklı çiçekleri seçer. Iris veri seti, basit görünse de filtreleme, gruplama ve özellik türetme pratiği için mükemmel bir örnektir.