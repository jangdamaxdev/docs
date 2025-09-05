---
description: Một tập các bước được sử dụng để chỉ ra tiến trình qua một quy trình đa bước.
category: navigation
links:
  - label: Stepper
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/stepper
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Stepper.vue
---

## Usage

### Items

Sử dụng prop `items` dưới dạng mảng các đối tượng với các thuộc tính sau:

- `title?: string`{lang="ts-type"}
- `description?: AvatarProps`{lang="ts-type"}
- `content?: string`{lang="ts-type"}
- `icon?: string`{lang="ts-type"}
- `value?: string | number`{lang="ts-type"}
- `disabled?: boolean`{lang="ts-type"}
- [`slot?: string`{lang="ts-type"}](#with-custom-slot)
- `class?: any`{lang="ts-type"}
- `ui?: { item?: ClassNameValue, container?: ClassNameValue, trigger?: ClassNameValue, indicator?: ClassNameValue, icon?: ClassNameValue, separator?: ClassNameValue, wrapper?: ClassNameValue, title?: ClassNameValue, description?: ClassNameValue }`{lang="ts-type"}

::component-code
---
ignore:
  - items
  - class
external:
  - items
externalTypes:
  - StepperItem[]
props:
  items:
    - title: 'Address'
      description: 'Add your address here'
      icon: 'i-lucide-house'
    - title: 'Shipping'
      description: 'Set your preferred shipping method'
      icon: 'i-lucide-truck'
    - title: 'Checkout'
      description: 'Confirm your order'
  class: 'w-full'
---
::

::note
Nhấp vào các mục để điều hướng qua các bước.
::

### Color

Sử dụng prop `color` để thay đổi màu của Stepper.

::component-code
---
ignore:
  - content
  - items
  - class
external:
  - items
externalTypes:
  - StepperItem[]
props:
  color: neutral
  items:
    - title: 'Address'
      description: 'Add your address here'
      icon: 'i-lucide-house'
    - title: 'Shipping'
      description: 'Set your preferred shipping method'
      icon: 'i-lucide-truck'
    - title: 'Checkout'
      description: 'Confirm your order'
  class: 'w-full'
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của Stepper.

::component-code
---
ignore:
  - content
  - items
  - class
external:
  - items
externalTypes:
  - StepperItem[]
props:
  size: xl
  items:
  - title: 'Address'
    description: 'Add your address here'
    icon: 'i-lucide-house'
  - title: 'Shipping'
    description: 'Set your preferred shipping method'
    icon: 'i-lucide-truck'
  - title: 'Checkout'
    description: 'Confirm your order'
  class: 'w-full'
---
::

### Orientation

Sử dụng prop `orientation` để thay đổi hướng của Stepper. Mặc định là `horizontal`.

::component-code
---
ignore:
  - content
  - items
  - class
external:
  - items
externalTypes:
  - StepperItem[]
props:
  orientation: vertical
  items:
  - title: 'Address'
    description: 'Add your address here'
    icon: 'i-lucide-house'
  - title: 'Shipping'
    description: 'Set your preferred shipping method'
    icon: 'i-lucide-truck'
  - title: 'Checkout'
    description: 'Confirm your order'
  class: 'w-full'
---
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa điều hướng qua các bước.

::component-code
---
ignore:
  - content
  - items
  - class
external:
  - items
externalTypes:
  - StepperItem[]
props:
  disabled: true
  items:
  - title: 'Address'
    description: 'Add your address here'
    icon: 'i-lucide-house'
  - title: 'Shipping'
    description: 'Set your preferred shipping method'
    icon: 'i-lucide-truck'
  - title: 'Checkout'
    description: 'Confirm your order'
---
::

::note{to="#with-controls"}
Điều này có thể hữu ích khi bạn muốn buộc điều hướng với controls.
::

## Examples

### With controls

Bạn có thể thêm các controls bổ sung cho stepper bằng buttons.

:component-example{name="stepper-with-controls-example"}

### Control active item

Bạn có thể kiểm soát mục active bằng cách sử dụng prop `default-value` hoặc directive `v-model` với index của mục.

:component-example{name="stepper-model-value-example"}

::tip
Bạn cũng có thể truyền `value` của một trong các mục nếu được cung cấp.
::

### With content slot

Sử dụng slot `#content` để tùy chỉnh nội dung của mỗi mục.

:component-example{name="stepper-content-slot-example"}

### With custom slot

Sử dụng thuộc tính `slot` để tùy chỉnh một mục cụ thể.

Bạn sẽ có quyền truy cập vào các slot sau:

- `#{{ item.slot }}`{lang="ts-type"}

:component-example{name="stepper-custom-slot-example"}

## API

### Props

:component-props

### Slots

:component-slots

### Emits

:component-emits

### Expose

Bạn có thể truy cập instance thành phần typed bằng cách sử dụng [`useTemplateRef`](https://vuejs.org/api/composition-api-helpers.html#usetemplateref).

```vue
<script setup lang="ts">
const stepper = useTemplateRef('stepper')
</script>

<template>
  <UStepper ref="stepper" />
</template>
```

Điều này sẽ cung cấp cho bạn quyền truy cập vào những thứ sau:

| Name | Type |
| ---- | ---- |
| `next`{lang="ts-type"} | `() => void`{lang="ts-type"} |
| `prev`{lang="ts-type"} | `() => void`{lang="ts-type"} |
| `hasNext`{lang="ts-type"} | `Ref<boolean>`{lang="ts-type"} |
| `hasPrev`{lang="ts-type"} | `Ref<boolean>`{lang="ts-type"} |

## Theme

:component-theme

## Changelog

:component-changelog