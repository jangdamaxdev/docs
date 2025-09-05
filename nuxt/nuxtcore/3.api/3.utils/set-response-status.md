---
title: 'setResponseStatus'
description: setResponseStatus sets the statusCode (and optionally the statusMessage) of the response.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/ssr.ts
    size: xs
---

Nuxt cung cấp composables và utilities cho hỗ trợ server-side-rendering hạng nhất.

`setResponseStatus` đặt statusCode (và tùy chọn statusMessage) của response.

::important
`setResponseStatus` chỉ có thể được gọi trong [Nuxt context](/docs/guide/going-further/nuxt-app#the-nuxt-context).
::

```js
const event = useRequestEvent()

// event sẽ undefined trong trình duyệt
if (event) {
  // Đặt status code thành 404 cho trang 404 tùy chỉnh
  setResponseStatus(event, 404)

  // Đặt status message cũng vậy
  setResponseStatus(event, 404, 'Page Not Found')
}
```

::note
Trong trình duyệt, `setResponseStatus` sẽ không có hiệu lực.
::

:read-more{to="/docs/getting-started/error-handling"}
