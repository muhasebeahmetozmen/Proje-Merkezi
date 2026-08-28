# Değişiklik Günlüğü

Bu dosya **kullanıcıya görünen** değişiklikleri listeler. Teknik ayrıntılar ve
karar gerekçeleri için [CLAUDE.md](CLAUDE.md) §12'ye bakın.

Sürüm numarası tek bir yerden gelir: `kpm/__init__.py` → `__version__`.

---


## v5.1 — Kullanım turu düzeltmeleri

Üç araçta, günlük kullanımda göze çarpan üç sorun giderildi. **Yeni araç yok,
ayarlarınız ve kayıtlı listeleriniz olduğu gibi kalıyor.**

### 🔴 Düzeltildi — Otobüsçü Fatura Kesme: yeni mükellefe başkasının IBAN'ı yazılıyordu

**"Yeni Mükellef"** penceresi bir önceki mükellefin **ödeme şeklini, kanalını
ve IBAN'ını** hazır getiriyordu. Kolaylık olsun diye konmuştu ama tehlikeliydi:
adı yazıp Kaydet'e basınca, altta duran ödeme bilgileri fark edilmeden yeni
mükellefe geçiyor ve **fatura başkasının hesabını gösteriyordu**.

Pencere artık **boş açılıyor**. Var olan bir mükellefi **✏ ile düzenlerken**
kendi bilgileri yine dolu geliyor; kayıtlı mükelleflerinizin ödeme bilgilerine
dokunulmadı.

### Düzeltildi — Banka Ekstresi Adlandırma: Kuveyt Türk hesap numarası

Kuveyt Türk ekstreleri **IBAN'ın son 4 hanesiyle** adlandırılıyordu. O haneler
bu bankada `0001` gibi anlamsız bir kuyruk oluyor ve **aynı müşterinin bütün ek
hesapları aynı ada düşüyordu** — dosyaları birbirinden ayırmak mümkün değildi.

Artık ekstrenin başlığındaki gerçek hesap okunuyor:

| Ekstre başlığı | Eski ad | Yeni ad |
|---|---|---|
| `Hesap Bilgisi:  7062710 - 1` | `kuveyt türk 0001` | **`kuveyt türk 2710-1`** |

Yani **hesap numarasının son 4 hanesi + ek numarası**. Kuveyt Türk'ün IBAN'sız
ekstre biçimi de aynı adı üretiyor (eskiden `1658 - 1` yazıyordu, artık
`1658-1`) — aynı hesap, hangi biçimde gelirse gelsin **tek bir ada** düşüyor.

⚠️ Diğer bankalar **etkilenmedi**: Denizbank yine son 6 hane (`7000 06`),
kalanlar son 4 hane.

### Düzeltildi — Araç Satış Yazısı: Marka ve Model örnekleri tersti

Alanlardaki sönük örnekler yer değiştirdi. Program zaten
*"… PLAKALI **2026** MODEL **RENAULT CLIO 1.5 DCI**, …"* cümlesini kuruyor;
örnekler ters olduğu için sizi ters doldurmaya yönlendiriyordu.

| Alan | Eski örnek | Yeni örnek |
|---|---|---|
| Marka | `RENAULT` | **`RENAULT CLIO 1.5 DCI`** |
| Model | `CLIO 1.5 DCI` | **`2026`** (araç yılı) |

### Notlar
- Birim test **916 → 924**; üç düzeltmenin her biri testle kilitlendi.
- Yeni bağımlılık yok, kurulum boyutu değişmedi.


## v5.0 — Altı yeni araç (7 → 13)

> GitHub'da son yayımlanan sürüm **v4.5**'ti. O günden bu yana eklenen
> altı modül (TC/VKN Sorgulama · Banka Ekstresi Adlandırma · Poliçe
> Hesaplama · Fatura Kalem Listesi · İnternet Satıcıları Fatura
> Otomasyonu · **GİB Kesinti Tarayıcı**) tek bir büyük güncellemede
> toplandı. Ara sürümlerin ayrıntısı:
> [belgeler/gecmis/changelog-eski.md](belgeler/gecmis/changelog-eski.md)

### GİB Kesinti Tarayıcı

### Eklendi
- 🆕 **Tam otomatik tarama — "kataloğun tamamı" artık gerçekten yapılabilir.**
  GİB tek istekte birden çok kesinti türü vermiyor (denendi, kapalı), o yüzden
  iş **üç kademeye** bölündü: **Keşif** (135 türün hepsi, 6 yıl — bir kez),
  **Banka dahil** (ay ay, yalnız gereken türlerde), **Bakım** (her gece:
  son aylar + kataloğun dönüşümlü bir dilimi). Program taramayı başlatmadan
  **kaç istek atacağını, ne kadar süreceğini ve kaç geceye yayılacağını**
  söylüyor. "Bu koşuda en fazla N sorgu" diyebilirsiniz: bütçe dolunca
  tarama **temiz durur**, yapılanlar kaydedilir, bir sonraki koşu kaldığı
  yerden devam eder. *Kotaya takılıp saatlerce beklemek yok.*
- 🆕 **Ücret, kira ve menkul sermaye kesintileri de geliyor.** GİB'in ana
  kesinti ekranı **"ücretler üzerinden yapılan kesintiler hariç"** diyor —
  yani ücret stopajını hiç göstermiyordu. O veri GİB'in "Mali Bilgilerim"
  bölümünde; artık oradan da çekiliyor (ücret stopajı, kira stopajı, menkul
  sermaye iradı kesintileri, temettü). **Yıl başına tek istek** — çok ucuz.
  ⚠️ Bu kalemler dökümde **ayrı bölümde** durur ve ana toplama **eklenmez**:
  aynı kesinti iki kaynakta birden görünebiliyor, toplasaydık mahsup şişerdi.
  İşlevi çapraz kontrol: *"ana ekranda görünmeyen bir kesinti var mı?"*
- 🆕 **GİB'in kendi toplamıyla karşılaştırma.** GİB her yanıtta toplam matrahı
  ve kesilen vergiyi de söylüyor. Program artık kendi topladığını onunla
  karşılaştırıyor; tutmazsa dökümde **"DİKKAT Toplam Tutmadı"** bölümü çıkıyor.
  Üç gerçek mükellefte kuruşuna kadar tuttu.

### Düzeltildi (27.08.2026 — GİB'e canlı bağlanılarak bulundu)
- 🔴 **Kesintiler iki kez sayılabiliyordu.** "Banka kesintileri dahil"
  seçeneği, sanıldığı gibi *yalnız* banka kesintilerini getirmiyor —
  normal kesintileri de **üstüne ekliyor**. Tam kapsama isteyip iki kipi de
  tarayan herkes normal kesintileri iki kez topluyordu. Artık aynı ay için
  "banka dahil" sorgu geçerli sayılıyor, tutar **tek kez** sayılıyor.
  (Arayüzdeki "Yalnız BANKA kesintileri" yazısı da yanlıştı, düzeltildi.)
- 🔴 **Geçici bir GİB arızası "şifre hatalı" sanılıyordu.** GİB bazen
  *"…bir süre sonra tekrar denemeniz gerekmektedir"* diyor; program bunu
  şifre reddi sayıp o mükellefi **atlıyor** ve size "giriş kabul edilmedi"
  yazıyordu. Aynı giriş iki dakika sonra sorunsuz geçiyordu. Artık kısa
  bekleyip yeniden deniyor.
- 🟠 **Boşuna sorulan tür grubu.** GİB'in tür listesinde sorgulanamayan bir
  beyanname türü (`GVK67`) vardı; "kataloğun tamamı" taramasında her seferinde
  hata dönüyordu. Artık katalogdan eleniyor.
- **Yeni modül: Gib Kesinti Tarayıcı (13. araç).** Mükelleflerin **adına
  yapılan kesintileri (stopaj)** Dijital Vergi Dairesi'nden toplu çeker,
  biriktirir ve mahsupta kullanacağınız Excel/HTML dökümünü üretir. Her
  mükellef kendi kullanıcı adı ve şifresiyle sorgulanır; giriş ekranındaki
  **güvenlik kodunu program kendisi okur.**
- **Ünvan ve VKN'yi kendisi getiriyor.** Mükellefi eklerken yalnız GİB
  kullanıcı adı ve şifresi yeterli; ünvan ile VKN e-Arşiv portalından
  kendiliğinden geliyor. Toplu tamamlama düğmesi de var.
- **Çekilmiş dönem bir daha sorulmuyor.** Kapanmış bir ayın kesintisi
  değişmez; program yalnız yeni dönemleri ve **son 3 ayı** yeniliyor
  (geç beyan ve düzeltme gelebilir diye).
- **GİB'in istek kotasını kendisi öğreniyor.** Kotaya yaklaşınca yavaşlıyor,
  sınıra takılırsa bekliyor; açılmıyorsa **erken pes edip ilerlemeyi
  kaydediyor** ve "sonra devam et" diyor. Aynı düğmeye basınca kalan yerden
  sürüyor.
- **Gece taraması.** Zamanlama sayfasından Windows'a bir görev kurup
  bilgisayar açıkken, siz başında olmadan taratabilirsiniz. Yönetici yetkisi
  istemez.
- **Döküm dürüst.** Alınamayan sorgular Excel'de **ayrı sayfada**, HTML'de
  kırmızı bantta görünür — "toplam şu kadar" diyen bir dökümün eksik olduğu
  gözden kaçmaz. GİB bir kaydın ayını vermezse dönem hücresi **(?)** ile
  işaretlenir; uydurma ay yazılmaz.
- Her mükellef Excel'de **kendi sayfasında**, TOPLAM satırı gerçek `=SUM`
  formülüyle — satır silerseniz Excel toplamı kendisi günceller.

### 🔴 Ayrı programdaki ciddi hatalar düzeltildi
- **Mükellef listeniz ve şifreleriniz kaybolabiliyordu — ve kayboldu.**
  Eski program mükellef dosyasını Drive ile senkronlanan bir klasörde
  tutuyordu. Windows koruması dosyayı *o bilgisayara* bağlar; ikinci
  bilgisayar üstüne yazınca dosya birincide **hiç açılamaz** oldu — şifreler
  ve ünvanlar birlikte gitti. Yeni modülde dosya buluttan **çıkarıldı** ve
  yalnız **şifre alanı** şifreleniyor: bilgisayar değiştirdiğinizde listeniz
  açılır, sadece şifreleri bir kez yeniden girersiniz.
- **Milyonluk bir kesinti sıfır görünebiliyordu.** "1.000.000" gibi bir tutar
  okunamayınca program sessizce **0** yazıyordu. Mahsup tablosuna sıfır
  girerdi ve hiçbir yerde uyarı çıkmazdı. Düzeltildi ve testle kilitlendi.
- **Aynı kesinti raporda iki kez sayılabiliyordu.** Önce "son 3 ay", sonra
  "son 12 ay" taradığınızda ortak aylar iki kez toplanıyor ve döküm **tam iki
  katı** çıkıyordu — hiçbir uyarı olmadan. Gece taraması bunu kendiliğinden
  üretiyordu. Düzeltildi; artık çekilmiş bir ay ikinci kez ne sorulur ne
  sayılır.
- **GİB'in "oturumunuz düştü" yanıtı "kayıt yok" sayılıyordu.** O dönem
  boş kabul edilip bir daha sorulmuyordu — mahsupta koca bir dönem sessizce
  eksik kalabilirdi.
- **Excel'de süzgeç kullanınca toplam yanlış görünüyordu.** "Yalnız Ocak"
  süzdüğünüzde ekranda 3 satır, altında **yılın toplamı** yazıyordu. Artık
  toplam süzgeci takip ediyor.
- **Mükellef listesi yenilenince eski veriler kaybolmuş görünüyordu.** Artık
  VKN ile kendiliğinden geri bağlanıyor — yeniden taramaya gerek yok.
- **Şahıs firmaları hiç taranamayacaktı.** Program mükellefi doğrularken tek
  bir numaraya bakıyordu; oysa şahıs firmasının hem TCKN'si hem VKN'si var ve
  GİB'in iki ekranı iki farklı numara döndürüyor. Bu mükellefler "yanlış
  mükellef" sayılıp **her taramada atlanacaktı**. Canlı denemede yakalandı.
- Ayrıca: rapordaki "hangi türlerde kayıt var" bölümü hep boş çıkıyordu ·
  yeni bir bilgisayarda ünvan sorgulama sessizce kapalı geliyordu · dönemi
  belirsiz kalemler her döneme birden sayılıyordu · tazelenemeyen dönemler
  sessizce bayat veri gösteriyordu. Hepsi düzeltildi.


> Bu düzeltmelerin çoğu, modül bittikten sonra yapılan **bağımsız bir
> denetimden** çıktı: altı ayrı denetçi programı çürütmek için taradı, 46
> iddianın 30'u kod çalıştırılarak doğrulandı ve giderildi. Geri kalanı
> **gerçek GİB'e bağlanınca** ortaya çıktı.

✅ **Gerçek veriyle denendi.** Mevduat kesintisi olan bir mükellefte 61 ham
kayıt 5 kaleme toplandı; tutarlar ve dönemler birebir tuttu, tek bir "(?)"
işaretli satır çıkmadı.

⚠️ **Eski programın verisi alınmıyor.** Bir ara eski aracın veritabanı ilk
açılışta kopyalanıyordu; artık kopyalanmıyor. Sıfırdan başlıyorsunuz: mükellef
listesini girin, bir kez "Tür kataloğunu yenile" deyin, tarayın.

⚠️ **İlk kullanımda:** mükelleflerinizi Excel'den içe aktarın (ya da eski
kasadan aktarmayı deneyin), bir kez "Tür kataloğunu yenile" deyin ve **tek bir
mükellefle, kısa bir dönemle** başlayın. GİB'in kotası dar; program yavaş
çalışıyor ve bu kasıtlı.

### İnternet Satıcıları Fatura Otomasyonu

### Eklendi
- **Yeni modül: İnternet Satıcıları Fatura Otomasyonu (12. araç).** Pazaryeri
  satıcılarının EDM / e-Arşiv fatura raporlarını okur, her satıra Zirve hesap
  planından hesap kodunu yazar ve muhasebeye aktarılacak Excel'i üretir.
  Ayrı bir program olarak çalışan sürüm (tarayıcı paneli + kendi Python'u)
  Proje Merkezi'ne taşındı; artık tek pencerede, tek temada çalışıyor.
- **Çift kayıt koruması**: daha önce işlenmiş faturalar (ETTN) yeni raporda
  gelirse çıkarılır ve raporda listelenir.
- **Red / İptal / Taslak** faturalar muhasebeye girmez, ayrı listelenir.
- **"Rapor" sayfası**: her kodlanmış dosyanın içinde özet, KDV mutabakatı,
  tevkifatlı faturalar, kod yazılamayan firmalar ve veri kontrol listesi.
- **Hepsiburada Fatura Genel Raporu** içerikten tanınır ve ayrı işlenir.
- 7 bölüm: Genel Bakış · Fatura İşle · Mükellefler · Kodlanmış Dosyalar ·
  Fatura Ara · İşlem Geçmişi · Ayarlar.
- Yeni bilgisayarda klasörler **kendiliğinden oluşur** — kopyalanacak bir şey
  yok. Otomatik yedek açık gelir.

### 🔴 Düzeltildi — bağımsız denetimde çıkan 26 bulgu

Modül bitince altı bağımsız denetçi onu **çürütmek** için taradı; 36 iddianın
26'sı kod çalıştırılarak doğrulandı ve düzeltildi. En önemlileri:

- **Fatura yanlış cariye yazılabiliyordu.** İsimle bulunan hesabın VKN'si
  faturanınkiyle çelişse bile kod yazılıyordu; artık kod boş bırakılıp raporda
  açıklanıyor.
- **"X A.Ş." faturası "X Ltd.Şti." hesabına yazılabiliyordu.** Bunlar ayrı
  VKN'li ayrı carilerdir; artık ayrı tutuluyor.
- **Otomatik yedek hiç çalışmıyordu.** Ayar duruyordu ama yedek alınmıyordu.
- **Belge klasörünü değiştirdikten sonra "İşlemi Geri Al" yanlış dosyayı
  silebiliyordu.**
- **Mükellef silme yarıda kalırsa çift kayıt koruması silinmiş kalıyordu.**
- **Program uzun işlerde donuyordu**: arama, yeniden işleme ve geri alma artık
  arka planda koşuyor; işlem sürerken düğmeler kilitleniyor.
- **Sonuç kartı artık sessiz kalmıyor**: taslak faturalar, KDV tutarsızlığı,
  tanımsız seri/pazaryeri ve çok dosyalı partide toplam özet gösteriliyor.
- Arşiv kopyasının sessizce ezilmesi, bayat hesap planına geri dönülmesi ve
  Genel Bakış'ın aynı raporu iki kez sayması giderildi.

⚠️ **Çıktılarınız değişmedi:** 5 gerçek rapor üzerinde ölçüldü — kodlanmış
fatura satırlarında **0 fark**. Yeni denetimler gerçek hesap planınızda hiçbir
eşleşmeyi reddetmedi.

### Değişti — düzen

- **Ayar dosyaları tek klasörde.** Program klasöründeki `*.json` ayarları
  artık `ayarlar/` alt klasöründe duruyor. İlk açılışta kendiliğinden
  taşınırlar; **hiçbir ayarınız kaybolmaz** (aynı adlı dosya varsa eskisine
  dokunulmaz).
- **Belgeler bölündü.** Geliştirici belgesi 157 KB'tan 43 KB'a indi; modül
  ayrıntıları, sorun giderme ve geçmiş `belgeler/` klasörüne ayrıldı.

### Düzeltildi — ağır kullanıcı turu

- **Okunamayan dosya artık doğru teşhis alıyor.** Boş/bozuk bir dosya
  "Mükellef veya yön tespit edilemedi" diyordu; kullanıcı listeden mükellef
  seçip tekrar deniyor, aynı mesajı alıyordu.
- **Yön seçici eklendi.** Adında GELEN/GİDEN geçmeyen bir raporu (ör. yeniden
  adlandırdığınız bir dosya) işlemenin daha önce hiçbir yolu yoktu.

### 🔴 Düzeltildi — dosya yolu çok uzun (Excel açamıyordu)

Mükellefi **tam unvanla** girdiğinizde (ör. "… SANAYİ VE TİCARET LİMİTED
ŞİRKETİ") bu ad dosya yolunda iki kez geçiyor ve yol Windows'un 260 karakter
sınırını aşıyordu. Program dosyayı yazıyor ama **Excel açamıyordu**.

- Yeni mükellefte **klasör adı** sınırlanıyor — görünen ad tam kalıyor.
- Çıktı dosyasının adı yola sığacak şekilde kısalıyor ve size söyleniyor.
- **Mevcut** uzun dosyalarınız da artık "Excel'de Aç" ile açılıyor.

### Değişti — Fatura Kalem Listesi

- **Portalın satır sınırı canlı ölçüldü:** 500 kaleme kadar kayıpsız
  yüklüyor. 500 kalem sınırı olduğu gibi kalıyor.
- **150 kalemin üzerinde süre uyarısı:** portal 500 satırı çizerken ~3 dakika
  sürüyor ve tarayıcı o sürede donmuş gibi görünüyor. Artık önceden
  söyleniyor — sekmeyi kapatmayın.

### Notlar
- Eski program **silinmedi**; yeni modül gerçek bir ayı işleyip çıktılar
  karşılaştırılana kadar duruyor.
- Program artık **13 araç** barındırıyor. Birim test 636 → **710**.

---

**Daha eski sürümler:** [belgeler/gecmis/changelog-eski.md](belgeler/gecmis/changelog-eski.md)
