# Facebook Prophet ile Zaman Serisi Tahmini

Bu ders, Facebook Prophet kütüphanesini kullanarak zaman serisi tahmini yapmayı, görselleştirmeyi ve gündelik hayattan örneklerle uygulamayı kapsar.

---

## 1. Facebook Prophet Nedir?

- Facebook (Meta) tarafından geliştirilen açık kaynaklı zaman serisi tahmin kütüphanesidir.
- Özellikle günlük, haftalık, mevsimsel verilerle çalışmak için optimize edilmiştir.
- Tatil günleri, mevsimsellik, trend gibi unsurları otomatik olarak ele alır.
- Kullanımı çok kolaydır, derin istatistik bilgisi gerektirmez.

**Neden Prophet?**
- Eksik verilerle başa çıkabilir
- Trend değişikliklerini otomatik algılar
- Mevsimsel örüntüleri yakalar
- Tatil ve özel günleri modele ekleyebilirsiniz

**Kurulum:**
```bash
pip install prophet
```

---

## 2. Facebook Prophet Temel Kavramlar

### Prophet'in İhtiyaç Duyduğu Veri Formatı

Prophet, iki sütunlu bir DataFrame bekler:
- `ds`: Tarih sütunu (datetime formatında)
- `y`: Tahmin edilecek değer (sayısal)

**Örnek Veri Yapısı:**
```python
import pandas as pd

veri = pd.DataFrame({
    'ds': pd.date_range('2023-01-01', periods=365, freq='D'),
    'y': [100 + i + (i % 7) * 5 for i in range(365)]
})
print(veri.head())
```

### Temel Bileşenler
- **Trend (Eğilim)**: Verinin genel yönü (artış/azalış)
- **Mevsimsellik (Seasonality)**: Tekrar eden örüntüler (günlük, haftalık, yıllık)
- **Tatiller (Holidays)**: Özel günlerin etkisi
- **Hata (Error)**: Modelin açıklayamadığı rastgele dalgalanmalar

---

## 3. İlk Prophet Modeli: Basit Tahmin

**Gündelik Hayat Örneği:**  
Bir marketin günlük satışlarını tahmin etmek.

```python
from prophet import Prophet
import pandas as pd
import numpy as np

# Örnek veri: 1 yıllık günlük satışlar
np.random.seed(42)
tarihler = pd.date_range('2023-01-01', '2023-12-31', freq='D')
satislar = 100 + np.arange(len(tarihler)) * 0.5 + np.random.randn(len(tarihler)) * 10

df = pd.DataFrame({
    'ds': tarihler,
    'y': satislar
})

# Prophet modeli oluştur
model = Prophet()
model.fit(df)

# 30 gün ilerisi için tahmin yap
gelecek = model.make_future_dataframe(periods=30)
tahmin = model.predict(gelecek)

print(tahmin[['ds', 'yhat', 'yhat_lower', 'yhat_upper']].tail())
```

**Açıklama:**
- `model.fit(df)`: Modeli veriye uydurmak
- `make_future_dataframe(periods=30)`: 30 gün ilerisi için tarih oluşturur
- `model.predict()`: Tahmin yapar
- `yhat`: Tahmin edilen değer
- `yhat_lower`, `yhat_upper`: Güven aralığı (alt ve üst sınırlar)

---

## 4. Facebook Prophet ile Zamana Bağlı Tahminler

### Haftalık Mevsimsellik Örneği

**Gündelik Hayat Örneği:**  
Bir restoranın hafta içi ve hafta sonu satışlarındaki fark.

```python
from prophet import Prophet
import pandas as pd
import numpy as np

# 2 yıllık veri
tarihler = pd.date_range('2022-01-01', '2023-12-31', freq='D')
hafta_gunu = tarihler.dayofweek
# Hafta sonu (5,6) satışlar daha yüksek
satislar = 200 + np.where(hafta_gunu >= 5, 50, 0) + np.random.randn(len(tarihler)) * 15

df = pd.DataFrame({'ds': tarihler, 'y': satislar})

model = Prophet(weekly_seasonality=True)
model.fit(df)

# 60 gün ilerisi tahmin
gelecek = model.make_future_dataframe(periods=60)
tahmin = model.predict(gelecek)

print(tahmin[['ds', 'yhat']].tail(10))
```

**Açıklama:**
- Hafta sonu satışları artıyor, Prophet bunu otomatik öğreniyor.

### Yıllık Mevsimsellik Örneği

**Gündelik Hayat Örneği:**  
Bir dondurma dükkanının yazın satışlarının artması, kışın azalması.

```python
# 3 yıllık veri
tarihler = pd.date_range('2021-01-01', '2023-12-31', freq='D')
ay = tarihler.month
# Yaz aylarında (6,7,8) satış artar
satislar = 100 + np.where((ay >= 6) & (ay <= 8), 100, 0) + np.random.randn(len(tarihler)) * 20

df = pd.DataFrame({'ds': tarihler, 'y': satislar})

model = Prophet(yearly_seasonality=True)
model.fit(df)

gelecek = model.make_future_dataframe(periods=90)
tahmin = model.predict(gelecek)

print(tahmin[['ds', 'yhat']].tail(10))
```

---

## 5. Tatil ve Özel Günleri Ekleme

**Gündelik Hayat Örneği:**  
Yılbaşı, Ramazan Bayramı gibi özel günlerde satışlar değişir.

```python
from prophet import Prophet
import pandas as pd

# Tatil günleri tanımlama
tatiller = pd.DataFrame({
    'holiday': 'yilbasi',
    'ds': pd.to_datetime(['2023-01-01', '2024-01-01']),
    'lower_window': 0,
    'upper_window': 1,
})

df = pd.DataFrame({
    'ds': pd.date_range('2023-01-01', '2023-12-31', freq='D'),
    'y': 150 + np.random.randn(365) * 20
})

# Yılbaşında satış artışı simüle et
df.loc[df['ds'] == '2023-01-01', 'y'] += 100

model = Prophet(holidays=tatiller)
model.fit(df)

gelecek = model.make_future_dataframe(periods=30)
tahmin = model.predict(gelecek)

print(tahmin[['ds', 'yhat']].head(5))
```

**Açıklama:**
- `holidays` parametresi ile tatil günlerini modele ekledik.
- Prophet bu günlerdeki farklılıkları öğrenir.

---

## 6. Trend Değişikliklerini Yakalamak

**Gündelik Hayat Örneği:**  
Bir e-ticaret sitesinin satışlarında ani artış (kampanya, viral içerik).

```python
from prophet import Prophet
import pandas as pd
import numpy as np

tarihler = pd.date_range('2023-01-01', '2023-12-31', freq='D')
# 6. aydan sonra trend değişimi (ani artış)
satislar = np.where(tarihler < '2023-06-01', 
                    100 + np.arange(len(tarihler)) * 0.2,
                    200 + np.arange(len(tarihler)) * 0.5)
satislar += np.random.randn(len(tarihler)) * 15

df = pd.DataFrame({'ds': tarihler, 'y': satislar})

model = Prophet(changepoint_prior_scale=0.5)
model.fit(df)

gelecek = model.make_future_dataframe(periods=30)
tahmin = model.predict(gelecek)

print(tahmin[['ds', 'yhat']].tail(10))
```

**Açıklama:**
- `changepoint_prior_scale`: Trend değişikliklerine ne kadar esnek olunacağını belirler.
- Değer arttıkça model daha esnek olur, ani değişimleri yakalar.

---

## 7. Facebook Prophet Görselleştirme

### Temel Tahmin Grafiği

```python
from prophet import Prophet
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Örnek veri
tarihler = pd.date_range('2023-01-01', '2023-12-31', freq='D')
satislar = 100 + np.arange(len(tarihler)) * 0.3 + np.random.randn(len(tarihler)) * 10

df = pd.DataFrame({'ds': tarihler, 'y': satislar})

model = Prophet()
model.fit(df)

gelecek = model.make_future_dataframe(periods=60)
tahmin = model.predict(gelecek)

# Grafik çizme
fig = model.plot(tahmin)
plt.title("Günlük Satış Tahmini")
plt.xlabel("Tarih")
plt.ylabel("Satış")
plt.show()
```

**Açıklama:**
- Siyah noktalar: Gerçek veriler
- Mavi çizgi: Tahmin
- Açık mavi alan: Güven aralığı

### Bileşenleri Görselleştirme

```python
fig2 = model.plot_components(tahmin)
plt.show()
```

**Açıklama:**
- **trend**: Genel eğilim
- **weekly**: Haftalık mevsimsellik
- **yearly**: Yıllık mevsimsellik

---

## 8. İleri Seviye Görselleştirme: Özelleştirilmiş Grafikler

```python
import matplotlib.pyplot as plt

# Sadece tahmin edilen kısmı çizme
gelecek_tarihler = tahmin[tahmin['ds'] > '2023-12-31']

plt.figure(figsize=(12, 6))
plt.plot(df['ds'], df['y'], 'o', label='Gerçek Veri', markersize=3)
plt.plot(gelecek_tarihler['ds'], gelecek_tarihler['yhat'], 'r-', label='Tahmin', linewidth=2)
plt.fill_between(gelecek_tarihler['ds'], 
                 gelecek_tarihler['yhat_lower'], 
                 gelecek_tarihler['yhat_upper'], 
                 alpha=0.3, label='Güven Aralığı')
plt.legend()
plt.title("Gelecek 60 Gün Satış Tahmini")
plt.xlabel("Tarih")
plt.ylabel("Satış")
plt.grid(True)
plt.show()
```

---

## 9. Gerçek Hayat Örneği: Elektrik Tüketimi Tahmini

```python
from prophet import Prophet
import pandas as pd
import numpy as np

# 2 yıllık günlük elektrik tüketimi (kWh)
tarihler = pd.date_range('2022-01-01', '2023-12-31', freq='D')
ay = tarihler.month
# Yaz aylarında klima kullanımı artar
tuketim = 50 + np.where((ay >= 6) & (ay <= 8), 30, 0) + np.random.randn(len(tarihler)) * 5

df = pd.DataFrame({'ds': tarihler, 'y': tuketim})

model = Prophet(yearly_seasonality=True, weekly_seasonality=True)
model.fit(df)

# Gelecek 3 ay tahmini
gelecek = model.make_future_dataframe(periods=90)
tahmin = model.predict(gelecek)

# Görselleştirme
fig = model.plot(tahmin)
plt.title("Elektrik Tüketimi Tahmini (3 Ay)")
plt.ylabel("Tüketim (kWh)")
plt.show()

fig2 = model.plot_components(tahmin)
plt.show()
```

---

## 10. Gerçek Hayat Örneği: Online Satış Tahmini (E-Ticaret)

```python
from prophet import Prophet
import pandas as pd
import numpy as np

# 18 aylık günlük online satış verisi
tarihler = pd.date_range('2023-01-01', '2024-06-30', freq='D')
hafta_gunu = tarihler.dayofweek

# Hafta sonu satışlar daha az, hafta içi artıyor
# Genel trend yukarı
satislar = (200 + np.arange(len(tarihler)) * 0.5 + 
            np.where(hafta_gunu >= 5, -30, 10) + 
            np.random.randn(len(tarihler)) * 20)

df = pd.DataFrame({'ds': tarihler, 'y': satislar})

# Kampanya günleri (Black Friday, Ramazan Bayramı vb.)
kampanyalar = pd.DataFrame({
    'holiday': 'kampanya',
    'ds': pd.to_datetime(['2023-11-24', '2024-04-10']),
    'lower_window': 0,
    'upper_window': 2,
})

# Kampanya günlerinde satışları artır
for tarih in kampanyalar['ds']:
    df.loc[df['ds'] == tarih, 'y'] += 200

model = Prophet(holidays=kampanyalar, weekly_seasonality=True)
model.fit(df)

# 60 gün tahmini
gelecek = model.make_future_dataframe(periods=60)
tahmin = model.predict(gelecek)

# Görselleştirme
fig = model.plot(tahmin)
plt.title("E-Ticaret Günlük Satış Tahmini")
plt.ylabel("Satış Adedi")
plt.show()

# Bileşenler
fig2 = model.plot_components(tahmin)
plt.show()

# Gelecek ayın toplam tahmini
gelecek_ay = tahmin[tahmin['ds'] >= '2024-07-01']
print("Gelecek 60 günün tahmini toplam satış:", gelecek_ay['yhat'].sum())
```

---

## 11. Model Performansını Değerlendirme

```python
from sklearn.metrics import mean_absolute_error, mean_squared_error
import numpy as np

# Test verisi ayırma
train = df[df['ds'] < '2024-05-01']
test = df[df['ds'] >= '2024-05-01']

model = Prophet()
model.fit(train)

gelecek = model.make_future_dataframe(periods=len(test))
tahmin = model.predict(gelecek)

# Test setindeki tahminler
tahmin_test = tahmin[tahmin['ds'] >= '2024-05-01']

mae = mean_absolute_error(test['y'], tahmin_test['yhat'])
rmse = np.sqrt(mean_squared_error(test['y'], tahmin_test['yhat']))

print(f"Ortalama Mutlak Hata (MAE): {mae:.2f}")
print(f"Kök Ortalama Kare Hata (RMSE): {rmse:.2f}")
```

---

## 12. Kapanış ve Ödevler

**Özet:**
- Facebook Prophet zaman serisi tahmini için güçlü ve kolay bir araçtır.
- Trend, mevsimsellik, tatiller otomatik olarak işlenir.
- Görselleştirme araçları ile tahminleri kolayca analiz edebilirsiniz.

**Ödevler:**
1. Kendi günlük adım sayınızı, su tüketiminizi veya harcamalarınızı kaydedin ve Prophet ile gelecek hafta tahminini yapın.
2. Bir işletmenin aylık satışlarını içeren veri seti bulun (Kaggle'dan) ve 6 ay ilerisi tahmin edin.
3. Tatil günlerini ekleyerek model performansını karşılaştırın.
4. Model bileşenlerini (trend, mevsimsellik) görselleştirip yorumlayın.

**Kaynaklar:**
- [Prophet Resmi Dokümantasyon](https://facebook.github.io/prophet/)
- [Prophet Quick Start](https://facebook.github.io/prophet/docs/quick_start.html)
- [Kaggle Zaman Serisi Veri Setleri](https://www.kaggle.com/datasets?search=time+series)

---