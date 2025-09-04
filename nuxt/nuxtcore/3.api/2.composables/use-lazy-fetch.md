---
title: 'useLazyFetch'
description: Wrapper này xung quanh useFetch kích hoạt điều hướng ngay lập tức.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/fetch.ts
    size: xs
---

## Description

Theo mặc định, [`useFetch`](/docs/api/composables/use-fetch) chặn điều hướng cho đến khi trình xử lý async của nó được giải quyết. `useLazyFetch` cung cấp một wrapper xung quanh [`useFetch`](/docs/api/composables/use-fetch) kích hoạt điều hướng trước khi trình xử lý được giải quyết bằng cách đặt tùy chọn `lazy` thành `true`.

::note
`useLazyFetch` has the same signature as [`useFetch`](/docs/api/composables/use-fetch).
::

::note
Việc awaiting `useLazyFetch` ở chế độ này chỉ đảm bảo cuộc gọi được khởi tạo. Trên điều hướng phía client, dữ liệu có thể không khả dụng ngay lập tức, và bạn nên đảm bảo xử lý trạng thái pending trong ứng dụng của mình.
::

:read-more{to="/docs/api/composables/use-fetch"}

## Example

```vue [pages/index.vue]
<script setup lang="ts">
/* Điều hướng sẽ xảy ra trước khi fetching hoàn tất.
 * Xử lý trạng thái 'pending' và 'error' trực tiếp trong template của component
 */
const { status, data: posts } = await useLazyFetch('/api/posts')
watch(posts, (newPosts) => {
  // Vì posts có thể bắt đầu là null, bạn sẽ không có quyền truy cập
  // vào nội dung của nó ngay lập tức, nhưng bạn có thể watch nó.
})
</script>

<template>
  <div v-if="status === 'pending'">
    Đang tải ...
  </div>
  <div v-else>
    <div v-for="post in posts">
      <!-- do something -->
    </div>
  </div>
</template>
```

::note
`useLazyFetch` là một tên hàm được bảo lưu được biến đổi bởi compiler, vì vậy bạn không nên đặt tên hàm của mình là `useLazyFetch`.
::

:read-more{to="/docs/getting-started/data-fetching"}
