---
title: 'clearNuxtData'
description: Xóa dữ liệu được lưu trong bộ nhớ cache, trạng thái lỗi và các promise đang chờ xử lý của useAsyncData và useFetch.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/asyncData.ts
    size: xs
---

::note
Phương thức này hữu ích nếu bạn muốn làm mất hiệu lực việc lấy dữ liệu cho một trang khác.
::

## Type

```ts
clearNuxtData (keys?: string | string[] | ((key: string) => boolean)): void
```

## Parameters

* `keys`: Một hoặc một mảng các khóa được sử dụng trong [`useAsyncData`](/docs/api/composables/use-async-data) để xóa dữ liệu được lưu trong bộ nhớ cache của chúng. Nếu không có khóa nào được cung cấp, **tất cả dữ liệu** sẽ bị làm mất hiệu lực.
