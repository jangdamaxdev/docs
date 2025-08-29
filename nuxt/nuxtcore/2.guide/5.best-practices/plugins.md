---
navigation.title: 'Nuxt Plugins'
title: Nuxt Plugins
description: Best practices when using Nuxt plugins.
---

Plugins trong Nuxt allow bạn để extend application của bạn với additional functionality. Tuy nhiên, improper use can lead đến performance bottlenecks. Guide này outlines best practices để optimize Nuxt plugins của bạn.

## Avoid costly plugin setup

Một large number của plugins can cause performance issues, especially if chúng require expensive computations hoặc take too long để initialize. Since plugins run during hydration phase, inefficient setups can block rendering và degrade user experience.

## Use Composition whenever possible

Whenever possible, favor composition over plugins. Just like trong Vue, many utilities và composables can be used directly without need cho một plugin. Điều này keeps project của bạn lightweight và improves maintainability.

## If `async`, enable `parallel`

By default, tất cả plugins loads synchronously.
Khi defining asynchronous plugins, setting `parallel: true` allows multiple plugins để load concurrently, improving performance bằng preventing blocking operations.
