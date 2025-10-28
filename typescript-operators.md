# TypeScript İşaretleri ve Operatörleri

Bu doküman, TypeScript'te sıklıkla kullanılan işaretlerin ve operatörlerin anlamlarını ve kullanım örneklerini içermektedir.

## 1. `=` (Atama Operatörü)

Bir değişkene değer atamak için kullanılır.

```typescript
// Basit atama
let name = "Ali"
const age = 25
let isActive = true

// Nesne atama
const user = {
  id: 1,
  name: "Ahmet"
}

// Dizi atama
const numbers = [1, 2, 3, 4, 5]
```

## 2. `:` (İki Nokta - Colon)

`:` işaretinin iki farklı kullanımı vardır:

### A. TypeScript Tür Belirtme (Type Annotation)

TypeScript'te bir değişkenin, parametrenin veya dönüş değerinin **türünü** belirtmek için kullanılır.

```typescript
// Değişken tür belirtme
let username: string = "Mehmet"
let count: number = 10
let isValid: boolean = true

// Fonksiyon parametresi ve dönüş türü
function greet(name: string): string {
  return `Merhaba, ${name}`
}

// Interface/Type'da özellik türü belirtme
interface User {
  id: number        // id özelliğinin TÜRÜ number
  name: string      // name özelliğinin TÜRÜ string
  email: string
  age?: number      // age opsiyonel ve TÜRÜ number
}

// Nesne literal türü
const config: { apiUrl: string; timeout: number } = {
  apiUrl: "https://api.example.com",
  timeout: 3000
}
```

### B. JavaScript Nesne Özelliği (Property: Value)

JavaScript'te **yeni bir nesne oluştururken** veya **fonksiyona nesne parametresi gönderirken** özellik adı ile değerini ayırmak için kullanılır. Bu, var olan bir nesneye değer ataması değil, nesne literal (nesne sabiti) oluşturma syntax'ıdır.

```typescript
// Nesne oluşturma - property: value
const user = {
  id: 1,              // "id" adında özellik, DEĞERI 1
  name: "Ali",        // "name" adında özellik, DEĞERI "Ali"
  age: 25             // "age" adında özellik, DEĞERI 25
}

// Fonksiyona nesne gönderme
grid.excelExport({
  dataSource: selectedRecords,    // dataSource özelliği: selectedRecords değişkeninin değeri
  fileName: "rapor.xlsx",         // fileName özelliği: "rapor.xlsx" string değeri
  hierarchyExportMode: "All"      // hierarchyExportMode özelliği: "All" değeri
})

// API çağrısında
fetch('/api/users', {
  method: 'POST',                 // method özelliği
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: userName,               // name özelliğine userName değişkenini ata
    email: userEmail              // email özelliğine userEmail değişkenini ata
  })
})

// Shorthand syntax - özellik adı ile değişken adı aynıysa
const name = "Ahmet"
const age = 30

const person = {
  name: name,     // Uzun hali
  age             // Kısa hali (name: name yerine sadece name)
}
```

### Fark Nedir?

```typescript
// TypeScript TÜR belirtme (sadece derleme zamanında, runtime'da yok)
let count: number = 10
//        ↑ Bu TypeScript - tür belirtiyor

// JavaScript nesne özelliği (runtime'da var)
const config = {
  timeout: 3000
//        ↑ Bu JavaScript - değer ataması yapıyor
}

// İkisi bir arada
const settings: { timeout: number } = {
  timeout: 3000
}
//              ↑ TypeScript tür         ↑ JavaScript değer ataması
```

## 3. `?` (Optional - Opsiyonel)

Bir özelliğin veya parametrenin zorunlu olmadığını belirtir.

```typescript
// Interface'de opsiyonel özellik
interface Product {
  id: number
  name: string
  description?: string // Zorunlu değil
  price?: number
}

// Fonksiyonda opsiyonel parametre
function createUser(name: string, age?: number) {
  if (age) {
    return `${name}, ${age} yaşında`
  }
  return name
}

createUser("Ali") // Geçerli
createUser("Ali", 30) // Geçerli

// Opsiyonel zincirleme (Optional Chaining)
const user = {
  profile: {
    address: {
      city: "İstanbul"
    }
  }
}

const city = user?.profile?.address?.city // Güvenli erişim
```

## 4. `?.` (Optional Chaining - Opsiyonel Zincirleme)

Bir nesnenin özelliğine güvenli bir şekilde erişmek için kullanılır. Eğer özellik undefined veya null ise hata vermez.

```typescript
interface User {
  name: string
  address?: {
    city?: string
    street?: string
  }
}

const user: User = { name: "Ayşe" }

// Optional chaining kullanımı
const city = user.address?.city // undefined döner, hata vermez
const street = user.address?.street // undefined döner

// Fonksiyon çağrısında
const result = someFunction?.() // Fonksiyon varsa çağrılır

// Dizi elemanına erişimde
const firstItem = items?.[0]
```

## 5. `!` (Non-null Assertion - Null Olmama İddiası)

TypeScript'e bir değerin kesinlikle null veya undefined olmadığını söyler. Dikkatli kullanılmalıdır!

```typescript
// Değişkenin kesinlikle değer içerdiğini belirtme
const element = document.getElementById("app")!
element.innerHTML = "Merhaba" // ! olmadan hata verirdi

// Nesne özelliğinde
interface User {
  name?: string
}

const user: User = { name: "Ali" }
const upperName = user.name!.toUpperCase() // name'in kesinlikle var olduğunu söylüyoruz

// Dikkat: Eğer gerçekten null/undefined ise runtime hatası verir!
```

## 6. `??` (Nullish Coalescing - Null Birleştirme)

Sol taraftaki değer null veya undefined ise sağ taraftaki değeri döndürür.

```typescript
// Temel kullanım
const value = null ?? "varsayılan" // "varsayılan"
const value2 = undefined ?? "varsayılan" // "varsayılan"
const value3 = "gerçek değer" ?? "varsayılan" // "gerçek değer"

// 0 veya false değerleri korunur (|| operatöründen farkı)
const count = 0 ?? 10 // 0 (|| ile 10 dönerdi)
const isActive = false ?? true // false (|| ile true dönerdi)

// Pratik kullanım
function getUserName(name?: string) {
  return name ?? "Misafir"
}

getUserName() // "Misafir"
getUserName("Ali") // "Ali"
```

## 7. `||` (Logical OR - Mantıksal VEYA)

Sol taraftaki değer falsy (false, 0, "", null, undefined, NaN) ise sağ taraftaki değeri döndürür.

```typescript
// Temel kullanım
const name = "" || "İsimsiz" // "İsimsiz"
const count = 0 || 10 // 10 (0 falsy)
const value = null || "varsayılan" // "varsayılan"

// Dikkat: ?? operatöründen farkı
const number = 0 || 100 // 100 (0 falsy kabul edilir)
const number2 = 0 ?? 100 // 0 (sadece null/undefined kontrolü)

// Mantıksal koşullarda
if (isAdmin || isModerator) {
  // Admin veya moderatör ise
}
```

## 8. `&&` (Logical AND - Mantıksal VE)

Sol taraftaki değer truthy ise sağ taraftaki değeri döndürür, değilse sol taraftakini döndürür.

```typescript
// Koşullu işlem
const user = { name: "Ali" }
const greeting = user && `Merhaba ${user.name}` // "Merhaba Ali"

// Kısa devre mantık
isLoggedIn && redirectToDashboard()

// Çoklu koşul
if (isActive && hasPermission && isVerified) {
  // Üç koşul da doğru ise
}

// React/Vue template'lerinde yaygın kullanım
const Component = () => {
  return (
    <div>
      {isLoading && <Spinner />}
      {!isLoading && data && <DataTable data={data} />}
    </div>
  )
}
```

## 9. `|` (Union Types - Birleşim Türleri)

Bir değişkenin birden fazla türden biri olabileceğini belirtir.

```typescript
// Basit union type
let value: string | number
value = "metin" // Geçerli
value = 123 // Geçerli

// Fonksiyon parametresi
function format(input: string | number): string {
  if (typeof input === "string") {
    return input.toUpperCase()
  }
  return input.toString()
}

// Literal union
type Status = "pending" | "approved" | "rejected"
let orderStatus: Status = "pending"

// Union type'lar interface'lerde
interface Success {
  status: "success"
  data: any
}

interface Error {
  status: "error"
  message: string
}

type ApiResponse = Success | Error
```

## 10. `&` (Intersection Types - Kesişim Türleri)

Birden fazla türü birleştirir. Tüm türlerin özelliklerini içerir.

```typescript
// İki interface'i birleştirme
interface Person {
  name: string
  age: number
}

interface Employee {
  employeeId: string
  department: string
}

type EmployeePerson = Person & Employee

const worker: EmployeePerson = {
  name: "Ahmet",
  age: 30,
  employeeId: "EMP001",
  department: "IT"
}

// Mixin pattern
type Timestamped = {
  createdAt: Date
  updatedAt: Date
}

type User = {
  id: number
  name: string
} & Timestamped
```

## 11. `as` (Type Assertion - Tür İddiası)

TypeScript'e bir değerin belirli bir tür olduğunu söyler.

```typescript
// Temel kullanım
const value: any = "Bu bir string"
const length = (value as string).length

// DOM elementlerinde
const input = document.getElementById("email") as HTMLInputElement
input.value = "test@example.com"

// Union type'dan spesifik türe
type Response = { success: true; data: any } | { success: false; error: string }

function handleResponse(response: Response) {
  if (response.success) {
    const data = (response as { success: true; data: any }).data
  }
}

// const assertion
const config = {
  apiUrl: "https://api.example.com",
  timeout: 3000
} as const // Tüm özellikler readonly olur
```

## 12. `...` (Spread/Rest Operator - Yayma/Toplama Operatörü)

### Spread (Yayma) - Dizi veya nesneyi açar

```typescript
// Dizi spread
const arr1 = [1, 2, 3]
const arr2 = [4, 5, 6]
const combined = [...arr1, ...arr2] // [1, 2, 3, 4, 5, 6]

// Nesne spread
const user = { name: "Ali", age: 25 }
const updatedUser = { ...user, age: 26 } // { name: "Ali", age: 26 }

// Fonksiyon argümanlarında
const numbers = [1, 2, 3]
Math.max(...numbers) // 3
```

### Rest (Toplama) - Birden fazla değeri tek bir değişkende toplar

```typescript
// Fonksiyon parametrelerinde
function sum(...numbers: number[]): number {
  return numbers.reduce((total, n) => total + n, 0)
}

sum(1, 2, 3, 4, 5) // 15

// Destructuring'de
const [first, second, ...rest] = [1, 2, 3, 4, 5]
// first: 1, second: 2, rest: [3, 4, 5]

const { name, age, ...otherProps } = { name: "Ali", age: 25, city: "İstanbul", job: "Developer" }
// name: "Ali", age: 25, otherProps: { city: "İstanbul", job: "Developer" }
```

## 13. `=>` (Arrow Function - Ok Fonksiyonu)

Kısa ve özlü fonksiyon yazımı sağlar.

```typescript
// Temel kullanım
const greet = (name: string) => {
  return `Merhaba, ${name}`
}

// Tek satırlık return (implicit return)
const double = (n: number) => n * 2

// Parametresiz
const getRandomNumber = () => Math.random()

// Nesne döndürme (parantez gerekli)
const createUser = (name: string) => ({ name, createdAt: new Date() })

// Tür belirtme
const add: (a: number, b: number) => number = (a, b) => a + b

// Array metodlarında
const numbers = [1, 2, 3, 4, 5]
const doubled = numbers.map(n => n * 2)
const evens = numbers.filter(n => n % 2 === 0)
```

## Özet Tablo

| İşaret | Adı | Kullanım Alanı | Örnek |
|--------|-----|----------------|-------|
| `=` | Atama | Değer atama | `let x = 5` |
| `:` | Tür belirteci | Tür tanımlama | `let x: number` |
| `?` | Opsiyonel | Zorunlu olmayan alan | `age?: number` |
| `?.` | Optional chaining | Güvenli erişim | `user?.address?.city` |
| `!` | Non-null assertion | Null değil iddiası | `element!.innerHTML` |
| `??` | Nullish coalescing | Null/undefined kontrolü | `value ?? "default"` |
| `\|\|` | Logical OR | Falsy kontrolü | `name \|\| "Guest"` |
| `&&` | Logical AND | Truthy kontrolü | `isActive && doSomething()` |
| `\|` | Union type | Birleşim türü | `string \| number` |
| `&` | Intersection type | Kesişim türü | `Person & Employee` |
| `as` | Type assertion | Tür iddiası | `value as string` |
| `...` | Spread/Rest | Yayma/Toplama | `[...arr]` veya `...args` |
| `=>` | Arrow function | Fonksiyon | `(x) => x * 2` |

## İyi Pratikler

1. **`!` operatörünü dikkatli kullanın** - Sadece değerin kesinlikle var olduğundan emin olduğunuzda kullanın
2. **`??` vs `||`** - Sadece null/undefined kontrolü için `??`, falsy değerler için `||` kullanın
3. **Union types temiz tutun** - Çok fazla union yerine daha spesifik tipler oluşturun
4. **Type assertion yerine type guards** - Mümkünse type assertion yerine type guard fonksiyonları kullanın
5. **Optional chaining tercih edin** - Uzun if kontrolleri yerine `?.` kullanın

## Kaynaklar

- [TypeScript Resmi Dokümantasyonu](https://www.typescriptlang.org/docs/)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)
