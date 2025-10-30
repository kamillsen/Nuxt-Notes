# Component Tasarım Notları

## İptal Butonu

```ts
<UButton
  icon="i-lucide-x"
  color="neutral"
  variant="soft"
  @click="handleCancel"
>
  İptal
</UButton>
```

**Özellikler:**
- `icon="i-lucide-x"` - X ikonu (kapatma/iptal için)
- `color="neutral"` - Nötr renk (gri tonları)
- `variant="soft"` - Yumuşak arka plan (bg-elevated hover:bg-accented/75)
- `@click="handleCancel"` - Tıklama eventi
- Metin: İptal

**Konum:** `app/pages/organizations/create.vue:38-45`
