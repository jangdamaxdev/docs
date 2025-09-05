---
title: 'abortNavigation'
description: 'abortNavigation là một hàm trợ giúp ngăn chặn việc điều hướng diễn ra và ném ra lỗi nếu có lỗi được đặt làm tham số.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/router.ts
    size: xs
---

::warning
`abortNavigation` chỉ có thể sử dụng bên trong một [trình xử lý middleware tuyến](/docs/guide/directory-structure/middleware).
::

## Type

```ts
abortNavigation(err?: Error | string): false
```

## Parameters

### `err`

- **Type**: [`Error`](https://developer.mozilla.org/pl/docs/Web/JavaScript/Reference/Global_Objects/Error) | `string`

  Lỗi tùy chọn được ném ra bởi `abortNavigation`.

## Examples

Ví dụ dưới đây cho thấy cách bạn có thể sử dụng `abortNavigation` trong middleware tuyến để ngăn chặn truy cập tuyến không được ủy quyền:

```ts [middleware/auth.ts]
export default defineNuxtRouteMiddleware((to, from) => {
  const user = useState('user')

  if (!user.value.isAuthorized) {
    return abortNavigation()
  }

  if (to.path !== '/edit-post') {
    return navigateTo('/edit-post')
  }
})
```

### `err` as a String

Bạn có thể truyền lỗi dưới dạng chuỗi:

```ts [middleware/auth.ts]
export default defineNuxtRouteMiddleware((to, from) => {
  const user = useState('user')

  if (!user.value.isAuthorized) {
    return abortNavigation('Insufficient permissions.')
  }
})
```

### `err` as an Error Object

Bạn có thể truyền lỗi dưới dạng đối tượng [`Error`](https://developer.mozilla.org/pl/docs/Web/JavaScript/Reference/Global_Objects/Error), ví dụ như được bắt bởi khối `catch`:

```ts [middleware/auth.ts]
export default defineNuxtRouteMiddleware((to, from) => {
  try {
    /* code that might throw an error */
  } catch (err) {
    return abortNavigation(err)
  }
})
```
