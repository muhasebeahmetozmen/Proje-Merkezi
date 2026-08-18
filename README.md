# Proje Merkezi

Türk muhasebeciler için **tek pencerede 7 araç** barındıran Windows masaüstü uygulaması.
Arayüz tamamen Türkçedir. Python veya başka bir kurulum gerektirmez.

## ⬇️ İndir

**[En son sürümü indir →](../../releases/latest)**

`ProjeMerkezi_Kurulum_vX.Y.exe` dosyasını indirip çalıştırın. Kurulum
**yönetici yetkisi istemez**; program kendi kullanıcı klasörünüze kurulur.

> Windows "bilinmeyen yayıncı" uyarısı verirse: **Ek bilgi → Yine de çalıştır**.
> (Uygulama imzalı değildir; kaynak kodu geliştiricide durur.)

---

## Araçlar

| Araç | Ne yapar |
|---|---|
| **Araç Satış Yazısı** | Araç satış faturası açıklama metnini üretir, panoya kopyalar |
| **Tevkifat Matrah Hesaplama** | Ödenecek tutardan geriye KDV matrahını bulur |
| **İki Oranlı KDV ve Matrah** | Genel toplam + toplam KDV'den iki farklı orandaki matrahları çözer |
| **Proforma Fatura** | Çok kalemli proforma hazırlar → PDF ve Excel |
| **EDM E-Fatura Alış Tevkifat Tarama** | EDM'de mükellefleri tarar, tevkifatlı gelen fatura adetlerini raporlar |
| **Otobüsçü Mükellef Fatura Kesme** | Toplu fatura taslağı oluşturur; onaylayınca resmî gönderir |

İlk dördü **internetsiz** çalışır. Son ikisi EDM portalını, manuel bir kullanıcıyı
taklit ederek Google Chrome üzerinden kullanır.

---

## Gereksinimler

- **Windows 10 / 11**
- EDM araçları için **Google Chrome**
- ⚠️ **Yönetici olarak çalıştırmayın** — Chrome yükseltilmiş oturumda açılmaz,
  EDM araçları çalışmaz.

---

## Güncelleme

Yeni sürüm çıktığında **[Sürümler](../../releases)** sayfasından yeni kurulum
dosyasını indirip çalıştırmanız yeterlidir; eskinin üzerine kurar.

**Ayarlarınız, mükellef listeleriniz ve EDM kimliğiniz kaybolmaz** — bunlar program
klasöründe değil, `%LOCALAPPDATA%\ProjeMerkezi` altında durur.

Nelerin değiştiğini [CHANGELOG.md](CHANGELOG.md) dosyasından görebilirsiniz.

---

## Verileriniz ve gizlilik

- **Hiçbir veri dışarı gönderilmez.** Telemetri, analitik veya uzak sunucu yoktur.
- Program yalnızca **sizin** EDM portalınıza, **sizin** başlattığınız işlem için bağlanır.
- EDM şifreniz Windows **DPAPI** ile şifrelenir; düz metin olarak saklanmaz.
- ⚠️ Şifre o bilgisayara + o kullanıcıya bağlıdır. Başka bilgisayarda kullanacaksanız
  kullanıcı adı/şifrenizi bir kez yeniden girmeniz gerekir. Bu bir hata değil,
  güvenlik özelliğidir.
- Tevkifat tarama **salt-okunurdur**: portaldaki KABUL / RED / İADE düğmelerine dokunmaz.
- **"Taslak Faturaları Onayla (Resmî Gönder)"** geri alınamaz bir işlemdir ve her zaman
  onay penceresi gösterir.

---

## Sorun bildirimi

[Issues](../../issues) sayfasını kullanın.

> ⚠️ **Gerçek mükellef adı, VKN/TCKN veya IBAN paylaşmayın.** Ekran görüntüsü
> gönderecekseniz bu alanları karartın.

---

## Lisans

[MIT](LICENSE). Yazılım "olduğu gibi" sunulur; üretilen fatura, beyanname ve
hesapların doğruluğundan **kullanıcı sorumludur**.
