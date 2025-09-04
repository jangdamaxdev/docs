---
navigation.title: 'Nuxt Plugins'
title: Nuxt Plugins
description: Best practices when using Nuxt plugins.
---

Plugins trong Nuxt cho phép bạn mở rộng ứng dụng của bạn với chức năng bổ sung. Tuy nhiên, việc sử dụng không đúng cách có thể dẫn đến tắc nghẽn hiệu suất. Hướng dẫn này nêu ra các thực tiễn tốt nhất để tối ưu hóa plugins Nuxt của bạn.

## Avoid costly plugin setup

Một số lượng lớn plugins có thể gây ra vấn đề hiệu suất, đặc biệt nếu chúng yêu cầu expensive computations hoặc mất quá nhiều thời gian để initialize. Vì plugins chạy trong hydration phase, inefficient setups có thể block rendering và degrade trải nghiệm người dùng.

## Use Composition whenever possible

Bất cứ khi nào có thể, ưu tiên composition over plugins. Giống như trong Vue, nhiều utilities và composables có thể được sử dụng trực tiếp mà không cần plugin. Điều này giữ cho project của bạn lightweight và cải thiện maintainability.

## If `async`, enable `parallel`

Theo mặc định, tất cả plugins load synchronously.
Khi định nghĩa asynchronous plugins, setting `parallel: true` cho phép multiple plugins load concurrently, cải thiện hiệu suất bằng cách ngăn chặn blocking operations.
