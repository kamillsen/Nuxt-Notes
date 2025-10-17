# 🧠 TypeScript'te Değişken Tanımlama: `var`, `let`, `const`

TypeScript’te **değişken tanımlamak** için 3 kelime kullanılır:  
`var`, `let`, `const`  
Bunlar birbirine benzer görünür ama **farklı davranırlar.**

---

## 🔹 1. `var`

**Eski yöntem**dir (ES5 öncesi JavaScript’ten gelir).  
**Fonksiyon kapsamlıdır (function-scoped)** → Yani `{}` bloklarını umursamaz.  
Ayrıca **tekrar tanımlanabilir** ve **yeniden atanabilir.**

### 🧩 Örnek:
```ts
var x = 10
if (true) {
  var x = 20 // aynı değişken aslında
}
console.log(x) // 20 (blok dışına taşar!)
```

### 📘 Özellikleri:
- `var` **blok** değil, **fonksiyon** içinde yaşar.  
- Tanımlamadan önce bile kullanılabilir (`undefined` olur).  
- Günümüzde **artık kullanılmaz**. Modern kodlarda **kullanma!**

---

## 🔹 2. `let`

**Modern ve güvenli değişken tanımıdır.**  
**Blok kapsamlıdır (block-scoped)** → Sadece tanımlandığı `{}` içinde geçerlidir.  
**Yeniden atanabilir**, ama **tekrar tanımlanamaz.**

### 🧩 Örnek:
```ts
let count = 1
count = 2 // ✅ yeniden atayabilirsin

if (true) {
  let count = 3 // bu farklı bir count (blok içi)
  console.log(count) // 3
}
console.log(count) // 2
```

### 📘 Özellikleri:
- Tanımlanmadan önce kullanılamaz (`TDZ` → Temporal Dead Zone).  
- Genellikle **değeri değişecek** şeyler için kullanılır (örn. sayaç, durum, döngü).  
- Modern JS ve TS’te **varsayılan seçim** budur.

---

## 🔹 3. `const`

**Sabit (constant)** değerler için kullanılır.  
Bir kez atandıktan sonra **yeniden atanamaz.**

### 🧩 Örnek:
```ts
const name = "Ada"
name = "Grace" // ❌ Hata! const değiştirilemez
```

Ama dikkat! Eğer `const` bir **nesne** veya **dizi** tutuyorsa,  
**içindekiler değişebilir**, sadece referans sabittir 👇

```ts
const user = { name: "Ada" }
user.name = "Grace" // ✅ olur
user = { name: "Marie" } // ❌ olmaz (referansı değiştirmeye çalıştın)
```

### 📘 Özellikleri:
- **Blok kapsamlıdır.**
- **Yeniden atanamaz.**
- **İçeriği (objelerde)** değişebilir.  
- Sabit, değişmeyecek veriler için kullanılır.  

---

## 🎯 Kısa Özet Tablo

| Özellik / Anahtar | `var` | `let` | `const` |
|--------------------|--------|--------|----------|
| Yeniden atama | ✅ | ✅ | ❌ |
| Yeniden tanımlama | ✅ | ❌ | ❌ |
| Kapsam | Fonksiyon | Blok | Blok |
| Tanımlanmadan önce erişim | ✅ (undefined) | ❌ (TDZ) | ❌ (TDZ) |
| Modern kullanım | ❌ (kullanma) | ✅ | ✅ |

---

## 💬 Basit Hatırlatma:

> 🟢 `let` → Değişecek şeyler  
> 🔵 `const` → Sabit kalacak şeyler  
> 🔴 `var` → Artık geçmişte kaldı 🚫
