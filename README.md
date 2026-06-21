# 📊 Finansal Araştırma Skill — v3

> Türkiye ve global piyasalar için **ekonometri + quant** temelli, kurumsal düzeyde
> finansal araştırma notları üreten bir [Claude](https://claude.com/claude-code) skill'i.
> **v3 yenilikleri:** Sektör/Tema Primer'i (Market Researcher), Fikir Üretimi/Tarama,
> Katalist Takvimi, Tez Takibi + üçüncü-taraf içerik güvenlik guardrail'i, `[KAYNAK YOK]`
> kaynak disiplini ve insan-onay çerçevesi. (v2'nin akıllı veri talebi + mail formatı korunur.)

[![Skill](https://img.shields.io/badge/type-Claude%20Skill-6b4fbb)](#)
[![Version](https://img.shields.io/badge/version-3.0.0-orange)](CHANGELOG.md)
[![Language](https://img.shields.io/badge/lang-TR-blue)](#)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

---

## Ne yapar?

Bir araştırma masasının ürettiği kalitede finansal notlar yazar. Her not somut veriden
başlar, mekanizmayı kurar, kantitatif çerçeveyle test eder ve uygulanabilir bir
stratejiyle biter:

```
Ham Veri (as-of) → Rejim Tespiti → Spread/Anomali (z-skor) →
Mekanizma → Ekonometrik/Quant Model → Risk & Hedge → Stratejik Yorum
```

Öne çıkan özellikler:

- **8 hazır rapor tipi** — günlük görünüm, makro veri, quant regresyon, opsiyon/vol,
  LME emtia, faiz/PPK, şirket/sektör, haber etki analizi
- **Quant disiplini** — sabit eşik yok; her şey z-skor/persentil, güven aralığı ve
  out-of-sample stabilite ile
- **Türkiye özgün değişkenleri** — AOFM spreadi, asimetrik petrol betası, CDS z-skoru,
  offshore TRY O/N, VİOP max pain
- **Dürüst sonuç** — istatistiksel kenar yoksa "flat" der, pozisyon zorlamaz
- **🆕 Akıllı veri talebi** — eksik veride pes etmez; elindekiyle raporu verir, sonra
  "şu veriyi sağlarsan şunu yaparım" diye **sınırlı, tekrarsız** bir istek sunar
- **🆕 Mail formatı** — rapor sonunda notu "İLT: ..." konulu kurumsal e-postaya çevirir

---

## Kurulum

Bu repo bir **plugin marketplace**'tir. İçinde `finansal-arastirma-v2` plugin'i ve onun
altında skill bulunur. v1 ile yan yana kurulabilir (adlar farklı).

### A) Plugin olarak (Claude Code CLI **ve** Cowork) — önerilen

GitHub'dan (erişimin varsa):

```
/plugin marketplace add ERDEMRD/finansal-arastirma-v2
/plugin install finansal-arastirma-v2@erdemrd-skills-v2
```

Yerel klasörden (kendi makinende test için, GitHub gerekmez):

```
/plugin marketplace add /tam/yol/finansal-arastirma-v2
/plugin install finansal-arastirma-v2@erdemrd-skills-v2
```

Kurulumdan sonra `/finansal-arastirma-v2 <istek>` ile çağır.

### B) Kişisel skill olarak (sadece Claude Code CLI)

```bash
git clone https://github.com/ERDEMRD/finansal-arastirma-v2.git /tmp/fa2
cp -R /tmp/fa2/skills/finansal-arastirma-v2 ~/.claude/skills/finansal-arastirma-v2
```

> Not: `~/.claude/skills/` yalnızca **Claude Code CLI** tarafından okunur. **Cowork**
> (masaüstü agent modu) skilleri yalnızca **plugin** olarak görür → A yolunu kullan.

---

## Kullanım

Skill, aşağıdaki gibi taleplerde otomatik tetiklenir:

| Talep | Üretilen rapor tipi |
|-------|---------------------|
| "Brent–BIST ilişkisini analiz et" | Quant regresyon raporu |
| "Bugünkü piyasa görünümü" | Günlük piyasa notu |
| "TÜİK enflasyon verisini yorumla" | Makro veri yorumu |
| "XAUUSD opsiyon datası ne diyor?" | Opsiyon/volatilite analizi |
| "Bu yasa BIST'i nasıl etkiler?" | Haber → etki analizi |
| "LME bakır görünümü" | Emtia/LME raporu |

**Örnek:**

```
> İLT ABD ENFLASYON mailindeki veriyle enflasyon yorumu yaz
```

Skill, makro veri şablonunu kullanarak "Büyük Resim" başlığı, aylık/yıllık/arındırılmış
tablo, mekanizma zinciri ve stratejik sonuç içeren bir not üretir.

---

## Repo Yapısı

```
finansal-arastirma-v2/                   # marketplace + plugin (repo kökü)
├── .claude-plugin/
│   ├── marketplace.json                 # erdemrd-skills-v2
│   └── plugin.json                      # finansal-arastirma-v2 (2.0.0)
├── README.md  ├── LICENSE  ├── CHANGELOG.md
└── skills/
    └── finansal-arastirma-v2/
        ├── SKILL.md                     # Skill tanımı (Claude bunu okur)
        └── examples/
            ├── ornek-rapor.md           # quant regresyon raporu
            └── makro-rapor-grafikli.md  # grafik + açıklayıcı paragraf
```

---

## Tasarım İlkeleri

Skill tek bir quant disiplinine tabidir:

1. **Sabit yok, görece var** — eşikler tarihsel dağılıma göre z-skor/persentil
2. **Tahmin = belirsizlik** — her katsayı SE ve %95 GA ile
3. **Önce gerçek mi, sahte mi** — durağanlık + örneklem + OOS
4. **Kenar yoksa pozisyon yok** — "flat" geçerli sonuç
5. **Korelasyon ≠ nedensellik** — mekanizmayla doğrulanmamışı işaretle
6. **Veri tazeliği** — her çıktı `as-of: <tarih>` taşır

Detay için → [`SKILL.md`](SKILL.md)

---

## ⚠️ Yasal Uyarı

Bu skill **yatırım tavsiyesi üretmez**. Çıktılar analitik ve eğitim amaçlıdır. Üretilen
notlar piyasa görüşü içerebilir; yatırım kararları kullanıcının kendi sorumluluğundadır.
Geçmiş performans gelecek getirinin garantisi değildir.

---

## Lisans

[MIT](LICENSE) © 2026
