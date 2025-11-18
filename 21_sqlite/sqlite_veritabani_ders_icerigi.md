# SQLite Veri Tabanı

Bu ders, SQLite ile veri tabanı oluşturmayı, tablo yönetimini, CRUD işlemlerini ve SQLite Browser ile görselleştirmeyi kapsar.

---

## 1. SQLite Nedir?

- SQLite, hafif ve taşınabilir bir **ilişkisel veri tabanı yönetim sistemi (RDBMS)** dir.
- Facebook'ta, mobil uygulamalarda, masaüstü uygulamalarda yaygın olarak kullanılır.
- Kurulum gerektirmez, tek bir dosya olarak kaydedilir.
- Python'da varsayılan olarak gelmektedir.

**Neden SQLite?**
- Kurulu olarak geliyor
- Kolay kullanım
- Hafif ve hızlı
- Dosya tabanlı (basit paylaşım)

---

## 2. Veri Tabanı Temelleri ve Kavramlar

### Temel Kavramlar

- **Veri Tabanı (Database)**: Verilerin düzenli biçimde saklandığı yer
- **Tablo (Table)**: Satır ve sütunlardan oluşan veri yapısı
- **Sütun (Column)**: Veri özellikleri (ad, yaş, email vb.)
- **Satır (Row)**: Bir nesnenin tüm özellikleri
- **Anahtar (Key)**: Verileri benzersiz şekilde tanımlayan alan

### Örnek Tablo Yapısı

| id | isim   | yas | email           |
|----|--------|-----|-----------------|
| 1  | Ali    | 25  | ali@example.com |
| 2  | Ayşe   | 30  | ayse@example.com|
| 3  | Mehmet | 22  | mehmet@example.com |

---

## 3. SQLite Kurulumu ve İlk Adımlar

### Python ile SQLite Kullanımı

SQLite Python'da yerleşik olarak gelir, sadece import etmek yeterlidir.

```python
import sqlite3

# Veri tabanı bağlantısı oluştur
baglanti = sqlite3.connect('ogrenciler.db')
print("Veri tabanı başarıyla oluşturuldu!")
```

**Açıklama:**
- `sqlite3.connect()` ile veri tabanına bağlanırız
- `ogrenciler.db` dosyası oluşturulur (bilgisayarda fiziksel bir dosya)

---

## 4. Veri Tabanı Oluşturma ve Yönetim

### Python ile Veri Tabanı Oluşturma

```python
import sqlite3

# Bağlantı oluştur
baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# Veri tabanı bilgisi
print("Veri tabanı adı: ogrenciler.db")
print("Bağlantı açık: Evet")

# Bağlantıyı kapat
baglanti.close()
print("Bağlantı kapatıldı")
```

**Açıklama:**
- `baglanti = sqlite3.connect()`: Veri tabanına bağlan
- `imleç = baglanti.cursor()`: Komutları çalıştırmak için imleç oluştur
- `baglanti.close()`: Bağlantıyı kapat

---

## 5. Tablo Oluşturma

### Tablo Oluşturma (CREATE TABLE)

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# Öğrenciler tablosu oluştur
sql_komut = """
CREATE TABLE IF NOT EXISTS ogrenciler (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    isim TEXT NOT NULL,
    yas INTEGER,
    email TEXT UNIQUE,
    sehir TEXT
)
"""

imleç.execute(sql_komut)
baglanti.commit()

print("Tablo başarıyla oluşturuldu!")
baglanti.close()
```

**Açıklama:**
- `INTEGER`: Tam sayı veri tipi
- `TEXT`: Metin veri tipi
- `PRIMARY KEY`: Benzersiz tanımlayıcı
- `AUTOINCREMENT`: Otomatik olarak artar (1, 2, 3...)
- `NOT NULL`: Boş bırakılamaz
- `UNIQUE`: Benzersiz değer (tekrar edemez)
- `baglanti.commit()`: Değişiklikleri kaydet

### Ürün Tablosu Örneği

```python
import sqlite3

baglanti = sqlite3.connect('market.db')
imleç = baglanti.cursor()

sql_komut = """
CREATE TABLE IF NOT EXISTS urunler (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    urun_adi TEXT NOT NULL,
    fiyat REAL,
    stok INTEGER,
    kategori TEXT
)
"""

imleç.execute(sql_komut)
baglanti.commit()

print("Ürün tablosu oluşturuldu!")
baglanti.close()
```

---

## 6. CRUD İşlemleri – CREATE (INSERT)

### INSERT: Veri Ekleme

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# Tek veri ekleme
sql_komut = """
INSERT INTO ogrenciler (isim, yas, email, sehir)
VALUES ('Ali', 25, 'ali@example.com', 'Ankara')
"""

imleç.execute(sql_komut)
baglanti.commit()

print("Veri başarıyla eklendi!")
baglanti.close()
```

**Açıklama:**
- `INSERT INTO`: Veri ekle komutu
- `VALUES`: Eklenecek değerler
- `baglanti.commit()`: Değişiklikleri kaydet

### Çoklu Veri Ekleme

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# Birden fazla öğrenci ekle
ogrenciler = [
    ('Ayşe', 30, 'ayse@example.com', 'İstanbul'),
    ('Mehmet', 22, 'mehmet@example.com', 'İzmir'),
    ('Zeynep', 28, 'zeynep@example.com', 'Bursa')
]

sql_komut = "INSERT INTO ogrenciler (isim, yas, email, sehir) VALUES (?, ?, ?, ?)"

imleç.executemany(sql_komut, ogrenciler)
baglanti.commit()

print("3 öğrenci başarıyla eklendi!")
baglanti.close()
```

**Açıklama:**
- `executemany()`: Birden fazla veri eklemek için kullanılır
- `?`: Güvenli veri girişi (SQL injection'ı önler)

### Gündelik Hayat Örneği: Restoran Müşteri Kaydı

```python
import sqlite3

baglanti = sqlite3.connect('restoran.db')
imleç = baglanti.cursor()

# Müşteriler tablosu oluştur
imleç.execute("""
CREATE TABLE IF NOT EXISTS musteriler (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    ad_soyad TEXT NOT NULL,
    telefon TEXT,
    rezervasyon_tarihi TEXT,
    kisi_sayisi INTEGER
)
""")

# Müşteri ekle
imleç.execute("""
INSERT INTO musteriler (ad_soyad, telefon, rezervasyon_tarihi, kisi_sayisi)
VALUES (?, ?, ?, ?)
""", ('Ahmet Yılmaz', '05321234567', '2025-11-20', 4))

baglanti.commit()
print("Müşteri kaydı yapıldı!")
baglanti.close()
```

---

## 7. CRUD İşlemleri – READ (SELECT)

### SELECT: Veri Sorgulama

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# Tüm verileri çek
sql_komut = "SELECT * FROM ogrenciler"
imleç.execute(sql_komut)
sonuclar = imleç.fetchall()

for satir in sonuclar:
    print(satir)

baglanti.close()
```

**Açıklama:**
- `SELECT *`: Tüm sütunları seç
- `fetchall()`: Tüm sonuçları listede al

### Belirli Sütunları Seçme

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# Sadece isim ve yaşı çek
sql_komut = "SELECT isim, yas FROM ogrenciler"
imleç.execute(sql_komut)
sonuclar = imleç.fetchall()

for isim, yas in sonuclar:
    print(f"{isim} - {yas} yaşında")

baglanti.close()
```

### Tek Satır Getirme

```python
# İlk sonucu getir
sonuc = imleç.fetchone()
print(sonuc)

# Belirli sayıda sonuç getir
sonuclar = imleç.fetchmany(2)  # İlk 2 sonuç
```

### Gündelik Hayat Örneği: Kütüphane Kitapları Listeleme

```python
import sqlite3

baglanti = sqlite3.connect('kutuphane.db')
imleç = baglanti.cursor()

# Kütüphane tablosu oluştur
imleç.execute("""
CREATE TABLE IF NOT EXISTS kitaplar (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    baslik TEXT NOT NULL,
    yazar TEXT,
    yil INTEGER,
    sayfa_sayisi INTEGER
)
""")

# Kitapları ekle
kitaplar = [
    ('1984', 'George Orwell', 1949, 328),
    ('Dört Dörtlük', 'Necip Fazıl', 1930, 120),
    ('Suç ve Ceza', 'Dostoyevski', 1866, 671)
]

imleç.executemany(
    "INSERT INTO kitaplar (baslik, yazar, yil, sayfa_sayisi) VALUES (?, ?, ?, ?)",
    kitaplar
)

baglanti.commit()

# Tüm kitapları listele
print("=== KÜTÜPHANE KİTAPLARI ===")
imleç.execute("SELECT * FROM kitaplar")
for kitap in imleç.fetchall():
    print(f"ID: {kitap[0]}, Başlık: {kitap[1]}, Yazar: {kitap[2]}, Yıl: {kitap[3]}")

baglanti.close()
```

---

## 8. CRUD İşlemleri – UPDATE

### UPDATE: Veri Güncelleme

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# Ali'nin yaşını 26'ya güncelle
sql_komut = "UPDATE ogrenciler SET yas = 26 WHERE isim = 'Ali'"
imleç.execute(sql_komut)
baglanti.commit()

print("Veri başarıyla güncellendi!")
baglanti.close()
```

**Açıklama:**
- `UPDATE`: Güncelleme komutu
- `SET`: Hangi sütunun değişeceği
- `WHERE`: Hangi satırın değişeceği

### Birden Fazla Sütunu Güncelleme

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# Mehmet'in yaşı ve şehrini güncelle
sql_komut = """
UPDATE ogrenciler 
SET yas = 23, sehir = 'Ankara' 
WHERE isim = 'Mehmet'
"""

imleç.execute(sql_komut)
baglanti.commit()

print("Birden fazla veri güncellendi!")
baglanti.close()
```

### Gündelik Hayat Örneği: Ürün Fiyat Güncelleme

```python
import sqlite3

baglanti = sqlite3.connect('market.db')
imleç = baglanti.cursor()

# Ürünler tablosu
imleç.execute("""
CREATE TABLE IF NOT EXISTS urunler (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    urun_adi TEXT NOT NULL,
    fiyat REAL,
    stok INTEGER
)
""")

# Ürünleri ekle
imleç.execute("INSERT INTO urunler (urun_adi, fiyat, stok) VALUES (?, ?, ?)",
              ('Süt', 10, 50))
imleç.execute("INSERT INTO urunler (urun_adi, fiyat, stok) VALUES (?, ?, ?)",
              ('Ekmek', 5, 100))

baglanti.commit()

# Fiyat indirimi uygula: Süt'ün fiyatı 8 TL'ye indirildi
imleç.execute("UPDATE urunler SET fiyat = 8 WHERE urun_adi = 'Süt'")
baglanti.commit()

print("Fiyat güncellemesi yapıldı!")
baglanti.close()
```

---

## 9. CRUD İşlemleri – DELETE

### DELETE: Veri Silme

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# Zeynep'i sil
sql_komut = "DELETE FROM ogrenciler WHERE isim = 'Zeynep'"
imleç.execute(sql_komut)
baglanti.commit()

print("Veri başarıyla silindi!")
baglanti.close()
```

**Açıklama:**
- `DELETE`: Silme komutu
- `WHERE`: Hangi satırın silineceği

### Uyarı: WHERE Olmadan Tüm Veriyi Silme

```python
# DİKKAT: Bu komut tüm tabloyu siler!
# DELETE FROM ogrenciler  (WHERE olmadan)
```

### Gündelik Hayat Örneği: Ürün Stoğu Silme

```python
import sqlite3

baglanti = sqlite3.connect('market.db')
imleç = baglanti.cursor()

# Stokta 0 olan ürünleri sil
sql_komut = "DELETE FROM urunler WHERE stok = 0"
imleç.execute(sql_komut)
baglanti.commit()

print("Stoğu sıfır olan ürünler silindi!")
baglanti.close()
```

---

## 10. WHERE Koşulu ile Sorgu

### WHERE: Şartlı Sorgulama

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# 25 yaşından büyük öğrencileri bul
sql_komut = "SELECT * FROM ogrenciler WHERE yas > 25"
imleç.execute(sql_komut)
sonuclar = imleç.fetchall()

for satir in sonuclar:
    print(satir)

baglanti.close()
```

### Karşılaştırma Operatörleri

```python
# > : Büyüktür
# < : Küçüktür
# >= : Büyük veya eşit
# <= : Küçük veya eşit
# = : Eşit
# != : Eşit değil
```

### Gündelik Hayat Örneği: Belirli Şehirde Oturanları Bulma

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# İstanbul'da oturan öğrencileri bul
sql_komut = "SELECT isim, yas FROM ogrenciler WHERE sehir = 'İstanbul'"
imleç.execute(sql_komut)
sonuclar = imleç.fetchall()

print("İstanbul'da oturan öğrenciler:")
for isim, yas in sonuclar:
    print(f"  - {isim} ({yas} yaş)")

baglanti.close()
```

---

## 11. LIKE Operatörü

### LIKE: Kısmi Metin Araması

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# İsmi 'A' ile başlayan öğrencileri bul
sql_komut = "SELECT * FROM ogrenciler WHERE isim LIKE 'A%'"
imleç.execute(sql_komut)
sonuclar = imleç.fetchall()

for satir in sonuclar:
    print(satir)

baglanti.close()
```

**LIKE Operatörü Desenleri:**
- `'A%'` : A ile başlayan
- `'%i'` : i ile biten
- `'%a%'` : İçinde a olan
- `'_li'` : 3 karakterli, son 2'si "li"

### Gündelik Hayat Örneği: Email Araması

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# gmail.com ile biten emailleri bul
sql_komut = "SELECT isim, email FROM ogrenciler WHERE email LIKE '%@gmail.com'"
imleç.execute(sql_komut)
sonuclar = imleç.fetchall()

print("Gmail kullanan öğrenciler:")
for isim, email in sonuclar:
    print(f"  {isim}: {email}")

baglanti.close()
```

---

## 12. AND ve OR Operatörleri

### AND: Her İki Koşul da Sağlanmalı

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# İstanbul'da ve yaşı 25'ten büyük olan öğrencileri bul
sql_komut = "SELECT * FROM ogrenciler WHERE sehir = 'İstanbul' AND yas > 25"
imleç.execute(sql_komut)
sonuclar = imleç.fetchall()

for satir in sonuclar:
    print(satir)

baglanti.close()
```

### OR: Herhangi Bir Koşul Sağlanırsa Yeterli

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# Ankara'da veya Bursa'da oturanları bul
sql_komut = "SELECT * FROM ogrenciler WHERE sehir = 'Ankara' OR sehir = 'Bursa'"
imleç.execute(sql_komut)
sonuclar = imleç.fetchall()

for satir in sonuclar:
    print(satir)

baglanti.close()
```

### AND ve OR Birleştirme

```python
import sqlite3

baglanti = sqlite3.connect('ogrenciler.db')
imleç = baglanti.cursor()

# (İstanbul'da ve 25 yaşından büyük) VEYA (Bursa'da ve 20 yaşından büyük)
sql_komut = """
SELECT * FROM ogrenciler 
WHERE (sehir = 'İstanbul' AND yas > 25) 
   OR (sehir = 'Bursa' AND yas > 20)
"""
imleç.execute(sql_komut)
sonuclar = imleç.fetchall()

for satir in sonuclar:
    print(satir)

baglanti.close()
```

### Gündelik Hayat Örneği: Banka Kredi Şartları

```python
import sqlite3

baglanti = sqlite3.connect('musteri.db')
imleç = baglanti.cursor()

# Kredi uygun müşteriler: (Gelir >= 3000 ve Yaş >= 25) VEYA (Gelir >= 5000 ve Yaş >= 20)
sql_komut = """
SELECT musteri_adi, gelir, yas FROM musteriler
WHERE (gelir >= 3000 AND yas >= 25) 
   OR (gelir >= 5000 AND yas >= 20)
"""
imleç.execute(sql_komut)
sonuclar = imleç.fetchall()

print("Kredi Uygun Müşteriler:")
for ad, gelir, yas in sonuclar:
    print(f"  {ad}: {gelir} TL, {yas} yaş")

baglanti.close()
```

---

## 13. SQLite Browser ile Görselleştirme

### SQLite Browser Nedir?

- SQLite Browser, SQLite veri tabanlarını görsel bir arayüzle yönetmek için kullanılan bir uygulamadır.
- Verileri tablo halinde görmek, sorgu çalıştırmak, grafik araçlar sunar.

### SQLite Browser İndirme

1. [DB Browser for SQLite](https://sqlitebrowser.org/dl/) indir
2. Bilgisayara kur
3. Uygulamayı aç

### SQLite Browser Kullanımı

**Adım 1: Veri Tabanını Aç**
- File → Open → ogrenciler.db dosyasını seç

**Adım 2: Tabloları Görüntüle**
- Database Structure sekmesinde tabloları görebilirsin
- Herhangi bir tablaya çift tıklayarak verileri görebilirsin

**Adım 3: Veri Tabanında Değişiklik Yap**
- Browse Data sekmesinde verileri ekleyebilir, silebilir, güncelleyebilirsin
- New Record: Yeni veri ekle
- Delete Record: Veri sil

**Adım 4: SQL Komut Çalıştır**
- Execute SQL sekmesine git
- SQL komutunu yaz ve Ctrl+Enter'e bas

**Örnek SQL Komutları SQLite Browser'da:**

```sql
-- Tüm öğrencileri göster
SELECT * FROM ogrenciler;

-- İstanbul'da oturanları göster
SELECT isim, yas FROM ogrenciler WHERE sehir = 'İstanbul';

-- 25 yaşından büyükleri göster
SELECT * FROM ogrenciler WHERE yas > 25 ORDER BY yas DESC;
```

---

## 14. Gerçek Hayat Projesi: Okul Yönetim Sistemi

```python
import sqlite3

# Veri tabanına bağlan
baglanti = sqlite3.connect('okul.db')
imleç = baglanti.cursor()

# 1. ÖĞRENCİLER TABLOSU
imleç.execute("""
CREATE TABLE IF NOT EXISTS ogrenciler (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    ad_soyad TEXT NOT NULL,
    sinif TEXT,
    telefon TEXT,
    veli_telefon TEXT
)
""")

# 2. SINAV SONUÇLARI TABLOSU
imleç.execute("""
CREATE TABLE IF NOT EXISTS sinavlar (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    ogrenci_id INTEGER,
    ders TEXT,
    not INTEGER,
    tarih TEXT,
    FOREIGN KEY (ogrenci_id) REFERENCES ogrenciler(id)
)
""")

# Öğrencileri ekle
ogrenciler = [
    ('Ali Yılmaz', '10-A', '05301234567', '05321111111'),
    ('Ayşe Kaya', '10-A', '05302234567', '05322222222'),
    ('Mehmet Demir', '10-B', '05303234567', '05323333333')
]

imleç.executemany(
    "INSERT INTO ogrenciler (ad_soyad, sinif, telefon, veli_telefon) VALUES (?, ?, ?, ?)",
    ogrenciler
)

# Sınav sonuçlarını ekle
sinavlar = [
    (1, 'Matematik', 85, '2025-11-15'),
    (1, 'Türkçe', 90, '2025-11-15'),
    (2, 'Matematik', 78, '2025-11-15'),
    (2, 'Türkçe', 92, '2025-11-15'),
    (3, 'Matematik', 88, '2025-11-15')
]

imleç.executemany(
    "INSERT INTO sinavlar (ogrenci_id, ders, not, tarih) VALUES (?, ?, ?, ?)",
    sinavlar
)

baglanti.commit()

# Sorgulamalar
print("=== OKUL YÖNETİM SİSTEMİ ===\n")

# 1. Tüm öğrencileri listele
print("1. Tüm Öğrenciler:")
imleç.execute("SELECT * FROM ogrenciler")
for ogrenci in imleç.fetchall():
    print(f"  ID: {ogrenci[0]}, Ad: {ogrenci[1]}, Sınıf: {ogrenci[2]}")

# 2. 10-A sınıfı öğrencilerini göster
print("\n2. 10-A Sınıfı Öğrencileri:")
imleç.execute("SELECT ad_soyad FROM ogrenciler WHERE sinif = '10-A'")
for ogrenci in imleç.fetchall():
    print(f"  - {ogrenci[0]}")

# 3. Matematik notları 80'den büyük olanlar
print("\n3. Matematik Notu 80'den Büyük Olanlar:")
imleç.execute("""
SELECT ogrenciler.ad_soyad, sinavlar.not 
FROM sinavlar 
JOIN ogrenciler ON sinavlar.ogrenci_id = ogrenciler.id 
WHERE sinavlar.ders = 'Matematik' AND sinavlar.not >= 80
""")
for sonuc in imleç.fetchall():
    print(f"  - {sonuc[0]}: {sonuc[1]}")

# 4. Her öğrencinin ortalama notu
print("\n4. Öğrencilerin Ortalama Notları:")
imleç.execute("""
SELECT ogrenciler.ad_soyad, AVG(sinavlar.not) as ortalama
FROM sinavlar
JOIN ogrenciler ON sinavlar.ogrenci_id = ogrenciler.id
GROUP BY ogrenciler.id
""")
for sonuc in imleç.fetchall():
    print(f"  - {sonuc[0]}: {sonuc[1]:.2f}")

baglanti.close()
print("\nVeri tabanı bağlantısı kapatıldı.")
```

---

## 15. Sık Kullanılan SQL Komutları Özeti

| Komut | Açıklama | Örnek |
|-------|----------|--------|
| `CREATE TABLE` | Tablo oluştur | `CREATE TABLE ogrenciler (id INTEGER, isim TEXT)` |
| `INSERT INTO` | Veri ekle | `INSERT INTO ogrenciler VALUES (1, 'Ali')` |
| `SELECT` | Veri sorgula | `SELECT * FROM ogrenciler` |
| `UPDATE` | Veri güncelle | `UPDATE ogrenciler SET isim='Ayşe' WHERE id=1` |
| `DELETE` | Veri sil | `DELETE FROM ogrenciler WHERE id=1` |
| `WHERE` | Koşul ekle | `WHERE yas > 25` |
| `LIKE` | Kısmi arama | `WHERE isim LIKE 'A%'` |
| `AND` | Her iki koşul | `WHERE yas > 25 AND sehir='Ankara'` |
| `OR` | Herhangi bir koşul | `WHERE sehir='Ankara' OR sehir='İstanbul'` |
| `ORDER BY` | Sıralama | `ORDER BY yas DESC` |
| `LIMIT` | Satır sayısı sınırla | `LIMIT 5` |
| `COUNT` | Satırları say | `SELECT COUNT(*) FROM ogrenciler` |

---

## 16. Kapanış ve Ödevler

**Özet:**
- SQLite basit ve taşınabilir bir veri tabanıdır
- CRUD işlemleri (Create, Read, Update, Delete) temel veritabanı işlemleridir
- WHERE, LIKE, AND, OR ile güçlü sorgular yazabilirsin
- SQLite Browser ile verileri görsel olarak yönetebilirsin

**Ödevler:**
1. Kendi kütüphanesi için kitap veri tabanı oluştur, en az 5 kitap ekle
2. Kitap fiyatını güncelle, ödünç alınan kitapları sil
3. Belirli yazarın kitaplarını ara (LIKE kullanarak)
4. 300 sayfadan fazla ve 2020 sonrası yayınlanan kitapları listele (AND kullanarak)
5. SQLite Browser ile oluşturduğun veri tabanını açıp verileri incele

**Kaynaklar:**
- [SQLite Resmi Dokümantasyon](https://www.sqlite.org/docs.html)
- [W3Schools SQLite Tutorial](https://www.w3schools.com/sql/)
- [DB Browser for SQLite](https://sqlitebrowser.org/)

---

**Hazırlayan:** haksaya  
**Tarih:** 2025-11-18  
**Son Güncelleme:** 2025-11-18 11:22:44 UTC

---