<div align="center">

# Proje Merkezi

**Türk muhasebeciler için tek pencerede 7 araç.**
Tevkifat taraması, KDV/matrah hesaplama, proforma fatura ve toplu fatura kesme —
hepsi Türkçe, kurulumu tek tık.

[![Sürüm](https://img.shields.io/badge/s%C3%BCr%C3%BCm-4.2-2ea44f?style=for-the-badge)](../../releases/latest)
[![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-0078d4?style=for-the-badge&logo=windows&logoColor=white)](../../releases/latest)
[![Lisans](https://img.shields.io/badge/lisans-MIT-8b5cf6?style=for-the-badge)](LICENSE)

### [⬇️  Programı İndir](../../releases/latest)

<sub>Python veya başka bir kurulum gerekmez · Yönetici yetkisi istemez · ~40 MB</sub>

<br>

<img src="docs/gorsel/01-anasayfa.png" alt="Proje Merkezi ana ekranı" width="100%">

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
| ➗ **İki Oranlı KDV ve Matrah** | Genel toplam + toplam KDV'den iki farklı orandaki matrahları ayırır | — |
| 📄 **Proforma Fatura** | Çok kalemli proforma hazırlar, PDF ve Excel olarak kaydeder | — |
| 🔍 **E-Fatura Alış Tevkifat Tarama** | EDM'de mükellef listesini dolaşır, dönemdeki tevkifatlı gelen fatura adetlerini raporlar | ✔️ |
| 🚌 **Otobüsçü Mükellef Fatura Kesme** | Toplu fatura taslağı oluşturur, onayınca resmî gönderir | ✔️ |

İlk dördü **tamamen çevrimdışı** çalışır ve hesapları birim testlerle güvence altındadır.
Son ikisi EDM portalını, tıpkı sizin gibi Google Chrome üzerinden kullanır.

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

## Ekranlar

<table>
<tr>
<td width="50%"><img src="docs/gorsel/03-tevkifat-matrah.png" alt="Tevkifat matrah hesaplama"><br>
<b>Tevkifat Matrah Hesaplama</b><br><sub>Ödenecek tutardan geriye matrah, KDV ve tevkifat.</sub></td>
<td width="50%"><img src="docs/gorsel/04-iki-oranli-kdv.png" alt="İki oranlı KDV"><br>
<b>İki Oranlı KDV ve Matrah</b><br><sub>Kuruşu kuruşuna ayrıştırma, sonuç doğrulaması.</sub></td>
</tr>
<tr>
<td width="50%"><img src="docs/gorsel/05-proforma.png" alt="Proforma fatura"><br>
<b>Proforma Fatura</b><br><sub>Çok kalemli, tevkifatlı; PDF ve Excel çıktısı.</sub></td>
<td width="50%"><img src="docs/gorsel/06-efatura-tevkifat-tarama.png" alt="E-fatura tevkifat tarama"><br>
<b>E-Fatura Alış Tevkifat Tarama</b><br><sub>Mükellef listesini dolaşır, adetleri raporlar.</sub></td>
</tr>
<tr>
<td colspan="2"><img src="docs/gorsel/02-arac-satis.png" alt="Araç satış yazısı"><br>
<b>Araç Satış Yazısı</b><br><sub>Takvim, hızlı kopyalama havuzu ve canlı metin önizlemesi.</sub></td>
</tr>
</table>

---

## Güncelleme

Programın içinde **"Güncellemeleri Denetle"** düğmesi vardır — basınca yeni sürüm
var mı diye bakar, varsa sorar ve onaylarsanız kendisi indirip kurar.

İsterseniz **"Açılışta otomatik denetle"** kutusunu işaretleyerek her açılışta
sessizce kontrol etmesini sağlayabilirsiniz. **Varsayılan olarak kapalıdır** —
yani siz istemedikçe program internete kendiliğinden çıkmaz.

**Ayarlarınız, mükellef listeleriniz ve EDM kimliğiniz güncellemede kaybolmaz.**

Nelerin değiştiğini [CHANGELOG.md](CHANGELOG.md) dosyasından görebilirsiniz.

---

## Gizlilik ve güvenlik

Bu program mükellef adı, VKN/TCKN ve IBAN gibi **gerçek mali veriyle** çalışır.
Tasarımı buna göre yapıldı:

- 🔒 **Verileriniz bilgisayarınızdan çıkmaz.** Telemetri, analitik, kullanım
  istatistiği veya uzak sunucu **yoktur**.
- 🔑 **EDM şifreniz Windows DPAPI ile şifrelenir**, düz metin olarak saklanmaz.
  Şifre o bilgisayara + o kullanıcıya bağlıdır; başka makineye kopyalanırsa
  çözülemez (güvenlik özelliği).
- 🌐 **Programın dışarıya çıktığı tek yer güncelleme denetimidir** — yalnız
  `github.com` adresine, yalnız HTTPS ile, **hiçbir veri göndermeden**.
  İndirilen dosya çalıştırılmadan önce doğrulanır.
- 👀 **Tevkifat tarama salt-okunurdur:** portaldaki KABUL / RED / İADE
  düğmelerine asla dokunmaz.
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
