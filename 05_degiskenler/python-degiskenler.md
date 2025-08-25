
# Python Değişkenler (3 Saatlik Ders İçeriği)

## 🎯 Dersin Amacı
- Değişken kavramını öğrenmek  
- Veri tiplerini tanımak  
- Değişken isimlendirme kurallarını anlamak  
- Pratik örneklerle uygulama yapmak  

---

## 1. Giriş: Değişken Nedir? (20 dk)

Değişken, bilgisayar belleğinde verileri saklamak için kullanılan isimlendirilmiş bir alandır.  
Python’da değişken tanımlarken **tip belirtmemize gerek yoktur**; değerine göre tip otomatik atanır.

```python
x = 10          # int (tam sayı)
y = 3.14        # float (ondalıklı sayı)
isim = "Ali"    # str (metin)
```

---

## 2. Değişkenlerin Özellikleri (25 dk)

- Değerler değiştirilebilir:
```python
x = 5
print(x)   # 5
x = 20
print(x)   # 20
```

- Aynı anda birden fazla değişkene değer atanabilir:
```python
a, b, c = 1, 2, 3
print(a, b, c)  # 1 2 3
```

- Tek değeri birden fazla değişkene atama:
```python
x = y = z = 100
print(x, y, z)  # 100 100 100
```

---

## 3. Veri Tipleri (40 dk)

Python’daki temel veri tipleri:  
- **int**: Tam sayılar  
- **float**: Ondalıklı sayılar  
- **str**: Metinler  
- **bool**: Doğru/Yanlış değerleri  

### Örnekler:
```python
# int
yas = 25
print(type(yas))  # <class 'int'>

# float
pi = 3.14159
print(type(pi))   # <class 'float'>

# str
isim = "Zeynep"
print(type(isim)) # <class 'str'>

# bool
aktif = True
print(type(aktif)) # <class 'bool'>
```

---

## 4. Değişken İsimlendirme Kuralları (30 dk)

✅ Geçerli örnekler:
```python
ad = "Ayşe"
soyad = "Kaya"
yas_2025 = 30
```

❌ Geçersiz örnekler:
```python
2isim = "Ali"    # sayı ile başlayamaz
ad-soyad = "Veli" # tire kullanılamaz
```

➡️ Kurallar:
- Sadece harf, rakam ve `_` kullanılabilir.  
- Sayı ile başlayamaz.  
- Python anahtar kelimeleri (`if`, `for`, `class`, vb.) değişken adı olamaz.  

---

## 5. Kullanıcıdan Veri Alma (20 dk)

```python
isim = input("Adınızı giriniz: ")
print("Merhaba,", isim)

yas = int(input("Yaşınızı giriniz: "))
print("Gelecek yıl yaşınız:", yas + 1)
```

---

## 6. Pratik Uygulamalar (30 dk)

1. Kullanıcıdan adı ve yaşı alıp ekrana yazdırın.  
2. Üçgenin alanını hesaplayan bir program yazın.  
3. İki sayıyı toplayıp sonucu gösterin.  

```python
# Örnek: Üçgen Alanı
taban = float(input("Taban uzunluğunu giriniz: "))
yukseklik = float(input("Yüksekliği giriniz: "))
alan = (taban * yukseklik) / 2
print("Üçgenin alanı:", alan)
```

---

## 7. Mini Quiz (15 dk)

1. Değişken nedir?  
2. Python’da hangi veri tipleri vardır?  
3. `x, y, z = 5, 10, 15` ifadesinde `y`’nin değeri nedir?  
4. `yas = int("25")` ifadesi hangi tipte veri döndürür?  

---

## 8. Ödev (10 dk)

- Kullanıcıdan adını, yaşını ve okulunu alıp bir cümle içinde yazdırın.  
- 3 farklı ürünün fiyatını kullanıcıdan alarak toplamını hesaplayın.  

---

⏰ **Toplam: 3 saat**
