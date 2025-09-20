# 🚗 Araç Kartı Bilgileri (Güncel + Genişletilmiş)

## 1. Araç Kimlik Bilgileri
- **Plaka**
- **Marka / Model / Model Yılı**
- **Ticari Adı**
- **Bağlı olduğu organizasyon** (şube/filo)
- **Bölge / Aktif lokasyon**

## 2. Durum & Operasyon
- **Durum rozeti** (Aktif, Pasif, Bakımda, Arıza vb.)
- **Araç kilometresi** (güncel odometre)
- **Harcanan yakıt** (aylık)
- **Atanmış sürücü** (aktif atama bilgisi)
- **Son hareket nedeni** (örn. periyodik bakım, kaza, test sürüşü)
- **Son konum bilgisi** (garaj, şehir, GPS etiketi)
- **Son güncellenme zamanı** (telemetri datası varsa)

## 3. Muayene & Sigorta
- **Muayene tarihi** (+ kalan gün)
- **Sigorta poliçe bitiş tarihi** (+ yenileme durumu)
- **Sigorta prim tutarı** (opsiyonel)
- **Zorunlu belgeler:**
  - Ruhsat geçerlilik durumu
  - Egzoz emisyon belgesi (bitiş tarihi + kalan gün)
  - K belgesi (varsa – taşımacılık için)
  - HGS/OGS etiketi (geçerlilik/bakiye durumu)
  - Trafik sigortası (zorunlu)
  - Kasko poliçesi (varsa)
- **Eksik belge uyarısı** (ör. kırmızı ikon ile "K belgesi eksik")

## 4. Bakım & Arıza
- **Arıza geçmişi** (özet: son arıza, tarihi, durumu)
- **Yapılan bakım işleri / değişen parçalar**
- **Yaklaşan bakım planı** (periyodik servis veya planlı müdahale)
- **Tahmini bakım maliyeti** (opsiyonel)
- **Servis periyodu** (örn. her 10.000 km'de bakım)

## 5. Teknik Özellikler
- **Araç sınıfı** (M1, N2 vb.)
- **Cinsi / Tipi** (Otomobil, Kamyonet vb.)
- **Renk**
- **Motor gücü** (kW)
- **Silindir hacmi** (cc)
- **Net ağırlık**
- **Azami yüklü ağırlık**
- **Römork kapasitesi** (varsa)
- **Koltuk sayısı**
- **Ayakta yolcu kapasitesi** (varsa)
- **Yakıt tipi**
- **Motor tipi / Emisyon standardı** (Euro 6, elektrikli vb.)
- **Şanzıman türü** (manuel, otomatik, CVT vb.)

## 6. Üst Yapı
- **Üst yapı tipi** (ör. vinç, tanker, kapalı kasa vb.)
- **Üretici**
- **Kapasite**
- **Mevcut doluluk** (örn. tanker litre, kasa % doluluk)

## 7. Resmi Kayıt Bilgileri
- **İlk tescil tarihi**
- **Son tescil tarihi** (+ tescil sıra no)
- **Şasi no**
- **Motor no**
- **Sahibin adı / TCKN – Vergi No**
- **Sahibin adresi** (isteğe bağlı gösterim)
- **Finansal durum** (araç kredi/lease mi, tamamen satın mı alınmış)

---

# 🖼 Araç Kartı Ekranı (Tasarım Mantığı)

## 📌 Sayfa Yapısı
- Üstte sayfa başlığı: **"Araç Detayları"** (yanında plaka büyük badge gibi)
- Altında alt alta komponent blokları, her biri kart/kutu şeklinde, başlık ve içeriği ile
- Bloklar arasında boşluk (margin) ve gölge (shadow-md) olacak, böylece her biri ayrı bir bilgi kartı gibi görünecek

## 🔹 Üst Bilgi Alanı (Header)
- Sol üstte **Plaka** → büyük badge formatında (ör. 34 ABC 123)
- Sağda küçük **Durum Rozeti** (yeşil = aktif, sarı = bakımda, kırmızı = arıza)
- Altında **Marka / Model / Yıl** büyük fontta
- Hemen altında **Ticari Adı** (ör. Corolla 1.6 Advance)

## 🔹 Araç Kimlik Bilgileri (Card 1)
**📦 Başlık:** Araç Kimlik Bilgileri
- Plaka
- Marka / Model / Model Yılı
- Ticari Adı
- Bağlı olduğu organizasyon
- Bölge / aktif lokasyon

## 🔹 Durum & Operasyon (Card 2)
**📦 Başlık:** Durum & Operasyon
- Durum Rozeti (ikon + renk)
- Araç kilometresi (odometre) → progress bar ile görselleştirilebilir
- Harcanan yakıt (aylık) → mini bar chart olabilir
- Atanmış sürücü → küçük avatar + isim
- Son hareket nedeni → küçük etiket (örn. "Periyodik Bakım")
- Son konum bilgisi (şehir/garaj) + son güncellenme zamanı

## 🔹 Muayene & Sigorta (Card 3)
**📦 Başlık:** Muayene & Sigorta
- Muayene tarihi + kalan gün → kalan gün için progress (örn. 12 gün kaldı)
- Sigorta poliçe bitiş tarihi + yenileme durumu → renkli uyarı kutusu
- **Zorunlu belgeler:** her biri küçük badge veya ✅❌ ikon ile:
  - Ruhsat
  - Egzoz emisyon
  - K belgesi
  - HGS/OGS
  - Trafik sigortası
  - Kasko

## 🔹 Bakım & Arıza (Card 4)
**📦 Başlık:** Bakım & Arıza
- Son arıza (tarih + açıklama)
- Yapılan bakım işleri (liste, tarih + kısa açıklama)
- Yaklaşan bakım planı
- Tahmini maliyet (jenerik rakam alanı)
- Servis periyodu (örn. "her 10.000 km")

## 🔹 Teknik Özellikler (Card 5)
**📦 Başlık:** Teknik Özellikler

**Grid düzeninde (2 kolon) gösterim:**
- Araç sınıfı
- Cinsi / Tipi
- Renk
- Motor gücü (kW)
- Silindir hacmi (cc)
- Net ağırlık
- Azami yüklü ağırlık
- Römork kapasitesi
- Koltuk sayısı
- Ayakta yolcu kapasitesi
- Yakıt tipi
- Motor tipi / Emisyon standardı
- Şanzıman türü

## 🔹 Üst Yapı (Card 6)
**📦 Başlık:** Üst Yapı
- Üst yapı tipi (ör. vinç, tanker)
- Üretici
- Kapasite
- Mevcut doluluk (örn. %65, progress bar ile)

## 🔹 Resmi Kayıt Bilgileri (Card 7)
**📦 Başlık:** Resmi Kayıt Bilgileri

**Liste halinde:**
- İlk tescil tarihi
- Son tescil tarihi + sıra no
- Şasi no
- Motor no
- Sahip bilgisi (Adı / TCKN-Vergi No)
- Sahibin adresi (opsiyonel)
- Finansal durum (satın / kredi / leasing)