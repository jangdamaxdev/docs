---
title: useHeadSafe
description: Cách được khuyến nghị để cung cấp dữ liệu head với đầu vào của người dùng.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/unjs/unhead/blob/main/packages/vue/src/composables.ts
    size: xs
---

Composable `useHeadSafe` là một wrapper xung quanh composable [`useHead`](/docs/api/composables/use-head) nhằm hạn chế đầu vào chỉ cho phép các giá trị an toàn.

## Usage

Bạn có thể truyền tất cả các giá trị giống như [`useHead`](/docs/api/composables/use-head)

```ts
useHeadSafe({
  script: [
    { id: 'xss-script', innerHTML: 'alert("xss")' }
  ],
  meta: [
    { 'http-equiv': 'refresh', content: '0;javascript:alert(1)' }
  ]
})
// Sẽ tạo ra một cách an toàn
// <script id="xss-script"></script>
// <meta content="0;javascript:alert(1)">
```

::read-more{to="https://unhead.unjs.io/docs/typescript/head/api/composables/use-head-safe" target="_blank"}
Đọc thêm về tài liệu `Unhead`.
::

## Type

```ts
useHeadSafe(input: MaybeComputedRef<HeadSafe>): void
```

Danh sách các giá trị được phép là:

```ts
const WhitelistAttributes = {
  htmlAttrs: ['class', 'style', 'lang', 'dir'],
  bodyAttrs: ['class', 'style'],
  meta: ['name', 'property', 'charset', 'content', 'media'],
  noscript: ['textContent'],
  style: ['media', 'textContent', 'nonce', 'title', 'blocking'],
  script: ['type', 'textContent', 'nonce', 'blocking'],
  link: ['color', 'crossorigin', 'fetchpriority', 'href', 'hreflang', 'imagesrcset', 'imagesizes', 'integrity', 'media', 'referrerpolicy', 'rel', 'sizes', 'type'],
}
```

Xem [@unhead/vue](https://github.com/unjs/unhead/blob/main/packages/vue/src/types/safeSchema.ts) để biết các loại chi tiết hơn.
