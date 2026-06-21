# Örnek Çıktı — Makro Veri Yorumu (grafikli + açıklayıcı)

> Bu, skill'in **5.2 Makro Veri Yorumu** şablonuyla ürettiği örnek bir nottur.
> Gerçek veri (kullanıcı maili) + grafik + akıcı paragraf anlatımının nasıl bir araya
> geldiğini gösterir. Sayılar kullanıcının paylaştığı veriden gelir; türetilen kalem
> "artık olarak hesaplandı" diye işaretlenir.

---

## ABD Tüketici Enflasyonu (TÜFE) — Mayıs 2026
*(Kaynak: kullanıcı verisi / US BLS · as-of: 2026-06-10)*

**Büyük Resim:** Dezenflasyon anlatısı kırıldı — manşet enflasyon düşmedi, enerji şokuyla yukarı sıçradı; ama altta yatan çekirdek aslında soğuyor.

### Katkı Ayrıştırması

| Dönem | Manşet TÜFE | Enerji katkısı | Enerji-dışı (artık) |
|-------|-------------|----------------|---------------------|
| Nisan 2026 | %3,8 | ~0,0 puan | 3,8 puan |
| Mayıs 2026 | %4,2 | 1,5 puan | 2,7 puan |

```html
<!-- Chart.js yığılı çubuk: manşete katkı ayrıştırması -->
<div style="position: relative; width: 100%; height: 300px;">
  <canvas id="c" role="img"
    aria-label="Yığılı çubuk: nisan manşet 3.8 tamamı enerji-dışı; mayıs manşet 4.2, enerji 1.5 enerji-dışı 2.7">
    Nisan 3.8 puan tamamı enerji-dışı. Mayıs 4.2 puan: enerji 1.5, enerji-dışı 2.7.
  </canvas>
</div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<script>
new Chart(document.getElementById('c'), {
  type: 'bar',
  data: {
    labels: ['Nisan 2026', 'Mayıs 2026'],
    datasets: [
      { label: 'Enerji-dışı', data: [3.8, 2.7], backgroundColor: '#185FA5', stack: 's' },
      { label: 'Enerji',      data: [0.0, 1.5], backgroundColor: '#BA7517', stack: 's' }
    ]
  },
  options: {
    responsive: true, maintainAspectRatio: false,
    scales: { x: { stacked: true }, y: { stacked: true, beginAtZero: true,
      title: { display: true, text: 'Manşete katkı (puan)' } } }
  }
});
</script>
```

### Yorum

Manşet enflasyonun %3,8'den %4,2'ye yükselmesi ilk bakışta dezenflasyon sürecinin
bozulduğu izlenimini verse de, sıçramanın kompozisyonu bambaşka bir hikâye anlatıyor.
Grafikte net görüldüğü gibi, artışın tamamı enerji kaleminden kaynaklanıyor: enerjinin
manşete katkısı bir ayda neredeyse sıfırdan 1,5 puana fırlamış durumda. Buna karşılık,
enerji-dışı (çekirdeğe yakın) katkı 3,8 puandan 2,7 puana **gerilemiş**. Yani altta
yatan fiyat baskısı aslında soğuyor; manşeti yukarı iten yegâne güç dışsal enerji şoku.

Bu ayrım, enflasyonun karakterini belirlediği için kritik. Enerji kaynaklı bir sıçrama,
tanımı gereği **arz yönlü (cost-push)** bir olaydır ve merkez bankaları bu tür geçici
şoklara genelde "bakar geçer" (look-through) yaklaşımıyla karşılık verir; çünkü faiz
artırmak bir varil petrolün arzını artırmaz. Dolayısıyla manşetteki bu yükselişin
Fed'in faiz patikasını tek başına değiştirmesi olası değil — kritik eşik, şokun
çekirdeğe ve ücretlere sıçrayarak (ikincil tur etkisi) beklenti çıpasını bozup
bozmayacağıdır.

### Korelasyon mu, nedensellik mi?

Burada nedensellik mekanik olarak doğrulanabilir: katkı ayrıştırması bir muhasebe
kimliğidir, yani "enerji manşeti yukarı itti" ifadesi istatistiksel bir korelasyon
değil tanımsal bir gerçektir. Asıl belirsizlik enerjinin manşeti ittiğinde değil, bu
itişin kalıcı olup olmayacağında.

---

## Stratejik Özet  *(as-of: 2026-06-10)*

- **Pozisyon:** USD tahvilde Nötr→Underweight; tam yön için çekirdek verisi gerektiğinden kısmen **FLAT**.
- **Kenar gerekçesi:** Şok arz-yönlü ve enerjiyle açıklanıyor; çekirdeğe geçiş henüz veriyle teyitli değil → agresif pozisyon için kenar zayıf.
- **Zaman ufku:** Kısa (0–1 ay) — bir sonraki çekirdek/supercore açıklamasına kadar.
- **Katalizör:** Çekirdek de yükselirse "higher for longer" güçlenir → tahvil short doğrulanır.
- **Risk senaryosu:** Jeopolitik çözülme → enerji primi geri alınır → manşet normalize → pozisyon ters döner.
- **Hedge:** Long enerji / kısa ulaşım sepeti; tahvilde payer swaption (faiz yukarı riskine ucuz koruma).
- **Aksiyon:**
  1. Manşeti değil, bir sonraki çekirdek + supercore baskısını izle.
  2. Brent'in 100 $ üzeri kalıcılığını takip et.
  3. SOFR futures eğrisinde indirim fiyatlamasının geri çekilmesini doğrulama sinyali al.

*Bu not yatırım tavsiyesi değildir; analitik/eğitim amaçlıdır.*
