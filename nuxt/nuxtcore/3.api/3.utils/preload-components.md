---
title: 'preloadComponents'
description: Nuxt provides utilities to give you control over preloading components.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/preload.ts
    size: xs
---

Việc preloading components tải các components mà trang của bạn sẽ cần rất sớm, mà bạn muốn bắt đầu tải sớm trong vòng đời render. Điều này đảm bảo chúng có sẵn sớm hơn và ít có khả năng chặn việc render trang, cải thiện hiệu suất.

Sử dụng `preloadComponents` để preload thủ công các component riêng lẻ đã được đăng ký toàn cục trong ứng dụng Nuxt của bạn. Theo mặc định, Nuxt đăng ký chúng như các async components. Bạn phải sử dụng phiên bản Pascal-cased của tên component.

```js
await preloadComponents('MyGlobalComponent')

await preloadComponents(['MyGlobalComponent1', 'MyGlobalComponent2'])
```

::note
Trên server, `preloadComponents` sẽ không có hiệu lực.
::
