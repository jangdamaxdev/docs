---
title: "useRouter"
description: "Composable useRouter trả về instance router."
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/router.ts
    size: xs
---

```vue [pages/index.vue]
<script setup lang="ts">
const router = useRouter()
</script>
```

Nếu bạn chỉ cần instance router trong template của bạn, sử dụng `$router`:

```vue [pages/index.vue]
<template>
  <button @click="$router.back()">Back</button>
</template>
```

Nếu bạn có thư mục `pages/`, `useRouter` có hành vi giống hệt với cái được cung cấp bởi `vue-router`.

::read-more{icon="i-simple-icons-vuedotjs" to="https://router.vuejs.org/api/interfaces/Router.html#Properties-currentRoute" target="_blank"}
Đọc `vue-router` documentation về `Router` interface.
::

## Basic Manipulation

- [`addRoute()`](https://router.vuejs.org/api/interfaces/Router.html#addRoute): Thêm một route mới vào instance router. `parentName` có thể được cung cấp để thêm route mới làm con của một route hiện có.
- [`removeRoute()`](https://router.vuejs.org/api/interfaces/Router.html#removeRoute): Xóa một route hiện có theo tên của nó.
- [`getRoutes()`](https://router.vuejs.org/api/interfaces/Router.html#getRoutes): Lấy danh sách đầy đủ của tất cả các route records.
- [`hasRoute()`](https://router.vuejs.org/api/interfaces/Router.html#hasRoute): Kiểm tra xem một route với tên đã cho có tồn tại hay không.
- [`resolve()`](https://router.vuejs.org/api/interfaces/Router.html#resolve): Trả về phiên bản normalized của vị trí route. Cũng bao gồm thuộc tính `href` bao gồm bất kỳ base nào hiện có.

```ts [Example]
const router = useRouter()

router.addRoute({ name: 'home', path: '/home', component: Home })
router.removeRoute('home')
router.getRoutes()
router.hasRoute('home')
router.resolve({ name: 'home' })
```

::note
`router.addRoute()` thêm chi tiết route vào một mảng các routes và nó hữu ích khi xây dựng [Nuxt plugins](/docs/guide/directory-structure/plugins) trong khi `router.push()` mặt khác, trigger một navigation mới ngay lập tức và nó hữu ích trong pages, Vue components và composable.
::

## Based on History API

- [`back()`](https://router.vuejs.org/api/interfaces/Router.html#back): Quay lại trong history nếu có thể, giống như `router.go(-1)`.
- [`forward()`](https://router.vuejs.org/api/interfaces/Router.html#forward): Tiến về phía trước trong history nếu có thể, giống như `router.go(1)`.
- [`go()`](https://router.vuejs.org/api/interfaces/Router.html#go): Di chuyển về phía trước hoặc phía sau qua history mà không có các hạn chế hierarchical được thực thi trong `router.back()` và `router.forward()`.
- [`push()`](https://router.vuejs.org/api/interfaces/Router.html#push): Programmatically navigate đến một URL mới bằng cách push một entry trong history stack. **Khuyến nghị sử dụng [`navigateTo`](/docs/api/utils/navigate-to) thay thế.**
- [`replace()`](https://router.vuejs.org/api/interfaces/Router.html#replace): Programmatically navigate đến một URL mới bằng cách thay thế entry hiện tại trong routes history stack. **Khuyến nghị sử dụng [`navigateTo`](/docs/api/utils/navigate-to) thay thế.**

```ts [Example]
const router = useRouter()

router.back()
router.forward()
router.go(3)
router.push({ path: "/home" })
router.replace({ hash: "#bio" })
```

::read-more{icon="i-simple-icons-mdnwebdocs" to="https://developer.mozilla.org/en-US/docs/Web/API/History" target="_blank"}
Đọc thêm về browser's History API.
::

## Navigation Guards

Composable `useRouter` cung cấp các phương thức trợ giúp `afterEach`, `beforeEach` và `beforeResolve` hoạt động như navigation guards.

Tuy nhiên, Nuxt có khái niệm **route middleware** giúp đơn giản hóa việc triển khai navigation guards và cung cấp trải nghiệm developer tốt hơn.

:read-more{to="/docs/guide/directory-structure/middleware"}

## Promise and Error Handling

- [`isReady()`](https://router.vuejs.org/api/interfaces/Router.html#isReady): Trả về một Promise resolve khi router đã hoàn thành navigation ban đầu.
- [`onError`](https://router.vuejs.org/api/interfaces/Router.html#onError): Thêm một error handler được gọi mỗi lần một lỗi không được catch xảy ra trong quá trình navigation.

:read-more{icon="i-simple-icons-vuedotjs" to="https://router.vuejs.org/api/interfaces/Router.html#Methods" title="Vue Router Docs" target="_blank"}

## Universal Router Instance

Nếu bạn không có thư mục `pages/`, thì [`useRouter`](/docs/api/composables/use-router) sẽ trả về một universal router instance với các phương thức trợ giúp tương tự, nhưng lưu ý rằng không phải tất cả các tính năng có thể được hỗ trợ hoặc hoạt động chính xác giống như với `vue-router`.
