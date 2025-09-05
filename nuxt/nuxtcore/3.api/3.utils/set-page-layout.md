---
title: 'setPageLayout'
description: setPageLayout allows you to dynamically change the layout of a page.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/router.ts
    size: xs
---

::important
`setPageLayout` cho phép bạn thay đổi động layout của một trang. Nó dựa vào việc truy cập Nuxt context và do đó chỉ có thể được gọi trong [Nuxt context](/docs/guide/going-further/nuxt-app#the-nuxt-context).
::

```ts [middleware/custom-layout.ts]
export default defineNuxtRouteMiddleware((to) => {
  // Đặt layout trên route bạn đang điều hướng _đến_
  setPageLayout('other')
})
```

::note
Nếu bạn chọn đặt layout động ở phía server, bạn _phải_ làm như vậy trước khi layout được render bởi Vue (tức là trong plugin hoặc route middleware) để tránh mismatch hydration.
::
