# Python'da IF, ELIF, ELSE Koşulları – Ders İçeriği

## 1. Giriş

### 1.1 Koşul Nedir?
- Programlamada koşullar, kodun belirli durumlarda farklı şekilde çalışmasını sağlar.
- Gerçek hayattan örnek: "Eğer hava yağmurluysa şemsiye al."

### 1.2 Neden Koşul Kullanılır?
- Karar mekanizması oluşturmak
- Akışı kontrol etmek
- Kullanıcıdan gelen veriye göre farklı işlemler yapmak

---

## 2. IF Koşulu – Temel Kullanım

### 2.1 Söz Dizimi ve Mantığı
```python
if koşul:
    # koşul doğruysa çalışacak kod
```

### 2.2 Basit Örnekler
```python
sayi = 7
if sayi > 5:
    print("Sayı 5'ten büyük.")
```

### 2.3 Girintileme (Indentation)
- Python’da bloklar girinti ile belirlenir.
- Hatalı girintileme çalışmaz:
```python
if True:
print("Girinti hatası!")  # SyntaxError!
```

### 2.4 Karşılaştırma Operatörleri
- ==, !=, >, <, >=, <=
- Mantıksal operatörler: and, or, not

#### Alıştırma:
Bir sayının pozitif mi negatif mi olduğunu belirleyen program yazın.

---

## 3. ELSE Koşulu – Alternatif Akış

### 3.1 Söz Dizimi
```python
if koşul:
    # koşul doğruysa
else:
    # koşul yanlışsa
```

### 3.2 Örnekler
```python
yas = int(input("Yaşınızı girin: "))
if yas >= 18:
    print("Reşitsiniz.")
else:
    print("Reşit değilsiniz.")
```

#### Alıştırma:
Kullanıcıdan alınan nota göre ‘Geçti’ veya ‘Kaldı’ mesajı veren program yazın.

---

## 4. ELIF Koşulu – Çoklu Durumlar

### 4.1 Söz Dizimi
```python
if koşul1:
    # koşul1 doğruysa
elif koşul2:
    # koşul2 doğruysa
else:
    # Diğer tüm durumlar
```

### 4.2 Örnekler
```python
notu = int(input("Notunuzu girin: "))
if notu >= 90:
    print("Pekiyi")
elif notu >= 70:
    print("İyi")
elif notu >= 50:
    print("Orta")
else:
    print("Zayıf")
```

### 4.3 Birden Fazla ELIF Kullanımı
- Sıralı kontrol ve akış örnekleri

#### Alıştırma:
Kullanıcıdan alınan gün adına göre hafta içi/hafta sonu bilgisini veren program yazın.

---

## 5. İç İçe Koşullar (Nested If)

### 5.1 Söz Dizimi
```python
if koşul1:
    if koşul2:
        # içteki koşul doğruysa çalışır
```

### 5.2 Örnekler
```python
sayi = int(input("Sayı girin: "))
if sayi > 0:
    if sayi % 2 == 0:
        print("Pozitif ve çift")
    else:
        print("Pozitif ve tek")
else:
    print("Sayı pozitif değil")
```

#### Alıştırma:
Kullanıcıdan alınan iki sayıdan büyük olana ve tek olana göre farklı mesajlar veren program yazın.

---

## 6. Mantıksal Operatörlerle Koşullar

### 6.1 and, or, not Operatörleri
```python
num = int(input("Bir sayı girin: "))
if num > 0 and num < 100:
    print("Sayı 0 ile 100 arasında.")
```

### 6.2 Birden Fazla Koşul Kullanımı
```python
kullanici = input("Kullanıcı adı: ")
sifre = input("Şifre: ")
if kullanici == "admin" and sifre == "1234":
    print("Giriş başarılı")
else:
    print("Hatalı giriş")
```

#### Alıştırma:
Kullanıcıdan alınan yaş ve cinsiyete göre askerlik uygunluğu kontrolü yapan program yazın.

---

## 7. Kısa İfadesel Koşullar (Ternary/One-liner If)

### 7.1 Tek Satırlık If Else
```python
x = 5
print("Pozitif") if x > 0 else print("Negatif veya sıfır")
```

### 7.2 Değişkene Atama ile Kısa Koşul
```python
sayi = -5
durum = "Pozitif" if sayi > 0 else "Negatif veya Sıfır"
print(durum)
```

#### Alıştırma:
Kullanıcıdan alınan sayının tek mi çift mi olduğunu kısa if ile ekrana yazdıran program yazın.

---

## 8. Hatalar ve İpuçları

- Girinti hataları
- Karşılaştırma ve atama farkı (= vs ==)
- Mantıksal operatörlerin doğru kullanımı
- Koşulların sıralaması ve kapsama alanı

#### Alıştırma:
Girinti hatası olan bir kodu düzeltin. Yanlış koşul sıralamasından dolayı hatalı çalışan bir kodu düzeltin.

---

## 9. Uygulama ve Mini Proje

- Sınav notu değerlendirme uygulaması (if, elif, else ile)
- Basit kullanıcı girişi ve yetkilendirme akışı
- İndirim hesaplama: Yaş, alışveriş tutarı ve müşteri tipine göre indirim oranı belirleme

---

## 10. Soru-Cevap ve Kapanış

- Sık yapılan hatalar
- Koşul kodlarıyla ilgili ileri uygulama örnekleri
- Ek kaynaklar ve ileri okuma

---

**Not:** Her bölüm sonunda kısa alıştırmalar ve uygulamalar yer almaktadır. Süreler, örnekler ve pratikler isteğe göre artırılabilir.