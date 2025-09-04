---
title: 'useRuntimeConfig'
description: 'Truy cập các biến config runtime với composable useRuntimeConfig.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/nuxt.ts
    size: xs
---

## Usage

```vue [app.vue]
<script setup lang="ts">
const config = useRuntimeConfig()
</script>
```

```ts [server/api/foo.ts]
export default defineEventHandler((event) => {
  const config = useRuntimeConfig(event)
})
```

:read-more{to="/docs/guide/going-further/runtime-config"}

## Define Runtime Config

Ví dụ dưới đây cho thấy cách thiết lập một public API base URL và một secret API token chỉ có thể truy cập trên server.

Chúng ta nên luôn định nghĩa các biến `runtimeConfig` bên trong `nuxt.config`.

```ts [nuxt.config.ts]
export default defineNuxtConfig({
  runtimeConfig: {
    // Private keys are only available on the server
    apiSecret: '123',

    // Public keys that are exposed to the client
    public: {
      apiBase: process.env.NUXT_PUBLIC_API_BASE || '/api'
    }
  }
})
```

::note
Các biến cần truy cập trên server được thêm trực tiếp bên trong `runtimeConfig`. Các biến cần truy cập trên cả client và server được định nghĩa trong `runtimeConfig.public`.
::

:read-more{to="/docs/guide/going-further/runtime-config"}

## Access Runtime Config

Để truy cập runtime config, chúng ta có thể sử dụng composable `useRuntimeConfig()`:

```ts [server/api/test.ts]
export default defineEventHandler(async (event) => {
  const config = useRuntimeConfig(event)

  // Access public variables
  const result = await $fetch(`/test`, {
    baseURL: config.public.apiBase,
    headers: {
      // Access a private variable (only available on the server)
      Authorization: `Bearer ${config.apiSecret}`
    }
  })
  return result
}
```

Trong ví dụ này, vì `apiBase` được định nghĩa trong namespace `public`, nó có thể truy cập universally trên cả server và client-side, trong khi `apiSecret` **chỉ có thể truy cập trên server-side**.

## Environment Variables

Có thể cập nhật các giá trị runtime config bằng cách sử dụng tên biến môi trường khớp với prefix `NUXT_`.

:read-more{to="/docs/guide/going-further/runtime-config"}

### Using the `.env` File

Chúng ta có thể thiết lập các biến môi trường bên trong file `.env` để làm cho chúng có thể truy cập trong quá trình **development** và **build/generate**.

```ini [.env]
NUXT_PUBLIC_API_BASE = "https://api.localhost:5555"
NUXT_API_SECRET = "123"
```

::note
Bất kỳ biến môi trường nào được thiết lập trong file `.env` được truy cập bằng `process.env` trong Nuxt app trong quá trình **development** và **build/generate**.
::

::warning
Trong **production runtime**, bạn nên sử dụng platform environment variables và `.env` không được sử dụng.
::

:read-more{to="/docs/guide/directory-structure/env"}

## `app` namespace

Nuxt sử dụng namespace `app` trong runtime-config với các keys bao gồm `baseURL` và `cdnURL`. Bạn có thể tùy chỉnh các giá trị của chúng tại runtime bằng cách thiết lập environment variables.

::note
Đây là một namespace reserved. Bạn không nên giới thiệu các keys bổ sung bên trong `app`.
::

### `app.baseURL`

Theo mặc định, `baseURL` được thiết lập thành `'/'`.

Tuy nhiên, `baseURL` có thể được cập nhật tại runtime bằng cách thiết lập `NUXT_APP_BASE_URL` làm environment variable.

Sau đó, bạn có thể truy cập base URL mới này bằng `config.app.baseURL`:

```ts [/plugins/my-plugin.ts]
export default defineNuxtPlugin((NuxtApp) => {
  const config = useRuntimeConfig()

  // Access baseURL universally
  const baseURL = config.app.baseURL
})
```

### `app.cdnURL`

Ví dụ này cho thấy cách thiết lập một custom CDN url và truy cập chúng bằng `useRuntimeConfig()`.

Bạn có thể sử dụng một custom CDN để serve static assets bên trong `.output/public` bằng environment variable `NUXT_APP_CDN_URL`.

Và sau đó truy cập CDN url mới bằng `config.app.cdnURL`.

```ts [server/api/foo.ts]
export default defineEventHandler((event) => {
  const config = useRuntimeConfig(event)

  // Access cdnURL universally
  const cdnURL = config.app.cdnURL
})
```

:read-more{to="/docs/guide/going-further/runtime-config"}
