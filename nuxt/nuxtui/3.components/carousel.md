---
description: Một carousel với chuyển động và vuốt được xây dựng bằng Embla.
category: data
links:
  - label: Embla
    to: https://www.embla-carousel.com/api/
    icon: i-custom-embla-carousel
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Carousel.vue
---

## Usage

### Items

Sử dụng prop `items` dưới dạng mảng và hiển thị từng mục bằng slot mặc định:

::note
Sử dụng chuột để kéo carousel theo chiều ngang trên desktop.
::

::component-example
---
name: 'carousel-items-example'
class: 'p-8'
---
::

Bạn cũng có thể truyền một mảng các đối tượng với các thuộc tính sau:

- `class?: any`{lang="ts-type"}
- `ui?: { item?: ClassNameValue }`{lang="ts-type"}

Bạn có thể kiểm soát số lượng mục hiển thị bằng cách sử dụng các lớp tiện ích [`basis`](https://tailwindcss.com/docs/flex-basis) / [`width`](https://tailwindcss.com/docs/width) trên `item`:

::component-example
---
name: 'carousel-items-multiple-example'
class: 'p-8 px-16'
---
::

### Orientation

Sử dụng prop `orientation` để thay đổi hướng của Carousel. Mặc định là `horizontal`.

::note
Sử dụng chuột để kéo carousel theo chiều dọc trên desktop.
::

::component-example
---
name: 'carousel-orientation-example'
class: 'p-8'
---
::

::caution
Bạn cần chỉ định `height` trên container trong hướng dọc.
::

### Arrows

Sử dụng prop `arrows` để hiển thị các nút prev và next.

::component-example
---
name: 'carousel-arrows-example'
class: 'p-8'
---
::

### Prev / Next

Sử dụng các prop `prev` và `next` để tùy chỉnh các nút prev và next với bất kỳ prop [Button](/components/button) nào.

::component-example
---
name: 'carousel-prev-next-example'
class: 'p-8'
---
::

### Prev / Next Icons

Sử dụng các prop `prev-icon` và `next-icon` để tùy chỉnh [Icon](/components/icon) của các nút. Mặc định là `i-lucide-arrow-left` / `i-lucide-arrow-right`.

::component-example
---
name: 'carousel-prev-next-icon-example'
class: 'p-8'
options:
  - name: 'prevIcon'
    label: 'prevIcon'
    default: 'i-lucide-chevron-left'
  - name: 'nextIcon'
    label: 'nextIcon'
    default: 'i-lucide-chevron-right'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh các biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.arrowLeft` / `ui.icons.arrowRight`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh các biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.arrowLeft` / `ui.icons.arrowRight`.
:::
::

### Dots

Sử dụng prop `dots` để hiển thị danh sách các chấm để cuộn đến slide cụ thể.

::component-example
---
name: 'carousel-dots-example'
class: 'p-8 pb-12'
---
::

Số lượng chấm dựa trên số lượng slide được hiển thị trong view:

::component-example
---
name: 'carousel-dots-multiple-example'
class: 'p-8 px-16 pb-12'
---
::

## Plugins

Thành phần Carousel triển khai các plugin [Embla Carousel](https://www.embla-carousel.com/plugins/) chính thức.

### Autoplay

Plugin này được sử dụng để mở rộng Embla Carousel với chức năng **tự động phát**.

Sử dụng prop `autoplay` dưới dạng boolean hoặc đối tượng để cấu hình [Autoplay plugin](https://www.embla-carousel.com/plugins/autoplay/).

::component-example
---
name: 'carousel-autoplay-example'
class: 'p-8 px-16 pb-12'
---
::

::note
Trong ví dụ này, chúng tôi đang sử dụng prop `loop` cho carousel vô hạn.
::

### Auto Scroll

Plugin này được sử dụng để mở rộng Embla Carousel với chức năng **tự động cuộn**.

Sử dụng prop `auto-scroll` dưới dạng boolean hoặc đối tượng để cấu hình [Auto Scroll plugin](https://www.embla-carousel.com/plugins/auto-scroll/).

::component-example
---
name: 'carousel-auto-scroll-example'
class: 'p-8 px-16 pb-12'
---
::

::note
Trong ví dụ này, chúng tôi đang sử dụng prop `loop` cho carousel vô hạn.
::

### Auto Height

Plugin này được sử dụng để mở rộng Embla Carousel với chức năng **tự động chiều cao**. Nó thay đổi chiều cao của container carousel để phù hợp với chiều cao của slide cao nhất trong view.

Sử dụng prop `auto-height` dưới dạng boolean hoặc đối tượng để cấu hình [Auto Height plugin](https://www.embla-carousel.com/plugins/auto-height/).

::component-example
---
name: 'carousel-auto-height-example'
class: 'p-8 pt-16'
---
::

::note
Trong ví dụ này, chúng tôi thêm lớp `transition-[height]` trên container để tạo hiệu ứng chuyển đổi chiều cao.
::

### Class Names

Class Names là plugin tiện ích **chuyển đổi tên lớp** cho Embla Carousel cho phép bạn tự động chuyển đổi tên lớp trên carousel của bạn.

Sử dụng prop `class-names` dưới dạng boolean hoặc đối tượng để cấu hình [Class Names plugin](https://www.embla-carousel.com/plugins/class-names/).

::component-example
---
name: 'carousel-class-names-example'
class: 'p-8'
---
::

::note
Trong ví dụ này, chúng tôi thêm các lớp `transition-opacity [&:not(.is-snapped)]:opacity-10` trên `item` để tạo hiệu ứng chuyển đổi độ mờ.
::

### Fade

Plugin này được sử dụng để thay thế chức năng cuộn Embla Carousel bằng **chuyển đổi mờ**.

Sử dụng prop `fade` dưới dạng boolean hoặc đối tượng để cấu hình [Fade plugin](https://www.embla-carousel.com/plugins/fade/).

::component-example
---
name: 'carousel-fade-example'
class: 'p-8 pb-12'
---
::

### Wheel Gestures

Plugin này được sử dụng để mở rộng Embla Carousel với khả năng **sử dụng bánh xe chuột/trackpad** để điều hướng carousel.

Sử dụng prop `wheel-gestures` dưới dạng boolean hoặc đối tượng để cấu hình [Wheel Gestures plugin](https://www.embla-carousel.com/plugins/wheel-gestures/).

::note
Sử dụng bánh xe chuột để cuộn carousel.
::

::component-example
---
name: 'carousel-wheel-gestures-example'
class: 'p-8 px-16'
---
::

## Examples

### With thumbnails

Bạn có thể sử dụng hàm [`emblaApi`](#expose) [scrollTo](https://www.embla-carousel.com/api/methods/#scrollto) để hiển thị hình thu nhỏ dưới carousel cho phép bạn điều hướng đến slide cụ thể.

::component-example
---
name: 'carousel-thumbnails-example'
class: 'p-8 px-16'
---
::

## API

### Props

:component-props

### Slots

:component-slots

### Emits

:component-emits

### Expose

Bạn có thể truy cập instance thành phần đã nhập bằng [`useTemplateRef`](https://vuejs.org/api/composition-api-helpers.html#usetemplateref).

```vue
<script setup lang="ts">
const carousel = useTemplateRef('carousel')
</script>

<template>
  <UCarousel ref="carousel" />
</template>
```

Điều này sẽ cho bạn quyền truy cập vào những thứ sau:

| Name | Type |
| ---- | ---- |
| `emblaRef`{lang="ts-type"} | `Ref<HTMLElement \| null>`{lang="ts-type"} |
| `emblaApi`{lang="ts-type"} | [`Ref<EmblaCarouselType \| null>`{lang="ts-type"}](https://www.embla-carousel.com/api/methods/#typescript) |

## Theme

:component-theme

## Changelog

:component-changelog
