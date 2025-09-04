---
title: "usePreviewMode"
description: "Sử dụng usePreviewMode để kiểm tra và kiểm soát chế độ preview trong Nuxt"
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/preview.ts
    size: xs
---

# `usePreviewMode`

Chế độ preview cho phép bạn xem cách các thay đổi của bạn sẽ được hiển thị trên một site trực tiếp mà không tiết lộ chúng cho người dùng.

Bạn có thể sử dụng composable tích hợp `usePreviewMode` để truy cập và kiểm soát trạng thái preview trong Nuxt. Nếu composable phát hiện chế độ preview, nó sẽ tự động buộc bất kỳ cập nhật nào cần thiết cho [`useAsyncData`](/docs/api/composables/use-async-data) và [`useFetch`](/docs/api/composables/use-fetch) để rerender nội dung preview.

```js
const { enabled, state } = usePreviewMode()
```

## Options

### Custom `enable` check

Bạn có thể chỉ định cách tùy chỉnh để kích hoạt chế độ preview. Theo mặc định, composable `usePreviewMode` sẽ kích hoạt chế độ preview nếu có param `preview` trong url bằng `true` (ví dụ, `http://localhost:3000?preview=true`). Bạn có thể wrap `usePreviewMode` vào composable tùy chỉnh, để giữ options nhất quán trên các usages và ngăn chặn bất kỳ lỗi nào.

```js
export function useMyPreviewMode () {
  return usePreviewMode({
    shouldEnable: () => {
      return !!route.query.customPreview
    }
  });
}
```

### Modify default state

`usePreviewMode` sẽ cố gắng lưu giá trị của param `token` từ url trong state. Bạn có thể sửa đổi state này và nó sẽ khả dụng cho tất cả các calls [`usePreviewMode`](/docs/api/composables/use-preview-mode).

```js
const data1 = ref('data1')

const { enabled, state } = usePreviewMode({
  getState: (currentState) => {
    return { data1, data2: 'data2' }
  }
})
```

::note
Hàm `getState` sẽ append các giá trị trả về vào state hiện tại, vì vậy hãy cẩn thận không vô tình ghi đè state quan trọng.
::

### Customize the `onEnable` and `onDisable` callbacks

Theo mặc định, khi `usePreviewMode` được kích hoạt, nó sẽ gọi `refreshNuxtData()` để re-fetch tất cả data từ server.

Khi chế độ preview bị vô hiệu hóa, composable sẽ attach một callback để gọi `refreshNuxtData()` để chạy sau một router navigation tiếp theo.

Bạn có thể chỉ định callbacks tùy chỉnh để được trigger bằng cách cung cấp các hàm riêng của bạn cho options `onEnable` và `onDisable`.

```js
const { enabled, state } = usePreviewMode({
  onEnable: () => {
    console.log('preview mode has been enabled')
  },
  onDisable: () => {
    console.log('preview mode has been disabled')
  }
})
```

## Example

Ví dụ dưới đây tạo một page nơi một phần nội dung chỉ được render trong chế độ preview.

```vue [pages/some-page.vue]
<script setup>
const { enabled, state } = usePreviewMode()

const { data } = await useFetch('/api/preview', {
  query: {
    apiKey: state.token
  }
})
</script>

<template>
  <div>
    Some base content
    <p v-if="enabled">
      Only preview content: {{ state.token }}
      <br>
      <button @click="enabled = false">
        disable preview mode
      </button>
    </p>
  </div>
</template>
```

Bây giờ bạn có thể generate site của bạn và serve nó:

```bash [Terminal]
npx nuxt generate
npx nuxt preview
```

Sau đó bạn có thể xem page preview của bạn bằng cách thêm query param `preview` vào cuối page bạn muốn xem một lần:

```js
?preview=true
```

::note
`usePreviewMode` nên được test locally với `nuxt generate` và sau đó `nuxt preview` thay vì `nuxt dev`. (Lệnh [preview](/docs/api/commands/preview) không liên quan đến chế độ preview.)
::
