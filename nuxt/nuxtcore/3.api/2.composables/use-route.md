---
title: "useRoute"
description: Composable useRoute trả về route hiện tại.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/router.ts
    size: xs
---

::note
Trong template của một Vue component, bạn có thể truy cập route bằng `$route`.
::

## Example

Trong ví dụ sau, chúng ta gọi một API qua [`useFetch`](/docs/api/composables/use-fetch) sử dụng một tham số trang động - `slug` - làm một phần của URL.

```html [~/pages/[slug\\].vue]
<script setup lang="ts">
const route = useRoute()
const { data: mountain } = await useFetch(`/api/mountains/${route.params.slug}`)
</script>

<template>
  <div>
    <h1>{{ mountain.title }}</h1>
    <p>{{ mountain.description }}</p>
  </div>
</template>
```

Nếu bạn cần truy cập các tham số query của route (ví dụ `example` trong path `/test?example=true`), thì bạn có thể sử dụng `useRoute().query` thay vì `useRoute().params`.

## API

Ngoài các tham số động và tham số query, `useRoute()` cũng cung cấp các computed references sau liên quan đến route hiện tại:

- `fullPath`: URL được encode liên quan đến route hiện tại chứa path, query và hash
- `hash`: phần hash được decode của URL bắt đầu với #
- `query`: truy cập tham số query của route
- `matched`: mảng các route đã match được normalized với vị trí route hiện tại
- `meta`: dữ liệu tùy chỉnh được gắn vào record
- `name`: tên duy nhất cho route record
- `path`: phần pathname được encode của URL
- `redirectedFrom`: vị trí route đã cố gắng truy cập trước khi kết thúc ở vị trí route hiện tại

::note
Browsers không gửi [URL fragments](https://url.spec.whatwg.org/#concept-url-fragment) (ví dụ `#foo`) khi thực hiện requests. Vì vậy, sử dụng `route.fullPath` trong template của bạn có thể trigger các vấn đề hydration vì điều này sẽ bao gồm fragment trên client nhưng không phải trên server.
::

:read-more{icon="i-simple-icons-vuedotjs" to="https://router.vuejs.org/api/type-aliases/RouteLocationNormalizedLoaded.html"}
