---
title: 'showError'
description: Nuxt provides a quick and simple way to show a full screen error page if needed.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/error.ts
    size: xs
---

Trong [Nuxt context](/docs/guide/going-further/nuxt-app#the-nuxt-context) bạn có thể sử dụng `showError` để hiển thị lỗi.

**Parameters:**

- `error`: `string | Error | Partial<{ cause, data, message, name, stack, statusCode, statusMessage }>`

```ts
showError("😱 Ôi không, một lỗi đã được ném ra.")
showError({
  statusCode: 404,
  statusMessage: "Không Tìm Thấy Trang"
})
```

Lỗi được đặt trong state bằng cách sử dụng [`useError()`](/docs/api/composables/use-error) để tạo một shared error state reactive và SSR-friendly trên các components.

::tip
`showError` gọi hook `app:error`.
::

:read-more{to="/docs/getting-started/error-handling"}
