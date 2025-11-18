# Django ile Web Geliştirme

Bu ders, Django kurulumundan başlayarak MVT yapısı, model-view-template oluşturma, admin paneli yönetimi ve kullanıcı rollerine kadar tüm temel konuları kapsar.

---

## 1. Django Kurulumu

### Django Nedir?

- **Django**, Python tabanlı ücretsiz ve açık kaynaklı bir web framework'üdür.
- Hızlı geliştirme, güvenlik ve ölçeklenebilirlik sağlar.
- Instagram, Pinterest, Mozilla gibi büyük projeler Django kullanır.

### Gereksinimler

- Python 3.8 veya üzeri
- pip (Python paket yöneticisi)
- Bir metin editörü (VS Code, PyCharm)

---

### Kurulum Adımları

#### 1. Python Kurulumu Kontrol

```bash
python --version
```

#### 2. Virtual Environment Oluşturma (Önerilen)

```bash
# Windows
python -m venv myenv
myenv\Scripts\activate

# Mac/Linux
python3 -m venv myenv
source myenv/bin/activate
```

**Açıklama:**
- `venv`: Sanal ortam oluşturur
- Her proje için ayrı paket yönetimi
- Çakışmaları önler

#### 3. Django Kurulumu

```bash
pip install django
```

#### 4. Django Sürümünü Kontrol Et

```bash
django-admin --version
```

---

### İlk Django Projesi Oluşturma

```bash
django-admin startproject blog_projesi
cd blog_projesi
```

**Oluşan Dosya Yapısı:**

```
blog_projesi/
    manage.py
    blog_projesi/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```

**Açıklama:**
- `manage.py`: Django komutlarını çalıştırır
- `settings.py`: Proje ayarları
- `urls.py`: URL yönlendirmeleri
- `wsgi.py/asgi.py`: Sunucu yapılandırmaları

---

### Geliştirme Sunucusunu Başlatma

```bash
python manage.py runserver
```

**Tarayıcıda açın:** http://127.0.0.1:8000/

Başarılı kurulum ekranını göreceksiniz!

---

## 2. Django Admin Paneli Oluşturma

### Admin Paneli Nedir?

- Django'nun hazır yönetim paneli
- Veritabanı verilerini kolayca yönetme
- Kullanıcı, içerik, model yönetimi

---

### Veritabanı Oluşturma (Migrate)

```bash
python manage.py migrate
```

**Açıklama:**
- İlk veritabanı tablolarını oluşturur
- Varsayılan olarak SQLite kullanılır
- `db.sqlite3` dosyası oluşur

---

### Superuser (Yönetici) Oluşturma

```bash
python manage.py createsuperuser
```

**Komut satırı soruları:**
```
Username: admin
Email: admin@example.com
Password: ****
Password (again): ****
```

---

### Admin Paneline Giriş

1. Sunucuyu başlat: `python manage.py runserver`
2. http://127.0.0.1:8000/admin/ adresine git
3. Kullanıcı adı ve şifre ile giriş yap

**Admin Paneli Özellikleri:**
- Kullanıcı yönetimi
- Grup yönetimi
- Model verileri görüntüleme/düzenleme

---

## 3. Django ile MVT Yapısı

### MVT Nedir?

**MVT = Model - View - Template**

| **Bileşen** | **Açıklama** | **Benzeri** |
|-------------|--------------|-------------|
| **Model** | Veritabanı yapısı | MVC'deki Model |
| **View** | İş mantığı ve veri işleme | MVC'deki Controller |
| **Template** | HTML şablonu (görünüm) | MVC'deki View |

---

### MVT Çalışma Akışı

```
1. Kullanıcı URL'e istek gönderir
   ↓
2. urls.py ile View'e yönlendirilir
   ↓
3. View, Model'den veri çeker
   ↓
4. View, Template'e veri gönderir
   ↓
5. Template HTML oluşturur ve kullanıcıya döner
```

---

### Örnek MVT Akışı

```python
# Model (veritabanı)
class Makale(models.Model):
    baslik = models.CharField(max_length=200)
    icerik = models.TextField()

# View (mantık)
def makale_listesi(request):
    makaleler = Makale.objects.all()
    return render(request, 'makaleler.html', {'makaleler': makaleler})

# Template (HTML)
{% for makale in makaleler %}
    <h2>{{ makale.baslik }}</h2>
    <p>{{ makale.icerik }}</p>
{% endfor %}
```

---

## 4. Django Uygulama (App) Oluşturma

### App Nedir?

- Django projesi içinde bağımsız modüller
- Her app belirli bir işlevi yerine getirir
- Örnek: blog app, kullanıcı app, ürün app

---

### App Oluşturma

```bash
python manage.py startapp blog
```

**Oluşan Dosya Yapısı:**

```
blog/
    __init__.py
    admin.py
    apps.py
    models.py
    tests.py
    views.py
    migrations/
```

---

### App'i Projeye Kaydetme

**blog_projesi/settings.py:**

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog',  # Yeni eklenen app
]
```

---

## 5. Django Model Oluşturma

### Model Nedir?

- Veritabanı tablolarını Python sınıfları olarak tanımlar
- Her model bir tablo, her alan bir sütun

---

### İlk Model Oluşturma

**blog/models.py:**

```python
from django.db import models

class Makale(models.Model):
    baslik = models.CharField(max_length=200)
    icerik = models.TextField()
    yazar = models.CharField(max_length=100)
    olusturma_tarihi = models.DateTimeField(auto_now_add=True)
    guncelleme_tarihi = models.DateTimeField(auto_now=True)
    
    def __str__(self):
        return self.baslik
    
    class Meta:
        verbose_name = "Makale"
        verbose_name_plural = "Makaleler"
        ordering = ['-olusturma_tarihi']
```

**Açıklama:**
- `CharField`: Kısa metin (max_length zorunlu)
- `TextField`: Uzun metin
- `DateTimeField`: Tarih ve saat
- `auto_now_add=True`: İlk kayıtta otomatik
- `auto_now=True`: Her güncellemede otomatik
- `__str__`: Nesnenin string gösterimi
- `Meta`: Model ayarları
- `ordering`: Sıralama

---

### Migration (Göç) Oluşturma

```bash
python manage.py makemigrations
```

**Çıktı:**
```
Migrations for 'blog':
  blog/migrations/0001_initial.py
    - Create model Makale
```

---

### Migration'ı Veritabanına Uygulama

```bash
python manage.py migrate
```

**Açıklama:**
- Model değişikliklerini veritabanına uygular
- Tablo oluşturur veya günceller

---

### Farklı Alan Türleri

```python
from django.db import models

class Urun(models.Model):
    ad = models.CharField(max_length=100)
    fiyat = models.DecimalField(max_digits=10, decimal_places=2)
    stok = models.IntegerField(default=0)
    aktif = models.BooleanField(default=True)
    resim = models.ImageField(upload_to='urunler/', null=True, blank=True)
    slug = models.SlugField(unique=True)
    
    def __str__(self):
        return self.ad
```

**Alan Türleri:**
- `CharField`: Metin (max_length zorunlu)
- `TextField`: Uzun metin
- `IntegerField`: Tam sayı
- `DecimalField`: Ondalıklı sayı
- `BooleanField`: True/False
- `DateField`: Tarih
- `DateTimeField`: Tarih ve saat
- `ImageField`: Resim (Pillow kurulumu gerekir)
- `FileField`: Dosya
- `SlugField`: URL dostu metin
- `EmailField`: E-posta
- `URLField`: URL

---

### İlişkili Modeller (Foreign Key, Many-to-Many)

```python
class Kategori(models.Model):
    ad = models.CharField(max_length=100)
    
    def __str__(self):
        return self.ad

class Makale(models.Model):
    baslik = models.CharField(max_length=200)
    icerik = models.TextField()
    kategori = models.ForeignKey(Kategori, on_delete=models.CASCADE)
    etiketler = models.ManyToManyField('Etiket', blank=True)
    
    def __str__(self):
        return self.baslik

class Etiket(models.Model):
    ad = models.CharField(max_length=50)
    
    def __str__(self):
        return self.ad
```

**Açıklama:**
- `ForeignKey`: Bire-çok ilişki (bir makale bir kategoriye ait)
- `on_delete=models.CASCADE`: Kategori silinirse makaleler de silinir
- `ManyToManyField`: Çoka-çok ilişki (bir makale birden fazla etikete sahip)

---

## 6. Django Template Oluşturma

### Template Nedir?

- HTML şablonlarıdır
- Django Template Language (DTL) ile dinamik içerik

---

### Template Klasörü Oluşturma

**Proje yapısı:**

```
blog/
    templates/
        blog/
            anasayfa.html
            makale_detay.html
```

---

### İlk Template Oluşturma

**blog/templates/blog/anasayfa.html:**

```html
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <title>Blog Anasayfa</title>
</head>
<body>
    <h1>Blog Anasayfası</h1>
    <p>Hoş geldiniz!</p>
</body>
</html>
```

---

### Django Template Language (DTL) Kullanımı

#### Değişken Yazdırma

```html
<h1>{{ baslik }}</h1>
<p>{{ icerik }}</p>
```

#### For Döngüsü

```html
<ul>
{% for makale in makaleler %}
    <li>{{ makale.baslik }}</li>
{% endfor %}
</ul>
```

#### If Koşulu

```html
{% if kullanici.is_authenticated %}
    <p>Hoş geldin, {{ kullanici.username }}</p>
{% else %}
    <p>Lütfen giriş yapın</p>
{% endif %}
```

#### Template Filtreleri

```html
{{ makale.baslik|upper }}  <!-- Büyük harf -->
{{ makale.icerik|truncatewords:20 }}  <!-- İlk 20 kelime -->
{{ makale.olusturma_tarihi|date:"d/m/Y" }}  <!-- Tarih formatı -->
```

---

### Base Template (Ana Şablon)

**blog/templates/blog/base.html:**

```html
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}Blog{% endblock %}</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body>
    <nav class="navbar navbar-dark bg-dark">
        <div class="container">
            <a class="navbar-brand" href="/">Blog</a>
        </div>
    </nav>
    
    <div class="container mt-4">
        {% block content %}
        {% endblock %}
    </div>
    
    <footer class="bg-light text-center py-3 mt-5">
        <p>&copy; 2025 Blog Projesi</p>
    </footer>
</body>
</html>
```

---

### Base Template'i Extend Etme

**blog/templates/blog/anasayfa.html:**

```html
{% extends 'blog/base.html' %}

{% block title %}Anasayfa - Blog{% endblock %}

{% block content %}
    <h1>Son Makaleler</h1>
    
    {% for makale in makaleler %}
    <div class="card mb-3">
        <div class="card-body">
            <h5 class="card-title">{{ makale.baslik }}</h5>
            <p class="card-text">{{ makale.icerik|truncatewords:30 }}</p>
            <p class="text-muted">{{ makale.yazar }} - {{ makale.olusturma_tarihi|date:"d/m/Y" }}</p>
            <a href="{% url 'makale_detay' makale.id %}" class="btn btn-primary">Devamını Oku</a>
        </div>
    </div>
    {% endfor %}
{% endblock %}
```

---

## 7. Django View Oluşturma

### View Nedir?

- İş mantığını içerir
- Model'den veri çeker
- Template'e veri gönderir

---

### Function-Based View (FBV)

**blog/views.py:**

```python
from django.shortcuts import render
from .models import Makale

def anasayfa(request):
    makaleler = Makale.objects.all()
    context = {
        'makaleler': makaleler
    }
    return render(request, 'blog/anasayfa.html', context)
```

**Açıklama:**
- `request`: HTTP isteği
- `Makale.objects.all()`: Tüm makaleleri getir
- `context`: Template'e gönderilen veriler
- `render()`: Template'i HTML'e dönüştürür

---

### View'i URL'e Bağlama

**blog/urls.py (yeni oluştur):**

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.anasayfa, name='anasayfa'),
]
```

**blog_projesi/urls.py:**

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')),
]
```

---

### Detay Sayfası View'i

**blog/views.py:**

```python
from django.shortcuts import render, get_object_or_404
from .models import Makale

def makale_detay(request, id):
    makale = get_object_or_404(Makale, id=id)
    context = {
        'makale': makale
    }
    return render(request, 'blog/makale_detay.html', context)
```

**blog/urls.py:**

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.anasayfa, name='anasayfa'),
    path('makale/<int:id>/', views.makale_detay, name='makale_detay'),
]
```

**blog/templates/blog/makale_detay.html:**

```html
{% extends 'blog/base.html' %}

{% block title %}{{ makale.baslik }} - Blog{% endblock %}

{% block content %}
    <h1>{{ makale.baslik }}</h1>
    <p class="text-muted">{{ makale.yazar }} - {{ makale.olusturma_tarihi|date:"d F Y" }}</p>
    <hr>
    <p>{{ makale.icerik }}</p>
    <a href="{% url 'anasayfa' %}" class="btn btn-secondary">Geri Dön</a>
{% endblock %}
```

---

## 8. Django ile Dinamik İçerik Oluşturma

### Form Oluşturma

**blog/forms.py (yeni oluştur):**

```python
from django import forms
from .models import Makale

class MakaleForm(forms.ModelForm):
    class Meta:
        model = Makale
        fields = ['baslik', 'icerik', 'yazar']
        widgets = {
            'baslik': forms.TextInput(attrs={'class': 'form-control', 'placeholder': 'Başlık'}),
            'icerik': forms.Textarea(attrs={'class': 'form-control', 'rows': 5}),
            'yazar': forms.TextInput(attrs={'class': 'form-control', 'placeholder': 'Yazar Adı'}),
        }
```

---

### Makale Ekleme View'i

**blog/views.py:**

```python
from django.shortcuts import render, redirect
from .forms import MakaleForm

def makale_ekle(request):
    if request.method == 'POST':
        form = MakaleForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('anasayfa')
    else:
        form = MakaleForm()
    
    return render(request, 'blog/makale_ekle.html', {'form': form})
```

**blog/urls.py:**

```python
urlpatterns = [
    path('', views.anasayfa, name='anasayfa'),
    path('makale/<int:id>/', views.makale_detay, name='makale_detay'),
    path('makale/ekle/', views.makale_ekle, name='makale_ekle'),
]
```

**blog/templates/blog/makale_ekle.html:**

```html
{% extends 'blog/base.html' %}

{% block title %}Yeni Makale Ekle{% endblock %}

{% block content %}
    <h1>Yeni Makale Ekle</h1>
    <form method="post">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit" class="btn btn-success">Kaydet</button>
        <a href="{% url 'anasayfa' %}" class="btn btn-secondary">İptal</a>
    </form>
{% endblock %}
```

---

### Makale Düzenleme

**blog/views.py:**

```python
def makale_duzenle(request, id):
    makale = get_object_or_404(Makale, id=id)
    if request.method == 'POST':
        form = MakaleForm(request.POST, instance=makale)
        if form.is_valid():
            form.save()
            return redirect('makale_detay', id=makale.id)
    else:
        form = MakaleForm(instance=makale)
    
    return render(request, 'blog/makale_duzenle.html', {'form': form, 'makale': makale})
```

---

### Makale Silme

**blog/views.py:**

```python
def makale_sil(request, id):
    makale = get_object_or_404(Makale, id=id)
    if request.method == 'POST':
        makale.delete()
        return redirect('anasayfa')
    
    return render(request, 'blog/makale_sil.html', {'makale': makale})
```

---

## 9. Admin Paneli İçerik Entegrasyonları

### Model'i Admin Paneline Kaydetme

**blog/admin.py:**

```python
from django.contrib import admin
from .models import Makale

admin.site.register(Makale)
```

---

### Gelişmiş Admin Paneli Özelleştirme

```python
from django.contrib import admin
from .models import Makale, Kategori, Etiket

@admin.register(Makale)
class MakaleAdmin(admin.ModelAdmin):
    list_display = ('baslik', 'yazar', 'kategori', 'olusturma_tarihi')
    list_filter = ('kategori', 'olusturma_tarihi')
    search_fields = ('baslik', 'icerik', 'yazar')
    prepopulated_fields = {'slug': ('baslik',)}
    date_hierarchy = 'olusturma_tarihi'
    ordering = ('-olusturma_tarihi',)

@admin.register(Kategori)
class KategoriAdmin(admin.ModelAdmin):
    list_display = ('ad',)
    search_fields = ('ad',)

@admin.register(Etiket)
class EtiketAdmin(admin.ModelAdmin):
    list_display = ('ad',)
```

**Açıklama:**
- `list_display`: Admin listesinde gösterilecek alanlar
- `list_filter`: Filtreleme seçenekleri
- `search_fields`: Arama yapılabilecek alanlar
- `prepopulated_fields`: Otomatik doldurulacak alanlar
- `date_hierarchy`: Tarih bazlı gezinme
- `ordering`: Sıralama

---

## 10. Kullanıcı Rolleri ve Yetkilendirme

### Django Kullanıcı Sistemi

Django varsayılan olarak kullanıcı yönetimi sunar:
- User (Kullanıcı)
- Group (Grup)
- Permission (İzin)

---

### Kullanıcı Kaydı (Register)

**blog/views.py:**

```python
from django.contrib.auth.forms import UserCreationForm
from django.contrib.auth import login

def kayit_ol(request):
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            user = form.save()
            login(request, user)
            return redirect('anasayfa')
    else:
        form = UserCreationForm()
    
    return render(request, 'blog/kayit_ol.html', {'form': form})
```

---

### Giriş (Login) ve Çıkış (Logout)

**blog/urls.py:**

```python
from django.contrib.auth import views as auth_views

urlpatterns = [
    path('', views.anasayfa, name='anasayfa'),
    path('kayit/', views.kayit_ol, name='kayit_ol'),
    path('giris/', auth_views.LoginView.as_view(template_name='blog/giris.html'), name='giris'),
    path('cikis/', auth_views.LogoutView.as_view(next_page='anasayfa'), name='cikis'),
]
```

**blog/templates/blog/giris.html:**

```html
{% extends 'blog/base.html' %}

{% block content %}
    <h1>Giriş Yap</h1>
    <form method="post">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit" class="btn btn-primary">Giriş</button>
    </form>
{% endblock %}
```

---

### Login Gerekli View (Yetkilendirme)

```python
from django.contrib.auth.decorators import login_required

@login_required
def makale_ekle(request):
    if request.method == 'POST':
        form = MakaleForm(request.POST)
        if form.is_valid():
            makale = form.save(commit=False)
            makale.yazar = request.user.username
            makale.save()
            return redirect('anasayfa')
    else:
        form = MakaleForm()
    
    return render(request, 'blog/makale_ekle.html', {'form': form})
```

**settings.py:**

```python
LOGIN_URL = 'giris'
LOGIN_REDIRECT_URL = 'anasayfa'
```

---

### Kullanıcı Grupları ve İzinler

**Admin panelinde:**
1. Groups → Add Group
2. Grup adı: "Editörler"
3. İzinleri seç (add_makale, change_makale, delete_makale)
4. Kullanıcıyı gruba ekle

**View'de grup kontrolü:**

```python
from django.contrib.auth.decorators import login_required, user_passes_test

def is_editor(user):
    return user.groups.filter(name='Editörler').exists()

@login_required
@user_passes_test(is_editor)
def makale_sil(request, id):
    makale = get_object_or_404(Makale, id=id)
    makale.delete()
    return redirect('anasayfa')
```

---

### Template'de Kullanıcı Kontrolü

```html
{% if user.is_authenticated %}
    <p>Hoş geldin, {{ user.username }}</p>
    <a href="{% url 'makale_ekle' %}">Yeni Makale</a>
    <a href="{% url 'cikis' %}">Çıkış</a>
{% else %}
    <a href="{% url 'giris' %}">Giriş Yap</a>
    <a href="{% url 'kayit_ol' %}">Kayıt Ol</a>
{% endif %}
```

---

## 11. Tam Örnek Proje: Blog Uygulaması

### Proje Yapısı

```
blog_projesi/
    manage.py
    blog_projesi/
        settings.py
        urls.py
    blog/
        models.py
        views.py
        urls.py
        forms.py
        admin.py
        templates/
            blog/
                base.html
                anasayfa.html
                makale_detay.html
                makale_ekle.html
```

---

### Örnek Çalışan Kod

**blog/models.py:**

```python
from django.db import models
from django.contrib.auth.models import User

class Kategori(models.Model):
    ad = models.CharField(max_length=100)
    
    def __str__(self):
        return self.ad
    
    class Meta:
        verbose_name_plural = "Kategoriler"

class Makale(models.Model):
    baslik = models.CharField(max_length=200)
    icerik = models.TextField()
    kategori = models.ForeignKey(Kategori, on_delete=models.CASCADE)
    yazar = models.ForeignKey(User, on_delete=models.CASCADE)
    olusturma_tarihi = models.DateTimeField(auto_now_add=True)
    guncelleme_tarihi = models.DateTimeField(auto_now=True)
    
    def __str__(self):
        return self.baslik
    
    class Meta:
        verbose_name_plural = "Makaleler"
        ordering = ['-olusturma_tarihi']
```

---

**blog/views.py:**

```python
from django.shortcuts import render, get_object_or_404, redirect
from django.contrib.auth.decorators import login_required
from .models import Makale
from .forms import MakaleForm

def anasayfa(request):
    makaleler = Makale.objects.all()
    return render(request, 'blog/anasayfa.html', {'makaleler': makaleler})

def makale_detay(request, id):
    makale = get_object_or_404(Makale, id=id)
    return render(request, 'blog/makale_detay.html', {'makale': makale})

@login_required
def makale_ekle(request):
    if request.method == 'POST':
        form = MakaleForm(request.POST)
        if form.is_valid():
            makale = form.save(commit=False)
            makale.yazar = request.user
            makale.save()
            return redirect('anasayfa')
    else:
        form = MakaleForm()
    
    return render(request, 'blog/makale_ekle.html', {'form': form})
```

---

## 12. Kapanış ve Ödevler

### Özet

- **Django Kurulumu**: Virtual environment, pip install django
- **Admin Paneli**: Superuser oluşturma, model kaydetme
- **MVT Yapısı**: Model (veri), View (mantık), Template (görünüm)
- **Model**: Veritabanı tablosu tanımlama
- **View**: İş mantığı ve veri işleme
- **Template**: HTML şablonları ve DTL
- **Dinamik İçerik**: Form, CRUD işlemleri
- **Kullanıcı Rolleri**: Login, yetkilendirme, grup yönetimi

---

### Ödevler

1. **Temel**: Kendi blog projenizi oluşturun, 3 makale ekleyin
2. **Orta**: Kategori sistemi ekleyin, makaleleri kategoriye göre filtreleyin
3. **İleri**: Yorum sistemi ekleyin (kullanıcılar makalelere yorum yapabilsin)
4. **Proje**: Tam özellikli blog: arama, sayfalama, profil sayfası

---

### Kaynaklar

- [Django Resmi Dokümantasyon](https://docs.djangoproject.com/)
- [Django Tutorial](https://docs.djangoproject.com/en/stable/intro/tutorial01/)
- [Django Girls Tutorial](https://tutorial.djangogirls.org/)
- [Django for Beginners](https://djangoforbeginners.com/)

---

**Hazırlayan:** haksaya  
**Tarih:** 2025-11-18  
**Son Güncelleme:** 2025-11-18 11:55:48 UTC

---