# Python Veri Koleksiyonları

Python'da birden fazla veriyi bir arada ve düzenli bir şekilde tutmak için **veri koleksiyonları** kullanılır. Her koleksiyonun kendine özgü özellikleri ve kullanım amaçları vardır. Python’da en sık kullanılan veri koleksiyonları şunlardır: **list**, **tuple**, **dict** ve **set**.

---

## 1️⃣ List (Liste)

- **Tanım:** Sıralı (indexli) ve değiştirilebilir veri yapısıdır.
- **Ne işe yarar?** Birden fazla veriyi, sırasını koruyarak saklamak ve üzerinde değişiklik yapmak için kullanılır.
- **Özellikler:** Eleman ekleyebilir, silebilir, güncelleyebilirsiniz.

```python
meyveler = ["elma", "muz", "çilek"]    # Liste oluşturma
print("List:", meyveler)

meyveler.append("portakal")            # Eleman ekleme
print("List güncel:", meyveler)

meyveler[1] = "karpuz"                 # Eleman güncelleme
print("List güncel2:", meyveler)
```

---

## 2️⃣ Tuple (Demet)

- **Tanım:** Sıralı fakat değiştirilemeyen (immutable) veri yapısıdır.
- **Ne işe yarar?** Sabit ve değişmemesi gereken veri gruplarını saklamak için kullanılır.
- **Özellikler:** Eleman ekleme, silme veya güncelleme yapılamaz.

```python
renkler = ("kırmızı", "mavi", "yeşil") # Tuple oluşturma
print("Tuple:", renkler)

# renkler[0] = "turuncu"  # ❌ Hata! Tuple elemanları değiştirilemez
```

---

## 3️⃣ Dict (Sözlük)

- **Tanım:** Anahtar-değer (key-value) çiftleriyle veri saklayan koleksiyondur.
- **Ne işe yarar?** Her bir veriye bir anahtar ile ulaşmak ve verileri anlamlı şekilde gruplamak için kullanılır.
- **Özellikler:** Değiştirilebilir; yeni anahtar-değer eklenebilir, mevcut değerler güncellenebilir veya silinebilir.

```python
ogrenci = {
    "ad": "Harun",
    "yas": 25,
    "ders": "Python"
}
print("Dict:", ogrenci)

ogrenci["yas"] = 26                   # Değer güncelleme
print("Dict güncel:", ogrenci)

ogrenci["okul"] = "YTÜ"               # Yeni anahtar-değer ekleme
print("Dict yeni:", ogrenci)
```

---

## 4️⃣ Set (Küme)

- **Tanım:** Sırasız ve benzersiz (unique) elemanlardan oluşan veri yapısıdır.
- **Ne işe yarar?** Tekrarlayan elemanları otomatik olarak silmek ve matematiksel kümelerin işlemlerini yapmak için kullanılır.
- **Özellikler:** Eleman sırası önemli değildir; tekrar eden elemanlar sadece bir kez yer alır.

```python
sayilar = {1, 2, 3, 3, 2}             # Tekrarlar otomatik silinir
print("Set:", sayilar)

sayilar.add(4)                        # Eleman ekleme
print("Set güncel:", sayilar)

sayilar.remove(2)                     # Eleman silme
print("Set güncel2:", sayilar)
```

---

## Kısa Özet

- **List:** Sıralı ve değiştirilebilir → [“elma”, “muz”, “çilek”]
- **Tuple:** Sıralı ama değiştirilemez → (“kırmızı”, “mavi”, “yeşil”)
- **Dict:** Anahtar-değer çiftiyle, anlamlı veri → {"ad": "Harun", "yas": 25}
- **Set:** Benzersiz, sırasız veri → {1, 2, 3, 4}

Her bir koleksiyonun farklı kullanım amacı ve avantajı vardır. Doğru koleksiyonu seçmek kodunuzu daha verimli ve anlaşılır hale getirir.