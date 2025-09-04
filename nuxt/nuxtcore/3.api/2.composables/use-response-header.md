---
title: "useResponseHeader"
description: "Sử dụng useResponseHeader để thiết lập một header response server."
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/ssr.ts
    size: xs
---

::important
Composable này khả dụng trong Nuxt v3.14+.
::

Bạn có thể sử dụng composable tích hợp [`useResponseHeader`](/docs/api/composables/use-response-header) để thiết lập bất kỳ header response server nào trong pages, components và plugins của bạn.

```ts
// Set a custom response header
const header = useResponseHeader('X-My-Header');
header.value = 'my-value';
```

## Example

Chúng ta có thể sử dụng `useResponseHeader` để dễ dàng thiết lập một header response trên cơ sở per-page.

```vue [pages/test.vue]
<script setup>
// pages/test.vue
const header = useResponseHeader('X-My-Header');
header.value = 'my-value';
</script>

<template>
  <h1>Test page with custom header</h1>
  <p>The response from the server for this "/test" page will have a custom "X-My-Header" header.</p>
</template>
```

Chúng ta có thể sử dụng `useResponseHeader` ví dụ trong Nuxt [middleware](/docs/guide/directory-structure/middleware) để thiết lập một header response cho tất cả pages.

```ts [middleware/my-header-middleware.ts]
export default defineNuxtRouteMiddleware((to, from) => {
  const header = useResponseHeader('X-My-Always-Header');
  header.value = `I'm Always here!`;
});

```
