---
title: 'prerenderRoutes'
description: prerenderRoutes hints to Nitro to prerender an additional route.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/ssr.ts
    size: xs
---

Khi prerendering, bạn có thể gợi ý cho Nitro prerender các đường dẫn bổ sung, ngay cả khi URL của chúng không xuất hiện trong HTML của trang được tạo.

::important
`prerenderRoutes` chỉ có thể được gọi trong [Nuxt context](/docs/guide/going-further/nuxt-app#the-nuxt-context).
::

::note
`prerenderRoutes` phải được thực thi trong quá trình prerendering. Nếu `prerenderRoutes` được sử dụng trong các trang/routes động không được prerender, thì nó sẽ không được thực thi.
::

```js
const route = useRoute()

prerenderRoutes('/')
prerenderRoutes(['/', '/about'])
```

::note
Trong trình duyệt, hoặc nếu được gọi bên ngoài prerendering, `prerenderRoutes` sẽ không có hiệu lực.
::

Bạn thậm chí có thể prerender các API routes, điều này đặc biệt hữu ích cho các trang web được tạo tĩnh hoàn toàn (SSG) vì bạn có thể `$fetch` dữ liệu như thể có một server khả dụng!

```js
prerenderRoutes('/api/content/article/name-of-article')

// Ở đâu đó sau này trong App
const articleContent = await $fetch('/api/content/article/name-of-article', {
  responseType: 'json',
})
```

::warning
Các API routes được prerender trong production có thể không trả về các header phản hồi mong đợi, tùy thuộc vào nhà cung cấp bạn triển khai. Ví dụ, một phản hồi JSON có thể được phục vụ với loại content `application/octet-stream`.
Luôn đặt `responseType` thủ công khi fetch các API routes được prerender.
::
