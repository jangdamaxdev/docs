---
title: ColorPicker
description: Một thành phần để chọn màu sắc.
category: form
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/ColorPicker.vue
---

## Usage

Sử dụng chỉ thị `v-model` để kiểm soát giá trị của ColorPicker.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: '#00C16A'
---
::

Sử dụng prop `default-value` để đặt giá trị ban đầu khi bạn không cần kiểm soát trạng thái của nó.

::component-code
---
ignore:
  - defaultValue
props:
  defaultValue: '#00BCD4'
---
::

### RGB Format

Sử dụng prop `format` để đặt giá trị `rgb` của ColorPicker.

::component-code
---
ignore:
  - modelValue
  - format
external:
  - modelValue
props:
  format: rgb
  modelValue: 'rgb(0, 193, 106)'
---
::

### HSL Format

Sử dụng prop `format` để đặt giá trị `hsl` của ColorPicker.

::component-code
---
ignore:
  - modelValue
  - format
external:
  - modelValue
props:
  format: hsl
  modelValue: 'hsl(153, 100%, 37.8%)'
---
::

### CMYK Format

Sử dụng prop `format` để đặt giá trị `cmyk` của ColorPicker.

::component-code
---
ignore:
  - modelValue
  - format
external:
  - modelValue
props:
  format: cmyk
  modelValue: 'cmyk(100%, 0%, 45.08%, 24.31%)'
---
::

### CIELab Format

Sử dụng prop `format` để đặt giá trị `lab` của ColorPicker.

::component-code
---
ignore:
  - modelValue
  - format
external:
  - modelValue
props:
  format: lab
  modelValue: 'lab(68.88% -60.41% 32.55%)'
---
::

### Throttle

Sử dụng prop `throttle` để đặt giá trị throttle của ColorPicker.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  throttle: 100
  modelValue: '#00C16A'
---
::

### Size

Sử dụng prop `size` để đặt kích thước của ColorPicker.

::component-code
---
props:
  size: xl
---
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa ColorPicker.

::component-code
---
props:
  disabled: true
---
::

## Examples

### As a Color chooser

Sử dụng một thành phần [Button](/components/button) và [Popover](/components/popover) để tạo một bộ chọn màu.

::component-example
---
name: 'color-picker-chooser-example'
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
