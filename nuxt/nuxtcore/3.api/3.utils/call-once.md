---
title: "callOnce"
description: "Chạy một hàm hoặc khối mã đã cho một lần trong quá trình SSR hoặc CSR."
navigation:
  badge: New
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/once.ts
    size: xs
---

::important
Tiện ích này có sẵn kể từ [Nuxt v3.9](/blog/v3-9).
::

## Purpose

Hàm `callOnce` được thiết kế để thực thi một hàm hoặc khối mã đã cho chỉ một lần trong quá trình:

- kết xuất phía máy chủ nhưng không phải hydrat hóa
- điều hướng phía máy khách

Điều này hữu ích cho mã chỉ nên được thực thi một lần, chẳng hạn như ghi nhật ký sự kiện hoặc thiết lập trạng thái toàn cầu.

## Usage

Chế độ mặc định của `callOnce` là chạy mã chỉ một lần. Ví dụ, nếu mã chạy trên máy chủ, nó sẽ không chạy lại trên máy khách. Nó cũng sẽ không chạy lại nếu bạn `callOnce` nhiều hơn một lần trên máy khách, ví dụ bằng cách điều hướng trở lại trang này.

```vue [app.vue]
<script setup lang="ts">
const websiteConfig = useState('config')

await callOnce(async () => {
  console.log('This will only be logged once')
  websiteConfig.value = await $fetch('https://my-cms.com/api/website-config')
})
</script>
```

Cũng có thể chạy trên mọi điều hướng trong khi vẫn tránh tải kép ban đầu máy chủ/máy khách. Để làm điều này, có thể sử dụng chế độ `navigation`:

```vue [app.vue]
<script setup lang="ts">
const websiteConfig = useState('config')

await callOnce(async () => {
  console.log('This will only be logged once and then on every client side navigation')
  websiteConfig.value = await $fetch('https://my-cms.com/api/website-config')
}, { mode: 'navigation' })
</script>
```

::important
Chế độ `navigation` có sẵn kể từ [Nuxt v3.15](/blog/v3-15).
::

::tip{to="/docs/getting-started/state-management#usage-with-pinia"}
`callOnce` hữu ích khi kết hợp với [mô-đun Pinia](/modules/pinia) để gọi các hành động store.
::

:read-more{to="/docs/getting-started/state-management"}

::warning
Lưu ý rằng `callOnce` không trả về gì. Bạn nên sử dụng [`useAsyncData`](/docs/api/composables/use-async-data) hoặc [`useFetch`](/docs/api/composables/use-fetch) nếu bạn muốn thực hiện việc lấy dữ liệu trong quá trình SSR.
::

::note
`callOnce` là một composable được thiết kế để được gọi trực tiếp trong hàm setup, plugin hoặc middleware tuyến, vì nó cần thêm dữ liệu vào payload Nuxt để tránh gọi lại hàm trên máy khách khi trang hydrat hóa.
::

## Type

```ts
callOnce (key?: string, fn?: (() => any | Promise<any>), options?: CallOnceOptions): Promise<void>
callOnce(fn?: (() => any | Promise<any>), options?: CallOnceOptions): Promise<void>

type CallOnceOptions = {
  /**
   * Execution mode for the callOnce function
   * @default 'render'
   */
  mode?: 'navigation' | 'render'
}
```

## Parameters

- `key`: Một khóa duy nhất đảm bảo rằng mã được chạy một lần. Nếu bạn không cung cấp khóa, thì một khóa duy nhất với tệp và số dòng của phiên bản `callOnce` sẽ được tạo cho bạn.
- `fn`: Hàm để chạy một lần. Nó có thể không đồng bộ.
- `options`: Thiết lập chế độ, hoặc để thực thi lại trên điều hướng (`navigation`) hoặc chỉ một lần trong suốt thời gian tồn tại của ứng dụng (`render`). Mặc định là `render`.
  - `render`: Thực thi một lần trong quá trình kết xuất ban đầu (hoặc SSR hoặc CSR) - Chế độ mặc định
  - `navigation`: Thực thi một lần trong quá trình kết xuất ban đầu và một lần cho mỗi điều hướng phía máy khách tiếp theo
