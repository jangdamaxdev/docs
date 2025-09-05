---
title: 'defineLazyHydrationComponent'
description: 'Định nghĩa một thành phần hydrat hóa lười với một chiến lược cụ thể.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/components/plugins/lazy-hydration-macro-transform.ts
    size: xs
---

`defineLazyHydrationComponent` là một macro trình biên dịch giúp bạn tạo một thành phần với chiến lược hydrat hóa lười cụ thể. Hydrat hóa lười trì hoãn hydrat hóa cho đến khi các thành phần trở nên hiển thị hoặc cho đến khi trình duyệt đã hoàn thành các tác vụ quan trọng hơn. Điều này có thể giảm đáng kể chi phí hiệu suất ban đầu, đặc biệt là đối với các thành phần không thiết yếu.

## Usage

### Visibility Strategy

Hydrat hóa thành phần khi nó trở nên hiển thị trong viewport.

```vue
<script setup lang="ts">
const LazyHydrationMyComponent = defineLazyHydrationComponent(
  'visible',
  () => import('./components/MyComponent.vue')
)
</script>

<template>
  <div>
    <!-- 
      Hydration will be triggered when
      the element(s) is 100px away from entering the viewport.
    -->
    <LazyHydrationMyComponent :hydrate-on-visible="{ rootMargin: '100px' }" />
  </div>
</template>
```

Prop `hydrateOnVisible` là tùy chọn. Bạn có thể truyền một đối tượng để tùy chỉnh hành vi của `IntersectionObserver` bên dưới.

::read-more{to="https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver/IntersectionObserver" title="IntersectionObserver options"}
Đọc thêm về các tùy chọn cho `hydrate-on-visible`.
::

::note
Bên dưới, điều này sử dụng chiến lược [`hydrateOnVisible`](https://vuejs.org/guide/components/async.html#hydrate-on-visible) tích hợp sẵn của Vue.
::

### Idle Strategy

Hydrat hóa thành phần khi trình duyệt đang rảnh. Điều này phù hợp nếu bạn cần thành phần tải càng sớm càng tốt, nhưng không chặn đường dẫn kết xuất quan trọng.

```vue
<script setup lang="ts">
const LazyHydrationMyComponent = defineLazyHydrationComponent(
  'idle',
  () => import('./components/MyComponent.vue')
)
</script>

<template>
  <div>
    <!-- Hydration will be triggered when the browser is idle or after 2000ms. -->
    <LazyHydrationMyComponent :hydrate-on-idle="2000" />
  </div>
</template>
```

Prop `hydrateOnIdle` là tùy chọn. Bạn có thể truyền một số dương để chỉ định thời gian chờ tối đa.

Chiến lược rảnh là dành cho các thành phần có thể được hydrat hóa khi trình duyệt đang rảnh.

::note
Bên dưới, điều này sử dụng chiến lược [`hydrateOnIdle`](https://vuejs.org/guide/components/async.html#hydrate-on-idle) tích hợp sẵn của Vue.
::

### Interaction Strategy

Hydrat hóa thành phần sau một tương tác được chỉ định (ví dụ: click, mouseover).

```vue
<script setup lang="ts">
const LazyHydrationMyComponent = defineLazyHydrationComponent(
  'interaction',
  () => import('./components/MyComponent.vue')
)
</script>

<template>
  <div>
    <!--
      Hydration will be triggered when
      the element(s) is hovered over by the pointer.
    -->
    <LazyHydrationMyComponent hydrate-on-interaction="mouseover" />
  </div>
</template>
```

Prop `hydrateOnInteraction` là tùy chọn. Nếu bạn không truyền một sự kiện hoặc danh sách các sự kiện, nó mặc định hydrat hóa trên `pointerenter`, `click`, và `focus`.

::note
Bên dưới, điều này sử dụng chiến lược [`hydrateOnInteraction`](https://vuejs.org/guide/components/async.html#hydrate-on-interaction) tích hợp sẵn của Vue.
::

### Media Query Strategy

Hydrat hóa thành phần khi cửa sổ khớp với một truy vấn phương tiện.

```vue
<script setup lang="ts">
const LazyHydrationMyComponent = defineLazyHydrationComponent(
  'mediaQuery',
  () => import('./components/MyComponent.vue')
)
</script>

<template>
  <div>
    <!--
      Hydration will be triggered when
      the window width is greater than or equal to 768px.
    -->
    <LazyHydrationMyComponent hydrate-on-media-query="(min-width: 768px)" />
  </div>
</template>
```

::note
Bên dưới, điều này sử dụng chiến lược [`hydrateOnMediaQuery`](https://vuejs.org/guide/components/async.html#hydrate-on-media-query) tích hợp sẵn của Vue.
::

### Time Strategy

Hydrat hóa thành phần sau một độ trễ được chỉ định (tính bằng mili giây).

```vue
<script setup lang="ts">
const LazyHydrationMyComponent = defineLazyHydrationComponent(
  'time', 
  () => import('./components/MyComponent.vue')
)
</script>

<template>
  <div>
    <!-- Hydration is triggered after 1000ms. -->
    <LazyHydrationMyComponent :hydrate-after="1000" />
  </div>
</template>
```

Chiến lược thời gian là dành cho các thành phần có thể chờ một khoảng thời gian cụ thể.

### If Strategy

Hydrat hóa thành phần dựa trên một điều kiện boolean.

```vue
<script setup lang="ts">
const LazyHydrationMyComponent = defineLazyHydrationComponent(
  'if',
  () => import('./components/MyComponent.vue')
)

const isReady = ref(false)

function myFunction() {
  // Trigger custom hydration strategy...
  isReady.value = true
}
</script>

<template>
  <div>
    <!-- Hydration is triggered when isReady becomes true. -->
    <LazyHydrationMyComponent :hydrate-when="isReady" />
  </div>
</template>
```

Chiến lược if là tốt nhất cho các thành phần có thể không luôn cần được hydrat hóa.

### Never Hydrate

Không bao giờ hydrat hóa thành phần.

```vue
<script setup lang="ts">
const LazyHydrationMyComponent = defineLazyHydrationComponent(
  'never',
  () => import('./components/MyComponent.vue')
)
</script>

<template>
  <div>
    <!-- This component will never be hydrated by Vue. -->
    <LazyHydrationMyComponent />
  </div>
</template>
```

### Listening to Hydration Events

Tất cả các thành phần hydrat hóa bị trì hoãn phát ra sự kiện `@hydrated` khi chúng được hydrat hóa.

```vue
<script setup lang="ts">
const LazyHydrationMyComponent = defineLazyHydrationComponent(
  'visible',
  () => import('./components/MyComponent.vue')
)

function onHydrate() {
  console.log("Component has been hydrated!")
}
</script>

<template>
  <div>
    <LazyHydrationMyComponent
      :hydrate-on-visible="{ rootMargin: '100px' }"
      @hydrated="onHydrated"
    />
  </div>
</template>
```

## Parameters

::warning
Để đảm bảo trình biên dịch nhận dạng đúng macro này, tránh sử dụng các biến bên ngoài. Cách tiếp cận sau sẽ ngăn macro được nhận dạng đúng cách:

```vue
<script setup lang="ts">
const strategy = 'visible'
const source = () => import('./components/MyComponent.vue')
const LazyHydrationMyComponent = defineLazyHydrationComponent(strategy, source)
</script>
```
::

### `strategy`

- **Type**: `'visible' | 'idle' | 'interaction' | 'mediaQuery' | 'if' | 'time' | 'never'`
- **Required**: `true`

| Strategy      | Description                                                    |
|---------------|----------------------------------------------------------------|
| `visible`     | Hydrat hóa khi thành phần trở nên hiển thị trong viewport.   |
| `idle`        | Hydrat hóa khi trình duyệt đang rảnh hoặc sau một độ trễ.            |
| `interaction` | Hydrat hóa khi có tương tác của người dùng (ví dụ: click, hover).           |
| `mediaQuery`  | Hydrat hóa khi điều kiện truy vấn phương tiện được chỉ định được đáp ứng.      |
| `if`          | Hydrat hóa khi điều kiện boolean được chỉ định được đáp ứng.            |
| `time`        | Hydrat hóa sau độ trễ thời gian được chỉ định.                         |
| `never`       | Ngăn Vue hydrat hóa thành phần.                     |

### `source`

- **Type**: `() => Promise<Component>`
- **Required**: `true`