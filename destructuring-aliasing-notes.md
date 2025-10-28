# Object Destructuring - Yeniden Adlandırma

## Temel Sözdizimi

```javascript
const { özellikAdı: yeniDeğişkenAdı } = obje
```

---

## MDN Örneği

```javascript
const o = { p: 42, q: true };
const { p: foo, q: bar } = o;

console.log(foo); // 42
console.log(bar); // true
```

- `p` property'sini `foo` değişkenine ata
- `q` property'sini `bar` değişkenine ata

---

## Projemizdeki Kullanım

```typescript
// useVehicleForm.ts
return {
  schema: createVehicleRequestSchema  // createVehicleRequestSchema'yı "schema" adıyla dışarı ver
}

// create.vue
const {
  schema: createVehicleRequestSchema  // "schema"yı createVehicleRequestSchema adıyla al
} = useVehicleForm()

<UForm :schema="createVehicleRequestSchema" />
```

---

## 🎯 EN ÖNEMLİ: Return vs Const - Yön Farkı

### Return → SAĞ taraf kaynak

```typescript
return {
  schema: createVehicleRequestSchema
  //  ↑       ↑
  // YENİ   KAYNAK
}
```
"createVehicleRequestSchema'yı schema adıyla dışarı ver" (Sağdan sola ←)

---

### Const → SOL taraf kaynak

```typescript
const {
  schema: createVehicleRequestSchema
  //  ↑       ↑
  // KAYNAK YENİ
} = useVehicleForm()
```
"schema'yı createVehicleRequestSchema adıyla al" (Soldan sağa →)

---

### Yan Yana Karşılaştırma

```typescript
// RETURN (Sağdan Sola ←)
const myData = "test"
return {
  data: myData  // myData → data olarak dışarı ver
//  ↑     ↑
// hedef kaynak
}

// CONST (Soldan Sağa →)
const {
  data: myData  // data → myData olarak al
//  ↑     ↑
// kaynak hedef
} = someFunction()
```

---

### Görsel Şema

```
RETURN: { hedefİsim: kaynakDeğişken }  ← SAĞDAN SOLA
CONST:  { kaynakProperty: hedefDeğişken }  → SOLDAN SAĞA
```

**Neden ters?**
- Return ile değeri DIŞARI veriyorsun
- Const ile değeri GERİ alıyorsun
- İki işlem birbirinin tersi 🔄

---

## Yaygın Hata

```typescript
// ❌ YANLIŞ: "createVehicleRequestSchema'yı schema olarak kullanacağım"
// ✅ DOĞRU: "schema'yı createVehicleRequestSchema olarak kullanacağım"
const { schema: createVehicleRequestSchema } = useVehicleForm()
```

---

## Hatırlatma Kuralı

- **Return:** "Bu değişkeni → şu isimle dışarı ver" (sağdan sola)
- **Const:** "Şu property'yi → bu isimle al" (soldan sağa)

---

## Kaynaklar

- **MDN:** https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment
- **JavaScript.info (TR):** https://tr.javascript.info/destructuring-assignment
