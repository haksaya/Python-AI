# Facebook Prophet Nedir?

**Facebook Prophet**, gelecekteki değerleri tahmin etmek için kullanılan bir **zaman serisi tahmin aracıdır**.

---

## Basit Anlatımla

Prophet, **geçmiş verilere bakarak geleceği tahmin eden** bir Python kütüphanesidir. Facebook (Meta) tarafından geliştirilmiştir.

---

## Ne İşe Yarar?

Elimizde **tarihe bağlı veriler** varsa (günlük, haftalık, aylık), Prophet bu verilerdeki örüntüleri öğrenerek **gelecekte ne olacağını tahmin eder**.

---

## Gündelik Hayattan Örnekler

- **Market sahibisiniz** → Geçmiş satış verilerinize bakarak gelecek ay kaç ürün satacağınızı tahmin eder
- **Elektrik faturalarınız** → Geçmiş aylara bakarak önümüzdeki ay ne kadar fatura geleceğini tahmin eder
- **Web siteniz var** → Geçmiş ziyaretçi sayılarına bakarak gelecek hafta kaç kişi geleceğini tahmin eder
- **Restoran işletiyorsunuz** → Hangi günler daha kalabalık olacağını tahmin eder

---

## Neden Kullanışlıdır?

✅ **Çok kolay kullanım** - Karmaşık istatistik bilgisi gerektirmez  
✅ **Otomatik öğrenme** - Haftalık/yıllık tekrar eden örüntüleri kendisi bulur  
✅ **Tatil günlerini anlama** - Bayram, özel günlerin etkisini hesaplar  
✅ **Eksik verileri tolere eder** - Bazı günler veri olmasa da çalışır  

---

## Basit Kullanım Örneği

```python
from prophet import Prophet
import pandas as pd

# Geçmiş satış verileriniz
veri = pd.DataFrame({
    'ds': ['2024-01-01', '2024-01-02', '2024-01-03'],  # Tarihler
    'y': [100, 120, 110]  # Satış miktarları
})

# Model oluştur ve öğret
model = Prophet()
model.fit(veri)

# Gelecek 7 günü tahmin et
gelecek = model.make_future_dataframe(periods=7)
tahmin = model.predict(gelecek)

print(tahmin[['ds', 'yhat']])  # Tahmin sonuçları
```

---

## Prophet'in Temel Özellikleri

### 1. Veri Formatı
Prophet sadece 2 sütun ister:
- **ds**: Tarih sütunu
- **y**: Tahmin edilecek değer

### 2. Otomatik Bileşenler
- **Trend**: Genel yükseliş veya düşüş
- **Mevsimsellik**: Haftalık, aylık, yıllık tekrar eden örüntüler
- **Tatiller**: Özel günlerin etkileri

### 3. Çıktılar
- **yhat**: Tahmin edilen değer
- **yhat_lower**: Alt güven sınırı
- **yhat_upper**: Üst güven sınırı

---

## Özet

**Prophet = Geçmişe bakıp geleceği tahmin eden akıllı asistan** 🔮📈

---

## Kurulum

```bash
pip install prophet
```

---

## Kaynaklar

- [Prophet Resmi Dokümantasyon](https://facebook.github.io/prophet/)
- [Prophet GitHub](https://github.com/facebook/prophet)
- [Prophet Quick Start](https://facebook.github.io/prophet/docs/quick_start.html)

---

**Hazırlayan:** haksayabunu  
