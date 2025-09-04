---
title: 'useRequestEvent'
description: 'Truy cập sự kiện request đến với composable useRequestEvent.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/ssr.ts
    size: xs
---

Trong [Nuxt context](/docs/guide/going-further/nuxt-app#the-nuxt-context) bạn có thể sử dụng `useRequestEvent` để truy cập request đến.

```ts
// Get underlying request event
const event = useRequestEvent()

// Get the URL
const url = event?.path
```

::tip
Trong browser, `useRequestEvent` sẽ trả về `undefined`.
::
