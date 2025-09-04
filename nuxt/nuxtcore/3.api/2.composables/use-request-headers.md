---
title: "useRequestHeaders"
description: "Sử dụng useRequestHeaders để truy cập các headers request đến."
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/ssr.ts
    size: xs
---

Bạn có thể sử dụng composable tích hợp [`useRequestHeaders`](/docs/api/composables/use-request-headers) để truy cập các headers request đến trong pages, components và plugins của bạn.

```js
// Get all request headers
const headers = useRequestHeaders()

// Get only cookie request header
const headers = useRequestHeaders(['cookie'])
```

::tip
Trong browser, `useRequestHeaders` sẽ trả về một object rỗng.
::

## Example

Chúng ta có thể sử dụng `useRequestHeaders` để truy cập và proxy header `authorization` của request ban đầu cho bất kỳ yêu cầu internal nào trong tương lai trong quá trình SSR.

Ví dụ dưới đây thêm header request `authorization` vào một call `$fetch` isomorphic.

```vue [pages/some-page.vue]
<script setup lang="ts">
const { data } = await useFetch('/api/confidential', {
  headers: useRequestHeaders(['authorization'])
})
</script>
```
