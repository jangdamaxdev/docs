---
title: FileUpload
description: 'An input element to upload files.'
category: form
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/FileUpload.vue
navigation.badge: New
---

## Usage

Sử dụng directive `v-model` để kiểm soát giá trị của FileUpload.

::component-code
---
ignore:
  - modelValue
  - class
external:
  - modelValue
props:
  modelValue: null
  class: 'w-96 min-h-48'
---
::

### Multiple

Sử dụng prop `multiple` để cho phép chọn nhiều tệp.

::component-code
---
ignore:
  - class
props:
  multiple: true
  class: 'w-96 min-h-48'
---
::

### Dropzone

Sử dụng prop `dropzone` để bật/tắt khu vực thả. Mặc định là `true`.

::component-code
---
ignore:
  - class
props:
  dropzone: false
  class: 'w-96 min-h-48'
---
::

### Interactive

Sử dụng prop `interactive` để bật/tắt khu vực có thể nhấp. Mặc định là `true`.

::tip{to="#with-files-bottom-slot"}
Điều này có thể hữu ích khi thêm một thành phần [`Button`](/components/button) trong slot `#actions`.
::

::component-code
---
ignore:
  - class
props:
  interactive: false
  class: 'w-96 min-h-48'
---
::

### Accept

Sử dụng prop `accept` để chỉ định các loại tệp được phép cho input. Cung cấp một danh sách được phân tách bằng dấu phẩy của [MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/MIME_types) hoặc phần mở rộng tệp (ví dụ: `image/png,application/pdf,.jpg`). Mặc định là `*` (tất cả loại tệp).

::component-code
---
ignore:
  - accept
  - class
props:
  accept: 'image/*'
  class: 'w-96 min-h-48'
---
::

### Label

Sử dụng prop `label` để đặt nhãn của FileUpload.

::component-code
---
prettier: true
ignore:
  - class
props:
  label: 'Drop your image here'
  class: 'w-96 min-h-48'
---
::

### Description

Sử dụng prop `description` để đặt mô tả của FileUpload.

::component-code
---
prettier: true
ignore:
  - label
  - class
props:
  label: 'Drop your image here'
  description: 'SVG, PNG, JPG or GIF (max. 2MB)'
  class: 'w-96 min-h-48'
---
::

### Icon

Sử dụng prop `icon` để đặt biểu tượng của FileUpload. Mặc định là `i-lucide-upload`.

::component-code
---
prettier: true
ignore:
  - label
  - description
  - class
props:
  icon: 'i-lucide-image'
  label: 'Drop your image here'
  description: 'SVG, PNG, JPG or GIF (max. 2MB)'
  class: 'w-96 min-h-48'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.upload`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.upload`.
:::
::

### Color

Sử dụng prop `color` để thay đổi màu sắc của FileUpload.

::component-code
---
prettier: true
ignore:
  - label
  - description
  - class
props:
  color: neutral
  highlight: true
  label: 'Drop your image here'
  description: 'SVG, PNG, JPG or GIF (max. 2MB)'
  class: 'w-96 min-h-48'
---
::

::note
Prop `highlight` được sử dụng ở đây để hiển thị trạng thái focus. Nó được sử dụng nội bộ khi xảy ra lỗi xác thực.
::

### Variant

Sử dụng prop `variant` để thay đổi biến thể của FileUpload.

::component-code
---
ignore:
  - class
props:
  variant: button
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của FileUpload.

::component-code
---
prettier: true
ignore:
  - label
  - description
  - class
props:
  size: xl
  variant: area
  label: 'Drop your image here'
  description: 'SVG, PNG, JPG or GIF (max. 2MB)'
---
::

### Layout

Sử dụng prop `layout` để thay đổi cách các tệp được hiển thị trong FileUpload. Mặc định là `grid`.

::warning
Prop này chỉ hoạt động khi `variant` là `area`.
::

::component-code
---
prettier: true
ignore:
  - label
  - description
  - multiple
  - class
  - ui.base
props:
  layout: list
  multiple: true
  label: 'Drop your images here'
  description: 'SVG, PNG, JPG or GIF (max. 2MB)'
  class: 'w-96'
  ui:
    base: 'min-h-48'
---
::

### Position

Sử dụng prop `position` để thay đổi vị trí của các tệp trong FileUpload. Mặc định là `outside`.

::warning
Prop này chỉ hoạt động khi `variant` là `area` và khi `layout` là `list`.
::

::component-code
---
prettier: true
ignore:
  - label
  - description
  - multiple
  - layout
  - class
  - ui.base
props:
  position: inside
  layout: list
  multiple: true
  label: 'Drop your images here'
  description: 'SVG, PNG, JPG or GIF (max. 2MB)'
  class: 'w-96'
  ui:
    base: 'min-h-48'
---
::

## Examples

### With Form validation

Bạn có thể sử dụng FileUpload trong các thành phần [Form](/components/form) và [FormField](/components/form-field) để xử lý xác thực và xử lý lỗi.

::component-example
---
prettier: true
collapse: true
name: 'file-upload-form-validation-example'
---
::

### With default slot

Bạn có thể sử dụng slot mặc định để tạo thành phần FileUpload của riêng bạn.

::component-example
---
prettier: true
collapse: true
name: 'file-upload-default-slot-example'
---
::

### With files-bottom slot

Bạn có thể sử dụng slot `files-bottom` để thêm một [Button](/components/button) dưới danh sách tệp để xóa tất cả tệp ví dụ.

::component-example
---
prettier: true
collapse: true
name: 'file-upload-files-bottom-slot-example'
---
::

::note{to="#interactive"}
Prop `interactive` được đặt thành `false` trong ví dụ này để ngăn khu vực có thể nhấp mặc định.
::

### With files-top slot

Bạn có thể sử dụng slot `files-top` để thêm một [Button](/components/button) trên danh sách tệp để thêm tệp mới ví dụ.

::component-example
---
prettier: true
collapse: true
name: 'file-upload-files-top-slot-example'
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

| Name | Type |
| ---- | ---- |
| `inputRef`{lang="ts-type"} | `Ref<HTMLInputElement \| null>`{lang="ts-type"} |
| `dropzoneRef`{lang="ts-type"} | `Ref<HTMLDivElement \| null>`{lang="ts-type"} |

## Theme

:component-theme

## Changelog

:component-changelog
