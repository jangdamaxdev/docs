---
description: Một lời kêu gọi để thu hút sự chú ý của người dùng.
category: element
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Alert.vue
---

## Usage

### Title

Sử dụng prop `title` để đặt tiêu đề của Alert.

::component-code
---
props:
  title: 'Heads up!'
---
::

### Description

Sử dụng prop `description` để đặt mô tả của Alert.

::component-code
---
prettier: true
props:
  title: 'Heads up!'
  description: 'You can change the primary color in your app config.'
---
::

### Icon

Sử dụng prop `icon` để hiển thị một [Icon](/components/icon).

::component-code
---
prettier: true
ignore:
  - title
  - description
props:
  title: 'Heads up!'
  description: 'You can change the primary color in your app config.'
  icon: 'i-lucide-terminal'
---
::

### Avatar

Sử dụng prop `avatar` để hiển thị một [Avatar](/components/avatar).

::component-code
---
prettier: true
ignore:
  - title
  - description
props:
  title: 'Heads up!'
  description: 'You can change the primary color in your app config.'
  avatar.src: 'https://github.com/nuxt.png'
---
::

### Color

Sử dụng prop `color` để thay đổi màu sắc của Alert.

::component-code
---
prettier: true
ignore:
  - title
  - description
  - icon
props:
  color: neutral
  title: 'Heads up!'
  description: 'You can change the primary color in your app config.'
  icon: 'i-lucide-terminal'
---
::

### Variant

Sử dụng prop `variant` để thay đổi biến thể của Alert.

::component-code
---
prettier: true
ignore:
  - title
  - description
  - icon
props:
  color: neutral
  variant: subtle
  title: 'Heads up!'
  description: 'You can change the primary color in your app config.'
  icon: 'i-lucide-terminal'
---
::

### Close

Sử dụng prop `close` để hiển thị một [Button](/components/button) để đóng Alert.

::tip
Một sự kiện `update:open` sẽ được phát ra khi nút đóng được nhấp.
::

::component-code
---
prettier: true
ignore:
  - title
  - description
  - close
  - color
  - variant
props:
  title: 'Heads up!'
  description: 'You can change the primary color in your app config.'
  color: neutral
  variant: outline
  close: true
---
::

Bạn có thể truyền bất kỳ thuộc tính nào từ thành phần [Button](/components/button) để tùy chỉnh nó.

::component-code
---
prettier: true
ignore:
  - title
  - description
  - close.color
  - close.variant
  - color
  - variant
props:
  title: 'Heads up!'
  description: 'You can change the primary color in your app config.'
  color: neutral
  variant: outline
  close:
    color: primary
    variant: outline
    class: 'rounded-full'
---
::

### Close Icon

Sử dụng prop `close-icon` để tùy chỉnh [Icon](/components/icon) của nút đóng. Mặc định là `i-lucide-x`.

::component-code
---
prettier: true
ignore:
  - title
  - description
  - close
  - color
  - variant
props:
  title: 'Heads up!'
  description: 'You can change the primary color in your app config.'
  color: neutral
  variant: outline
  close: true
  closeIcon: 'i-lucide-arrow-right'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` dưới khóa `ui.icons.close`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` dưới khóa `ui.icons.close`.
:::
::

### Actions

Sử dụng prop `actions` để thêm một số hành động [Button](/components/button) vào Alert.

::component-code
---
prettier: true
ignore:
  - title
  - actions
  - color
  - variant
props:
  title: 'Heads up!'
  description: 'You can change the primary color in your app config.'
  color: neutral
  variant: outline
  actions:
    - label: Action 1
    - label: Action 2
      color: neutral
      variant: subtle
---
::

### Orientation

Sử dụng prop `orientation` để thay đổi hướng của Alert.

::component-code
---
prettier: true
ignore:
  - title
  - actions
  - color
  - variant
props:
  title: 'Heads up!'
  description: 'You can change the primary color in your app config.'
  color: neutral
  variant: outline
  orientation: horizontal
  actions:
    - label: Action 1
    - label: Action 2
      color: neutral
      variant: subtle
---
::

## Examples

### `class` prop

Sử dụng prop `class` để ghi đè các kiểu cơ sở của Alert.

::component-code
---
prettier: true
ignore:
  - title
  - description
props:
  title: 'Heads up!'
  description: 'You can change the primary color in your app config.'
  class: 'rounded-none'
---
::

### `ui` prop

Sử dụng prop `ui` để ghi đè các kiểu slot của Alert.

::component-code
---
prettier: true
ignore:
  - ui
  - title
  - description
  - icon
props:
  title: 'Heads up!'
  description: 'You can change the primary color in your app config.'
  icon: i-lucide-rocket
  ui:
    icon: 'size-11'
---
::

## API

### Props

:component-props

### Slots

:component-slots

### Emits

:component-emits

## Theme

:component-theme

## Changelog

:component-changelog
