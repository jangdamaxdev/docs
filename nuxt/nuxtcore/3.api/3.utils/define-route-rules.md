---
title: 'defineRouteRules'
description: 'Định nghĩa quy tắc tuyến cho kết xuất hybrid ở cấp độ trang.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/pages/runtime/composables.ts
    size: xs
---

::read-more{to="/docs/guide/going-further/experimental-features#inlinerouterules" icon="i-lucide-star"}
Tính năng này là thử nghiệm và để sử dụng nó, bạn phải bật tùy chọn `experimental.inlineRouteRules` trong `nuxt.config` của mình.
::

## Usage

```vue [pages/index.vue]
<script setup lang="ts">
defineRouteRules({
  prerender: true
})
</script>

<template>
  <h1>Hello world!</h1>
</template>
```

Sẽ được dịch sang:

```ts [nuxt.config.ts]
export default defineNuxtConfig({
  routeRules: {
    '/': { prerender: true }
  }
})
```

::note
Khi chạy [`nuxt build`](/docs/api/commands/build), trang chủ sẽ được pre-rendered trong `.output/public/index.html` và được phục vụ tĩnh.
::

## Notes

- Một quy tắc được định nghĩa trong `~/pages/foo/bar.vue` sẽ được áp dụng cho các yêu cầu `/foo/bar`.
- Một quy tắc trong `~/pages/foo/[id].vue` sẽ được áp dụng cho các yêu cầu `/foo/**`.

Để kiểm soát nhiều hơn, chẳng hạn như nếu bạn đang sử dụng `path` hoặc `alias` tùy chỉnh được đặt trong [`definePageMeta`](/docs/api/utils/define-page-meta) của trang, bạn nên đặt `routeRules` trực tiếp trong `nuxt.config` của mình.

::read-more{to="/docs/guide/concepts/rendering#hybrid-rendering" icon="i-lucide-medal"}
Đọc thêm về `routeRules`.
::