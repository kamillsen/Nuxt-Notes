# 🧠 Kısa Not: `ref` Nedir? (Nuxt / Vue 3)

- `ref`, **Vue 3’ün reaktif sisteminin** temel parçasıdır; Nuxt projelerinde de aynı şekilde kullanılır.  
- **Amacı:** Bir değeri **reaktif** (değişimi izlenebilir) hâle getirmek.  
- **Tanım:**  
  ```ts
  const count = ref(0)
  ```
- **Erişim:**  
  - JavaScript içinde: `count.value`  
  - Template içinde: `{{ count }}` (otomatik `.value` açılır)
- Değer değiştiğinde, Vue **otomatik olarak DOM’u günceller**.
- `ref` ayrıca **DOM elemanlarına referans** almak için de kullanılabilir:  
  ```vue
  <input ref="myInput" />
  ```
- Nuxt’ta `ref` **yalnızca bileşen içinde** tanımlanmalıdır (SSR uyumu için).  
- Global durum yönetimi gerekiyorsa `useState()` tercih edilir.
