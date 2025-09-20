# 📊 Sistem RAM Bilgisi Raporu

Bu rapor, `dmidecode` çıktıları kullanılarak hazırlanmıştır.  
Amaç: Mevcut RAM yapısını, maksimum kapasiteyi ve yükseltme imkânlarını göstermek.

---

## 1. Genel RAM Kapasitesi

| Komut | Çıktı | Yorum |
|-------|-------|-------|
| `sudo dmidecode -t memory \| grep -i "Maximum Capacity"` | `Maximum Capacity: 64 GB` | Anakart **toplamda 64 GB RAM** destekliyor. |
| `sudo dmidecode -t memory \| grep -i "Number Of Devices"` | `Number Of Devices: 2` | Anakartta **2 RAM slotu** mevcut. |

---

## 2. Slotlarda Takılı RAM Modülleri

| Komut | Çıktı (Özet) | Yorum |
|-------|--------------|-------|
| `sudo dmidecode -t memory \| grep -E "Size:|Locator:"` | - Slot 1: `Size: 8 GB, Locator: Controller0-ChannelA`  <br> - Slot 2: `Size: 8 GB, Locator: Controller1-ChannelA-DIMM0` | Her iki slota da **8 GB RAM** takılı. Toplam **16 GB RAM** mevcut. Boş slot yok. |

---

## 3. Detaylı Slot Bilgileri

| Komut | Çıktı (Özet) | Yorum |
|-------|--------------|-------|
| `sudo dmidecode -t memory` (Memory Device bölümü) | **Slot 1** <br> - Kapasite: 8 GB <br> - Tür: DDR4 SO-DIMM <br> - Hız: 3200 MT/s <br> - Üretici: Micron <br> - Model: 4ATF1G64HZ-3G2E1 <br><br> **Slot 2** <br> - Kapasite: 8 GB <br> - Tür: DDR4 SO-DIMM <br> - Hız: 3200 MT/s <br> - Üretici: SK Hynix <br> - Model: HMA81GS6DJR8N-XN | - İki slot da **DDR4 SO-DIMM 3200 MT/s** RAM ile dolu. <br> - Şu anda toplam **16 GB DDR4-3200** RAM kullanılıyor. |

---

## 4. Sonuç ve Yükseltme Senaryoları

- **Mevcut Durum:**  
  - 2×8 GB DDR4-3200 SO-DIMM → **16 GB RAM**  
- **Maksimum Destek:**  
  - 2×32 GB DDR4-3200 SO-DIMM → **64 GB RAM**  

### Yükseltme Önerileri:
1. **32 GB yapmak için** → 2×16 GB DDR4-3200 SO-DIMM ile değiştirme.  
2. **Maksimum 64 GB yapmak için** → 2×32 GB DDR4-3200 SO-DIMM ile değiştirme.  
3. En iyi performans için **aynı marka ve model** modüller tercih edilmeli.  

---

✅ Bu bilgiler ışığında, sistemin **maksimum kapasitesi 64 GB (DDR4-3200 SO-DIMM)** olup mevcut 16 GB RAM yükseltme için yeterli alan vardır.
