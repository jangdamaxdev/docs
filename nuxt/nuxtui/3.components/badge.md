---
description: Một văn bản ngắn để đại diện cho trạng thái hoặc danh mục.
category: element
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Badge.vue
---

## Usage

### Label

Sử dụng slot mặc định để đặt nhãn của Badge.

::component-code
---
slots:
  default: Badge
---
::

Bạn có thể đạt được kết quả tương tự bằng cách sử dụng prop `label`.

::component-code
---
props:
  label: Badge
---
::

### Color

Sử dụng prop `color` để thay đổi màu sắc của Badge.

::component-code
---
props:
  color: neutral
slots:
  default: Badge
---
::

### Variant

Sử dụng prop `variant` để thay đổi biến thể của Badge.

::component-code
---
props:
  color: neutral
  variant: outline
slots:
  default: Badge
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của Badge.

::component-code
---
props:
  size: xl
slots:
  default: Badge
---
::

### Icon

Sử dụng prop `icon` để hiển thị một [Icon](/components/icon) bên trong Badge.

::component-code
---
props:
  icon: i-lucide-rocket
  size: md
  color: primary
  variant: solid
slots:
  default: Badge
---
::

Sử dụng prop `leading` và `trailing` để đặt vị trí biểu tượng hoặc prop `leading-icon` và `trailing-icon` để đặt biểu tượng khác nhau cho mỗi vị trí.

::component-code
---
props:
  trailingIcon: i-lucide-arrow-right
  size: md
slots:
  default: Badge
---
::

### Avatar

Sử dụng prop `avatar` để hiển thị một [Avatar](/components/avatar) bên trong Badge.

::component-code
---
prettier: true
props:
  avatar:
    src: 'https://github.com/nuxt.png'
  size: md
  color: neutral
  variant: outline
slots:
  default: |

    Badge
---
::

## Examples

### `class` prop

Sử dụng prop `class` để ghi đè các kiểu cơ sở của Badge.

::component-code
---
props:
  class: 'font-bold rounded-full'
slots:
  default: Badge
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
