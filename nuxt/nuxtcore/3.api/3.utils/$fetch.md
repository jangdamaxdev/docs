---
title: "$fetch"
description: Nuxt sử dụng ofetch để hiển thị toàn cầu trình trợ giúp $fetch để thực hiện các yêu cầu HTTP.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/entry.ts
    size: xs
---

Nuxt sử dụng [ofetch](https://github.com/unjs/ofetch) để hiển thị toàn cầu trình trợ giúp `$fetch` để thực hiện các yêu cầu HTTP trong ứng dụng Vue hoặc các tuyến API của bạn.

::tip{icon="i-lucide-rocket"}
Trong quá trình kết xuất phía máy chủ, việc gọi `$fetch` để lấy dữ liệu từ các [tuyến API](/docs/guide/directory-structure/server) nội bộ của bạn sẽ trực tiếp gọi hàm liên quan (mô phỏng yêu cầu), **tiết kiệm một cuộc gọi API bổ sung**.
::

::note{color="blue" icon="i-lucide-info"}
Sử dụng `$fetch` trong các thành phần mà không bao bọc nó bằng [`useAsyncData`](/docs/api/composables/use-async-data) khiến việc lấy dữ liệu hai lần: ban đầu trên máy chủ, sau đó lại trên phía máy khách trong quá trình hydrat hóa, vì `$fetch` không chuyển trạng thái từ máy chủ sang máy khách. Do đó, việc lấy dữ liệu sẽ được thực hiện ở cả hai phía vì máy khách phải lấy dữ liệu lại.
::

## Usage

Chúng tôi khuyên dùng [`useFetch`](/docs/api/composables/use-fetch) hoặc [`useAsyncData`](/docs/api/composables/use-async-data) + `$fetch` để ngăn chặn việc lấy dữ liệu hai lần khi lấy dữ liệu thành phần.

```vue [app.vue]
<script setup lang="ts">
// During SSR data is fetched twice, once on the server and once on the client.
const dataTwice = await $fetch('/api/item')

// During SSR data is fetched only on the server side and transferred to the client.
const { data } = await useAsyncData('item', () => $fetch('/api/item'))

// You can also useFetch as shortcut of useAsyncData + $fetch
const { data } = await useFetch('/api/item')
</script>
```

:read-more{to="/docs/getting-started/data-fetching"}

Bạn có thể sử dụng `$fetch` trong bất kỳ phương thức nào chỉ được thực hiện ở phía máy khách.

```vue [pages/contact.vue]
<script setup lang="ts">
async function contactForm() {
  await $fetch('/api/contact', {
    method: 'POST',
    body: { hello: 'world '}
  })
}
</script>

<template>
  <button @click="contactForm">Contact</button>
</template>
```

::tip
`$fetch` là cách ưu tiên để thực hiện các cuộc gọi HTTP trong Nuxt thay vì [@nuxt/http](https://github.com/nuxt/http) và [@nuxtjs/axios](https://github.com/nuxt-community/axios-module) được tạo cho Nuxt 2.
::

::note
Nếu bạn sử dụng `$fetch` để gọi một URL HTTPS (bên ngoài) với chứng chỉ tự ký trong quá trình phát triển, bạn sẽ cần đặt `NODE_TLS_REJECT_UNAUTHORIZED=0` trong môi trường của mình.
::

### Passing Headers and Cookies

Khi chúng ta gọi `$fetch` trong trình duyệt, các tiêu đề người dùng như `cookie` sẽ được gửi trực tiếp đến API.

Tuy nhiên, trong quá trình Kết xuất Phía Máy chủ, do các rủi ro bảo mật như **Server-Side Request Forgery (SSRF)** hoặc **Lạm dụng Xác thực**, `$fetch` sẽ không bao gồm cookie của trình duyệt người dùng, cũng không chuyển tiếp cookie từ phản hồi lấy dữ liệu.

::code-group

```vue [pages/index.vue]
<script setup lang="ts">
// This will NOT forward headers or cookies during SSR
const { data } = await useAsyncData(() => $fetch('/api/cookies'))
</script>
```

```ts [server/api/cookies.ts]
export default defineEventHandler((event) => {
  const foo = getCookie(event, 'foo')
  // ... Do something with the cookie
})
```

::

Nếu bạn cần chuyển tiếp tiêu đề và cookie trên máy chủ, bạn phải truyền chúng theo cách thủ công:

```vue [pages/index.vue]
<script setup lang="ts">
// This will forward the user's headers and cookies to `/api/cookies`
const requestFetch = useRequestFetch()
const { data } = await useAsyncData(() => requestFetch('/api/cookies'))
</script>
```

Tuy nhiên, khi gọi `useFetch` với một URL tương đối trên máy chủ, Nuxt sẽ sử dụng [`useRequestFetch`](/docs/api/composables/use-request-fetch) để proxy tiêu đề và cookie (với ngoại lệ các tiêu đề không được chuyển tiếp, như `host`).
