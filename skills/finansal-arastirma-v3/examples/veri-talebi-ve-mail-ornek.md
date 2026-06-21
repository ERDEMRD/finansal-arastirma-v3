# Örnek Çıktı — Akıllı Veri Talebi + Mail Formatı (v2)

> v2'nin iki yeni davranışını gösterir: (1) eksik veride pes etmeyip sınırlı bir veri
> isteği sunma, (2) rapor sonunda kurumsal mail formatına çevirme.

---

## THYAO – PGSUS Kıyaslamalı Quant Görünüm
*(as-of: 16 Haziran 2026 kapanışı · Kaynak: TradingView, Mynet)*

**Büyük Resim:** İki havayolu hissesi de 11 Haziran tabanından eş zamanlı ~%10 sıçradı;
hareket sektörel, üzerine PGSUS'ta M&A primi biniyor.

[... fiyat tablosu, z-skor, teknik seviyeler — eldeki veriyle yapılan analiz burada ...]

### Quant Katmanları — Elimizdeki Veriyle
Günlük 5 seanslık pencerede z-skorları hesapladık (THYAO z≈+1,18; PGSUS z≈+1,35).
Ancak **regresyon ve korelasyon katmanı için 5 gözlem yetersiz** — anlamlı bir β veya
ρ tahmini istatistiksel olarak güvenilir olmaz (örneklem çok küçük, GA çok geniş).
Bu yüzden bu katmanı şimdilik **atlıyoruz** ve aşağıda gerekli veriyi istiyoruz.

---

## Daha Derine İnmek İçin İhtiyacım Olan Veri

| İstenen veri | Neyi açar | Üreteceğim ek analiz |
|--------------|-----------|----------------------|
| THYAO + PGSUS günlük kapanış (son ~2 yıl) | Regresyon + korelasyon | β (THYAO~PGSUS), R², asimetrik β⁺/β⁻, pairs trade sinyali |
| Brent günlük kapanış (aynı dönem) | Makro duyarlılık | Asimetrik petrol betası, kuyruk riski |
| VİOP THYAO/PGSUS opsiyon zinciri | Volatilite | IV/HV, skew persentili, hedge maliyeti |

*Bu üçü yeterli; başka veriye gerek yok. Hepsini bir kerede yüklersen raporu bu
analizlerle birlikte yeniden üretirim.*

---

## 📧 Mail Formatı

**Konu:** İLT: THYAO–PGSUS Kıyaslamalı Quant Görünüm

Merhaba,

16 Haziran kapanışı itibarıyla havacılık tarafında dikkat çekici bir tablo görüyoruz:
THYAO ve PGSUS, 11 Haziran tabanından itibaren eş zamanlı ve benzer büyüklükte
(yaklaşık %10) bir yükseliş kaydetti. Hareketin eş zamanlılığı, bunun şirket-spesifik
değil ağırlıkla sektörel bir momentum olduğuna işaret etmektedir; PGSUS özelinde
Smartwings/Czech Airlines beklentisi ek bir M&A primi yaratmaktadır.

Kısa vadeli dağılıma baktığımızda her iki hissenin de kendi son dalga ortalamasının
üzerinde (THYAO z≈+1,2; PGSUS z≈+1,4), ancak henüz ±2σ "aşırı" eşiğine ulaşmadığını
söyleyebiliriz; yani ivme güçlü fakat teknik olarak aşırı alım bölgesinde değil. Daha
sağlam bir β/korelasyon ve opsiyon (skew, IV/HV) okuması için uzun tarihli seriye
ihtiyaç duyuyoruz; bu veriler sağlandığında asimetrik petrol betası ve pairs trade
sinyalini de raporlayabiliriz.

Pozisyon olarak PGSUS'ta M&A hikâyesi nedeniyle seçici bir pozitif eğilim öne çıkarken,
THYAO'da momentum-temelli temkinli pozitif görünüm korunmaktadır. Ana risk, Brent'in
yukarı yönlü hareketinin TL bazında CASK baskısı yaratmasıdır.

Detaylı tablolar ve quant çıktıları raporun tam halindedir.

Saygılarımla,
Araştırma

*Bu e-posta yatırım tavsiyesi değildir; analitik/eğitim amaçlıdır.*
