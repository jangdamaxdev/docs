---
title: InputNumber
description: An input for numerical values with a customizable range.
category: form
links:
  - label: NumberField
    icon: i-custom-reka-ui
    to: https://www.reka-ui.com/docs/components/number-field
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/InputNumber.vue
---

::note
Thành phần này dựa vào gói [`@internationalized/number`](https://react-spectrum.adobe.com/internationalized/number/index.html) cung cấp tiện ích để định dạng và phân tích số trên các locale và hệ thống đánh số.
::

## Usage

Sử dụng directive `v-model` để kiểm soát giá trị của InputNumber.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: 5
---
::

Sử dụng prop `default-value` để đặt giá trị ban đầu khi bạn không cần kiểm soát trạng thái của nó.

::component-code
---
ignore:
  - defaultValue
props:
  defaultValue: 5
---
::

### Min / Max

Sử dụng prop `min` và `max` để đặt giá trị tối thiểu và tối đa của InputNumber.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: 5
  min: 0
  max: 10
---
::

### Step

Sử dụng prop `step` để đặt giá trị bước của InputNumber.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: 5
  step: 2
---
::

### Orientation

Sử dụng prop `orientation` để thay đổi hướng của InputNumber.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: 5
  orientation: vertical
---
::

### Placeholder

Sử dụng prop `placeholder` để đặt văn bản placeholder.

::component-code
---
props:
  placeholder: 'Enter a number'
---
::

### Color

Sử dụng prop `color` để thay đổi màu vòng khi InputNumber được focus.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: 5
  color: neutral
  highlight: true
---
::

### Variant

Sử dụng prop `variant` để thay đổi biến thể của InputNumber.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: 5
  variant: subtle
  color: neutral
  highlight: false
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của InputNumber.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: 5
  size: xl
---
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa InputNumber.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: 5
  disabled: true
---
::

### Increment / Decrement

Sử dụng prop `increment` và `decrement` để tùy chỉnh các nút tăng và giảm với bất kỳ prop [Button](/components/button) nào. Mặc định là `{ variant: 'link' }`{lang="ts-type"}.

::component-code
---
prettier: true
ignore:
  - modelValue
  - increment.size
  - increment.color
  - increment.variant
  - decrement.size
  - decrement.color
  - decrement.variant
external:
  - modelValue
props:
  modelValue: 5
  increment:
    color: neutral
    variant: solid
    size: xs
  decrement:
    color: neutral
    variant: solid
    size: xs
---
::

### Increment / Decrement Icons

Sử dụng prop `increment-icon` và `decrement-icon` để tùy chỉnh [Icon](/components/icon) của các nút. Mặc định là `i-lucide-plus` / `i-lucide-minus`.

::component-code
---
prettier: true
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: 5
  incrementIcon: 'i-lucide-arrow-right'
  decrementIcon: 'i-lucide-arrow-left'
---
::

## Examples

### With decimal format

Sử dụng prop `format-options` để tùy chỉnh định dạng của giá trị.

::component-example
---
name: 'input-number-decimal-example'
---
::

### With percentage format

Sử dụng prop `format-options` với `style: 'percent'` để tùy chỉnh định dạng của giá trị.

::component-example
---
name: 'input-number-percentage-example'
---
::

### With currency format

Sử dụng prop `format-options` với `style: 'currency'` để tùy chỉnh định dạng của giá trị.

::component-example
---
name: 'input-number-currency-example'
---
::

### Within a FormField

Bạn có thể sử dụng InputNumber trong thành phần [FormField](/components/form-field) để hiển thị nhãn, văn bản trợ giúp, chỉ báo bắt buộc, v.v.

::component-example
---
name: 'input-number-form-field-example'
---
::

### With slots

Sử dụng slot `#increment` và `#decrement` để tùy chỉnh các nút.

::component-example
---
name: 'input-number-slots-example'
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

When accessing the component via a template ref, you can use the following:

| Name                       | Type                                            |
| -------------------------- | ----------------------------------------------- |
| `inputRef`{lang="ts-type"} | `Ref<InstanceType<typeof NumberFieldInput> \| null>`{lang="ts-type"} |

## Theme

:component-theme

## Changelog

:component-changelog
