# Yapılacak Geliştirmeler

## PDF ve Excel Export İşlemleri

### Genel Yaklaşım
- PDF ve Excel export işlemleri **server-side** tarafında gerçekleştirilecek
- Kullanıcıya işlem durumu hakkında **toast bildirimleri** gösterilecek

### Detaylar
- Export işlemleri backend tarafında yapılacak
- İşlem başladığında kullanıcıya bildirim gösterilecek
- İşlem tamamlandığında başarı/hata bildirimi verilecek
- Dosya indirme işlemi otomatik başlatılacak veya indirme linki sağlanacak

### Gereksinimler
- [ ] Backend API endpoint'leri oluşturulacak
- [ ] Toast notification sistemi entegre edilecek
- [ ] Export işlemi sırasında loading state yönetimi
- [ ] Hata durumları için uygun mesajlar

## Tasarım ve Stil Yönetimi

### Renk Kullanımı
- Statik renk değerleri (hex, rgb) kullanılmamalı
- Hazır utility class'ları tercih edilmeli (örn: `primary`, `secondary`, `success`, `danger`, `warning`, `info`)
- Theme değişkenlerine bağlı class'lar kullanılmalı

### Gerekçe
- Tema değişikliklerinde tutarlılık sağlanır
- Kod bakımı kolaylaşır
- Design system'e uygunluk artar
- Dark mode ve farklı tema desteği kolayca sağlanır

### Örnek Kullanım
```vue
<!-- ❌ Yanlış -->
<div style="background-color: #3B82F6">

<!-- ✅ Doğru -->
<div class="bg-primary">
```
