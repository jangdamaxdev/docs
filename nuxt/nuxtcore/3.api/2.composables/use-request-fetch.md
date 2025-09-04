---
title: 'useRequestFetch'
description: 'Chuyển tiếp ngữ cảnh request và headers cho các yêu cầu fetch server-side với composable useRequestFetch.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/ssr.ts
    size: xs
---

Bạn có thể sử dụng `useRequestFetch` để chuyển tiếp ngữ cảnh request và headers khi thực hiện các yêu cầu fetch server-side.

Khi thực hiện yêu cầu fetch client-side, browser tự động gửi các headers cần thiết.

Tuy nhiên, khi thực hiện yêu cầu trong quá trình server-side rendering, do các cân nhắc bảo mật, chúng ta cần chuyển tiếp headers thủ công.

::note
Headers mà **không được thiết kế để chuyển tiếp** sẽ **không được bao gồm** trong yêu cầu. Các headers này bao gồm, ví dụ:

`transfer-encoding`, `connection`, `keep-alive`, `upgrade`, `expect`, `host`, `accept`
::

::tip
Composable [`useFetch`](/docs/api/composables/use-fetch) sử dụng `useRequestFetch` under the hood để tự động chuyển tiếp ngữ cảnh request và headers.
::

::code-group

```vue [pages/index.vue]
<script setup lang="ts">
// This will forward the user's headers to the `/api/cookies` event handler
// Result: { cookies: { foo: 'bar' } }
const requestFetch = useRequestFetch()
const { data: forwarded } = await useAsyncData(() => requestFetch('/api/cookies'))

// This will NOT forward anything
// Result: { cookies: {} }
const { data: notForwarded } = await useAsyncData(() => $fetch('/api/cookies')) 
</script>
```

```ts [server/api/cookies.ts]
export default defineEventHandler((event) => {
  const cookies = parseCookies(event)

  return { cookies }
})
```

::

::tip
Trong browser trong quá trình navigation client-side, `useRequestFetch` sẽ hoạt động giống như [`$fetch`](/docs/api/utils/dollarfetch) thông thường.
::
