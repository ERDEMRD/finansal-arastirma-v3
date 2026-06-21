# Changelog

Bu projedeki kayda değer değişiklikler bu dosyada tutulur.
Format [Keep a Changelog](https://keepachangelog.com/tr/1.0.0/) standardına dayanır.

## [3.0.0] — 2026-06-21 (v3 — ayrı klasör)

v2 üzerine, Anthropic [Financial-Services](https://github.com/anthropics/financial-services)
agent/skill desenleri incelenip masamızın iş akışına uyanlar entegre edildi. v2'nin tüm
quant çerçevesi (5 katman, iki test, denge mantığı), veri talebi protokolü ve mail formatı
**aynen korunur**.

### Eklendi
- **Bölüm 0 — Çalışma Ürünü, Güvenlik ve Kaynak Disiplini**
  - **Çalışma ürünü çerçevesi:** çıktı = analistin onaylayacağı taslak; tavsiye/işlem/dağıtım yok.
  - **İnsan-onay kontrol noktaları (stop & surface):** comps spread, not taslağı ve fikir
    listesi sonrası dur-ve-incelemeye-sun.
  - **Üçüncü-taraf içerik güvenlik guardrail'i (prompt-injection):** yutulan `.msg`/PDF/
    Excel/broker/KAP/web içeriğindeki talimatlar komut değil **veri**dir; asla yürütülmez.
  - **Kaynak/atıf disiplini:** her sayı kaynaklı; kaynaklanamayan `[KAYNAK YOK]` etiketli
    (tahmin yasak); kaynak çakışınca öncelik hiyerarşisi; connector/MCP > web.
- **Bölüm 5.6 — Quant Araç Kutusu & Yönlendirme Matrisi (quant × temel):** soru→teknik→veri/frekans/min-örneklem→kaynak→tuzak matrisi; finansal mühendislik araç
  ailesi (kointegrasyon vs korelasyon, GARCH/EWMA/realize vol, Markov/HMM rejim, Black-Scholes/
  Monte Carlo türev fiyatlama, Vasicek/CIR/Hull-White/HJM vade yapısı, VaR/Expected Shortfall);
  örneklem/frekans eşikleri, teknik öncelik karar ağacı, teknik↔kaynak bağı ve **quantamental**
  sentez ilkesi. İnternetten quant research taranarak (kointegrasyon, quantamental, GARCH,
  rejim, kısa-faiz modelleri, skew/RR, VaR↔ES) ve yüklenen finansal mühendislik cheat sheet'iyle
  (Bölüm 14.1 formül ailesi) harmanlandı.
- **Bölüm 6.9 — Sektör/Tema Primer'i** *(Market Researcher iş akışı)*: genel görünüm +
  rekabet haritası + peer comps spread (aynı mali yıl, outlier z-skor flag) + 3-5 isimlik
  fikir kısa listesi + not (opsiyonel slayt).
- **Bölüm 6.10 — Fikir Üretimi / Tarama:** değer/büyüme/kalite/short/özel-durum taramaları +
  tema değer-zinciri sweep + isim başına tez/risk/katalist kartı.
- **Bölüm 6.11 — Katalist Takvimi:** kazanç/TCMB-Fed/TÜİK-veri/KAP olayları + etki(Y/O/D) +
  konumlanma + haftalık önizleme.
- **Bölüm 6.12 — Tez Takibi:** yanlışlanabilir tez + pillar scorecard + güncelleme logu +
  konviksiyon + stop/çıkış tetiği.

### Değişti
- Plugin/skill adı `finansal-arastirma-v3`, marketplace `erdemrd-skills-v3`.
- İçindekiler ve giriş, Bölüm 0 ve 6.9–6.12 ile genişletildi.

### Korundu
- 5 katmanlı quant çerçeve, iki-test mantığı, vade/eğri okuma, sektör çerçeveleri, model
  seçim protokolü, Türkiye özgün değişkenleri, referans formüller, veri talebi protokolü
  ve "İLT: ..." mail formatı — hiçbiri kaldırılmadı.


## [2.0.0] — 2026-06-17 (v2 — ayrı repo)

v1 (`finansal-arastirma`) üzerine iki yeni davranış eklenerek ayrı repo olarak yayınlandı.
v1'in tüm quant çerçevesi (5 katman, iki test, denge mantığı) korunur.

### Eklendi
- **Eksik Veri & Veri Talebi Protokolü (Bölüm 15)** — veri eksikse önce kendisi çekmeyi
  dener, elindekiyle raporu verir, sonra net ve sınırlı bir veri isteği sunar
  ("şu veriyi sağlarsan şu analizi yaparım"). Aşırı/gereksiz veri istemez, tekrar tekrar
  sormaz, tek seferde gruplu ister. Veri gelince raporu baştan sormadan yeniler.
- **Mail Formatına Çevirme (Bölüm 16)** — rapor bittikten sonra ekstra olarak notu
  "İLT: ..." konulu, akıcı paragraflı kurumsal araştırma e-postası formatına çevirir.

### Değişti
- Plugin/skill adı `finansal-arastirma-v2`, marketplace `erdemrd-skills-v2`
  (v1 ile yan yana kurulup kıyaslanabilmesi için).

## [1.2.1] — 2026-06-17

### Değişti
- Quant katmanları artık "zorunlu" değil, **"iki test"e bağlı**: (1) uygun veri var mı?
  (2) mantıklı/ekonomik ilişki var mı? İkisi de evetse katman kesinlikle uygulanır;
  biri hayırsa zorlanmaz ama nedeni bir cümleyle belirtilir.
- Denge vurgusu: ne yapay zorlama (anlamsız regresyon/uydurma korelasyon), ne tembellik
  (sadece haber tarayıp fiyat+ortalama yazmak).
- Görsel ilkesi "uygunsa tercih et" olarak güncellendi (veri elverişliyse kur, değilse zorlama).

## [1.2.0] — 2026-06-17

### Eklendi
- **Quant Derinlik Standardı (Bölüm 5)** — her analizde varsayılan, genel-geçer 5 katman:
  ① regresyon & asimetrik beta (β⁺/β⁻) ② korelasyon matrisi & eşbütünleşme
  ③ dağılım & volatilite (z-skor, EWMA) ④ opsiyon (IV/HV, skew, RR, term structure, gamma)
  ⑤ koşullu beklenti & VaR. Kullanıcı tek tek istemese de uygulanır.
- "Kapsam kuralı": fiyat + hareketli ortalama tek başına analiz sayılmaz; en az Katman 1–3
  zorunlu. Veri yoksa katman sessizce atlanmaz, belirtilir.
- İlke #2 "Quant derinlik varsayılan" eklendi; iş akışı Adım 5 "atlanamaz" yapıldı.
- Referans formüllere CAPM, beta, korelasyon, EWMA varyans, Sharpe eklendi.

### Değişti
- Rapor tipleri hangi quant katmanlarını içereceğine göre etiketlendi.
- Plugin marketplace yapısına geçildi (önceki sürümde): repo artık `.claude-plugin/` +
  `skills/finansal-arastirma/` ile hem CLI hem plugin kurulumunu destekler.

## [1.1.1] — 2026-06-17

### Değişti
- Görsel artık **zorunlu değil, yerinde kullanılıyor**. "Ne zaman grafik, ne zaman
  gerekmez" karar kuralı eklendi (Bölüm 3): veri-yoğun analizlerde grafik önerilir,
  kısa günlük/haber/faiz-duyurusu notlarında gerekmez.
- Rapor tipleri (Bölüm 5) "grafik zorunlu" yerine tip bazında "önerilir/gerekmez" olarak
  işaretlendi.

## [1.1.0] — 2026-06-17

### Eklendi
- **Gerçek veri zorunluluğu** — uydurma sayı yasak; veri hiyerarşisi (kullanıcı → dosya
  → canlı çekme → python hesaplama) ve doğruluk kuralları (Bölüm 2)
- **Görselleştirme bölümü** — bulgu→grafik eşleme tablosu, Chart.js/matplotlib üretimi,
  her grafikte başlık/kaynak/as-of zorunluluğu (Bölüm 3)
- **Açıklayıcı anlatım tonu** — gerekçeler madde değil, neden-sonuç kuran akıcı
  paragraflarla; zayıf vs güçlü yazım örneği (Bölüm 4)
- Rapor tiplerine grafik gereksinimi eklendi
- İkinci örnek: `examples/makro-rapor-grafikli.md` (grafik kodu + paragraf anlatımı)

## [1.0.0] — 2026-06-17

### Eklendi
- İlk yayın: `SKILL.md` quant temelli finansal araştırma notu üreteci
- 8 hazır rapor tipi şablonu (günlük görünüm, makro veri, quant regresyon,
  opsiyon/volatilite, LME emtia, faiz/PPK, şirket/sektör, haber etki analizi)
- Quant disiplini: z-skor/persentil eşikler, güven aralıkları, OOS stabilite,
  model seçim protokolü (durağanlık → anlamlılık → asimetri → çoklu test)
- Türkiye özgün değişkenler referansı (AOFM spreadi, asimetrik petrol betası,
  CDS z-skoru, offshore TRY O/N, VİOP max pain)
- Sektör analiz çerçeveleri (inşaat, havacılık, bankacılık, LME, enerji)
- Haber → etki zinciri tetikleyicileri
- README, LICENSE (MIT), örnek rapor
