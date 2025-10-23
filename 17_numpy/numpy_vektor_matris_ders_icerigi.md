# NumPy ile Vektör ve Matris İşlemleri Ders İçeriği


---

## 1) NumPy Nedir?

- NumPy, Python’da sayısal işlemler için en popüler kütüphanedir.
- En önemli özelliği: **Dizi (array) ve matris** işlemlerini hızlı ve kolayca yapabilmek.
- Listelere göre çok daha hızlıdır ve büyük verilerle çalışmak için idealdir.

**Kurulum:**
```python
import numpy as np
```
Bu satır NumPy kütüphanesini kullanmak için içe aktarır.

**Günlük Hayattan Örnek:**
Bir markette aldığınız ürünlerin fiyatlarının listesini tutmak ve toplam harcamanızı hesaplamak istiyorsunuz.

```python
urun_fiyatlari = np.array([25, 15, 30, 10])
print(urun_fiyatlari)
```
- Bir NumPy dizisi oluşturduk, içinde market ürünlerinin fiyatları var.
- Diziyi ekrana yazdırdık.

**Toplam harcama:**
```python
print("Toplam harcama:", urun_fiyatlari.sum())
```
- `.sum()` ile dizi içindeki tüm fiyatları topladık.

---

## 2) Vektörel İşlemler Nedir?

- NumPy ile **vektör** gibi tek boyutlu diziler üzerinde toplama, çıkarma, çarpma, bölme gibi işlemleri tek adımda yapabilirsin.
- Tüm elemanlara **tek seferde** işlem uygulanır, döngü gerekmez.

**Günlük Hayattan Örnek:**
Bir haftalık hava sıcaklıklarını ve nem oranlarını tutup, bunların toplamlarını ve ortalamalarını bulmak.

```python
gunler = np.array(["Pazartesi", "Salı", "Çarşamba", "Perşembe", "Cuma"])
sicakliklar = np.array([18, 20, 22, 19, 21])
nemler = np.array([65, 60, 55, 70, 68])

print("Haftalık ortalama sıcaklık:", sicakliklar.mean())
print("Haftalık toplam nem:", nemler.sum())
```
- `gunler`: Gün isimleri için bir NumPy dizisi (string tipinde, işlemlerde kullanmayacağız).
- `sicakliklar`: Her günün sıcaklık değeri (derece).
- `nemler`: Her günün nem oranı (%).
- `.mean()` ile sıcaklıkların ortalamasını bulduk.
- `.sum()` ile nemlerin toplamını bulduk.

**Vektörler arası işlem (örnek):**
Haftanın her günü için “hissedilen sıcaklığı” sıcaklık ve nemden hesaplayalım (kabaca):
```python
hissedilen = sicakliklar + (nemler / 100)
print("Hissedilen sıcaklıklar:", hissedilen)
```
- Nem oranını 100’e bölerek sıcaklığa ekledik. Her gün için yeni bir değer oluştu.

**Alıştırma:**
- Bir hafta boyunca spor yaptığınız dakikaları bir diziye girin. Haftalık toplam ve ortalama süreyi bulun.

---

## 3) NumPy Vektörleri

- **Vektör:** Tek boyutlu NumPy dizisidir.
- NumPy ile farklı şekillerde vektör oluşturabilirsin.

**Günlük Hayattan Örnek:**
Bir sınıftaki öğrencilerin sınav notlarını kaydedip, kimlerin geçtiğini bulmak.

```python
sinav_notlari = np.array([45, 67, 89, 30, 56, 78, 90])
print("Sınav notları:", sinav_notlari)
```
- Sınıftaki öğrencilerin notlarını bir NumPy dizisine aktardık.

**Geçen öğrenciler:**
```python
gecenler = sinav_notlari >= 50
print("Geçenler (True/False):", gecenler)
print("Geçenlerin notları:", sinav_notlari[gecenler])
```
- `sinav_notlari >= 50` ile 50 ve üzeri notları geçen olarak işaretledik (Boolean maske).
- `sinav_notlari[gecenler]` ile sadece geçenlerin notlarını aldık.

**En yüksek notu bulma:**
```python
print("En yüksek not:", sinav_notlari.max())
```
- `.max()` ile en yüksek değeri bulduk.

**Alıştırma:**
- 10 kişinin adım sayısını bir NumPy dizisine girin. 8000 adımdan fazla atanların adım sayılarını yazdırın.

---

## 4) NumPy Matrisleri

- **Matris:** İki boyutlu NumPy dizisidir. Satır ve sütunlardan oluşur.

**Günlük Hayattan Örnek:**
Bir haftalık market alışverişinizin ürün bazında fiyat listesini tablo halinde tutmak.

| Ürünler   | Pazartesi | Salı | Çarşamba |
|-----------|-----------|------|----------|
| Süt       | 15        | 16   | 15       |
| Ekmek     | 5         | 6    | 5        |
| Yumurta   | 20        | 18   | 19       |

```python
fiyatlar = np.array([[15, 16, 15],
                     [5, 6, 5],
                     [20, 18, 19]])
print("Market fiyatları matrisi:\n", fiyatlar)
```
- 3 ürün ve 3 günün fiyatlarını tablo halinde bir NumPy matrisine aktardık.

**Her ürünün haftalık toplam maliyeti:**
```python
urun_toplam = fiyatlar.sum(axis=1)
print("Her ürünün haftalık toplam maliyeti:", urun_toplam)
```
- `axis=1` ile satır bazında topladık (her ürünün toplamı).

**Her günün toplam harcaması:**
```python
gun_toplam = fiyatlar.sum(axis=0)
print("Her günün toplam harcaması:", gun_toplam)
```
- `axis=0` ile sütun bazında topladık (her günün toplamı).

**Alıştırma:**
- 4x3’lük bir matris oluşturun. Her satırda en yüksek değeri bulup yazdırın (ör: 4 farklı öğrencinin 3 sınav notu).

---

## 5) Matris Metotları

- NumPy ile matrislerde toplama, ortalama, maksimum, minimum gibi işlemler çok kolaydır.

**Günlük Hayattan Örnek:**
Bir okulda, 3 farklı sınıfın 4 farklı sınavdan aldığı notları bir tabloya aktarıp analiz edelim.

```python
notlar = np.array([[70, 80, 65, 90],
                   [60, 55, 75, 85],
                   [88, 92, 79, 95]])
print("Sınıf sınav notları:\n", notlar)
```
- 3 sınıf (satır), 4 sınav (sütun) notlarını bir matrise aktardık.

**Her sınavın ortalaması:**
```python
sinav_ort = notlar.mean(axis=0)
print("Her sınavın ortalaması:", sinav_ort)
```
- `axis=0` ile her sütunun ortalamasını bulduk (her sınav için).

**Her sınıfın en yüksek notu:**
```python
sinif_max = notlar.max(axis=1)
print("Her sınıfın en yüksek notu:", sinif_max)
```
- `axis=1` ile her satırın en büyük değerini bulduk (her sınıf için).

**Transpoz (satır/sütunları yer değiştirme):**
```python
print("Notlar transpoz:\n", notlar.T)
```
- `.T` ile satır ve sütunları yer değiştirdik.

**Alıştırma:**
- 5x2’lik bir matris oluşturun. Her sütunun toplamını ve her satırın ortalamasını yazdırın (ör: 5 gün boyunca 2 farklı kişiye ait su tüketimi).

---

## Kapanış ve Ödev

**Özet:**
- NumPy dizileriyle vektör ve matris işlemleri hızlı ve kolaydır.
- Toplama, ortalama, maksimum, minimum gibi işlemler tek satırda yapılabilir.
- Filtreleme ve maskelerle günlük hayatta veri analizi kolaylaşır.

**Ödev (isteğe bağlı):**
1. Bir ay boyunca günlük harcamanızı bir vektöre girin. En fazla harcama yaptığınız günü bulun.
2. 3 öğrencinin 5 sınav notunu matris olarak girin. Her öğrencinin ortalamasını ve en düşük notunu yazdırın.

**Kaynaklar:**
- NumPy Dokümantasyon: https://numpy.org/doc/
- Başlangıç için NumPy: https://numpy.org/doc/stable/user/absolute_beginners.html