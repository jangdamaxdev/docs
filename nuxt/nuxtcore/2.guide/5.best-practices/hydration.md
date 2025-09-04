---
navigation.title: 'Nuxt and hydration'
title: Nuxt and hydration
description: Why fixing hydration issues is important
---

Khi phát triển, bạn có thể gặp phải các vấn đề hydration. Đừng bỏ qua những cảnh báo đó.

# Why is it important to fix them?

Các lỗi hydration không chỉ là cảnh báo - chúng là dấu hiệu của các vấn đề nghiêm trọng có thể phá vỡ ứng dụng của bạn:

## Performance Impact

- **Thời gian tương tác tăng lên**: Lỗi hydration buộc Vue phải render lại toàn bộ cây component, điều này sẽ tăng thời gian để ứng dụng Nuxt của bạn trở nên tương tác
- **Trải nghiệm người dùng kém**: Người dùng có thể thấy nội dung nhấp nháy hoặc dịch chuyển bố cục bất ngờ

## Functionality Issues

- **Tương tác bị hỏng**: Các event listener có thể không gắn kết đúng cách, khiến các nút và form không hoạt động
- **Không nhất quán trạng thái**: Trạng thái ứng dụng có thể không đồng bộ giữa những gì người dùng thấy và những gì ứng dụng nghĩ là đã render
- **Vấn đề SEO**: Công cụ tìm kiếm có thể index nội dung khác với những gì người dùng thực sự thấy

# How to detect them

## Development Console Warnings

Vue sẽ ghi lại các cảnh báo lỗi hydration trong console trình duyệt trong quá trình phát triển:

![Screenshot of Vue hydration mismatch warning in the browser console](/assets/docs/best-practices/vue-console-hydration.png)

# Common reasons

## Browser-only APIs in Server Context

**Vấn đề**: Sử dụng các API dành riêng cho trình duyệt trong quá trình render phía server.

```html
<template>
  <div>User preference: {{ userTheme }}</div>
</template>

<script setup>
// This will cause hydration mismatch!
// localStorage doesn't exist on the server!
const userTheme = localStorage.getItem('theme') || 'light'
</script>
```

**Giải pháp**: Bạn có thể sử dụng [`useCookie`](/docs/api/composables/use-cookie):

```html
<template>
  <div>User preference: {{ userTheme }}</div>
</template>

<script setup>
// This works on both server and client
const userTheme = useCookie('theme', { default: () => 'light' })
</script>
```

## Inconsistent Data

**Vấn đề**: Dữ liệu khác nhau giữa server và client.

```html
<template>
  <div>{{ Math.random() }}</div>
</template>
```

**Giải pháp**: Sử dụng trạng thái thân thiện với SSR:

```html
<template>
  <div>{{ state }}</div>
</template>

<script setup>
const state = useState('random', () => Math.random())
</script>
```

## Conditional Rendering Based on Client State

**Vấn đề**: Sử dụng điều kiện chỉ dành cho client trong SSR.

```html
<template>
  <div v-if="window?.innerWidth > 768">
    Desktop content
  </div>
</template>
```

**Giải pháp**: Sử dụng media queries hoặc xử lý phía client:

```html
<template>
  <div class="responsive-content">
    <div class="hidden md:block">Desktop content</div>
    <div class="md:hidden">Mobile content</div>
  </div>
</template>
```

## Third-party Libraries with Side Effects

**Vấn đề**: Các thư viện sửa đổi DOM hoặc có phụ thuộc trình duyệt (điều này xảy ra RẤT NHIỀU với tag managers).

```html
<script setup>
if (import.meta.client) {
    const { default: SomeBrowserLibrary } = await import('browser-only-lib')
    SomeBrowserLibrary.init()
}
</script>
```

**Giải pháp**: Khởi tạo thư viện sau khi hydration hoàn thành:

```html
<script setup>
onMounted(async () => {
  const { default: SomeBrowserLibrary } = await import('browser-only-lib')
  SomeBrowserLibrary.init()
})
</script>
```

## Dynamic Content Based on Time

**Vấn đề**: Nội dung thay đổi dựa trên thời gian hiện tại.

```html
<template>
  <div>{{ greeting }}</div>
</template>

<script setup>
const hour = new Date().getHours()
const greeting = hour < 12 ? 'Good morning' : 'Good afternoon'
</script>
```

**Giải pháp**: Sử dụng component [`NuxtTime`](/docs/api/components/nuxt-time) hoặc xử lý phía client:

```html
<template>
  <div>
    <NuxtTime :date="new Date()" format="HH:mm" />
  </div>
</template>
```

```html
<template>
  <div>
    <ClientOnly>
      {{ greeting }}
      <template #fallback>
        Hello!
      </template>
    </ClientOnly>
  </div>
</template>

<script setup>
const greeting = ref('Hello!')

onMounted(() => {
  const hour = new Date().getHours()
  greeting.value = hour < 12 ? 'Good morning' : 'Good afternoon'
})
</script>
```

## In summary

1. **Sử dụng composables thân thiện với SSR**: [`useFetch`](/docs/api/composables/use-fetch), [`useAsyncData`](/docs/api/composables/use-async-data), [`useState`](/docs/api/composables/use-state)
2. **Bao bọc code chỉ dành cho client**: Sử dụng component [`ClientOnly`](/docs/api/components/client-only) cho nội dung dành riêng cho trình duyệt
3. **Nguồn dữ liệu nhất quán**: Đảm bảo server và client sử dụng cùng dữ liệu
4. **Tránh side effects trong setup**: Di chuyển code phụ thuộc trình duyệt vào `onMounted`

::tip
Bạn có thể đọc [tài liệu Vue về lỗi hydration SSR](https://vuejs.org/guide/scaling-up/ssr.html#hydration-mismatch) để hiểu rõ hơn về hydration.
::
