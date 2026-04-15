# 🏦 Soru 1 — Logistic Regresyon ile Banka Müşteri Kaybı Tahmini
## Satır Satır, Bol Açıklamalı Tam Kod

> **Veri seti:** `Churn_Modelling.csv`  
> Kodu VS Code'a yapıştır, dosya yolunu düzenle ve direkt çalıştır!

---

## ✅ Direkt Çalışan Tam Kod

```python
# =============================================================
# SORU 1: Logistic Regresyon ile Banka Müşteri Kaybı Tahmini
# Veri seti: Churn_Modelling.csv
# =============================================================
# Bu dosyayı VS Code'a yapıştır ve çalıştır.
# Gerekli kütüphaneler: pip install pandas scikit-learn
# =============================================================


# ── BÖLÜM 1: KÜTÜPHANELERİ YÜKLE ────────────────────────────────────────────

import pandas as pd
# pandas → veri okuma ve tablo işlemleri için kullanılır.
# "pd" kısaltması genel kabul görmüş bir gelenek.

from sklearn.linear_model import LogisticRegression
# sklearn → makine öğrenmesi kütüphanesi (scikit-learn)
# LogisticRegression → ikili sınıflandırma (0 veya 1 tahmini) için algoritma

from sklearn.model_selection import train_test_split
# train_test_split → veriyi eğitim ve test olarak ikiye böler

from sklearn.preprocessing import StandardScaler
# StandardScaler → sütunlardaki büyük-küçük sayı farkını dengeler (ölçeklendirme)

from sklearn.metrics import accuracy_score, confusion_matrix, classification_report
# accuracy_score     → modelin kaçını doğru tahmin ettiğini yüzde olarak verir
# confusion_matrix   → doğru/yanlış tahminleri tablo olarak gösterir
# classification_report → precision, recall, f1 gibi detaylı metrikleri verir


# ── BÖLÜM 2: VERİYİ OKU ─────────────────────────────────────────────────────

df = pd.read_csv("Churn_Modelling.csv")
# pd.read_csv() → CSV dosyasını okur ve bir tablo (DataFrame) oluşturur.
# "df" → DataFrame kısaltması, tablo değişkenine verilen genel isim.
# ÖNEMLİ: Bu dosya (.py) ile Churn_Modelling.csv aynı klasörde olmalı!
# Farklı bir klasördeyse tam yolu yaz:
# df = pd.read_csv(r"C:\Users\kullanici\Downloads\Churn_Modelling.csv")

print("=" * 55)
print("VERİ HAKKINDA GENEL BİLGİ")
print("=" * 55)

print(f"\nToplam satır ve sütun sayısı: {df.shape}")
# df.shape → (satır_sayısı, sütun_sayısı) döndürür.
# Beklenen çıktı: (10000, 14) → 10.000 müşteri, 14 sütun

print("\nİlk 3 satır (örnek veri):")
print(df.head(3))
# df.head(3) → tablonun ilk 3 satırını gösterir.
# Veriyi tanımak için kullanılır.

print("\nSütun isimleri:")
print(df.columns.tolist())
# df.columns → tüm sütun isimlerini listeler.
# Hangi sütunun ne olduğunu görmek için kullanılır.

print("\nKaç müşteri bankadan ayrılmış? (0=Kaldı, 1=Ayrıldı)")
print(df["Exited"].value_counts())
# df["Exited"] → sadece "Exited" sütununu seçer.
# .value_counts() → o sütundaki her değerden kaç tane olduğunu sayar.
# Beklenen: 0 (Kaldı): ~7963, 1 (Ayrıldı): ~2037


# ── BÖLÜM 3: ÖZELLİKLERİ VE ETİKETİ SEÇ ────────────────────────────────────

print("\n" + "=" * 55)
print("ÖZELLİK VE ETİKET SEÇİMİ")
print("=" * 55)

X = df[["CreditScore", "Age", "Tenure", "Balance",
        "NumOfProducts", "HasCrCard", "IsActiveMember", "EstimatedSalary"]]
# X → modelin öğreneceği giriş verileri (özellikler / features)
# Sadece SAYISAL sütunları seçiyoruz.
# Şimdilik metin sütunlarını (Geography, Gender) atlıyoruz.
#
# Seçilen sütunlar:
#   CreditScore    → müşterinin kredi notu (350-850 arası)
#   Age            → müşterinin yaşı
#   Tenure         → kaç yıldır bu bankada müşteri (0-10)
#   Balance        → hesap bakiyesi (0 ise hesapta para yok)
#   NumOfProducts  → bankanın kaç ürününü kullanıyor (kredi kartı, sigorta vb.)
#   HasCrCard      → kredi kartı var mı? (1=evet, 0=hayır)
#   IsActiveMember → aktif müşteri mi? (1=aktif, 0=pasif)
#   EstimatedSalary→ müşterinin tahmini yıllık maaşı ($)

y = df["Exited"]
# y → modelin tahmin etmeye çalışacağı etiket (hedef / label)
# "Exited" sütunu:  0 = müşteri bankada kaldı
#                   1 = müşteri bankadan ayrıldı
# Model bu değeri (0 veya 1) tahmin etmeye çalışacak.

print(f"\nX boyutu (özellikler): {X.shape}")
# Beklenen: (10000, 8) → 10.000 satır, 8 sütun

print(f"y boyutu (etiket)    : {y.shape}")
# Beklenen: (10000,) → 10.000 satır, 1 sütun


# ── BÖLÜM 4: VERİYİ EĞİTİM VE TEST OLARAK BÖL ──────────────────────────────

print("\n" + "=" * 55)
print("VERİ BÖLME: EĞİTİM / TEST")
print("=" * 55)

X_train, X_test, y_train, y_test = train_test_split(
    X,             # özellikler tablosu
    y,             # etiket sütunu
    test_size=0.2, # verinin %20'si test, %80'i eğitim olacak
    random_state=42  # her çalıştırmada aynı bölme yapılsın diye sabit tohum
)
# train_test_split() → 4 ayrı parça döndürür:
#   X_train → eğitim için kullanılacak özellikler  (%80)
#   X_test  → test için kullanılacak özellikler    (%20)
#   y_train → eğitimdeki müşterilerin gerçek cevapları (0/1)
#   y_test  → testteki müşterilerin gerçek cevapları (0/1)
#
# test_size=0.2 → 10.000 satırın 2.000'i test, 8.000'i eğitim olur.
#
# random_state=42 → rastgele sayı tohumudur.
#   Olmasa: her çalıştırmada farklı müşteriler test setine düşer.
#   42 yazınca: her seferinde aynı bölme yapılır → sonuçlar tekrarlanabilir.
#   42 sayısının özel anlamı yok, gelenek olarak kullanılır.

print(f"\nEğitim seti boyutu : {X_train.shape[0]} satır")
# X_train.shape[0] → kaç satır olduğunu verir (sütun sayısı için [1] kullanılır)

print(f"Test seti boyutu   : {X_test.shape[0]} satır")


# ── BÖLÜM 5: ÖLÇEKLENDİRME (SCALING) ────────────────────────────────────────

print("\n" + "=" * 55)
print("ÖLÇEKLENDİRME")
print("=" * 55)

print("\nÖlçeklendirme ÖNCESİ — örnek değerler:")
print(X_train.describe().round(0)[["CreditScore", "Age", "Balance"]].head(2))
# describe() → ortalama, min, max gibi istatistikleri gösterir.
# Bakıyoruz: CreditScore ~650, Age ~38, Balance ~76.000
# Bu kadar büyük fark model için sorun yaratır.

scaler = StandardScaler()
# StandardScaler nesnesi oluşturuldu.
# Henüz hiçbir şey yapmadı, sadece araç hazır.

X_train = scaler.fit_transform(X_train)
# fit_transform() → iki işlemi birden yapar:
#
#   fit()       → Eğitim verisinin her sütununun ORTALAMASINI ve
#                 STANDART SAPMASINI hesaplar ve aklında tutar.
#
#   transform() → Her değeri şu formüle göre dönüştürür:
#                 yeni_değer = (eski_değer - ortalama) / standart_sapma
#
# Örnek:
#   Age sütunu ortalaması = 38.9, standart sapması = 10.5
#   Bir müşterinin yaşı 45 ise:
#   yeni_yaş = (45 - 38.9) / 10.5 = +0.58
#   Bir müşterinin yaşı 28 ise:
#   yeni_yaş = (28 - 38.9) / 10.5 = -1.04
#
# Sonuç: Tüm değerler -3 ile +3 arası sayılara dönüşür.
# Artık Balance=150.000 ile HasCrCard=1 eşit ağırlıkta değerlendirilebilir.
#
# ⚠️ KURAL: fit_transform SADECE EĞİTİM verisine uygulanır!

X_test = scaler.transform(X_test)
# transform() → Sadece dönüştürme yapar, yeni bir fit() YAPMAZ.
# Eğitim verisinden öğrenilen ortalama ve std, test verisine uygulanır.
#
# Neden ayrı?
# Test verisi gerçek dünyayı simüle eder.
# Gerçek hayatta yeni bir müşterinin istatistiklerini bilmezsin.
# Ölçeği sadece geçmiş (eğitim) verisinden öğrenir, yeniye uygularsın.
#
# ❌ YANLIŞ: X_test = scaler.fit_transform(X_test)  ← BU HATA!
# ✅ DOĞRU : X_test = scaler.transform(X_test)      ← BU DOĞRU!

print("Ölçeklendirme tamamlandı ✅")
print("Artık tüm değerler -3 ile +3 arasında.")


# ── BÖLÜM 6: MODELİ KUR VE EĞİT ─────────────────────────────────────────────

print("\n" + "=" * 55)
print("MODEL EĞİTİMİ")
print("=" * 55)

model = LogisticRegression(max_iter=200)
# LogisticRegression() → modeli oluşturur, henüz eğitilmedi.
#
# max_iter=200 → modelin içindeki matematiksel hesaplama kaç kez tekrar etsin?
#   Varsayılan 100'dür. Büyük veri setlerinde 100 yetmez, model öğrenemez.
#   200 yazmak: "daha uzun çalış, daha iyi öğren" demek.
#   Çok düşük bırakırsan: ConvergenceWarning hatası alırsın.

print("\nModel eğitiliyor...")

model.fit(X_train, y_train)
# fit() → GERÇEk ÖĞRENME BURADA OLUR.
#
# Ne yapıyor?
# 8.000 müşterinin özelliklerine (X_train) ve
# gerçek cevaplarına (y_train: 0 veya 1) bakarak
# her özelliğin ne kadar etkili olduğunu hesaplar.
#
# Arka planda şunu öğrenir:
#   "Yaşlı müşteriler daha çok mu ayrılıyor?"
#   "Bakiyesi 0 olan müşteri ayrılıyor mu?"
#   "Aktif üye bankada kalıyor mu?"
#
# Matematiksel olarak her özellik için bir AĞIRLIK (w) bulur:
#   P(ayrılır) = sigmoid(w1*CreditScore + w2*Age + w3*Balance + ...)
#   sigmoid fonksiyonu sonucu 0-1 arasına sıkıştırır:
#   0.0 → kesinlikle kalmış | 0.5 → kararsız | 1.0 → kesinlikle ayrılmış

print("Model eğitimi tamamlandı ✅")

print("\nModelin öğrendiği katsayılar (ağırlıklar):")
katsayilar = pd.Series(model.coef_[0],
                       index=["CreditScore", "Age", "Tenure", "Balance",
                               "NumOfProducts", "HasCrCard", "IsActiveMember",
                               "EstimatedSalary"])
print(katsayilar.sort_values(ascending=False).round(3))
# model.coef_ → her özellik için öğrenilen ağırlığı gösterir.
# Pozitif değer → bu özellik arttıkça ayrılma ihtimali artar.
# Negatif değer → bu özellik arttıkça ayrılma ihtimali azalır.
# Sıfıra yakın → bu özellik modeli çok etkilemiyor.


# ── BÖLÜM 7: TAHMİN YAP ──────────────────────────────────────────────────────

print("\n" + "=" * 55)
print("TAHMİN")
print("=" * 55)

y_pred = model.predict(X_test)
# predict() → test verisindeki her müşteri için 0 veya 1 döndürür.
#
# ��çeride ne oluyor?
#   1. Model her müşteri için bir olasılık hesaplar.
#   2. Olasılık >= 0.5 ise → 1 (Ayrılır)
#      Olasılık  < 0.5 ise → 0 (Kalır)
#
# y_pred şuna benzer bir dizi olur:
# [0, 1, 0, 0, 1, 0, 1, 0, 0, ...]

y_pred_proba = model.predict_proba(X_test)
# predict_proba() → olasılıkları görmek istersen bunu kullan.
# Her satır için [kalma_olasılığı, ayrılma_olasılığı] döndürür.
# Örnek: [0.78, 0.22] → %78 kalır, %22 ayrılır → tahmin: 0 (Kalır)

print("\nİlk 5 müşterinin tahminleri:")
print(f"{'Tahmin':<10} {'Kalma %':<12} {'Ayrılma %':<12} {'Gerçek'}")
print("-" * 47)
for i in range(5):
    tahmin = y_pred[i]
    kalma = y_pred_proba[i][0] * 100
    ayrilma = y_pred_proba[i][1] * 100
    gercek = y_test.iloc[i]
    dogru = "✅" if tahmin == gercek else "❌"
    print(f"{tahmin:<10} %{kalma:<10.1f} %{ayrilma:<10.1f} {gercek}  {dogru}")


# ── BÖLÜM 8: BAŞARIYI ÖLÇ ────────────────────────────────────────────────────

print("\n" + "=" * 55)
print("MODEL BAŞARISI")
print("=" * 55)

acc = accuracy_score(y_test, y_pred)
# accuracy_score(gerçek_değerler, tahmin_edilen_değerler)
# Formül: Doğru Tahmin Sayısı / Toplam Tahmin Sayısı
# Örnek: 2000 testten 1640 doğruysa → 1640/2000 = 0.82 → %82

print(f"\n✅ Model Doğruluğu: %{acc * 100:.1f}")


# ── BÖLÜM 9: KARISIKLIK MATRİSİ ──────────────────────────────────────────────

print("\n" + "=" * 55)
print("KARISIKLIK MATRİSİ (Confusion Matrix)")
print("=" * 55)

cm = confusion_matrix(y_test, y_pred)
# confusion_matrix() → modelin hangi tip hata yaptığını gösterir.
# 2x2'lik bir tablo döndürür.

TN = cm[0][0]   # True Negative  → Gerçekte Kaldı,    model de "Kalır" dedi  ✅
FP = cm[0][1]   # False Positive → Gerçekte Kaldı,    model "Ayrılır" dedi   ❌
FN = cm[1][0]   # False Negative → Gerçekte Ayrıldı,  model "Kalır" dedi     ❌ (kötü!)
TP = cm[1][1]   # True Positive  → Gerçekte Ayrıldı,  model de "Ayrılır" dedi ✅

print(f"""
Karışıklık Matrisi:
┌─────────────────────────────────────────┐
│           MODELİN TAHMİNİ               │
│        Kaldı (0)    Ayrıldı (1)         │
├──────────────────────────────────────── │
│ G Kaldı (0) │  TN={TN:>5}  │  FP={FP:>5}  │  ✅❌
│ E           │              │              │
│ R Ayrıldı(1)│  FN={FN:>5}  │  TP={TP:>5}  │  ❌✅
└─────────────────────────────────────────┘
""")

print("─" * 55)
print(f"TN (Doğru Negatif)  : {TN:>5} → Kaldı, model de 'Kalır' dedi   ✅")
print(f"FP (Yanlış Pozitif) : {FP:>5} → Kaldı, ama model 'Ayrılır' dedi ❌")
print(f"FN (Yanlış Negatif) : {FN:>5} → Ayrıldı, ama model 'Kalır' dedi ❌ ← En kötüsü!")
print(f"TP (Doğru Pozitif)  : {TP:>5} → Ayrıldı, model de 'Ayrılır' dedi ✅")
print("─" * 55)
print(f"""
💡 Bankacılık Yorumu:
   FN = {FN} müşteriyi KAÇIRDIK!
   Bu müşteriler bankadan ayrıldı, ama model
   'kalır' dedi. Banka onlara özel teklif yapmadı.
   FN hatası bankacılıkta en maliyetli hatadır!
""")


# ── BÖLÜM 10: DETAYLI RAPOR ──────────────────────────────────────────────────

print("=" * 55)
print("DETAYLI SINIFLANDIRMA RAPORU")
print("=" * 55)

print(classification_report(y_test, y_pred,
                             target_names=["Kaldı (0)", "Ayrıldı (1)"]))
# classification_report → her sınıf için detaylı metrikler:
#
#   Precision (Kesinlik):
#     "Ayrılır" dediğimizin kaçı gerçekten ayrıldı?
#     Formül: TP / (TP + FP)
#
#   Recall (Duyarlılık):
#     Gerçekte ayrılanların kaçını yakaladık?
#     Formül: TP / (TP + FN)
#     ← Bankacılıkta en önemli metrik budur!
#
#   F1-Score:
#     Precision ve Recall'un dengeli ortalaması.
#     İkisi arasında denge kurar.
#
#   Support:
#     O sınıftan kaç örnek vardı?


# ── BÖLÜM 11: YENİ MÜŞTERİ TAHMİNİ ─────────────────────────────────────────

print("=" * 55)
print("YENİ MÜŞTERİ İÇİN TAHMİN")
print("=" * 55)

# Senaryo:
# 40 yaşında bir müşteri bankaya geliyor.
# Kredi skoru: 600, 5 yıldır müşteri, bakiye: 80.000$,
# 2 ürün kullanıyor, kredi kartı var, aktif değil, maaş: 90.000$

yeni_musteri = [[600, 40, 5, 80000, 2, 1, 0, 90000]]
# Dikkat: Sütun sırası X ile aynı olmalı!
# [CreditScore, Age, Tenure, Balance, NumOfProducts, HasCrCard, IsActiveMember, EstimatedSalary]

yeni_olcekli = scaler.transform(yeni_musteri)
# Yeni müşteriyi de eğitimde kullandığımız aynı ölçekle dönüştür.
# fit_transform değil, sadece transform! (fit eğitimde yapıldı zaten)

tahmin = model.predict(yeni_olcekli)
# 0 veya 1 döndürür.

olasilik = model.predict_proba(yeni_olcekli)
# [[kalma_olasiligi, ayrilma_olasiligi]] döndürür.

print(f"""
Müşteri Profili:
  Yaş           : 40
  Kredi Skoru   : 600
  Tenure        : 5 yıl
  Bakiye        : $80.000
  Ürün Sayısı   : 2
  Kredi Kartı   : Var
  Aktif Üye     : Hayır
  Maaş          : $90.000

Tahmin Sonucu:
  Karar            : {"⚠️  BANKADAN AYRILIR!" if tahmin[0] == 1 else "✅  BANKADA KALIR"}
  Kalma Olasılığı  : %{olasilik[0][0] * 100:.1f}
  Ayrılma Olasılığı: %{olasilik[0][1] * 100:.1f}
""")


# ── BÖLÜM 12: ÖZET TABLO ─────────────────────────────────────────────────────

print("=" * 55)
print("ÖZET")
print("=" * 55)
print(f"""
  Toplam test müşterisi : {len(y_test)}
  Doğru tahmin sayısı   : {(y_pred == y_test).sum()}
  Yanlış tahmin sayısı  : {(y_pred != y_test).sum()}
  Model Doğruluğu       : %{acc * 100:.1f}

  Doğru Pozitif  (TP): {TP}  → Ayrılanları doğru yakaladık ✅
  Yanlış Negatif (FN): {FN}  → Ayrılanları kaçırdık        ❌

  İpucu: FN'i azaltmak için eşik değeri (0.5)
  0.3'e düşürülebilir → daha fazla "ayrılır" tahmini yapılır.
""")
```

---

## 🖥️ VS Code'da Çalıştırmak için Adımlar

```
1. Bu kodun tamamını kopyala
2. VS Code'da yeni bir dosya aç: soru1.py
3. Kodu yapıştır
4. Churn_Modelling.csv dosyasını aynı klasöre koy
5. Terminal aç (Ctrl + `) ve şunu yaz:
       pip install pandas scikit-learn
6. Dosyayı çalıştır (F5 veya sağ tık → Run Python File)
```

---

## 📊 Beklenen Çıktı (Özet)

```
✅ Model Doğruluğu: %81.0

Karışıklık Matrisi:
  TN: ~1543  FP: ~64
  FN: ~317   TP: ~76

              precision  recall  f1-score
  Kaldı (0)     0.83      0.96     0.89
  Ayrıldı (1)   0.54      0.19     0.28

Yeni Müşteri Tahmini:
  → BANKADA KALIR ✅
  → Kalma olasılığı: ~%73
```

---

## 📌 Sütunların Kısa Anlamları

| Sütun | Türkçe Anlamı | Örnek Değer |
|---|---|---|
| `CreditScore` | Kredi notu | 350 – 850 |
| `Geography` | Ülke | France, Germany, Spain |
| `Gender` | Cinsiyet | Male, Female |
| `Age` | Yaş | 18 – 92 |
| `Tenure` | Bankada kaç yıldır | 0 – 10 |
| `Balance` | Hesap bakiyesi ($) | 0 – 250.898 |
| `NumOfProducts` | Kaç ürün kullanıyor | 1 – 4 |
| `HasCrCard` | Kredi kartı var mı | 0 veya 1 |
| `IsActiveMember` | Aktif üye mi | 0 veya 1 |
| `EstimatedSalary` | Tahmini maaş ($) | 11 – 200.000 |
| `Exited` | Bankadan ayrıldı mı | **0 veya 1** ← tahmin edilen |

---

## 💡 Hatırlatma — En Sık Yapılan 3 Hata

| Hata | Neden Yanlış | Doğrusu |
|---|---|---|
| `scaler.fit_transform(X_test)` | Test verisinin istatistiğini öğreniriz, gerçekçi olmaz | `scaler.transform(X_test)` |
| `random_state` yazmamak | Her çalıştırmada farklı sonuç çıkar | `random_state=42` yaz |
| Sadece accuracy'e bakmak | Dengesiz veri setinde accuracy yanıltır | Confusion matrix'e de bak |