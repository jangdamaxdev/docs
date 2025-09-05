---
title: 'prefetchComponents'
description: Nuxt provides utilities to give you control over prefetching components.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/preload.ts
    size: xs
---


Việc prefetching component tải xuống mã code trong nền, điều này dựa trên giả định rằng component có khả năng sẽ được sử dụng để render, cho phép component tải ngay lập tức nếu và khi người dùng yêu cầu. Component được tải xuống và lưu cache cho việc sử dụng tương lai dự kiến mà không cần người dùng thực hiện yêu cầu rõ ràng.

Sử dụng `prefetchComponents` để prefetch thủ công các component riêng lẻ đã được đăng ký toàn cục trong ứng dụng Nuxt của bạn. Theo mặc định, Nuxt đăng ký chúng như các async components. Bạn phải sử dụng phiên bản Pascal-cased của tên component.

```ts
await prefetchComponents('MyGlobalComponent')

await prefetchComponents(['MyGlobalComponent1', 'MyGlobalComponent2'])
```

::note
Việc triển khai hiện tại hoạt động giống hệt như [`preloadComponents`](/docs/api/utils/preload-components) bằng cách preload components thay vì chỉ prefetch, chúng tôi đang làm việc để cải thiện hành vi này.
::

::note
Trên server, `prefetchComponents` sẽ không có hiệu lực.
::
