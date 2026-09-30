# Sorgu Defteri

SQL, Python ve veri analizi pratiği için tarayıcıda çalışan, tek dosyalık bir web sitesi. DataLemur tarzı hikâyeli sorular, örnek tablolar ve otomatik sonuç kontrolü içerir.

**Canlı demo:** https://enessiranli.github.io/sorgu-defteri/

## Özellikler

- **31 SQL sorusu:** 11 Kolay, 12 Orta, 8 Zor. Her soruda hikâyeli açıklama, tablo şeması, örnek girdi, örnek çıktı ve açıklama bulunur.
- **Gerçek SQL kontrolü:** Sorgun tarayıcıda SQLite (sql.js) ile çalışır, sonucu beklenen çıktıyla karşılaştırılır. Doğruysa soru otomatik çözüldü olarak kaydedilir.
- **PostgreSQL / SQL Server seçici:** Çözümler her iki sisteme göre gösterilir. `TOP`/`LIMIT`, `DATE_TRUNC`/`DATEFROMPARTS`, recursive CTE gibi farklar ayrıca belirtilir.
- **Python (8), pandas (6) ve İstatistik (5) soruları:** Bunlar otomatik kontrol edilmez, çözümle karşılaştırıp elle işaretlenir.
- **İlerleme takibi:** Alan bazında renkli pasta grafik, günlük seri sayacı, zorluk ve durum filtreleri, arama, konu listesi.
- **Yedek:** İlerlemeyi JSON olarak indirme ve geri yükleme.

## Bilinen sınırlar

- Motor SQLite'tır, tam bir PostgreSQL veya SQL Server değildir. Yaygın sözdizimi çevrilir, ama `PERCENTILE_CONT` ve `generate_series` gibi yapılar çalışmaz. Bu sorularda "Elle işaretle" kullanılır.
- Kontrol yalnızca sayfadaki örnek verilerle yapılır, gizli test verisi yoktur.
- İlerleme tarayıcının `localStorage` alanında tutulur. Cihazlar arası senkron ve Google girişi yoktur; yedek butonunu kullan.

## Proje yapısı

```
sorgu-defteri/
├── index.html   # Tüm uygulama: HTML, CSS, JavaScript ve soru veritabanı
├── README.md
└── LICENSE
```

## Yerelde çalıştırma

`index.html` dosyasını tarayıcıda aç. Yazı tipleri ve SQL motoru CDN'den yüklendiği için internet bağlantısı gerekir.

## Yeni soru ekleme

Sorular `index.html` içindeki `SQLP` dizisindedir. Örnek:

```js
{id:"q32", lv:"Kolay", g:"WHERE", t:"Başlık", tb:["orders"],
 h:"İsteğe bağlı ipucu",
 s:"SELECT * FROM orders WHERE status = 'completed';"}
```

- `tb`: soruda gösterilecek tablolar (`D` nesnesinde tanımlı).
- `s`: PostgreSQL çözümü. SQL Server'da farklıysa `m` alanına ayrıca yaz.
- Sistemlere göre değişen küçük parçalar için `{{TOP 3}}`, `{{LIMIT 3}}`, `{{MONTH}}`, `{{REC}}` işaretleri kullanılır.
- Hikâye ve açıklama `STORY` nesnesine eklenir: `q32:["Hikâye...\n\nGörev...","Açıklama"]`.
- Beklenen çıktı çözüm sorgusu çalıştırılarak otomatik üretilir. SQLite'ta çalışmayan sorularda `x` alanına elle yazılır.

## Yol haritası

- SQL soru sayısını 100'e çıkarmak
- Python ve pandas soruları için tarayıcıda Python motoru (Pyodide)
- Gizli test verisiyle daha sağlam kontrol
- Firebase ile hesaba bağlı ilerleme

## Kullanılan teknolojiler

- [sql.js](https://github.com/sql-js/sql.js) (tarayıcıda SQLite)
- Google Fonts (Plus Jakarta Sans, JetBrains Mono)

## Lisans

MIT. Ayrıntılar için `LICENSE` dosyasına bak.
