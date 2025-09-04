---
title: "useError"
description: useError composable trả về lỗi Nuxt toàn cục đang được xử lý.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/error.ts
    size: xs
---

## Usage

Composable `useError` trả về lỗi Nuxt toàn cục đang được xử lý và có sẵn trên cả client và server. Nó cung cấp một error state reactive, thân thiện với SSR trên app của bạn.

```ts
const error = useError()
```

Bạn có thể sử dụng composable này trong components, pages hoặc plugins của bạn để access hoặc react với Nuxt error hiện tại.

## Type

```ts
interface NuxtError<DataT = unknown> {
  statusCode: number
  statusMessage: string
  message: string
  data?: DataT
  error?: true
}

export const useError: () => Ref<NuxtError | undefined>
```

## Parameters

Composable này không nhận bất kỳ parameters nào.

## Return Values

Trả về một `Ref` chứa Nuxt error hiện tại (hoặc `undefined` nếu không có error). Error object là reactive và sẽ update tự động khi error state changes.

## Example

```ts
<script setup lang="ts">
const error = useError()

if (error.value) {
  console.error('Nuxt error:', error.value)
}
</script>
```

:read-more{to="/docs/getting-started/error-handling"}
