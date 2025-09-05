---
title: 'preloadRouteComponents'
description: preloadRouteComponents allows you to manually preload individual pages in your Nuxt app.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/preload.ts
    size: xs
---

Việc preloading routes tải các components của một route nhất định mà người dùng có thể điều hướng đến trong tương lai. Điều này đảm bảo rằng các components có sẵn sớm hơn và ít có khả năng chặn việc điều hướng, cải thiện hiệu suất.

::tip{icon="i-lucide-rocket"}
Nuxt đã tự động preload các routes cần thiết nếu bạn đang sử dụng component `NuxtLink`.
::

:read-more{to="/docs/api/components/nuxt-link"}

## Example

Preload một route khi sử dụng `navigateTo`.

```ts
// chúng ta không await hàm async này, để tránh chặn việc render
// hàm setup của component này
preloadRouteComponents('/dashboard')

const submit = async () => {
  const results = await $fetch('/api/authentication')

  if (results.token) {
    await navigateTo('/dashboard')
  }
}
```

:read-more{to="/docs/api/utils/navigate-to"}

::note
Trên server, `preloadRouteComponents` sẽ không có hiệu lực.
::
