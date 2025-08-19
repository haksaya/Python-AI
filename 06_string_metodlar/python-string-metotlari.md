# 📘 Ders Planı: Python String Metotları (3 Saat)

## 🎯 Öğrenme Hedefleri
- String veri tipinin özelliklerini kavramak  
- Python’daki sık kullanılan string metotlarını öğrenmek  
- Uygulamalı alıştırmalar ile pekiştirmek  
- Küçük projelerle gerçek senaryolara uyarlamak  

---

## 🕒 Ders Akışı

### **0. Bölüm – Giriş (10 dk)**
- String nedir?  
- String veri tipinin temel özellikleri  
- Karakter dizilerinde indeksleme ve dilimleme hatırlatma  

```python
metin = "Merhaba Python"
print(metin[0])      # İlk karakter
print(metin[-1])     # Son karakter
print(metin[0:7])    # Dilimleme
```

---

### **1. Bölüm – String İnceleme Metotları (40 dk)**
**Kullanılacak metotlar:**
- `len()`
- `.upper()`, `.lower()`, `.title()`, `.capitalize()`, `.swapcase()`
- `.startswith()`, `.endswith()`
- `.isalpha()`, `.isdigit()`, `.isalnum()`, `.isspace()`

```python
yazi = "Python 3"
print(len(yazi))          # Uzunluk
print(yazi.upper())       # PYTHON 3
print(yazi.lower())       # python 3
print(yazi.title())       # Python 3
print(yazi.swapcase())    # pYTHON 3

print(yazi.startswith("Py"))  # True
print(yazi.endswith("on"))    # False

print("Merhaba".isalpha())  # True
print("123".isdigit())      # True
print("abc123".isalnum())   # True
print("   ".isspace())      # True
```

📌 **Etkinlik:** Öğrencilerden kendi isimlerini string değişkenine atayıp yukarıdaki metotları denemeleri istenir.

---

### **2. Bölüm – Arama ve Bulma Metotları (30 dk)**
- `.find()`, `.rfind()`
- `.index()`, `.rindex()`
- `.count()`
- `"in"` operatörü

```python
metin = "python programlama python"
print(metin.find("python"))   # 0
print(metin.rfind("python"))  # 18
print(metin.count("python"))  # 2
print("pro" in metin)         # True
```

📌 **Alıştırma:** Bir cümlede kaç tane “a” harfi geçtiğini say.

---

### **3. Bölüm – Değiştirme ve Düzenleme Metotları (40 dk)**
- `.replace()`
- `.strip()`, `.lstrip()`, `.rstrip()`
- `.split()`, `.rsplit()`, `.splitlines()`
- `.join()`

```python
metin = "   Python dersleri   "
print(metin.strip())   # "Python dersleri"

adres = "Ankara-İstanbul-İzmir"
print(adres.split("-"))   # ['Ankara', 'İstanbul', 'İzmir']

kelimeler = ["Python", "Java", "C#"]
print(", ".join(kelimeler))  # "Python, Java, C#"
```

📌 **Uygulama:** Kullanıcıdan alınan bir cümlede boşlukları temizleyip kelimeleri listele.

---

### **4. Bölüm – Biçimlendirme Metotları (30 dk)**
- `.format()`  
- f-string (Python 3.6+)  
- `.center()`, `.ljust()`, `.rjust()`, `.zfill()`

```python
isim = "Harun"
yas = 25
print("Benim adım {} ve {} yaşındayım".format(isim, yas))
print(f"Benim adım {isim} ve {yas} yaşındayım")

print(isim.center(20, "-"))  # -------Harun--------
print(isim.ljust(20, "."))   # Harun...............
print(isim.zfill(5))         # 0Harun ❌ (sayılarla daha mantıklı)
print(str(42).zfill(5))      # 00042
```

📌 **Alıştırma:** Kullanıcıdan isim ve yaş alarak f-string ile kişisel tanıtım yazısı oluştur.

---

### **5. Bölüm – Uygulama Projesi (30 dk)**
**Mini Proje:** Basit bir **metin analiz programı** yazın.  
- Kullanıcıdan bir paragraf alın.  
- Kaç karakter, kaç kelime olduğunu yazdırın.  
- “Python” kelimesi geçiyor mu kontrol edin.  
- En çok tekrar eden harfi bulun.  

---

## 🎓 Ders Sonu
- Öğrenciler ile birlikte özet tablo çıkarılır.  
- Ev ödevi: “Kendi ad-soyadını alıp string metotlarını dene, farklı sonuçlar bul.”  
