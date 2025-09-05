---
title: "clearError"
description: "Composable clearError xóa tất cả các lỗi đã xử lý."
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/error.ts
    size: xs
---

Trong các trang, thành phần và plugin của bạn, bạn có thể sử dụng `clearError` để xóa tất cả lỗi và chuyển hướng người dùng.

**Parameters:**

- `options?: { redirect?: string }`

Bạn có thể cung cấp một đường dẫn tùy chọn để chuyển hướng đến (ví dụ, nếu bạn muốn điều hướng đến một trang 'an toàn').

```js
// Without redirect
clearError()

// With redirect
clearError({ redirect: '/homepage' })
```

Lỗi được đặt trong trạng thái bằng cách sử dụng [`useError()`](/docs/api/composables/use-error). Composable `clearError` sẽ đặt lại trạng thái này và gọi hook `app:error:cleared` với các tùy chọn được cung cấp.

:read-more{to="/docs/getting-started/error-handling"}
