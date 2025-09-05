---
description: A succinct message to provide information or feedback to the user.
category: overlay
links:
  - label: Toast
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/toast
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Toast.vue
---

## Usage

Sử dụng composable [useToast](/composables/use-toast) để hiển thị toast trong ứng dụng của bạn.

::warning
Đảm bảo bao bọc ứng dụng của bạn với thành phần [`App`](/components/app) sử dụng thành phần [`Toaster`](https://github.com/nuxt/ui/blob/v3/src/runtime/components/Toaster.vue) của chúng tôi sử dụng thành phần [`ToastProvider`](https://reka-ui.com/docs/components/toast#provider) từ Reka UI.
::

::tip{to="/components/app#props"}
Bạn có thể kiểm tra prop `toaster` của thành phần `App` để xem cách cấu hình Toaster toàn cầu.
::

### Title

Truyền trường `title` cho phương thức `toast.add` để hiển thị tiêu đề.

::component-example
---
options:
  - name: 'title'
    label: 'title'
    default: 'Uh oh! Something went wrong.'
name: 'toast-title-example'
---
::

### Description

Truyền trường `description` cho phương thức `toast.add` để hiển thị mô tả.

::component-example
---
options:
  - name: 'title'
    label: 'title'
    default: 'Uh oh! Something went wrong.'
  - name: 'description'
    label: 'description'
    default: 'There was a problem with your request.'
name: 'toast-description-example'
---
::

### Icon

Truyền trường `icon` cho phương thức `toast.add` để hiển thị một [Icon](/components/icon).

::component-example
---
options:
  - name: 'icon'
    label: 'icon'
    default: 'i-lucide-wifi'
name: 'toast-icon-example'
---
::

### Avatar

Truyền trường `avatar` cho phương thức `toast.add` để hiển thị một [Avatar](/components/avatar).

::component-example
---
options:
  - name: 'avatar.src'
    alias: 'avatar'
    label: 'avatar.src'
    default:
      src: 'https://github.com/benjamincanac.png'
name: 'toast-avatar-example'
---
::

### Color

Truyền trường `color` cho phương thức `toast.add` để thay đổi màu sắc của Toast.

::component-example
---
options:
  - name: 'color'
    label: 'color'
    default: neutral
    items:
      - primary
      - secondary
      - success
      - info
      - warning
      - error
      - neutral
name: 'toast-color-example'
---
::

### Close

Truyền trường `close` để tùy chỉnh hoặc ẩn [Button](/components/button) đóng (với giá trị `false`).

::component-example
---
name: 'toast-close-example'
---
::

### Close Icon

Truyền trường `closeIcon` để tùy chỉnh [Icon](/components/icon) của nút đóng. Mặc định là `i-lucide-x`.

::component-example
---
options:
  - name: 'closeIcon'
    label: 'closeIcon'
    default: 'i-lucide-arrow-right'
name: 'toast-close-icon-example'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cầu trong `app.config.ts` của bạn dưới khóa `ui.icons.close`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cầu trong `vite.config.ts` của bạn dưới khóa `ui.icons.close`.
:::
::

### Actions

Truyền trường `actions` để thêm một số hành động [Button](/components/button) vào Toast.

::component-example
---
options:
  - name: 'description'
    label: 'description'
    default: 'There was a problem with your request.'
name: 'toast-actions-example'
---
::

### Progress :badge{label="New" class="align-text-top"}

Truyền trường `progress` để tùy chỉnh hoặc ẩn thanh [Progress](/components/progress) (với giá trị `false`).

::tip
Thanh Progress kế thừa màu Toast theo mặc định, nhưng bạn có thể ghi đè bằng trường `progress.color`.
::

::component-example
---
name: 'toast-progress-example'
---
::

### Orientation

Truyền trường `orientation` cho phương thức `toast.add` để thay đổi hướng của Toast.

::component-example
---
options:
  - name: 'orientation'
    label: 'orientation'
    default: 'horizontal'
    items:
      - horizontal
      - vertical
name: 'toast-orientation-example'
---
::

## Examples

### Change global position

Thay đổi prop `toaster.position` trên thành phần [App](/components/app#props) để thay đổi vị trí của các toast.

::component-example
---
prettier: true
name: 'toast-example'
---

#options
:toaster-position-example
::

::note{to="https://github.com/nuxt/ui/blob/v3/docs/app/app.config.ts#L3"}
Trong ví dụ này, chúng tôi sử dụng `AppConfig` để cấu hình prop `position` của thành phần `Toaster` toàn cầu.
::

### Change global duration

Thay đổi prop `toaster.duration` trên thành phần [App](/components/app#props) để thay đổi thời lượng của các toast.

::component-example
---
prettier: true
name: 'toast-example'
---

#options
:toaster-duration-example
::

::note{to="https://github.com/nuxt/ui/blob/v3/docs/app/app.config.ts#L5"}
Trong ví dụ này, chúng tôi sử dụng `AppConfig` để cấu hình prop `duration` của thành phần `Toaster` toàn cầu.
::

### Stacked toasts

Đặt prop `toaster.expand` thành `false` trên thành phần [App](/components/app#props) để hiển thị các toast xếp chồng.

::tip
Bạn có thể di chuột qua các toast để mở rộng chúng. Điều này cũng sẽ tạm dừng bộ đếm thời gian của các toast.
::

::component-example
---
prettier: true
name: 'toast-example'
---

#options
:toaster-expand-example
::

::note{to="https://github.com/nuxt/ui/blob/v3/docs/app/app.config.ts#L4"}
Trong ví dụ này, chúng tôi sử dụng `AppConfig` để cấu hình prop `expand` của thành phần `Toaster` toàn cầu.
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
