---
title: "defineNuxtComponent"
description: defineNuxtComponent() là một hàm trợ giúp để định nghĩa các thành phần an toàn kiểu với Options API.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/component.ts
    size: xs
---

::note
`defineNuxtComponent()` là một hàm trợ giúp để định nghĩa các thành phần Vue an toàn kiểu bằng cách sử dụng options API tương tự như [`defineComponent()`](https://vuejs.org/api/general.html#definecomponent). Wrapper `defineNuxtComponent()` cũng thêm hỗ trợ cho các tùy chọn thành phần `asyncData` và `head`.
::

::note
Sử dụng `<script setup lang="ts">` là cách được khuyến nghị để khai báo các thành phần Vue trong Nuxt.
::

:read-more{to=/docs/getting-started/data-fetching}

## `asyncData()`

Nếu bạn chọn không sử dụng `setup()` trong ứng dụng của mình, bạn có thể sử dụng phương thức `asyncData()` trong định nghĩa thành phần của mình:

```vue [pages/index.vue]
<script lang="ts">
export default defineNuxtComponent({
  async asyncData() {
    return {
      data: {
        greetings: 'hello world!'
      }
    }
  },
})
</script>
```

## `head()`

Nếu bạn chọn không sử dụng `setup()` trong ứng dụng của mình, bạn có thể sử dụng phương thức `head()` trong định nghĩa thành phần của mình:

```vue [pages/index.vue]
<script lang="ts">
export default defineNuxtComponent({
  head(nuxtApp) {
    return {
      title: 'My site'
    }
  },
})
</script>
```
