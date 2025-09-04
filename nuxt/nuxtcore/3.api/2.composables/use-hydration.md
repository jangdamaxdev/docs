---
title: 'useHydration'
description: 'Cho phép kiểm soát đầy đủ chu kỳ hydration để đặt và nhận dữ liệu từ máy chủ.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/hydrate.ts
    size: xs
---

::note
Đây là một composable nâng cao, chủ yếu được thiết kế để sử dụng trong các plugin, chủ yếu được sử dụng bởi các module Nuxt.
::

::note
`useHydration` được thiết kế để **đảm bảo đồng bộ hóa và khôi phục trạng thái trong quá trình SSR**. Nếu bạn cần tạo một trạng thái phản ứng toàn cục thân thiện với SSR trong Nuxt, [`useState`](/docs/api/composables/use-state) là lựa chọn được khuyến nghị.
::

`useHydration` là một composable tích hợp cung cấp cách để đặt dữ liệu ở phía máy chủ mỗi khi có yêu cầu HTTP mới và nhận dữ liệu đó ở phía client. Bằng cách này `useHydration` cho phép bạn kiểm soát đầy đủ chu kỳ hydration.

Dữ liệu trả về từ hàm `get` trên máy chủ được lưu trữ trong `nuxtApp.payload` dưới khóa duy nhất được cung cấp làm tham số đầu tiên cho `useHydration`. Trong quá trình hydration, dữ liệu này sau đó được truy xuất trên client, ngăn chặn các tính toán hoặc gọi API dư thừa.

## Usage

::code-group

```ts [Without useHydration]
export default defineNuxtPlugin((nuxtApp) => {
  const myStore = new MyStore()

  if (import.meta.server) {
    nuxt.hooks.hook('app:rendered', () => {
      nuxtApp.payload.myStoreState = myStore.getState()
    })
  }

  if (import.meta.client) {
    nuxt.hooks.hook('app:created', () => {
      myStore.setState(nuxtApp.payload.myStoreState)
    })
  }
})
```

```ts [With useHydration]
export default defineNuxtPlugin((nuxtApp) => {
  const myStore = new MyStore()

  useHydration(
    'myStoreState',
    () => myStore.getState(),
    (data) => myStore.setState(data)
  )
})
```

::

## Type

```ts [signature]
useHydration <T> (key: string, get: () => T, set: (value: T) => void) => void
```

## Parameters

- `key`: Một khóa duy nhất xác định dữ liệu trong ứng dụng Nuxt của bạn.
- `get`: Một hàm được thực thi **chỉ trên máy chủ** (được gọi khi kết xuất SSR hoàn tất) để đặt giá trị ban đầu.
- `set`: Một hàm được thực thi **chỉ trên client** (được gọi khi instance vue ban đầu được tạo) để nhận dữ liệu.
