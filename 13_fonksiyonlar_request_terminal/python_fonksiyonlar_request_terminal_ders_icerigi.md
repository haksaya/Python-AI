# Python Programlama: Fonksiyonlar, Request Kütüphanesi ve Terminal – Ders İçeriği

## 1. Giriş

### 1.1 Dersin Amacı
- Python'da fonksiyonlar, internetten veri çekmek için request kütüphanesi, terminal kavramı ve temel terminal komutları hakkında temel bilgiler ve bol örneklerle pratik yapmak.

---

## 2. Fonksiyonlar

### 2.1 Fonksiyon Nedir?
- Belli bir görevi yerine getiren kod bloklarıdır.
- Kod tekrarını azaltır, kodun okunabilirliğini artırır.

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


---

## 4. Terminal Kavramı

### 4.1 Terminal Nedir?
- Bilgisayar ile etkileşim kurmak için kullanılan komut satırı arayüzüdür.
- Grafik arayüz yerine yazılı komutlar ile işlem yapılır.

### 4.2 Terminal Kullanım Alanları
- Dosya ve klasör işlemleri
- Program kurulumu ve çalıştırma
- Versiyon kontrolü (Git)
- Uzaktan sunucu yönetimi

### 4.3 Terminal Açma
- Windows: CMD, PowerShell veya Windows Terminal
- MacOS/Linux: Terminal uygulaması

---

## 5. Temel Terminal Komutları

### 5.1 Dizini Görüntüleme
```bash
pwd  # Bulunduğunuz klasörü gösterir (Linux/Mac)
cd   # Klasör değiştirir
ls   # Klasördeki dosyaları listeler (Linux/Mac)
dir  # Windows'ta dosya listeler
```

### 5.2 Dosya ve Klasör İşlemleri
```bash
mkdir yeni_klasor      # Yeni klasör oluşturur
touch dosya.txt        # Yeni dosya oluşturur (Linux/Mac)
echo Merhaba > dosya.txt  # Dosya içerisine yazı ekler
del dosya.txt          # Dosya siler (Windows)
rm dosya.txt           # Dosya siler (Linux/Mac)
```

### 5.3 Dosya Okuma ve Düzenleme
```bash
cat dosya.txt          # Dosya içeriğini gösterir (Linux/Mac)
type dosya.txt         # Windows'ta dosya içeriğini gösterir
nano dosya.txt         # Linux/Mac'te dosyayı düzenler
```

### 5.4 Komutları Zincirleme ve Yardım Alma
```bash
ls -l                 # Dosyaları detaylı listeler
ls | grep txt         # txt içeren dosyaları bulur
komut --help          # Komutun nasıl kullanıldığını gösterir
```

---

## 7. Soru-Cevap ve Kapanış

- Konulara dair sık sorulan sorular ve ipuçları.
- Daha fazla öğrenmek için kaynaklar ve ileri okuma önerileri.

---
