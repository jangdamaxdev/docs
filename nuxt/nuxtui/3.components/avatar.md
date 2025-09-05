---
description: Một phần tử img với dự phòng và hỗ trợ Nuxt Image.
category: element
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Avatar.vue
---

## Usage

Avatar sử dụng thành phần `<NuxtImg>` khi [`@nuxt/image`](https://github.com/nuxt/image) được cài đặt, quay lại `img` nếu không.

::note
Bạn có thể truyền bất kỳ thuộc tính nào từ phần tử HTML `<img>` như `alt`, `loading`, v.v.
::

### Src

Sử dụng prop `src` để đặt URL hình ảnh.

::component-code
---
props:
  src: 'https://github.com/benjamincanac.png'
---
::

### Size

Sử dụng prop `size` để đặt kích thước của Avatar.

::component-code
---
ignore:
  - src
props:
  src: 'https://github.com/benjamincanac.png'
  size: xl
---
::

::note
`width` và `height` của phần tử `<img>` được tự động đặt dựa trên prop `size`.
::

### Icon

Sử dụng prop `icon` để hiển thị một [Icon](/components/icon) dự phòng.

::component-code
---
props:
  icon: 'i-lucide-image'
  size: md
---
::

### Text

Sử dụng prop `text` để hiển thị văn bản dự phòng.

::component-code
---
props:
  text: '+1'
  size: md
---
::

### Alt

Khi không có biểu tượng hoặc văn bản nào được cung cấp, **chữ cái đầu** của prop `alt` được sử dụng làm dự phòng.

::component-code
---
props:
  alt: 'Benjamin Canac'
  size: md
---
::

::note
Prop `alt` được truyền cho phần tử `img` dưới dạng thuộc tính `alt`.
::

## Examples

### With tooltip

Bạn có thể sử dụng thành phần [Tooltip](/components/tooltip) để hiển thị chú giải khi di chuột lên Avatar.

:component-example{name="avatar-tooltip-example"}

### With chip

Bạn có thể sử dụng thành phần [Chip](/components/chip) để hiển thị chip xung quanh Avatar.

:component-example{name="avatar-chip-example"}

## API

### Props

:component-props

## Theme

:component-theme

## Changelog

:component-changelog
