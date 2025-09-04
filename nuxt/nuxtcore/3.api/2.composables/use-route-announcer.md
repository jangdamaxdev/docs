---
title: 'useRouteAnnouncer'
description: Composable này quan sát các thay đổi tiêu đề trang và cập nhật thông báo announcer tương ứng.
navigation:
  badge: New
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/route-announcer.ts
    size: xs
---

::important
Composable này khả dụng trong Nuxt v3.12+.
::

## Description

Một composable quan sát các thay đổi tiêu đề trang và cập nhật thông báo announcer tương ứng. Được sử dụng bởi [`<NuxtRouteAnnouncer>`](/docs/api/components/nuxt-route-announcer) và có thể kiểm soát.

Nó hook vào [`dom:rendered`](https://unhead.unjs.io/docs/typescript/head/api/hooks/dom-rendered) của Unhead để đọc tiêu đề trang và thiết lập nó làm thông báo announcer.

## Parameters

- `politeness`: Thiết lập mức độ khẩn cấp cho các thông báo screen reader: `off` (tắt thông báo), `polite` (chờ im lặng), hoặc `assertive` (ngắt ngay lập tức). (mặc định `polite`).

## Properties

### `message`

- **type**: `Ref<string>`
- **description**: Thông báo để announce

### `politeness`

- **type**: `Ref<string>`
- **description**: Mức độ khẩn cấp thông báo screen reader `off`, `polite`, hoặc `assertive`

## Methods

### `set(message, politeness = "polite")`

Thiết lập thông báo để announce với mức độ khẩn cấp của nó.

### `polite(message)`

Thiết lập thông báo với `politeness = "polite"`

### `assertive(message)`

Thiết lập thông báo với `politeness = "assertive"`

## Example

```vue [pages/index.vue]
<script setup lang="ts">
  const { message, politeness, set, polite, assertive } = useRouteAnnouncer({
    politeness: 'assertive'
  })
</script>
```
