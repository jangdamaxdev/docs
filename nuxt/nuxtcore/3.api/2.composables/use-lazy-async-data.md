---
title: useLazyAsyncData
description: Wrapper này xung quanh useAsyncData kích hoạt điều hướng ngay lập tức.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/asyncData.ts
    size: xs
---

## Description

Theo mặc định, [`useAsyncData`](/docs/api/composables/use-async-data) chặn điều hướng cho đến khi trình xử lý async của nó được giải quyết. `useLazyAsyncData` cung cấp một wrapper xung quanh [`useAsyncData`](/docs/api/composables/use-async-data) kích hoạt điều hướng trước khi trình xử lý được giải quyết bằng cách đặt tùy chọn `lazy` thành `true`.

::note
`useLazyAsyncData` has the same signature as [`useAsyncData`](/docs/api/composables/use-async-data).
::

:read-more{to="/docs/api/composables/use-async-data"}

## Example

```vue [pages/index.vue]
<script setup lang="ts">
/* Điều hướng sẽ xảy ra trước khi fetching hoàn tất.
  Xử lý trạng thái 'pending' và 'error' trực tiếp trong template của component
*/
const { status, data: count } = await useLazyAsyncData('count', () => $fetch('/api/count'))

watch(count, (newCount) => {
  // Vì count có thể bắt đầu là null, bạn sẽ không có quyền truy cập
  // vào nội dung của nó ngay lập tức, nhưng bạn có thể watch nó.
})
</script>

<template>
  <div>
    {{ status === 'pending' ? 'Đang tải' : count }}
  </div>
</template>
```

::warning
`useLazyAsyncData` là một tên hàm được bảo lưu được biến đổi bởi compiler, vì vậy bạn không nên đặt tên hàm của mình là `useLazyAsyncData`.
::

:read-more{to="/docs/getting-started/data-fetching"}
