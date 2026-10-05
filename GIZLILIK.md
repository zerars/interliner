# Gizlilik

Interliner bilgisayarınızda çalışan bir masaüstü programıdır. Bir sunucusu yoktur,
hesap açtırmaz ve geliştiriciye hiçbir veri göndermez.

## Ne nereye gider

| Veri | Nereye gider | Ne zaman |
|---|---|---|
| Seçtiğiniz metin | Yalnızca **sizin seçtiğiniz** çeviri/açıklama sağlayıcısına | Çeviri, açıklama, soru sorma sırasında |
| Taranmış sayfanın görüntüsü | Önce hiçbir yere (Windows OCR bilgisayarınızda çalışır); Windows okuyamazsa seçtiğiniz sağlayıcıya | Yalnızca "Görüntüden oku" teklifini kabul ettiğinizde |
| API anahtarlarınız | Hiçbir yere. Yalnızca ilgili sağlayıcıya kimlik doğrulama başlığında gider | İstek atarken |
| Bağlantı ön hazırlığı | Yalnızca seçtiğiniz çeviri hizmetinin sunucusuna; **hiçbir veri içermeyen** bir bağlantı açılır (çeviri daha hızlı gelsin diye) | İzinli bir PDF okuyucusunda fareye bastığınızda, en fazla 20 saniyede bir |
| Model listesi isteği | Anahtarını girdiğiniz sağlayıcıya (Anthropic, OpenAI, Google) — **metin içermez**, yalnızca o sağlayıcının anahtarı | Haftada en fazla bir kez, program ya da Ayarlar açılırken; ayrıca "Listeyi yenile"ye bastığınızda |
| Güncelleme denetimi | github.com'a (GitHub, Microsoft'a ait). Yalnızca yayımlanmış sürüm listesi istenir; **sizinle ilgili hiçbir bilgi gönderilmez**. Her internet isteğinde olduğu gibi IP adresiniz ve isteği yapan programın adı ve sürümü GitHub'a görünür | Günde en çok bir kez. Ayarlar → Gelişmiş'ten kapatılabilir. Microsoft Store sürümünde yoktur (Store günceller) |
| Geri bildirim | Program göndermez: **kendi e-posta programınız** hazır bir iletiyle açılır, göndermek sizin elinizdedir | "Geri bildirim gönder" dediğinizde |
| Defter notlarınız, ayarlarınız | Hiçbir yere. Bilgisayarınızda kalır | — |
| Kullanım istatistiği, telemetri | **Toplanmaz** | — |
| Anonim hata kaydı | Bilgisayarınızda tutulur; **yalnızca siz onaylarsanız** geliştiriciye gider | Ayda bir sorulur |

Sağlayıcı seçimi sizindir: Claude (Anthropic), ChatGPT (OpenAI), Gemini (Google),
Perplexity, DeepL, Google Çeviri, MyMemory. Gönderdiğiniz metnin o şirkette nasıl
işlendiği o şirketin koşullarına tabidir. Seçtiğiniz motor dışına metin gönderen
"ücretsiz motorlara düş" seçeneği **varsayılan olarak kapalıdır**.

## Bilgisayarınızda ne, nerede durur

| Dosya | İçerik |
|---|---|
| `%APPDATA%\PdfTranslator\config.json` | Ayarlar ve API anahtarları |
| `%APPDATA%\PdfTranslator\models.json` | Sağlayıcıların son bildirdiği model adları (anahtar içermez) |
| `%APPDATA%\PdfTranslator\errors.json` | Anonim hata kayıtları (gönderilince silinir) |
| `%APPDATA%\PdfTranslator\notebooks\` | Defterleriniz |
| `%APPDATA%\PdfTranslator\log.txt` | Yalnızca tanılama kaydını **siz açarsanız** oluşur |

**API anahtarları Windows DPAPI ile şifrelenir.** Şifreleme Windows hesabınıza ve bu
bilgisayara bağlıdır: `config.json` dosyası kopyalanıp başka bir bilgisayara taşınsa
bile anahtarlar okunamaz.

**Tanılama kaydı** varsayılan olarak kapalıdır. Açarsanız, hangi metni seçtiğiniz gibi
ayrıntılar bu dosyaya yazılır (API anahtarları yazılmaz). Dosya bilgisayarınızdan
çıkmaz; bize bir sorun bildirirken göndermeye karar verirseniz önce içeriğine bakın.

## Hata bildirimi

Program bir hatayla karşılaştığında, hatanın **şeklini** bilgisayarınızda not eder: nerede
olduğu (örneğin "ocr", "ceviri"), hatanın türü, temizlenmiş hata mesajı ve yığının ilk
birkaç satırı. Bu not hiçbir yere gönderilmez.

Ayda bir kez, kayıtlı hata varsa, program size bir pencere açar ve **gönderilecek metnin
tamamını** gösterir. Göndermek, panoya kopyalamak, sonra karar vermek ya da bir daha hiç
sorulmamasını istemek sizin elinizdedir. Hiçbir şey arka planda gönderilmez.

Gönderilen metinde **bulunmayanlar:** çevirdiğiniz metinler, okuduğunuz belgelerin adları,
dosya yolları, API anahtarlarınız, Windows kullanıcı adınız ve bilgisayarınızın adı.
Bunlar kayıt anında temizlenir: yollar `<yol>`, uzun anahtar benzeri diziler `<gizlendi>`
olarak yazılır.

Gönderilen metinde **bulunanlar:** program sürümü, Windows sürümü, arayüz dili, seçili
çeviri motorunun adı (anahtar değil), hata kayıtları ve rastgele üretilmiş bir kurulum
kimliği. Bu kimlik yalnızca aynı bilgisayardan gelen tekrarlı raporların ayrı ayrı
sayılmasını önler; sizinle ya da donanımınızla ilişkilendirilemez.

Kapatmak için: tepsi simgesi → **Tanılama** → "Hata bildirimini göster…" penceresinde
**Bir daha sorma**. Ayar dosyasındaki karşılığı `errorReportMode: "off"`.

## Güncellemeler

Program günde en çok bir kez github.com'daki sürüm listesine bakar. Yeni bir sürüm varsa
size sorar; **siz onaylamadan hiçbir şey indirilmez ya da kurulmaz.** İndirilen dosya,
geliştiricinin imzasıyla ve SHA-256 özetiyle doğrulanmadan kurulmaz. Ayarlarınız, API
anahtarlarınız ve defterleriniz güncellemeden etkilenmez. Kapatmak için: Ayarlar → Gelişmiş
→ "Güncellemeleri denetle".

## Geri bildirim

Tepsi menüsündeki **Geri bildirim gönder…** penceresinde yazdıklarınız, e-posta programınızda
hazır bir ileti olarak açılır; program kendisi hiçbir şey göndermez. "Sürüm ve Windows
bilgisini ekle" işaretliyse iletiye yalnızca program sürümü, Windows sürümü ve arayüz dili
eklenir; işareti kaldırabilirsiniz.

## Pano

Fareyle seçtiğinizde program, okuyucuya bir kopyalama komutu gönderip panoyu okur.
"Panoyu eski haline getir" ayarı açıkken (varsayılan) panonuzdaki metin geri konur.
Panodaki içerik hiçbir yere gönderilmez; yalnızca seçtiğiniz metin gönderilir.

## Bağış

Program ücretsizdir ve lisans doğrulaması yapmaz. "Destek ol" düğmesi yalnızca Polar
sayfasını tarayıcınızda açar; program Polar'a hiçbir şey göndermez. Bağış yaparsanız
ödeme bilgileriniz Polar ve ödeme sağlayıcısında işlenir; geliştirici yalnızca Polar
panelinde görünen adı, e-postayı ve isteğe bağlı mesajınızı görür.

## Çocuklar ve hassas veriler

Program hangi metni çevirdiğinizi denetlemez. Sağlık, hukuk, kimlik gibi hassas
bilgileri bir yapay zekâ sağlayıcısına göndermeden önce o sağlayıcının koşullarını
değerlendirin.

## Sorular

urazerarslan@gmail.com
