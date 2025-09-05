---
description: Một phần tử nút có thể hoạt động như một liên kết hoặc kích hoạt một hành động.
category: element
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Button.vue
---

## Usage

### Label

Sử dụng slot mặc định để đặt nhãn của Button.

::component-code
---
slots:
  default: Button
---
::

Bạn có thể đạt được kết quả tương tự bằng cách sử dụng prop `label`.

::component-code
---
props:
  label: Button
---
::

### Color

Sử dụng prop `color` để thay đổi màu sắc của Button.

::component-code
---
props:
  color: neutral
slots:
  default: Button
---
::

### Variant

Sử dụng prop `variant` để thay đổi biến thể của Button.

::component-code
---
props:
  color: neutral
  variant: outline
slots:
  default: Button
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của Button.

::component-code
---
props:
  size: xl
slots:
  default: Button
---
::

### Icon

Sử dụng prop `icon` để hiển thị một [Icon](/components/icon) bên trong Button.

::component-code
---
props:
  icon: i-lucide-rocket
  size: md
  color: primary
  variant: solid
slots:
  default: Button
---
::

Sử dụng prop `leading` và `trailing` để đặt vị trí biểu tượng hoặc prop `leading-icon` và `trailing-icon` để đặt biểu tượng khác nhau cho mỗi vị trí.

::component-code
---
props:
  trailingIcon: i-lucide-arrow-right
  size: md
slots:
  default: Button
---
::

Phần tử `label` dưới dạng prop hoặc slot là tùy chọn nên bạn có thể sử dụng Button dưới dạng nút chỉ biểu tượng.

::component-code
---
props:
  icon: i-lucide-search
  size: md
  color: primary
  variant: solid
---
::

### Avatar

Sử dụng prop `avatar` để hiển thị một [Avatar](/components/avatar) bên trong Button.

::component-code
---
prettier: true
props:
  avatar:
    src: 'https://github.com/nuxt.png'
  size: md
  color: neutral
  variant: outline
slots:
  default: |

    Button
---
::

Phần tử `label` dưới dạng prop hoặc slot là tùy chọn nên bạn có thể sử dụng Button dưới dạng nút chỉ avatar.

::component-code
---
prettier: true
props:
  avatar:
    src: 'https://github.com/nuxt.png'
  size: md
  color: neutral
  variant: outline
---
::

### Link

Bạn có thể truyền bất kỳ thuộc tính nào từ thành phần [Link](/components/link#props) như `to`, `target`, v.v.

::component-code
---
ignore:
  - target
props:
  to: https://github.com/nuxt/ui
  target: _blank
slots:
  default: Button
---
::

Khi Button là liên kết hoặc khi sử dụng prop `active`, bạn có thể sử dụng prop `active-color` và `active-variant` để tùy chỉnh trạng thái hoạt động.

::component-code
---
prettier: true
ignore:
  - color
  - variant
items:
  activeColor:
    - primary
    - secondary
    - success
    - info
    - warning
    - error
    - neutral
  activeVariant:
    - solid
    - outline
    - soft
    - subtle
    - ghost
    - link
props:
  active: true
  color: neutral
  variant: outline
  activeColor: primary
  activeVariant: solid
slots:
  default: |

    Button
---

Button
::

Bạn cũng có thể sử dụng prop `active-class` và `inactive-class` để tùy chỉnh trạng thái hoạt động.

::component-code
---
props:
  active: true
  activeClass: 'font-bold'
  inactiveClass: 'font-light'
slots:
  default: Button
---

Button
::

::tip
Bạn có thể cấu hình các kiểu này toàn cục trong tệp `app.config.ts` của bạn dưới khóa `ui.button.variants.active`.

```ts
export default defineAppConfig({
  ui: {
    button: {
      variants: {
        active: {
          true: {
            base: 'font-bold'
          }
        }
      }
    }
  }
})
```
::

### Loading

Sử dụng prop `loading` để hiển thị biểu tượng tải và vô hiệu hóa Button.

::component-code
---
props:
  loading: true
  trailing: false
slots:
  default: Button
---
Button
::

Sử dụng prop `loading-auto` để hiển thị biểu tượng tải tự động trong khi promise `@click` đang chờ.

:component-example{name="button-loading-auto-example"}

Điều này cũng hoạt động với thành phần [Form](/components/form).

:component-example{name="button-loading-auto-form-example"}

### Loading Icon

Sử dụng prop `loading-icon` để tùy chỉnh biểu tượng tải. Mặc định là `i-lucide-loader-circle`.

::component-code
---
props:
  loading: true
  loadingIcon: 'i-lucide-loader'
slots:
  default: Button
---
Button
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` dưới khóa `ui.icons.loading`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` dưới khóa `ui.icons.loading`.
:::
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa Button.

::component-code
---
props:
  disabled: true
slots:
  default: Button
---

Button
::

## Examples

### `class` prop

Sử dụng prop `class` để ghi đè các kiểu cơ sở của Button.

::component-code
---
props:
  class: 'font-bold rounded-full'
slots:
  default: Button
---
::

### `ui` prop

Sử dụng prop `ui` để ghi đè các kiểu slot của Button.

::component-code
---
prettier: true
ignore:
  - ui
  - color
  - variant
  - icon
props:
  icon: i-lucide-rocket
  color: neutral
  variant: outline
  ui:
    leadingIcon: 'text-primary'
slots:
  default: |

    Button
---
::

## API

### Props

:component-props

::callout{icon="i-simple-icons-github" to="https://github.com/nuxt/ui/blob/v3/src/runtime/components/Link.vue#L13"}
Thành phần `Button` mở rộng thành phần `Link`. Kiểm tra mã nguồn trên GitHub.
::

### Slots

:component-slots

## Theme

:component-theme

## Changelog

:component-changelog
