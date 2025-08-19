# Python String Metotları

Bu dokümanda Python'da string (metin) veriler üzerinde kullanılabilen tüm önemli metotlar kısa açıklamaları ve örnekleriyle birlikte sunulmuştur.  

---

## 1. Temel Dönüşüm ve Biçimlendirme Metotları

### `upper()`  
Metindeki tüm harfleri **büyük harfe** çevirir.

```python
text = "python programlama"
print(text.upper())  # PYTHON PROGRAMLAMA
```

### `lower()`  
Metindeki tüm harfleri **küçük harfe** çevirir.

```python
text = "Python Programlama"
print(text.lower())  # python programlama
```

### `title()`  
Her kelimenin **ilk harfini büyük**, diğerlerini küçük yapar.

```python
text = "python programlama dili"
print(text.title())  # Python Programlama Dili
```

### `capitalize()`  
Sadece **ilk harfi büyük** yapar, geri kalan harfleri küçük yapar.

```python
text = "python PROGRAMLAMA"
print(text.capitalize())  # Python programlama
```

### `swapcase()`  
Büyük harfleri küçük, küçük harfleri büyük yapar.

```python
text = "PyThOn"
print(text.swapcase())  # pYtHoN
```

---

## 2. Arama ve Kontrol Metotları

### `startswith()`  
Bir stringin belirli bir ifadeyle başlayıp başlamadığını kontrol eder.

```python
text = "python öğreniyorum"
print(text.startswith("py"))  # True
```

### `endswith()`  
Bir stringin belirli bir ifadeyle bitip bitmediğini kontrol eder.

```python
text = "python öğreniyorum"
print(text.endswith("yorum"))  # True
```

### `find()`  
Aranan alt stringin ilk indexini döndürür. Yoksa `-1` döner.

```python
text = "programlama"
print(text.find("gram"))  # 3
```

### `rfind()`  
Aranan alt stringin **sondan** ilk bulunduğu indexi döndürür.

```python
text = "programlama"
print(text.rfind("a"))  # 9
```

### `index()`  
Aranan alt stringin ilk indexini döndürür. Yoksa hata verir.

```python
text = "programlama"
print(text.index("gram"))  # 3
```

### `count()`  
Bir alt stringin kaç kere geçtiğini döndürür.

```python
text = "banana"
print(text.count("a"))  # 3
```

---

## 3. Değiştirme ve Düzenleme Metotları

### `replace()`  
Bir alt stringi başka bir alt string ile değiştirir.

```python
text = "ben python seviyorum"
print(text.replace("python", "java"))  # ben java seviyorum
```

### `strip()`  
Başta ve sondaki boşlukları (veya belirtilen karakterleri) siler.

```python
text = "   python   "
print(text.strip())  # "python"
```

### `lstrip()`  
Sadece baştaki boşlukları siler.

```python
text = "   python"
print(text.lstrip())  # "python"
```

### `rstrip()`  
Sadece sondaki boşlukları siler.

```python
text = "python   "
print(text.rstrip())  # "python"
```

---

## 4. Kontrol Metotları

### `isalnum()`  
Tüm karakterler harf veya rakam mı?

```python
print("abc123".isalnum())  # True
print("abc 123".isalnum())  # False
```

### `isalpha()`  
Tüm karakterler harf mi?

```python
print("abc".isalpha())  # True
print("abc123".isalpha())  # False
```

### `isdigit()`  
Tüm karakterler rakam mı?

```python
print("123".isdigit())  # True
print("12a3".isdigit())  # False
```

### `isspace()`  
Tüm karakterler boşluk mu?

```python
print("   ".isspace())  # True
```

### `isupper()`  
Tüm karakterler büyük harf mi?

```python
print("ABC".isupper())  # True
```

### `islower()`  
Tüm karakterler küçük harf mi?

```python
print("abc".islower())  # True
```

### `istitle()`  
Her kelimenin ilk harfi büyük mü?

```python
print("Python Programlama".istitle())  # True
```

---

## 5. Bölme ve Birleştirme Metotları

### `split()`  
Stringi boşluk veya belirtilen karaktere göre böler.

```python
text = "python,java,c++"
print(text.split(","))  # ['python', 'java', 'c++']
```

### `rsplit()`  
Sağdan bölme işlemi yapar.

```python
text = "a,b,c,d"
print(text.rsplit(",", 2))  # ['a,b', 'c', 'd']
```

### `splitlines()`  
Metni satırlara böler.

```python
text = "merhaba\ndünya"
print(text.splitlines())  # ['merhaba', 'dünya']
```

### `join()`  
Liste elemanlarını belirtilen ayraç ile birleştirir.

```python
liste = ["python", "java", "c++"]
print("-".join(liste))  # python-java-c++
```

---

## 6. Hizalama ve Doldurma Metotları

### `center()`  
Stringi belirtilen uzunlukta ortalar.

```python
print("python".center(20, "-"))
# -------python-------
```

### `ljust()`  
Stringi sola yaslar.

```python
print("python".ljust(10, "*"))  # python****
```

### `rjust()`  
Stringi sağa yaslar.

```python
print("python".rjust(10, "*"))  # ****python
```

### `zfill()`  
Başa sıfır ekleyerek doldurur.

```python
print("42".zfill(5))  # 00042
```

---

## 7. Encode / Decode Metotları

### `encode()`  
Stringi belirtilen kodlama ile byte dizisine çevirir.

```python
text = "python"
print(text.encode("utf-8"))
```

---

# Ders Akışı (3 Saat)

1. **Giriş (15 dk)** → String kavramı ve önemi  
2. **Temel Metotlar (40 dk)** → Dönüşüm, biçimlendirme, arama metotları  
3. **Uygulamalı Çalışma (30 dk)** → Öğrencilerle küçük örnekler çözme  
4. **İleri Metotlar (40 dk)** → Bölme, birleştirme, kontrol metotları  
5. **Uygulama (30 dk)** → Mini proje: Kullanıcıdan alınan metin üzerinde analiz yapma  
6. **Soru-Cevap & Kapanış (25 dk)**  

---

Bu içerik ile yaklaşık 3 saatlik kapsamlı bir ders işlenebilir.
