# Python Veri Koleksiyonları 
Python'da birden fazla veriyi saklamak için kullanılan **veri koleksiyonları** şunlardır: `list`, `tuple`, `dict` ve `set`.  

```python
# 1️⃣ List → Sıralı ve değiştirilebilir
meyveler = ["elma", "muz", "çilek"]
print("List:", meyveler)
meyveler.append("portakal")  # Eleman ekleme
print("List güncel:", meyveler)

# 2️⃣ Tuple → Sıralı ama değiştirilemez
renkler = ("kırmızı", "mavi", "yeşil")
print("Tuple:", renkler)
# renkler[0] = "turuncu"  # ❌ Hata! Tuple değiştirilemez

# 3️⃣ Dict → Anahtar-Değer çiftleri
ogrenci = {
    "ad": "Harun",
    "yas": 25,
    "ders": "Python"
}
print("Dict:", ogrenci)
ogrenci["yas"] = 26  # Değer güncelleme
print("Dict güncel:", ogrenci)

# 4️⃣ Set → Benzersiz ve sırasız
sayilar = {1, 2, 3, 3, 2}  # Tekrarlar otomatik silinir
print("Set:", sayilar)
sayilar.add(4)  # Eleman ekleme
print("Set güncel:", sayilar)
