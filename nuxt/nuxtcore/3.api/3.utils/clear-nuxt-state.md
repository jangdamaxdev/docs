---
title: 'clearNuxtState'
description: Xóa trạng thái được lưu trong bộ nhớ cache của useState.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/state.ts
    size: xs
---

::note
Phương thức này hữu ích nếu bạn muốn làm mất hiệu lực trạng thái của `useState`.
::

## Type

```ts
clearNuxtState (keys?: string | string[] | ((key: string) => boolean)): void
```

## Parameters

- `keys`: Một hoặc một mảng các khóa được sử dụng trong [`useState`](/docs/api/composables/use-state) để xóa trạng thái được lưu trong bộ nhớ cache của chúng. Nếu không có khóa nào được cung cấp, **tất cả trạng thái** sẽ bị làm mất hiệu lực.
