# Filo Yönetimi Raporlama Ekranı Fikirleri

## 1. Araç ve Envanter Raporları

| Rapor Adı | Açıklama | Özellikler | Öncelik |
|-----------|----------|------------|---------|
| **Araç Durum Paneli** | Filodaki araçların mevcut durumlarının görsel dağılımı | • Pasta/Bar grafik ile durum gösterimi<br>• "Aktif", "Bakımda", "Satılmış", "Kiralık" kategorileri<br>• Anlık durum özeti | Yüksek |
| **Araç Envanter Listesi** | Tüm araçların detaylı listesi | • Marka, model, yıl, plaka filtreleri<br>• Departman bazlı görüntüleme<br>• Excel/PDF export | Yüksek |
| **Donanım Raporu** | Araç ek donanımlarının takibi | • Kış lastiği, GPS, yangın tüpü vb.<br>• Donanım bazlı arama<br>• Eksik donanım uyarıları | Orta |
| **Araç Yaşı Analizi** | Filo yaş dağılımı ve yenileme planlaması | • Yaş gruplarına göre dağılım grafiği<br>• Ortalama filo yaşı<br>• Yenileme önerileri | Orta |

## 2. Operasyonel Raporlar

| Rapor Adı | Açıklama | Özellikler | Öncelik |
|-----------|----------|------------|---------|
| **Yakıt Tüketim Raporu** | Yakıt verimliliği ve maliyet analizi | • Araç/Sürücü bazında ortalama tüketim (lt/100km)<br>• Kilometre başına maliyet (TL/km)<br>• Trend analizleri ve grafikler | Çok Yüksek |
| **Lastik Yönetim Raporu** | Lastik kullanım ömrü ve maliyet takibi | • Lastik ömür tahminleri<br>• Maliyet/km analizi<br>• Mevsimsel değişim hatırlatıcıları | Orta |
| **İkame Araç Raporu** | İkame araç kullanım analizi | • Kullanım süreleri<br>• Toplam ikame maliyeti<br>• Araç bazlı ikame geçmişi | Düşük |

## 3. Finansal Raporlar

| Rapor Adı | Açıklama | Özellikler | Öncelik |
|-----------|----------|------------|---------|
| **TCO (Toplam Sahip Olma Maliyeti)** | Araç bazında tüm maliyetlerin analizi | • Satın alma, yakıt, bakım, sigorta, vergi detayları<br>• Araç karşılaştırmaları<br>• Maliyet/km hesaplaması | Çok Yüksek |
| **Fatura ve Ödeme Durum Raporu** | Finansal yükümlülüklerin takibi | • Ödendi/Beklemede/Vadesi geçmiş kategorileri<br>• Fatura tiplerine göre filtreleme<br>• Vade uyarıları | Yüksek |
| **Bütçe vs Gerçekleşen** | Planlanan ve gerçekleşen harcamaların karşılaştırması | • Departman/Araç bazlı analiz<br>• Sapma yüzdeleri<br>• Aylık/Yıllık görünümler | Yüksek |

## 4. Uyumluluk ve Belge Yönetimi Raporları

| Rapor Adı | Açıklama | Özellikler | Öncelik |
|-----------|----------|------------|---------|
| **Süresi Dolan Belgeler Paneli** | Yaklaşan belge yenileme tarihleri | • Sigorta, muayene, egzoz tarihleri<br>• 30-60-90 gün önceden uyarılar<br>• Renk kodlu uyarı sistemi | Çok Yüksek |
| **Eksik Belge Raporu** | Araç türüne göre eksik belgelerin tespiti | • Zorunlu belgeler kontrolü<br>• Araç türü bazlı analiz<br>• Ceza riski uyarıları | Yüksek |
| **Ceza Raporu** | Trafik cezaları takibi | • Araç/Sürücü bazlı cezalar<br>• Ödeme durumu takibi<br>• Ceza tiplerine göre analiz | Orta |

## Teknik Uygulama Planı

### Aşama 1: Veri Altyapısı
| Görev | Açıklama | Süre |
|-------|----------|------|
| **Veritabanı Kurulumu** | SQL scriptlerinden test DB oluşturma | 1 gün |
| **Örnek Veri Yükleme** | Test için gerçekçi veri seti hazırlama | 2 gün |
| **API Katmanı** | CRUD işlemleri için REST API | 3 gün |

### Aşama 2: Frontend Geliştirme
| Görev | Açıklama | Süre |
|-------|----------|------|
| **Dashboard Tasarımı** | Ana kontrol paneli UI/UX | 2 gün |
| **Grafik Entegrasyonu** | Chart.js/Recharts kurulumu | 2 gün |
| **Rapor Modülleri** | Her rapor için ayrı component | 10 gün |

### Aşama 3: Entegrasyon ve Test
| Görev | Açıklama | Süre |
|-------|----------|------|
| **API Entegrasyonu** | Frontend-Backend bağlantısı | 2 gün |
| **Performans Optimizasyonu** | Sorgu ve yükleme hızı iyileştirmeleri | 2 gün |
| **Kullanıcı Testleri** | UAT ve feedback toplama | 3 gün |

## Teknoloji Stack Önerisi

| Katman | Teknoloji | Alternatif |
|--------|-----------|------------|
| **Frontend** | React + TypeScript | Vue.js, Angular |
| **Grafik Kütüphanesi** | Recharts | Chart.js, D3.js |
| **Backend** | Node.js + Express | Python + FastAPI |
| **Veritabanı** | PostgreSQL | SQLite (test için) |
| **State Management** | Redux Toolkit | Zustand, Context API |
| **UI Components** | Material-UI | Ant Design, Tailwind UI |

## Başlangıç için Öncelikli Raporlar

1. **Süresi Dolan Belgeler Paneli** - Yasal uyumluluk kritik
2. **Yakıt Tüketim Raporu** - Maliyet kontrolü için önemli
3. **TCO Raporu** - Stratejik karar verme için gerekli
4. **Araç Durum Paneli** - Genel görünüm sağlar