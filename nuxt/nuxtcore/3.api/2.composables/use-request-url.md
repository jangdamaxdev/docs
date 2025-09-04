---
title: 'useRequestURL'
description: 'Truy cập URL request đến với composable useRequestURL.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/url.ts
    size: xs
---

`useRequestURL` là một hàm trợ giúp trả về một [URL object](https://developer.mozilla.org/en-US/docs/Web/API/URL/URL) hoạt động trên cả server-side và client-side.

::important
Khi sử dụng [Hybrid Rendering](/docs/guide/concepts/rendering#hybrid-rendering) với các chiến lược cache, tất cả headers request đến sẽ bị drop khi xử lý các responses cache qua [Nitro caching layer](https://nitro.build/guide/cache) (có nghĩa là `useRequestURL` sẽ trả về `localhost` cho `host`).

Bạn có thể định nghĩa option [`cache.varies`](https://nitro.build/guide/cache#options) để chỉ định headers sẽ được xem xét khi cache và serve responses, chẳng hạn như `host` và `x-forwarded-host` cho các môi trường multi-tenant.
::

::code-group

```vue [pages/about.vue]
<script setup lang="ts">
const url = useRequestURL()
</script>

<template>
  <p>URL is: {{ url }}</p>
  <p>Path is: {{ url.pathname }}</p>
</template>
```

```html [Result in development]
<p>URL is: http://localhost:3000/about</p>
<p>Path is: /about</p>
```

::

::tip{icon="i-simple-icons-mdnwebdocs" to="https://developer.mozilla.org/en-US/docs/Web/API/URL#instance_properties" target="_blank"}
Đọc về các thuộc tính instance URL trên tài liệu MDN.
::
