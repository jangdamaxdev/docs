---
title: 'useFetch'
description: 'Fetch dữ liệu từ một API endpoint với một composable thân thiện với SSR.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/fetch.ts
    size: xs
---

Composable này cung cấp một wrapper tiện lợi xung quanh [`useAsyncData`](/docs/api/composables/use-async-data) và [`$fetch`](/docs/api/utils/dollarfetch).

Nó tự động generate một key dựa trên URL và fetch options, cung cấp type hints cho request url dựa trên server routes, và infers API response type.

::note
`useFetch` là một composable được thiết kế để được gọi trực tiếp trong một setup function, plugin, hoặc route middleware. Nó trả về các composables reactive và xử lý việc thêm responses vào Nuxt payload để chúng có thể được truyền từ server sang client mà không re-fetch dữ liệu trên client side khi trang hydrate.
::

## Usage

```vue [pages/modules.vue]
<script setup lang="ts">
const { data, status, error, refresh, clear } = await useFetch('/api/modules', {
  pick: ['title']
})
</script>
```

::warning
Nếu bạn đang sử dụng một useFetch wrapper tùy chỉnh, không await nó trong composable, vì điều đó có thể gây ra hành vi không mong muốn. Vui lòng làm theo [recipe này](/docs/guide/recipes/custom-usefetch#custom-usefetch) để biết thêm thông tin về cách tạo một custom async data fetcher.
::

::note
`data`, `status`, và `error` là Vue refs, và chúng nên được truy cập với `.value` khi được sử dụng trong `<script setup>`, trong khi `refresh`/`execute` và `clear` là các hàm plain.
::

Sử dụng option `query`, bạn có thể thêm search parameters vào query của bạn. Option này được extended từ [unjs/ofetch](https://github.com/unjs/ofetch) và sử dụng [unjs/ufo](https://github.com/unjs/ufo) để tạo URL. Objects được tự động stringified.

```ts
const param1 = ref('value1')
const { data, status, error, refresh } = await useFetch('/api/modules', {
  query: { param1, param2: 'value2' }
})
```

Ví dụ trên results in `https://api.nuxt.com/modules?param1=value1&param2=value2`.

Bạn cũng có thể sử dụng [interceptors](https://github.com/unjs/ofetch#%EF%B8%8F-interceptors):

```ts
const { data, status, error, refresh, clear } = await useFetch('/api/auth/login', {
  onRequest({ request, options }) {
    // Set the request headers
    // note that this relies on ofetch >= 1.4.0 - you may need to refresh your lockfile
    options.headers.set('Authorization', '...')
  },
  onRequestError({ request, options, error }) {
    // Handle the request errors
  },
  onResponse({ request, response, options }) {
    // Process the response data
    localStorage.setItem('token', response._data.token)
  },
  onResponseError({ request, response, options }) {
    // Handle the response errors
  }
})
```

### Reactive Keys và Shared State

Bạn có thể sử dụng một computed ref hoặc một plain ref làm URL, cho phép fetching dữ liệu động tự động cập nhật khi URL thay đổi:

```vue [pages/[id\\].vue]
<script setup lang="ts">
const route = useRoute()
const id = computed(() => route.params.id)

// Khi route thay đổi và id cập nhật, dữ liệu sẽ được tự động refetched
const { data: post } = await useFetch(() => `/api/posts/${id.value}`)
</script>
```

Khi sử dụng `useFetch` với cùng URL và options trong multiple components, chúng sẽ share cùng `data`, `error` và `status` refs. Điều này đảm bảo consistency trên components.

::tip
Keyed state được tạo bằng `useFetch` có thể được retrieved trên Nuxt application của bạn bằng [`useNuxtData`](/docs/api/composables/use-nuxt-data).
::

::warning
`useFetch` là một function name được reserved được transformed bởi compiler, vì vậy bạn không nên đặt tên cho function của riêng bạn là `useFetch`.
::

::warning
Nếu bạn encounter variable `data` destructured từ một `useFetch` returns một string và không phải là JSON parsed object thì đảm bảo component của bạn không include một import statement như `import { useFetch } from '@vueuse/core`.
::

:video-accordion{title="Xem video từ Alexander Lichter để tránh sử dụng useFetch theo cách sai" videoId="njsGVmcWviY"}

:read-more{to="/docs/getting-started/data-fetching"}

## Type

```ts [Signature]
function useFetch<DataT, ErrorT>(
  url: string | Request | Ref<string | Request> | (() => string | Request),
  options?: UseFetchOptions<DataT>
): Promise<AsyncData<DataT, ErrorT>>

type UseFetchOptions<DataT> = {
  key?: MaybeRefOrGetter<string>
  method?: string
  query?: SearchParams
  params?: SearchParams
  body?: RequestInit['body'] | Record<string, any>
  headers?: Record<string, string> | [key: string, value: string][] | Headers
  baseURL?: string
  server?: boolean
  lazy?: boolean
  immediate?: boolean
  getCachedData?: (key: string, nuxtApp: NuxtApp, ctx: AsyncDataRequestContext) => DataT | undefined
  deep?: boolean
  dedupe?: 'cancel' | 'defer'
  default?: () => DataT
  transform?: (input: DataT) => DataT | Promise<DataT>
  pick?: string[]
  $fetch?: typeof globalThis.$fetch
  watch?: MultiWatchSources | false
}

type AsyncDataRequestContext = {
  /** Lý do cho data request này */
  cause: 'initial' | 'refresh:manual' | 'refresh:hook' | 'watch'
}

type AsyncData<DataT, ErrorT> = {
  data: Ref<DataT | undefined>
  refresh: (opts?: AsyncDataExecuteOptions) => Promise<void>
  execute: (opts?: AsyncDataExecuteOptions) => Promise<void>
  clear: () => void
  error: Ref<ErrorT | undefined>
  status: Ref<AsyncDataRequestStatus>
}

interface AsyncDataExecuteOptions {
  dedupe?: 'cancel' | 'defer'
}

type AsyncDataRequestStatus = 'idle' | 'pending' | 'success' | 'error'
```

## Parameters

- `URL` (`string | Request | Ref<string | Request> | () => string | Request`): URL hoặc request để fetch. Có thể là string, Request object, Vue ref, hoặc function returning string/Request. Supports reactivity cho dynamic endpoints.

- `options` (object): Configuration cho fetch request. Extends [unjs/ofetch](https://github.com/unjs/ofetch) options và [`AsyncDataOptions`](/docs/api/composables/use-async-data#params). Tất cả options có thể là static value, `ref`, hoặc computed value.

| Option | Type | Default | Description |
| ---| --- | --- | --- |
| `key` | `MaybeRefOrGetter<string>` | auto-gen | Unique key cho de-duplication. Nếu không provided, generated từ URL và options. |
| `method` | `string` | `'GET'` | HTTP request method. |
| `query` | `object` | - | Query/search params để append vào URL. Alias: `params`. Supports refs/computed. |
| `params` | `object` | - | Alias cho `query`. |
| `body` | `RequestInit['body'] \| Record<string, any>` | - | Request body. Objects được tự động stringified. Supports refs/computed. |
| `headers` | `Record<string, string> \| [key, value][] \| Headers` | - | Request headers. |
| `baseURL` | `string` | - | Base URL cho request. |
| `timeout` | `number` | - | Timeout in milliseconds để abort request. |
| `cache` | `boolean \| string` | - | Cache control. Boolean disables cache, hoặc use Fetch API values: `default`, `no-store`, etc. |
| `server` | `boolean` | `true` | Có fetch trên server hay không. |
| `lazy` | `boolean` | `false` | Nếu true, resolves sau khi loading route (không block navigation). |
| `immediate` | `boolean` | `true` | Nếu false, prevents request firing ngay lập tức. |
| `default` | `() => DataT` | - | Factory cho default value của `data` trước khi async resolves. |
| `transform` | `(input: DataT) => DataT \| Promise<DataT>` | - | Function để transform result sau khi resolving. |
| `getCachedData`| `(key, nuxtApp, ctx) => DataT \| undefined` | - | Function để return cached data. Xem dưới cho default. |
| `pick` | `string[]` | - | Chỉ pick specified keys từ result. |
| `watch` | `MultiWatchSources \| false` | - | Array của reactive sources để watch và auto-refresh. `false` disables watching. |
| `deep` | `boolean` | `false` | Return data trong deep ref object. |
| `dedupe` | `'cancel' \| 'defer'` | `'cancel'` | Tránh fetching cùng key nhiều hơn một lần tại một thời điểm. |
| `$fetch` | `typeof globalThis.$fetch` | - | Custom $fetch implementation. |

::note
Tất cả fetch options có thể được given một `computed` hoặc `ref` value. Những cái này sẽ được watched và new requests made tự động với bất kỳ new values nào nếu chúng được updated.
::

**getCachedData default:**

```ts
const getDefaultCachedData = (key, nuxtApp, ctx) => nuxtApp.isHydrating 
  ? nuxtApp.payload.data[key] 
  : nuxtApp.static.data[key]
```

Chỉ cache data khi `experimental.payloadExtraction` trong `nuxt.config` được enabled.

## Return Values

| Name | Type | Description |
| --- | --- |--- |
| `data` | `Ref<DataT \| undefined>` | Kết quả của asynchronous fetch. |
| `refresh` | `(opts?: AsyncDataExecuteOptions) => Promise<void>` | Function để manually refresh data. Theo mặc định, Nuxt waits cho đến khi một `refresh` hoàn thành trước khi nó có thể được execute lại. |
| `execute` | `(opts?: AsyncDataExecuteOptions) => Promise<void>` | Alias cho `refresh`. |
| `error` | `Ref<ErrorT \| undefined>` | Error object nếu data fetching thất bại. |
| `status` | `Ref<'idle' \| 'pending' \| 'success' \| 'error'>` | Status của data request. Xem dưới cho possible values. |
| `clear` | `() => void` | Resets `data` thành `undefined` (hoặc giá trị của `options.default()` nếu provided), `error` thành `undefined`, set `status` thành `idle`, và cancels bất kỳ pending requests hiện tại nào. |

### Status values

- `idle`: Request chưa bắt đầu (e.g. `{ immediate: false }` hoặc `{ server: false }` trên server render)
- `pending`: Request đang trong tiến trình
- `success`: Request hoàn thành thành công
- `error`: Request thất bại

::note
Nếu bạn chưa fetch data trên server (ví dụ, với `server: false`), thì data _sẽ không_ được fetch cho đến khi hydration hoàn thành. Điều này có nghĩa là ngay cả khi bạn await `useFetch` trên client-side, `data` sẽ vẫn là null trong `<script setup>`.
::

### Examples

:link-example{to="/docs/examples/advanced/use-custom-fetch-composable"}

:link-example{to="/docs/examples/features/data-fetching"}
