# Python String Metotları - Kapsamlı Ders İçeriği

## Ders Planı (3 Saat - 180 Dakika)

### 🕐 **1. Saat (0-60 dk): Temel String Metotları**
- String'e Giriş ve Temel Kavramlar (10 dk)
- Büyük/Küçük Harf Dönüşümleri (15 dk)
- Arama ve Kontrol Metotları (20 dk)
- Başlangıç ve Bitiş Kontrolleri (15 dk)

### 🕑 **2. Saat (60-120 dk): İleri String İşlemleri**
- Bölme ve Birleştirme İşlemleri (20 dk)
- Temizleme ve Düzenleme Metotları (20 dk)
- Değiştirme İşlemleri (20 dk)

### 🕒 **3. Saat (120-180 dk): Formatıama ve Özel Metotlar**
- String Formatlama (20 dk)
- Karakter Kontrolü Metotları (20 dk)
- Encoding/Decoding ve Diğer Metotlar (20 dk)

---

## 🚀 **1. SAAT: TEMEL STRING METOTLARI**

### 📚 **String'e Giriş ve Temel Kavramlar (10 dk)**

Python'da string'ler immutable (değişmez) veri tipleridir. String metotları orijinal string'i değiştirmez, yeni bir string döndürür.

```python
# String tanımlama
metin = "Python Programlama"
print(f"Orijinal metin: '{metin}'")
print(f"String uzunluğu: {len(metin)}")
print(f"String tipi: {type(metin)}")

# String karakterlerine erişim
print(f"İlk karakter: '{metin[0]}'")
print(f"Son karakter: '{metin[-1]}'")
print(f"Slice örneği: '{metin[0:6]}'")
```

**Çıktı:**
```
Orijinal metin: 'Python Programlama'
String uzunluğu: 18
String tipi: <class 'str'>
İlk karakter: 'P'
Son karakter: 'a'
Slice örneği: 'Python'
```

### 🔤 **Büyük/Küçük Harf Dönüşümleri (15 dk)**

#### **1. `upper()` - Tüm harfleri büyük yapar**
```python
metin = "python programlama"
buyuk_metin = metin.upper()
print(f"Orijinal: '{metin}'")
print(f"upper(): '{buyuk_metin}'")

# Pratik kullanım
kullanici_girisi = "evet"
if kullanici_girisi.upper() == "EVET":
    print("Onaylandı!")
```

#### **2. `lower()` - Tüm harfleri küçük yapar**
```python
metin = "PYTHON PROGRAMLAMA"
kucuk_metin = metin.lower()
print(f"Orijinal: '{metin}'")
print(f"lower(): '{kucuk_metin}'")

# E-posta kontrolü örneği
email = "KULLANICI@GMAIL.COM"
normalized_email = email.lower()
print(f"Normalleştirilmiş e-posta: {normalized_email}")
```

#### **3. `capitalize()` - İlk harfi büyük, diğerleri küçük**
```python
metin = "python programlama dili"
capitalize_metin = metin.capitalize()
print(f"Orijinal: '{metin}'")
print(f"capitalize(): '{capitalize_metin}'")

# Cümle başları için
cumle = "merhaba dünya. nasılsın?"
print(f"Düzeltilmiş: '{cumle.capitalize()}'")
```

#### **4. `title()` - Her kelimenin ilk harfini büyük yapar**
```python
metin = "python programlama dili"
title_metin = metin.title()
print(f"Orijinal: '{metin}'")
print(f"title(): '{title_metin}'")

# İsim formatlama
isim = "ahmet mehmet ayşe"
formatli_isim = isim.title()
print(f"Formatlanmış isim: '{formatli_isim}'")
```

#### **5. `swapcase()` - Büyük/küçük harfleri ters çevirir**
```python
metin = "PyThOn ProGramLama"
swap_metin = metin.swapcase()
print(f"Orijinal: '{metin}'")
print(f"swapcase(): '{swap_metin}'")
```

#### **6. `casefold()` - Gelişmiş küçük harf dönüşümü**
```python
# Türkçe karakterler için önemli
metin1 = "İSTANBUL"
metin2 = "Straße"  # Almanca

print(f"lower(): '{metin1.lower()}'")
print(f"casefold(): '{metin1.casefold()}'")
print(f"Almanca lower(): '{metin2.lower()}'")
print(f"Almanca casefold(): '{metin2.casefold()}'")
```

### 🔍 **Arama ve Kontrol Metotları (20 dk)**

#### **1. `find()` - Alt string'in ilk konumunu bulur**
```python
metin = "Python programlama dili Python"
konum = metin.find("Python")
konum2 = metin.find("Java")
konum3 = metin.find("prog")

print(f"Metin: '{metin}'")
print(f"'Python' konumu: {konum}")
print(f"'Java' konumu: {konum2}")  # -1 (bulunamadı)
print(f"'prog' konumu: {konum3}")

# Belirli bir konumdan sonra arama
konum_sonraki = metin.find("Python", 10)
print(f"10. karakterden sonra 'Python': {konum_sonraki}")
```

#### **2. `rfind()` - Alt string'in son konumunu bulur**
```python
metin = "Python programlama dili Python"
son_konum = metin.rfind("Python")
print(f"Son 'Python' konumu: {son_konum}")

# Aralık belirtme
son_konum2 = metin.rfind("a", 0, 15)
print(f"İlk 15 karakterde son 'a': {son_konum2}")
```

#### **3. `index()` ve `rindex()` - find() benzeri ama hata fırlatır**
```python
metin = "Python programlama"
try:
    konum = metin.index("Python")
    print(f"'Python' konumu: {konum}")
    
    # Bulunamayan durumda hata
    konum2 = metin.index("Java")
except ValueError as e:
    print(f"Hata: {e}")

# rindex örneği
try:
    son_konum = metin.rindex("a")
    print(f"Son 'a' konumu: {son_konum}")
except ValueError as e:
    print(f"Hata: {e}")
```

#### **4. `count()` - Alt string'in kaç kez geçtiğini sayar**
```python
metin = "Python programlama dili Python ile programlama"
python_sayisi = metin.count("Python")
prog_sayisi = metin.count("prog")
a_sayisi = metin.count("a")

print(f"Metin: '{metin}'")
print(f"'Python' sayısı: {python_sayisi}")
print(f"'prog' sayısı: {prog_sayisi}")
print(f"'a' harfi sayısı: {a_sayisi}")

# Belirli aralıkta sayma
a_sayisi_aralik = metin.count("a", 0, 20)
print(f"İlk 20 karakterde 'a' sayısı: {a_sayisi_aralik}")
```

#### **5. `in` operatörü - Alt string kontrolü**
```python
metin = "Python programlama dili"

# Temel kontrol
if "Python" in metin:
    print("Python kelimesi bulundu!")

if "Java" not in metin:
    print("Java kelimesi bulunamadı!")

# Pratik kullanım
email = "kullanici@gmail.com"
if "@" in email and "." in email:
    print("Geçerli e-posta formatı!")
```

### 🎯 **Başlangıç ve Bitiş Kontrolleri (15 dk)**

#### **1. `startswith()` - Belirli string ile başlayıp başlamadığını kontrol eder**
```python
metin = "Python programlama dili"

# Temel kullanım
print(f"'Python' ile başlıyor mu? {metin.startswith('Python')}")
print(f"'Java' ile başlıyor mu? {metin.startswith('Java')}")

# Çoklu seçenek
print(f"Birden fazla seçenek: {metin.startswith(('Python', 'Java', 'C++'))}")

# Belirli pozisyondan kontrol
print(f"7. karakterden itibaren 'prog': {metin.startswith('prog', 7)}")

# Dosya uzantısı kontrolü örneği
dosya_adi = "resim.jpg"
if dosya_adi.startswith(("image_", "img_", "photo_")):
    print("Resim dosyası prefiksi var")
else:
    print("Standart dosya adı")
```

#### **2. `endswith()` - Belirli string ile bitip bitmediğini kontrol eder**
```python
metin = "Python programlama dili"

# Temel kullanım
print(f"'dili' ile bitiyor mu? {metin.endswith('dili')}")
print(f"'language' ile bitiyor mu? {metin.endswith('language')}")

# Çoklu seçenek
print(f"Birden fazla seçenek: {metin.endswith(('dili', 'language', 'tool'))}")

# Dosya uzantısı kontrolü
dosya_adi = "document.pdf"
if dosya_adi.endswith(('.txt', '.doc', '.pdf')):
    print("Desteklenen belge formatı")
    
# URL kontrolü
url = "https://www.example.com"
if url.endswith('.com'):
    print("Ticari site")
elif url.endswith('.org'):
    print("Organizasyon sitesi")
```

#### **Pratik Örnek: Dosya İşlemleri**
```python
def dosya_turu_kontrol(dosya_adi):
    """Dosya türünü kontrol eden fonksiyon"""
    if dosya_adi.endswith(('.jpg', '.jpeg', '.png', '.gif')):
        return "Resim dosyası"
    elif dosya_adi.endswith(('.mp4', '.avi', '.mov')):
        return "Video dosyası"
    elif dosya_adi.endswith(('.py', '.js', '.html', '.css')):
        return "Kod dosyası"
    elif dosya_adi.endswith(('.txt', '.doc', '.pdf')):
        return "Belge dosyası"
    else:
        return "Bilinmeyen tür"

# Test
dosyalar = ["foto.jpg", "video.mp4", "script.py", "belge.pdf", "data.csv"]
for dosya in dosyalar:
    print(f"{dosya}: {dosya_turu_kontrol(dosya)}")
```

---

## ⚡ **2. SAAT: İLERİ STRING İŞLEMLERİ**

### ✂️ **Bölme ve Birleştirme İşlemleri (20 dk)**

#### **1. `split()` - String'i böler**
```python
# Temel kullanım (boşluk karakterine göre)
metin = "Python programlama dili"
kelimeler = metin.split()
print(f"Orijinal: '{metin}'")
print(f"Bölünmüş: {kelimeler}")
print(f"Kelime sayısı: {len(kelimeler)}")

# Belirli ayıraç ile bölme
email_listesi = "user1@gmail.com,user2@yahoo.com,user3@hotmail.com"
emailler = email_listesi.split(',')
print(f"E-postalar: {emailler}")

# Maksimum bölme sayısı
metin2 = "a-b-c-d-e-f"
parcalar = metin2.split('-', 2)  # Sadece 2 kez böl
print(f"Sınırlı bölme: {parcalar}")

# CSV verisi işleme örneği
csv_satir = "Ahmet,25,İstanbul,Mühendis"
veriler = csv_satir.split(',')
isim, yas, sehir, meslek = veriler
print(f"İsim: {isim}, Yaş: {yas}, Şehir: {sehir}, Meslek: {meslek}")
```

#### **2. `rsplit()` - Sağdan sola böler**
```python
dosya_yolu = "/home/user/documents/file.txt"
# Normal split
normal_split = dosya_yolu.split('/', 2)
print(f"Normal split: {normal_split}")

# rsplit - sağdan 2 kez böl
rsplit_sonuc = dosya_yolu.rsplit('/', 2)
print(f"rsplit: {rsplit_sonuc}")

# Dosya adı ve uzantısını ayırma
dosya = "backup_2024_01_15.tar.gz"
ad, uzanti = dosya.rsplit('.', 1)
print(f"Dosya adı: {ad}, Uzantı: {uzanti}")
```

#### **3. `splitlines()` - Satır sonlarına göre böler**
```python
cok_satirli_metin = """Birinci satır
İkinci satır
Üçüncü satır
Dördüncü satır"""

satirlar = cok_satirli_metin.splitlines()
print(f"Satır sayısı: {len(satirlar)}")
for i, satir in enumerate(satirlar, 1):
    print(f"{i}. satır: '{satir}'")

# Satır sonlarını koruma
satirlar_keepends = cok_satirli_metin.splitlines(keepends=True)
print(f"Satır sonları korunmuş: {satirlar_keepends}")

# Dosya okuma simülasyonu
dosya_icerigi = "isim,yaş\nAhmet,25\nMehmet,30\nAyşe,28"
satirlar = dosya_icerigi.splitlines()
baslik = satirlar[0].split(',')
print(f"Başlık: {baslik}")
for satir in satirlar[1:]:
    veriler = satir.split(',')
    print(f"{baslik[0]}: {veriler[0]}, {baslik[1]}: {veriler[1]}")
```

#### **4. `join()` - Liste elemanlarını birleştirir**
```python
kelimeler = ["Python", "programlama", "dili"]
# Boşluk ile birleştirme
cumle = " ".join(kelimeler)
print(f"Cümle: '{cumle}'")

# Farklı ayıraçlar
tire_ile = "-".join(kelimeler)
virgul_ile = ", ".join(kelimeler)
print(f"Tire ile: '{tire_ile}'")
print(f"Virgül ile: '{virgul_ile}'")

# Sayıları birleştirme (önce string'e çevirmeli)
sayilar = [1, 2, 3, 4, 5]
sayi_str = "-".join(map(str, sayilar))
print(f"Sayılar: '{sayi_str}'")

# Dosya yolu oluşturma
klasorler = ["home", "user", "documents", "projects"]
dosya_yolu = "/".join(klasorler)
print(f"Dosya yolu: /{dosya_yolu}")

# HTML liste oluşturma
urunler = ["Laptop", "Mouse", "Klavye"]
html_liste = "<li>" + "</li>\n<li>".join(urunler) + "</li>"
print(f"HTML Liste:\n<ul>\n<li>{html_liste}\n</ul>")
```

#### **5. `partition()` ve `rpartition()` - Üçe böler**
```python
# partition - ilk bulduğu ayıraçta böler
email = "kullanici@domain.com"
kullanici, ayirac, domain = email.partition('@')
print(f"Kullanıcı: '{kullanici}', Ayıraç: '{ayirac}', Domain: '{domain}'")

# rpartition - son bulduğu ayıraçta böler
dosya_yolu = "/home/user/documents/file.txt"
yol, ayirac, dosya = dosya_yolu.rpartition('/')
print(f"Yol: '{yol}', Ayıraç: '{ayirac}', Dosya: '{dosya}'")

# URL parse etme
url = "https://www.example.com/page?param=value"
protokol, ayirac, geri_kalan = url.partition('://')
print(f"Protokol: '{protokol}', Geri kalan: '{geri_kalan}'")
```

### 🧹 **Temizleme ve Düzenleme Metotları (20 dk)**

#### **1. `strip()` - Baştan ve sondan boşlukları temizler**
```python
# Temel kullanım
metin = "   Python programlama   "
temiz_metin = metin.strip()
print(f"Orijinal: '{metin}'")
print(f"Temizlenmiş: '{temiz_metin}'")

# Belirli karakterleri temizleme
metin2 = "...Python programlama..."
temiz_metin2 = metin2.strip('.')
print(f"Nokta temizleme: '{temiz_metin2}'")

# Çoklu karakter temizleme
metin3 = "###***Python***###"
temiz_metin3 = metin3.strip('#*')
print(f"Çoklu karakter: '{temiz_metin3}'")

# Kullanıcı girişi temizleme
kullanici_girisi = input("Adınızı girin: ").strip()
if kullanici_girisi:
    print(f"Merhaba {kullanici_girisi}!")
else:
    print("Geçerli bir isim giriniz!")
```

#### **2. `lstrip()` - Soldan temizler**
```python
metin = "   Python programlama"
sol_temiz = metin.lstrip()
print(f"Sol temizlik: '{sol_temiz}'")

# Belirli karakter
metin2 = "000123456"
sayi = metin2.lstrip('0')
print(f"Sıfır temizleme: '{sayi}'")

# Log dosyası temizleme örneği
log_satiri = "    [INFO] Sistem başlatıldı"
temiz_log = log_satiri.lstrip()
print(f"Temiz log: '{temiz_log}'")
```

#### **3. `rstrip()` - Sağdan temizler**
```python
metin = "Python programlama   "
sag_temiz = metin.rstrip()
print(f"Sağ temizlik: '{sag_temiz}'")

# Dosya uzantısı temizleme
dosya_adi = "document.txt..."
temiz_dosya = dosya_adi.rstrip('.')
print(f"Temiz dosya adı: '{temiz_dosya}'")

# Satır sonu karakteri temizleme
satir = "Bu bir satır\n\r"
temiz_satir = satir.rstrip('\n\r')
print(f"Temiz satır: '{temiz_satir}'")
```

#### **4. `center()`, `ljust()`, `rjust()` - Hizalama metotları**
```python
metin = "Python"

# Ortalama
ortalanmis = metin.center(20)
print(f"Ortalanmış: '{ortalanmis}'")

# Doldurma karakteri ile ortalama
ortalanmis_yildiz = metin.center(20, '*')
print(f"Yıldız ile: '{ortalanmis_yildiz}'")

# Sola hizalama
sola_hizali = metin.ljust(15, '-')
print(f"Sola hizalı: '{sola_hizali}'")

# Sağa hizalama
saga_hizali = metin.rjust(15, '-')
print(f"Sağa hizalı: '{saga_hizali}'")

# Tablo oluşturma örneği
print("Ad".ljust(15) + "Yaş".rjust(5) + "Şehir".rjust(12))
print("-" * 32)
print("Ahmet".ljust(15) + "25".rjust(5) + "İstanbul".rjust(12))
print("Mehmet".ljust(15) + "30".rjust(5) + "Ankara".rjust(12))
```

#### **5. `zfill()` - Sıfır ile doldurma**
```python
# Sayıları belirli uzunlukta gösterme
sayi = "42"
sifir_dolgulu = sayi.zfill(5)
print(f"Sıfır dolgulu: '{sifir_dolgulu}'")

# Negatif sayılar
negatif = "-42"
negatif_dolgulu = negatif.zfill(6)
print(f"Negatif dolgulu: '{negatif_dolgulu}'")

# Dosya numaralandırma
for i in range(1, 11):
    dosya_adi = f"file_{str(i).zfill(3)}.txt"
    print(dosya_adi)

# ID oluşturma
kullanici_id = "123"
formatted_id = f"USR{kullanici_id.zfill(6)}"
print(f"Formatlanmış ID: {formatted_id}")
```

### 🔄 **Değiştirme İşlemleri (20 dk)**

#### **1. `replace()` - String değiştirme**
```python
metin = "Python programlama dili Python"

# Temel değiştirme
yeni_metin = metin.replace("Python", "Java")
print(f"Orijinal: '{metin}'")
print(f"Değiştirilmiş: '{yeni_metin}'")

# Sınırlı değiştirme
sinirli = metin.replace("Python", "Java", 1)  # Sadece ilk bulduğunu değiştir
print(f"Sınırlı değiştirme: '{sinirli}'")

# Boşluk temizleme
bozuk_metin = "Python  programlama   dili"
duzgun_metin = bozuk_metin.replace("  ", " ").replace("   ", " ")
print(f"Düzgün metin: '{duzgun_metin}'")

# Karakter temizleme
telefon = "0(532) 123-45-67"
temiz_telefon = telefon.replace("(", "").replace(")", "").replace("-", "").replace(" ", "")
print(f"Temiz telefon: '{temiz_telefon}'")

# Template değiştirme
template = "Merhaba {isim}, yaşınız {yas}"
mesaj = template.replace("{isim}", "Ahmet").replace("{yas}", "25")
print(f"Mesaj: '{mesaj}'")
```

#### **2. `translate()` ve `maketrans()` - Karakter çevirisi**
```python
# Temel karakter çevirisi
metin = "Hello World"
ceviri_tablosu = str.maketrans("aeiou", "12345")
cevrilmis = metin.translate(ceviri_tablosu)
print(f"Orijinal: '{metin}'")
print(f"Çevrilmiş: '{cevrilmis}'")

# Türkçe karakter dönüşümü
turkce_metin = "çğıöşüÇĞIÖŞÜ"
turkce_ingilizce = str.maketrans("çğıöşüÇĞIÖŞÜ", "cgiosucgiOSU")
ingilizce_metin = turkce_metin.translate(turkce_ingilizce)
print(f"Türkçe: '{turkce_metin}'")
print(f"İngilizce: '{ingilizce_metin}'")

# Karakter silme
metin_rakamli = "abc123def456ghi"
rakam_sil = str.maketrans("", "", "0123456789")
harf_sadece = metin_rakamli.translate(rakam_sil)
print(f"Rakamlar silinmiş: '{harf_sadece}'")

# ROT13 şifreleme
import string
rot13 = str.maketrans(
    string.ascii_lowercase + string.ascii_uppercase,
    string.ascii_lowercase[13:] + string.ascii_lowercase[:13] +
    string.ascii_uppercase[13:] + string.ascii_uppercase[:13]
)
mesaj = "Hello World"
sifreli = mesaj.translate(rot13)
print(f"ROT13 şifreli: '{sifreli}'")
```

#### **3. `expandtabs()` - Tab karakterlerini genişletir**
```python
# Tab karakterli metin
tab_metin = "Python\tprogramlama\tdili"
genisletilmis = tab_metin.expandtabs()
print(f"Orijinal: '{tab_metin}'")
print(f"Genişletilmiş: '{genisletilmis}'")

# Özel tab boyutu
genisletilmis_4 = tab_metin.expandtabs(4)
genisletilmis_8 = tab_metin.expandtabs(8)
print(f"4 boşluk: '{genisletilmis_4}'")
print(f"8 boşluk: '{genisletilmis_8}'")

# CSV formatını düzeltme
csv_data = "isim\tyaş\tşehir"
duzeltilmis = csv_data.expandtabs(10)
print(f"Düzeltilmiş CSV: '{duzeltilmis}'")
```

---

## 🎨 **3. SAAT: FORMATLAMA VE ÖZEL METOTLAR**

### 📝 **String Formatlama (20 dk)**

#### **1. `format()` metodu**
```python
# Temel kullanım
isim = "Ahmet"
yas = 25
mesaj = "Merhaba {}, yaşınız {}".format(isim, yas)
print(mesaj)

# İndeks ile
mesaj2 = "Merhaba {0}, yaşınız {1}. {0} hoş geldiniz!".format(isim, yas)
print(mesaj2)

# İsimli parametreler
mesaj3 = "Merhaba {isim}, yaşınız {yas}".format(isim="Mehmet", yas=30)
print(mesaj3)

# Sözlük ile
kisi = {"isim": "Ayşe", "yas": 28, "sehir": "İstanbul"}
mesaj4 = "Merhaba {isim}, {yas} yaşındasınız ve {sehir}'da yaşıyorsunuz".format(**kisi)
print(mesaj4)

# Formatıama seçenekleri
sayi = 3.14159
para = 1234.56

print("Pi sayısı: {:.2f}".format(sayi))  # 2 ondalık
print("Para: {:.2f} TL".format(para))    # Para formatı
print("Yüzde: {:.1%}".format(0.1234))   # Yüzde formatı
print("Büyük sayı: {:,}".format(1234567))  # Binlik ayıracı

# Hizalama ve genişlik
print("'{:>10}'".format("sağ"))        # Sağa hizalı
print("'{:<10}'".format("sol"))        # Sola hizalı
print("'{:^10}'".format("orta"))       # Orta hizalı
print("'{:*^15}'".format("orta"))      # Yıldız ile doldurulmuş
```

#### **2. f-string (Python 3.6+)**
```python
isim = "Ahmet"
yas = 25
sehir = "İstanbul"

# Temel f-string
mesaj = f"Merhaba {isim}, yaşınız {yas}"
print(mesaj)

# İfadeler
print(f"Gelecek yıl {yas + 1} yaşında olacaksınız")
print