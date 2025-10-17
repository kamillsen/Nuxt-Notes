# Syncfusion ImageEditor API Dokümantasyonu

## 🎯 Genel Bakış

Bu doküman, Syncfusion ImageEditor component'inin `ej2Instances` property'sinin içinde bulunan tüm fonksiyonları ve kullanımlarını açıklar.

---

## 📚 ej2Instances API Metodları

```typescript
ej2Instances: {
  // Temel İşlemler
  reset: Function,              // Editörü sıfırla
  getImageData: Function,       // Resim verisini al
  setImageData: Function,       // Resim verisini ayarla
  
  // Düzenleme İşlemleri
  crop: Function,               // Resmi kırp
  rotate: Function,             // Resmi döndür (90°, 180°, 270°)
  flip: Function,               // Resmi çevir (yatay/dikey)
  zoom: Function,               // Yakınlaştır/uzaklaştır
  
  // Görsel Efektler
  filter: Function,             // Filtre uygula (parlaklık, kontrast, vb.)
  brightness: Function,         // Parlaklık ayarla
  contrast: Function,          // Kontrast ayarla
  saturation: Function,        // Doygunluk ayarla
  
  // Çizim ve Metin
  draw: Function,               // Çizim yap
  text: Function,               // Metin ekle
  shape: Function,              // Şekil ekle (dikdörtgen, daire, vb.)
  
  // Geçmiş İşlemleri
  undo: Function,               // Geri al
  redo: Function,               // İleri al
  clearHistory: Function,       // Geçmişi temizle
  
  // Dosya İşlemleri
  open: Function,               // Dosya aç
  save: Function,               // Dosya kaydet
  export: Function,             // Dışa aktar
  
  // Boyut ve Pozisyon
  resize: Function,             // Boyutlandır
  move: Function,               // Taşı
  select: Function,             // Seç
  
  // Araçlar
  selectTool: Function,         // Araç seç
  freehandDraw: Function,       // Serbest çizim
  lineDraw: Function,           // Çizgi çiz
  arrowDraw: Function,          // Ok çiz
}
```

---

## 🎨 Kullanım Örnekleri

### Temel İşlemler

```typescript
// Editörü sıfırla
imageEditorObj.value.ej2Instances.reset()

// Resim verisini al
const imageData = imageEditorObj.value.ej2Instances.getImageData()

// Resim verisini ayarla
imageEditorObj.value.ej2Instances.setImageData(imageData)
```

### Düzenleme İşlemleri

```typescript
// Resmi kırp
imageEditorObj.value.ej2Instances.crop()

// Resmi 90° döndür
imageEditorObj.value.ej2Instances.rotate(90)

// Resmi yatay çevir
imageEditorObj.value.ej2Instances.flip('horizontal')

// Resmi dikey çevir
imageEditorObj.value.ej2Instances.flip('vertical')

// Yakınlaştır
imageEditorObj.value.ej2Instances.zoom(1.5)

// Uzaklaştır
imageEditorObj.value.ej2Instances.zoom(0.5)
```

### Görsel Efektler

```typescript
// Filtre uygula
imageEditorObj.value.ej2Instances.filter('brightness', 50)
imageEditorObj.value.ej2Instances.filter('contrast', 30)
imageEditorObj.value.ej2Instances.filter('saturation', 40)

// Parlaklık ayarla
imageEditorObj.value.ej2Instances.brightness(50)

// Kontrast ayarla
imageEditorObj.value.ej2Instances.contrast(30)

// Doygunluk ayarla
imageEditorObj.value.ej2Instances.saturation(40)
```

### Çizim ve Metin

```typescript
// Çizim yap
imageEditorObj.value.ej2Instances.draw('freehand')

// Metin ekle
imageEditorObj.value.ej2Instances.text('Merhaba', {
  x: 100,
  y: 100,
  fontSize: 20,
  color: '#000000'
})

// Şekil ekle
imageEditorObj.value.ej2Instances.shape('rectangle', {
  x: 50,
  y: 50,
  width: 100,
  height: 80
})
```

### Geçmiş İşlemleri

```typescript
// Geri al
imageEditorObj.value.ej2Instances.undo()

// İleri al
imageEditorObj.value.ej2Instances.redo()

// Geçmişi temizle
imageEditorObj.value.ej2Instances.clearHistory()
```

### Dosya İşlemleri

```typescript
// Dosya aç
imageEditorObj.value.ej2Instances.open(file)

// Dosya kaydet
imageEditorObj.value.ej2Instances.save('image.png')

// Dışa aktar
imageEditorObj.value.ej2Instances.export('image.jpg')
```

### Boyut ve Pozisyon

```typescript
// Boyutlandır
imageEditorObj.value.ej2Instances.resize(800, 600)

// Taşı
imageEditorObj.value.ej2Instances.move(100, 100)

// Seç
imageEditorObj.value.ej2Instances.select(50, 50, 200, 200)
```

### Araçlar

```typescript
// Araç seç
imageEditorObj.value.ej2Instances.selectTool('crop')
imageEditorObj.value.ej2Instances.selectTool('rotate')
imageEditorObj.value.ej2Instances.selectTool('text')

// Serbest çizim
imageEditorObj.value.ej2Instances.freehandDraw()

// Çizgi çiz
imageEditorObj.value.ej2Instances.lineDraw()

// Ok çiz
imageEditorObj.value.ej2Instances.arrowDraw()
```

---

## 🎯 Pratik Örnekler

### Resim Sıfırlama

```typescript
function resetImageEditor() {
  const imageEditor = imageEditorObj.value?.ej2Instances
  if (imageEditor) {
    imageEditor.reset()
    toast.add({
      title: 'Sıfırlandı!',
      description: 'Resim editörü başlangıç durumuna sıfırlandı.',
      color: 'success'
    })
  }
}
```

### Resim İndirme

```typescript
function downloadImage() {
  const imageEditor = imageEditorObj.value?.ej2Instances
  if (!imageEditor) {
    toast.add({
      title: 'Hata!',
      description: 'Image Editor bulunamadı.',
      color: 'error'
    })
    return
  }

  try {
    const imageData = imageEditor.getImageData()
    const canvas = document.createElement('canvas')
    canvas.width = imageData.width
    canvas.height = imageData.height
    const context = canvas.getContext('2d')
    
    if (!context) {
      throw new Error('Canvas context oluşturulamadı')
    }
    
    context.putImageData(imageData, 0, 0)
    const base64String = canvas.toDataURL('image/png')
    
    const link = document.createElement('a')
    link.href = base64String
    link.download = `ruhsat-${Date.now()}.png`
    
    document.body.appendChild(link)
    link.click()
    document.body.removeChild(link)
    
    toast.add({
      title: 'Başarılı!',
      description: 'Resim başarıyla indirildi.',
      color: 'success'
    })
  } catch (error) {
    toast.add({
      title: 'Hata!',
      description: 'Resim indirilirken bir hata oluştu.',
      color: 'error'
    })
  }
}
```

### Resim Düzenleme

```typescript
// Resmi 90° döndür
function rotateImage() {
  const imageEditor = imageEditorObj.value?.ej2Instances
  if (imageEditor) {
    imageEditor.rotate(90)
  }
}

// Resmi kırp
function cropImage() {
  const imageEditor = imageEditorObj.value?.ej2Instances
  if (imageEditor) {
    imageEditor.crop()
  }
}

// Metin ekle
function addText() {
  const imageEditor = imageEditorObj.value?.ej2Instances
  if (imageEditor) {
    imageEditor.text('Ruhsat No: 12345', {
      x: 100,
      y: 100,
      fontSize: 16,
      color: '#000000'
    })
  }
}
```

---

## 📚 İlgili Dosyalar

- `app/composables/vehicles/useVehicleImageEditor.ts` - ej2Instances kullanımı
- `app/components/vehicles/VehicleImageUpload.vue` - Template binding
- `app/pages/vehicles/create.vue` - Kullanım örneği

---

*Bu doküman Syncfusion ImageEditor ej2Instances API'sini açıklamaktadır. Güncellenme tarihi: 2024*
