---
title: 'addRouteMiddleware'
description: 'addRouteMiddleware() là một hàm trợ giúp để thêm middleware một cách động trong ứng dụng của bạn.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/router.ts
    size: xs
---

::note
Middleware tuyến là các bảo vệ điều hướng được lưu trữ trong thư mục [`middleware/`](/docs/guide/directory-structure/middleware) của ứng dụng Nuxt của bạn (trừ khi [đặt khác](/docs/api/nuxt-config#middleware)).
::

## Type

```ts
function addRouteMiddleware (name: string, middleware: RouteMiddleware, options?: AddRouteMiddlewareOptions): void
function addRouteMiddleware (middleware: RouteMiddleware): void

interface AddRouteMiddlewareOptions {
  global?: boolean
}
```

## Parameters

### `name`

- **Type:** `string` | `RouteMiddleware`

Có thể là một chuỗi hoặc một hàm của loại `RouteMiddleware`. Hàm nhận tuyến tiếp theo `to` làm đối số đầu tiên và tuyến hiện tại `from` làm đối số thứ hai, cả hai đều là các đối tượng tuyến Vue.

Learn more about available properties of [route objects](/docs/api/composables/use-route).

### `middleware`

- **Type:** `RouteMiddleware`

Đối số thứ hai là một hàm của loại `RouteMiddleware`. Giống như trên, nó cung cấp các đối tượng tuyến `to` và `from`. Nó trở nên tùy chọn nếu đối số đầu tiên trong `addRouteMiddleware()` đã được truyền dưới dạng hàm.

### `options`

- **Type:** `AddRouteMiddlewareOptions`

Một đối số `options` tùy chọn cho phép bạn đặt giá trị của `global` thành `true` để chỉ ra xem middleware bộ định tuyến có phải là toàn cầu hay không (đặt thành `false` theo mặc định).

## Examples

### Named Route Middleware

Middleware tuyến được đặt tên được định nghĩa bằng cách cung cấp một chuỗi làm đối số đầu tiên và một hàm làm đối số thứ hai:

```ts [plugins/my-plugin.ts]
export default defineNuxtPlugin(() => {
  addRouteMiddleware('named-middleware', () => {
    console.log('named middleware added in Nuxt plugin')
  })
})
```

Khi được định nghĩa trong một plugin, nó ghi đè bất kỳ middleware nào có cùng tên nằm trong thư mục `middleware/`.

### Global Route Middleware

Middleware tuyến toàn cầu có thể được định nghĩa theo hai cách:

- Truyền một hàm trực tiếp làm đối số đầu tiên mà không có tên. Nó sẽ tự động được coi là middleware toàn cầu và áp dụng trên mọi thay đổi tuyến.

  ```ts [plugins/my-plugin.ts]
  export default defineNuxtPlugin(() => {
    addRouteMiddleware((to, from) => {
      console.log('anonymous global middleware that runs on every route change')
    })
  })
  ```

- Đặt đối số thứ ba tùy chọn `{ global: true }` để chỉ ra xem middleware tuyến có phải là toàn cầu hay không.

  ```ts [plugins/my-plugin.ts]
  export default defineNuxtPlugin(() => {
    addRouteMiddleware('global-middleware', (to, from) => {
        console.log('global middleware that runs on every route change')
      },
      { global: true }
    )
  })
  ```
