---
title: 'useLoadingIndicator'
description: Composable này cung cấp cho bạn quyền truy cập vào trạng thái loading của trang ứng dụng.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/loading-indicator.ts
    size: xs
---

## Description

Một composable trả về trạng thái loading của trang. Được sử dụng bởi [`<NuxtLoadingIndicator>`](/docs/api/components/nuxt-loading-indicator) và có thể kiểm soát.
Nó hook vào [`page:loading:start`](/docs/api/advanced/hooks#app-hooks-runtime) và [`page:loading:end`](/docs/api/advanced/hooks#app-hooks-runtime) để thay đổi trạng thái của nó.

## Parameters

- `duration`: Thời lượng của thanh loading, tính bằng mili giây (mặc định `2000`).
- `throttle`: Throttle việc xuất hiện và ẩn, tính bằng mili giây (mặc định `200`).
- `estimatedProgress`: Theo mặc định Nuxt sẽ back off khi nó tiếp cận 100%. Bạn có thể cung cấp một hàm tùy chỉnh để tùy chỉnh ước tính tiến độ, hàm này nhận thời lượng của thanh loading (ở trên) và thời gian đã trôi qua. Nó nên trả về một giá trị từ 0 đến 100.

## Properties

### `isLoading`

- **type**: `Ref<boolean>`
- **description**: Trạng thái loading

### `error`

- **type**: `Ref<boolean>`
- **description**: Trạng thái lỗi

### `progress`

- **type**: `Ref<number>`
- **description**: Trạng thái tiến độ. Từ `0` đến `100`.

## Methods

### `start()`

Đặt `isLoading` thành true và bắt đầu tăng giá trị `progress`. `start` chấp nhận tùy chọn `{ force: true }` để bỏ qua khoảng thời gian và hiển thị trạng thái loading ngay lập tức.

### `set()`

Đặt giá trị `progress` thành một giá trị cụ thể. `set` chấp nhận tùy chọn `{ force: true }` để bỏ qua khoảng thời gian và hiển thị trạng thái loading ngay lập tức.

### `finish()`

Đặt giá trị `progress` thành `100`, dừng tất cả timer và interval sau đó reset trạng thái loading sau `500` ms. `finish` chấp nhận `{ force: true }` để bỏ qua khoảng thời gian trước khi trạng thái được reset, và `{ error: true }` để thay đổi màu thanh loading và đặt thuộc tính error thành true.

### `clear()`

Được sử dụng bởi `finish()`. Xóa tất cả timer và interval được sử dụng bởi composable.

## Example

```vue
<script setup lang="ts">
  const { progress, isLoading, start, finish, clear } = useLoadingIndicator({
    duration: 2000,
    throttle: 200,
    // Đây là cách tiến độ được tính toán theo mặc định
    estimatedProgress: (duration, elapsed) => (2 / Math.PI * 100) * Math.atan(elapsed / duration * 100 / 50)
  })
</script>
```

```vue
<script setup lang="ts">
  const { start, set } = useLoadingIndicator()
  // giống như set(0, { force: true })
  // đặt tiến độ thành 0, và hiển thị loading ngay lập tức
  start({ force: true })
</script>
```
