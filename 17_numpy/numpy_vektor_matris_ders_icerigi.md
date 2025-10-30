# Python'da NumPy – Basit, Açıklamalı ve Gündelik Hayattan Örneklerle Ders İçeriği

Bu ders, NumPy kütüphanesini sıfırdan başlayarak gündelik hayattan örneklerle anlatır. Her bölüm bol açıklama ve gerçek yaşamdan örnekler içerir.

---

## 1. NumPy Nedir? Giriş ve Kurulum

- NumPy, Python’da hızlı ve verimli bilimsel hesaplama için kullanılır.
- Temel veri yapısı: ndarray (n-boyutlu dizi).
- Neden NumPy?
  - Büyük veriyle hızlı çalışır.
  - Döngü yazmadan toplu işlemler yapılabilir.
  - Listelere göre çok daha hızlıdır.

**Kurulum ve ilk kullanım:**
```python
import numpy as np
print(np.__version__)  # NumPy sürümünü yazdırır
```

**Günlük Hayattan Örnek:**  
Market alışverişindeki ürün fiyatlarını bir diziye koyup toplam harcamayı hesaplamak.

```python
urun_fiyatlari = np.array([15, 10, 8, 12])
print("Toplam harcama:", urun_fiyatlari.sum())
```
- Bir NumPy dizisi oluşturduk, içinde ürün fiyatları var.
- `.sum()` ile toplamı aldık.

---

## 2. NumPy Dizileri (Array) ve Vektörler

- NumPy ile tek boyutlu ve çok boyutlu diziler oluşturulabilir.
- Vektör = Tek boyutlu dizi.
- Matris = İki boyutlu dizi.

**Dizi oluşturma:**
```python
a = np.array([1, 2, 3])
b = np.arange(5)          # [0 1 2 3 4]
c = np.linspace(0, 1, 5)  # [0.  0.25 0.5 0.75 1.]
```

**Günlük Hayattan Örnek:**  
Bir hafta boyunca her gün kaç adım attığınızı kaydetmek.
```python
adimlar = np.array([3500, 7000, 5000, 8500, 10000, 3000, 4000])
print("Toplam adım:", adimlar.sum())
print("Ortalama adım:", adimlar.mean())
```
- Haftalık adım sayısını bir diziye koyduk.
- `.sum()` ile toplamı, `.mean()` ile ortalamayı bulduk.

**Dilimleme ve indeksleme:**
```python
print(adimlar[0])     # Pazartesi adımı
print(adimlar[-1])    # Pazar adımı
print(adimlar[2:5])   # 3. ve 5. günler arası adımlar
```

**Alıştırma:**  
Bir haftalık su tüketiminizi (litre cinsinden) bir vektöre girin ve toplam ile ortalamayı bulun.

---

## 3. Vektörel İşlemler

- NumPy ile vektörler üzerinde toplama, çıkarma, çarpma, bölme gibi işlemler döngü olmadan yapılır.

**Günlük Hayattan Örnek:**  
Haftalık harcamalarınızın üstüne her gün için 5 TL indirim uygulama.
```python
harcamalar = np.array([30, 22, 18, 25, 40, 35, 28])
indirimli = harcamalar - 5
print("İndirimli harcamalar:", indirimli)
```
- Her harcamadan 5 TL çıkardık.

**Farklı dizilerle işlem:**
Arkadaşınızın adım sayısı ile kendi adım sayınızı toplayıp toplam adımı bulun.
```python
adimlar_sen = np.array([3500, 7000, 5000, 8500, 10000, 3000, 4000])
adimlar_arkadas = np.array([4000, 6500, 6000, 9000, 8500, 3200, 4100])
toplam_adim = adimlar_sen + adimlar_arkadas
print("Günlük toplam adımlar:", toplam_adim)
```

**Dot product (noktasal çarpım):**  
Her gün harcanan kalori ve adım sayısını çarpıp haftalık toplam enerji harcaması.
```python
adimlar = np.array([3500, 7000, 5000, 8500, 10000, 3000, 4000])
kalori = np.array([0.03, 0.04, 0.035, 0.038, 0.032, 0.029, 0.031])
enerji = adimlar @ kalori
print("Toplam enerji harcaması:", enerji)
```
- Her gün adım ve kalori katsayısını çarpıp topladık.

**Alıştırma:**  
Bir haftalık elektrik tüketiminize zam oranı (örneğin %8) ekleyerek yeni tutarları hesaplayın.

---

## 4. Boolean Maske ve Filtreleme

- NumPy ile filtreleme yapmak çok kolaydır.

**Günlük Hayattan Örnek:**  
Bir sınıfta 10 öğrencinin notlarını girip, sadece geçenleri (>=50) bulmak.
```python
notlar = np.array([45, 67, 89, 30, 56, 78, 90, 40, 50, 60])
gecenler = notlar >= 50
print("Geçenlerin notları:", notlar[gecenler])
```
- `notlar >= 50` ile geçenleri seçtik.

**Alıştırma:**  
Bir hafta boyunca gün gün harcadığınız parayı bir diziye girin. Sadece 20 TL’den fazla harcamaları listeleyin.

---

## 5. NumPy Matrisleri ve 2D Diziler

- Matris: Satır ve sütunlardan oluşan 2 boyutlu dizi.

**Oluşturma:**
```python
A = np.array([[1, 2, 3],
              [4, 5, 6]])
```

**Günlük Hayattan Örnek:**  
3 ürünün 4 gün boyunca marketteki fiyatlarını tablo halinde tutmak.
```python
fiyatlar = np.array([[15, 16, 15, 17],   # Süt fiyatları
                     [5, 6, 5, 6],      # Ekmek fiyatları
                     [20, 18, 19, 20]]) # Yumurta fiyatları
```
- Satırlar ürünleri, sütunlar günleri temsil ediyor.

**Satır ve sütun toplamları:**
```python
urun_toplam = fiyatlar.sum(axis=1)
gun_toplam = fiyatlar.sum(axis=0)
print("Her ürünün toplamı:", urun_toplam)
print("Her günün toplamı:", gun_toplam)
```
- `axis=1` ile satır, `axis=0` ile sütun bazında topladık.

**Alıştırma:**  
Bir matris oluşturun (ör: 5 öğrencinin 3 sınav notu). Her öğrencinin ortalamasını ve en yüksek notunu bulun.

---

## 6. Matris Metotları: Toplama, Ortalama, Transpoz, Çarpım

**Toplam, Ortalama, Maksimum, Minimum:**
```python
A = np.array([[1, 2, 3],
              [4, 5, 6]])
print(A.sum())           # Tüm elemanların toplamı
print(A.mean())          # Tüm elemanların ortalaması
print(A.max())           # En büyük değer
print(A.min())           # En küçük değer
print(A.sum(axis=0))     # Sütunların toplamı
print(A.mean(axis=1))    # Satırların ortalaması
```

**Günlük Hayattan Örnek:**  
Bir ay boyunca 4 haftalık su tüketiminizi tabloya girip, her haftanın toplamını ve ortalamasını bulun.
```python
su = np.array([[2, 2.5, 3, 2.8, 2.2, 2.4, 2.6],     # 1. hafta
               [2.1, 2.3, 2.7, 2.5, 2.2, 2.0, 2.8], # 2. hafta
               [2.9, 2.7, 2.8, 2.6, 2.4, 2.7, 2.5], # 3. hafta
               [2.5, 2.6, 2.5, 2.3, 2.4, 2.2, 2.1]])# 4. hafta
hafta_toplam = su.sum(axis=1)
hafta_ortalama = su.mean(axis=1)
print("Hafta toplamları:", hafta_toplam)
print("Hafta ortalamaları:", hafta_ortalama)
```

**Transpoz (satır/sütun yer değiştirme):**
```python
print("Transpoz:\n", su.T)
```

**Matris çarpımı:**
```python
A = np.array([[1, 2],
              [3, 4]])
B = np.array([[2, 0],
              [1, 2]])
C = A @ B
print("Matris çarpımı:\n", C)
```

**Alıştırma:**  
Bir 4x2 matris oluşturun (ör: 4 kişinin 2 farklı günde yaptığı spor dakikası), toplamları ve ortalamaları bulun.

---


## 7. NumPy'da Rastgele Sayılar ve Basit İstatistik

**Rastgele dizi ve matris oluşturma:**
```python
rastgele_v = np.random.randint(1, 100, size=10)  # 1-99 arası 10 sayı
rastgele_m = np.random.rand(3, 4)                # 3x4 matris, [0,1) arası
print("Rastgele vektör:", rastgele_v)
print("Rastgele matris:\n", rastgele_m)
```

**Basit istatistikler:**
```python
print("En büyük değer:", rastgele_v.max())
print("En küçük değer:", rastgele_v.min())
print("Ortalama:", rastgele_v.mean())
print("Standart sapma:", rastgele_v.std())
```

**Alıştırma:**  
20 günlük sıcaklıkları rastgele oluşturun. En sıcak ve en soğuk günü bulun.

---

## 8. Gerçek Hayat Mini Proje

**Proje:** 1 ay boyunca günlük harcamalarınızı kaydedin, haftalık toplamları ve en fazla harcama yapılan günü bulun.

```python
harcamalar = np.array([55, 40, 60, 70, 45, 30, 50, 65, 80, 35, 60, 75, 40, 55, 60, 70, 45, 50, 65, 80, 35, 60, 75, 40, 55, 60, 70, 45, 50, 65])
hafta_toplamlari = harcamalar.reshape(4, 7).sum(axis=1)
print("Haftalık harcamalar:", hafta_toplamlari)
gun_index = harcamalar.argmax()
print("En fazla harcama yapılan gün:", gun_index + 1, "->", harcamalar[gun_index], "TL")
```
- 1 ayı (30 gün) 4 haftaya böldük (`reshape(4,7)`).
- Her haftanın toplamını aldık.
- En fazla harcamanın yapıldığı günü bulduk.

**Proje Alıştırması:**
- Bir ay boyunca günlük adım, su tüketimi ve harcama verilerini 3 farklı vektörde tutun. Haftalık ortalamaları ve en yüksek değerleri bulun.

---

## 9. Kapanış ve Öneriler

**Özet:**
- NumPy ile vektör ve matrisler kolayca oluşturulur.
- Toplama, ortalama, maksimum, minimum, filtreleme, çarpım gibi işlemler çok hızlıdır.
- Gerçek yaşamda veri analizi ve hızlı hesaplamalar için NumPy çok faydalıdır.

**Ödev (isteğe bağlı):**
- Kendi günlük, haftalık veya aylık verinizi NumPy ile analiz edin.
- Matrislerde toplam, ortalama, transpoz, çarpım gibi işlemleri uygulayın.
- Rastgele veri üreterek istatistikler çıkarın.

**Kaynaklar:**
- NumPy Dokümantasyon: https://numpy.org/doc/
- NumPy Başlangıç: https://numpy.org/doc/stable/user/absolute_beginners.html
