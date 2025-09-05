---
description: An input element to enter text.
category: form
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Input.vue
---

## Usage

Sử dụng directive `v-model` để kiểm soát giá trị của Input.

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

### Type

Sử dụng prop `type` để thay đổi loại input. Mặc định là `text`.

Một số loại đã được triển khai trong các thành phần riêng của chúng như [Checkbox](/components/checkbox), [Radio](/components/radio-group), [InputNumber](/components/input-number) v.v. và những loại khác đã được tạo kiểu như `file` ví dụ.

::component-code
---
items:
  type:
    - text
    - number
    - password
    - search
    - file
props:
  type: 'file'
---
::

::callout{icon="i-simple-icons-mdnwebdocs" to="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types" target="_blank"}
Bạn có thể kiểm tra tất cả các loại có sẵn trên MDN Web Docs.
::

### Placeholder

Sử dụng prop `placeholder` để đặt văn bản placeholder.

::component-code
---
props:
  placeholder: 'Search...'
---
::

### Color

Sử dụng prop `color` để thay đổi màu vòng khi Input được focus.

::component-code
---
ignore:
  - placeholder
props:
  color: neutral
  highlight: true
  placeholder: 'Search...'
---
::

::note
Prop `highlight` được sử dụng ở đây để hiển thị trạng thái focus. Nó được sử dụng nội bộ khi xảy ra lỗi xác thực.
::

### Variant

Sử dụng prop `variant` để thay đổi biến thể của Input.

::component-code
---
ignore:
  - placeholder
props:
  color: neutral
  variant: subtle
  highlight: false
  placeholder: 'Search...'
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của Input.

::component-code
---
ignore:
  - placeholder
props:
  size: xl
  placeholder: 'Search...'
---
::

### Icon

Sử dụng prop `icon` để hiển thị một [Icon](/components/icon) bên trong Input.

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
---
::

### Avatar

Sử dụng prop `avatar` để hiển thị một [Avatar](/components/avatar) bên trong Input.

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
---
::

### Loading

Sử dụng prop `loading` để hiển thị biểu tượng loading trên Input.

::component-code
---
ignore:
  - placeholder
props:
  loading: true
  trailing: false
  placeholder: 'Search...'
---
::

### Loading Icon

Sử dụng prop `loading-icon` để tùy chỉnh biểu tượng loading. Mặc định là `i-lucide-loader-circle`.

::component-code
---
ignore:
  - placeholder
props:
  loading: true
  loadingIcon: 'i-lucide-loader'
  placeholder: 'Search...'
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

Sử dụng prop `disabled` để vô hiệu hóa Input.

::component-code
---
ignore:
  - placeholder
props:
  disabled: true
  placeholder: 'Search...'
---
::

## Examples

### With clear button

Bạn có thể đặt một [Button](/components/button) bên trong slot `#trailing` để xóa Input.

::component-example
---
name: 'input-clear-button-example'
---
::

### With copy button

Bạn có thể đặt một [Button](/components/button) bên trong slot `#trailing` để sao chép giá trị vào clipboard.

::component-example
---
name: 'input-copy-button-example'
---
::

### With password toggle

Bạn có thể đặt một [Button](/components/button) bên trong slot `#trailing` để chuyển đổi khả năng hiển thị mật khẩu.

::component-example
---
name: 'input-password-toggle-example'
---
::

### With password strength indicator

Bạn có thể sử dụng thành phần [Progress](/components/progress) để hiển thị chỉ báo độ mạnh mật khẩu.

::component-example
---
collapse: true
name: 'input-password-strength-indicator-example'
---
::

### With character limit

Bạn có thể sử dụng slot `#trailing` để thêm giới hạn ký tự cho Input.

::component-example
---
name: 'input-character-limit-example'
---
::

### With keyboard shortcut

Bạn có thể sử dụng thành phần [Kbd](/components/kbd) bên trong slot `#trailing` để thêm phím tắt bàn phím cho Input.

::component-example
---
name: 'input-kbd-example'
---
::

::note{to="/composables/define-shortcuts"}
Ví dụ này sử dụng composable `defineShortcuts` để focus Input khi phím :kbd{value="/"} được nhấn.
::

### With mask

Không có hỗ trợ tích hợp cho mặt nạ, nhưng bạn có thể sử dụng các thư viện như [maska](https://github.com/beholdr/maska) để che Input.

::component-example
---
name: 'input-mask-example'
---
::

### With floating label

Bạn có thể sử dụng slot `#default` để thêm nhãn nổi cho Input.

::component-example
---
name: 'input-floating-label-example'
---
::

### Within a FormField

Bạn có thể sử dụng Input trong thành phần [FormField](/components/form-field) để hiển thị nhãn, văn bản trợ giúp, chỉ báo bắt buộc, v.v.

::component-example
---
name: 'input-form-field-example'
---
::

::tip{to="/components/form"}
Nó cũng cung cấp xác thực và xử lý lỗi khi được sử dụng trong thành phần **Form**.
::

### Within a ButtonGroup

Bạn có thể sử dụng Input trong thành phần [ButtonGroup](/components/button-group) để nhóm nhiều phần tử lại với nhau.

::component-example
---
name: 'input-button-group-example'
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

## Theme

:component-theme

## Changelog

:component-changelog
