# NumPy vs Pandas: Genel Karşılaştırma Tablosu

## 📊 Temel Özellikler Karşılaştırması

| Özellik | NumPy | Pandas |
|---------|-------|--------|
| **Ana Amaç** | Sayısal hesaplamalar | Veri analizi ve manipülasyonu |
| **Temel Veri Yapısı** | ndarray (N-boyutlu dizi) | Series (1D), DataFrame (2D) |
| **Veri Tipi** | Homojen (tek tip) | Heterojen (çok tip) |
| **İndeksleme** | Sayısal (0, 1, 2, ...) | Etiketli (isim, tarih, vb.) |
| **Eksik Veri** | Zayıf destek (NaN) | Güçlü destek (NaN, None) |
| **Performans** | Çok hızlı | NumPy üzerine kurulu (biraz yavaş) |
| **Kullanım Alanı** | Matematik, lineer cebir | Veri analizi, iş zekası |
| **Dosya I/O** | Sınırlı | Excel, CSV, SQL, JSON vb. |
| **Bellek Kullanımı** | Optimize edilmiş | Daha fazla bellek kullanır |
| **Kurulum** | `pip install numpy` | `pip install pandas` |
| **Temel Import** | `import numpy as np` | `import pandas as pd` |

## 🎯 Performans Değerlendirmesi

| Kriter | NumPy | Pandas |
|--------|-------|--------|
| **Hız** | ⚡⚡⚡⚡⚡ (Çok Hızlı) | ⚡⚡⚡⚡ (Hızlı) |
| **Esneklik** | ⭐⭐⭐ (Orta) | ⭐⭐⭐⭐⭐ (Çok Esnek) |
| **Veri Analizi** | ⭐⭐ (Temel) | ⭐⭐⭐⭐⭐ (Gelişmiş) |
| **Matematik İşlemleri** | ⭐⭐⭐⭐⭐ (Mükemmel) | ⭐⭐⭐ (İyi) |
| **Dosya İşlemleri** | ⭐⭐ (Sınırlı) | ⭐⭐⭐⭐⭐ (Kapsamlı) |
| **Öğrenme Eğrisi** | Orta | Orta-Zor |

## 📁 Desteklenen Dosya Formatları

| Format | NumPy | Pandas |
|--------|-------|--------|
| **CSV** | ✅ (Temel) | ✅ (Gelişmiş) |
| **Excel** | ❌ | ✅ |
| **JSON** | ❌ | ✅ |
| **SQL** | ❌ | ✅ |
| **HTML** | ❌ | ✅ |
| **Pickle** | ✅ | ✅ |
| **HDF5** | ✅ | ✅ |
| **Parquet** | ❌ | ✅ |
| **.npy/.npz** | ✅ | ❌ |

## 🔧 Temel Fonksiyon Karşılaştırması

| İşlem | NumPy | Pandas |
|-------|-------|--------|
| **Ortalama** | `arr.mean()` | `df.mean()` veya `series.mean()` |
| **Medyan** | `np.median(arr)` | `df.median()` |
| **Standart Sapma** | `arr.std()` | `df.std()` |
| **Maksimum** | `arr.max()` | `df.max()` |
| **Minimum** | `arr.min()` | `df.min()` |
| **Toplam** | `arr.sum()` | `df.sum()` |
| **Sıralama** | `np.sort(arr)` | `df.sort_values()` |
| **Benzersiz Değerler** | `np.unique(arr)` | `df.unique()` veya `df.nunique()` |
| **Gruplama** | ❌ | `df.groupby()` |
| **Pivot** | ❌ | `df.pivot_table()` |

## 💡 Ne Zaman Kullanmalı?

### NumPy İçin İdeal Durumlar

| Durum | Açıklama |
|-------|----------|
| ✅ Matematiksel hesaplamalar | Lineer cebir, matris işlemleri |
| ✅ Yüksek performans gerekli | Milyonlarca elemanlı diziler |
| ✅ Homojen veri | Tüm elemanlar aynı tip |
| ✅ Çok boyutlu veriler | 3D, 4D diziler |
| ✅ Bilimsel hesaplamalar | Fizik, mühendislik simülasyonları |
| ✅ Görüntü işleme | Piksel dizileri |

### Pandas İçin İdeal Durumlar

| Durum | Açıklama |
|-------|----------|
| ✅ Tablo formatında veri | Satır-sütun yapısı |
| ✅ Farklı veri tipleri | String, sayı, tarih karışık |
| ✅ Etiketli veri | İsim, tarih indeksleri |
| ✅ Eksik veri çok | NaN yönetimi önemli |
| ✅ Dosya okuma/yazma | CSV, Excel, SQL |
| ✅ Veri temizleme | Filtreleme, dönüştürme |
| ✅ Zaman serisi analizi | Tarihsel veriler |
| ✅ İş zekası raporları | Özet tablolar, pivot |

## 🔄 Dönüşüm İşlemleri

| Dönüşüm | Kod |
|---------|-----|
| **NumPy → Pandas** | `pd.DataFrame(numpy_array)` |
| **Pandas → NumPy** | `df.values` veya `df.to_numpy()` |
| **List → NumPy** | `np.array(liste)` |
| **List → Pandas** | `pd.Series(liste)` veya `pd.DataFrame(liste)` |

## 📚 Bağımlılıklar

| Kütüphane | NumPy'ye Bağımlı | Pandas'a Bağımlı |
|-----------|------------------|------------------|
| **Pandas** | ✅ Evet | - |
| **Matplotlib** | ✅ Evet | ❌ Hayır |
| **Scikit-learn** | ✅ Evet | ❌ Hayır (opsiyonel) |
| **TensorFlow** | ✅ Evet | ❌ Hayır |
| **SciPy** | ✅ Evet | ❌ Hayır |

## 🎯 Kullanım Senaryoları Örnekleri

| Senaryo | Önerilen Kütüphane |
|---------|-------------------|
| Makine öğrenmesi veri hazırlama | **Pandas** |
| Derin öğrenme veri işleme | **NumPy** |
| Excel raporları oluşturma | **Pandas** |
| Sinir ağı ağırlık matrisleri | **NumPy** |
| Müşteri veri analizi | **Pandas** |
| Görüntü filtresi uygulama | **NumPy** |
| Satış verilerini gruplama | **Pandas** |
| Fourier dönüşümü | **NumPy** |
| SQL veritabanı entegrasyonu | **Pandas** |
| Matris çarpımı | **NumPy** |

---

**Hazırlayan:** @haksaya  
**Tarih:** 2025-10-30  
**Versiyon:** 1.0