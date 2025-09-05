---
title: "onNuxtReady"
description: Composable onNuxtReady cho phép chạy một callback sau khi ứng dụng của bạn đã hoàn thành khởi tạo.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/ready.ts
    size: xs
---

::important
`onNuxtReady` chỉ chạy ở phía máy khách. :br
Nó lý tưởng để chạy mã không nên chặn việc kết xuất ban đầu của ứng dụng của bạn.
::

```ts [plugins/ready.client.ts]
export default defineNuxtPlugin(() => {
  onNuxtReady(async () => {
    const myAnalyticsLibrary = await import('my-big-analytics-library')
    // do something with myAnalyticsLibrary
  })
})
```

Nó 'an toàn' để chạy ngay cả sau khi ứng dụng của bạn đã khởi tạo. Trong trường hợp này, thì mã sẽ được đăng ký để chạy trong callback rảnh tiếp theo.