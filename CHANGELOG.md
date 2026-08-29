# Değişiklik Günlüğü

Bu dosya **kullanıcıya görünen** değişiklikleri listeler. Teknik ayrıntılar ve
karar gerekçeleri için [CLAUDE.md](CLAUDE.md) §12'ye bakın.

Sürüm numarası tek bir yerden gelir: `kpm/__init__.py` → `__version__`.

---


## v5.2 — Kuveyt Türk ek hesapları ve üç küçük düzeltme

Hepsi gerçek dosyalarla bulundu. **Yeni araç yok; ayarlarınız ve kayıtlı
listeleriniz olduğu gibi kalıyor.**

### 🔴 Düzeltildi — Kuveyt Türk'ün ek hesapları hâlâ birbirine karışıyordu

v5.1 hesabı `2710-1` gibi doğru adlandırıyordu ama **ek numarası yalnızca 1–2
haneyse**. Gerçek bir ekstrede ek numarası `4000` çıktı; kural tutmayınca
program sessizce eski yola (IBAN'ın son 4 hanesi) düştü. IBAN'ın son 4 hanesi
de tesadüfen `4000` olduğu için sonuç **`kuveyt türk 4000`** oldu: doğru gibi
görünen ama hesap numarasını kaybetmiş bir ad.

Ek numarası artık **4 haneye kadar** okunuyor. Aynı müşterinin üç hesabı,
gerçek dosyalarla ölçüldü:

| Ekstre başlığı | v5.1 | **v5.2** |
|---|---|---|
| `Hesap Bilgisi:  91593111 - 1` | `kuveyt türk 0001` | **`kuveyt türk 3111-1`** |
| `Hesap Bilgisi:  91593111 - 2` | `kuveyt türk 0002` | **`kuveyt türk 3111-2`** |
| `Hesap Bilgisi:  91593111 - 4000` | `kuveyt türk 4000` | **`kuveyt türk 3111-4000`** |

### 🔴 Düzeltildi — "Listeyi Temizle" temizlemiyordu

Banka Ekstresi Adlandırma'da düğme listeyi siliyor gibi görünüyor, ama başka
bir modüle geçip döndüğünüzde — ya da programı kapatıp açtığınızda — **eski
liste geri geliyordu**. Sebebi: düğme yalnız ekrandaki tabloyu boşaltıyor,
diskteki kayda dokunmuyordu.

Artık gerçekten temizleniyor. ⚠️ **Geri alma etkilenmez**: listeyi temizlemek
"yaptıklarını geri alamayasın" demek değildir, **Geri Al** düğmesi çalışmaya
devam eder.

### Düzeltildi — TC/VKN Sorgulama örneği

Alandaki sönük örnek `Örn. 1234567890 (VKN) veya 11 haneli TCKN` yazıyordu.
Uydurma bir numara gösteriyordu; asıl söylenmek istenen hane sayısıydı. Artık:
**`Örn. 10 haneli VKN veya 11 haneli TCKN`**

### Düzeltildi — Araç Satış Yazısı, Noter örneği

Örnek `NİĞDE 1. NOTERLİĞİ` yazıyordu; program cümleyi zaten
*"… NOTERLİĞİNİN …"* diye kuruyor, yani örneği olduğu gibi yazan
*"NİĞDE 1. NOTERLİĞİ NOTERLİĞİNİN"* elde ediyordu. Örnek artık **`NİĞDE 1.`**

### Notlar
- Birim test **924 → 930**; dört düzeltmenin her biri testle kilitlendi.
- Yeni bağımlılık yok, kurulum boyutu değişmedi.


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


**Daha eski sürümler:** [belgeler/gecmis/changelog-eski.md](belgeler/gecmis/changelog-eski.md)
