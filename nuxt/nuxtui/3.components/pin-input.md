---
title: PinInput
description: Một input element để enter a pin.
category: form
links:
  - label: PinInput
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/pin-input
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/PinInput.vue
---

## Usage

Sử dụng directive `v-model` để kiểm soát value của PinInput.

::component-code
---
prettier: true
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: []
---
::

Sử dụng prop `default-value` để đặt initial value khi bạn không cần kiểm soát state của nó.

::component-code
---
prettier: true
ignore:
  - defaultValue
props:
  defaultValue: ['1','2','3']
---
::

### Type

Sử dụng prop `type` để thay đổi input type. Mặc định là `text`.

::component-code
---
items:
  type:
    - text
    - number
props:
  type: 'number'
---
::

::note
Khi `type` được đặt thành `number`, nó sẽ chỉ accept numeric characters.
::

### Mask

Sử dụng prop `mask` để treat input như một password.

::component-code
---
prettier: true
ignore:
  - placeholder
  - defaultValue
props:
  mask: true
  defaultValue: ['1','2','3','4','5']
---
::

### OTP

Sử dụng prop `otp` để enable One-Time Password functionality. Khi enabled, mobile devices có thể automatically detect và fill OTP codes từ SMS messages hoặc clipboard content, với autocomplete support.

::component-code
---
props:
  otp: true
---
::

### Length

Sử dụng prop `length` để thay đổi amount of inputs.

::component-code
---
props:
  length: 6
---
::

### Placeholder

Sử dụng prop `placeholder` để đặt placeholder text.

::component-code
---
props:
  placeholder: '○'
---
::

### Color

Sử dụng prop `color` để thay đổi ring color khi PinInput được focused.

::component-code
---
ignore:
  - placeholder
props:
  color: neutral
  highlight: true
  placeholder: '○'
---
::

::note
Prop `highlight` được sử dụng ở đây để show focus state. Nó được sử dụng internally khi có validation error.
::

### Variant

Sử dụng prop `variant` để thay đổi variant của PinInput.

::component-code
---
ignore:
  - placeholder
props:
  color: neutral
  variant: subtle
  highlight: false
  placeholder: '○'
---
::

### Size

Sử dụng prop `size` để thay đổi size của PinInput.

::component-code
---
ignore:
  - placeholder
props:
  size: xl
  placeholder: '○'
---
::

### Disabled

Sử dụng prop `disabled` để disable PinInput.

::component-code
---
ignore:
  - placeholder
props:
  disabled: true
  placeholder: '○'
---
::

## API

### Props

:component-props

### Emits

:component-emits

### Expose

Khi accessing component via template ref, bạn có thể sử dụng:

| Name | Type |
| ---- | ---- |
| `inputsRef`{lang="ts-type"} | `Ref<ComponentPublicInstance[]>`{lang="ts-type"} |

## Theme

:component-theme

## Changelog

:component-changelog