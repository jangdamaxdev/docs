---
title: defineShortcuts
description: 'A composable to define keyboard shortcuts in your app.'
---

## Usage

Sử dụng composable `defineShortcuts` được tự động nhập để định nghĩa các phím tắt bàn phím.

```vue
<script setup lang="ts">
const open = ref(false)

defineShortcuts({
  meta_k: () => {
    open.value = !open.value
  }
})
</script>
```

- Các phím tắt được tự động điều chỉnh cho các nền tảng không phải macOS, chuyển đổi `meta` thành `ctrl`.
- Composable sử dụng [`useEventListener`](https://vueuse.org/core/useEventListener/) của VueUse để xử lý các sự kiện keydown.
- Để có danh sách đầy đủ các phím tắt có sẵn, hãy tham khảo tài liệu API [`KeyboardEvent.key`](https://developer.mozilla.org/en-US/docs/Web/API/UI_Events/Keyboard_event_key_values). Lưu ý rằng phím nên được viết bằng chữ thường.

::tip{to="/components/kbd"}
Tìm hiểu cách hiển thị các phím tắt trong các thành phần trong tài liệu thành phần **Kbd**.
::

## API

### `defineShortcuts(config: ShortcutsConfig, options?: ShortcutsOptions)`

Định nghĩa các phím tắt bàn phím cho ứng dụng của bạn.

- `config`: Một đối tượng nơi các khóa là định nghĩa phím tắt và các giá trị là các hàm xử lý hoặc đối tượng cấu hình phím tắt.
- `options`: Cấu hình tùy chọn cho hành vi của các phím tắt.
  - `chainDelay`: Độ trễ giữa các lần nhấn phím để xem xét phím tắt là được liên kết. Mặc định là `250`.

#### Shortcut Definition

Các phím tắt được định nghĩa bằng định dạng sau:

- Phím đơn: `'a'`, `'b'`, `'1'`, `'?'`, v.v.
- Sự kết hợp phím: Sử dụng `_` để tách các phím, ví dụ, `'meta_k'`, `'ctrl_shift_f'`
- Chuỗi phím: Sử dụng `-` để định nghĩa một chuỗi, ví dụ, `'g-d'`

#### Modifiers

- `meta`: Đại diện cho `⌘ Command` trên macOS và `Ctrl` trên các nền tảng khác
- `ctrl`: Đại diện cho `Ctrl` trên tất cả các nền tảng
- `shift`: Được sử dụng cho các phím chữ cái khi cần Shift

#### Special Keys

- `escape`: Kích hoạt trên phím Esc
- `enter`: Kích hoạt trên phím Enter
- `arrowleft`, `arrowright`, `arrowup`, `arrowdown`: Kích hoạt trên các phím mũi tên tương ứng

#### Shortcut Configuration

Mỗi phím tắt có thể được định nghĩa là một hàm hoặc một đối tượng với các thuộc tính sau:

```ts
interface ShortcutConfig {
  handler: () => void
  usingInput?: boolean | string
}
```

- `handler`: Hàm được thực thi khi phím tắt được kích hoạt
- `usingInput`:
  - `false` (mặc định): Phím tắt chỉ kích hoạt khi không có đầu vào nào được tập trung
  - `true`: Phím tắt kích hoạt ngay cả khi bất kỳ đầu vào nào được tập trung
  - `string`: Phím tắt chỉ kích hoạt khi đầu vào được chỉ định (theo tên) được tập trung

## Examples

### Basic usage

```vue
<script setup lang="ts">
defineShortcuts({
  '?': () => openHelpModal(),
  'meta_k': () => openCommandPalette(),
  'g-d': () => navigateToDashboard()
})
</script>
```

### With input focus handling

Tùy chọn `usingInput` cho phép bạn chỉ định rằng một phím tắt chỉ nên kích hoạt khi một đầu vào cụ thể được tập trung.

```vue
<template>
  <UInput v-model="query" name="queryInput" />
</template>

<script setup lang="ts">
const query = ref('')

defineShortcuts({
  enter: {
    usingInput: 'queryInput',
    handler: () => performSearch()
  },
  escape: {
    usingInput: true,
    handler: () => clearSearch()
  }
})
</script>
```

### Extracting shortcuts from menu items

Tiện ích `extractShortcuts` có thể được sử dụng để tự động định nghĩa các phím tắt từ các mục menu:

```vue
<script setup lang="ts">
const items = [{
  label: 'Save',
  icon: 'i-lucide-file-down',
  kbds: ['meta', 'S'],
  onSelect() {
    save()
  }
}, {
  label: 'Copy',
  icon: 'i-lucide-copy',
  kbds: ['meta', 'C'],
  onSelect() {
    copy()
  }
}]

defineShortcuts(extractShortcuts(items))
</script>
```
