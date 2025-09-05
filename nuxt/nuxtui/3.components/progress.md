---
description: Một indicator showing the progress of a task.
category: element
links:
  - label: Progress
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/progress
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Progress.vue
---

## Usage

Sử dụng directive `v-model` để kiểm soát value của Progress.

::component-code
---
external:
  - modelValue
props:
  modelValue: 50
---
::

### Max

Sử dụng prop `max` để đặt maximum value của Progress.

::component-code
---
external:
  - modelValue
props:
  modelValue: 3
  max: 4
---
::

Sử dụng prop `max` với một array of strings để hiển thị active step dưới bar, maximum value của Progress là length của array.

::component-code
---
prettier: true
ignore:
  - max
external:
  - modelValue
props:
  modelValue: 3
  max:
    - 'Waiting...'
    - 'Cloning...'
    - 'Migrating...'
    - 'Deploying...'
    - 'Done!'
---
::

### Status

Sử dụng prop `status` để hiển thị current Progress value above the bar.

::component-code
---
external:
  - modelValue
props:
  modelValue: 50
  status: true
---
::

### Indeterminate

Khi no `v-model` được set hoặc value là `null`, Progress trở thành _indeterminate_. Progress bar được animated như một `carousel`, nhưng bạn có thể thay đổi nó bằng prop [`animation`](#animation).

::component-code
---
external:
  - modelValue
props:
  modelValue: null
---
::

### Animation

Sử dụng prop `animation` để thay đổi animation của Progress thành inverse carousel, swinging bar hoặc elastic bar. Mặc định là `carousel`.

::component-code
---
props:
  animation: swing
---
::

### Orientation

Sử dụng prop `orientation` để thay đổi orientation của Progress. Mặc định là `horizontal`.

::component-code
---
ignore:
  - class
props:
  orientation: vertical
  class: 'h-48'
---
::

### Color

Sử dụng prop `color` để thay đổi color của Slider.

::component-code
---
props:
  color: neutral
---
::

### Size

Sử dụng prop `size` để thay đổi size của Slider.

::component-code
---
props:
  size: xl
---
::

### Inverted

Sử dụng prop `inverted` để visually invert Progress.

::component-code
---
props:
  inverted: true
  modelValue: 25
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