---
title: "defineNuxtRouteMiddleware"
description: "Tạo middleware tuyến được đặt tên bằng hàm trợ giúp defineNuxtRouteMiddleware."
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/router.ts
    size: xs
---

Middleware tuyến được lưu trữ trong [`middleware/`](/docs/guide/directory-structure/middleware) của ứng dụng Nuxt của bạn (trừ khi [đặt khác](/docs/api/nuxt-config#middleware)).

## Type

```ts
defineNuxtRouteMiddleware(middleware: RouteMiddleware) => RouteMiddleware

interface RouteMiddleware {
  (to: RouteLocationNormalized, from: RouteLocationNormalized): ReturnType<NavigationGuard>
}
```

## Parameters

### `middleware`

- **Type**: `RouteMiddleware`

Một hàm nhận hai đối tượng vị trí tuyến của Vue Router làm tham số: tuyến tiếp theo `to` làm đầu tiên, và tuyến hiện tại `from` làm thứ hai.

Learn more about available properties of `RouteLocationNormalized` in the **[Vue Router docs](https://router.vuejs.org/api/interfaces/RouteLocationNormalized.html)**.

## Examples

### Showing Error Page

Bạn có thể sử dụng middleware tuyến để ném lỗi và hiển thị thông báo lỗi hữu ích:

```ts [middleware/error.ts]
export default defineNuxtRouteMiddleware((to) => {
  if (to.params.id === '1') {
    throw createError({ statusCode: 404, statusMessage: 'Page Not Found' })
  }
})
```

Middleware tuyến ở trên sẽ chuyển hướng người dùng đến trang lỗi tùy chỉnh được định nghĩa trong tệp `~/error.vue`, và hiển thị thông báo lỗi và mã được truyền từ middleware.

### Redirection

Sử dụng [`useState`](/docs/api/composables/use-state) kết hợp với hàm trợ giúp `navigateTo` bên trong middleware tuyến để chuyển hướng người dùng đến các tuyến khác nhau dựa trên trạng thái xác thực của họ:

```ts [middleware/auth.ts]
export default defineNuxtRouteMiddleware((to, from) => {
  const auth = useState('auth')

  if (!auth.value.isAuthenticated) {
    return navigateTo('/login')
  }

  if (to.path !== '/dashboard') {
    return navigateTo('/dashboard')
  }
})
```

Cả [navigateTo](/docs/api/utils/navigate-to) và [abortNavigation](/docs/api/utils/abort-navigation) đều là các hàm trợ giúp có sẵn toàn cầu mà bạn có thể sử dụng bên trong `defineNuxtRouteMiddleware`.