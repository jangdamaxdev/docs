---
title: "onPrehydrate"
description: "Sử dụng onPrehydrate để chạy một callback trên client ngay lập tức trước khi Nuxt hydrate trang."
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/ssr.ts
    size: xs
---

::important
Composable này có sẵn trong Nuxt v3.12+.
::

`onPrehydrate` là một composable lifecycle hook cho phép bạn chạy một callback trên client ngay lập tức trước khi Nuxt hydrate trang.
::note
Đây là một tiện ích nâng cao và nên được sử dụng cẩn thận. Ví dụ, [`nuxt-time`](https://github.com/danielroe/nuxt-time/pull/251) và [`@nuxtjs/color-mode`](https://github.com/nuxt-modules/color-mode/blob/main/src/script.js) thao tác DOM để tránh các lỗi hydration không khớp.
::

## Usage

Gọi `onPrehydrate` trong hàm setup của một Vue component (ví dụ, trong `<script setup>`) hoặc trong một plugin. Nó chỉ có hiệu lực khi được gọi trên server và sẽ không được bao gồm trong build client của bạn.

## Type

```ts [Signature]
export function onPrehydrate(callback: (el: HTMLElement) => void): void
export function onPrehydrate(callback: string | ((el: HTMLElement) => void), key?: string): undefined | string
```

## Parameters

| Parameter | Type | Required | Description |
| ---- | --- | --- | --- |
| `callback` | `((el: HTMLElement) => void) \| string` | Yes | Một hàm (hoặc hàm được stringified) để chạy trước khi Nuxt hydrates. Nó sẽ được stringified và inline trong HTML. Không nên có các dependencies bên ngoài hoặc tham chiếu đến các biến bên ngoài callback. Chạy trước khi Nuxt runtime khởi tạo, vì vậy nó không nên phụ thuộc vào Nuxt hoặc Vue context. |
| `key` | `string` | No | (Nâng cao) Một key duy nhất để xác định prehydrate script, hữu ích cho các kịch bản nâng cao như nhiều root nodes. |

## Return Values

- Trả về `undefined` khi được gọi chỉ với một callback function.
- Trả về một string (prehydrate id) khi được gọi với một callback và một key, có thể được sử dụng để set hoặc access thuộc tính `data-prehydrate-id` cho các use case nâng cao.

## Example

```vue twoslash [app.vue]
<script setup lang="ts">
declare const window: Window
// ---cut---
// Chạy code trước khi Nuxt hydrates
onPrehydrate(() => {
  console.log(window)
})

// Truy cập root element
onPrehydrate((el) => {
  console.log(el.outerHTML)
  // <div data-v-inspector="app.vue:15:3" data-prehydrate-id=":b3qlvSiBeH:"> Hi there </div>
})

// Nâng cao: truy cập/set `data-prehydrate-id` của chính bạn
const prehydrateId = onPrehydrate((el) => {})
</script>

<template>
  <div>
    Hi there
  </div>
</template>
```
