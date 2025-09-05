---
description: A textarea element to input multi-line text.
category: form
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Textarea.vue
---

## Usage

Sử dụng directive `v-model` để kiểm soát giá trị của Textarea.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: ''
---
::

### Rows

Sử dụng prop `rows` để đặt số lượng hàng. Mặc định là `3`.

::component-code
---
props:
  rows: 12
---
::

### Placeholder

Sử dụng prop `placeholder` để đặt văn bản giữ chỗ.

::component-code
---
props:
  placeholder: 'Type something...'
---
::

### Autoresize

Sử dụng prop `autoresize` để bật tự động điều chỉnh kích thước chiều cao của Textarea.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: 'This is a long text that will autoresize the height of the Textarea.'
  autoresize: true
---
::

Sử dụng prop `maxrows` để đặt số lượng hàng tối đa khi tự động điều chỉnh. Nếu đặt thành `0`, Textarea sẽ tăng vô hạn.

::component-code
---
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: 'This is a long text that will autoresize the height of the Textarea with a maximum of 4 rows.'
  maxrows: 4
  autoresize: true
---
::

### Color

Sử dụng prop `color` để thay đổi màu vòng khi Textarea được tập trung.

::component-code
---
ignore:
  - placeholder
props:
  color: neutral
  highlight: true
  placeholder: 'Type something...'
---
::

::note
Prop `highlight` được sử dụng ở đây để hiển thị trạng thái tập trung. Nó được sử dụng nội bộ khi xảy ra lỗi xác thực.
::

### Variant

Sử dụng prop `variant` để thay đổi biến thể của Textarea.

::component-code
---
ignore:
  - placeholder
props:
  color: neutral
  variant: subtle
  highlight: false
  placeholder: 'Type something...'
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của Textarea.

::component-code
---
ignore:
  - placeholder
props:
  size: xl
  placeholder: 'Type something...'
---
::

### Icon

Sử dụng prop `icon` để hiển thị một [Icon](/components/icon) bên trong Textarea.

::component-code
---
prettier: true
ignore:
  - placeholder
props:
  icon: 'i-lucide-search'
  size: md
  variant: outline
  placeholder: 'Search...'
  rows: 1
---
::

Sử dụng prop `leading` và `trailing` để đặt vị trí biểu tượng hoặc prop `leading-icon` và `trailing-icon` để đặt biểu tượng khác cho mỗi vị trí.

::component-code
---
prettier: true
ignore:
  - placeholder
props:
  trailingIcon: i-lucide-at-sign
  placeholder: 'Enter your email'
  size: md
  rows: 1
---
::

### Avatar

Sử dụng prop `avatar` để hiển thị một [Avatar](/components/avatar) bên trong Textarea.

::component-code
---
prettier: true
ignore:
  - placeholder
props:
  avatar:
    src: 'https://github.com/nuxt.png'
  size: md
  variant: outline
  placeholder: 'Search...'
  rows: 1
---
::

### Loading

Sử dụng prop `loading` để hiển thị biểu tượng tải trên Textarea.

::component-code
---
ignore:
  - placeholder
props:
  loading: true
  trailing: false
  placeholder: 'Search...'
  rows: 1
---
::

### Loading Icon

Sử dụng prop `loading-icon` để tùy chỉnh biểu tượng tải. Mặc định là `i-lucide-loader-circle`.

::component-code
---
ignore:
  - placeholder
props:
  loading: true
  loadingIcon: 'i-lucide-loader'
  placeholder: 'Search...'
  rows: 1
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cầu trong `app.config.ts` của bạn dưới khóa `ui.icons.loading`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cầu trong `vite.config.ts` của bạn dưới khóa `ui.icons.loading`.
:::
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa Textarea.

::component-code
---
ignore:
  - placeholder
props:
  disabled: true
  placeholder: 'Type something...'
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

Khi truy cập thành phần qua template ref, bạn có thể sử dụng như sau:

| Name | Type |
| ---- | ---- |
| `textareaRef`{lang="ts-type"} | `Ref<HTMLTextAreaElement \| null>`{lang="ts-type"} |

## Theme

:component-theme

## Changelog

:component-changelog
