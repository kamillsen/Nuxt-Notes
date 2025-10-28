# Syncfusion EJ2 Vue ListBox - Sürükle-Bırak Sıralama ve ID Listesi Alma

Bu belge, **aynı ListBox içinde fareyle** sürükle-bırak yapınca oluşan *yeni sırayı* **yalnızca ID dizisi** olarak elde etmeyi gösterir. Kod, Syncfusion EJ2 **resmi dokümantasyonundaki** yapıya sadık kalır (bkz. kaynaklar).

---

## Ön Koşullar

Gerekli paketi yükleyin:

```bash
npm i @syncfusion/ej2-vue-dropdowns
```

**Not:** Tema CSS'lerini de eklediğinizden emin olun (aşağıdaki örnekte gösterildi).

---

## Yapıştır-Çalıştır Örnek (Vue 3 Composition API)

> **Not:** `ref` ile alınan EJ2 instance'a `lb.value.ej2Instances` üzerinden erişilir.

```ts
<!-- App.vue (veya herhangi bir .vue sayfan) -->
<template>
  <div id="app">
    <div id="container" style="margin:10px auto 0; width:250px;">
      <ejs-listbox
        ref="lb"
        :dataSource="data"
        :fields="{ text: 'text', value: 'id' }"
        :allowDragAndDrop="true"
        @drop="onDrop"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { ListBoxComponent as EjsListbox } from "@syncfusion/ej2-vue-dropdowns";

const lb = ref(null);

const data = [
  { text: 'Hennessey Venom', id: 'list-01' },
  { text: 'Bugatti Chiron', id: 'list-02' },
  { text: 'Bugatti Veyron Super Sport', id: 'list-03' },
  { text: 'SSC Ultimate Aero', id: 'list-04' },
  { text: 'Koenigsegg CCR', id: 'list-05' },
  { text: 'McLaren F1', id: 'list-06' },
  { text: 'Aston Martin One- 77', id: 'list-07' },
  { text: 'Jaguar XJ220', id: 'list-08' },
  { text: 'McLaren P1', id: 'list-09' },
  { text: 'Ferrari LaFerrari', id: 'list-10' }
];

// Bırakma anında yeni sırayı yalnızca ID dizisi olarak yazdır
const onDrop = () => {
  const api = lb.value?.ej2Instances;
  if (!api) return;

  // Güncel veri (yeniden sıralandıktan sonra)
  const newDataOrder = api.getDataList();

  // Yalnızca ID dizisi (fields.value = 'id' olduğu için)
  const idOrder = newDataOrder.map(item => item[api.fields.value]);

  console.log("Yeni sıra (id only):", idOrder);
};
</script>
```

---

## Nasıl Çalışır?

### Temel Özellikler

- **Sürükle-Bırak:** `:allowDragAndDrop="true"` tek başına, aynı listede öğeleri sürükleyip bırakmaya yeter.

- **Olay Yakalama:** `@drop` ile bırakma anını yakalıyoruz.

- **Güncel Veri:** `getDataList()` metodu *ListBox içindeki güncel dataSource'u* döndürür (sıra değiştiyse yeni sırayla).

- **Sadece ID:** `fields.value`'ı `id` olarak ayarladık. Böylece `newDataOrder.map(item => item[api.fields.value])` ile **yalnızca ID** dizisini elde edip performans kazanıyoruz.

### İpucu

Bu ID dizisini backend'e POST ederek sıralamayı kalıcılaştırabilirsiniz.

---

## Kaynaklar (Resmi Dokümantasyon)

### Drag & Drop (Vue ListBox)

`allowDragAndDrop`, `drag/dragStart/drop` olayları ve tek listede sürükle-bırak örneği:

https://ej2.syncfusion.com/vue/documentation/list-box/drag-and-drop

### ListBox API (JS)

`getDataList()` ve diğer metotların açıklaması:

https://ej2.syncfusion.com/documentation/api/list-box/

### Data Binding (Vue ListBox)

`fields.text` / `fields.value` eşlemeleri:

https://ej2.syncfusion.com/vue/documentation/list-box/data-binding

### Knowledge Base

`getDataList()` ile güncel veriyi alma kullanımı:

https://support.syncfusion.com/kb/article/11159/how-to-use-getdatalist-method-in-listbox
