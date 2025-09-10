# Python'da Döngüler – Ders İçeriği

## 1. Giriş

### 1.1 Döngü Nedir?
- Programlamada döngüler, belirli bir işlemin birden fazla kez otomatik olarak tekrarlanmasını sağlar.
- Döngüler sayesinde uzun ve tekrarlı işlemleri kısaca ve hatasız şekilde yazabiliriz.

### 1.2 Neden Döngü Kullanılır?
- Aynı kodun birden fazla kez çalışması gerektiğinde döngüler kullanılır.
- Veri koleksiyonlarını (liste, sözlük, dizi vs.) işlemek, tekrar eden hesaplamalar yapmak, otomasyon sağlamak için döngüler vazgeçilmezdir.

### 1.3 Python'da Döngü Türleri
- Python’da en çok kullanılan döngüler: `for` ve `while`.
- Her iki döngü tipinin farklı avantajları ve kullanım yerleri vardır.

---

## 2. For Döngüsü – Temel Kullanım

### 2.1 Basit For Döngüsü
```python
for i in range(5):
    print(i)
```

### 2.2 Liste Üzerinde Dolaşma
```python
meyveler = ["elma", "muz", "çilek"]
for meyve in meyveler:
    print(meyve)
```

### 2.3 String Üzerinde Dolaşma
```python
kelime = "Python"
for harf in kelime:
    print(harf)
```

### 2.4 enumerate() ile İndeksli Döngü
```python
for i, meyve in enumerate(meyveler):
    print(i, meyve)
```

#### Alıştırma:
Bir listedeki elemanların indeks ve değerini ekrana yazdıran programı yazın.

---

## 3. For Döngüsünde range() Kullanımı

### 3.1 range() ile Sayısal Döngü
```python
for i in range(1, 11):
    print(i)
```

### 3.2 range(start, stop, step)
```python
for i in range(0, 10, 2):
    print(i)
```

#### Alıştırma:
1’den 100’e kadar olan çift sayıları ekrana yazdıran bir program yazın.

---

## 4. İç İçe (Nested) For Döngüleri

### 4.1 2 Boyutlu Liste Üzerinde Dolaşma
```python
matris = [[1,2,3], [4,5,6], [7,8,9]]
for satir in matris:
    for eleman in satir:
        print(eleman, end=" ")
    print()
```

### 4.2 Çarpım Tablosu
```python
for i in range(1, 6):
    for j in range(1, 6):
        print(i*j, end="\t")
    print()
```

#### Alıştırma:
Kullanıcıdan alınan bir sayı için çarpım tablosunu ekrana yazdıran programı yazın.

---

## 5. For Döngüsü ile Liste Üreteci (List Comprehension)

### 5.1 Temel Kullanım
```python
kareler = [x**2 for x in range(10)]
print(kareler)
```

### 5.2 Filtreleme ile List Comprehension
```python
tekler = [x for x in range(20) if x % 2 == 1]
print(tekler)
```

#### Alıştırma:
Bir listede negatif olanları filtreleyip yeni listede saklayan bir program yazın.

---

## 6. While Döngüsü – Temel Kullanım

### 6.1 Basit While Döngüsü
```python
i = 0
while i < 5:
    print(i)
    i += 1
```

### 6.2 Kullanıcıdan Veri Alma ile While
```python
sayi = int(input("Pozitif sayı girin: "))
while sayi <= 0:
    sayi = int(input("Tekrar pozitif sayı girin: "))
print("Girdiğiniz sayı:", sayi)
```

#### Alıştırma:
Kullanıcı doğru şifreyi girene kadar tekrar soran bir program yazın.

---

## 7. While Döngüsünde Sonsuz Döngü ve break Kullanımı

### 7.1 Sonsuz Döngü
```python
while True:
    cevap = input("Çıkmak için q yazın: ")
    if cevap == "q":
        break
```

### 7.2 Döngüyü break ile Sonlandırma
```python
for i in range(10):
    if i == 5:
        break
    print(i)
```

#### Alıştırma:
Kullanıcı q girene kadar sayı istemeye devam eden ve alınan sayıları listeleyen programı yazın.

---

## 8. continue ve pass Kullanımı

### 8.1 continue ile Döngü Atlatma
```python
for i in range(10):
    if i % 2 == 0:
        continue
    print(i)
```

### 8.2 pass ile Boş Döngü Bloğu
```python
for i in range(5):
    pass  # Şimdilik işlem yok
```

#### Alıştırma:
Bir listede sıfır olan elemanları atlayıp kalanları yazdıran bir program yazın.

---

## 9. Sözlük ve Küme Üzerinde Döngü

### 9.1 Sözlükte Anahtar-Değer Üzerinde Döngü
```python
ogrenci = {"ad": "Ahmet", "yas": 20, "sinif": 2}
for anahtar, deger in ogrenci.items():
    print(f"{anahtar}: {deger}")
```

### 9.2 Kümede Döngü
```python
renkler = {"kırmızı", "mavi", "yeşil"}
for renk in renkler:
    print(renk)
```

#### Alıştırma:
Bir sözlükteki tüm anahtarları ve değerleri ayrı ayrı yazdıran program yazın.

---

## 10. Döngülerde else Kullanımı

### 10.1 for-else ve while-else
```python
for i in range(5):
    print(i)
else:
    print("Döngü normal bitti.")

i = 0
while i < 3:
    print(i)
    i += 1
else:
    print("While döngüsü tamamlandı.")
```

#### Alıştırma:
Bir listede aranan değeri bulamazsa "Bulunamadı" mesajı veren for-else örneği yazın.

---

## 11. Döngülerde Hatalar ve İpuçları

- Sonsuz döngü hataları
- Yanlış indeks veya koşul kullanımı
- Girinti hataları
- break ve continue’nun doğru kullanımı

#### Alıştırma:
Hatalı bir döngüyü düzeltin. break ve continue’nun işleyişini örneklerle açıklayın.

---

## 12. Uygulama ve Mini Proje

- Kullanıcıdan alınan sayıları toplayan, negatif girilirse döngüyü bitiren program
- Sınıf listesi: Not ortalaması, en yüksek notu bulma (for ve while ile)
- Mini oyun: Tahmin oyunu – kullanıcı doğru cevabı bulana kadar döngü devam etsin

---

## 13. Soru-Cevap ve Kapanış

- Sık yapılan döngü hataları ve pratik ipuçları
- Döngülerin gerçek hayatta kullanım örnekleri
- Ek kaynaklar ve ileri okuma

---

**Not:** Her bölüm sonunda bol örnek, uygulama ve kısa alıştırmalar yer almaktadır.