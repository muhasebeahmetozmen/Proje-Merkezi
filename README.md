<div align="center">

# Proje Merkezi

**Türk muhasebeciler için tek pencerede 13 araç.**
GİB kesinti (stopaj) tarama · e-fatura tevkifat taraması · KDV ve matrah
hesaplama · banka ekstresi adlandırma · proforma fatura · toplu fatura kesme.
Hepsi Türkçe, kurulumu tek tık, yönetici yetkisi istemez.

[![Sürüm](https://img.shields.io/badge/s%C3%BCr%C3%BCm-5.0-2ea44f?style=for-the-badge)](../../releases/latest)
[![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-0078d4?style=for-the-badge&logo=windows&logoColor=white)](../../releases/latest)
[![Lisans](https://img.shields.io/badge/lisans-MIT-8b5cf6?style=for-the-badge)](LICENSE)

### [⬇️  Programı İndir](../../releases/latest)

<sub>Python veya başka bir kurulum gerekmez · Yönetici yetkisi istemez</sub>

<br>


</div>

<br>

---

## Ne işe yarar?

Muhasebe bürosunda her ay tekrar eden, elle yapılması hem uzun hem hataya açık
işleri tek bir programda topladık:

| Araç | Ne yapar | İnternet |
|:--|:--|:--:|
| 🚗 **Araç Satış Yazısı** | Araç satış faturasının açıklama metnini şablondan üretir, panoya kopyalar | — |
| 🧮 **Tevkifat Matrah Hesaplama** | Ödenecek tutardan geriye doğru matrahı ve tevkifatı çözer | — |
| ➗ **İki Oranlı Matrah ve KDV** | Genel toplam + toplam KDV'den iki farklı orandaki matrahları ayırır | — |
| 🛡️ **Poliçe Hesaplama** | Sigorta poliçesini kapsadığı güne göre dönemlere böler, 180/280 hesaplarıyla kuruşu kuruşuna denk muhasebe fişi üretir; döviz poliçelerinde TCMB kuru | Yalnız kur düğmesi |
| 📄 **Proforma Fatura** | Çok kalemli proforma hazırlar, PDF ve Excel olarak kaydeder | — |
| 🔎 **TC / VKN Sorgulama** | VKN veya TCKN'den mükellefin ünvan, ad-soyad ve vergi dairesini getirir; toplu sorgu ve Excel çıktısı | ✔️ |
| 🧾 **GİB Kesinti Tarayıcı** | Mükelleflerinizin **adına yapılan kesintileri (stopaj)** Dijital Vergi Dairesi'nden toplu çeker, biriktirir ve mahsupta kullanacağınız Excel/HTML dökümünü üretir; giriş ekranındaki güvenlik kodunu kendisi okur, GİB'in istek kotasını öğrenip taramayı gecelere yayar | ✔️ |
| 📦 **E-Fatura PDF Ayıklayıcı** | Portaldan inen fatura zip'ini **kendiliğinden** PDF'e çevirir, panoya koyar, zip'i geri dönüşüme atar | — |
| 🏦 **Banka Ekstresi Adlandırma** | Ekstre dosyasının içini okur, IBAN'ından bankayı ve hesabı bulur, `garanti 2265.pdf` gibi adlandırır; sürükle-bırak, Explorer'dan tek hamlede gönderme ve geri alma | — |
| 🔍 **E-Fatura Alış Tevkifat Tarama** | EDM'de mükellef listesini dolaşır, dönemdeki tevkifatlı gelen fatura adetlerini raporlar | ✔️ |
| 📋 **Fatura Kalem Listesi** | Çok kalemli faturayı hızlı girer, EDM portalına yüklenecek kalem Excel'ini masaüstüne üretir; canlı toplam ve portal kurallarına göre denetim | — |
| 🛒 **İnternet Satıcıları Fatura Otomasyonu** | Pazaryeri satıcılarının fatura raporlarını okur, her satıra hesap planından kodunu yazar, mükerrer faturaları ayıklar ve muhasebeye aktarılacak Excel'i üretir | — |
| 🚌 **Otobüsçü Mükellef Fatura Kesme** | Toplu fatura taslağı oluşturur, onayınca resmî gönderir | ✔️ |

İlk dördü, Poliçe Hesaplama (TL), Fatura Kalem Listesi, İnternet Satıcıları Fatura
Otomasyonu ve Banka Ekstresi Adlandırma **tamamen çevrimdışı** çalışır; hesapları ve
dosya işlemleri birim testlerle güvence altındadır. TC/VKN Sorgulama, **sizin kendi GİB
e-Arşiv girişinizle** portala bağlanır; GİB Kesinti Tarayıcı ise **her mükellefin kendi GİB girişiyle** Dijital Vergi Dairesi'ne bağlanır. PDF Ayıklayıcı yalnızca kendi diskinizdeki klasöre bakar (e-Arşiv faturasını çevirirken **interneti tamamen
kapatılmış** görünmez bir tarayıcı açar). Son ikisi EDM portalını, tıpkı sizin gibi Google
Chrome üzerinden kullanır.

---

## Kurulum

1. **[Sürümler sayfasından](../../releases/latest)** `ProjeMerkezi_Kurulum_vX.Y.exe` dosyasını indirin
2. Çalıştırın — yönetici yetkisi istemez, kendi kullanıcı klasörünüze kurulur
3. Masaüstündeki kısayoldan açın

> **Windows "bilinmeyen yayıncı" uyarısı verirse:** *Ek bilgi → Yine de çalıştır.*
> Program dijital sertifikayla imzalı değildir (sertifika ücretli bir kurumsal hizmettir).

**Gerekenler:** Windows 10/11 · EDM araçlarını kullanacaksanız Google Chrome

> ⚠️ Programı **yönetici olarak çalıştırmayın.** Chrome yükseltilmiş oturumda açılmadığı
> için EDM araçları çalışmaz.

---

## Güncelleme

Program **açılışta arka planda** yeni sürüm var mı diye bakar; varsa ne değiştiğini
gösteren bir pencere açar. İsterseniz **"Daha Sonra"** deyip kapatabilirsiniz.
İstediğiniz an sol alttaki **"Güncellemeleri Denetle"** düğmesine de basabilirsiniz —
o zaman sonucu her hâlükârda bildirir ("güncelsiniz" ya da yeni sürüm penceresi).

Güncelleme denetimi **hiçbir veri göndermez**: yalnız GitHub'a düz bir istek yapılır,
internet yoksa sessizce vazgeçilir.

**Ayarlarınız, mükellef listeleriniz ve EDM kimliğiniz güncellemede kaybolmaz.**

Nelerin değiştiğini [CHANGELOG.md](CHANGELOG.md) dosyasından görebilirsiniz.

---

## Gizlilik ve güvenlik

Bu program mükellef adı, VKN/TCKN ve IBAN gibi **gerçek mali veriyle** çalışır.
Tasarımı buna göre yapıldı:

- 🔒 **Telemetri, analitik veya kullanım istatistiği YOKTUR.** Hiçbir veri
  bize ya da üçüncü bir tarafa gönderilmez; bizim sunucumuz diye bir şey yok.
- 🔑 **Şifreleriniz Windows DPAPI ile şifrelenir**, düz metin olarak saklanmaz.
  Şifre o bilgisayara + o kullanıcıya bağlıdır; başka makineye kopyalanırsa
  çözülemez (güvenlik özelliği). Günlüğe şifre yazılmaz, sorgulanan numaralar
  bile `123****890` diye maskelenir.
- 🌐 **Program dışarıya yalnız DÖRT adrese çıkar, dördü de kilitlidir:**

  | Nereye | Hangi araç | Ne gönderiliyor |
  |:--|:--|:--|
  | `github.com` | Güncelleme denetimi | **hiçbir şey** — düz bir istek; indirilen dosya çalıştırılmadan doğrulanır |
  | `earsivportal.efatura.gov.tr` | TC/VKN Sorgulama · Kesinti Tarayıcı (ünvan) | **sizin** GİB e-Arşiv kullanıcı kodunuz ve şifreniz |
  | `dijital.gib.gov.tr` | **GİB Kesinti Tarayıcı** | **her mükellefin kendi** GİB kullanıcı kodu ve şifresi |
  | `www.tcmb.gov.tr` | Poliçe Hesaplama (döviz) | **hiçbir şey** — yalnız kur tarihini içeren düz bir istek |

  Şifre gönderilen iki adres, tarayıcıda o portala girdiğinizde olanın
  aynısını yapar: sorgu **sizin (ya da mükellefin) kendi girişiyle** çalışır.
  Şifreler yalnız GİB'e gider, diske **DPAPI ile şifreli** yazılır ve hiçbir
  günlüğe düşmez.

  Dört adres de kaynak kodda **sabittir**; program her istekte adresi ve
  HTTPS şartını denetler, bozuk bir ayar dosyası bile başka bir sunucuya
  bağlanamaz. Bu kural testlerle kilitlidir.

  > EDM araçları (E-Fatura Alış Tevkifat Tarama · Otobüsçü Fatura Kesme)
  > bu listede yok, çünkü onlar kendi başlarına bağlanmaz: **Google
  > Chrome'u açıp sizin gibi kullanırlar.**
- 📦 **PDF Ayıklayıcı yalnız iki şart birden tutan zip'e dokunur** (adı portal
  biçiminde OLACAK ve içeriği beklenen türde OLACAK). Diğer dosyalarınıza parmağını
  bile sürmez; işlediği zip'i **geri dönüşüm kutusuna** gönderir, kalıcı silmez.
- 👀 **Tevkifat tarama salt-okunurdur:** portaldaki KABUL / RED / İADE
  düğmelerine asla dokunmaz.
- ⚠️ **GİB tek oturuma izin verir:** tarayıcıda e-Arşiv Portalı açıkken TC/VKN
  sorgusu yaparsanız oradaki oturumunuz düşebilir. Program her sorgudan sonra
  kendi oturumunu kapatır.
- ⚠️ **"Taslak Faturaları Onayla (Resmî Gönder)"** geri alınamaz bir işlemdir ve
  her zaman onay penceresi gösterir.

**Verileriniz nerede?** `%LOCALAPPDATA%\ProjeMerkezi` klasöründe — program
klasöründe değil. Bu sayede güncelleme veya kaldırma verilerinizi silmez.

---

## Sorun bildirimi

[Issues](../../issues) sayfasından bildirebilirsiniz. Şunları yazmak çok yardımcı olur:
hangi araçta, hangi adımda, ekranda ne yazdığı.

> ⚠️ **Gerçek mükellef adı, VKN/TCKN veya IBAN paylaşmayın.**
> Ekran görüntüsü gönderecekseniz bu alanları karartın.

---

<div align="center">
<sub>

**Lisans:** [MIT](LICENSE) · Serbestçe kullanabilir, değiştirebilir ve dağıtabilirsiniz.

Yazılım "olduğu gibi" sunulur; üretilen fatura, beyanname ve hesapların
doğruluğundan **kullanıcı sorumludur**.

</sub>
</div>
