# Pip

## Pip Nedir?
Pip, Python paket yöneticisidir. Python kütüphanelerini yüklemek, güncellemek ve kaldırmak için kullanılır.

## Temel Komutlar
```bash
pip install paket_adi           # Paket yükleme
pip uninstall paket_adi         # Paket kaldırma
pip show paket_adi               # Paket bilgisi
pip list                         # Kurulu paketleri listeleme
pip install paket_adi==1.2.0     # Belirli sürümü yükleme
pip install --upgrade paket_adi  # Paket güncelleme
pip freeze > requirements.txt    # Paket listesini kaydetme
pip install -r requirements.txt  # Paket listesinden yükleme
```

## Uygulama Örneği
```bash
pip install numpy
pip show numpy
pip list
pip uninstall numpy
```

## Alıştırmalar
1. Terminalde `pip --version` çalıştırın.
2. `requests` kütüphanesini yükleyin ve `pip show requests` ile bilgilerini görün.
3. Tüm kurulu paketleri `pip list` ile listeleyin.
