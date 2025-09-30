# Python Mini Proje: Şehir Adına Göre Hava Durumu Sorgulama

## Proje Açıklaması

Bu mini projede, kullanıcıdan bir şehir adı alınacak ve bu şehirle ilgili güncel hava durumu verileri bir API üzerinden çekilip terminalde gösterilecektir. Hava durumu verisi için [OpenWeatherMap](https://openweathermap.org/api) API'si kullanılacaktır.

---

## Adımlar

### 1. OpenWeatherMap API Anahtarı Alın

- [OpenWeatherMap](https://openweathermap.org/) sitesine kaydolun.
- “API keys” bölümünden ücretsiz bir API anahtarı alın.

### 2. Gerekli Kütüphaneyi Yükleyin

Terminalden:
```bash
pip install requests
```

---

### 3. Kodun Tamamı

```python
import requests

def hava_durumu_getir(sehir, api_key):
    url = f"http://api.openweathermap.org/data/2.5/weather"
    params = {
        "q": sehir,
        "appid": api_key,
        "lang": "tr",
        "units": "metric"
    }
    try:
        response = requests.get(url, params=params)
        response.raise_for_status()
        veri = response.json()
        print(f"\n{sehir.title()} için hava durumu:")
        print(f"Sıcaklık: {veri['main']['temp']}°C")
        print(f"Durum: {veri['weather'][0]['description']}")
        print(f"Nem: %{veri['main']['humidity']}")
        print(f"Rüzgar Hızı: {veri['wind']['speed']} m/s")
    except requests.exceptions.RequestException as e:
        print("İstek sırasında hata oluştu:", e)
    except KeyError:
        print("Şehir bulunamadı veya API cevabı beklenmedik.")

def main():
    api_key = "YOUR_API_KEY_HERE"  # Buraya kendi API anahtarınızı girin!
    sehir = input("Hava durumunu öğrenmek istediğiniz şehir: ")
    hava_durumu_getir(sehir, api_key)

if __name__ == "__main__":
    main()
```

---

### 4. Kullanım

1. Kodun içinde `"YOUR_API_KEY_HERE"` kısmını kendi anahtarınız ile değiştirin.
2. Programı çalıştırın:
    ```bash
    python hava_durumu.py
    ```
3. Program sizden bir şehir adı isteyecek, örneğin: `İstanbul`
4. Sonuçlar terminalde gösterilecektir.

---

### 5. Örnek Çıktı

```
Hava durumunu öğrenmek istediğiniz şehir: Ankara

Ankara için hava durumu:
Sıcaklık: 19.5°C
Durum: açık
Nem: %45
Rüzgar Hızı: 2.5 m/s
```

---

### 6. Ekstra İpuçları

- Farklı şehirler için tekrar tekrar sorgulama ekleyebilirsiniz.
- Hatalı şehir adı girildiğinde kullanıcıya tekrar sorma mekanizması ekleyebilirsiniz.
- Farklı bir API veya farklı bilgileri (örneğin, hava basıncı) gösterebilirsiniz.

---

**Not:** API anahtarınız olmadan veri çekemezsiniz! Ücretsiz anahtar almak çok kolaydır.