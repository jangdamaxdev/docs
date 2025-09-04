---
title: useRuntimeHook
description: Đăng ký một runtime hook trong ứng dụng Nuxt và đảm bảo nó được dispose đúng cách khi scope bị destroy.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/runtime-hook.ts
    size: xs
---

::important
Composable này khả dụng trong Nuxt v3.14+.
::

```ts [signature]
function useRuntimeHook<THookName extends keyof RuntimeNuxtHooks>(
  name: THookName,
  fn: RuntimeNuxtHooks[THookName] extends HookCallback ? RuntimeNuxtHooks[THookName] : never
): void
```

## Usage

### Parameters

- `name`: Tên của runtime hook để đăng ký. Bạn có thể xem danh sách đầy đủ của [runtime Nuxt hooks here](/docs/api/advanced/hooks#app-hooks-runtime).
- `fn`: Hàm callback để thực thi khi hook được trigger. Chữ ký hàm thay đổi dựa trên tên hook.

### Returns

Composable không trả về giá trị, nhưng nó tự động unregister hook khi scope của component bị destroy.

## Example

```vue twoslash [pages/index.vue]
<script setup lang="ts">
// Register a hook that runs every time a link is prefetched, but which will be
// automatically cleaned up (and not called again) when the component is unmounted
useRuntimeHook('link:prefetch', (link) => {
  console.log('Prefetching', link)
})
</script>
```
