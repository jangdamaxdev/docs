---
title: 'useAsyncData'
description: useAsyncData cung cấp quyền truy cập vào dữ liệu được giải quyết bất đồng bộ trong một composable thân thiện với SSR.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/asyncData.ts
    size: xs
---

Trong các pages, components và plugins của bạn, bạn có thể sử dụng useAsyncData để có quyền truy cập vào dữ liệu được giải quyết bất đồng bộ.

::note
[`useAsyncData`](/docs/api/composables/use-async-data) là một composable được thiết kế để được gọi trực tiếp trong [Nuxt context](/docs/guide/going-further/nuxt-app#the-nuxt-context). Nó trả về các composables reactive và xử lý việc thêm responses vào Nuxt payload để chúng có thể được truyền từ server sang client **mà không cần fetch lại dữ liệu trên client side** khi trang hydrate.
::

## Usage

```vue [pages/index.vue]
<script setup lang="ts">
const { data, status, error, refresh, clear } = await useAsyncData(
  'mountains',
  () => $fetch('https://api.nuxtjs.dev/mountains')
)
</script>
```

::warning
Nếu bạn đang sử dụng một useAsyncData wrapper tùy chỉnh, không await nó trong composable, vì điều đó có thể gây ra hành vi không mong muốn. Vui lòng làm theo [recipe này](/docs/guide/recipes/custom-usefetch#custom-usefetch) để biết thêm thông tin về cách tạo một custom async data fetcher.
::

::note
`data`, `status` và `error` là Vue refs và chúng nên được truy cập với `.value` khi được sử dụng trong `<script setup>`, trong khi `refresh`/`execute` và `clear` là các hàm plain.
::

### Watch Params

Option `watch` tích hợp cho phép tự động rerun hàm fetcher khi phát hiện bất kỳ thay đổi nào.

```vue [pages/index.vue]
<script setup lang="ts">
const page = ref(1)
const { data: posts } = await useAsyncData(
  'posts',
  () => $fetch('https://fakeApi.com/posts', {
    params: {
      page: page.value
    }
  }), {
    watch: [page]
  }
)
</script>
```

### Reactive Keys

Bạn có thể sử dụng một computed ref, plain ref hoặc một getter function làm key, cho phép fetching dữ liệu động tự động cập nhật khi key thay đổi:

```vue [pages/[id\\].vue]
<script setup lang="ts">
const route = useRoute()
const userId = computed(() => `user-${route.params.id}`)

// Khi route thay đổi và userId cập nhật, dữ liệu sẽ được tự động refetch
const { data: user } = useAsyncData(
  userId,
  () => fetchUserById(route.params.id)
)
</script>
```

::warning
[`useAsyncData`](/docs/api/composables/use-async-data) là một function name được reserved được transformed bởi compiler, vì vậy bạn không nên đặt tên cho function của riêng bạn là [`useAsyncData`](/docs/api/composables/use-async-data).
::

:read-more{to="/docs/getting-started/data-fetching#useasyncdata"}

## Params

- `key`: một key duy nhất để đảm bảo rằng việc fetching dữ liệu có thể được de-duplicated đúng cách trên các requests. Nếu bạn không cung cấp key, thì một key sẽ được tạo cho bạn duy nhất cho file name và line number của instance của `useAsyncData`.
- `handler`: một hàm asynchronous phải trả về một giá trị truthy (ví dụ, nó không nên là `undefined` hoặc `null`) hoặc request có thể bị duplicated trên client side.
::warning
Hàm `handler` nên là **side-effect free** để đảm bảo hành vi predictable trong SSR và CSR hydration. Nếu bạn cần trigger side effects, hãy sử dụng utility [`callOnce`](/docs/api/utils/call-once) để làm điều đó.
::
- `options`:
  - `server`: có fetch dữ liệu trên server hay không (mặc định là `true`)
  - `lazy`: có resolve hàm async sau khi loading route hay không, thay vì blocking client-side navigation (mặc định là `false`)
  - `immediate`: khi được set thành `false`, sẽ ngăn request firing ngay lập tức. (mặc định là `true`)
  - `default`: một factory function để set giá trị mặc định của `data`, trước khi hàm async resolves - hữu ích với option `lazy: true` hoặc `immediate: false`
  - `transform`: một hàm có thể được sử dụng để alter `handler` function result sau khi resolving
  - `getCachedData`: Cung cấp một hàm trả về cached data. Một return value `null` hoặc `undefined` sẽ trigger một fetch. Theo mặc định, điều này là:
    ```ts
    const getDefaultCachedData = (key, nuxtApp, ctx) => nuxtApp.isHydrating 
      ? nuxtApp.payload.data[key] 
      : nuxtApp.static.data[key]
    ```
    Chỉ cache data khi `experimental.payloadExtraction` của `nuxt.config` được enabled.
  - `pick`: chỉ pick specified keys trong array này từ `handler` function result
  - `watch`: watch reactive sources để auto-refresh
  - `deep`: return data trong một deep ref object. Nó là `false` theo mặc định để return data trong một shallow ref object, có thể cải thiện performance nếu data của bạn không cần reactive deeply.
  - `dedupe`: tránh fetching cùng key nhiều hơn một lần tại một thời điểm (mặc định là `cancel`). Các options có thể:
    - `cancel` - cancels existing requests khi một request mới được thực hiện
    - `defer` - không thực hiện new requests nếu có một pending request

::note
Dưới hood, `lazy: false` sử dụng `<Suspense>` để block loading của route trước khi data đã được fetched. Cân nhắc sử dụng `lazy: true` và implement một loading state thay thế để có user experience mượt mà hơn.
::

:read-more{to="/docs/api/composables/use-lazy-async-data"}
Bạn có thể sử dụng `useLazyAsyncData` để có cùng behavior như `lazy: true` với `useAsyncData`.
::

:video-accordion{title="Xem video từ Alexander Lichter về client-side caching với getCachedData" videoId="aQPR0xn-MMk"}

### Shared State và Option Consistency

Khi sử dụng cùng key cho multiple `useAsyncData` calls, chúng sẽ share cùng `data`, `error` và `status` refs. Điều này đảm bảo consistency trên components nhưng yêu cầu option consistency.

Các options sau **phải consistent** trên tất cả calls với cùng key:
- `handler` function
- `deep` option
- `transform` function
- `pick` array
- `getCachedData` function
- `default` value

Các options sau **có thể khác** mà không trigger warnings:
- `server`
- `lazy`
- `immediate`
- `dedupe`
- `watch`

```ts
// ❌ Điều này sẽ trigger development warning
const { data: users1 } = useAsyncData('users', () => $fetch('/api/users'), { deep: false })
const { data: users2 } = useAsyncData('users', () => $fetch('/api/users'), { deep: true })

// ✅ Điều này được cho phép
const { data: users1 } = useAsyncData('users', () => $fetch('/api/users'), { immediate: true })
const { data: users2 } = useAsyncData('users', () => $fetch('/api/users'), { immediate: false })
```

::tip
Keyed state được tạo bằng `useAsyncData` có thể được retrieved trên Nuxt application của bạn bằng [`useNuxtData`](/docs/api/composables/use-nuxt-data).
::

## Return Values

- `data`: kết quả của hàm asynchronous được truyền vào.
- `refresh`/`execute`: một hàm có thể được sử dụng để refresh data được trả về bởi hàm `handler`.
- `error`: một error object nếu việc fetching data thất bại.
- `status`: một string chỉ ra status của data request:
  - `idle`: khi request chưa bắt đầu, chẳng hạn như:
    - khi `execute` chưa được gọi và `{ immediate: false }` được set
    - khi rendering HTML trên server và `{ server: false }` được set
  - `pending`: request đang trong tiến trình
  - `success`: request đã hoàn thành thành công
  - `error`: request đã thất bại
- `clear`: một hàm có thể được sử dụng để set `data` thành `undefined` (hoặc giá trị của `options.default()` nếu được cung cấp), set `error` thành `undefined`, set `status` thành `idle`, và mark bất kỳ pending requests hiện tại nào là cancelled.

Theo mặc định, Nuxt chờ cho đến khi một `refresh` hoàn thành trước khi nó có thể được execute lại.

::note
Nếu bạn chưa fetch data trên server (ví dụ, với `server: false`), thì data _sẽ không_ được fetch cho đến khi hydration hoàn thành. Điều này có nghĩa là ngay cả khi bạn await [`useAsyncData`](/docs/api/composables/use-async-data) trên client side, `data` sẽ vẫn là `undefined` trong `<script setup>`.
::

## Type

```ts [Signature]
function useAsyncData<DataT, DataE>(
  handler: (nuxtApp?: NuxtApp) => Promise<DataT>,
  options?: AsyncDataOptions<DataT>
): AsyncData<DataT, DataE>
function useAsyncData<DataT, DataE>(
  key: MaybeRefOrGetter<string>,
  handler: (nuxtApp?: NuxtApp) => Promise<DataT>,
  options?: AsyncDataOptions<DataT>
): Promise<AsyncData<DataT, DataE>>

type AsyncDataOptions<DataT> = {
  server?: boolean
  lazy?: boolean
  immediate?: boolean
  deep?: boolean
  dedupe?: 'cancel' | 'defer'
  default?: () => DataT | Ref<DataT> | null
  transform?: (input: DataT) => DataT | Promise<DataT>
  pick?: string[]
  watch?: MultiWatchSources | false
  getCachedData?: (key: string, nuxtApp: NuxtApp, ctx: AsyncDataRequestContext) => DataT | undefined
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
};

interface AsyncDataExecuteOptions {
  dedupe?: 'cancel' | 'defer'
}

type AsyncDataRequestStatus = 'idle' | 'pending' | 'success' | 'error'
```

:read-more{to="/docs/getting-started/data-fetching"}
