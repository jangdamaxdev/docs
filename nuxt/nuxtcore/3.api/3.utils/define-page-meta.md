---
title: 'definePageMeta'
description: 'Định nghĩa siêu dữ liệu cho các thành phần trang của bạn.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/pages/runtime/composables.ts
    size: xs
---

`definePageMeta` là một macro trình biên dịch mà bạn có thể sử dụng để đặt siêu dữ liệu cho các thành phần **trang** của mình nằm trong thư mục [`pages/`](/docs/guide/directory-structure/pages) (trừ khi [đặt khác](/docs/api/nuxt-config#pages)). Bằng cách này, bạn có thể đặt siêu dữ liệu tùy chỉnh cho mỗi tuyến tĩnh hoặc động của ứng dụng Nuxt của mình.

```vue [pages/some-page.vue]
<script setup lang="ts">
definePageMeta({
  layout: 'default'
})
</script>
```

:read-more{to="/docs/guide/directory-structure/pages#page-metadata"}

## Type

```ts
definePageMeta(meta: PageMeta) => void

interface PageMeta {
  validate?: (route: RouteLocationNormalized) => boolean | Promise<boolean> | Partial<NuxtError> | Promise<Partial<NuxtError>>
  redirect?: RouteRecordRedirectOption
  name?: string
  path?: string
  props?: RouteRecordRaw['props']
  alias?: string | string[]
  pageTransition?: boolean | TransitionProps
  layoutTransition?: boolean | TransitionProps
  viewTransition?: boolean | 'always'
  key?: false | string | ((route: RouteLocationNormalizedLoaded) => string)
  keepalive?: boolean | KeepAliveProps
  layout?: false | LayoutKey | Ref<LayoutKey> | ComputedRef<LayoutKey>
  middleware?: MiddlewareKey | NavigationGuard | Array<MiddlewareKey | NavigationGuard>
  scrollToTop?: boolean | ((to: RouteLocationNormalizedLoaded, from: RouteLocationNormalizedLoaded) => boolean)
  [key: string]: unknown
}
```

## Parameters

### `meta`

- **Type**: `PageMeta`

  Một đối tượng chấp nhận siêu dữ liệu trang sau:

  **`name`**

  - **Type**: `string`

    Bạn có thể định nghĩa một tên cho tuyến của trang này. Theo mặc định, tên được tạo dựa trên đường dẫn bên trong thư mục [`pages/`](/docs/guide/directory-structure/pages).

  **`path`**

  - **Type**: `string`

    Bạn có thể định nghĩa một [biểu thức chính quy tùy chỉnh](#using-a-custom-regular-expression) nếu bạn có một mẫu phức tạp hơn có thể được biểu đạt bằng tên tệp.

  **`props`**
   
  - **Type**: [`RouteRecordRaw['props']`](https://router.vuejs.org/guide/essentials/passing-props)

    Cho phép truy cập `params` tuyến dưới dạng props được truyền cho thành phần trang.

  **`alias`**

  - **Type**: `string | string[]`

    Bí danh cho bản ghi. Cho phép định nghĩa các đường dẫn bổ sung sẽ hoạt động như một bản sao của bản ghi. Cho phép có các đường dẫn viết tắt như `/users/:id` và `/u/:id`. Tất cả giá trị `alias` và `path` phải chia sẻ cùng params.

  **`keepalive`**

  - **Type**: `boolean` | [`KeepAliveProps`](https://vuejs.org/api/built-in-components.html#keepalive)

    Đặt thành `true` khi bạn muốn bảo tồn trạng thái trang qua các thay đổi tuyến hoặc sử dụng [`KeepAliveProps`](https://vuejs.org/api/built-in-components.html#keepalive) để kiểm soát chi tiết.

  **`key`**

  - **Type**: `false` | `string` | `((route: RouteLocationNormalizedLoaded) => string)`

    Đặt giá trị `key` khi bạn cần kiểm soát nhiều hơn về khi thành phần `<NuxtPage>` được kết xuất lại.

  **`layout`**

  - **Type**: `false` | `LayoutKey` | `Ref<LayoutKey>` | `ComputedRef<LayoutKey>`

    Đặt tên tĩnh hoặc động của layout cho mỗi tuyến. Điều này có thể được đặt thành `false` trong trường hợp layout mặc định cần được tắt.

  **`layoutTransition`**

  - **Type**: `boolean` | [`TransitionProps`](https://vuejs.org/api/built-in-components.html#transition)

    Đặt tên của chuyển tiếp để áp dụng cho layout hiện tại. Bạn cũng có thể đặt giá trị này thành `false` để tắt chuyển tiếp layout.

  **`middleware`**

  - **Type**: `MiddlewareKey` | [`NavigationGuard`](https://router.vuejs.org/api/interfaces/NavigationGuard.html#navigationguard) | `Array<MiddlewareKey | NavigationGuard>`

    Định nghĩa middleware ẩn danh hoặc được đặt tên trực tiếp trong `definePageMeta`. Tìm hiểu thêm về [middleware tuyến](/docs/guide/directory-structure/middleware).

  **`pageTransition`**

  - **Type**: `boolean` | [`TransitionProps`](https://vuejs.org/api/built-in-components.html#transition)

    Đặt tên của chuyển tiếp để áp dụng cho trang hiện tại. Bạn cũng có thể đặt giá trị này thành `false` để tắt chuyển tiếp trang.

  **`viewTransition`**

  - **Type**: `boolean | 'always'`

    **Tính năng thử nghiệm, chỉ có sẵn khi [được bật trong tệp nuxt.config của bạn](/docs/getting-started/transitions#view-transitions-api-experimental)**</br>
    Bật/tắt Chuyển tiếp Chế độ xem cho trang hiện tại.
    Nếu đặt thành true, Nuxt sẽ không áp dụng chuyển tiếp nếu trình duyệt của người dùng khớp với `prefers-reduced-motion: reduce` (khuyến nghị). Nếu đặt thành `always`, Nuxt sẽ luôn áp dụng chuyển tiếp.

  **`redirect`**

  - **Type**: [`RouteRecordRedirectOption`](https://router.vuejs.org/guide/essentials/redirect-and-alias.html#redirect-and-alias)

    Nơi chuyển hướng nếu tuyến được khớp trực tiếp. Việc chuyển hướng xảy ra trước bất kỳ bảo vệ điều hướng nào và kích hoạt một điều hướng mới với vị trí đích mới.

  **`validate`**

  - **Type**: `(route: RouteLocationNormalized) => boolean | Promise<boolean> | Partial<NuxtError> | Promise<Partial<NuxtError>>`

    Xác thực xem một tuyến đã cho có thể được kết xuất hợp lệ với trang này hay không. Trả về true nếu hợp lệ, hoặc false nếu không. Nếu không tìm thấy khớp khác, điều này sẽ có nghĩa là 404. Bạn cũng có thể trực tiếp trả về một đối tượng với `statusCode`/`statusMessage` để phản hồi ngay lập tức với lỗi (các khớp khác sẽ không được kiểm tra).

  **`scrollToTop`**

  - **Type**: `boolean | (to: RouteLocationNormalized, from: RouteLocationNormalized) => boolean`

    Yêu cầu Nuxt cuộn lên đầu trước khi kết xuất trang hay không. Nếu bạn muốn ghi đè hành vi cuộn mặc định của Nuxt, bạn có thể làm như vậy trong `~/router.options.ts` (xem [định tuyến tùy chỉnh](/docs/guide/recipes/custom-routing#using-approuteroptions)) để biết thêm thông tin.

  **`[key: string]`**

  - **Type**: `any`

    Ngoài các thuộc tính ở trên, bạn cũng có thể đặt siêu dữ liệu **tùy chỉnh**. Bạn có thể muốn làm như vậy theo cách an toàn kiểu bằng cách [mở rộng loại của đối tượng `meta`](/docs/guide/directory-structure/pages/#typing-custom-metadata).

## Examples

### Basic Usage

Ví dụ dưới đây minh họa:

- cách `key` có thể là một hàm trả về một giá trị;
- cách thuộc tính `keepalive` đảm bảo rằng thành phần `<modal>` không được lưu trong bộ nhớ cache khi chuyển đổi giữa nhiều thành phần;
- thêm `pageType` làm thuộc tính tùy chỉnh:

```vue [pages/some-page.vue]
<script setup lang="ts">
definePageMeta({
  key: (route) => route.fullPath,

  keepalive: {
    exclude: ['modal']
  },

  pageType: 'Checkout'
})
</script>
```

### Defining Middleware

Ví dụ dưới đây cho thấy cách middleware có thể được định nghĩa bằng cách sử dụng một `function` trực tiếp trong `definePageMeta` hoặc đặt làm `string` khớp với tên tệp middleware nằm trong thư mục `middleware/`:

```vue [pages/some-page.vue]
<script setup lang="ts">
definePageMeta({
  // define middleware as a function
  middleware: [
    function (to, from) {
      const auth = useState('auth')

      if (!auth.value.authenticated) {
          return navigateTo('/login')
      }

      if (to.path !== '/checkout') {
        return navigateTo('/checkout')
      }
    }
  ],

  // ... or a string
  middleware: 'auth'

  // ... or multiple strings
  middleware: ['auth', 'another-named-middleware']
})
</script>
```

### Using a Custom Regular Expression

Biểu thức chính quy tùy chỉnh là một cách tốt để giải quyết xung đột giữa các tuyến chồng chéo, ví dụ:

Hai tuyến "/test-category" và "/1234-post" khớp với cả hai tuyến trang `[postId]-[postSlug].vue` và `[categorySlug].vue`.

Để đảm bảo rằng chúng ta chỉ khớp với chữ số (`\d+`) cho `postId` trong tuyến `[postId]-[postSlug]`, chúng ta có thể thêm như sau vào mẫu trang `[postId]-[postSlug].vue`:

```vue [pages/[postId\\]-[postSlug\\].vue]
<script setup lang="ts">
definePageMeta({
  path: '/:postId(\\d+)-:postSlug' 
})
</script>
```

Để biết thêm ví dụ, xem [Cú pháp Khớp của Vue Router](https://router.vuejs.org/guide/essentials/route-matching-syntax.html).

### Defining Layout

Bạn có thể định nghĩa layout khớp với tên tệp layout nằm (theo mặc định) trong thư mục [`layouts/`](/docs/guide/directory-structure/layouts). Bạn cũng có thể tắt layout bằng cách đặt `layout` thành `false`:

```vue [pages/some-page.vue]
<script setup lang="ts">
definePageMeta({
  // set custom layout
  layout: 'admin'

  // ... or disable a default layout
  layout: false
})
</script>
```
