## `!!()` Kullanımı (TypeScript)

### 🔹 Amaç

`!!` (double bang) operatörü, bir ifadeyi **boolean** (`true` / `false`)
türüne dönüştürmek için kullanılır.

``` ts
return !!(ifade);
```

Bu ifade: - `ifade` **truthy** ise `true` döner.\
- `ifade` **falsy** ise `false` döner.

------------------------------------------------------------------------

### 🔹 Nasıl Çalışır?

1.  İlk `!` (ünlem) ifadeyi boolean'a çevirir ve tersini alır.\
2.  İkinci `!` tekrar tersleyerek **salt boolean** değeri elde eder.

------------------------------------------------------------------------

### 🔹 Örnekler

``` ts
!!"merhaba"    // true
!!""           // false
!!123          // true
!!0            // false
!![]           // true
!!{}           // true
!!null         // false
!!undefined    // false
!!NaN          // false
```

------------------------------------------------------------------------

### 🔹 Kullanım Alanları

-   Fonksiyonlardan net boolean döndürmek için:

    ``` ts
    function isNonEmpty(s?: string): boolean {
      return !!s;
    }
    ```

-   Filtreleme işlemlerinde:

    ``` ts
    ['a', '', 'b'].filter(Boolean); // ['a', 'b']
    ```

------------------------------------------------------------------------

### 🔹 TypeScript Tür Desteği

`!!expr` ifadesinin türü **`boolean`** olur.\
Alternatif olarak şu da kullanılabilir:

``` ts
Boolean(expr);
```

------------------------------------------------------------------------

### ⚠️ Dikkat Edilmesi Gerekenler

-   `0` ve `""` gibi **geçerli ama falsy** değerler yanlışlıkla `false`
    sayılabilir.\
-   Daha açık kontroller bazen daha iyi olur:

``` ts
value != null        // null ve undefined kontrolü
s.trim().length > 0  // boş olmayan string
Array.isArray(a) && a.length > 0
```

> **Not:** `!!promise` her zaman `true` olur (çünkü Promise bir
> objedir), bu nedenle "tamamlandı mı?" kontrolü için uygun değildir.

------------------------------------------------------------------------

### 🔹 Özet

`return !!(ifade)`\
➡️ ifadeyi açıkça `true` veya `false`'a indirger.\
✅ Okunabilirliği artırır.\
⚠️ "Falsy" değerlerin anlamlı olduğu durumlarda dikkatli
kullanılmalıdır.
