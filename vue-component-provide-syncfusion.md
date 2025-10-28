# Vue Component Provide & Syncfusion Grid Modülleri

## Tarih
2025-10-18

## Konu
`defineOptions` ile component kaydı ve Syncfusion Grid'e modül enjeksiyonu

---

## 1. defineOptions Nedir?

- Vue 3'te `<script setup>` kullanırken component ayarlarını tanımlamak için kullanılan **makro**
- **Derleme zamanında** (compile-time) çalışır
- `export default {}` yazmadan component seçeneklerini belirlememizi sağlar

### Kullanım Alanları
- `name`: Component ismi (DevTools'da görünür)
- `components`: Template'de kullanılacak componentleri kaydetme
- `provide`: Child componentlere veri/modül sağlama

---

## 2. Components Kaydı

### Söz Dizimi
```javascript
components: {
  'template-tag-adi': ActualComponentName
}
```

### Örnek
```javascript
components: {
  'ejs-grid': GridComponent,
  'ejs-multiselect': MultiSelectComponent
}
```

### Neden Böyle Yapıyoruz?
1. **HTML kuralı**: Tag isimleri büyük harf tanımaz
   - ✅ `<ejs-grid>` çalışır
   - ❌ `<EjsGrid>` çalışmaz (HTML'de)

2. **Syncfusion konvansiyonu**: `ejs-` prefix kullanırlar

3. **Okunabilirlik**: Hangi kütüphaneden geldiği belli

---

## 3. Provide - Dependency Injection

### Ne İşe Yarar?
- Parent component'ten child componentlere veri/özellik **sağlama**
- Child'lar `inject` ile bu verilere erişir
- Props gibi değil, **derin** child'lara da ulaşır (prop drilling olmadan)

### Syncfusion Grid'de Provide

```javascript
provide: {
  grid: [Toolbar, Resize, Reorder, Sort, Filter, PdfExport, ExcelExport, Page, ColumnChooser]
}
```

#### Neden Gerekli?

**Syncfusion'ın Modüler Yapısı:**
- Grid component varsayılan olarak **minimal** gelir
- Her özellik (toolbar, sort, filter) **ayrı modül**
- Kullanmadığın modülleri import etmezsen **bundle boyutu küçülür**

#### Nasıl Çalışır?

1. **Import ediyoruz:**
   ```javascript
   import { Toolbar, Sort, Filter } from '@syncfusion/ej2-vue-grids'
   ```

2. **Provide ile sağlıyoruz:**
   ```javascript
   provide: {
     grid: [Toolbar, Sort, Filter]
   }
   ```

3. **Grid içinde inject ediliyor:**
   - GridComponent bu modülleri alıyor
   - İlgili özellikleri aktive ediyor

4. **Template'de kullanıyoruz:**
   ```vue
   <ejs-grid
     :allowSorting="true"    <!-- Sort modülü gerekli -->
     :allowFiltering="true"   <!-- Filter modülü gerekli -->
     :toolbar="[...]"         <!-- Toolbar modülü gerekli -->
   >
   ```

#### ⚠️ Modül Eklemezsek Ne Olur?

```javascript
// Sort modülü provide edilmemiş
provide: {
  grid: [Toolbar, Filter]  // Sort YOK!
}
```

```vue
<!-- Template'de kullansak bile çalışmaz -->
<ejs-grid :allowSorting="true">  ❌ Çalışmaz, console'da hata!
```

**Hata:** `"Inject Sort module in Grid to use sorting feature"`

---

## 4. Tam Örnek - Akış

### Adım 1: Import
```javascript
import { GridComponent, Toolbar, Sort, Filter } from '@syncfusion/ej2-vue-grids'
```

### Adım 2: defineOptions ile Kayıt
```javascript
defineOptions({
  name: 'VehiclesPage',
  components: {
    'ejs-grid': GridComponent  // Template'de <ejs-grid> yazabilmek için
  },
  provide: {
    grid: [Toolbar, Sort, Filter]  // Grid'e modülleri sağla
  }
})
```

### Adım 3: Template'de Kullan
```vue
<ejs-grid
  :allowSorting="true"     <!-- Sort modülü sayesinde çalışır -->
  :allowFiltering="true"    <!-- Filter modülü sayesinde çalışır -->
  :toolbar="['Add', 'Delete']"  <!-- Toolbar modülü sayesinde çalışır -->
>
```

---

## 5. Önemli Notlar

### Component Naming
- **Kebab-case** kullan: `'ejs-grid'`, `'e-column'`
- PascalCase HTML'de çalışmaz: `<EjsGrid>` ❌

### Modül Yönetimi
- Sadece **kullandığın** modülleri import et
- Her modül bundle boyutuna eklenir
- Örnek: PDF export kullanmıyorsan `PdfExport` modülünü ekleme

### Provide vs Props Farkı
- **Props**: Sadece direkt child'a geçer
- **Provide**: Tüm child ağacına erişilebilir
- Syncfusion componentleri internal olarak `inject` kullanır

---

## 6. Sorular & Cevaplar

### S: Neden süslü parantez `{}` var?
```javascript
import { GridComponent } from '@syncfusion/ej2-vue-grids'
```
**C:** **Named import** kullanıyoruz. Dosyadan belirli isimdeki export'u alıyoruz. `export default` olsaydı `{}` kullanmazdık.

---

### S: `type VehicleGridRow` neden `type` kelimesi ile import ediliyor?
```javascript
import { type VehicleGridRow } from '~/data/vehicles/mockVehiclesData'
```
**C:** TypeScript **tip tanımı** olduğunu belirtiyoruz. Derleme sonrası bu satır silinir (runtime'da kullanılmaz).

---

### S: Provide ettiğimiz modüller nereye gidiyor?
**C:** GridComponent'in içinde `inject` ile alınıyor. Biz provide ediyoruz, component inject ediyor.

---

### S: Grid'e 10 modül var, hepsini eklemek zorunda mıyım?
**C:** Hayır! Sadece **kullanacağın** özelliklerin modüllerini ekle:
- `allowSorting` kullanıyorsan → `Sort` ekle
- `allowFiltering` kullanıyorsan → `Filter` ekle
- PDF export yok → `PdfExport` ekleme

---

## 7. Kaynak Kod Referansı

Dosya: `app/pages/vehicles/index.vue:38-52`

```javascript
defineOptions({
  name: 'VehiclesPage',
  components: {
    'ejs-grid': GridComponent,
    'e-columns': ColumnsDirective,
    'e-column': ColumnDirective,
    'ejs-multiselect': MultiSelectComponent,
    'ejs-toolbar': ToolbarComponent,
    'ejs-button': ButtonComponent,
    'ejs-dropdownbutton': EjsDropdownbutton
  },
  provide: {
    grid: [Toolbar, Resize, Reorder, Sort, Filter, PdfExport, ExcelExport, Page, ColumnChooser]
  }
})
```

---

## 8. Özet Tablo

| Kavram | Açıklama | Örnek |
|--------|----------|-------|
| `defineOptions` | Component ayarlarını tanımla | `defineOptions({ name: 'Foo' })` |
| `components` | Template'de kullanılacak componentler | `'ejs-grid': GridComponent` |
| `provide` | Child'lara veri/modül sağla | `grid: [Toolbar, Sort]` |
| Named Import | Belirli isimdeki export'u al | `import { Foo } from 'bar'` |
| Modüler Yapı | Özellikleri ayrı modüller halinde sunma | `import { Sort, Filter }` |

---

## 9. İleri Okuma

- Vue Provide/Inject: https://vuejs.org/guide/components/provide-inject.html
- Syncfusion Grid Modules: https://ej2.syncfusion.com/vue/documentation/grid/module
- TypeScript Type Imports: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-8.html#type-only-imports-and-export

---

**Not:** Bu döküman `vehicles/index.vue` sayfasını öğrenirken çıkan soruları içerir.
