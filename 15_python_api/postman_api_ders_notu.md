# API Metotlarının Postman Benzeri Araçlarla Test Edilmesi
## Öğretmen Ders Notu

---

## 🎯 Dersin Amacı

Bu derste öğrencilerin:

- API kavramını anlaması  
- HTTP metodlarını tanıması (GET, POST, PUT, DELETE)  
- Bir API’ye istek gönderip yanıtları yorumlayabilmesi  
- Temel hata durumlarını analiz edebilmesi hedeflenmektedir  

---

## 🧰 Kullanılacak Araçlar

- Postman (tercihen)
- Alternatif olarak tarayıcı tabanlı araçlar da kullanılabilir (https://hoppscotch.io/)

---



---

## 1️⃣ Giriş


### Tahtada Örnek

```
GET /posts        → tüm veriler
GET /posts/1      → tek kayıt
POST /posts       → yeni kayıt
```

### Vurgu

- API’ler sistemler arası iletişim sağlar  
- JSON veri formatı en yaygın kullanılan formattır  

---

## 2️⃣ Araç Tanıtımı 


- URL alanı  
- Method seçimi (GET, POST vs.)  
- Headers bölümü  
- Body (istek içeriği)  
- Response (sunucu cevabı)  

---

## 3️⃣ Uygulama 1: GET (Veri Çekme) 

### Kullanılacak Endpoint

https://jsonplaceholder.typicode.com/posts

### Yapılacaklar

- GET isteği gönderilir  
- Dönen JSON veri incelenir  

### Ek Çalışma

https://jsonplaceholder.typicode.com/posts?userId=1



---

## 4️⃣ Uygulama 2: GET (Tek Kayıt) 

### Endpoint

https://jsonplaceholder.typicode.com/posts/1

### Öğrenci Görevi

- JSON içeriğini incele  
- Aşağıdaki alanları bul:
  - id
  - title
  - body  

---

## 5️⃣ Uygulama 3: POST (Veri Gönderme) 
### Endpoint

https://jsonplaceholder.typicode.com/posts

### Body (JSON)

{
  "title": "Benim ilk API postum",
  "body": "Postman ile gönderildi",
  "userId": 1
}

### Yapılacaklar

- POST metodu seçilir  
- Body kısmına JSON eklenir  
- İstek gönderilir  

---

## 6️⃣ Uygulama 4: Header Kullanımı

Authorization: Bearer test123

### Açıklama

- Header’lar ek bilgileri taşır  
- Özellikle kimlik doğrulamada kullanılır  

---

## 7️⃣ Uygulama 5: Hata Senaryosu 

### Hatalı Endpoint

https://jsonplaceholder.typicode.com/invalid

### Öğrenci Görevi

- İstek gönder  
- Status code’u incele  
- Hata mesajını yorumla  

---

## 8️⃣ Bonus: PUT & DELETE (5 dk)

PUT /posts/1  
DELETE /posts/1  

### Açıklama

- PUT → güncelleme  
- DELETE → silme  

---
