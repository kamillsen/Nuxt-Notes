# 🚗 Filo API Dokümantasyonu

## 📋 Genel Bilgiler

| Özellik | Değer |
|---------|--------|
| **Base URL** | `http://localhost:3001` |
| **Port** | 3001 |
| **Teknoloji** | json-server v1.0.0-beta.3 |
| **Veri Formatı** | JSON |
| **Desteklenen Metodlar** | GET, POST, PUT, PATCH, DELETE |

## 🔗 API Endpoint'leri Özet Tablosu

| Endpoint | Yol | Açıklama | Kayıt Sayısı |
|----------|-----|----------|--------------|
| **vehicle-header** | `/vehicle-header/:id` | Araç üst bilgi kartı | 10 |
| **vehicle-identity** | `/vehicle-identity/:id` | Araç kimlik bilgileri | 10 |
| **vehicle-status** | `/vehicle-status/:id` | Durum ve operasyon | 10 |
| **vehicle-inspection** | `/vehicle-inspection/:id` | Muayene ve sigorta | 10 |
| **vehicle-maintenance** | `/vehicle-maintenance/:id` | Bakım ve arıza | 10 |
| **vehicle-technical** | `/vehicle-technical/:id` | Teknik özellikler | 10 |
| **vehicle-superstructure** | `/vehicle-superstructure/:id` | Üst yapı bilgileri | 10 |
| **vehicle-registration** | `/vehicle-registration/:id` | Resmi kayıt bilgileri | 10 |

---

## 1️⃣ vehicle-header

### Endpoint Detayları

| Özellik | Değer |
|---------|--------|
| **URL** | `/vehicle-header/:id` |
| **Metodlar** | GET, PUT, PATCH |
| **ID Aralığı** | 1-10 |
| **Açıklama** | Araç üst bilgi kartı için özet bilgiler |

### Veri Alanları

| Alan | Tip | Açıklama | Örnek Değer |
|------|-----|----------|-------------|
| `id` | string | Araç ID | "1" |
| `plaka` | string | Araç plakası | "34 ABC 123" |
| `durum` | string | Araç durumu | "aktif", "bakimda", "ariza" |
| `durumRenk` | string | Durum renk kodu | "success", "warning", "danger" |
| `marka` | string | Araç markası | "Toyota" |
| `model` | string | Araç modeli | "Corolla" |
| `yil` | number | Model yılı | 2021 |
| `ticariAdi` | string | Ticari model adı | "Corolla 1.6 Advance" |
| `renk` | string | Araç rengi | "Beyaz" |

---

## 2️⃣ vehicle-identity

### Endpoint Detayları

| Özellik | Değer |
|---------|--------|
| **URL** | `/vehicle-identity/:id` |
| **Metodlar** | GET, PUT, PATCH |
| **ID Aralığı** | 1-10 |
| **Açıklama** | Araç kimlik ve organizasyon bilgileri |

### Veri Alanları

| Alan | Tip | Açıklama | Örnek Değer |
|------|-----|----------|-------------|
| `id` | string | Araç ID | "1" |
| `plaka` | string | Araç plakası | "34 ABC 123" |
| `marka` | string | Araç markası | "Toyota" |
| `model` | string | Araç modeli | "Corolla" |
| `modelYili` | number | Model yılı | 2021 |
| `ticariAdi` | string | Ticari model adı | "Corolla 1.6 Advance" |
| `organizasyon` | string | Bağlı organizasyon | "İstanbul Bölge Müdürlüğü" |
| `bolge` | string | Bölge adı | "Marmara" |
| `aktifLokasyon` | string | Mevcut konum | "Kadıköy Garajı" |
| `departman` | string | Departman | "Satış Ekibi" |
| `aracTipi` | string | Araç tipi | "Binek", "SUV", "Premium Binek" |

---

## 3️⃣ vehicle-status

### Endpoint Detayları

| Özellik | Değer |
|---------|--------|
| **URL** | `/vehicle-status/:id` |
| **Metodlar** | GET, PUT, PATCH |
| **ID Aralığı** | 1-10 |
| **Açıklama** | Araç durum, kilometre ve operasyon bilgileri |

### Veri Alanları

| Alan | Tip | Açıklama | Örnek Değer |
|------|-----|----------|-------------|
| `id` | string | Araç ID | "1" |
| `durumRozeti` | object | Durum bilgisi | `{durum, renk, ikon}` |
| `durumRozeti.durum` | string | Durum | "aktif", "bakimda", "ariza" |
| `durumRozeti.renk` | string | Renk kodu | "success", "warning", "danger" |
| `durumRozeti.ikon` | string | İkon adı | "check-circle", "wrench" |
| `kilometre` | object | Kilometre bilgisi | `{guncel, maksimum, yuzde}` |
| `kilometre.guncel` | number | Güncel km | 45320 |
| `kilometre.maksimum` | number | Max km | 200000 |
| `kilometre.yuzde` | number | Kullanım % | 22.66 |
| `yakitTuketimi` | object | Yakıt tüketimi | `{aylik, litre, sonAylar, ortalamaKm}` |
| `yakitTuketimi.aylik` | number | Aylık tüketim | 185 |
| `yakitTuketimi.litre` | string | Birim | "litre", "kWh" |
| `yakitTuketimi.sonAylar` | array | Son aylar | [145, 165, 178, 190, 185] |
| `yakitTuketimi.ortalamaKm` | string | Ortalama tüketim | "6.8 L/100km" |
| `atanmisSurucu` | object | Sürücü bilgisi | `{ad, avatar, telefon}` |
| `sonHareketNedeni` | string | Son hareket nedeni | "Müşteri Ziyareti" |
| `sonKonum` | object | Konum bilgisi | `{sehir, adres, guncellemeSaati, koordinat}` |

---

## 4️⃣ vehicle-inspection

### Endpoint Detayları

| Özellik | Değer |
|---------|--------|
| **URL** | `/vehicle-inspection/:id` |
| **Metodlar** | GET, PUT, PATCH |
| **ID Aralığı** | 1-10 |
| **Açıklama** | Muayene, sigorta ve belge bilgileri |

### Veri Alanları

| Alan | Tip | Açıklama | Örnek Değer |
|------|-----|----------|-------------|
| `id` | string | Araç ID | "1" |
| `muayene` | object | Muayene bilgisi | `{tarih, kalanGun, yuzde, durum}` |
| `muayene.tarih` | string | Muayene tarihi | "14.10.2025" |
| `muayene.kalanGun` | number | Kalan gün | 359 |
| `muayene.yuzde` | number | Kalan süre % | 98 |
| `muayene.durum` | string | Durum | "success", "warning", "danger" |
| `sigorta` | object | Sigorta bilgisi | `{policeNo, bitisTarihi, yenilemeDurumu, sirket, durum}` |
| `kasko` | object | Kasko bilgisi | `{policeNo, bitisTarihi, sirket, durum}` |
| `belgeler` | object | Belgeler durumu | `{ruhsat, egzozEmisyon, kBelgesi, hgsOgs, trafik, kasko}` |
| `belgeler.ruhsat` | boolean | Ruhsat durumu | true/false |
| `belgeler.egzozEmisyon` | boolean | Egzoz emisyon | true/false |
| `belgeler.kBelgesi` | boolean | K belgesi | true/false |
| `hgsOgs` | object | HGS/OGS bilgisi | `{hgsNo, bakiye, sonYukleme}` |

---

## 5️⃣ vehicle-maintenance

### Endpoint Detayları

| Özellik | Değer |
|---------|--------|
| **URL** | `/vehicle-maintenance/:id` |
| **Metodlar** | GET, PUT, PATCH |
| **ID Aralığı** | 1-10 |
| **Açıklama** | Bakım, arıza ve servis geçmişi |

### Veri Alanları

| Alan | Tip | Açıklama | Örnek Değer |
|------|-----|----------|-------------|
| `id` | string | Araç ID | "1" |
| `sonAriza` | object | Son arıza | `{tarih, aciklama, maliyet, durum}` |
| `sonAriza.tarih` | string | Arıza tarihi | "15.07.2024" |
| `sonAriza.aciklama` | string | Açıklama | "Klima soğutma problemi" |
| `sonAriza.maliyet` | number | Maliyet | 1250.00 |
| `sonAriza.durum` | string | Durum | "Çözüldü", "Bakımda", "Arızalı" |
| `bakimGecmisi` | array | Bakım listesi | Array of objects |
| `bakimGecmisi[].tarih` | string | Bakım tarihi | "10.09.2024" |
| `bakimGecmisi[].tip` | string | Bakım tipi | "Periyodik Bakım" |
| `bakimGecmisi[].aciklama` | string | Açıklama | "20.000 km bakımı" |
| `bakimGecmisi[].maliyet` | number | Maliyet | 2500.00 |
| `bakimGecmisi[].servis` | string | Servis | "Toyota Yetkili Servis" |
| `yaklasanBakim` | object | Yaklaşan bakım | `{tip, aciklama, tahminiTarih, kalanKm, tahminiMaliyet}` |
| `servisPeriyodu` | string | Servis periyodu | "Her 10.000 km" |
| `garantiDurumu` | string | Garanti durumu | "Devam Ediyor", "Sona Erdi" |
| `garantiBitis` | string | Garanti bitiş | "14.10.2026" |

---

## 6️⃣ vehicle-technical

### Endpoint Detayları

| Özellik | Değer |
|---------|--------|
| **URL** | `/vehicle-technical/:id` |
| **Metodlar** | GET, PUT, PATCH |
| **ID Aralığı** | 1-10 |
| **Açıklama** | Teknik özellikler ve motor bilgileri |

### Veri Alanları

| Alan | Tip | Açıklama | Örnek Değer |
|------|-----|----------|-------------|
| `id` | string | Araç ID | "1" |
| `aracSinifi` | string | Araç sınıfı | "Sedan", "Hatchback", "SUV" |
| `cinsi` | string | Araç cinsi | "Otomobil", "Arazi Aracı" |
| `tipi` | string | Araç tipi | "M1", "M1G" |
| `renk` | string | Renk | "Beyaz" |
| `motorGucu` | object | Motor gücü | `{kw, hp, birim}` |
| `motorGucu.kw` | number | Kilowatt | 90 |
| `motorGucu.hp` | number | Beygir gücü | 122 |
| `silindirHacmi` | number | Silindir hacmi (cc) | 1600 |
| `netAgirlik` | number | Net ağırlık (kg) | 1285 |
| `azamiYukluAgirlik` | number | Azami yüklü ağırlık | 1750 |
| `romorkKapasitesi` | object | Römork kapasitesi | `{frenli, frensiz}` |
| `koltukSayisi` | number | Koltuk sayısı | 5 |
| `ayaktaYolcuKapasitesi` | number | Ayakta yolcu | 0 |
| `yakitTipi` | string | Yakıt tipi | "Benzin", "Dizel", "Elektrik" |
| `motorTipi` | string | Motor tipi | "4 Silindir Sıralı" |
| `emisyonStandardi` | string | Emisyon standardı | "Euro 6" |
| `sanziman` | object | Şanzıman | `{tip, vitesSayisi}` |
| `cekisSistemi` | string | Çekiş sistemi | "Önden Çekiş" |
| `lastikBoyutu` | string | Lastik boyutu | "205/55 R16" |
| `yakitDepoHacmi` | number | Yakıt deposu (L) | 50 |
| `bataryaKapasitesi` | string | Batarya (elektrikli) | "60 kWh" |

---

## 7️⃣ vehicle-superstructure

### Endpoint Detayları

| Özellik | Değer |
|---------|--------|
| **URL** | `/vehicle-superstructure/:id` |
| **Metodlar** | GET, PUT, PATCH |
| **ID Aralığı** | 1-10 |
| **Açıklama** | Üst yapı ve özel donanım bilgileri |

### Veri Alanları

| Alan | Tip | Açıklama | Örnek Değer |
|------|-----|----------|-------------|
| `id` | string | Araç ID | "1" |
| `ustYapiTipi` | string | Üst yapı tipi | "Yok", "Frigorifik Kasa", "Tanker", "VIP Donanım" |
| `uretici` | string | Üretici | "Carrier Transicold" |
| `kapasite` | string | Kapasite | "8 m³", "5000 litre" |
| `mevcutDoluluk` | number | Mevcut doluluk | 5.2 |
| `dolulukYuzde` | number | Doluluk yüzdesi | 65 |
| `ekDonanim` | array | Ek donanımlar | ["Soğutma Ünitesi", "Sayaç"] |
| `ozellikler` | object | Özel özellikler | Değişken yapıda |

### Üst Yapı Tiplerine Göre Özellikler

| Üst Yapı Tipi | Özel Alanlar |
|---------------|--------------|
| **Frigorifik** | sicaklikAraligi, sogutmaGucu, yalitim, kapiBoyutu |
| **Tanker** | tankMalzemesi, bolmeSayisi, pompaKapasitesi, emniyet |
| **VIP Donanım** | koltukMalzemesi, iklimKontrol, barUnit, perdeSystem |
| **Kurtarma** | vincModeli, cekmeKapasitesi, halatUzunlugu, snorkel |

---

## 8️⃣ vehicle-registration

### Endpoint Detayları

| Özellik | Değer |
|---------|--------|
| **URL** | `/vehicle-registration/:id` |
| **Metodlar** | GET, PUT, PATCH |
| **ID Aralığı** | 1-10 |
| **Açıklama** | Resmi tescil ve sahiplik bilgileri |

### Veri Alanları

| Alan | Tip | Açıklama | Örnek Değer |
|------|-----|----------|-------------|
| `id` | string | Araç ID | "1" |
| `ilkTescilTarihi` | string | İlk tescil tarihi | "15.03.2020" |
| `sonTescilTarihi` | string | Son tescil tarihi | "14.10.2024" |
| `tescilSiraNo` | string | Tescil sıra no | "2024/123456" |
| `sasiNo` | string | Şasi numarası | "VN202509040001AAAAA" |
| `motorNo` | string | Motor numarası | "1ZR-FE-789012" |
| `sahipBilgisi` | object | Sahip bilgisi | `{adi, tcknVergiNo, adres}` |
| `finansalDurum` | object | Finansal durum | `{durum, finansKurumu, krediDurumu}` |
| `finansalDurum.durum` | string | Finansal durum | "Satın Alma", "Kredi", "Finansal Kiralama" |
| `oncekiSahipler` | array | Önceki sahipler | Array of objects |
| `noterBilgileri` | object | Noter bilgileri | `{noterAdi, satisNo, satisTarihi}` |
| `aracUzerindekiHakSahibi` | string | Rehin durumu | "Yok", "XYZ Bank A.Ş." |
| `tescilBelgesi` | object | Tescil belgesi | `{seriNo, onaylayanTescil, tipOnayNo}` |
| `kullanimAmaci` | string | Kullanım amacı | "Hususi", "Ticari" |

---

## 📊 Diğer Tablolar

### vehicles (Ana Araç Tablosu)

| Alan | Tip | Açıklama |
|------|-----|----------|
| `id` | string | Araç ID (1-40) |
| `plaka` | string | Plaka |
| `sase_no` | string | Şase numarası |
| `marka` | string | Marka |
| `model` | string | Model |
| `yil` | number | Yıl |
| `yakit_tipi` | string | Yakıt tipi |
| `motor_hacmi` | string | Motor hacmi |
| `arac_sinifi` | string | Araç sınıfı |
| `motor_gucu` | string | Motor gücü |
| `kayit_tarihi` | string | Kayıt tarihi |
| `muayene_tarihi` | string | Muayene tarihi |

### vehicleDetails (Detaylı Araç Bilgileri)

| Alan | Tip | Açıklama |
|------|-----|----------|
| `id` | string | Araç ID (1-10) |
| `licensePlate` | string | Plaka |
| `brand` | string | Marka |
| `commercialName` | string | Ticari adı |
| `modelYear` | number | Model yılı |
| `color` | string | Renk |
| `chassisNo` | string | Şasi no |
| `engineNo` | string | Motor no |
| `fuelType` | string | Yakıt tipi |
| `ownerInfo` | string | Sahip bilgisi |

### Yardımcı Tablolar

| Tablo Adı | Açıklama | Kayıt Sayısı |
|-----------|----------|--------------|
| `arac_siniflari` | Araç sınıfları listesi | 16 |
| `yakit_tipleri` | Yakıt tipleri listesi | 11 |
| `motor_hacmi` | Motor hacimleri listesi | 40 |

---

## 🔍 Filtreleme ve Sorgulama

### Temel Sorgulama Örnekleri

| İşlem | Örnek URL | Açıklama |
|-------|-----------|----------|
| **Tüm Kayıtlar** | `/vehicle-header` | Tüm araç başlıklarını getirir |
| **Tekil Kayıt** | `/vehicle-header/3` | ID=3 olan aracın başlığını getirir |
| **Filtreleme** | `/vehicle-status?durumRozeti.durum=aktif` | Aktif araçları getirir |
| **Sıralama** | `/vehicle-technical?_sort=motorGucu.hp&_order=desc` | Motor gücüne göre sıralar |
| **Sayfalama** | `/vehicle-maintenance?_page=1&_limit=5` | İlk 5 kaydı getirir |
| **Arama** | `/vehicle-identity?q=İstanbul` | İstanbul içeren kayıtları getirir |

### Gelişmiş Filtreleme Operatörleri

| Operatör | Açıklama | Örnek |
|----------|----------|--------|
| `_gte` | Büyük veya eşit | `?motorGucu.hp_gte=150` |
| `_lte` | Küçük veya eşit | `?kilometre.guncel_lte=50000` |
| `_ne` | Eşit değil | `?durum_ne=ariza` |
| `_like` | Benzer (regex) | `?plaka_like=34` |

---

## 🚀 Hızlı Başlangıç

### Sunucuyu Başlatma

```bash
# Bağımlılıkları yükle
npm install

# Sunucuyu başlat
npm run dev

# Sunucu http://localhost:3001 adresinde çalışacaktır
```

### Test İstekleri

```bash
# Tüm araç başlıklarını getir
curl http://localhost:3001/vehicle-header

# ID=5 olan aracın teknik bilgilerini getir
curl http://localhost:3001/vehicle-technical/5

# ID=3 olan aracın durumunu güncelle
curl -X PATCH http://localhost:3001/vehicle-status/3 \
  -H "Content-Type: application/json" \
  -d '{"durumRozeti": {"durum": "aktif", "renk": "success"}}'
```

---

## 📝 Notlar

- Tüm ID'ler string formatındadır ("1", "2", ... "10")
- Tarihler DD.MM.YYYY formatında saklanır
- Para birimleri TL olarak kabul edilir
- Kilometreler km cinsinden saklanır
- Elektrikli araçlarda `silindirHacmi: 0` ve `yakitDepoHacmi: 0` olur
- Her endpoint bağımsız olarak güncellenebilir