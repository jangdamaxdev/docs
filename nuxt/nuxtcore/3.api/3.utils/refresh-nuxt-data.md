---
title: 'refreshNuxtData'
description: Refresh all or specific asyncData instances in Nuxt
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/asyncData.ts
    size: xs
---

`refreshNuxtData` được sử dụng để refetch tất cả hoặc các instance `asyncData` cụ thể, bao gồm những instance từ [`useAsyncData`](/docs/api/composables/use-async-data), [`useLazyAsyncData`](/docs/api/composables/use-lazy-async-data), [`useFetch`](/docs/api/composables/use-fetch), và [`useLazyFetch`](/docs/api/composables/use-lazy-fetch).

::note
Nếu component của bạn được cache bởi `<KeepAlive>` và vào trạng thái deactivated, `asyncData` bên trong component vẫn sẽ được refetch cho đến khi component bị unmount.
::

## Type

```ts
refreshNuxtData(keys?: string | string[])
```

## Parameters

* `keys`: Một chuỗi đơn hoặc mảng các chuỗi làm `keys` được sử dụng để fetch dữ liệu. Tham số này là **tùy chọn**. Tất cả keys [`useAsyncData`](/docs/api/composables/use-async-data) và [`useFetch`](/docs/api/composables/use-fetch) được re-fetch khi không có `keys` nào được chỉ định rõ ràng.

## Return Values

`refreshNuxtData` trả về một promise, resolve khi tất cả hoặc các instance `asyncData` cụ thể đã được làm mới.

## Examples

### Refresh All Data

Ví dụ dưới đây làm mới tất cả dữ liệu đang được fetch bằng `useAsyncData` và `useFetch` trong ứng dụng Nuxt.

```vue [pages/some-page.vue]
<script setup lang="ts">
const refreshing = ref(false)

async function refreshAll () {
  refreshing.value = true
  try {
    await refreshNuxtData()
  } finally {
    refreshing.value = false
  }
}
</script>

<template>
  <div>
    <button :disabled="refreshing" @click="refreshAll">
      Refetch Tất Cả Dữ Liệu
    </button>
  </div>
</template>
```

### Refresh Specific Data

Ví dụ dưới đây chỉ làm mới dữ liệu nơi key khớp với `count` và `user`.

```vue [pages/some-page.vue]
<script setup lang="ts">
const refreshing = ref(false)

async function refresh () {
  refreshing.value = true
  try {
    // bạn cũng có thể truyền một mảng các keys để làm mới nhiều dữ liệu
    await refreshNuxtData(['count', 'user'])
  } finally {
    refreshing.value = false
  }
}
</script>

<template>
  <div v-if="refreshing">
    Đang tải
  </div>
  <button @click="refresh">Refresh</button>
</template>
```

::note
Nếu bạn có quyền truy cập vào instance `asyncData`, bạn nên sử dụng phương thức `refresh` hoặc `execute` của nó như cách ưu tiên để refetch dữ liệu.
::

:read-more{to="/docs/getting-started/data-fetching"}
