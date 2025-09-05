---
title: "refreshCookie"
description: "Refresh useCookie values manually when a cookie has changed"
navigation:
  badge: New
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/cookie.ts
    size: xs
---

::important
Tiện ích này có sẵn kể từ [Nuxt v3.10](/blog/v3-10).
::

## Purpose

Hàm `refreshCookie` được thiết kế để làm mới giá trị cookie được trả về bởi `useCookie`.

Điều này hữu ích để cập nhật ref `useCookie` khi chúng ta biết giá trị cookie mới đã được đặt trong trình duyệt.

## Usage

```vue [app.vue]
<script setup lang="ts">
const tokenCookie = useCookie('token')

const login = async (username, password) => {
  const token = await $fetch('/api/token', { ... }) // Sets `token` cookie on response
  refreshCookie('token')
}

const loggedIn = computed(() => !!tokenCookie.value)
</script>
```

::note{to="/docs/guide/going-further/experimental-features#cookiestore"}
Bạn có thể bật tùy chọn `cookieStore` thử nghiệm để tự động làm mới giá trị `useCookie` khi cookie thay đổi trong trình duyệt.
::

## Type

```ts
refreshCookie(name: string): void
```
