# 🐼 Pandas Pratik Soru-Cevap

> Tüm sorular [`erkansirin78/datasets`](https://github.com/erkansirin78/datasets) reposundaki gerçek veri setleri ile hazırlanmıştır.

---

## 📦 Kullanılan Veri Setleri

### 1. `Churn_Modelling.csv`
🔗 [GitHub'da Görüntüle](https://github.com/erkansirin78/datasets/blob/master/Churn_Modelling.csv)

Bir bankanın müşteri kaybı (churn) verisini içerir. Hangi müşterilerin bankadan ayrıldığını tahmin etmek için kullanılır.

| Alan | Tür | Açıklama |
|---|---|---|
| `RowNumber` | int | Satır numarası |
| `CustomerId` | int | Benzersiz müşteri kimliği |
| `Surname` | str | Müşteri soyadı |
| `CreditScore` | int | Kredi skoru (350–850) |
| `Geography` | str | Ülke: `France`, `Germany`, `Spain` |
| `Gender` | str | Cinsiyet: `Male`, `Female` |
| `Age` | int | Yaş |
| `Tenure` | int | Bankadaki hizmet süresi (yıl, 0–10) |
| `Balance` | float | Hesap bakiyesi ($) |
| `NumOfProducts` | int | Kullanılan ürün sayısı (1–4) |
| `HasCrCard` | int | Kredi kartı var mı? (0/1) |
| `IsActiveMember` | int | Aktif üye mi? (0/1) |
| `EstimatedSalary` | float | Tahmini maaş ($) |
| `Exited` | int | **Hedef değişken** — Bankadan ayrıldı mı? (0/1) |

- **Satır sayısı:** 10.000
- **Sütun sayısı:** 14
- **Eksik değer:** Yok
- **Boyut:** ~660 KB

---

### 2. `Advertising.csv`
🔗 [GitHub'da Görüntüle](https://github.com/erkansirin78/datasets/blob/master/Advertising.csv)

Farklı medya kanallarına yapılan reklam harcamalarının satışa etkisini gösteren klasik bir regresyon veri setidir.

| Alan | Tür | Açıklama |
|---|---|---|
| `ID` | int | Kampanya numarası |
| `TV` | float | TV reklam harcaması (bin $) |
| `Radio` | float | Radyo reklam harcaması (bin $) |
| `Newspaper` | float | Gazete reklam harcaması (bin $) |
| `Sales` | float | **Hedef değişken** — Satış miktarı (bin adet) |

- **Satır sayısı:** 200
- **Sütun sayısı:** 5
- **Eksik değer:** Yok
- **Boyut:** ~4.5 KB

---

### 3. `tips.csv`
🔗 [GitHub'da Görüntüle](https://github.com/erkansirin78/datasets/blob/master/tips.csv)

Bir restoranda ödenen toplam hesap ve bırakılan bahşişlere ait gözlem verisini içerir. Seaborn kütüphanesinin de dahili veri setidir.

| Alan | Tür | Açıklama |
|---|---|---|
| `total_bill` | float | Toplam hesap tutarı ($) |
| `tip` | float | Bırakılan bahşiş ($) |
| `sex` | str | Ödemeyi yapanın cinsiyeti: `Male`, `Female` |
| `smoker` | str | Sigara içen masa mı? `Yes`, `No` |
| `day` | str | Gün: `Sun`, `Sat`, `Thur`, `Fri` |
| `time` | str | Öğün: `Dinner`, `Lunch` |
| `size` | int | Masadaki kişi sayısı (1–6) |

- **Satır sayısı:** 244
- **Sütun sayısı:** 7
- **Eksik değer:** Yok
- **Boyut:** ~7.9 KB

---

### 4. `Mall_Customers.csv`
🔗 [GitHub'da Görüntüle](https://github.com/erkansirin78/datasets/blob/master/Mall_Customers.csv)

Bir alışveriş merkezine ait müşteri segmentasyon verisini içerir. Kümeleme (clustering) algoritmalarında sıklıkla kullanılır.

| Alan | Tür | Açıklama |
|---|---|---|
| `CustomerID` | int | Benzersiz müşteri kimliği (1–200) |
| `Gender` | str | Cinsiyet: `Male`, `Female` |
| `Age` | int | Yaş (18–70) |
| `AnnualIncome` | int | Yıllık gelir (bin $, 15k–137k) |
| `SpendingScore` | int | Harcama puanı (1–100, 100=en yüksek) |

- **Satır sayısı:** 200
- **Sütun sayısı:** 5
- **Eksik değer:** Yok
- **Boyut:** ~4.3 KB

---

### 5. `iris.csv`
🔗 [GitHub'da Görüntüle](https://github.com/erkansirin78/datasets/blob/master/iris.csv)

Botanik ölçümlerine dayalı, makine öğrenmesinin "merhaba dünya" veri setidir. 3 farklı iris çiçeği türünü içerir.

| Alan | Tür | Açıklama |
|---|---|---|
| `SepalLengthCm` | float | Çanak yaprak uzunluğu (cm) |
| `SepalWidthCm` | float | Çanak yaprak genişliği (cm) |
| `PetalLengthCm` | float | Taç yaprak uzunluğu (cm) |
| `PetalWidthCm` | float | Taç yaprak genişliği (cm) |
| `Species` | str | **Hedef değişken** — Tür: `Iris-setosa`, `Iris-versicolor`, `Iris-virginica` |

- **Satır sayısı:** 150 (her türden tam 50 kayıt)
- **Sütun sayısı:** 5
- **Eksik değer:** Yok
- **Boyut:** ~4.6 KB

---

## 🗂 Veri Setleri Özet Tablosu

| Veri Seti | Satır | Sütun | Konu | Zorluk |
|---|---|---|---|---|
| `Churn_Modelling.csv` | 10.000 | 14 | Banka müşteri kaybı | ⭐⭐⭐ |
| `Advertising.csv` | 200 | 5 | Reklam → Satış etkisi | ⭐ |
| `tips.csv` | 244 | 7 | Restoran bahşişleri | ⭐⭐ |
| `Mall_Customers.csv` | 200 | 5 | AVM müşteri segmentasyonu | ⭐ |
| `iris.csv` | 150 | 5 | Çiçek sınıflandırması | ⭐ |

---

## Soru 1 — Banka Müşteri Verisi: Temel Keşif ve Filtreleme

> 📁 **Veri seti:** `Churn_Modelling.csv` · 10.000 satır · 14 sütun

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
# → (10000, 14)

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
| `.shape` | `(satır, sütun)` döner → bu veri setinde `(10000, 14)` |
| `.isnull().sum()` | Sütun başına eksik değer sayısını verir |
| `(koşul1) & (koşul2)` | İki koşulu aynı anda uygulamak için `&` kullanılır; Python'un `and` anahtar kelimesi burada hata verir |
| `.mean()` | Sayısal sütunun aritmetik ortalamasını hesaplar |

**Yorum:** `Geography` sütunu 3 değer alır (`France`, `Germany`, `Spain`). Almanya kayıtları toplam verinin yaklaşık 1/4'ünü oluşturur. Almanya'dan ayrılan müşterilerin yüksek bakiyeye sahip olması dikkat çekicidir — bu müşteri segmenti "değerli ama riskli" profil olarak öne çıkar.

---

## Soru 2 — Reklam Harcamaları: Yeni Sütun ve Gruplama

> 📁 **Veri seti:** `Advertising.csv` · 200 satır · 5 sütun  
> TV, Radio ve Newspaper harcamaları **bin $** cinsinden; Sales ise **bin adet** cinsinden ifade edilmektedir.

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
| `def` ile fonksiyon | Birden fazla koşul içerdiğinden `lambda` yerine ayrı fonksiyon daha okunabilirdir |
| `.groupby("Butce")["Sales"].mean()` | Butce değerine göre gruplar, her grup için Sales ortalamasını döndürür |

**Yorum:** 200 kampanya kaydında TV harcamasının satışlarla en güçlü ilişkide olduğu görülür (0–300+ bin $ aralığında). Yüksek bütçeli kampanyaların satışı gerçekten artırıp artırmadığı gruplama ile kolayca test edilebilir.

---

## Soru 3 — Restoran Bahşiş Verisi: Pivot Tablo ve Aykırı Değer

> 📁 **Veri seti:** `tips.csv` · 244 satır · 7 sütun  
> Veriler Cuma–Pazar akşam yemekleri ve Perşembe–Cuma öğle yemeklerinden toplanmıştır.

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
# Toplam 244 kayıt; total_bill ort ≈ 19.8$, tip ort ≈ 3.0$, masa büyüklüğü 1–6 kişi

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
| `pivot_table(values, index, columns, aggfunc)` | Excel'deki PivotTable'ın Pandas karşılığıdır |
| `.stack()` | Çok sütunlu tabloyu tek sütuna indirgeyerek `idxmax()` kullanmayı mümkün kılar |
| IQR yöntemi | `Q1 - 1.5×IQR` ile `Q3 + 1.5×IQR` dışında kalan değerler aykırı kabul edilir |

**Yorum:** `tips.csv` yalnızca 244 satır içerse de 4 farklı gün, 2 öğün ve 2 cinsiyet kombinasyonuyla zengin bir gruplama zemini sunar. IQR aykırı değer tespiti, özellikle küçük restoran verilerinde büyük masaların (5–6 kişi) hesaplarını ayırt etmede işe yarar.

---

## Soru 4 — AVM Müşteri Verisi: Birleştirme ve String İşlemi

> 📁 **Veri seti:** `Mall_Customers.csv` · 200 satır · 5 sütun  
> `SpendingScore` 1–100 arasındadır; 100 en yüksek harcama eğilimini temsil eder.  
> `AnnualIncome` bin $ cinsinden verilmiştir (ör: 15 → 15.000 $).

Aşağıdaki görevleri sırasıyla yapın:

1. `Mall_Customers.csv` dosyasını okuyun.
2. `Gender` sütunundaki `"Male"` ve `"Female"` değerlerini `str.replace()` ile Türkçeleştirin: `"Erkek"` ve `"Kadın"`.
3. Aşağıdaki kampanya tablosuyla `pd.merge()` kullanarak birleştirin (`left join`):

```python
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
# 200 müşteri, CustomerID: 1–200, Age: 18–70, AnnualIncome: 15k–137k$

# 2. Gender sütununu Türkçeleştir
df["Cinsiyet"] = df["Gender"].str.replace("Male", "Erkek").str.replace("Female", "Kadın")
print("Cinsiyet değerleri:", df["Cinsiyet"].unique())

# 3. Kampanya tablosu
kampanya = pd.DataFrame({
    "CustomerID": [1, 5, 10, 20, 50, 100],
    "Kampanya": ["Yaz İndirimi", "Hoş Geldin", "VIP", "Sadakat", "Flash Sale", "Gold Üye"]
})

# Left join: tüm 200 müşteri korunur, kampanyası olmayanlar NaN alır
birlesik = pd.merge(df, kampanya, on="CustomerID", how="left")
print("\nBirleşik veri (ilk 5):")
print(birlesik[["CustomerID", "Cinsiyet", "SpendingScore", "Kampanya"]].head())

# 4. Kampanyası olmayan müşteri sayısı
kampanyasiz = birlesik["Kampanya"].isnull().sum()
print(f"\nKampanyası olmayan müşteri sayısı: {kampanyasiz}")
# → 194 (200 müşteriden yalnızca 6'sı kampanya listesinde)

# 5. Kampanyası olan müşterilerin ort. harcama puanı
kampanyali = birlesik[birlesik["Kampanya"].notnull()]
print(f"Kampanyalı müşterilerin ort. SpendingScore: {kampanyali['SpendingScore'].mean():.1f}")
```

**Açıklamalar:**

| Satır | Ne yapıyor? |
|---|---|
| `.str.replace("eski", "yeni")` | Sütundaki tüm hücrelerde metni değiştirir; döngü yazmaya gerek yoktur |
| `.str.replace(...).str.replace(...)` | Zincirleme (chaining) ile birden fazla değişiklik tek satırda yapılabilir |
| `pd.merge(..., how="left")` | Sol tablonun tüm 200 satırını korur; sağda eşleşme yoksa `NaN` yazar |
| `.isnull().sum()` | Kaç satırın `NaN` olduğunu sayar — kampanyası olmayan müşterileri bulmak için kullanılır |
| `.notnull()` | `NaN` olmayanları filtreler |

**Yorum:** 200 müşteriden yalnızca 6'sı kampanya tablosunda yer aldığı için `left join` sonucunda 194 müşterinin `Kampanya` sütunu `NaN` olacaktır. Bu, gerçek CRM senaryolarında çok yaygın bir durumdur.

---

## Soru 5 — Iris Veri Seti: GroupBy, Özellik Türetme ve Kayıt

> 📁 **Veri seti:** `iris.csv` · 150 satır · 5 sütun  
> Her 3 türden (`Iris-setosa`, `Iris-versicolor`, `Iris-virginica`) tam olarak **50 kayıt** bulunmaktadır.  
> Tüm ölçümler santimetre (cm) cinsindendir.

Aşağıdaki görevleri sırasıyla yapın:

1. `iris.csv` dosyasını okuyun ve kaç farklı tür (`Species`) içerdiğini bulun.
2. Tür bazında `SepalLengthCm` ve `PetalLengthCm` sütunlarının **ortalama, min ve max** değerlerini tek bir `groupby + agg` işlemiyle hesaplayın.
3. Her çiçeğin `SepalLengthCm / SepalWidthCm` oranını hesaplayıp `SepalOran` adında yeni bir sütun olarak ekleyin.
4. `SepalOran` değeri **2.0'dan büyük** olan çiçekleri filtreleyin.
5. Bu filtrelenmiş veriyi `iris_genis_tac.csv` adıyla kaydedin ve kaydedilen dosyayı geri okuyarak kaç satır içerdiğini doğrulayın.

---

### ✅ Cevap 5

```python
import pandas as pd

# 1. Veriyi oku, tür sayısını bul
df = pd.read_csv("iris.csv")
print("Benzersiz türler:", df["Species"].unique())
# → ['Iris-setosa', 'Iris-versicolor', 'Iris-virginica']
print("Tür sayısı:", df["Species"].nunique())
# → 3 (her türden tam 50 kayıt, toplam 150 satır)

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
# Iris-setosa'nın geniş çanak yaprakları nedeniyle bu filtreye takılmayacağı beklenir

# 5. Kaydet ve doğrula
genis_tac.to_csv("iris_genis_tac.csv", index=False)
print("\n✅ Dosya kaydedildi: iris_genis_tac.csv")

dogrulama = pd.read_csv("iris_genis_tac.csv")
print(f"Kaydedilen dosyadaki satır sayısı: {len(dogrulama)}")
```

**Açıklamalar:**

| Satır | Ne yapıyor? |
|---|---|
| `.nunique()` | Sütundaki benzersiz değer sayısını verir → bu veri setinde `3` |
| `groupby().agg(ad=(sütun, fonksiyon))` | Gruplama ve çoklu istatistiği tek seferde hesaplar; sonuç sütunlarına özel isim verilir |
| `df["A"] / df["B"]` | İki sütunu eleman bazında böler; döngü gerekmez |
| `to_csv("dosya.csv", index=False)` | `index=False` yazılmazsa Pandas satır numaralarını ekstra sütun olarak kaydeder |
| Kayıt + geri okuma | Dosyanın doğru kaydedildiğini doğrulamak için iyi bir alışkanlıktır |

**Yorum:** `Iris-setosa` türü kısa ama geniş çanak yapraklara sahipken `Iris-virginica` daha uzun ve dar çanak yapraklara sahiptir. Bu nedenle `SepalOran > 2.0` filtresi ağırlıklı olarak `versicolor` ve `virginica` türlerini seçer. 150 kayıt küçük görünse de tür dağılımı mükemmel dengelenmiştir — grupby sonuçlarını karşılaştırmak için idealdir.