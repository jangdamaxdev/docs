---
title: InputTags
description: An input element that displays interactive tags.
category: form
links:
  - label: InputTags
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/tags-input
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/InputTags.vue
---

## Usage

Sử dụng directive `v-model` để kiểm soát giá trị của InputTags.

::component-code
---
prettier: true
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: ['Vue']
---
::

Sử dụng prop `default-value` để đặt giá trị ban đầu khi bạn không cần kiểm soát trạng thái của nó.

::component-code
---
prettier: true
ignore:
  - defaultValue
props:
  defaultValue: ['Vue']
---
::

### Placeholder

Sử dụng prop `placeholder` để đặt văn bản placeholder.

::component-code
---
props:
  placeholder: 'Enter tags...'
---
::

### Max Length :badge{label="New" class="align-text-top"}

Sử dụng prop `max-length` để đặt số ký tự tối đa được phép trong một thẻ.

::component-code
---
props:
  maxLength: 4
---
::

### Color

Sử dụng prop `color` để thay đổi màu vòng khi InputTags được focus.

::component-code
---
prettier: true
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: ['Vue']
  color: neutral
  highlight: true
---
::

::note
Prop `highlight` được sử dụng ở đây để hiển thị trạng thái focus. Nó được sử dụng nội bộ khi xảy ra lỗi xác thực.
::

### Variants

Sử dụng prop `variant` để thay đổi giao diện của InputTags.

::component-code
---
prettier: true
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: ['Vue']
  variant: subtle
  color: neutral
  highlight: false
---
::

### Sizes

Sử dụng prop `size` để điều chỉnh kích thước của InputTags.

::component-code
---
prettier: true
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: ['Vue']
  size: xl
---
::

### Icon

Sử dụng prop `icon` để hiển thị một [Icon](/components/icon) bên trong InputTags.

::component-code
---
prettier: true
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: ['Vue']
  icon: 'i-lucide-search'
  size: md
  variant: outline
---
::

::note
Sử dụng prop `leading` và `trailing` để đặt vị trí biểu tượng hoặc prop `leading-icon` và `trailing-icon` để đặt biểu tượng khác cho mỗi vị trí.
::

### Avatar

Sử dụng prop `avatar` để hiển thị một [Avatar](/components/avatar) bên trong InputTags.

::component-code
---
prettier: true
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: ['Vue']
  avatar:
    src: 'https://github.com/vuejs.png'
  size: md
  variant: outline
---
::

### Delete Icon

Sử dụng prop `delete-icon` để tùy chỉnh [Icon](/components/icon) xóa trong các thẻ. Mặc định là `i-lucide-x`.

::component-code
---
prettier: true
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: ['Vue']
  deleteIcon: 'i-lucide-trash'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.close`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.close`.
:::
::

### Loading

Sử dụng prop `loading` để hiển thị biểu tượng loading trên InputTags.

::component-code
---
prettier: true
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: ['Vue']
  loading: true
  trailing: false
---
::

### Loading Icon

Sử dụng prop `loading-icon` để tùy chỉnh biểu tượng loading. Mặc định là `i-lucide-loader-circle`.

::component-code
---
prettier: true
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: ['Vue']
  loading: true
  loadingIcon: 'i-lucide-loader'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.loading`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.loading`.
:::
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa InputTags.

::component-code
---
prettier: true
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: ['Vue']
  disabled: true
---
::

## Examples

### Within a FormField

Bạn có thể sử dụng InputTags trong thành phần [FormField](/components/form-field) để hiển thị nhãn, văn bản trợ giúp, chỉ báo bắt buộc, v.v.

::component-example
---
name: 'input-tags-form-field-example'
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
| `inputRef`{lang="ts-type"} | `Ref<InstanceType<typeof TagsInputInput> \| null>`{lang="ts-type"} |

## Theme

:component-theme

## Changelog

:component-changelog
