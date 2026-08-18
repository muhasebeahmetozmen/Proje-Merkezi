# Değişiklik Günlüğü

Bu dosya **kullanıcıya görünen** değişiklikleri listeler. Teknik ayrıntılar ve
karar gerekçeleri için [CLAUDE.md](CLAUDE.md) §12'ye bakın.

Sürüm numarası tek bir yerden gelir: `kpm/__init__.py` → `__version__`.

---

## [4.1] — 18.08.2026

### Yeni
- **Otomatik güncelleme.** Program açılışta yeni sürüm var mı diye bakar; varsa
  sorar ve onaylarsan kendisi indirip kurar. Artık GitHub'dan elle dosya
  indirmene gerek yok. Kenar çubuğundaki **"Güncellemeleri denetle"** kutusundan
  kapatabilirsin — kapalıyken program internete kendiliğinden hiç bağlanmaz.
- **Program %84 küçüldü:** kurulum boyutu ~756 MB'tan **~123 MB**'a indi.
  Kullanılmayan Qt bileşenleri (Chromium tabanlı web motoru, QML, tüm dillerin
  çevirileri) paketten çıkarıldı. İndirme ve kurulum belirgin hızlandı.

### Düzeltildi
- **E-Fatura Alış Tevkifat Tarama tamamen onarıldı.** EDM portalı v2.1'e geçince
  modül çalışmıyor, daha kötüsü bazı durumlarda **sessizce yanlış adet**
  raporluyordu (94 faturalı bir mükellefte 18 yazıyordu). Sayım artık ızgaranın
  sayfalayıcısındaki toplamdan okunuyor.
- **Yanlış mükellef sorgulama hatası giderildi.** Tarayıcının otomatik tamamlaması
  arama kutusundaki adı değiştirebiliyor, bir mükellefin adının altında **başka
  mükellefin rakamları** raporlanabiliyordu. Artık yazılan metin geri okunup
  doğrulanıyor; şüphede rakam üretilmiyor, hata veriliyor.
- Portal oturumu düşerse (`Login.aspx`) otomatik yeniden giriş yapılıyor.
- Mükellef **VKN ile de** aranabiliyor; kırpılmış uzun unvanlar doğru eşleşiyor.
- Fatura kesme modülünün kırık yedek adresi düzeltildi (oturumu düşürüyordu).

### Değişti
- **Temalar sadeleşti:** yalnızca **Sistem · Açık · Koyu**. (Kağıt, Gece ve
  Antrasit kaldırıldı; eski tercihiniz kayıtlıysa otomatik "Sistem"e döner.)
- **Fatura Asistanı** ve **Zirve E-Arşiv Tevkifat Sorgulama** modülleri kaldırıldı.
  Buna bağlı `pywinauto` bağımlılığı da çıkarıldı.
- Fatura türü listesi portalın canlı listesinden geliyor ("Konaklama Vergisi" eklendi).

### Türkçe uyumluluğu
- Mükellef listesi `.txt` dosyaları artık **ANSI (cp1254)** kodlamayla da okunuyor —
  Not Defteri ile kaydedilen listeler `ş/ğ/İ` yüzünden okunamıyordu.
- PDF üretiminde Türkçe-uyumlu font seçimi tek kaynağa taşındı ve sağlamlaştırıldı;
  Arial yoksa Segoe UI / Tahoma / Calibri / Verdana sırayla denenir.
- Türkçe karakterler için uçtan uca test paketi eklendi (dosya kodlaması, Türkçe
  klasör/dosya adları, PDF ve Excel çıktıları, büyük/küçük harf dönüşümleri).

### Arayüz
- Boştaki ilerleme çubuğu artık "dolu" görünmüyor.
- Devre dışı **Durdur** düğmesi pasif görünüyor (canlı kırmızı kalmıyordu).
- Koyu temada geri alınamaz **"Resmî Gönder"** düğmesinin kontrastı düzeltildi
  (WCAG AA altındaydı); artık ekrandaki en dikkat çekici öge.
- Anasayfadaki kısayol aralığı ve tema ipucu artık kendini güncelliyor.

---

## [4.0] — 2026

- customtkinter sürümünün (3.2) **PySide6/Qt ile sıfırdan yeniden yazımı**.
- Modül kayıt defteri (registry): yeni modül eklemek için tek bir çağrı yeter.
- Tema değişimi arayüzü yıkmadan, yalnız stylesheet değiştirerek yapılır.
- Uzun işler `QThread` içinde; arayüz donmaz.
- Windows DPAPI ile şifre saklama.
- `.exe` + kurulum dosyası üretimi (PyInstaller + Inno Setup).

---

## Sürüm numarası nasıl artar?

- **Yama (4.1 → 4.1.1):** yalnız hata düzeltmesi.
- **Küçük (4.1 → 4.2):** yeni özellik / modül, mevcut kullanım bozulmadan.
- **Büyük (4.x → 5.0):** kullanıcının alışkanlığını değiştiren köklü değişiklik.
