---
title: 'useNuxtData'
description: 'Truy cập giá trị cache hiện tại của các composables fetch data.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/asyncData.ts
    size: xs
---

::note
`useNuxtData` cho bạn truy cập giá trị cache hiện tại của [`useAsyncData`](/docs/api/composables/use-async-data) , [`useLazyAsyncData`](/docs/api/composables/use-lazy-async-data), [`useFetch`](/docs/api/composables/use-fetch) và [`useLazyFetch`](/docs/api/composables/use-lazy-fetch) với key được cung cấp rõ ràng.
::

## Usage

Composable `useNuxtData` được sử dụng để truy cập giá trị cache hiện tại của các composables fetch data như `useAsyncData`, `useLazyAsyncData`, `useFetch`, và `useLazyFetch`. Bằng cách cung cấp key được sử dụng trong quá trình fetch data, bạn có thể truy xuất data cache và sử dụng nó khi cần.

Điều này đặc biệt hữu ích để tối ưu hóa performance bằng cách tái sử dụng data đã fetch hoặc triển khai các tính năng như Optimistic Updates hoặc cascading data updates.

Để sử dụng `useNuxtData`, đảm bảo rằng composable fetch data (`useFetch`, `useAsyncData`, etc.) đã được gọi với key được cung cấp rõ ràng.

:video-accordion{title="Watch a video from LearnVue about useNuxtData" videoId="e-_u6swXRWk"}

## Params

- `key`: Key duy nhất xác định data cache. Key này nên khớp với key được sử dụng trong quá trình fetch data ban đầu.

## Return Values

- `data`: Một reactive reference đến data cache liên quan đến key được cung cấp. Nếu không có data cache tồn tại, giá trị sẽ là `null`. `Ref` này tự động cập nhật nếu data cache thay đổi, cho phép reactivity liền mạch trong các components của bạn.

## Example

Ví dụ dưới đây cho thấy cách bạn có thể sử dụng data cache làm placeholder trong khi data mới nhất đang được fetch từ server.

```vue [pages/posts.vue]
<script setup lang="ts">
// We can access same data later using 'posts' key
const { data } = await useFetch('/api/posts', { key: 'posts' })
</script>
```

```vue [pages/posts/[id\\].vue]
<script setup lang="ts">
// Access to the cached value of useFetch in posts.vue (parent route)
const { data: posts } = useNuxtData('posts')

const route = useRoute()

const { data } = useLazyFetch(`/api/posts/${route.params.id}`, {
  key: `post-${route.params.id}`,
  default() {
    // Find the individual post from the cache and set it as the default value.
    return posts.value.find(post => post.id === route.params.id)
  }
})
</script>
```

## Optimistic Updates

Ví dụ dưới đây cho thấy cách triển khai Optimistic Updates có thể được thực hiện bằng cách sử dụng useNuxtData.

Optimistic Updates là một kỹ thuật mà giao diện người dùng được cập nhật ngay lập tức, giả định rằng một operation server sẽ thành công. Nếu operation cuối cùng thất bại, UI sẽ được rollback về trạng thái trước đó.

```vue [pages/todos.vue]
<script setup lang="ts">
// We can access same data later using 'todos' key
const { data } = await useAsyncData('todos', () => $fetch('/api/todos'))
</script>
```

```vue [components/NewTodo.vue]
<script setup lang="ts">
const newTodo = ref('')
let previousTodos = []

// Access to the cached value of useAsyncData in todos.vue
const { data: todos } = useNuxtData('todos')

async function addTodo () {
  return $fetch('/api/addTodo', {
    method: 'post',
    body: {
      todo: newTodo.value
    },
    onRequest () {
      // Store the previously cached value to restore if fetch fails.
      previousTodos = todos.value

      // Optimistically update the todos.
      todos.value = [...todos.value, newTodo.value]
    },
    onResponseError () {
      // Rollback the data if the request failed.
      todos.value = previousTodos
    },
    async onResponse () {
      // Invalidate todos in the background if the request succeeded.
      await refreshNuxtData('todos')
    }
  })
}
</script>
```

## Type

```ts
useNuxtData<DataT = any> (key: string): { data: Ref<DataT | undefined> }
```
