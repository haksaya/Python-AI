# 🐍 NumPy – Gerçek Hayat ve Yazılım Geliştirme Süreçlerinden 5 Soru & Cevap

> **Hedef kitle:** NumPy'a yeni başlayanlar  
> **Gereksinim:** `pip install numpy`  
> **Seviye:** Başlangıç → Orta

---

## 📋 İçindekiler

| # | Konu | Kullanılan NumPy Özellikleri |
|---|------|------------------------------|
| [1](#-soru-1--market-sepeti-analizi) | 🛒 Market Sepeti Analizi | `*`, `.sum()`, Boolean Maske |
| [2](#-soru-2--yazılım-ekibi-performans-takibi) | 👩‍💻 Yazılım Ekibi Performans Takibi | `.sum(axis)`, `.mean(axis)`, `.argmax()` |
| [3](#-soru-3--sunucu-sıcaklık-izleme-sistemi) | 🌡️ Sunucu Sıcaklık İzleme | Boolean maske sayma, `axis` |
| [4](#-soru-4--ab-test-sonuçlarını-analiz-etme) | 📊 A/B Test Analizi | `.std()`, `np.where()`, vektör çıkarma |
| [5](#-soru-5--öğrenci-not-sistemi-ve-harf-notu-dönüşümü) | 🎓 Öğrenci Not Sistemi | `@` operatörü, `np.select()`, `~` |

---

## 🛒 Soru 1 – Market Sepeti Analizi

### 📌 Senaryo

Bir market uygulaması geliştiriyorsunuz. Müşterinin sepetinde şu ürünler var:

| Ürün | Birim Fiyat (TL) | Adet |
|------|-----------------|------|
| Süt | 35 | 2 |
| Ekmek | 10 | 3 |
| Yumurta | 45 | 1 |
| Peynir | 80 | 1 |
| Su | 8 | 4 |

### ❓ Görevler

1. Her ürünün **toplam tutarını** (fiyat × adet) hesaplayın.
2. **Sepet toplamını** bulun.
3. **30 TL ve üzeri** toplam tutarlı ürünleri filtreleyin.
4. Tüm ürünlere **%10 indirim** uygulayın, yeni sepet toplamını hesaplayın.

### ✅ Cevap

```python
import numpy as np

# Ürün fiyatları ve adetleri iki ayrı vektörde tutulur
fiyatlar = np.array([35, 10, 45, 80,  8])   # Her ürünün birim fiyatı
adetler  = np.array([ 2,  3,  1,  1,  4])   # Her ürünün adedi

# ── ADIM 1: Her ürünün toplam tutarı ──────────────────────────────────
# Vektörel çarpım: aynı indeksteki elemanlar çarpılır, döngüye gerek yok
tutarlar = fiyatlar * adetler
print("Her ürünün toplam tutarı (TL):", tutarlar)
# ▶ [ 70  30  45  80  32]

# ── ADIM 2: Sepet toplamı ─────────────────────────────────────────────
sepet_toplam = tutarlar.sum()
print("Sepet toplamı:", sepet_toplam, "TL")
# ▶ 257 TL

# ── ADIM 3: 30 TL ve üzeri tutarlı ürünler (Boolean Maskeleme) ────────
# Her tutarı 30 ile karşılaştırıyoruz → True/False dizisi oluşur
maske = tutarlar >= 30
print("Pahalı ürünlerin tutarları:", tutarlar[maske])
# ▶ [70 30 45 80 32]

# ── ADIM 4: %10 indirim uygula ────────────────────────────────────────
# Her elemandan %10 düşürmek için 0.90 ile çarpmak yeterli
indirimli_tutarlar = tutarlar * 0.90
print("İndirimli tutarlar:", indirimli_tutarlar)
# ▶ [63.  27.  40.5 72.  28.8]

indirimli_toplam = indirimli_tutarlar.sum()
print("İndirimli sepet toplamı:", indirimli_toplam, "TL")
# ▶ 231.3 TL