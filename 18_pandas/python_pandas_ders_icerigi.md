# Python'da Pandas Ders İçeriği

Bu ders, Pandas kütüphanesini sıfırdan başlayarak gündelik hayattan örneklerle anlatır. Bol açıklama ve pratik uygulamalar içerir.

---

## 1. Pandas Nedir? Kurulum ve Temel Kavramlar

- Pandas, Python'da veri analizi ve işleme için en çok kullanılan kütüphanedir.
- Tablo (DataFrame) ve dizi (Series) yapısı sunar.
- Büyük ve karmaşık verilerle kolayca çalışmayı sağlar.

**Kurulum:**
```bash
pip install pandas
```

**Kütüphaneyi Kullanma:**
```python
import pandas as pd
print(pd.__version__)
```

---

## 2. Series ve DataFrame Temelleri

### Series Nedir?
- Tek boyutlu, indeksli veri yapısıdır. Listeye benzer ama indekslerle çalışır.
```python
import pandas as pd
meyveler = pd.Series([10, 20, 15], index=["Elma", "Armut", "Muz"])
print(meyveler)
```
- Elma, Armut, Muz adlı ürünlerin satış adetleri tutuldu.

### DataFrame Nedir?
- Satır ve sütunlardan oluşan tablo yapısıdır.
```python
veri = {
    "isim": ["Ali", "Ayşe", "Mehmet"],
    "yas": [25, 30, 22],
    "sehir": ["Ankara", "İstanbul", "İzmir"]
}
df = pd.DataFrame(veri)
print(df)
```
- Her sütun farklı bir özelliği temsil eder (isim, yaş, şehir).

---

## 3. Gündelik Hayattan Series ve DataFrame Örnekleri

### Market Alışverişi
```python
fiyatlar = pd.Series([15, 8, 12, 6], index=["Süt", "Ekmek", "Peynir", "Yumurta"])
print("Alışveriş Listesi:\n", fiyatlar)
print("Toplam harcama:", fiyatlar.sum())
```
- Her ürünün fiyatı ve toplam harcama kolayca hesaplanabilir.

### Sınıf Notları Tablosu
```python
notlar = {
    "Öğrenci": ["Ali", "Ayşe", "Mehmet", "Zeynep"],
    "Matematik": [80, 90, 70, 85],
    "Fizik": [75, 85, 65, 95]
}
df_notlar = pd.DataFrame(notlar)
print(df_notlar)
print("Matematik ortalaması:", df_notlar["Matematik"].mean())
```
- Öğrencilerin ders notları tablo şeklinde tutuldu ve ortalamaları alındı.

---

## 4. Veri Okuma ve Yazma (CSV, Excel, TXT)

### CSV Dosyası Okuma/Yazma
```python
# Kaydetme
df_notlar.to_csv("notlar.csv", index=False)

# Okuma
df_yeni = pd.read_csv("notlar.csv")
print(df_yeni)
```

### Excel Dosyası Okuma/Yazma
```python
df_notlar.to_excel("notlar.xlsx", index=False)
df_yeni = pd.read_excel("notlar.xlsx")
print(df_yeni)
```

### TXT (Düz Metin) Dosya Okuma
```python
df = pd.read_csv("veri.txt", delimiter="\t")  # Tab ile ayrılmışsa
```

**Gündelik Hayat Örneği:**  
Bir marketin günlük satışlarını CSV’den oku, toplam satışı yazdır.

---

## 5. Veri İnceleme ve Temel Analiz

### İlk ve Son Satırları Görme
```python
print(df.head())    # İlk 5 satır
print(df.tail())    # Son 5 satır
```

### Veri Yapısı ve Özeti
```python
print(df.shape)         # Satır ve sütun sayısı
print(df.info())        # Veri tipi ve eksik veri bilgisi
print(df.describe())    # Sayısal sütunlar için özet istatistikler
```

### Sütunlara ve Satırlara Erişim
```python
print(df["isim"])               # Bir sütunu seçmek
print(df[["isim", "yas"]])      # Birden fazla sütun
print(df.iloc[0])               # İlk satır (konum bazlı)
print(df.loc[0])                # İlk satır (etiket bazlı)
```

---

## 6. Filtreleme, Sıralama ve Seçim

### Koşullu Filtreleme
```python
print(df[df["yas"] > 25])      # Yaşı 25'ten büyük olanlar
```

### Sıralama
```python
print(df.sort_values("yas"))   # Yaşa göre artan sıralama
print(df.sort_values("isim", ascending=False))  # İsme göre azalan
```

### Değerleri Değiştirme
```python
df.loc[df["isim"] == "Ali", "yas"] = 26
```

**Gündelik Hayat Örneği:**  
Bir sınıfta 60’tan düşük not alan öğrencileri bul.

---

## 7. Eksik ve Hatalı Verilerle Çalışmak

### Eksik Değerleri Bulma ve Doldurma
```python
df = pd.DataFrame({
    "isim": ["Ali", "Ayşe", "Veli"],
    "yas": [25, None, 22]
})
print(df.isnull())          # Eksik değerleri göster
df["yas"].fillna(df["yas"].mean(), inplace=True)
```

### Değer Silme
```python
df.dropna(inplace=True)        # Eksik satırları sil
```

### Hatalı/Alakasız Verileri Temizleme
```python
df = df[df["yas"] > 0]        # 0'dan büyük yaşlar
```

---

## 8. Yeni Sütun Ekleme ve Hesaplama

### Basit Hesaplama
```python
df["doğum_yılı"] = 2025 - df["yas"]
```

### Koşullu Sütun
```python
df["kategori"] = df["yas"].apply(lambda x: "Genç" if x < 30 else "Orta-Yaş")
```

**Gündelik Hayat Örneği:**  
Aldığınız ürünlerin adet ve birim fiyat bilgisinden toplam tutar sütunu üretin.

---

## 9. Gruplama ve Toplu İşlemler (GroupBy)

### Gruplama
```python
veri = {
    "Mağaza": ["A", "B", "A", "B", "A"],
    "Satış": [100, 150, 200, 180, 120]
}
df = pd.DataFrame(veri)
print(df.groupby("Mağaza")["Satış"].sum())
```
- Mağaza bazında toplam satışlar alındı.

### Çoklu Gruplama
```python
veri = {
    "Şehir": ["Ankara", "Ankara", "İstanbul", "İstanbul"],
    "Ürün": ["Süt", "Ekmek", "Süt", "Ekmek"],
    "Satış": [100, 200, 150, 300]
}
df = pd.DataFrame(veri)
print(df.groupby(["Şehir", "Ürün"])["Satış"].sum())
```
- Hem şehir hem ürün bazında gruplayıp topladık.

---

## 10. Pivot Tablolar ve Özetleme

### Pivot Tablo Oluşturma
```python
pivot = df.pivot_table(values="Satış", index="Şehir", columns="Ürün", aggfunc="sum")
print(pivot)
```
- Şehir ve ürün bazında tablo (Excel’deki gibi).

### Özetleme Fonksiyonları
```python
print(df["Satış"].agg(["sum", "mean", "max"]))
```

---

## 11. Zaman Serileri ve Tarih ile Çalışmak

### Tarih Sütunu Tanıma
```python
df["Tarih"] = pd.to_datetime(df["Tarih"])
```

### Zaman Serisi Analizi
```python
df = pd.DataFrame({
    "Tarih": pd.date_range("2025-01-01", periods=7, freq="D"),
    "Satış": [100, 150, 200, 120, 180, 140, 160]
})
df.set_index("Tarih", inplace=True)
print(df.resample("W").sum())  # Haftalık toplam satış
```

**Gündelik Hayat Örneği:**  
Aylık elektrik faturalarını zaman serisi olarak analiz edin.

---

## 12. Veri Birleştirme (Join, Merge, Concat)

### Birleştirme (merge)
```python
musteriler = pd.DataFrame({
    "id": [1, 2, 3],
    "isim": ["Ali", "Ayşe", "Mehmet"]
})
siparisler = pd.DataFrame({
    "musteri_id": [1, 2, 1, 3],
    "tutar": [50, 100, 75, 60]
})
sonuc = pd.merge(musteriler, siparisler, left_on="id", right_on="musteri_id")
print(sonuc)
```

### Concatenation (Yan yana veya alt alta ekleme)
```python
df1 = pd.DataFrame({"A": [1,2], "B": [3,4]})
df2 = pd.DataFrame({"A": [5,6], "B": [7,8]})
print(pd.concat([df1, df2], ignore_index=True))
```

---

## 13. String ve Kategorik Verilerle Çalışmak

### Metin Fonksiyonları
```python
df = pd.DataFrame({"isim": ["ali", "Ayşe", "MEHMET"]})
df["isim"] = df["isim"].str.capitalize()
print(df)
```

### Kategorik Dönüşümler
```python
df = pd.DataFrame({"cinsiyet": ["Erkek", "Kadın", "Kadın", "Erkek"]})
df["cinsiyet"] = df["cinsiyet"].astype("category")
print(df["cinsiyet"].value_counts())
```

---

## 14. Veri Görselleştirme (Matplotlib ile Entegrasyon)

### Basit Grafikler
```python
import matplotlib.pyplot as plt
df = pd.DataFrame({"Gün": ["Pzt", "Sal", "Çar", "Per", "Cum"], "Satış": [100, 120, 90, 110, 150]})
df.plot(x="Gün", y="Satış", kind="bar")
plt.show()
```
- Haftalık satışlar çubuk grafikle gösterildi.

---

## 15. Gerçek Hayat Proje: Kişisel Bütçe Analizi

### Adım Adım Proje
1. **Veri Toplama:** 1 ay boyunca günlük harcamalarınızı Excel veya CSV’ye kaydedin.
2. **Veri Okuma:** Pandas ile veriyi okuyun.
3. **Veri Analizi:** Toplam, ortalama, kategori bazında harcamalar, en fazla harcama yapılan gün vs.
4. **Filtreleme:** Belirli bir kategoriye veya haftaya göre harcamaları bulun.
5. **Görselleştirme:** Günlük/haftalık harcamaları grafikle gösterin.
```python
# Örnek veri yükleme
df = pd.read_csv("butce.csv")
print(df.groupby("Kategori")["Tutar"].sum())
```

---

## 16. Sık Karşılaşılan Hatalar ve İpuçları

- Eksik veri, veri tipi uyumsuzluğu, dosya yolu hatası gibi temel sorunlar ve çözümleri.
- DataFrame kopyalama (`.copy()`), inplace işlemler, veri tipleri dönüşümü.

---

## 17. Kapanış ve Ödevler

- Pandas ile kendi gündelik verinizi analiz edin (alışveriş, bütçe, egzersiz, vb.).
- CSV veya Excel’den veri okuyup analiz ve görselleştirme yapın.
- Kendi küçük projenizi tasarlayın (ör: evdeki kitap, film, harcama arşivi).

**Kaynaklar:**
- Pandas Dokümantasyon: https://pandas.pydata.org/pandas-docs/stable/
- Pandas Getting Started: https://pandas.pydata.org/pandas-docs/stable/getting_started/index.html
- Matplotlib: https://matplotlib.org/stable/tutorials/introductory/pyplot.html

---