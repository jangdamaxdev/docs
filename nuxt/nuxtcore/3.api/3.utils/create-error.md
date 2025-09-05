---
title: 'createError'
description: Tạo một đối tượng lỗi với siêu dữ liệu bổ sung.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/error.ts
    size: xs
---

Bạn có thể sử dụng hàm này để tạo một đối tượng lỗi với siêu dữ liệu bổ sung. Nó có thể sử dụng được trong cả phần Vue và Nitro của ứng dụng của bạn, và được thiết kế để được ném ra.

## Parameters

- `err`: `string | { cause, data, message, name, stack, statusCode, statusMessage, fatal }`

Bạn có thể truyền một chuỗi hoặc một đối tượng cho hàm `createError`. Nếu bạn truyền một chuỗi, nó sẽ được sử dụng làm `message` lỗi, và `statusCode` sẽ mặc định là `500`. Nếu bạn truyền một đối tượng, bạn có thể đặt nhiều thuộc tính của lỗi, chẳng hạn như `statusCode`, `message`, và các thuộc tính lỗi khác.

## In Vue App

Nếu bạn ném một lỗi được tạo với `createError`:

- ở phía máy chủ, nó sẽ kích hoạt một trang lỗi toàn màn hình mà bạn có thể xóa với `clearError`.
- ở phía máy khách, nó sẽ ném một lỗi không nghiêm trọng để bạn xử lý. Nếu bạn cần kích hoạt một trang lỗi toàn màn hình, thì bạn có thể làm điều này bằng cách đặt `fatal: true`.

### Example

```vue [pages/movies/[slug\\].vue]
<script setup lang="ts">
const route = useRoute()
const { data } = await useFetch(`/api/movies/${route.params.slug}`)
if (!data.value) {
  throw createError({ statusCode: 404, statusMessage: 'Page Not Found' })
}
</script>
```

## In API Routes

Sử dụng `createError` để kích hoạt xử lý lỗi trong các tuyến API máy chủ.

### Example

```ts [server/api/error.ts]
export default eventHandler(() => {
  throw createError({
    statusCode: 404,
    statusMessage: 'Page Not Found'
  })
})
```

Trong các tuyến API, việc sử dụng `createError` bằng cách truyền một đối tượng với `statusMessage` ngắn được khuyến nghị vì nó có thể được truy cập ở phía máy khách. Nếu không, một `message` được truyền cho `createError` trên một tuyến API sẽ không được truyền đến máy khách. Ngoài ra, bạn có thể sử dụng thuộc tính `data` để truyền dữ liệu trở lại máy khách. Trong mọi trường hợp, luôn cân nhắc tránh đặt đầu vào người dùng động vào message để tránh các vấn đề bảo mật tiềm ẩn.

:read-more{to="/docs/getting-started/error-handling"}
