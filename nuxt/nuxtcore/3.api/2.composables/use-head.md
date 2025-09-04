---
title: useHead
description: useHead tùy chỉnh các thuộc tính head của các trang riêng lẻ trong ứng dụng Nuxt của bạn.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/unjs/unhead/blob/main/packages/vue/src/composables.ts
    size: xs
---

Hàm composable [`useHead`](/docs/api/composables/use-head) cho phép bạn quản lý các thẻ head của mình theo cách lập trình và phản ứng, được hỗ trợ bởi [Unhead](https://unhead.unjs.io). Nếu dữ liệu đến từ người dùng hoặc nguồn không đáng tin cậy, chúng tôi khuyên bạn nên kiểm tra [`useHeadSafe`](/docs/api/composables/use-head-safe).

:read-more{to="/docs/getting-started/seo-meta"}

## Type

```ts
useHead(meta: MaybeComputedRef<MetaObject>): void
```

Dưới đây là các loại không phản ứng cho [`useHead`](/docs/api/composables/use-head).

```ts
interface MetaObject {
  title?: string
  titleTemplate?: string | ((title?: string) => string)
  base?: Base
  link?: Link[]
  meta?: Meta[]
  style?: Style[]
  script?: Script[]
  noscript?: Noscript[]
  htmlAttrs?: HtmlAttributes
  bodyAttrs?: BodyAttributes
}
```

Xem [@unhead/vue](https://github.com/unjs/unhead/blob/main/packages/vue/src/types/schema.ts) để biết các loại chi tiết hơn.

::note
Các thuộc tính của `useHead` có thể động, chấp nhận các thuộc tính `ref`, `computed` và `reactive`. Tham số `meta` cũng có thể chấp nhận một hàm trả về một đối tượng để làm cho toàn bộ đối tượng phản ứng.
::

## Params

### `meta`

**Type**: `MetaObject`

Một đối tượng chấp nhận siêu dữ liệu head sau:

- `meta`: Mỗi phần tử trong mảng được ánh xạ tới một thẻ `<meta>` mới được tạo, nơi các thuộc tính đối tượng được ánh xạ tới các thuộc tính tương ứng.
  - **Type**: `Array<Record<string, any>>`
- `link`: Mỗi phần tử trong mảng được ánh xạ tới một thẻ `<link>` mới được tạo, nơi các thuộc tính đối tượng được ánh xạ tới các thuộc tính tương ứng.
  - **Type**: `Array<Record<string, any>>`
- `style`: Mỗi phần tử trong mảng được ánh xạ tới một thẻ `<style>` mới được tạo, nơi các thuộc tính đối tượng được ánh xạ tới các thuộc tính tương ứng.
  - **Type**: `Array<Record<string, any>>`
- `script`: Mỗi phần tử trong mảng được ánh xạ tới một thẻ `<script>` mới được tạo, nơi các thuộc tính đối tượng được ánh xạ tới các thuộc tính tương ứng.
  - **Type**: `Array<Record<string, any>>`
- `noscript`: Mỗi phần tử trong mảng được ánh xạ tới một thẻ `<noscript>` mới được tạo, nơi các thuộc tính đối tượng được ánh xạ tới các thuộc tính tương ứng.
  - **Type**: `Array<Record<string, any>>`
- `titleTemplate`: Cấu hình mẫu động để tùy chỉnh tiêu đề trang trên một trang riêng lẻ.
  - **Type**: `string` | `((title: string) => string)`
- `title`: Đặt tiêu đề trang tĩnh trên một trang riêng lẻ.
  - **Type**: `string`
- `bodyAttrs`: Đặt các thuộc tính của thẻ `<body>`. Mỗi thuộc tính đối tượng được ánh xạ tới thuộc tính tương ứng.
  - **Type**: `Record<string, any>`
- `htmlAttrs`: Đặt các thuộc tính của thẻ `<html>`. Mỗi thuộc tính đối tượng được ánh xạ tới thuộc tính tương ứng.
  - **Type**: `Record<string, any>`
