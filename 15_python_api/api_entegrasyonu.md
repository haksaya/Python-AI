# 🧩 Python ile API Entegrasyonu (requests)

Bu doküman, Python `requests` kütüphanesi kullanarak API entegrasyonunun
temel adımlarını gerçek bir senaryo üzerinden anlatır.

------------------------------------------------------------------------

## 🎯 Senaryo

Bir blog sistemi geliştiriyoruz:

-   Kullanıcıya ait postları çek
-   İlk birkaç postu listele
-   Yeni bir post oluştur
-   Hataları güvenli şekilde yakala

------------------------------------------------------------------------

## ⚙️ Gereksinimler

``` bash
pip install requests
```

------------------------------------------------------------------------

## 🧾 Örnek Kod

``` python
import requests
import os

BASE_URL = "https://jsonplaceholder.typicode.com"
API_TOKEN = os.getenv("API_TOKEN", "dummy-token")

headers = {
    "Accept": "application/json",
    "Authorization": f"Bearer {API_TOKEN}"
}

try:
    print("📥 Kullanıcının postları çekiliyor...")

    params = {"userId": 2}

    response = requests.get(
        f"{BASE_URL}/posts",
        params=params,
        headers=headers,
        timeout=5
    )

    response.raise_for_status()
    posts = response.json()

    print("\n📝 İlk 5 post:")
    for post in posts[:5]:
        print(f"ID: {post['id']} | Başlık: {post['title']}")

    print("\n🔗 Gerçekleşen URL:", response.url)

    print("\n📤 Yeni post oluşturuluyor...")

    new_post = {
        "title": "API ile oluşturulan yazı",
        "body": "Bu içerik Python requests ile gönderildi.",
        "userId": 2
    }

    post_response = requests.post(
        f"{BASE_URL}/posts",
        json=new_post,
        headers=headers,
        timeout=5
    )

    post_response.raise_for_status()
    created_post = post_response.json()

    print("\n✅ Yeni post oluşturuldu!")
    print("Yeni ID:", created_post.get("id"))

    print("\n⚠️ Hatalı endpoint test ediliyor...")

    bad_response = requests.get(
        f"{BASE_URL}/invalid-endpoint",
        timeout=5
    )

    bad_response.raise_for_status()

except requests.exceptions.Timeout:
    print("⏱️ Zaman aşımı oluştu!")

except requests.exceptions.HTTPError as e:
    print("🚨 HTTP hatası:", e)

except requests.exceptions.RequestException as e:
    print("❌ Genel hata:", e)
```

------------------------------------------------------------------------

## 🚀 Alıştırmalar

1.  userId=2 olan ilk 5 post'u listeleyin\
2.  POST ile yeni kayıt oluşturup id yazdırın\
3.  Hatalı endpoint ile hata yakalayın
