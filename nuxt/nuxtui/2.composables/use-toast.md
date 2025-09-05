---
title: useToast
description: 'A composable to display toast notifications in your app.'
---

## Usage

Sử dụng composable `useToast` được tự động nhập để hiển thị thông báo [Toast](/components/toast).

```vue
<script setup lang="ts">
const toast = useToast()
</script>
```

- Composable `useToast` sử dụng `useState` của Nuxt để quản lý trạng thái toast, đảm bảo tính phản ứng trên toàn bộ ứng dụng của bạn.
- Tối đa 5 toast được hiển thị cùng lúc. Khi thêm một toast mới vượt quá giới hạn này, toast cũ nhất sẽ được tự động loại bỏ.
- Khi loại bỏ một toast, có độ trễ 200ms trước khi nó thực sự được loại bỏ khỏi trạng thái, cho phép các animation thoát.

::warning
Đảm bảo bọc ứng dụng của bạn với thành phần [`App`](/components/app) sử dụng thành phần [`Toaster`](https://github.com/nuxt/ui/blob/v3/src/runtime/components/Toaster.vue) của chúng tôi sử dụng thành phần [`ToastProvider`](https://reka-ui.com/docs/components/toast#provider) từ Reka UI.
::

::tip{to="/components/toast"}
Tìm hiểu cách tùy chỉnh giao diện và hành vi của toast trong tài liệu thành phần **Toast**.
::

## API

### `add(toast: Partial<Toast>): Toast`

Thêm một thông báo toast mới.

- Parameters:
  - `toast`: Một đối tượng `Toast` một phần với các thuộc tính sau:
    - `id` (tùy chọn): Một mã định danh duy nhất cho toast. Nếu không được cung cấp, một timestamp sẽ được sử dụng.
    - `open` (tùy chọn): Toast có mở hay không. Mặc định là `true`.
    - Các thuộc tính khác từ interface `Toast`.
- Returns: Đối tượng `Toast` hoàn chỉnh đã được thêm.

```vue
<script setup lang="ts">
const toast = useToast()

function showToast() {
  toast.add({
    title: 'Success',
    description: 'Your action was completed successfully.',
    color: 'success'
  })
}
</script>
```

### `update(id: string | number, toast: Partial<Toast>)`

Cập nhật một thông báo toast hiện có.

- Parameters:
  - `id`: Mã định danh duy nhất của toast để cập nhật.
  - `toast`: Một đối tượng `Toast` một phần với các thuộc tính để cập nhật.

```vue
<script setup lang="ts">
const toast = useToast()

function updateToast(id: string | number) {
  toast.update(id, {
    title: 'Updated Toast',
    description: 'This toast has been updated.'
  })
}
</script>
```

### `remove(id: string | number)`

Loại bỏ một thông báo toast.

- Parameters:
  - `id`: Mã định danh duy nhất của toast để loại bỏ.

```vue
<script setup lang="ts">
const toast = useToast()

function removeToast(id: string | number) {
  toast.remove(id)
}
</script>
```

### `clear()`

Loại bỏ tất cả thông báo toast.

```vue
<script setup lang="ts">
const toast = useToast()

function clearAllToasts() {
  toast.clear()
}
</script>
```

### `toasts`

- Type: `Ref<Toast[]>`
- Description: Một mảng phản ứng chứa tất cả thông báo toast hiện tại.