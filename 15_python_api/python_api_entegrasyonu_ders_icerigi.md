# PYTHON API ENTEGRASYONU – Ders İçeriği

Bu ders; “Python API Entegrasyonu”, “JSON ve XML Kodlama Dilleri”, “JSON ile API entegrasyonu” ve “XML ile API entegrasyonu” başlıklarında temel bilgileri, örnekleri ve mini alıştırmaları içerir.

---

## 1) PYTHON API ENTEGRASYONU

- API (Application Programming Interface): Uygulamalar arası veri/işlev paylaşımı için standart arayüzdür.
- HTTP metodları:
  - GET: Veri çekme
  - POST: Veri oluşturma/gönderme
  - PUT/PATCH: Veri güncelleme
  - DELETE: Veri silme
- Önemli bileşenler:
  - URL/Endpoint: https://example.com/api/users
  - Query parametreleri: ?page=2&limit=10
  - Header’lar: Authorization, Content-Type, Accept
  - Body: JSON veya XML veri gövdesi
  - Status kodları: 200 (OK), 201 (Created), 400 (Bad Request), 401 (Unauthorized), 404 (Not Found), 500 (Server Error)
- Temel araçlar:
  - Python: requests, json, xml.etree.ElementTree, (opsiyonel) xmltodict

**Mini Örnek (durum kodu kontrolü):**
```python
import requests

r = requests.get("https://jsonplaceholder.typicode.com/todos/1", timeout=10)
print(r.status_code)
print(r.headers.get("Content-Type"))
print(r.text[:200])  # ilk 200 karakter
```

---

## 2) Json Kodlama Dili

- JSON (JavaScript Object Notation): Hafif veri formatı, anahtar-değer yapısı.
- Avantajlar: İnsan tarafından okunabilir, diller arası uyumlu, web API’lerinde de-facto standart.

**Temel JSON tipleri:**
- object (dict): { "ad": "Ali", "yas": 22 }
- array (list): [1, 2, 3]
- string, number, boolean, null

**Örnek JSON:**
```json
{
  "ad": "Ali",
  "yas": 22,
  "diller": ["Python", "JavaScript"],
  "aktif": true,
  "adres": { "sehir": "İstanbul", "ilce": "Kadıköy" }
}
```

**Python’da JSON okuma/yazma:**
```python
import json

# String -> Python sözlüğü
s = '{"ad":"Ali","yas":22,"aktif":true}'
veri = json.loads(s)
print(veri["ad"], veri["yas"], veri["aktif"])

# Python objesi -> JSON string
obj = {"mesaj": "Merhaba", "sayi": 42}
json_str = json.dumps(obj, ensure_ascii=False, indent=2)
print(json_str)

# Dosyadan okuma/yazma
with open("ornek.json", "w", encoding="utf-8") as f:
    json.dump(obj, f, ensure_ascii=False, indent=2)

with open("ornek.json", "r", encoding="utf-8") as f:
    tekrar = json.load(f)
    print(tekrar)
```

**Sık Hatalar ve İpuçları:**
- JSON tek tırnak değil, çift tırnak kullanır.
- Python None -> JSON null; True/False -> true/false
- Türkçe karakterler için `ensure_ascii=False` kullanın.

**Alıştırma:**
- Bir JSON stringinden “sehir” alanını okuyup ekrana yazdırın.
- Bir Python dict’i JSON’a çevirip dosyaya kaydedin.

---

## 3) XML Kodlama Dili

- XML (eXtensible Markup Language): Etiket tabanlı hiyerarşik veri formatı.
- Avantajları: Şema ile doğrulanabilir, güçlü hiyerarşi, metaveri/attribute’lar.
- Dezavantajı: JSON’a göre daha uzun/verbosedir.

**Temel XML:**
```xml
<kisi id="101">
  <ad>Ali</ad>
  <yas>22</yas>
  <diller>
    <dil>Python</dil>
    <dil>JavaScript</dil>
  </diller>
</kisi>
```

**Python ile XML parse (ElementTree):**
```python
import xml.etree.ElementTree as ET

xml_str = """
<kisi id="101">
  <ad>Ali</ad>
  <yas>22</yas>
  <diller>
    <dil>Python</dil>
    <dil>JavaScript</dil>
  </diller>
</kisi>
"""

root = ET.fromstring(xml_str)
print("ID:", root.attrib.get("id"))
print("Ad:", root.findtext("ad"))
print("Yaş:", root.findtext("yas"))

for dil in root.findall(".//diller/dil"):
    print("Dil:", dil.text)
```

**xmltodict ile pratik dönüşüm:**
```python
import requests, xmltodict

url = "https://www.w3schools.com/xml/simple.xml"
r = requests.get(url, timeout=10)
data = xmltodict.parse(r.text)
# XML -> nested dict
print(data["breakfast_menu"]["food"][0]["name"])
```

**Alıştırma:**
- Bir XML stringinden tüm “dil” etiketlerini listeleyin.

---

## 4) JSON ile API entegrasyonu

**Temel GET (jsonplaceholder):**
```python
import requests

url = "https://jsonplaceholder.typicode.com/todos/1"
r = requests.get(url, timeout=10)
r.raise_for_status()
data = r.json()
print("Kullanıcı:", data["userId"], "Başlık:", data["title"], "Tamamlandı:", data["completed"])
```

**GET + Query Parametreleri:**
```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"
params = {"userId": 1}
r = requests.get(url, params=params, timeout=10)
r.raise_for_status()
for post in r.json()[:3]:
    print(post["id"], post["title"])
print("İstek URL:", r.url)  # otomatik parametre eklendi mi?
```

**POST JSON (oluşturma):**
```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"
payload = {
    "title": "Deneme Başlık",
    "body": "Merhaba Dünya",
    "userId": 1
}
r = requests.post(url, json=payload, timeout=10)  # json= otomatik Content-Type ayarlar
r.raise_for_status()
print("Oluşan kayıt:", r.json())
```

**Header Kullanımı (Accept, Authorization):**
```python
import os, requests

url = "https://httpbin.org/anything"
headers = {
    "Accept": "application/json",
    "Authorization": f"Bearer {os.getenv('API_TOKEN', 'dummy-token')}"
}
r = requests.get(url, headers=headers, timeout=10)
print(r.status_code, r.json().get("headers", {}).get("Authorization"))
```

**Hata Yönetimi:**
```python
import requests

try:
    r = requests.get("https://jsonplaceholder.typicode.com/invalid", timeout=5)
    r.raise_for_status()
    print(r.json())
except requests.exceptions.Timeout:
    print("Zaman aşımı!")
except requests.exceptions.HTTPError as e:
    print("HTTP hatası:", e, "Kod:", getattr(e.response, "status_code", None))
except requests.exceptions.RequestException as e:
    print("Genel istek hatası:", e)
```

**Alıştırmalar:**
- userId=2 olan ilk 5 post’un başlığını listeleyin.
- POST ile yeni bir post oluşturup dönen id alanını yazdırın.
- Hatalı endpoint çağırıp `raise_for_status` ile hatayı yakalayın.

---

## 5) XML ile API entegrasyonu

**XML GET ve Parse (httpbin örneği):**
```python
import requests
import xml.etree.ElementTree as ET

url = "https://httpbin.org/xml"  # RSS benzeri örnek XML döndürür
r = requests.get(url, timeout=10)
r.raise_for_status()

root = ET.fromstring(r.content)
titles = [elem.text for elem in root.findall(".//title")]
print("Başlıklar:")
for t in titles:
    print("-", t)
```

**ECB XML’den kur çekme (namespace ile):**
```python
import requests
import xml.etree.ElementTree as ET

url = "https://www.ecb.europa.eu/stats/eurofxref/eurofxref-daily.xml"
r = requests.get(url, timeout=10)
r.raise_for_status()

root = ET.fromstring(r.content)
ns = {"gesmes": "http://www.gesmes.org/xml/2002-08-01",
      "e": "http://www.ecb.int/vocabulary/2002-08-01/eurofxref"}

cube_date = root.find(".//e:Cube/e:Cube", ns)
rates = {child.attrib["currency"]: child.attrib["rate"] for child in cube_date.findall("e:Cube", ns)}
print("Mevcut kurlar:", list(rates.keys())[:10], "...")
print("EUR->USD:", rates.get("USD"))
print("EUR->TRY:", rates.get("TRY"))
```

**XML POST (echo testi – httpbin):**
```python
import requests

xml_body = """<?xml version="1.0" encoding="UTF-8"?>
<order>
  <id>123</id>
  <customer>Ali</customer>
  <items>
    <item sku="ABC123" qty="2">Kalem</item>
    <item sku="XYZ999" qty="1">Defter</item>
  </items>
</order>
"""

url = "https://httpbin.org/post"
headers = {"Content-Type": "application/xml", "Accept": "application/xml, application/json"}
r = requests.post(url, data=xml_body.encode("utf-8"), headers=headers, timeout=10)
r.raise_for_status()

# httpbin JSON döner ve gönderdiğiniz XML'i 'data' alanında yansıtır
print("Sunucuya gönderilen (echo):")
print(r.json()["data"])
```

**xmltodict ile pratik dönüşüm:**
```python
import requests, xmltodict

url = "https://www.w3schools.com/xml/simple.xml"
r = requests.get(url, timeout=10)
menu = xmltodict.parse(r.text)
for food in menu["breakfast_menu"]["food"]:
    print(food["name"], "-", food["price"])
```

**Alıştırmalar:**
- httpbin.org/xml içinden tüm “item” başlıklarını listeleyin.
- Bir XML body içinde yeni bir alan ekleyip POST edin ve echo çıktısını doğrulayın.
- ECB XML’den EUR->GBP ve EUR->JPY’yi birlikte yazdırın.

---

## 6) Kapanış

**Özet:**
- JSON ve XML’in temellerini gördük.
- requests ile GET/POST, header, parametre, hata yönetimi uyguladık.
- JSON ve XML yanıtlarını güvenle parse etmeyi öğrendik.

**Ödev (isteğe bağlı):**
- Bir hava durumu veya döviz API’sini hem JSON hem XML (mümkünse) biçiminde tüketen bir komut satırı aracı yazın.
- Ortam değişkeninden API anahtarı okuyan bir yapı kurun.
- Yanıtları dosyaya cache’leyip (JSON) tekrar kullanımda API çağrısını azaltın.

**Kaynaklar:**
- requests: https://requests.readthedocs.io
- json modülü: https://docs.python.org/3/library/json.html
- xml.etree.ElementTree: https://docs.python.org/3/library/xml.etree.elementtree.html
- xmltodict: https://github.com/martinblech/xmltodict
- httpbin test uçları: https://httpbin.org
- JSONPlaceholder: https://jsonplaceholder.typicode.com
- ECB XML Kurlar: https://www.ecb.europa.eu/stats/eurofxref/eurofxref-daily.xml