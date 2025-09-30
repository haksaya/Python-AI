# Python Programlama: Fonksiyonlar, Request Kütüphanesi ve Temel Terminal – Ders İçeriği

## 1. Giriş

### 1.1 Dersin Amacı
- Python'da fonksiyonlar, internetten veri çekmek için request kütüphanesi ve terminal kavramı hakkında temel bilgiler ve örneklerle pratik yapmak.

---

## 2. Fonksiyonlar

### 2.1 Fonksiyon Nedir?
- Belirli bir görevi yerine getiren kod bloklarıdır.
- Kod tekrarını azaltır, okunabilirliği artırır.

### 2.2 Basit Fonksiyon Tanımlama
```python
def merhaba():
    print("Merhaba Python!")
```
- Fonksiyonu çağırmak:
```python
merhaba()
```

### 2.3 Parametreli Fonksiyonlar
```python
def topla(a, b):
    return a + b

sonuc = topla(3, 5)
print(sonuc)
```

### 2.4 Varsayılan Parametreler
```python
def selamla(isim="Python"):
    print(f"Merhaba, {isim}!")
```

### 2.5 Dönüş Değeri (return)
```python
def kare(x):
    return x ** 2

print(kare(4))
```

### 2.6 Çoklu Dönüş (Tuple)
```python
def islemler(a, b):
    return a+b, a-b, a*b

toplam, fark, carpim = islemler(5, 3)
print(toplam, fark, carpim)
```

#### Alıştırma:
- İki parametre alan ve bunların çarpımını döndüren bir fonksiyon yazın.
- Bir listeyi parametre olarak alıp içindeki en büyük sayıyı döndüren fonksiyon yazın.

---

## 3. Request Kütüphanesi

### 3.1 Nedir? Ne işe yarar?
- İnternetten veri çekmek için (HTTP istekleri) kullanılır.
- API veya web sayfalarından veri almak için idealdir.

### 3.2 Kurulum
```bash
pip install requests
```

### 3.3 Basit GET İsteği
```python
import requests

response = requests.get("https://api.github.com")
print(response.status_code)
print(response.text)
```

### 3.4 JSON Veri Çekme
```python
url = "https://jsonplaceholder.typicode.com/todos/1"
veri = requests.get(url).json()
print(veri)
```

### 3.5 Parametre ile GET İsteği
```python
params = {"q": "python"}
response = requests.get("https://www.google.com/search", params=params)
print(response.url)
```

### 3.6 POST İsteği
```python
data = {"isim": "Ali", "yas": 22}
response = requests.post("https://httpbin.org/post", data=data)
print(response.text)
```

### 3.7 Hata Kontrolü
```python
try:
    r = requests.get("https://olmayanadres.com")
    r.raise_for_status()
except requests.exceptions.RequestException as e:
    print("Hata:", e)
```

#### Alıştırma:
- Bir API'den rastgele veri çekip ekrana yazdıran basit bir program yazın.
- POST ile bir form gönderen örnek kod yazın.

---

## 4. Temel Terminal Kavramı ve Komutları

### 4.1 Terminal Nedir?
- Bilgisayar ile etkileşim kurmak için kullanılan komut satırı arayüzüdür.

### 4.2 Terminal Açma
- Windows: CMD, PowerShell veya Windows Terminal
- MacOS/Linux: Terminal uygulaması

### 4.3 Sık Kullanılan Temel Komutlar
```bash
pwd  # Bulunduğunuz klasörü gösterir (Linux/Mac)
cd   # Klasör değiştirir
ls   # Klasördeki dosyaları listeler (Linux/Mac)
dir  # Windows'ta dosya listeler
mkdir yeni_klasor      # Yeni klasör oluşturur
```

#### Alıştırma:
- Terminalde bir klasör oluşturup içine girin ve dizin yolunu görüntüleyin.

---

## 5. Pratik Uygulamalar ve Mini Proje

- Basit bir Python fonksiyonu ile kullanıcıdan alınan iki sayıyı toplayıp ekrana yazdıran program.
- Bir API'den veri çekip terminalde gösteren Python programı.
- Mini Proje: Kullanıcıdan şehir adını alıp, bu şehirle ilgili hava durumu verilerini bir API'den çekip terminalde gösteren Python programı.

---

## 6. Soru-Cevap ve Kapanış

- Konulara dair sık sorulan sorular ve ipuçları.
- Daha fazla öğrenmek için kaynaklar ve ileri okuma önerileri.

---
