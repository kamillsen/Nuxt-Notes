# Vue Ref Tipleri - Basit Kılavuz

## Tarih
2025-10-19

## Konu
`ref()` ile tip tanımlama: Component vs Veri

---

## Ana Kural

### Soru: Ne referans ediyorsun?

| Ne? | Nasıl? | Örnek |
|-----|--------|-------|
| **Component (class)** | `ref<InstanceType<typeof X> \| null>(null)` | Syncfusion, PrimeVue |
| **Veri (interface/type)** | `ref<X>(initialValue)` | Araba, Kullanici, Vehicle |

---

## 1️⃣ Component Ref (Class-based)

### Kullanım
```typescript
import { GridComponent } from '@syncfusion/ej2-vue-grids'

const grid = ref<InstanceType<typeof GridComponent> | null>(null)
```

### Template
```vue
<ejs-grid ref="grid">
</ejs-grid>
```

### Neden InstanceType?
- GridComponent bir **class** (Syncfusion'ın yazdığı)
- `typeof GridComponent` → Class'ın tipi
- `InstanceType<...>` → Class'tan yaratılan instance'ın tipi

### Kullanım Örneği
```typescript
// Component metodlarını çağır
grid.value?.refresh()
grid.value?.clearSorting()
grid.value?.exportToPdf()
```

---

## 2️⃣ Veri Ref (Interface/Type)

### Interface Tanımı
```typescript
interface Araba {
  marka: string
  renk: string
  yil: number
}
```

### Kullanım
```typescript
// Tek obje
const araba = ref<Araba | null>(null)

// Array
const arabalar = ref<Araba[]>([])

// Primitive
const mesaj = ref<string>('')
const sayi = ref<number>(0)
```

### Neden Direkt Tip?
- Araba bir **interface** (sadece tip tanımı, class değil)
- `InstanceType` sadece class'lar için kullanılır

### Kullanım Örneği
```typescript
// Veri atama
araba.value = { marka: 'Toyota', renk: 'Kırmızı', yil: 2024 }

// Veri okuma
console.log(araba.value?.marka)  // 'Toyota'

// Array'e ekleme
arabalar.value.push({ marka: 'BMW', renk: 'Siyah', yil: 2023 })
```

---

## Fark: Class vs Interface

### Class (Çalıştırılabilir Kod)
```typescript
class GridComponent {
  refresh() {
    console.log('Grid yenilendi')
  }
}

// Instance yaratabilirsin
const grid = new GridComponent()  ✅
grid.refresh()  // Metod çağrılır
```

### Interface (Sadece Tip Tanımı)
```typescript
interface Araba {
  marka: string
}

// Instance yaratamazsın!
const araba = new Araba()  ❌ HATA!
// "Araba sadece bir tip tanımı, constructor yok"
```

---

## Tam Örnek

```typescript
// ============================================
// COMPONENT REF
// ============================================
import { ref } from 'vue'
import { GridComponent } from '@syncfusion/ej2-vue-grids'

const grid = ref<InstanceType<typeof GridComponent> | null>(null)

// Component mount olduktan sonra:
grid.value?.refresh()  // ✅ Metod çağır


// ============================================
// VERİ REF
// ============================================
interface Kullanici {
  ad: string
  yas: number
  email: string
}

const kullanici = ref<Kullanici | null>(null)

// Veri işlemleri:
kullanici.value = {
  ad: 'Ali',
  yas: 25,
  email: 'ali@example.com'
}

console.log(kullanici.value?.ad)  // 'Ali'
```

---

## Type Alias Kullanımı

### Tip Tanımla ve Yeniden Kullan

```typescript
// types/vehicles/index.ts
import { GridComponent } from '@syncfusion/ej2-vue-grids'

export type GridInstance = InstanceType<typeof GridComponent>
```

### Kullanım
```typescript
import type { GridInstance } from '~/types/vehicles'

// Artık daha kısa:
const grid = ref<GridInstance | null>(null)

// Yerine:
// const grid = ref<InstanceType<typeof GridComponent> | null>(null)
```

### Faydaları
- ✅ Kod tekrarını önler
- ✅ Okunabilir
- ✅ Tek yerden yönetim
- ✅ Değişiklik kolaylığı

---

## Hızlı Karar Ağacı

```
ref() yaratacaksın
    ↓
    ┌─────────────────────────────┐
    │ Component mi? Veri mi?      │
    └─────────────────────────────┘
           ↓              ↓
    Component          Veri
           ↓              ↓
    Class mi?      Interface/Type
           ↓              ↓
    InstanceType    Direkt Yaz
           ↓              ↓
ref<InstanceType<  ref<Araba>
typeof Grid>>
```

---

## Yaygın Hatalar

### ❌ Veri için InstanceType kullanma
```typescript
interface Vehicle { id: number }
const vehicle = ref<InstanceType<typeof Vehicle>>(null)
// HATA: Vehicle bir class değil!
```

**✅ Doğrusu:**
```typescript
const vehicle = ref<Vehicle | null>(null)
```

---

### ❌ null başlangıç ama tipte null yok
```typescript
const count = ref<number>(null)
// HATA: null number değil
```

**✅ Doğrusu:**
```typescript
const count = ref<number | null>(null)
// veya
const count = ref<number>(0)
```

---

### ❌ Component için yanlış tip
```typescript
const grid = ref<GridComponent>(null)
// Çalışabilir ama standart değil
```

**✅ Doğrusu:**
```typescript
const grid = ref<InstanceType<typeof GridComponent> | null>(null)
```

---

## Özet Tablo

| Senaryo | Kod | Açıklama |
|---------|-----|----------|
| Syncfusion Grid | `ref<InstanceType<typeof GridComponent> \| null>(null)` | Class-based component |
| Vue Component | `ref<ComponentPublicInstance \| null>(null)` | Generic Vue component |
| Custom Type Alias | `ref<GridInstance \| null>(null)` | Type alias kullanımı |
| Interface (tek) | `ref<Vehicle \| null>(null)` | Nullable interface |
| Interface (array) | `ref<Vehicle[]>([])` | Array |
| String | `ref<string>('')` | Primitive |
| Number | `ref<number>(0)` | Primitive |

---

## Gerçek Proje Örneği

```typescript
// types/vehicles/index.ts
import { GridComponent } from '@syncfusion/ej2-vue-grids'
import { MultiSelectComponent } from '@syncfusion/ej2-vue-dropdowns'

export type GridInstance = InstanceType<typeof GridComponent>
export type MultiSelectInstance = InstanceType<typeof MultiSelectComponent>

export interface VehicleGridRow {
  vehicle_id: string
  plate_number: string
  brand_name: string
  model_year: number
}
```

```typescript
// pages/vehicles/index.vue
import type { GridInstance, MultiSelectInstance, VehicleGridRow } from '~/types/vehicles'

const grid = ref<GridInstance | null>(null)
const ms = ref<MultiSelectInstance | null>(null)
const vehiclesData = ref<VehicleGridRow[]>([])

// Component metodları
grid.value?.refresh()

// Veri işlemleri
vehiclesData.value.push({
  vehicle_id: '1',
  plate_number: '34ABC123',
  brand_name: 'Toyota',
  model_year: 2024
})
```

---

## Sonuç

**Tek kural:**
- Class → `InstanceType<typeof ...>`
- Interface/Type → Direkt kullan

**Neden önemli?**
- TypeScript tip kontrolü yapar
- Otomatik tamamlama çalışır
- Hataları derleme zamanında yakalar

---

## Kaynaklar

- TypeScript InstanceType: https://www.typescriptlang.org/docs/handbook/utility-types.html#instancetypetype
- Vue Refs: https://vuejs.org/guide/essentials/template-refs.html
- Vue TypeScript: https://vuejs.org/guide/typescript/composition-api.html

---

**Not:** Bu döküman `vehicles/index.vue` sayfasını öğrenirken ref tiplemeleri konusunda çıkan soruları içerir.
