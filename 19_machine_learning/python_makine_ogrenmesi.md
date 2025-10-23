# Python ile Makine Öğrenmesi – 10 Saatlik Basit, Açıklamalı ve Gündelik Hayattan Örneklerle Ders İçeriği

Bu ders, Python ile makine öğrenmesine giriş, Scikit-learn ile uygulamalar ve gündelik hayattan bol örneklerle temel algoritmaları kapsar.

---

## 1. Makine Öğrenmesi Nedir?

- Makine öğrenmesi, bilgisayarların veriden öğrenerek tahmin, sınıflandırma veya karar verme yeteneği kazanmasını sağlar.
- Kodla açık kurallar yazmak yerine bilgisayarın örneklerden genelleme yapması hedeflenir.

**Gündelik Hayat Örneği:**
- E-posta uygulamasının spam olup olmadığını otomatik olarak anlaması.
- Online alışveriş sitelerinin sana uygun ürün önermesi.

---

## 2. Makine Öğrenmesi Temel Kavramlar

- Veri, Özellik (Feature), Etiket (Label/Target)
- Eğitim verisi, test verisi
- Model, tahmin (prediction), hata (loss), doğruluk (accuracy)
- Aşırı öğrenme (overfitting), az öğrenme (underfitting)
- Gözetimli (Supervised), gözetimsiz (Unsupervised) öğrenme

**Gündelik Hayat Örneği:**
- Bir evin fiyatını tahmin ederken oda sayısı, konum, yaş gibi özellikler kullanılır.

---

## 3. SkLearn (Scikit-learn) Kütüphanesi

- Python’da makine öğrenmesi için en yaygın kütüphane.
- Hazır veri setleri, kolay model kurma ve değerlendirme.
- Kurulum:  
  ```bash
  pip install scikit-learn
  ```

**Temel Kullanım:**
```python
from sklearn import datasets
iris = datasets.load_iris()
print(iris.data[:5])    # Özellikler
print(iris.target[:5])  # Sınıflar
```

---

## 4. Regresyon Kavramı

- Regresyon, sayısal bir değeri tahmin etme problemidir.
- Gündelik hayatta: Ev fiyatı, araba değeri, hava sıcaklığı tahmininde kullanılır.

**Örnek:**  
Bir arabanın yaşı ve kilometresi verildiğinde ikinci el fiyatını tahmin etmek.

---

## 5. Sınıflandırma Kavramı

- Sınıflandırma, öğeleri gruplara (sınıflara) ayırma problemidir.
- Gündelik hayatta: E-postanın spam olup olmadığını belirleme, hastalığın olup olmadığını tahmin etme.

**Örnek:**  
Bir öğrencinin sınav notlarına göre “Geçti” veya “Kaldı” olarak sınıflandırılması.

---

## 6. Linear (Doğrusal) Regresyon

- İki değişken arasında doğrusal bağıntı kurar: y = a*x + b
- scikit-learn ile basit uygulama

**Gündelik Hayat Örneği:**
Bir evin metrekaresi ile fiyatı arasındaki ilişki.

**Kod ve Açıklama:**
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression

# Evin metrekaresi ve fiyatı
m2 = np.array([50, 60, 80, 100, 120]).reshape(-1, 1)
fiyat = np.array([150, 170, 210, 250, 270])

model = LinearRegression()
model.fit(m2, fiyat)             # Modeli veriye uydur

print("Tahmin edilen fiyat (90 m2):", model.predict(np.array([[90]])))

plt.scatter(m2, fiyat)
plt.plot(m2, model.predict(m2), color='red')
plt.xlabel("Metrekare")
plt.ylabel("Fiyat")
plt.title("Doğrusal Regresyon: Ev Fiyatı Tahmini")
plt.show()
```
- Modeli eğittik, grafik çizdik, 90 m2 evin tahmini fiyatını bulduk.

---

## 7. Multi Linear (Çoklu Doğrusal) Regresyon

- Birden fazla özellik kullanarak tahmin yapar: y = a1*x1 + a2*x2 + ... + b

**Gündelik Hayat Örneği:**
Evin fiyatını tahmin etmek için hem metrekaresi hem oda sayısı kullanmak.

**Kod ve Açıklama:**
```python
from sklearn.linear_model import LinearRegression
import numpy as np

# Metrekare, oda sayısı
X = np.array([
    [50, 2],
    [60, 2],
    [80, 3],
    [100, 3],
    [120, 4]
])
fiyat = np.array([150, 170, 210, 250, 270])

model = LinearRegression()
model.fit(X, fiyat)

tahmin = model.predict(np.array([[90, 3]]))
print("Tahmin edilen fiyat (90 m2, 3 oda):", tahmin)
```
- İki özelliğe göre fiyat tahmini yaptık.

---

## 8. Ridge Regresyon

- Doğrusal regresyona ceza (regularization) ekler, aşırı öğrenmeyi önler.
- Özellikle çoklu regresyonda faydalı.

**Gündelik Hayat Örneği:**
Birçok özellik içeren ev fiyatı tahmininde bazı özelliklerin etkisini azaltmak.

**Kod ve Açıklama:**
```python
from sklearn.linear_model import Ridge

model = Ridge(alpha=1.0)
model.fit(X, fiyat)
print("Ridge ile tahmin:", model.predict(np.array([[90, 3]])))
```
- Ridge ile modelin karmaşıklığını kontrol ettik.

---

## 9. Lasso Regresyon

- Bazı özelliklerin katsayısını sıfırlayarak gereksiz olanları modelden çıkarır.

**Gündelik Hayat Örneği:**
Ev fiyatını etkileyen çok fazla özellik varsa gereksiz olanları otomatik olarak elemek.

**Kod ve Açıklama:**
```python
from sklearn.linear_model import Lasso

model = Lasso(alpha=0.1)
model.fit(X, fiyat)
print("Lasso ile tahmin:", model.predict(np.array([[90, 3]])))
```
- Lasso ile gereksiz özellikleri modelden attık.

---

## 10. ElasticNet

- Ridge ve Lasso’nun birleşimi, hem ceza hem de gereksiz özellikleri sıfırlama.

**Gündelik Hayat Örneği:**
Ev fiyatı tahmininde hem aşırı öğrenmeyi önlemek hem de önemsiz özellikleri çıkarmak.

**Kod ve Açıklama:**
```python
from sklearn.linear_model import ElasticNet

model = ElasticNet(alpha=0.1)
model.fit(X, fiyat)
print("ElasticNet ile tahmin:", model.predict(np.array([[90, 3]])))
```

---

## 11. Logistic Regresyon

- Sınıflandırma için kullanılır (ör: Geçti/Kaldı, Hasta/Sağlıklı)
- Tahmin edilen değer 0 ile 1 arasında olasılıktır.

**Gündelik Hayat Örneği:**
Bir müşteri alışveriş yaptı mı/yapmadı mı? Bir öğrencinin sınavdan geçip geçmeyeceği.

**Kod ve Açıklama:**
```python
from sklearn.linear_model import LogisticRegression

# Yaş ve saat çalıştı, geçti mi?
X = np.array([
    [18, 2],
    [20, 3],
    [22, 1],
    [25, 4],
    [30, 3]
])
geçti_mi = np.array([0, 1, 0, 1, 1])

model = LogisticRegression()
model.fit(X, geçti_mi)

tahmin = model.predict(np.array([[21, 2]]))
print("Tahmin (21 yaş, 2 saat çalıştı):", "Geçti" if tahmin[0] == 1 else "Kaldı")
```
- Yaş ve çalışma saatine göre geçme tahmini yaptık.

---

## 12. Decision Tree Algoritması

- Karar ağaçları, if-else gibi dallanarak karar verir.
- Hem regresyon hem sınıflandırmada kullanılabilir.

**Gündelik Hayat Örneği:**
Bir banka, kredi başvurusunu onaylarken gelir, yaş, borç gibi kriterlere göre karar verir.

**Kod ve Açıklama:**
```python
from sklearn.tree import DecisionTreeClassifier

# Gelir, yaş, borç var mı? Onaylandı mı? (1: Onay, 0: Red)
X = np.array([
    [3000, 25, 0],
    [4500, 35, 1],
    [2000, 22, 0],
    [5000, 40, 1],
    [2500, 28, 0]
])
onay = np.array([1, 1, 0, 1, 0])

tree = DecisionTreeClassifier(max_depth=2)
tree.fit(X, onay)

sonuc = tree.predict(np.array([[3200, 26, 0]]))
print("Kredi başvurusu:", "Onaylandı" if sonuc[0] == 1 else "Red")
```
- Basit kredi onay simülasyonu.

---

## 13. Random Forest Algoritması

- Birden fazla karar ağacının birleşimi, daha sağlam tahminler.
- Genellikle daha yüksek başarı.

**Gündelik Hayat Örneği:**
Bir alışveriş sitesinde ürün tavsiyeleri birden fazla algoritmanın ortalamasıyla sunulur.

**Kod ve Açıklama:**
```python
from sklearn.ensemble import RandomForestClassifier

forest = RandomForestClassifier(n_estimators=10)
forest.fit(X, onay)

sonuc = forest.predict(np.array([[3200, 26, 0]]))
print("Random Forest ile kredi:", "Onaylandı" if sonuc[0] == 1 else "Red")
```

---

## 14. KNN (K-En Yakın Komşu) Algoritması

- Bir veriye en yakın K komşunun sınıfına bakarak tahmin yapar.
- Özellikle sınıflandırmada popüler.

**Gündelik Hayat Örneği:**
Bir kişinin hobilerine en çok benzeyen kişilerin tercih ettiği tatil destinasyonunu önerme.

**Kod ve Açıklama:**
```python
from sklearn.neighbors import KNeighborsClassifier

X_hobi = np.array([
    [1, 2],    # Deniz, Doğa
    [3, 1],    # Kültür, Deniz
    [2, 3],    # Doğa, Kültür
    [3, 2],    # Kültür, Doğa
    [1, 3]     # Deniz, Kültür
])
tatil = np.array([0, 1, 0, 1, 0])  # 0: Kamp, 1: Otel

knn = KNeighborsClassifier(n_neighbors=3)
knn.fit(X_hobi, tatil)

tahmin = knn.predict(np.array([[2, 2]]))
print("Önerilen tatil:", "Otel" if tahmin[0] == 1 else "Kamp")
```
- Hobi puanlamasına göre tatil önerisi.

---

## 15. Uygulamalar, Değerlendirme ve Kapanış

- Her algoritmadan sonra modelin başarısını ölçmek için accuracy, mean squared error, confusion matrix gibi metrikler kullanılır.
- Sklearn’de model değerlendirme kolaydır:
```python
from sklearn.metrics import accuracy_score

# y_true: gerçek etiketler, y_pred: tahminler
print("Doğruluk:", accuracy_score([1,0,1,1], [1,0,0,1]))
```

**Gündelik Hayat Projesi Önerisi:**  
Kendi veri setinizi oluşturun:  
- Evinizin elektrik faturaları, market harcamaları, spor aktiviteleriniz gibi verileri kullanarak fiyat tahmini, sınıflandırma gibi makine öğrenmesi uygulamaları yapın.

---

## 16. Ödevler ve Kaynaklar

**Ödevler:**
1. Bir ev fiyatı veri seti üretin, Linear ve Ridge regresyon ile tahminler yapın.
2. Öğrenci notlarından geçme tahmini için Logistic Regression ve Decision Tree uygulayın.
3. Kendi alışveriş geçmişinizden ürün kategorisi tahmini için KNN kullanın.
4. Model başarısını ölçmek için doğruluk skorunu ve karışıklık matrisini hesaplayın.

**Kaynaklar:**
- [Scikit-learn belgeleri](https://scikit-learn.org/stable/)
- [Makine Öğrenmesi Temelleri](https://www.kaggle.com/learn/intro-to-machine-learning)
- [Pandas ile Veri Analizi](https://pandas.pydata.org/pandas-docs/stable/getting_started/index.html)
- [Matplotlib ile Görselleştirme](https://matplotlib.org/stable/tutorials/introductory/pyplot.html)

---