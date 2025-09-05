---
description: Một control chuyển đổi giữa hai trạng thái.
category: form
links:
  - label: Switch
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/switch
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Switch.vue
---

## Usage

Sử dụng directive `v-model` để kiểm soát trạng thái checked của Switch.

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

### Label

Sử dụng prop `label` để đặt label của Switch.

::component-code
---
props:
  label: Check me
---
::

Khi sử dụng prop `required`, một dấu hoa thị được thêm vào bên cạnh label.

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

Sử dụng prop `description` để đặt mô tả của Switch.

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

Sử dụng prop `checked-icon` và `unchecked-icon` để đặt icons của Switch khi checked và unchecked.

::component-code
---
prettier: true
ignore:
  - label
  - defaultValue
props:
  uncheckedIcon: 'i-lucide-x'
  checkedIcon: 'i-lucide-check'
  defaultValue: true
  label: Check me
---
::

### Loading

Sử dụng prop `loading` để hiển thị icon loading trên Switch.

::component-code
---
ignore:
  - label
  - defaultValue
props:
  loading: true
  defaultValue: true
  label: Check me
---
::

### Loading Icon

Sử dụng prop `loading-icon` để tùy chỉnh icon loading. Mặc định là `i-lucide-loader-circle`.

::component-code
---
ignore:
  - label
  - defaultValue
props:
  loading: true
  loadingIcon: 'i-lucide-loader'
  defaultValue: true
  label: Check me
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.loading`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.loading`.
:::
::

### Color

Sử dụng prop `color` để thay đổi màu của Switch.

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

### Size

Sử dụng prop `size` để thay đổi kích thước của Switch.

::component-code
---
ignore:
  - label
  - defaultValue
props:
  size: xl
  defaultValue: true
  label: Check me
---
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa Switch.

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