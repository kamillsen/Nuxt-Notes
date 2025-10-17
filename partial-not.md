# 🧩 Kısa Not: `Partial<T>` Nedir? (TypeScript)

- **Tanım:** `Partial<T>`, `T` tipindeki **tüm özellikleri opsiyonel** (`?`) yapan yardımcı tiptir.
- **Kullanım amacı:** *Patch* / *update* senaryoları, form/ayar nesnelerinde **kısmi** veri taşımak.

## Nasıl Çalışır?
- Her `K in keyof T` için özellik `T[K] | undefined` olur **ve** özellik **bulunmayabilir** (opsiyonel).
- **Derin** değildir; yalnızca **ilk seviye** özellikleri opsiyonel yapar.
- **Birlik tiplerinde (union)** dağıtıcıdır: `Partial<A | B> -> Partial<A> | Partial<B>`.

## Örnek
```ts
interface User {
  id: number
  name: string
  email: string
  profile?: { bio: string; avatar: string } // zaten opsiyonel
}

function updateUser(id: number, patch: Partial<User>) {
  // id dışındaki alanlardan herhangi birkaçı gelebilir
  // örn: updateUser(1, { name: 'Ada' });
}
```

## Dikkat
- Derin opsiyonellik gerekirse **`DeepPartial<T>`** gibi bir yardımcı kurun veya bir kütüphane kullanın.
- Tüm özellikleri tekrar zorunlu yapmak için **`Required<T>`**.
- Sadece bazı alanları opsiyonel/zorunlu yapmak için **`Pick<T, K>`**, **`Omit<T, K>`** ile birlikte kullanın.
- Salt-okunur alanlar için **`Readonly<T>`**; `Partial` bunları opsiyonel yapar ama salt-okunurluğu kaldırmaz.

## Kısa Özet
> `Partial<T>` = *T’nin “kısmi” versiyonu.* Kısmi güncellemeler ve esnek API girişleri için idealdir.
