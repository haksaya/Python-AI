# Django ile Web Yazılımları

Bu ders, web geliştirme temellerini, Frontend-Backend-FullStack kavramlarını, UX/UI tasarımı, HTML, CSS ve Bootstrap'i basitçe ve örneklerle anlatır.

---

## 1. Django ile Web Yazılımları Nedir?

### Django Nedir?

- **Django**, Python ile web siteleri ve uygulamaları geliştirmek için kullanılan güçlü bir **web framework**'üdür.
- Hızlı geliştirme, güvenlik, ölçeklenebilirlik sağlar.
- Instagram, Spotify, YouTube gibi büyük platformlarda kullanılır.

**Neden Django?**
- Python ile yazılır (kolay öğrenme)
- Hazır admin paneli
- Güvenlik özellikleri (SQL injection, XSS koruması)
- ORM (veritabanı yönetimi kolaylaşır)

---

## 2. Frontend, Backend ve FullStack Kavramları

### Frontend Nedir?

- **Frontend (Ön Yüz)**: Kullanıcının gördüğü ve etkileşim kurduğu kısımdır.
- Teknolojiler: **HTML, CSS, JavaScript, Bootstrap, React, Vue**

**Örnekler:**
- Web sitesindeki butonlar, renkler, yazı tipleri
- Kullanıcı formu, menü, görsel tasarım

**Örnek:**
- Bir restoranın menüsü, masaları, dekorasyonu → Frontend

---

### Backend Nedir?

- **Backend (Arka Yüz)**: Kullanıcının görmediği, sunucuda çalışan ve veri işleyen kısımdır.
- Teknolojiler: **Python (Django), Node.js, PHP, Java, veritabanları (MySQL, PostgreSQL, SQLite)**

**Örnekler:**
- Kullanıcı girişi kontrolü
- Veritabanından veri çekme
- E-posta gönderme

**Örnek:**
- Restoranın mutfağı, sipariş yönetimi, stok kontrolü → Backend

---

### FullStack Nedir?

- **FullStack**: Hem Frontend hem de Backend geliştirme yapabilen kişi veya proje.
- Hem kullanıcı arayüzü hem de sunucu tarafı geliştirme.

**FullStack Developer:**
- HTML, CSS, JavaScript bilir (Frontend)
- Python, Django, veritabanı bilir (Backend)

**Örnek:**
- Hem mutfakta yemek yapan hem de servis yapan kişi → FullStack

---

### Karşılaştırma Tablosu

| **Özellik** | **Frontend** | **Backend** | **FullStack** |
|-------------|--------------|-------------|---------------|
| **Görevi** | Kullanıcı arayüzü | Veri işleme, mantık | Her ikisi |
| **Teknolojiler** | HTML, CSS, JS | Python, Django, SQL | Hepsi |
| **Örnek** | Butonlar, formlar | Veritabanı, API | Tüm uygulama |

---

## 3. UX - UI Tasarım Nedir?

### UI Tasarım (User Interface - Kullanıcı Arayüzü)

- **UI**: Web sitesinin görsel tasarımıdır (renkler, butonlar, yazı tipleri).
- Kullanıcının gördüğü her şey UI'dir.

**Örnekler:**
- Buton renkleri
- Menü tasarımı
- Logo, ikonlar

**Örnek:**
- Bir arabanın direksiyon, gösterge paneli, koltuk tasarımı → UI

---

### UX Tasarım (User Experience - Kullanıcı Deneyimi)

- **UX**: Kullanıcının web sitesini kullanırken yaşadığı deneyimdir.
- Kullanıcı memnuniyeti, kolay kullanım, hızlı erişim.

**Örnekler:**
- Formu kolayca doldurabilme
- Hızlı yüklenen sayfalar
- Anlaşılır menü yapısı

**Örnek:**
- Arabanın sürüş konforu, kolay kullanım, güvenlik → UX

---

### UI vs UX Karşılaştırması

| **Özellik** | **UI (Arayüz)** | **UX (Deneyim)** |
|-------------|-----------------|------------------|
| **Odak** | Görsel tasarım | Kullanıcı memnuniyeti |
| **Örnek** | Buton rengi | Butona kolayca tıklama |
| **Araçlar** | Photoshop, Figma | Kullanıcı testleri, anketler |

---

## 4. Web App (Web Uygulaması) Nedir?

- **Web App**: Tarayıcıda çalışan, dinamik ve etkileşimli uygulamalardır.
- Kurulum gerektirmez, internet üzerinden erişilir.

**Örnekler:**
- Gmail (e-posta yönetimi)
- Google Drive (dosya yönetimi)
- Netflix (video izleme)
- Online bankacılık

**Web App vs Web Sitesi:**

| **Web Sitesi** | **Web Uygulaması** |
|----------------|--------------------|
| Statik içerik | Dinamik içerik |
| Bilgi sunar | Kullanıcı etkileşimi |
| Örnek: Blog | Örnek: Gmail |

---

## 5. Temel HTML Eğitimi

### HTML Nedir?

- **HTML (HyperText Markup Language)**: Web sayfalarının iskelet yapısını oluşturur.
- Etiketler (tags) ile çalışır: `<etiket>içerik</etiket>`

---

### İlk HTML Sayfası

```html
<!DOCTYPE html>
<html>
<head>
    <title>İlk Web Sayfam</title>
</head>
<body>
    <h1>Merhaba Dünya!</h1>
    <p>Bu benim ilk web sayfam.</p>
</body>
</html>
```

**Açıklama:**
- `<!DOCTYPE html>`: HTML5 belgesi
- `<html>`: HTML başlangıcı
- `<head>`: Sayfa bilgileri (başlık, meta)
- `<title>`: Sekme başlığı
- `<body>`: Görünen içerik
- `<h1>`: Büyük başlık
- `<p>`: Paragraf

---

### Temel HTML Etiketleri

#### Başlıklar (Headings)

```html
<h1>En Büyük Başlık</h1>
<h2>Alt Başlık</h2>
<h3>Daha Küçük Başlık</h3>
<h4>...</h4>
<h5>...</h5>
<h6>En Küçük Başlık</h6>
```

#### Paragraf ve Metin

```html
<p>Bu bir paragraftır.</p>
<strong>Kalın yazı</strong>
<em>İtalik yazı</em>
<br> <!-- Satır atlatma -->
<hr> <!-- Yatay çizgi -->
```

#### Listeler

```html
<!-- Sırasız Liste -->
<ul>
    <li>Elma</li>
    <li>Armut</li>
    <li>Muz</li>
</ul>

<!-- Sıralı Liste -->
<ol>
    <li>Birinci</li>
    <li>İkinci</li>
    <li>Üçüncü</li>
</ol>
```

#### Linkler ve Görseller

```html
<!-- Link -->
<a href="https://www.google.com">Google'a Git</a>

<!-- Görsel -->
<img src="resim.jpg" alt="Açıklama">
```

#### Tablolar

```html
<table border="1">
    <tr>
        <th>İsim</th>
        <th>Yaş</th>
    </tr>
    <tr>
        <td>Ali</td>
        <td>25</td>
    </tr>
    <tr>
        <td>Ayşe</td>
        <td>30</td>
    </tr>
</table>
```

#### Formlar

```html
<form action="/kaydet" method="POST">
    <label>İsim:</label>
    <input type="text" name="isim" placeholder="Adınızı girin">
    
    <label>E-posta:</label>
    <input type="email" name="email" placeholder="E-posta adresiniz">
    
    <label>Şifre:</label>
    <input type="password" name="sifre">
    
    <button type="submit">Gönder</button>
</form>
```

---

### Örnek: Kişisel Blog Sayfası

```html
<!DOCTYPE html>
<html>
<head>
    <title>Benim Blogum</title>
</head>
<body>
    <h1>Hoş Geldiniz</h1>
    <p>Ben Ali, bu benim kişisel blogum.</p>
    
    <h2>Hakkımda</h2>
    <p>Web geliştirme ile ilgileniyorum.</p>
    
    <h2>Hobilerim</h2>
    <ul>
        <li>Kitap okumak</li>
        <li>Fotoğrafçılık</li>
        <li>Seyahat</li>
    </ul>
    
    <h2>İletişim</h2>
    <a href="mailto:ali@example.com">E-posta Gönder</a>
</body>
</html>
```

---

## 6. Temel CSS Eğitimi

### CSS Nedir?

- **CSS (Cascading Style Sheets)**: HTML sayfalarına stil (renk, yazı tipi, boyut, konum) ekler.
- HTML → İskelet, CSS → Tasarım

---

### CSS Kullanımı

#### 1. Inline CSS (Etiket içinde)

```html
<h1 style="color: blue;">Mavi Başlık</h1>
```

#### 2. Internal CSS (Head içinde)

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        h1 {
            color: red;
            font-size: 40px;
        }
        p {
            color: green;
        }
    </style>
</head>
<body>
    <h1>Kırmızı Başlık</h1>
    <p>Yeşil paragraf.</p>
</body>
</html>
```

#### 3. External CSS (Ayrı dosya)

**style.css:**
```css
h1 {
    color: blue;
    text-align: center;
}
p {
    font-size: 18px;
}
```

**index.html:**
```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Mavi Başlık</h1>
    <p>Stillendirilmiş paragraf.</p>
</body>
</html>
```

---

### Temel CSS Özellikleri

#### Renk ve Yazı

```css
h1 {
    color: #FF5733;           /* Renk */
    font-size: 32px;          /* Yazı boyutu */
    font-family: Arial;       /* Yazı tipi */
    text-align: center;       /* Hizalama */
    text-decoration: underline; /* Alt çizgi */
}
```

#### Arkaplan

```css
body {
    background-color: #f0f0f0;  /* Arkaplan rengi */
    background-image: url('resim.jpg'); /* Arkaplan resmi */
}
```

#### Kutu Modeli (Box Model)

```css
div {
    width: 300px;            /* Genişlik */
    height: 200px;           /* Yükseklik */
    padding: 20px;           /* İç boşluk */
    margin: 10px;            /* Dış boşluk */
    border: 2px solid black; /* Kenarlık */
}
```

#### Hover Efekti

```css
button {
    background-color: blue;
    color: white;
    padding: 10px 20px;
}

button:hover {
    background-color: red; /* Üzerine gelindiğinde kırmızı olur */
}
```

---

### Örnek: Stil Eklenmiş Blog

**index.html:**
```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="style.css">
    <title>Benim Blogum</title>
</head>
<body>
    <h1>Hoş Geldiniz</h1>
    <p class="intro">Bu benim kişisel blogum.</p>
    
    <div class="kutu">
        <h2>Hobilerim</h2>
        <ul>
            <li>Kitap okumak</li>
            <li>Fotoğrafçılık</li>
        </ul>
    </div>
    
    <button>İletişime Geç</button>
</body>
</html>
```

**style.css:**
```css
body {
    background-color: #f9f9f9;
    font-family: Arial, sans-serif;
}

h1 {
    color: #333;
    text-align: center;
}

.intro {
    font-size: 20px;
    color: #555;
    text-align: center;
}

.kutu {
    width: 400px;
    margin: 20px auto;
    padding: 20px;
    background-color: white;
    border: 1px solid #ddd;
    border-radius: 10px;
}

button {
    display: block;
    margin: 20px auto;
    padding: 10px 30px;
    background-color: #007BFF;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}
```

---

## 7. Temel Bootstrap Eğitimi

### Bootstrap Nedir?

- **Bootstrap**, hazır CSS ve JavaScript bileşenleri içeren bir **frontend framework**'üdür.
- Hızlı ve responsive (mobil uyumlu) tasarım yapılmasını sağlar.

**Neden Bootstrap?**
- Hazır bileşenler (buton, form, tablo, menü)
- Mobil uyumlu (responsive)
- Hızlı prototip geliştirme

---

### Bootstrap Kurulumu

#### CDN ile (En Kolay Yol)

```html
<!DOCTYPE html>
<html>
<head>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <h1 class="text-center">Bootstrap ile Merhaba!</h1>
    
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

---

### Temel Bootstrap Bileşenleri

#### 1. Grid Sistemi (Düzen)

```html
<div class="container">
    <div class="row">
        <div class="col-md-4" style="background-color: lightblue;">Kolon 1</div>
        <div class="col-md-4" style="background-color: lightgreen;">Kolon 2</div>
        <div class="col-md-4" style="background-color: lightcoral;">Kolon 3</div>
    </div>
</div>
```

**Açıklama:**
- `container`: Sayfayı merkezler
- `row`: Satır oluşturur
- `col-md-4`: Ekran genişliğinin 1/3'ü (12 sütunluk sistem: 4+4+4=12)

---

#### 2. Butonlar

```html
<button class="btn btn-primary">Mavi Buton</button>
<button class="btn btn-success">Yeşil Buton</button>
<button class="btn btn-danger">Kırmızı Buton</button>
<button class="btn btn-warning">Sarı Buton</button>
```

---

#### 3. Formlar

```html
<div class="container mt-5">
    <form>
        <div class="mb-3">
            <label class="form-label">İsim</label>
            <input type="text" class="form-control" placeholder="Adınızı girin">
        </div>
        
        <div class="mb-3">
            <label class="form-label">E-posta</label>
            <input type="email" class="form-control" placeholder="E-posta adresiniz">
        </div>
        
        <button type="submit" class="btn btn-primary">Gönder</button>
    </form>
</div>
```

---

#### 4. Kartlar (Cards)

```html
<div class="container">
    <div class="row">
        <div class="col-md-4">
            <div class="card">
                <img src="resim1.jpg" class="card-img-top" alt="...">
                <div class="card-body">
                    <h5 class="card-title">Başlık 1</h5>
                    <p class="card-text">Bu bir karttır.</p>
                    <a href="#" class="btn btn-primary">Detay</a>
                </div>
            </div>
        </div>
    </div>
</div>
```

---

#### 5. Navbar (Menü)

```html
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
        <a class="navbar-brand" href="#">Logo</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav">
                <li class="nav-item">
                    <a class="nav-link active" href="#">Ana Sayfa</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Hakkımızda</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">İletişim</a>
                </li>
            </ul>
        </div>
    </div>
</nav>
```

---

### Örnek: Kişisel Portföy Sitesi

```html
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portföy Sitem</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <!-- Menü -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
        <div class="container">
            <a class="navbar-brand" href="#">Ali Yılmaz</a>
            <ul class="navbar-nav">
                <li class="nav-item"><a class="nav-link" href="#">Ana Sayfa</a></li>
                <li class="nav-item"><a class="nav-link" href="#">Projeler</a></li>
                <li class="nav-item"><a class="nav-link" href="#">İletişim</a></li>
            </ul>
        </div>
    </nav>
    
    <!-- Hero Bölümü -->
    <div class="bg-light text-center py-5">
        <h1>Merhaba, Ben Ali!</h1>
        <p class="lead">Web Developer & Designer</p>
        <button class="btn btn-primary btn-lg">Projelerimi Görüntüle</button>
    </div>
    
    <!-- Projeler -->
    <div class="container my-5">
        <h2 class="text-center mb-4">Projelerim</h2>
        <div class="row">
            <div class="col-md-4">
                <div class="card">
                    <img src="proje1.jpg" class="card-img-top" alt="Proje 1">
                    <div class="card-body">
                        <h5 class="card-title">E-Ticaret Sitesi</h5>
                        <p class="card-text">Django ile geliştirildi.</p>
                        <a href="#" class="btn btn-outline-primary">Detay</a>
                    </div>
                </div>
            </div>
            
            <div class="col-md-4">
                <div class="card">
                    <img src="proje2.jpg" class="card-img-top" alt="Proje 2">
                    <div class="card-body">
                        <h5 class="card-title">Blog Sitesi</h5>
                        <p class="card-text">HTML, CSS, Bootstrap</p>
                        <a href="#" class="btn btn-outline-primary">Detay</a>
                    </div>
                </div>
            </div>
            
            <div class="col-md-4">
                <div class="card">
                    <img src="proje3.jpg" class="card-img-top" alt="Proje 3">
                    <div class="card-body">
                        <h5 class="card-title">Portföy Sitesi</h5>
                        <p class="card-text">Responsive tasarım</p>
                        <a href="#" class="btn btn-outline-primary">Detay</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Footer -->
    <footer class="bg-dark text-white text-center py-3">
        <p>&copy; 2025 Ali Yılmaz. Tüm hakları saklıdır.</p>
    </footer>
    
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

---

## 8. Kapanış ve Ödevler

### Özet

- **Frontend**: Kullanıcının gördüğü arayüz (HTML, CSS, Bootstrap)
- **Backend**: Sunucu tarafı mantık (Django, Python, veritabanı)
- **FullStack**: Her ikisini birden yapabilme
- **UX/UI**: Kullanıcı deneyimi ve arayüz tasarımı
- **HTML**: Sayfa yapısı
- **CSS**: Görsel tasarım
- **Bootstrap**: Hızlı ve responsive tasarım

---

### Ödevler

1. **HTML:** Kendi CV'nizi HTML ile oluşturun (isim, eğitim, deneyim, iletişim)
2. **CSS:** CV sayfanıza CSS ile stil ekleyin (renk, yazı tipi, kutu tasarımı)
3. **Bootstrap:** Bootstrap kullanarak kişisel portföy sitesi yapın (menü, projeler, iletişim formu)
4. **Kombine:** Bir restoran menü sayfası yapın (HTML+CSS+Bootstrap)

---

### Kaynaklar

- [W3Schools HTML](https://www.w3schools.com/html/)
- [W3Schools CSS](https://www.w3schools.com/css/)
- [Bootstrap Resmi Dokümantasyon](https://getbootstrap.com/docs/)
- [MDN Web Docs](https://developer.mozilla.org/)
- [Django Resmi Dokümantasyon](https://docs.djangoproject.com/)

---

**Hazırlayan:** haksaya  
**Tarih:** 2025-11-18  
**Son Güncelleme:** 2025-11-18 11:45:46 UTC

---