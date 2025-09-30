# Streamlit Basit ve Güzel Proje Örnekleri

## 1. Anlık Metin Analizi Uygulaması

### Amaç
Kullanıcıdan bir metin alınır; kelime sayısı, karakter sayısı ve en çok geçen kelime gösterilir.

```python
import streamlit as st
from collections import Counter

st.title("Anlık Metin Analizi")

metin = st.text_area("Metninizi buraya yazın", "")
if metin:
    kelimeler = metin.split()
    karakter_sayisi = len(metin)
    kelime_sayisi = len(kelimeler)
    en_cok = Counter(kelimeler).most_common(1)[0][0] if kelimeler else "Yok"

    st.write(f"Kelime sayısı: {kelime_sayisi}")
    st.write(f"Karakter sayısı: {karakter_sayisi}")
    st.write(f"En çok geçen kelime: {en_cok}")
```

---

## 2. Kullanıcıdan Sayı Alıp Grafik Çizen Uygulama

### Amaç
Kullanıcı bir sayı girer, o kadar uzun bir rastgele sayı listesi üretilip histogram çizilir.

```python
import streamlit as st
import numpy as np
import matplotlib.pyplot as plt

st.title("Rastgele Sayı Histogramı")
adet = st.slider("Kaç sayı üretelim?", min_value=10, max_value=1000, step=10, value=100)
veri = np.random.randn(adet)

fig, ax = plt.subplots()
ax.hist(veri, bins=20, color="skyblue")
st.pyplot(fig)
```

---

## 3. Basit Döviz Kuru Uygulaması (API ile)

### Amaç
Kullanıcı para birimini seçer, API'den güncel döviz kurunu gösterir.

```python
import streamlit as st
import requests

st.title("Döviz Kuru Sorgulama")

para_birimi = st.selectbox("Para birimi seçin", ["USD", "EUR", "GBP"])
api_url = f"https://api.exchangerate-api.com/v4/latest/{para_birimi}"

if st.button("Kurları Göster"):
    r = requests.get(api_url)
    if r.status_code == 200:
        veri = r.json()
        st.write("TRY kuru:", veri["rates"]["TRY"])
        st.write("EUR kuru:", veri["rates"]["EUR"])
        st.write("USD kuru:", veri["rates"]["USD"])
    else:
        st.error("Veri alınamadı.")
```

---

## 4. Anlık Hava Durumu Gösterici

### Amaç
Kullanıcıdan şehir alır, OpenWeatherMap API ile hava durumu raporunu gösterir.

```python
import streamlit as st
import requests

st.title("Anlık Hava Durumu")

sehir = st.text_input("Şehir adı girin")
api_key = "YOUR_API_KEY_HERE"

if st.button("Sorgula") and sehir:
    url = f"http://api.openweathermap.org/data/2.5/weather?q={sehir}&appid={api_key}&units=metric&lang=tr"
    r = requests.get(url)
    if r.status_code == 200:
        veri = r.json()
        st.write("Sıcaklık:", veri["main"]["temp"], "°C")
        st.write("Durum:", veri["weather"][0]["description"])
        st.write("Nem:", veri["main"]["humidity"])
    else:
        st.error("Şehir bulunamadı veya API anahtarı hatalı.")
```
> Not: `api_key` alanına kendi OpenWeatherMap API anahtarını girmen gerekir.

---

## 5. Basit To-Do List (Yapılacaklar Listesi)

### Amaç
Kullanıcı yeni görev ekler, eklenen görevler listelenir ve tamamlananlar işaretlenir.

```python
import streamlit as st

st.title("Yapılacaklar Listesi")

if "gorevler" not in st.session_state:
    st.session_state["gorevler"] = []

yeni_gorev = st.text_input("Yeni görev ekle")
if st.button("Ekle") and yeni_gorev:
    st.session_state["gorevler"].append({"ad": yeni_gorev, "tamam": False})

for i, gorev in enumerate(st.session_state["gorevler"]):
    tamamlandi = st.checkbox(gorev["ad"], value=gorev["tamam"], key=i)
    st.session_state["gorevler"][i]["tamam"] = tamamlandi
```

---
