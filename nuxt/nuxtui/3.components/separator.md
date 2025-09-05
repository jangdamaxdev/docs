---
description: Phân tách nội dung theo chiều ngang hoặc dọc.
category: layout
links:
  - label: Separator
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/separator
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Separator.vue
---

## Usage

Sử dụng Separator component as-is để phân tách nội dung.

::component-code
---
class: 'p-8'
---
::

### Orientation

Sử dụng prop `orientation` để thay đổi hướng của Separator. Mặc định là `horizontal`.

::component-code
---
ignore:
  - class
class: 'p-8'
props:
  orientation: vertical
  class: 'h-48'
---
::

### Label

Sử dụng prop `label` để hiển thị một label ở giữa Separator.

::component-code
---
class: 'p-8'
props:
  label: 'Hello World'
---
::

### Icon

Sử dụng prop `icon` để hiển thị một icon ở giữa Separator.

::component-code
---
class: 'p-8'
props:
  icon: 'i-simple-icons-nuxtdotjs'
---
::

### Avatar

Sử dụng prop `avatar` để hiển thị một avatar ở giữa Separator.

::component-code
---
prettier: true
class: 'p-8'
props:
  avatar:
    src: 'https://github.com/nuxt.png'
---
::

### Color

Sử dụng prop `color` để thay đổi màu của Separator. Mặc định là `neutral`.

::component-code
---
class: 'p-8'
props:
  color: primary
  type: solid
---
::

### Type

Sử dụng prop `type` để thay đổi loại của Separator. Mặc định là `solid`.

::component-code
---
class: 'p-8'
props:
  type: dashed
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của Separator. Mặc định là `xs`.

::component-code
---
class: 'p-8'
props:
  size: lg
---
::

## API

### Props

:component-props

### Slots

:component-slots

## Theme

:component-theme

## Changelog

:component-changelog