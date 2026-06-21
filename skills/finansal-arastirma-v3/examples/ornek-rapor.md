# Örnek Çıktı — Quant İlişki / Regresyon Raporu

> Bu, skill'in **2.3 Quant İlişki Raporu** şablonuyla ürettiği örnek bir nottur.
> Sayılar yalnızca format gösterimidir; gerçek analizde o anki veriyle yeniden hesaplanır.

---

## Brent Petrol – BIST100 Kantitatif İlişki
*(Örneklem: 103 haftalık gözlem, ~2 yıl · as-of: 2026-05-20)*

**Büyük Resim:** Brent ile BIST100 arasındaki ilişki doğrusal değil, **asimetrik**.
Standart lineer model yetersiz kalıyor; petrol yükselişi ile düşüşü endekse farklı
şiddette geçiyor.

### Spot Değerler
- Brent: **108.88 $**
- BIST100: **13.962,85**

### Model Karşılaştırma

| Model | Katsayı (SE) | %95 GA | R² | p | OOS stabil? |
|-------|-------------|--------|-----|-----|-------------|
| Lineer (Y = βX + α) | β = −0.041 (0.038) | [−0.116, 0.034] | 0.04 | 0.28 | ✗ |
| β⁺ (Brent yükselişinde) | −0.134 (0.052) | [−0.236, −0.032] | — | 0.01 | ✓ |
| β⁻ (Brent düşüşünde) | −0.008 (0.049) | [−0.104, 0.088] | — | 0.87 | ✓ |

### Yorum
- **Lineer model çöküyor:** R² = 0.04 ve p = 0.28 — tek bir beta ile ilişki
  istatistiksel olarak anlamsız. Tek başına okunsaydı "Brent BIST'i etkilemiyor"
  denirdi; bu yanlış olurdu.
- **Asimetri gerçek:** `β⁺ = β⁻` hipotezi reddediliyor. Brent yükselişinde β⁺ = −0.134
  (p = 0.01, anlamlı), düşüşünde β⁻ ≈ 0 (p = 0.87, anlamsız). Yani **petrol artışı
  BIST'e negatif geçiyor, ama düşüşü pozitif katkı yapmıyor.**
- **Mekanizma:** Brent ↑ → ithal enflasyon ↑ → TÜFE yapışkanlaşır → TCMB sıkı kalır →
  iskonto oranı yükselir → endeks baskılanır. Düşüşte bu zincir simetrik çalışmıyor
  çünkü maliyet düşüşü fiyatlara hızla yansımıyor (asimetrik fiyat geçişkenliği).

### Koşullu Beklenti
Brent'in mevcut seviyeden %10 yükseldiği senaryoda:

```
E(ΔBIST | ΔBrent = +%10) ≈ β⁺ × 10 + α ± 1σ
                          ≈ −1.34% ± 0.9%
```

---

## Stratejik Özet  *(as-of: 2026-05-20)*

- **Pozisyon:** Brent yükseliş rejiminde enerji-yoğun/ulaşım hisseleri **Underweight**;
  düşüş rejiminde **Nötr** (asimetri nedeniyle long kenarı zayıf).
- **Kenar gerekçesi:** β⁺ anlamlı (p = 0.01, GA sıfırı içermiyor); β⁻ anlamsız
  (GA sıfırı içeriyor) → yalnızca yukarı şokta ticari kenar var.
- **Zaman ufku:** Orta (1–3 ay) — petrol rejimi ve TCMB tepkisine bağlı.
- **Katalizör:** Jeopolitik prim kaynaklı Brent > 110 $ kalıcılığı.
- **Risk senaryosu:** Jeopolitik çözülme → Brent geri çekilir → asimetri nedeniyle
  short pozisyon hızla zarar etmez ama kenar kaybolur.
- **Hedge:** THYAO/ulaşım sepeti üzerine protective put; enerji üreticileri ile
  pairs trade (eşbütünleşme teyidiyle).
- **Aksiyon:**
  1. Brent yükseliş rejimi teyit edilirse ulaşım/sanayi ağırlığını azalt.
  2. Enerji üreticilerini relatif overweight yap (asimetrik kazanan).
  3. β⁺'yı rolling 60-gün pencerede izle; stabilite bozulursa pozisyonu gözden geçir.

---

*Bu not yatırım tavsiyesi değildir; analitik/eğitim amaçlıdır.*
