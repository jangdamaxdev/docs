---
title: 'useServerSeoMeta'
description: 'Composable useServerSeoMeta cho phép bạn định nghĩa các meta tags SEO của site dưới dạng một object phẳng với hỗ trợ TypeScript đầy đủ.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/unjs/unhead/blob/main/packages/vue/src/composables.ts
    size: xs
---

Giống như [`useSeoMeta`](/docs/api/composables/use-seo-meta), composable `useServerSeoMeta` cho phép bạn định nghĩa các meta tags SEO của site dưới dạng một object phẳng với hỗ trợ TypeScript đầy đủ.

:read-more{to="/docs/api/composables/use-seo-meta"}

Trong hầu hết các trường hợp, meta không cần reactive vì robots sẽ chỉ scan initial load. Vì vậy chúng tôi khuyến nghị sử dụng [`useServerSeoMeta`](/docs/api/composables/use-server-seo-meta) làm utility tập trung vào performance sẽ không làm gì (hoặc trả về một object `head`) trên client.

```vue [app.vue]
<script setup lang="ts">
useServerSeoMeta({
  robots: 'index, follow'
})
</script>
```

Parameters chính xác giống như với [`useSeoMeta`](/docs/api/composables/use-seo-meta)

:read-more{to="/docs/getting-started/seo-meta"}
