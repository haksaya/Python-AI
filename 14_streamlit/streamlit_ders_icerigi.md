# Python Streamlit: Web Tabanlı Arayüz Geliştirme – Ders İçeriği

## 1. Giriş

### 1.1 Streamlit Nedir?
- Streamlit, Python ile hızlı ve kolay bir şekilde web tabanlı arayüzler (dashboard, form, görselleştirme) geliştirmeye yarayan bir framework'tür.
- Kod yazarken web arayüzünüzü anlık olarak görebilirsiniz.
- Hiçbir frontend (HTML/CSS/JS) bilgisi olmadan modern arayüzler oluşturabilirsiniz.

---

## 2. Streamlit Kurulumu

### 2.1 Ortam Hazırlığı
- Python yüklü olmalı.
- Tavsiye: Sanal ortam kullanımı (`venv` veya `conda`).

### 2.2 Kurulum Komutu
```bash
pip install streamlit
```

### 2.3 Kurulumun Doğrulanması
```bash
streamlit hello
```
- Bu komutla örnek bir arayüz açılır ve kurulumun başarılı olduğu görülür.

#### Alıştırma:
- Kendi bilgisayarınızda yukarıdaki komutu çalıştırın ve arayüzün açılışını gözlemleyin.

---

## 3. Streamlit ile Web Tabanlı Arayüz Tasarlama

### 3.1 Basit Streamlit Uygulaması
- Yeni bir Python dosyası oluşturun: `app.py`

```python
import streamlit as st

st.title("Hoşgeldiniz!")
st.write("Bu bir örnek Streamlit uygulamasıdır.")
```

- Uygulamayı çalıştırmak için:
```bash
streamlit run app.py
```

### 3.2 Metin ve Başlıklar
```python
st.header("Başlık")
st.subheader("Alt Başlık")
st.text("Sıradan bir yazı")
```

### 3.3 Input (Kullanıcıdan veri alma)
```python
isim = st.text_input("Adınızı girin:")
st.write("Merhaba", isim)
```

### 3.4 Buton ve Etkileşim
```python
if st.button("Tıkla"):
    st.write("Butona tıkladınız!")
```

### 3.5 Seçim Kutusu ve Radio Button
```python
renk = st.selectbox("Bir renk seçin:", ["Kırmızı", "Mavi", "Yeşil"])
st.write("Seçtiğiniz renk:", renk)

secim = st.radio("Favori meyveniz?", ["Elma", "Muz", "Çilek"])
st.write("Seçiminiz:", secim)
```

### 3.6 Dosya Yükleme
```python
dosya = st.file_uploader("Bir dosya yükleyin")
if dosya:
    st.write("Dosya yüklendi:", dosya.name)
```

### 3.7 Görselleştirme (Matplotlib, Altair, Plotly ile)
```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)
y = np.sin(x)

fig, ax = plt.subplots()
ax.plot(x, y)
st.pyplot(fig)
```

#### Alıştırma:
- Kullanıcıdan bir sayı alıp karesini ekranda gösteren küçük bir arayüz tasarlayın.
- Bir liste verip, kullanıcıya seçim yaptıran ve seçimi ekrana yazan uygulama yapın.

---

## 4. Streamlit Metotları

### 4.1 Temel Metotlar
- `st.title()`, `st.header()`, `st.text()`, `st.write()`: Metin ve başlık ekleme.
- `st.button()`, `st.checkbox()`, `st.radio()`, `st.selectbox()`, `st.slider()`: Etkileşimli öğeler.
- `st.file_uploader()`: Dosya yükleme.
- `st.image()`, `st.audio()`, `st.video()`: Medya gösterimi.
- `st.pyplot()`, `st.line_chart()`, `st.bar_chart()`: Grafik ve veri görselleştirme.

### 4.2 Layout (Sayfa düzeni)
```python
col1, col2 = st.columns(2)
col1.button("Sol Buton")
col2.button("Sağ Buton")
```

### 4.3 Sidebar Kullanımı
```python
st.sidebar.title("Yan Menü")
secenek = st.sidebar.selectbox("Bir seçenek seçin", ["A", "B", "C"])
st.write("Seçilen:", secenek)
```

### 4.4 Durum ve Bilgi Mesajları
```python
st.success("İşlem başarılı!")
st.warning("Dikkat!")
st.error("Bir hata oluştu!")
st.info("Bilgilendirme mesajı")
```

#### Alıştırma:
- Sidebar'da seçim yaptırıp ana sayfada sonucu gösteren arayüzü kodlayın.
- Grafik gösteren ve sonucu durum mesajı ile bildiren bir örnek hazırlayın.

---

## 5. Streamlit Yayınlama

### 5.1 Lokal Sunucu ile Yayınlama
- Uygulamanızı geliştirdiğinizde şu komutla lokal olarak yayınlarsınız:
```bash
streamlit run app.py
```
- Tarayıcıda `localhost:8501` adresinde açılır.

### 5.2 Streamlit Cloud ile Yayınlama
- [Streamlit Cloud](https://streamlit.io/cloud) hesabı açın.
- Uygulamanızı GitHub'a yükleyin.
- Streamlit Cloud'da yeni bir uygulama oluşturun ve GitHub repo adresinizi verin.
- Otomatik olarak web'de yayınlanır.

### 5.3 Yayınlama İpuçları
- Gereksiz dosyaları repo’ya eklemeyin.
- `requirements.txt` dosyası ile paketlerinizi belirtin.

#### Alıştırma:
- Kendi Streamlit uygulamanızı GitHub’a yükleyip Streamlit Cloud’da yayınlayın.

---

## 6. Soru-Cevap ve Kapanış

- Streamlit ile ilgili sık yapılan hatalar ve çözümleri.
- Daha fazla öğrenmek için dokümantasyon ve örnek projeler.
- İleri seviye Streamlit konularına giriş önerileri.

---

**Not:** Her bölümde bol örnek ve pratik uygulama vardır. Katılımcılar kendi bilgisayarlarında kodları çalıştırıp görmesi teşvik edilir.