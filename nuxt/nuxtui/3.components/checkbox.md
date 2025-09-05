---
description: Một phần tử đầu vào để chuyển đổi giữa các trạng thái đã kiểm tra và chưa kiểm tra.
category: form
links:
  - label: Checkbox
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/checkbox
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Checkbox.vue
---

## Usage

Sử dụng chỉ thị `v-model` để kiểm soát trạng thái đã kiểm tra của Checkbox.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: true
---
::

Sử dụng prop `default-value` để đặt giá trị ban đầu khi bạn không cần kiểm soát trạng thái của nó.

::component-code
---
ignore:
  - defaultValue
props:
  defaultValue: true
---
::

### Indeterminate

Sử dụng giá trị `indeterminate` trong chỉ thị `v-model` hoặc prop `default-value` để đặt Checkbox ở trạng thái không xác định.

::component-code
---
ignore:
  - defaultValue
props:
  defaultValue: 'indeterminate'
---
::

### Indeterminate Icon

Sử dụng prop `indeterminate-icon` để tùy chỉnh biểu tượng không xác định. Mặc định là `i-lucide-minus`.

::component-code
---
ignore:
  - defaultValue
props:
  defaultValue: 'indeterminate'
  indeterminateIcon: 'i-lucide-plus'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.minus`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.minus`.
:::
::

### Label

Sử dụng prop `label` để đặt nhãn của Checkbox.

::component-code
---
props:
  label: Check me
---
::

Khi sử dụng prop `required`, một dấu hoa thị được thêm bên cạnh nhãn.

::component-code
---
ignore:
  - label
props:
  required: true
  label: Check me
---
::

### Description

Sử dụng prop `description` để đặt mô tả của Checkbox.

::component-code
---
ignore:
  - label
props:
  label: Check me
  description: 'This is a checkbox.'
---
::

### Icon

Sử dụng prop `icon` để đặt biểu tượng của Checkbox khi nó được kiểm tra. Mặc định là `i-lucide-check`.

::component-code
---
ignore:
  - label
  - defaultValue
props:
  icon: 'i-lucide-heart'
  defaultValue: true
  label: Check me
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.check`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.check`.
:::
::

### Color

Sử dụng prop `color` để thay đổi màu sắc của Checkbox.

::component-code
---
ignore:
  - label
  - defaultValue
props:
  color: neutral
  defaultValue: true
  label: Check me
---
::

### Variant

Sử dụng prop `variant` để thay đổi biến thể của Checkbox.

::component-code
---
ignore:
  - label
  - defaultValue
props:
  color: 'primary'
  variant: 'card'
  defaultValue: true
  label: Check me
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của Checkbox.

::component-code
---
ignore:
  - label
  - defaultValue
props:
  size: xl
  variant: list
  defaultValue: true
  label: Check me
---
::

### Indicator

Sử dụng prop `indicator` để thay đổi vị trí hoặc ẩn chỉ báo. Mặc định là `start`.

::component-code
---
ignore:
  - label
  - defaultValue
props:
  indicator: 'end'
  variant: 'card'
  defaultValue: true
  label: Check me
---
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa Checkbox.

::component-code
---
ignore:
  - label
props:
  disabled: true
  label: Check me
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
