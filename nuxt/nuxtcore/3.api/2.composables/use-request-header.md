---
title: "useRequestHeader"
description: "Sử dụng useRequestHeader để truy cập một header request đến nhất định."
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/ssr.ts
    size: xs
---

Bạn có thể sử dụng composable tích hợp [`useRequestHeader`](/docs/api/composables/use-request-header) để truy cập bất kỳ header request đến nào trong pages, components và plugins của bạn.

```ts
// Get the authorization request header
const authorization = useRequestHeader('authorization')
```

::tip
Trong browser, `useRequestHeader` sẽ trả về `undefined`.
::

## Example

Chúng ta có thể sử dụng `useRequestHeader` để dễ dàng xác định xem một user có được ủy quyền hay không.

Ví dụ dưới đây đọc header request `authorization` để tìm hiểu xem một người có thể truy cập tài nguyên bị hạn chế hay không.

```ts [middleware/authorized-only.ts]
export default defineNuxtRouteMiddleware((to, from) => {
  if (!useRequestHeader('authorization')) {
    return navigateTo('/not-authorized')
  }
})
```
