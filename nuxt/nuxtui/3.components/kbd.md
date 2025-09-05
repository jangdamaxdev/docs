---
title: Kbd
description: Một phần tử kbd để hiển thị phím bàn phím.
category: element
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Kbd.vue
---

## Usage

### Value

Sử dụng slot mặc định để đặt giá trị của Kbd.

::component-code
---
slots:
  default: K
---
::

Bạn có thể đạt được kết quả tương tự bằng cách sử dụng prop `value`.

::component-code
---
props:
  value: K
---
::

Bạn có thể truyền các phím đặc biệt vào prop `value` mà đi qua composable [`useKbd`](https://github.com/nuxt/ui/blob/v3/src/runtime/composables/useKbd.ts). Ví dụ, phím `meta` hiển thị là `⌘` trên macOS và `Ctrl` trên các nền tảng khác.

::component-code
---
props:
  value: meta
items:
  value:
    - meta
    - win
    - command
    - shift
    - ctrl
    - option
    - alt
    - enter
    - delete
    - backspace
    - escape
    - tab
    - capslock
    - arrowup
    - arrowright
    - arrowdown
    - arrowleft
    - pageup
    - pagedown
    - home
    - end
---
::

### Color :badge{label="New" class="align-text-top"}

Sử dụng prop `color` để thay đổi màu của Kbd.

::component-code
---
props:
  color: neutral
slots:
  default: K
---
::

### Variant

Sử dụng prop `variant` để thay đổi biến thể của Kbd.

::component-code
---
props:
  color: neutral
  variant: solid
slots:
  default: K
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của Kbd.

::component-code
---
props:
  size: lg
slots:
  default: K
---
::

## Examples

### `class` prop

Sử dụng prop `class` để ghi đè các kiểu cơ sở của Badge.

::component-code
---
props:
  class: 'font-bold rounded-full'
  variant: subtle
slots:
  default: K
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
