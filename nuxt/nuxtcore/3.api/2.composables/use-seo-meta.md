---
title: 'useSeoMeta'
description: 'Composable useSeoMeta cho phép bạn định nghĩa các meta tags SEO của site dưới dạng một object phẳng với hỗ trợ TypeScript đầy đủ.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/unjs/unhead/blob/main/packages/vue/src/composables.ts
    size: xs
---

Điều này giúp bạn tránh các lỗi phổ biến, chẳng hạn như sử dụng `name` thay vì `property`, cũng như lỗi đánh máy - với hơn 100+ meta tags được typed đầy đủ.

::important
Đây là cách được khuyến nghị để thêm meta tags vào site của bạn vì nó an toàn XSS và có hỗ trợ TypeScript đầy đủ.
::

:read-more{to="/docs/getting-started/seo-meta"}

## Usage

```vue [app.vue]
<script setup lang="ts">
useSeoMeta({
  title: 'My Amazing Site',
  ogTitle: 'My Amazing Site',
  description: 'This is my amazing site, let me tell you all about it.',
  ogDescription: 'This is my amazing site, let me tell you all about it.',
  ogImage: 'https://example.com/image.png',
  twitterCard: 'summary_large_image',
})
</script>
```

Khi chèn các tags là reactive, bạn nên sử dụng syntax computed getter (`() => value`):

```vue [app.vue]
<script setup lang="ts">
const title = ref('My title')

useSeoMeta({
  title,
  description: () => `This is a description for the ${title.value} page`
})
</script>
```

## Parameters

Có hơn 100 parameters. Xem [danh sách đầy đủ các parameters trong source code](https://github.com/harlan-zw/zhead/blob/main/packages/zhead/src/metaFlat.ts#L1035).

:read-more{to="/docs/getting-started/seo-meta"}

## Performance

Trong hầu hết các trường hợp, SEO meta tags không cần reactive vì search engine robots chủ yếu scan initial page load.

Để có performance tốt hơn, bạn có thể wrap các calls `useSeoMeta` của bạn trong một điều kiện server-only khi các meta tags không cần reactive:

```vue [app.vue]
<script setup lang="ts">
if (import.meta.server) {
  // These meta tags will only be added during server-side rendering
  useSeoMeta({
    robots: 'index, follow',
    description: 'Static description that does not need reactivity',
    ogImage: 'https://example.com/image.png',
    // other static meta tags...
  })
}

const dynamicTitle = ref('My title')
// Only use reactive meta tags outside the condition when necessary
useSeoMeta({
  title: () => dynamicTitle.value,
  ogTitle: () => dynamicTitle.value,
})
</script>
```

Trước đây sử dụng composable [`useServerSeoMeta`](/docs/api/composables/use-server-seo-meta), nhưng nó đã bị deprecated để ủng hộ approach này.
