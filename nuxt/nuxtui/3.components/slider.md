---
description: Một input để chọn một giá trị số trong một phạm vi.
category: form
links:
  - label: Slider
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/slider
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Slider.vue
---

## Usage

Sử dụng directive `v-model` để kiểm soát giá trị của Slider.

::component-code
---
external:
  - modelValue
props:
  modelValue: 50
---
::

Sử dụng prop `default-value` để đặt giá trị ban đầu khi bạn không cần kiểm soát trạng thái của nó.

::component-code
---
ignore:
  - defaultValue
props:
  defaultValue: 50
---
::

### Min / Max

Sử dụng prop `min` và `max` để đặt giá trị tối thiểu và tối đa của Slider. Mặc định là `0` và `100`.

::component-code
---
ignore:
  - defaultValue
props:
  min: 0
  max: 50
  defaultValue: 50
---
::

### Step

Sử dụng prop `step` để đặt giá trị tăng của Slider. Mặc định là `1`.

::component-code
---
ignore:
  - defaultValue
props:
  step: 10
  defaultValue: 50
---
::

### Multiple

Sử dụng directive `v-model` hoặc prop `default-value` với một mảng giá trị để tạo một range Slider.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: [25, 75]
---
::

Sử dụng prop `min-steps-between-thumbs` để giới hạn khoảng cách tối thiểu giữa các thumbs.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: [25, 50, 75]
  minStepsBetweenThumbs: 10
---
::

### Orientation

Sử dụng prop `orientation` để thay đổi hướng của Slider. Mặc định là `horizontal`.

::component-code
---
ignore:
  - defaultValue
  - class
props:
  orientation: vertical
  defaultValue: 50
  class: 'h-48'
---
::

### Color

Sử dụng prop `color` để thay đổi màu của Slider.

::component-code
---
ignore:
  - defaultValue
props:
  color: neutral
  defaultValue: 50
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của Slider.

::component-code
---
ignore:
  - defaultValue
props:
  size: xl
  defaultValue: 50
---
::

### Tooltip

Sử dụng prop `tooltip` để hiển thị một [Tooltip](/components/tooltip) xung quanh các thumbs của Slider với giá trị hiện tại. Bạn có thể đặt nó thành `true` cho hành vi mặc định hoặc truyền một object để tùy chỉnh với bất kỳ thuộc tính nào từ thành phần [Tooltip](/components/tooltip#props).

::component-code
---
ignore:
  - defaultValue
  - tooltip
props:
  defaultValue: 50
  tooltip: true
---
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa Slider.

::component-code
---
ignore:
  - defaultValue
props:
  disabled: true
  defaultValue: 50
---
::

### Inverted

Sử dụng prop `inverted` để đảo ngược trực quan Slider.

::component-code
---
ignore:
  - defaultValue
props:
  inverted: true
  defaultValue: 25
---
::

## API

### Props

:component-props

### Emits

:component-emits

## Theme

:component-theme

## Changelog

:component-changelog