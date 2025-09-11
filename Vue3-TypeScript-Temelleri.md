# Vue 3 TypeScript Temelleri - Soru & Cevap

## Soru: `const loading = ref(false)`, `const vehicle: Ref<Vehicle | null> = ref(null)`, `const error = ref<string | null>(null)` bu tanımlamalar ne demek?

**Cevap:** Bu tanımlamalar Vue 3 Composition API'de reactive referanslar oluşturuyor:

- `loading = ref(false)` - Boolean tipinde reaktif değişken, başlangıçta `false`
- `vehicle: Ref<Vehicle | null> = ref(null)` - `Vehicle` tipinde veya `null` olabilen reaktif değişken, başlangıçta `null`
- `error = ref<string | null>(null)` - String veya `null` olabilen reaktif değişken, başlangıçta `null`

`ref()` fonksiyonu primitive değerleri reaktif yapar, değiştiğinde component otomatik re-render olur.

```typescript
const data = ref(null)
// data.value = "yeni değer" şeklinde erişilir
```

## Soru: `=` ile `:` arasındaki fark ne bu tanımlamalarda?

**Cevap:** Bu tanımlamalarda `=` ve `:` farklı amaçlar için kullanılıyor:

**`:` (iki nokta üst üste)** - TypeScript tip tanımlaması
```typescript
const vehicle: Ref<Vehicle | null> = ref(null)
//            ^^^^^^^^^^^^^^^^^ tip tanımı
```

**`Ref<Vehicle | null>`** ne demek:
- `Ref<>` = Vue 3'te reactive reference tipi
- `Vehicle | null` = Ya Vehicle objesi ya da null olabilir (Union type)
- `|` = "veya" anlamında (Union operator)

**`=` (eşittir)** - Değer ataması
```typescript
const vehicle: Ref<Vehicle | null> = ref(null)
//                                 ^ değer ataması
```

Kısaca:
- `:` → "Bu değişkenin tipi şudur"
- `=` → "Bu değişkenin değeri şudur"

## Soru: `Record<string, any>` bu ne demek?

**Cevap:** `Record<string, any>` TypeScript'te bir tip tanımlamasıdır:

**Record<K, V>** - Anahtar-değer çiftlerinden oluşan obje tipi
- `K` = Anahtar tipi
- `V` = Değer tipi

`Record<string, any>` demek:
- **Anahtarlar**: `string` tipinde
- **Değerler**: `any` tipinde (herhangi bir tip olabilir)

**Örnek kullanım:**
```typescript
const updateData: Record<string, any> = {
  name: "Yeni İsim",        // string anahtar, string değer
  age: 25,                  // string anahtar, number değer
  isActive: true,           // string anahtar, boolean değer
  colors: ["red", "blue"]   // string anahtar, array değer
}
```

## Soru: `ref(null)`, `Record` bunlar ne demek?

**Cevap:**

**`ref(null)`** - Vue 3 Composition API fonksiyonu:
- Reaktif referans oluşturur
- Başlangıç değeri `null`
- Değer değiştiğinde component otomatik güncellenir

```typescript
const data = ref(null)
// data.value = "yeni değer" şeklinde erişilir
```

**`Record`** - TypeScript'te built-in utility type:
- Obje tiplerini tanımlamak için kullanılır
- `Record<KeyType, ValueType>` formatında

```typescript
// Bu ikisi aynı anlama gelir:
Record<string, any>
{ [key: string]: any }

// Örnek:
const user: Record<string, string> = {
  name: "Ali",
  email: "ali@example.com"
}
```

**Kısaca:**
- `ref()` = Vue'da reaktiflik için
- `Record` = TypeScript'te obje tipi tanımlamak için

## Pratik Örnek

```typescript
const updateVehicle = async (id: string, updateData: Record<string, any>) => {
    await vehiclesStore.patchVehicle(id, updateData)
    // Sync local state without API call
    Object.assign(vehicle.value, updateData)
}

// Kullanım
updateVehicle("123", {
  name: "Yeni Araç",
  model: "2024",
  color: "Kırmızı"
})
```