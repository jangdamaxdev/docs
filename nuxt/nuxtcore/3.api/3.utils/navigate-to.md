---
title: "navigateTo"
description: navigateTo là một hàm trợ giúp điều hướng người dùng theo chương trình.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/router.ts
    size: xs
---

## Usage

`navigateTo` có sẵn ở cả phía máy chủ và phía máy khách. Nó có thể được sử dụng trong [bối cảnh Nuxt](/docs/guide/going-further/nuxt-app#the-nuxt-context), hoặc trực tiếp, để thực hiện điều hướng trang.

::warning
Đảm bảo luôn sử dụng `await` hoặc `return` trên kết quả của `navigateTo` khi gọi nó.
::

::note
`navigateTo` không thể được sử dụng trong các tuyến Nitro. Để thực hiện chuyển hướng phía máy chủ trong các tuyến Nitro, hãy sử dụng [`sendRedirect`](https://h3.dev/utils/response#sendredirectevent-location-code) thay thế.
::

### Within a Vue Component

```vue
<script setup lang="ts">
// passing 'to' as a string
await navigateTo('/search')

// ... or as a route object
await navigateTo({ path: '/search' })

// ... or as a route object with query parameters
await navigateTo({
  path: '/search',
  query: {
    page: 1,
    sort: 'asc'
  }
})
</script>
```

### Within Route Middleware

```ts
export default defineNuxtRouteMiddleware((to, from) => {
  if (to.path !== '/search') {
    // setting the redirect code to '301 Moved Permanently'
    return navigateTo('/search', { redirectCode: 301 })
  }
})
```

Khi sử dụng `navigateTo` trong middleware tuyến, bạn phải **trả về kết quả của nó** để đảm bảo luồng thực thi middleware hoạt động đúng cách.

Ví dụ, việc triển khai sau **sẽ không hoạt động như mong đợi**:

```ts
export default defineNuxtRouteMiddleware((to, from) => {
  if (to.path !== '/search') {
    // ❌ This will not work as expected
    navigateTo('/search', { redirectCode: 301 })
    return
  }
})
```

Trong trường hợp này, `navigateTo` sẽ được thực thi nhưng không được trả về, điều này có thể dẫn đến hành vi không mong muốn.

:read-more{to="/docs/guide/directory-structure/middleware"}

### Navigating to an External URL

Tham số `external` trong `navigateTo` ảnh hưởng đến cách điều hướng đến URL được xử lý:

- **Không có `external: true`**:
  - URL nội bộ điều hướng như mong đợi.
  - URL bên ngoài ném ra lỗi.

- **Với `external: true`**:
  - URL nội bộ điều hướng với tải lại toàn trang.
  - URL bên ngoài điều hướng như mong đợi.

#### Example

```vue
<script setup lang="ts">
// will throw an error;
// navigating to an external URL is not allowed by default
await navigateTo('https://nuxt.com')

// will redirect successfully with the 'external' parameter set to 'true'
await navigateTo('https://nuxt.com', {
  external: true
})
</script>
```

### Opening a Page in a New Tab

```vue
<script setup lang="ts">
// will open 'https://nuxt.com' in a new tab
await navigateTo('https://nuxt.com', {
  open: {
    target: '_blank',
    windowFeatures: {
      width: 500,
      height: 500
    }
  }
})
</script>
```

## Type

```ts
function navigateTo(
  to: RouteLocationRaw | undefined | null,
  options?: NavigateToOptions
) => Promise<void | NavigationFailure | false> | false | void | RouteLocationRaw 

interface NavigateToOptions {
  replace?: boolean
  redirectCode?: number
  external?: boolean
  open?: OpenOptions
}

type OpenOptions = {
  target: string
  windowFeatures?: OpenWindowFeatures
}

type OpenWindowFeatures = {
  popup?: boolean
  noopener?: boolean
  noreferrer?: boolean
} & XOR<{ width?: number }, { innerWidth?: number }>
  & XOR<{ height?: number }, { innerHeight?: number }>
  & XOR<{ left?: number }, { screenX?: number }>
  & XOR<{ top?: number }, { screenY?: number }>
```

## Parameters

### `to`

**Type**: [`RouteLocationRaw`](https://router.vuejs.org/api/interfaces/RouteLocationOptions.html#Interface-RouteLocationOptions) | `undefined` | `null`

**Default**: `'/'`

`to` có thể là một chuỗi đơn giản hoặc một đối tượng tuyến để chuyển hướng đến. Khi được truyền dưới dạng `undefined` hoặc `null`, nó sẽ mặc định là `'/'`.

#### Example

```ts
// Passing the URL directly will redirect to the '/blog' page
await navigateTo('/blog')

// Using the route object, will redirect to the route with the name 'blog'
await navigateTo({ name: 'blog' })

// Redirects to the 'product' route while passing a parameter (id = 1) using the route object.
await navigateTo({ name: 'product', params: { id: 1 } })
```

### `options` (optional)

**Type**: `NavigateToOptions`

Một đối tượng chấp nhận các thuộc tính sau:

- `replace`

  - **Type**: `boolean`
  - **Default**: `false`
  - Theo mặc định, `navigateTo` đẩy tuyến đã cho vào instance của Vue Router ở phía máy khách.

    Hành vi này có thể được thay đổi bằng cách đặt `replace` thành `true`, để chỉ ra rằng tuyến đã cho nên được thay thế.

- `redirectCode`

  - **Type**: `number`
  - **Default**: `302`

  - `navigateTo` chuyển hướng đến đường dẫn đã cho và đặt mã chuyển hướng thành [`302 Found`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/302) theo mặc định khi chuyển hướng diễn ra ở phía máy chủ.

    Hành vi mặc định này có thể được sửa đổi bằng cách cung cấp `redirectCode` khác. Thường thì [`301 Moved Permanently`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/301) có thể được sử dụng cho các chuyển hướng vĩnh viễn.

- `external`

  - **Type**: `boolean`
  - **Default**: `false`

  - Cho phép điều hướng đến một URL bên ngoài khi đặt thành `true`. Nếu không, `navigateTo` sẽ ném ra lỗi, vì điều hướng bên ngoài không được phép theo mặc định.

- `open`

  - **Type**: `OpenOptions`
  - Cho phép điều hướng đến URL bằng cách sử dụng phương thức [open()](https://developer.mozilla.org/en-US/docs/Web/API/Window/open) của cửa sổ. Tùy chọn này chỉ áp dụng ở phía máy khách và sẽ bị bỏ qua ở phía máy chủ.

    Một đối tượng chấp nhận các thuộc tính sau:

  - `target`

    - **Type**: `string`
    - **Default**: `'_blank'`

    - Một chuỗi, không có khoảng trắng, chỉ định tên của bối cảnh duyệt mà tài nguyên được tải vào.

  - `windowFeatures`

    - **Type**: `OpenWindowFeatures`

    - Một đối tượng chấp nhận các thuộc tính sau:

      | Property | Type    | Description |
      |----------|---------|--------------|
      | `popup`  | `boolean` | Yêu cầu một cửa sổ popup tối thiểu thay vì tab mới, với các tính năng UI được quyết định bởi trình duyệt. |
      | `width` or `innerWidth`  | `number`  | Chỉ định chiều rộng của khu vực nội dung (tối thiểu 100 pixel), bao gồm thanh cuộn. |
      | `height` or `innerHeight` | `number`  | Chỉ định chiều cao của khu vực nội dung (tối thiểu 100 pixel), bao gồm thanh cuộn. |
      | `left` or `screenX`   | `number`  | Đặt vị trí ngang của cửa sổ mới tương đối với cạnh trái của màn hình. |
      | `top` or `screenY`   | `number`  | Đặt vị trí dọc của cửa sổ mới tương đối với cạnh trên của màn hình. |
      | `noopener` | `boolean` | Ngăn cửa sổ mới truy cập cửa sổ gốc qua `window.opener`. |
      | `noreferrer` | `boolean` | Ngăn tiêu đề Referer được gửi và ngầm bật `noopener`. |

      Tham khảo [tài liệu](https://developer.mozilla.org/en-US/docs/Web/API/Window/open#windowfeatures) để biết thông tin chi tiết hơn về các thuộc tính **windowFeatures**.