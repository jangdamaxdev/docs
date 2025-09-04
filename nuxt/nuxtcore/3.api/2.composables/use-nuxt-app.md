---
title: 'useNuxtApp'
description: 'Truy cập ngữ cảnh thời gian chạy chia sẻ của Ứng dụng Nuxt.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/nuxt.ts
    size: xs
---

`useNuxtApp` là một composable tích hợp cung cấp cách truy cập ngữ cảnh thời gian chạy chia sẻ của Nuxt, còn được gọi là [Nuxt context](/docs/guide/going-further/nuxt-app#the-nuxt-context), có sẵn trên cả client và server side (nhưng không trong Nitro routes). Nó giúp bạn truy cập Vue app instance, runtime hooks, runtime config variables và internal states, chẳng hạn như `ssrContext` và `payload`.

```vue [app.vue]
<script setup lang="ts">
const nuxtApp = useNuxtApp()
</script>
```

Nếu ngữ cảnh thời gian chạy không khả dụng trong phạm vi của bạn, `useNuxtApp` sẽ ném ra một ngoại lệ khi được gọi. Bạn có thể sử dụng [`tryUseNuxtApp`](#tryusenuxtapp) thay thế cho các composables không yêu cầu `nuxtApp`, hoặc để đơn giản kiểm tra xem ngữ cảnh có khả dụng hay không mà không có ngoại lệ.

<!--
note
By default, the shared runtime context of Nuxt is namespaced under the [`buildId`](/docs/api/nuxt-config#buildid) option. It allows the support of multiple runtime contexts.

## Params

- `appName`: an optional application name. If you do not provide it, the Nuxt `buildId` option is used. Otherwise, it must match with an existing `buildId`. -->

## Methods

### `provide (name, value)`

`nuxtApp` là một ngữ cảnh thời gian chạy mà bạn có thể mở rộng bằng cách sử dụng [Nuxt plugins](/docs/guide/directory-structure/plugins). Sử dụng hàm `provide` để tạo Nuxt plugins để làm cho các giá trị và phương thức trợ giúp khả dụng trong ứng dụng Nuxt của bạn trên tất cả các composables và components.

Hàm `provide` chấp nhận các tham số `name` và `value`.

```js
const nuxtApp = useNuxtApp()
nuxtApp.provide('hello', (name) => `Hello ${name}!`)

// Prints "Hello name!"
console.log(nuxtApp.$hello('name'))
```

Như bạn có thể thấy trong ví dụ trên, `$hello` đã trở thành phần mới và tùy chỉnh của ngữ cảnh `nuxtApp` và nó khả dụng ở tất cả các nơi mà `nuxtApp` có thể truy cập.

### `hook(name, cb)`

Các hooks khả dụng trong `nuxtApp` cho phép bạn tùy chỉnh các khía cạnh thời gian chạy của ứng dụng Nuxt của bạn. Bạn có thể sử dụng runtime hooks trong Vue.js composables và [Nuxt plugins](/docs/guide/directory-structure/plugins) để hook vào vòng đời rendering.

Hàm `hook` hữu ích để thêm logic tùy chỉnh bằng cách hook vào vòng đời rendering tại một điểm cụ thể. Hàm `hook` chủ yếu được sử dụng khi tạo Nuxt plugins.

See [Runtime Hooks](/docs/api/advanced/hooks#app-hooks-runtime) for available runtime hooks called by Nuxt.

```ts [plugins/test.ts]
export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.hook('page:start', () => {
    /* your code goes here */
  })
  nuxtApp.hook('vue:error', (..._args) => {
    console.log('vue:error')
    // if (import.meta.client) {
    //   console.log(..._args)
    // }
  })
})
```

### `callHook(name, ...args)`

`callHook` trả về một promise khi được gọi với bất kỳ hooks hiện có nào.

```ts
await nuxtApp.callHook('my-plugin:init')
```

## Properties

`useNuxtApp()` hiển thị các thuộc tính sau mà bạn có thể sử dụng để mở rộng và tùy chỉnh ứng dụng của bạn và chia sẻ state, data và variables.

### `vueApp`

`vueApp` là [application instance](https://vuejs.org/api/application.html#application-api) Vue.js toàn cục mà bạn có thể truy cập thông qua `nuxtApp`.

Một số phương thức hữu ích:
- [`component()`](https://vuejs.org/api/application.html#app-component) - Đăng ký một component toàn cục nếu truyền cả tên string và định nghĩa component, hoặc truy xuất một component đã đăng ký nếu chỉ truyền tên.
- [`directive()`](https://vuejs.org/api/application.html#app-directive) - Đăng ký một directive tùy chỉnh toàn cục nếu truyền cả tên string và định nghĩa directive, hoặc truy xuất một directive đã đăng ký nếu chỉ truyền tên[(example)](/docs/guide/directory-structure/plugins#vue-directives).
- [`use()`](https://vuejs.org/api/application.html#app-use) - Cài đặt một **[Vue.js Plugin](https://vuejs.org/guide/reusability/plugins.html)** [(example)](/docs/guide/directory-structure/plugins#vue-plugins).

:read-more{icon="i-simple-icons-vuedotjs" to="https://vuejs.org/api/application.html#application-api"}

### `ssrContext`

`ssrContext` được tạo ra trong quá trình server-side rendering và nó chỉ khả dụng trên server side.

Nuxt hiển thị các thuộc tính sau thông qua `ssrContext`:
- `url` (string) -  URL yêu cầu hiện tại.
- `event` ([h3js/h3](https://github.com/h3js/h3) request event) - Truy cập request & response của route hiện tại.
- `payload` (object) - Đối tượng payload NuxtApp.

### `payload`

`payload` hiển thị data và state variables từ server side sang client side. Các keys sau sẽ khả dụng trên client sau khi chúng đã được truyền từ server side:

- `serverRendered` (boolean) - Cho biết nếu response là server-side-rendered.
- `data` (object) - Khi bạn fetch data từ một API endpoint bằng cách sử dụng [`useFetch`](/docs/api/composables/use-fetch) hoặc [`useAsyncData`](/docs/api/composables/use-async-data), payload kết quả có thể được truy cập từ `payload.data`. Data này được cache và giúp bạn ngăn chặn việc fetch cùng một data trong trường hợp một yêu cầu giống hệt được thực hiện nhiều hơn một lần.

  ::code-group
  ```vue [app.vue]
  <script setup lang="ts">
  const { data } = await useAsyncData('count', () => $fetch('/api/count'))
  </script>
  ```
  ```ts [server/api/count.ts]
  export default defineEventHandler(event => {
    return { count: 1 }
  })
  ```
  ::

  Sau khi fetch giá trị của `count` bằng cách sử dụng [`useAsyncData`](/docs/api/composables/use-async-data) trong ví dụ trên, nếu bạn truy cập `payload.data`, bạn sẽ thấy `{ count: 1 }` được ghi lại ở đó.

  Khi truy cập cùng một `payload.data` từ [`ssrcontext`](#ssrcontext), bạn có thể truy cập cùng một giá trị trên server side cũng vậy.

- `state` (object) - Khi bạn sử dụng composable [`useState`](/docs/api/composables/use-state) trong Nuxt để thiết lập shared state, data state này được truy cập thông qua `payload.state.[name-of-your-state]`.

  ```ts [plugins/my-plugin.ts]
  export const useColor = () => useState<string>('color', () => 'pink')

  export default defineNuxtPlugin((nuxtApp) => {
    if (import.meta.server) {
      const color = useColor()
    }
  })
  ```

  Cũng có thể sử dụng các loại nâng cao hơn, chẳng hạn như `ref`, `reactive`, `shallowRef`, `shallowReactive` và `NuxtError`.

  Kể từ [Nuxt v3.4](https://nuxt.com/blog/v3-4#payload-enhancements), có thể định nghĩa reducer/reviver riêng của bạn cho các loại không được hỗ trợ bởi Nuxt.

  :video-accordion{title="Watch a video from Alexander Lichter about serializing payloads, especially with regards to classes" videoId="8w6ffRBs8a4"}

  Trong ví dụ dưới đây, chúng ta định nghĩa một reducer (hoặc serializer) và một reviver (hoặc deserializer) cho lớp DateTime [Luxon](https://moment.github.io/luxon/#/), sử dụng một payload plugin.

  ```ts [plugins/date-time-payload.ts]
  /**
   * This kind of plugin runs very early in the Nuxt lifecycle, before we revive the payload.
   * You will not have access to the router or other Nuxt-injected properties.
   *
   * Note that the "DateTime" string is the type identifier and must
   * be the same on both the reducer and the reviver.
   */
  export default definePayloadPlugin((nuxtApp) => {
    definePayloadReducer('DateTime', (value) => {
      return value instanceof DateTime && value.toJSON()
    })
    definePayloadReviver('DateTime', (value) => {
      return DateTime.fromISO(value)
    })
  })
  ```

### `isHydrating`

Sử dụng `nuxtApp.isHydrating` (boolean) để kiểm tra xem Nuxt app có đang hydrating trên client side hay không.

```ts [components/nuxt-error-boundary.ts]
export default defineComponent({
  setup (_props, { slots, emit }) {
    const nuxtApp = useNuxtApp()
    onErrorCaptured((err) => {
      if (import.meta.client && !nuxtApp.isHydrating) {
        // ...
      }
    })
  }
})
```

### `runWithContext`

::note
Bạn có thể ở đây vì bạn nhận được thông báo "Nuxt instance unavailable". Vui lòng sử dụng phương thức này một cách tiết kiệm, và báo cáo các ví dụ gây ra vấn đề, để cuối cùng nó có thể được giải quyết ở cấp độ framework.
::

Phương thức `runWithContext` được thiết kế để gọi một hàm và cung cấp cho nó một ngữ cảnh Nuxt rõ ràng. Thông thường, ngữ cảnh Nuxt được truyền xung quanh một cách ngầm định và bạn không cần lo lắng về điều này. Tuy nhiên, khi làm việc với các kịch bản `async`/`await` phức tạp trong middleware/plugins, bạn có thể gặp phải các trường hợp mà instance hiện tại đã bị unset sau một async call.

```ts [middleware/auth.ts]
export default defineNuxtRouteMiddleware(async (to, from) => {
  const nuxtApp = useNuxtApp()
  let user
  try {
    user = await fetchUser()
    // the Vue/Nuxt compiler loses context here because of the try/catch block.
  } catch (e) {
    user = null
  }
  if (!user) {
    // apply the correct Nuxt context to our `navigateTo` call.
    return nuxtApp.runWithContext(() => navigateTo('/auth'))
  }
})
```

#### Usage

```js
const result = nuxtApp.runWithContext(() => functionWithContext())
```

- `functionWithContext`: Bất kỳ hàm nào yêu cầu ngữ cảnh của ứng dụng Nuxt hiện tại. Ngữ cảnh này sẽ được áp dụng chính xác một cách tự động.

`runWithContext` sẽ trả về bất cứ gì được trả về bởi `functionWithContext`.

#### A Deeper Explanation of Context

Vue.js Composition API (và Nuxt composables tương tự) hoạt động bằng cách phụ thuộc vào một ngữ cảnh ngầm định. Trong vòng đời, Vue thiết lập instance tạm thời của component hiện tại (và instance tạm thời của nuxtApp trong Nuxt) vào một biến toàn cục và unset nó trong cùng một tick. Khi rendering trên server side, có nhiều yêu cầu từ các user khác nhau và nuxtApp chạy trong cùng một ngữ cảnh toàn cục. Vì vậy, Nuxt và Vue ngay lập tức unset instance toàn cục này để tránh rò rỉ tham chiếu chia sẻ giữa hai user hoặc components.

Điều này có nghĩa là gì? Composition API và Nuxt Composables chỉ khả dụng trong vòng đời và trong cùng một tick trước bất kỳ async operation nào:

```js
// --- Vue internal ---
const _vueInstance = null
const getCurrentInstance = () => _vueInstance
// ---

// Vue / Nuxt sets a global variable referencing to current component in _vueInstance when calling setup()
async function setup() {
  getCurrentInstance() // Works
  await someAsyncOperation() // Vue unsets the context in same tick before async operation!
  getCurrentInstance() // null
}
```

Giải pháp cổ điển cho điều này là cache instance hiện tại trên lần gọi đầu tiên vào một biến local như `const instance = getCurrentInstance()` và sử dụng nó trong lần gọi composable tiếp theo nhưng vấn đề là bất kỳ nested composable calls nào bây giờ cần chấp nhận instance một cách rõ ràng làm đối số và không phụ thuộc vào ngữ cảnh ngầm định của composition-api. Đây là giới hạn thiết kế với composables và không phải là vấn đề per-se.

Để vượt qua giới hạn này, Vue thực hiện một số công việc behind the scenes khi compile code ứng dụng của chúng ta và khôi phục ngữ cảnh sau mỗi lần gọi cho `<script setup>`:

```js
const __instance = getCurrentInstance() // Generated by Vue compiler
getCurrentInstance() // Works!
await someAsyncOperation() // Vue unsets the context
__restoreInstance(__instance) // Generated by Vue compiler
getCurrentInstance() // Still works!
```

Để có mô tả tốt hơn về những gì Vue thực sự làm, xem [unjs/unctx#2 (comment)](https://github.com/unjs/unctx/issues/2#issuecomment-942193723).

#### Solution

Đây là nơi `runWithContext` có thể được sử dụng để khôi phục ngữ cảnh, tương tự như cách `<script setup>` hoạt động.

Nuxt nội bộ sử dụng [unjs/unctx](https://github.com/unjs/unctx) để hỗ trợ composables tương tự như Vue cho plugins và middleware. Điều này cho phép các composables như `navigateTo()` hoạt động mà không cần truyền trực tiếp `nuxtApp` cho chúng - mang lại lợi ích DX và performance của Composition API cho toàn bộ framework Nuxt.

Kiểm tra [unjs/unctx#2](https://github.com/unjs/unctx/issues/2) (proposal), [unjs/unctx#4](https://github.com/unjs/unctx/pull/4) (transform implementation), và [nuxt/framework#3884](https://github.com/nuxt/framework/pull/3884) (Integration to Nuxt).

Vue hiện tại chỉ hỗ trợ async context restoration cho `<script setup>` cho việc sử dụng async/await. Trong Nuxt, hỗ trợ transform cho `defineNuxtPlugin()` và `defineNuxtRouteMiddleware()` đã được thêm vào, có nghĩa là khi bạn sử dụng chúng Nuxt tự động transform chúng với context restoration.

#### Remaining Issues

Transformation `unjs/unctx` để tự động khôi phục ngữ cảnh dường như có bug với các câu lệnh `try/catch` chứa `await` mà cuối cùng cần được giải quyết để loại bỏ yêu cầu của workaround được đề xuất ở trên.

#### Native Async Context

Sử dụng một tính năng thử nghiệm mới, có thể kích hoạt hỗ trợ native async context bằng cách sử dụng [Node.js `AsyncLocalStorage`](https://nodejs.org/api/async_context.html#class-asynclocalstorage) và hỗ trợ unctx mới để làm cho async context khả dụng **một cách native** cho **bất kỳ nested async composable nào** mà không cần transform hoặc truyền/gọi thủ công với context.

::tip
Hỗ trợ native async context hiện tại hoạt động trong Bun và Node.
::

:read-more{to="/docs/guide/going-further/experimental-features#asynccontext"}

## tryUseNuxtApp

Hàm này hoạt động chính xác giống như `useNuxtApp`, nhưng trả về `null` nếu ngữ cảnh không khả dụng thay vì ném ra ngoại lệ.

Bạn có thể sử dụng nó cho các composables không yêu cầu `nuxtApp`, hoặc để đơn giản kiểm tra xem ngữ cảnh có khả dụng hay không mà không có ngoại lệ.

Ví dụ sử dụng:

```ts [composable.ts]
export function useStandType() {
  // Always works on the client
  if (tryUseNuxtApp()) {
    return useRuntimeConfig().public.STAND_TYPE
  } else {
    return process.env.STAND_TYPE
  }
}
```

<!-- ### Params

- `appName`: an optional application name. If you do not provide it, the Nuxt `buildId` option is used. Otherwise, it must match with an existing `buildId`. -->
