# 🤖 Python ile Makine Öğrenmesi — Gerçek Verilerle 5 Soru & Cevap

> **Kaynak:** [`erkansirin78/datasets`](https://github.com/erkansirin78/datasets)
> Tüm sorular **e-ticaret, finans ve banka** alanlarından gerçek veri setleriyle hazırlanmıştır.

---

## 📦 Kullanılan Veri Setleri

| # | Veri Seti | Satır | Alan | Konu |
|---|---|---|---|---|
| 1 | `Churn_Modelling.csv` | 10.000 | 14 | Banka müşteri kaybı tahmini |
| 2 | `Advertising.csv` | 200 | 5 | Reklam harcaması → Satış tahmini |
| 3 | `Mall_Customers.csv` | 200 | 5 | AVM müşteri segmentasyonu |

---

## ❓ Soru 1 — Logistic Regresyon ile Banka Müşteri Kaybı Tahmini

> 📁 **Veri seti:** `Churn_Modelling.csv` · 10.000 satır · 14 sütun  
> 🏦 **Alan:** Bankacılık / Finans  
> 📘 **Konu:** Sınıflandırma (Classification) → Logistic Regresyon

### 🎯 Problem Tanımı

Bir bankanın 10.000 müşteri kaydı var.
Her müşteri hakkında şu bilgiler biliniyor:
- Kredi skoru, yaş, bakiye, ülke, ürün sayısı, aktif üye mi vs.

**Soru:** Bu bilgilere bakarak bir müşterinin bankadan ayrılıp ayrılmayacağını (`Exited` = 1 mi, 0 mı?) tahmin eden bir model kur.

### 🧠 Hangi Kavramlar Kullanılıyor?

| Kavram | Açıklama |
|---|---|
| **Etiket (Label)** | `Exited` sütunu — tahmin etmek istediğimiz değer |
| **Özellikler (Features)** | `CreditScore`, `Age`, `Balance`, `NumOfProducts` vb. |
| **Eğitim / Test Verisi** | Veriyi %80 eğitim, %20 test olarak böleceğiz |
| **Logistic Regresyon** | İkili sınıflandırma için (Ayrıldı mı / Ayrılmadı mı?) |
| **Doğruluk (Accuracy)** | Modelin kaç tanesini doğru tahmin ettiği |

---

### ✅ Cevap 1

```python
# ── Kütüphaneleri yükle ──────────────────────────────────────────
import pandas as pd
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import accuracy_score, confusion_matrix

# ── 1. Veriyi oku ────────────────────────────────────────────────
df = pd.read_csv("Churn_Modelling.csv")

# İlk 5 satıra bakalım
print("Veri boyutu:", df.shape)
# → (10000, 14)
print(df[["CreditScore", "Age", "Balance", "Exited"]].head())

# ── 2. Özellikleri ve etiketi seç ───────────────────────────────
# Sayısal sütunları seçiyoruz (metin sütunlarını şimdilik atlıyoruz)
# CreditScore: 350–850 arası kredi notu
# Age: Müşterinin yaşı
# Tenure: Bankada kaç yıldır müşteri
# Balance: Hesap bakiyesi ($)
# NumOfProducts: Kaç ürün kullanıyor (1–4)
# IsActiveMember: Aktif mi? (0/1)
X = df[["CreditScore", "Age", "Tenure", "Balance",
        "NumOfProducts", "HasCrCard", "IsActiveMember", "EstimatedSalary"]]

y = df["Exited"]   # 0 = Kaldı, 1 = Bankadan ayrıldı

# 🔍 Logistic Regresyon — Satır Satır Açıklama

> Aşağıdaki her kod bloğu **tek tek** ele alınmış, ne yaptığı sade bir dille açıklanmıştır.

---

## 📦 ADIM 3 — Veriyi Eğitim ve Test Olarak Böl

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

### 🧩 Bu satır ne yapıyor?

Elimizdeki veriyi **iki parçaya** ayırır:

```
Tüm Veri (10.000 satır)
        │
        ├──── Eğitim Verisi (%80) → 8.000 satır  →  X_train, y_train
        │
        └──── Test Verisi   (%20) → 2.000 satır  →  X_test,  y_test
```

### 🔤 Her değişken ne?

| Değişken | Ne içeriyor? | Boyut |
|---|---|---|
| `X_train` | Modelin **öğreneceği** özellikler | 8.000 satır |
| `y_train` | `X_train`'e karşılık gelen doğru cevaplar (0 ya da 1) | 8.000 satır |
| `X_test` | Modelin **hiç görmediği** özellikler | 2.000 satır |
| `y_test` | `X_test`'in gerçek cevapları — modelin tahminini bununla karşılaştırırız | 2.000 satır |

### ⚙️ Parametreler ne anlama geliyor?

```python
test_size=0.2
# Verinin %20'si test için ayrılır.
# Geriye kalan %80'i eğitim için kullanılır.
# Küçük bir test seti → model çok az "sınava" girer
# Büyük bir test seti → model çok az öğrenir
# %80/%20 genel kabul görmüş dengeli bir orandır.

random_state=42
# Veriyi karıştırırken kullanılan "tohum" sayısıdır.
# 42 yazdığında her çalıştırmada aynı karıştırma yapılır.
# Yazmasan rastgele farklı böler → sonuçlar her seferinde değişir.
# 42 sayısının özel bir anlamı yok, yaygın bir gelenek :)
```

### 🏫 Gerçek Hayat Benzetmesi

> Bir öğretmen sınava hazırlık için öğrenciye 100 soru verir.
> 80 soruyu çalışmaya (eğitim), 20 soruyu sınava (test) ayırır.
> Sınav soruları öğrencinin daha önce görmediği sorulardır.
> Makine öğrenmesinde de model test verisini hiç görmeden tahmin eder.

---

```python
print(f"\nEğitim seti boyutu : {X_train.shape[0]} satır")
print(f"Test seti boyutu   : {X_test.shape[0]} satır")
```

### 🧩 Bu satır ne yapıyor?

Bölme işleminin doğru yapıldığını **ekranda doğrular**.

```
.shape[0]  →  kaç satır var?
.shape[1]  →  kaç sütun var?  (burada kullanılmadı)
```

**Beklenen çıktı:**
```
Eğitim seti boyutu : 8000 satır
Test seti boyutu   : 2000 satır
```

---

## 📦 ADIM 4 — Ölçeklendirme (Scaling)

```python
scaler = StandardScaler()
```

### 🧩 Bu satır ne yapıyor?

`StandardScaler` adında bir **ölçeklendirici nesne** oluşturur.
Henüz hiçbir şey yapmaz, sadece araç hazırlanır.

---

### 🤔 Neden Ölçeklendirme Gerekiyor?

Verimizdeki sütunlara bakalım:

| Sütun | Örnek Değer | Büyüklük |
|---|---|---|
| `Balance` | 150.000 | Çok büyük |
| `EstimatedSalary` | 85.000 | Büyük |
| `Age` | 35 | Orta |
| `Tenure` | 5 | Küçük |
| `HasCrCard` | 0 veya 1 | Çok küçük |

Model matematiksel hesaplama yaparken büyük sayılar küçükleri **ezer**.
Sanki `Balance` her şeyi tek başına belirliyor gibi davranır.
Ölçeklendirme tüm sütunları **eşit oyun alanına** getirir.

```
Ölçeklendirme Öncesi:   Balance=150.000   HasCrCard=1
                           dev bir fil    vs  küçük bir karınca

Ölçeklendirme Sonrası:  Balance=1.3       HasCrCard=-0.8
                           dengeli         vs  dengeli
```

---

```python
X_train = scaler.fit_transform(X_train)
```

### 🧩 Bu satır ne yapıyor?

İki işlemi birden yapar:

```
fit()         →  Eğitim verisinden ortalama ve standart sapma öğrenir
transform()   →  Bu bilgiyle eğitim verisini dönüştürür (ölçekler)
```

**`fit_transform()` bu ikisini tek seferde yapar.**

Matematiksel olarak her değere şunu uygular:

```
yeni_değer = (eski_değer - ortalama) / standart_sapma

Örnek:
  Age sütunu ortalaması = 38.9, std = 10.5
  Bir müşterinin yaşı = 45 ise:
  yeni_yaş = (45 - 38.9) / 10.5 = 0.58
```

Sonuç: Tüm değerler 0 civarında, -3 ile +3 arasında bir sayıya dönüşür.

### ⚠️ Kritik Kural

```python
# DOĞRU ✅ — fit_transform sadece EĞİTİM verisine uygulanır
X_train = scaler.fit_transform(X_train)

# YANLIŞ ❌ — Test verisine fit_transform ASLA uygulanmaz
# X_test = scaler.fit_transform(X_test)   ← BU HATALI!
```

**Neden?**
Test verisi gerçek hayatı simüle eder.
Gerçek hayatta yeni gelen bir müşterinin verisinin istatistiklerini bilmezsin.
Ölçeği yalnızca eğitim verisinden öğrenir, test verisine o ölçeği uygularsın.

---

```python
X_test = scaler.transform(X_test)
```

### 🧩 Bu satır ne yapıyor?

Test verisine **sadece dönüştürme** uygular.
Yeni bir `fit()` yapmaz — eğitim verisinden öğrenilen ortalama ve std kullanılır.

```
fit()       →  ❌ Yok (eğitim verisinden öğrenileni kullan)
transform() →  ✅ Var (test verisi aynı ölçekle dönüştürülür)
```

### 🏫 Gerçek Hayat Benzetmesi

> Bir terzi müşterisinin ölçüsünü alır (fit).
> Sonra aynı ölçüyle kumaşı keser (transform).
> Yeni bir müşteri geldiğinde eski ölçüyü kullanmaz,
> ama eski makineyi (scaler) kullanarak yeni kumaşı keser.

---

## 📦 ADIM 5 — Modeli Kur ve Eğit

```python
model = LogisticRegression(max_iter=200)
```

### 🧩 Bu satır ne yapıyor?

`LogisticRegression` algoritmasından bir **model nesnesi** oluşturur.

```python
max_iter=200
# Model içindeki matematiksel hesaplama 200 kez tekrar eder.
# Varsayılan değer 100'dür; büyük veri setlerinde yetmeyebilir.
# 200 yazmak modele "daha uzun çalış, daha iyi öğren" demektir.
# Çok düşük olursa: "ConvergenceWarning" hatası alırsın.
```

---

```python
model.fit(X_train, y_train)
```

### 🧩 Bu satır ne yapıyor?

Modeli **eğitir** — gerçek öğrenme burada gerçekleşir.

```
fit(X_train, y_train)
    │            │
    │            └── Doğru cevaplar (Exited: 0 veya 1)
    └── Özellikler (CreditScore, Age, Balance...)

Model bu ikisini karşılaştırarak şunu öğrenir:
  "Balance yüksek olan müşteri ayrılıyor mu?"
  "Yaşlı müşteri daha çok mu ayrılıyor?"
  "Aktif üye ayrılmıyor mu?"
```

Arka planda şunu hesaplar:

```
Her özellik için bir ağırlık (w) bulur:
  Exited = sigmoid(w1*CreditScore + w2*Age + w3*Balance + ...)
  
  Sigmoid fonksiyonu sonucu 0 ile 1 arasına sıkıştırır:
  0.0 → kesinlikle kalmış
  0.5 → kararsız
  1.0 → kesinlikle ayrılmış
```

### 🏫 Gerçek Hayat Benzetmesi

> Bir banka çalışanı 8.000 eski müşteri dosyasını inceler.
> "Ayrılan müşterilerin ortak özellikleri neydi?" diye sorar.
> Bunu öğrendikten sonra yeni müşterilere bakarak tahmin yapar.
> `fit()` de tam olarak bunu yapar — geçmiş veriden kalıp bulur.

---

## 📦 ADIM 6 — Tahmin Yap

```python
y_pred = model.predict(X_test)
```

### 🧩 Bu satır ne yapıyor?

Eğitilmiş modeli kullanarak **test verisi için tahmin üretir**.

```
X_test  →  [müşteri özellikleri, hiç görülmemiş]
              ↓
          model.predict()
              ↓
y_pred  →  [0, 1, 0, 0, 1, 1, 0, ...]
            Her satır için: 0=Kaldı, 1=Ayrıldı
```

**Arka planda ne oluyor?**

```
1. Model her müşteri için bir olasılık hesaplar:
     Müşteri 1 → %23 ayrılır
     Müşteri 2 → %78 ayrılır
     Müşteri 3 → %41 ayrılır

2. Olasılık >= 0.5 ise → 1 (Ayrılır)
   Olasılık <  0.5 ise → 0 (Kalır)

     %23 → 0 (Kalır)
     %78 → 1 (Ayrılır)
     %41 → 0 (Kalır)
```

> Eğer olasılık değerlerini görmek istersen:
> ```python
> y_proba = model.predict_proba(X_test)
> # [[0.77, 0.23],   ← %77 kalır, %23 ayrılır
> #  [0.22, 0.78],   ← %22 kalır, %78 ayrılır
> #  [0.59, 0.41]]   ← %59 kalır, %41 ayrılır
> ```

---

## 📦 ADIM 7 — Başarıyı Ölç

```python
acc = accuracy_score(y_test, y_pred)
print(f"\n✅ Model Doğruluğu: %{acc * 100:.1f}")
```

### 🧩 Bu satır ne yapıyor?

Modelin tahminlerini gerçek cevaplarla karşılaştırır ve **yüzde doğruluk** hesaplar.

```
accuracy_score(y_test, y_pred)
               │        │
               │        └── Modelin tahminleri
               └── Gerçek doğru cevaplar

Formül:
  Doğruluk = Doğru Tahminler / Toplam Tahmin

  2000 test örneğinden 1640 doğru tahmin yaptıysa:
  Doğruluk = 1640 / 2000 = 0.82 → %82
```

---

### Confusion Matrix (Karışıklık Matrisi)

```python
cm = confusion_matrix(y_test, y_pred)
print("\nKarışıklık Matrisi:")
print(cm)
```

### 🧩 Bu satır ne yapıyor?

Modelin **hangi tip hataları yaptığını** gösterir.
4 farklı tahmin türü vardır:

```
                    ┌─────────────────────────────────────┐
                    │        MODELİN TAHMİNİ              │
                    │   Kaldı (0)    │   Ayrıldı (1)       │
      ┌─────────────┼────────────────┼────────────────────┤
      │ Kaldı (0)   │   TN ✅        │   FP ❌             │
GERÇEK│─────────────┼────────────────┼────────────────────┤
      │ Ayrıldı (1) │   FN ❌        │   TP ✅             │
      └─────────────┴────────────────┴────────────────────┘
```

### 🔤 TN, FP, FN, TP Ne Demek?

| Kısaltma | Açık Adı | Ne anlama geliyor? |
|---|---|---|
| **TN** | True Negative (Doğru Negatif) | Gerçekten kaldı, model de "kalır" dedi ✅ |
| **FP** | False Positive (Yanlış Pozitif) | Gerçekte kaldı ama model "ayrılır" dedi ❌ |
| **FN** | False Negative (Yanlış Negatif) | Gerçekte ayrıldı ama model "kalır" dedi ❌ |
| **TP** | True Positive (Doğru Pozitif) | Gerçekten ayrıldı, model de "ayrılır" dedi ✅ |

### 🏦 Bankacılık Açısından Hangi Hata Daha Kötü?

```
FP (Yanlış Alarm):
  Müşteri ayrılmayacak ama model "ayrılır" dedi.
  Banka gereksiz yere müşteriyi aramak zorunda kaldı.
  → Küçük bir maliyet, kabul edilebilir.

FN (Kaçırılan Alarm):
  Müşteri ayrıldı ama model "kalır" dedi.
  Banka o müşteriyi tutmak için hiçbir şey yapmadı.
  → Büyük bir kayıp! Müşteri gitti, geri kazanmak zor.
```

> **Sonuç:** Bankacılıkta FN hatası FP hatasından çok daha maliyetlidir.
> Bu yüzden sadece `accuracy`'e değil, `Recall` ve `F1-Score`'a da bakılır.

### 🔢 Gerçek Sayılarla Örnek

```
Diyelim ki confusion matrix şöyle çıktı:

[[1550  57]    ← Gerçekte Kaldı    satırı
 [ 303 90]]    ← Gerçekte Ayrıldı  satırı

TN = 1550  → Model "Kaldı" dedi, gerçekten kaldı       ✅
FP =   57  → Model "Ayrıldı" dedi, ama kaldı           ❌
FN =  303  → Model "Kaldı" dedi, ama ayrıldı           ❌ (kötü!)
TP =   90  → Model "Ayrıldı" dedi, gerçekten ayrıldı   ✅

Toplam doğru  = TN + TP = 1550 + 90  = 1640
Toplam tahmin = 2000
Doğruluk      = 1640 / 2000 = %82
```

---

## 📋 Tüm Adımların Özet Akışı

```
┌─────────────────────────────────────────────────────────┐
│  ADIM 3: Veriyi böl                                     │
│  X, y  →  train_test_split  →  X_train, X_test         │
│                                  y_train, y_test         │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│  ADIM 4: Ölçeklendir                                    │
│  scaler.fit_transform(X_train)  →  büyük sayıları eşitle│
│  scaler.transform(X_test)       →  aynı ölçeği uygula  │
└──────────────────────┬──────────────────────────────────┘
                       │
┌─────────────���────────▼──────────────────────────────────┐
│  ADIM 5: Modeli eğit                                    │
│  model.fit(X_train, y_train)  →  kalıpları öğren       │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│  ADIM 6: Tahmin yap                                     │
│  model.predict(X_test)  →  y_pred  [0,1,0,1,...]       │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│  ADIM 7: Değerlendir                                    │
│  accuracy_score(y_test, y_pred)  →  %82                 │
│  confusion_matrix(y_test, y_pred)→  TN FP / FN TP      │
└─────────────────────────────────────────────────────────┘
```

---

## 💡 Hatırlatıcı — En Sık Yapılan Hatalar

| Hata | Açıklama |
|---|---|
| `fit_transform` test verisine uygulamak | Test verisi gerçek dünyayı simüle eder; ölçeği ondan öğrenemezsin |
| `random_state` kullanmamak | Her çalıştırmada farklı bölme → tekrarlanamaz deney |
| Sadece `accuracy`'e bakmak | Dengesiz veri setinde `accuracy` yanıltıcıdır; `confusion matrix` daha bilgilendiricidir |
| `max_iter` düşük bırakmak | Model yeterince öğrenemez, `ConvergenceWarning` alırsın |

# ── 8. Yeni bir müşteri tahmin et ───────────────────────────────
# Kredi Skoru: 600, Yaş: 40, Tenure: 5 yıl, Bakiye: 80.000$,
# 2 ürün, Kredi kartı var, Aktif üye değil, Maaş: 90.000$
yeni_musteri = [[600, 40, 5, 80000, 2, 1, 0, 90000]]
yeni_olcekli = scaler.transform(yeni_musteri)
tahmin = model.predict(yeni_olcekli)

print("\n🔮 Yeni müşteri tahmini:")
print("Bankadan ayrılır mı?", "EVET ⚠️" if tahmin[0] == 1 else "HAYIR ✅")
```

### 📌 Adım Adım Özet

```
1. Veriyi oku (10.000 banka müşterisi)
        ↓
2. Özellikleri seç (CreditScore, Age, Balance...)
        ↓
3. %80 Eğitim | %20 Test olarak böl
        ↓
4. StandardScaler ile ölçeklendir
        ↓
5. LogisticRegression modeli kur ve eğit (fit)
        ↓
6. Test verisiyle tahmin yap (predict)
        ↓
7. Accuracy ile başarıyı ölç
        ↓
8. Yeni müşteri için tahmin üret
```

### 💡 Neden Logistic Regresyon?

> Bir müşteri ya bankadan **ayrılır (1)** ya da **ayrılmaz (0)**.
> Bu ikili karar problemi için Logistic Regresyon idealdir.
> Tıpta "hasta mı / sağlıklı mı", bankacılıkta "ayrıldı mı / kaldı mı" gibi sorularda kullanılır.

---

## ❓ Soru 2 — Linear Regresyon ile Reklam Harcamasından Satış Tahmini

> 📁 **Veri seti:** `Advertising.csv` · 200 satır · 5 sütun  
> 🛒 **Alan:** E-Ticaret / Pazarlama  
> 📘 **Konu:** Regresyon → Linear Regresyon + Çoklu Regresyon + Ridge + Lasso karşılaştırması

### 🎯 Problem Tanımı

Bir e-ticaret şirketi TV, radyo ve gazeteye reklam bütçesi harcıyor.

| Sütun | Açıklama |
|---|---|
| `TV` | TV reklam harcaması (bin $) |
| `Radio` | Radyo reklam harcaması (bin $) |
| `Newspaper` | Gazete reklam harcaması (bin $) |
| `Sales` | Satış miktarı (bin adet) — **tahmin etmek istediğimiz** |

**Soru:** TV, radyo ve gazeteye harcanan bütçeye bakarak satış miktarını tahmin et.  
Hangi reklam kanalı satışa en çok katkı sağlıyor?  
Ridge ve Lasso modelleri sonucu değiştiriyor mu?

---

### ✅ Cevap 2

```python
# ── Kütüphaneleri yükle ──────────────────────────────────────────
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression, Ridge, Lasso
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score

# ── 1. Veriyi oku ────────────────────────────────────────────────
df = pd.read_csv("Advertising.csv")

print("Veri boyutu:", df.shape)   # (200, 5)
print(df.head())
#    ID     TV  Radio  Newspaper  Sales
# 0   1  230.1   37.8       69.2   22.1
# 1   2   44.5   39.3       45.1   10.4

print("\nİstatistikler:")
print(df[["TV", "Radio", "Newspaper", "Sales"]].describe().round(2))

# ── 2. Özellikleri ve hedefi belirle ────────────────────────────
X = df[["TV", "Radio", "Newspaper"]]  # 3 reklam kanalı = özellik
y = df["Sales"]                        # Tahmin etmek istediğimiz satış

# ── 3. Eğitim / test bölmesi ────────────────────────────────────
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# ── 4. Üç farklı model kur ve karşılaştır ───────────────────────

# --- Model A: Standart Linear Regresyon ---
lr = LinearRegression()
lr.fit(X_train, y_train)
y_pred_lr = lr.predict(X_test)

# --- Model B: Ridge Regresyon ---
# alpha = ceza katsayısı; büyük alpha → daha güçlü ceza → basit model
ridge = Ridge(alpha=1.0)
ridge.fit(X_train, y_train)
y_pred_ridge = ridge.predict(X_test)

# --- Model C: Lasso Regresyon ---
# Lasso bazı özelliklerin katsayısını 0'a indirir (özellik eleme)
lasso = Lasso(alpha=0.1)
lasso.fit(X_train, y_train)
y_pred_lasso = lasso.predict(X_test)

# ── 5. Modelleri değerlendir ─────────────────────────────────────
def degerlendirme(model_adi, y_gercek, y_tahmin):
    rmse = np.sqrt(mean_squared_error(y_gercek, y_tahmin))
    r2   = r2_score(y_gercek, y_tahmin)
    print(f"{model_adi:25s} | RMSE: {rmse:.3f} | R²: {r2:.3f}")

print("\n" + "="*60)
print(f"{'Model':<25} | {'RMSE':^10} | {'R²':^8}")
print("="*60)
degerlendirme("Linear Regresyon",   y_test, y_pred_lr)
degerlendirme("Ridge (alpha=1.0)",  y_test, y_pred_ridge)
degerlendirme("Lasso (alpha=0.1)",  y_test, y_pred_lasso)
print("="*60)

# RMSE: Ortalama hata büyüklüğü — küçük olması daha iyidir
# R²  : 1.0 = mükemmel, 0.0 = hiçbir şey açıklamıyor

# ── 6. Katsayılara bak: hangi kanal satışa katkı sağlıyor? ──────
print("\n📊 Linear Regresyon Katsayıları (Önem Sırası):")
katsayilar = pd.Series(lr.coef_, index=["TV", "Radio", "Newspaper"])
print(katsayilar.sort_values(ascending=False))
# Büyük katsayı → o özellik satışı daha çok etkiliyor

print("\n📊 Lasso Katsayıları (0 ise özellik elendi):")
print(pd.Series(lasso.coef_, index=["TV", "Radio", "Newspaper"]))

# ── 7. TV harcamasına göre satış grafiği ────────────────────────
plt.figure(figsize=(8, 5))
plt.scatter(df["TV"], df["Sales"], alpha=0.6, label="Gerçek Veri")
plt.xlabel("TV Reklam Harcaması (bin $)")
plt.ylabel("Satış (bin adet)")
plt.title("TV Harcaması vs Satış — Advertising.csv")
plt.legend()
plt.tight_layout()
plt.show()

# ── 8. Yeni bütçe için tahmin ───────────────────────────────────
# Senaryo: TV=200$, Radio=30$, Newspaper=10$ bütçesi için satış?
yeni_butce = pd.DataFrame([[200, 30, 10]], columns=["TV", "Radio", "Newspaper"])
print(f"\n🔮 Yeni Bütçe Tahmini (TV=200, Radio=30, Newspaper=10):")
print(f"  Linear : {lr.predict(yeni_butce)[0]:.1f} bin adet")
print(f"  Ridge  : {ridge.predict(yeni_butce)[0]:.1f} bin adet")
print(f"  Lasso  : {lasso.predict(yeni_butce)[0]:.1f} bin adet")
```

### 📌 Modeller Neden Farklı?

```
Linear Regresyon
  → Hiç ceza yok. Verideki her pattern'e uyar.
  → Küçük veri setlerinde aşırı öğrenme riski var.

Ridge (L2 ceza)
  → Katsayıları küçültür ama sıfırlamaz.
  → Tüm özellikler modelde kalır.

Lasso (L1 ceza)
  → Bazı katsayıları tam sıfır yapar.
  → "Newspaper" gibi düşük katkılı özelliği otomatik eler.
  → Gerçek hayatta özellik seçimi için çok kullanılır.
```

### 💡 Gerçek Hayat Yorumu

> Lasso modeli muhtemelen `Newspaper` katsayısını 0'a indirger.
> Bu da bize şunu söyler: **gazete reklamı satışa pek katkı sağlamıyor**,
> bütçeyi TV ve radyoya odaklamak daha akıllıca.

---

## ❓ Soru 3 — Decision Tree ile Banka Müşteri Kayıp Riski Analizi

> 📁 **Veri seti:** `Churn_Modelling.csv` · 10.000 satır · 14 sütun  
> 🏦 **Alan:** Bankacılık  
> 📘 **Konu:** Karar Ağacı (Decision Tree) + Random Forest karşılaştırması

### 🎯 Problem Tanımı

Banka, müşterilerini kaybetmeden önce tespit etmek istiyor.
Soru 1'de Logistic Regresyon kullandık.
Şimdi **Decision Tree** ve **Random Forest** kullanarak:
1. Hangi özellik müşteri kaybını en çok etkiliyor?
2. Decision Tree mi, Random Forest mi daha başarılı?
3. Karar ağacını görselleştirelim.

---

### ✅ Cevap 3

```python
# ── Kütüphaneleri yükle ──────────────────────────────────────────
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, classification_report
from sklearn.preprocessing import LabelEncoder

# ── 1. Veriyi oku ve hazırla ─────────────────────────────────────
df = pd.read_csv("Churn_Modelling.csv")

# Geography (Fransa/Almanya/İspanya) sütunu metinsel
# Bunu sayıya çevirmemiz gerekiyor: LabelEncoder kullan
le = LabelEncoder()
df["Geography_enc"] = le.fit_transform(df["Geography"])
# France=0, Germany=1, Spain=2 gibi
df["Gender_enc"]    = le.fit_transform(df["Gender"])
# Female=0, Male=1

# ── 2. Özellik ve etiket seç ─────────────────────────────────────
ozellikler = ["CreditScore", "Geography_enc", "Gender_enc",
              "Age", "Tenure", "Balance", "NumOfProducts",
              "HasCrCard", "IsActiveMember", "EstimatedSalary"]

X = df[ozellikler]
y = df["Exited"]

# ── 3. Eğitim / test bölmesi ────────────────────────────────────
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# ── 4. Decision Tree ─────────────────────────────────────────────
# max_depth=4: Ağaç en fazla 4 kat derine iner
# Çok derin ağaç → aşırı öğrenme (overfitting)
# Çok sığ ağaç  → az öğrenme   (underfitting)
dt = DecisionTreeClassifier(max_depth=4, random_state=42)
dt.fit(X_train, y_train)
dt_pred = dt.predict(X_test)
dt_acc  = accuracy_score(y_test, dt_pred)
print(f"Decision Tree Doğruluğu : %{dt_acc * 100:.1f}")

# ── 5. Random Forest ─────────────────────────────────────────────
# 100 farklı karar ağacı kurar, oy çokluğuyla karar verir
# Tek ağaca göre çok daha sağlam sonuçlar üretir
rf = RandomForestClassifier(n_estimators=100, max_depth=6, random_state=42)
rf.fit(X_train, y_train)
rf_pred = rf.predict(X_test)
rf_acc  = accuracy_score(y_test, rf_pred)
print(f"Random Forest Doğruluğu : %{rf_acc * 100:.1f}")

# ── 6. Detaylı rapor ─────────────────────────────────────────────
print("\n📋 Random Forest — Sınıflandırma Raporu:")
print(classification_report(y_test, rf_pred,
                             target_names=["Kaldı (0)", "Ayrıldı (1)"]))
# Precision: Tahmin ettiğimiz "ayrıldı"ların kaçı gerçekten ayrıldı?
# Recall   : Gerçekte ayrılanların kaçını yakaladık?
# F1-Score : Precision ve Recall'un dengeli ortalaması

# ── 7. Özellik Önem Sıralaması ───────────────────────────────────
# Hangi özellik müşteri kaybını en çok etkiliyor?
onem = pd.Series(rf.feature_importances_, index=ozellikler)
onem_sirali = onem.sort_values(ascending=False)
print("\n🏆 Özellik Önem Sıralaması (Random Forest):")
for ozellik, deger in onem_sirali.items():
    bar = "█" * int(deger * 100)
    print(f"  {ozellik:<20} {bar} {deger:.3f}")

# ── 8. Karar ağacını görselleştir ────────────────────────────────
plt.figure(figsize=(20, 8))
plot_tree(dt,
          feature_names=ozellikler,
          class_names=["Kaldı", "Ayrıldı"],
          filled=True,       # Renklendirme
          max_depth=3,       # Sadece 3 derinlik göster
          fontsize=10)
plt.title("Decision Tree — Banka Müşteri Kaybı (max_depth=3)")
plt.tight_layout()
plt.show()

# ── 9. Yeni müşteri tahmini ──────────────────────────────────────
# 35 yaşında, Almanyalı, erkek, kredi skoru 500,
# bakiyesi 0, 2 ürün, aktif değil
yeni = pd.DataFrame([[500, 1, 1, 35, 3, 0, 2, 1, 0, 70000]],
                    columns=ozellikler)
tahmin_rf = rf.predict(yeni)[0]
olasilik  = rf.predict_proba(yeni)[0]

print(f"\n🔮 Yeni Müşteri Tahmini (Random Forest):")
print(f"  Karar          : {'Ayrılır ⚠️' if tahmin_rf == 1 else 'Kalır ✅'}")
print(f"  Kalma olasılığı: %{olasilik[0]*100:.1f}")
print(f"  Ayrılma olasılığı: %{olasilik[1]*100:.1f}")
```

### 📌 Decision Tree vs Random Forest

```
Decision Tree (Tek Ağaç)
  ✅ Anlaşılması kolay, görselleştirilebilir
  ✅ Hızlı eğitim
  ❌ Aşırı öğrenmeye yatkın
  ❌ Veri biraz değişse sonuç büyük değişir

Random Forest (100 Ağaç)
  ✅ Çok daha yüksek doğruluk
  ✅ Aşırı öğrenmeye dayanıklı
  ✅ Özellik önem sıralaması verir
  ❌ Daha yavaş ve görselleştirmesi zor
```

### 💡 Beklenen Özellik Önem Sonucu

> Random Forest büyük olasılıkla şunu gösterecek:
> - **Age (Yaş)** → en güçlü etken (yaşlı müşteriler daha çok ayrılıyor)
> - **Balance (Bakiye)** → bakiyesi 0 olan müşteriler risk altında
> - **NumOfProducts** → 3–4 ürünü olan müşteriler daha çok ayrılıyor
>
> Bu bilgiler banka için müşteri tutundurma stratejisi oluşturmada doğrudan kullanılır.

---

## ❓ Soru 4 — KNN ile AVM Müşteri Segmentasyonu ve Harcama Tahmini

> 📁 **Veri seti:** `Mall_Customers.csv` · 200 satır · 5 sütun  
> 🛍️ **Alan:** Perakende / E-Ticaret  
> 📘 **Konu:** KNN (K-En Yakın Komşu) Sınıflandırma

### 🎯 Problem Tanımı

Bir alışveriş merkezi müşterilerini şu bilgilerle takip ediyor:

| Sütun | Açıklama |
|---|---|
| `Gender` | Cinsiyet |
| `Age` | Yaş |
| `AnnualIncome` | Yıllık gelir (bin $) |
| `SpendingScore` | Harcama puanı (1–100) |

**Soru:** Gelir ve yaşa bakarak bir müşterinin "Yüksek Harcamacı" mı yoksa "Düşük Harcamacı" mı olduğunu tahmin et.  
Kaç komşu (K) en iyi sonucu veriyor?

---

### ✅ Cevap 4

```python
# ── Kütüphaneleri yükle ──────────────────────────────────────────
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import accuracy_score

# ── 1. Veriyi oku ────────────────────────────────────────────────
df = pd.read_csv("Mall_Customers.csv")

print("Veri boyutu:", df.shape)          # (200, 5)
print(df.head())
#    CustomerID Gender  Age  AnnualIncome  SpendingScore
# 0           1   Male   19         15000             39
# 1           2   Male   21         15000             81

print("\nSpendingScore istatistikleri:")
print(df["SpendingScore"].describe())
# min=1, max=99, ortalama≈50

# ── 2. Hedef sütun oluştur ──────────────────────────────────────
# SpendingScore > 50 ise "Yüksek Harcamacı" (1), değilse (0)
# Bu basit bir threshold; gerçek hayatta daha sofistike olabilir
df["HarcamaSinifi"] = (df["SpendingScore"] > 50).astype(int)

print(f"\nYüksek Harcamacı (1): {df['HarcamaSinifi'].sum()} kişi")
print(f"Düşük Harcamacı  (0): {(df['HarcamaSinifi']==0).sum()} kişi")

# ── 3. Cinsiyet kodlaması ────────────────────────────────────────
df["Gender_enc"] = (df["Gender"] == "Male").astype(int)
# Male=1, Female=0

# ── 4. Özellik ve etiket ─────────────────────────────────────────
X = df[["Age", "AnnualIncome", "Gender_enc"]]
y = df["HarcamaSinifi"]

# ── 5. Eğitim / test bölmesi ────────────────────────────────────
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.25, random_state=42
)

# ── 6. Ölçeklendirme ─────────────────────────────────────────────
# KNN, mesafeye göre çalışır!
# AnnualIncome (15.000–137.000) ile Age (18–70) aynı ölçekte değil.
# StandardScaler olmadan AnnualIncome her şeye baskın olur.
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test  = scaler.transform(X_test)

# ── 7. Farklı K değerleri için doğruluk hesapla ─────────────────
# K=1: Sadece en yakın 1 komşuya bak (çok hassas, aşırı öğrenme riski)
# K=15: 15 komşuya bak (daha dengeli)
k_degerler = range(1, 20)
dogruluklar = []

for k in k_degerler:
    knn = KNeighborsClassifier(n_neighbors=k)
    knn.fit(X_train, y_train)
    acc = accuracy_score(y_test, knn.predict(X_test))
    dogruluklar.append(acc)

# En iyi K değeri
en_iyi_k   = k_degerler[np.argmax(dogruluklar)]
en_iyi_acc = max(dogruluklar)
print(f"\n🏆 En iyi K değeri : {en_iyi_k}")
print(f"   En yüksek doğruluk: %{en_iyi_acc * 100:.1f}")

# ── 8. En iyi K ile final model ─────────────────────────────────
knn_final = KNeighborsClassifier(n_neighbors=en_iyi_k)
knn_final.fit(X_train, y_train)

# ── 9. K değeri grafiği ──────────────────────────────────────────
plt.figure(figsize=(8, 4))
plt.plot(k_degerler, [d * 100 for d in dogruluklar], marker='o', color='steelblue')
plt.axvline(x=en_iyi_k, color='red', linestyle='--', label=f'En iyi K={en_iyi_k}')
plt.xlabel("K (Komşu Sayısı)")
plt.ylabel("Doğruluk (%)")
plt.title("K Değerine Göre Model Doğruluğu — Mall Customers")
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()

# ── 10. Yeni müşteri tahmini ─────────────────────────────────────
# 28 yaşında, yıllık 75.000$ geliri olan kadın müşteri
yeni_musteri = [[28, 75000, 0]]   # 0 = Female
yeni_olcekli = scaler.transform(yeni_musteri)
tahmin = knn_final.predict(yeni_olcekli)[0]
olasilik = knn_final.predict_proba(yeni_olcekli)[0]

print(f"\n🔮 Yeni Müşteri Tahmini:")
print(f"  Harcama Sınıfı    : {'Yüksek Harcamacı 🛍️' if tahmin == 1 else 'Düşük Harcamacı 💰'}")
print(f"  Yüksek Olasılığı  : %{olasilik[1]*100:.1f}")
```

### 📌 KNN Nasıl Çalışıyor?

```
Yeni müşteri → (Yaş=28, Gelir=75.000$)

KNN sırasıyla şunu yapar:
  1. Bu noktaya en yakın K komşuyu bul
  2. Bu komşuların çoğunluğu "Yüksek Harcamacı" ise → o da öyle tahmin edilir

K=1 → sadece en yakın 1 kişiye bak (çok hassas, gürültüye duyarlı)
K=5 → en yakın 5 kişinin oy çokluğuna bak (daha dengeli)
K=15 → 15 kişi (çok genel, underfitting riski)
```

### 💡 Gerçek Hayat Kullanımı

> Bir e-ticaret sitesi yeni bir kullanıcının yaşına ve gelirine bakarak
> önce "Yüksek Harcamacı mı?" diye tahmin eder.
> Yüksek harcamacıysa premium ürünler, indirim kodları önerir.
> Düşük harcamacıysa bütçe dostu ürünleri öne çıkarır.

---

## ❓ Soru 5 — Ridge & Lasso ile Müşteri Yaşam Boyu Değeri Tahmini

> 📁 **Veri seti:** `Churn_Modelling.csv` · 10.000 satır · 14 sütun  
> 🏦 **Alan:** Finans / Bankacılık  
> 📘 **Konu:** Regresyon → Ridge ve Lasso Karşılaştırması + Aşırı Öğrenme (Overfitting) Tespiti

### 🎯 Problem Tanımı

Banka, bir müşterinin **tahmini maaşını** (`EstimatedSalary`) diğer bilgilere dayanarak tahmin etmek istiyor.

**Neden önemli?** Müşterinin gelirini tahmin edebilirsen:
- Kişiselleştirilmiş finansal ürün önerebilirsin
- Kredi limitini doğru belirleyebilirsin
- Müşteri yaşam boyu değerini hesaplayabilirsin

**Soru:**
1. LinearRegression ile Ridge ve Lasso arasındaki farkı ölç.
2. Eğitim ve test hatalarını karşılaştırarak aşırı öğrenme var mı bak.
3. En iyi `alpha` değerini bul.

---

### ✅ Cevap 5

```python
# ── Kütüphaneleri yükle ──────────────────────────────────────────
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression, Ridge, Lasso
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.metrics import mean_absolute_error, r2_score

# ── 1. Veriyi oku ve hazırla ─────────────────────────────────────
df = pd.read_csv("Churn_Modelling.csv")

le = LabelEncoder()
df["Geography_enc"] = le.fit_transform(df["Geography"])
df["Gender_enc"]    = le.fit_transform(df["Gender"])

# ── 2. Özellikler ve hedef ───────────────────────────────────────
ozellikler = ["CreditScore", "Geography_enc", "Gender_enc",
              "Age", "Tenure", "Balance", "NumOfProducts",
              "HasCrCard", "IsActiveMember", "Exited"]

X = df[ozellikler]
y = df["EstimatedSalary"]   # Tahmin edeceğimiz: Tahmini Maaş

print("Maaş istatistikleri:")
print(y.describe().round(2))
# min≈11, max≈200.000, ortalama≈100.000

# ── 3. Eğitim / test bölmesi ────────────────────────────────────
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# ── 4. Ölçeklendirme ─────────────────────────────────────────────
scaler = StandardScaler()
X_train_s = scaler.fit_transform(X_train)
X_test_s  = scaler.transform(X_test)

# ── 5. Modelleri kur ─────────────────────────────────────────────

# --- Model A: Standart Linear Regresyon ---
lr = LinearRegression()
lr.fit(X_train_s, y_train)

# --- Model B: Ridge (L2 ceza) ---
# alpha ne kadar büyük → ceza o kadar sert → katsayılar küçülür
ridge = Ridge(alpha=10.0)
ridge.fit(X_train_s, y_train)

# --- Model C: Lasso (L1 ceza) ---
# Bazı katsayılar 0 olur → otomatik özellik eleme
lasso = Lasso(alpha=100.0)
lasso.fit(X_train_s, y_train)

# ── 6. Eğitim ve Test Hatalarını Karşılaştır ────────────────────
# ÖNEMLİ: Aşırı öğrenme tespiti için ikisine de bakmalıyız!
# Eğitim hatası küçük, test hatası büyük → Aşırı öğrenme var

def hata_raporu(model_adi, model, X_tr, X_te, y_tr, y_te):
    train_r2 = r2_score(y_tr, model.predict(X_tr))
    test_r2  = r2_score(y_te, model.predict(X_te))
    test_mae = mean_absolute_error(y_te, model.predict(X_te))
    fark     = train_r2 - test_r2
    print(f"\n{'─'*50}")
    print(f"📦 Model: {model_adi}")
    print(f"  Eğitim R² : {train_r2:.4f}")
    print(f"  Test R²   : {test_r2:.4f}")
    print(f"  Fark      : {fark:.4f}  {'⚠️ Aşırı öğrenme olabilir!' if fark > 0.05 else '✅ Dengeli'}")
    print(f"  Ortalama Hata (MAE): ${test_mae:,.0f}")

hata_raporu("Linear Regresyon",   lr,    X_train_s, X_test_s, y_train, y_test)
hata_raporu("Ridge (alpha=10)",   ridge, X_train_s, X_test_s, y_train, y_test)
hata_raporu("Lasso (alpha=100)",  lasso, X_train_s, X_test_s, y_train, y_test)

# ── 7. En iyi Ridge alpha değerini bul ──────────────────────────
# 5-Katlı Çapraz Doğrulama (Cross Validation) ile her alpha'yı test et
print("\n\n🔍 Ridge için En İyi Alpha Arayışı:")
alpha_degerler = [0.01, 0.1, 1, 10, 50, 100, 500, 1000]
sonuclar = []

for a in alpha_degerler:
    r = Ridge(alpha=a)
    # cv=5: veriyi 5 parçaya böl, her seferinde 1'ini test olarak kullan
    skorlar = cross_val_score(r, X_train_s, y_train,
                              cv=5, scoring="r2")
    sonuclar.append({
        "alpha": a,
        "ortalama_r2": skorlar.mean(),
        "std": skorlar.std()
    })

df_alpha = pd.DataFrame(sonuclar)
print(df_alpha.to_string(index=False))

en_iyi_alpha = df_alpha.loc[df_alpha["ortalama_r2"].idxmax(), "alpha"]
print(f"\n🏆 En iyi Ridge alpha: {en_iyi_alpha}")

# ── 8. Lasso katsayılarına bak ───────────────────────────────────
print("\n📊 Lasso Katsayıları (0 ise özellik elendi):")
lasso_katsayilar = pd.Series(lasso.coef_, index=ozellikler)
for ozellik, katsayi in lasso_katsayilar.items():
    durum = "✅ Aktif" if katsayi != 0 else "❌ Elendi (katsayı=0)"
    print(f"  {ozellik:<22}: {katsayi:>10.2f}  {durum}")

# ── 9. Alpha vs R² grafiği ───────────────────────────────────────
plt.figure(figsize=(8, 4))
plt.semilogx(df_alpha["alpha"], df_alpha["ortalama_r2"],
             marker='o', color='darkorange')
plt.xlabel("Alpha (log ölçek)")
plt.ylabel("R² Skoru (CV Ortalaması)")
plt.title("Ridge Alpha Değeri vs Model Performansı")
plt.grid(True, which="both", linestyle="--", alpha=0.5)
plt.tight_layout()
plt.show()

# ── 10. Yeni müşteri için maaş tahmini ──────────────────────────
# KrediSkoru=700, Fransa(0), Erkek(1), Yaş=35, Tenure=5,
# Bakiye=50.000, 1 ürün, kredi kartı var, aktif, kalmış
yeni = pd.DataFrame([[700, 0, 1, 35, 5, 50000, 1, 1, 1, 0]],
                    columns=ozellikler)
yeni_s = scaler.transform(yeni)

print("\n🔮 Yeni Müşteri Maaş Tahmini:")
print(f"  Linear : ${lr.predict(yeni_s)[0]:,.0f}")
print(f"  Ridge  : ${ridge.predict(yeni_s)[0]:,.0f}")
print(f"  Lasso  : ${lasso.predict(yeni_s)[0]:,.0f}")
```

### 📌 Aşırı Öğrenme Nedir? Nasıl Anlaşılır?

```
       Eğitim R²     Test R²     Yorum
LR       0.95         0.70     ⚠️  Aşırı öğrenme var!
Ridge    0.90         0.87     ✅  Dengeli
Lasso    0.82         0.80     ✅  Biraz daha genel

Kural: Eğitim R² >> Test R² ise model eğitim datasını
       "ezberliyor" ama yeni veriye genelleme yapamıyor.
       Ridge ve Lasso bunu engellemek için katsayılara
       ceza uygular.
```

### 📌 Cross Validation (Çapraz Doğrulama) Nedir?

```
Veriyi 5 parçaya böl:
  [ P1 | P2 | P3 | P4 | P5 ]

Tur 1: [P1 test] [P2 P3 P4 P5 eğitim]
Tur 2: [P2 test] [P1 P3 P4 P5 eğitim]
Tur 3: [P3 test] [P1 P2 P4 P5 eğitim]
Tur 4: [P4 test] [P1 P2 P3 P5 eğitim]
Tur 5: [P5 test] [P1 P2 P3 P4 eğitim]

5 sonucun ortalaması = daha güvenilir performans ölçüsü
```

### 💡 Gerçek Hayat Yorumu

> `EstimatedSalary` sütunu aslında bankaya müşteri tarafından bildirilen gelirdir.
> Çoğu zaman eksik ya da yanlış olabilir.
> Bu modeli kullanarak banka, mevcut müşteri davranışlarından (bakiye, ürün sayısı, aktiflik)
> **gelir tahmini** yapabilir ve eksik bilgileri tamamlayabilir.
> Böylece kredi teklifleri daha gerçekçi kişiselleştirilir.

---

## 📊 Genel Özet — 5 Soruda Hangi Algoritma, Nerede?

| # | Problem | Algoritma | Veri Seti | Alan |
|---|---|---|---|---|
| 1 | Müşteri ayrılıyor mu? (0/1) | Logistic Regresyon | Churn_Modelling | Bankacılık |
| 2 | Reklam → Satış tahmini ($) | Linear / Ridge / Lasso | Advertising | E-Ticaret |
| 3 | Müşteri kaybı (ağaç modeli) | Decision Tree + Random Forest | Churn_Modelling | Bankacılık |
| 4 | Harcama sınıfı tahmini | KNN | Mall_Customers | Perakende |
| 5 | Maaş tahmini + overfitting | Ridge / Lasso + Cross Validation | Churn_Modelling | Finans |

---

## 🧠 Algoritma Seçim Rehberi

```
Tahmin etmek istediğin değer sayısal mı?
  EVET → Regresyon
    → Az özellik, basit ilişki  : Linear Regresyon
    → Aşırı öğrenme endişesi    : Ridge
    → Gereksiz özellik var       : Lasso
    → İkisi birden               : ElasticNet

Tahmin etmek istediğin değer kategori mi?
  EVET → Sınıflandırma
    → İkili sınıf (evet/hayır)  : Logistic Regresyon
    → Kural bazlı anlaşılır      : Decision Tree
    → En yüksek doğruluk         : Random Forest
    → Benzerlik/mesafeye göre    : KNN
```