# İncelediklerim

## VEHİCLE
- **Araç Listesi** - index.vue (`3-c-veh-feat-001`)
- **OCR ile Araç Ekleme** - create.vue (`10-c-veh-fe-002`)
  - Composable'lar:
    1. `useVehicleForm.ts` - Form state yönetimi, validation ve submission işlemleri
    2. `useVehicleImageEditor.ts` - Syncfusion image editor yapılandırması ve görsel işleme
    3. `useVehicleStepper.ts` - Çok adımlı form navigasyonu ve step yönetimi

## CARİ-ORGANİZASYON
- **Organizasyon(cari) Listeleme** - index.vue (`34-f-ten-fe-003`)
  - **Not:** Bu kısmın composable'ı çok geniş. Her şeyi yaptım. Buradan örnek alabiliriz.
  - Checkbox işaretlileri alma data seçili iken
  - Server side pdf excel yapacağız indirme için
  - DATE RANGE olayı burada ✅ **TAMAMLANDI**
  - Composable'lar:
    1. `useTenantsToolbar.ts` - Toolbar yapılandırması ve event handler'ları
    2. `useTenantsMenu.ts` - Menu actions ve clipboard kopyalama
    3. `useGridSearch.ts` - Grid arama fonksiyonelliği
    4. `useTenantsCustomFilters.ts` - Custom filter yapılandırmaları
    5. `useTenantsSorting.ts` - Sıralama event tracking
    6. `useTenantsPaging.ts` - Sayfalama (pagination) yönetimi
    7. `useTenantsColumns.ts` - Kolon değişiklikleri tracking (resize, reorder, visibility)
    8. `useDateRangeFilter.ts` - Date range filter yönetimi

- **Organizasyon(cari) Ekleme** - create.vue (`31-f-ten-fe-004`)
  - **Not:** Bu kısım composable ve type'a ayrılacak
  - Composable'lar:
    1. `useOrganizationForm.ts` - Form state yönetimi ve organizasyon create/edit işlemleri (tip değişimi, submit, cancel, reset)
    2. `usePhoneInput.ts` - Türk telefon numarası maskeleme (+90 5XX XXX XX XX)

## DRİVER
- **Sürücü Listesi** - index.vue (`37-s-drv-fe-001`)
  - Composable'lar:
    1. `useDriversToolbar.ts` - Toolbar yapılandırması ve event handler'ları
    2. `useDriversMenu.ts` - Menu actions ve clipboard kopyalama
    3. `useGridSearch.ts` - Grid arama fonksiyonelliği
    4. `useDriversCustomFilters.ts` - Custom filter yapılandırmaları (Şoför Adı, Şoför Soyadı)
    5. `useDriversSorting.ts` - Sıralama event tracking
    6. `useDriversPaging.ts` - Sayfalama (pagination) yönetimi
    7. `useDriversColumns.ts` - Kolon değişiklikleri tracking (resize, reorder, visibility)

- **Sürücü Ekleme** - create.vue (`40-s-drv-fe-003`)

## AUTHENTICATION
- **Authentication** - (`14-f-aut-fe-001`)
  - Composable'lar:
    1. `useErrorMessage.ts` - Hata mesajı yönetimi için reactive state ve metodlar
    2. `useIdentifierInput.ts` - Email veya telefon input için dinamik UI özellikleri (tip algılama, icon, placeholder, mask)
    3. `usePasswordVisibility.ts` - Şifre görünürlük toggle yönetimi
