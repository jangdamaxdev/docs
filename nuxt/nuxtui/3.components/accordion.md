---
description: Một tập hợp các bảng có thể thu gọn xếp chồng.
category: data
links:
  - label: Accordion
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/accordion
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Accordion.vue
---

## Usage

### Items

Sử dụng prop `items` dưới dạng một mảng các đối tượng với các thuộc tính sau:

- `label?: string`{lang="ts-type"}
- `icon?: string`{lang="ts-type"}
- `trailingIcon?: string`{lang="ts-type"}
- `content?: string`{lang="ts-type"}
- `value?: string`{lang="ts-type"}
- `disabled?: boolean`{lang="ts-type"}
- [`slot?: string`{lang="ts-type"}](#with-custom-slot)
- `class?: any`{lang="ts-type"}
- `ui?: { item?: ClassNameValue, header?: ClassNameValue, trigger?: ClassNameValue, leadingIcon?: ClassNameValue, label?: ClassNameValue, trailingIcon?: ClassNameValue, content?: ClassNameValue, body?: ClassNameValue }`{lang="ts-type"}

::component-code
---
ignore:
  - items
external:
  - items
externalTypes:
  - AccordionItem[]
hide:
  - class
props:
  class: 'px-4'
  items:
    - label: 'Icons'
      icon: 'i-lucide-smile'
      content: 'You have nothing to do, @nuxt/icon will handle it automatically.'
    - label: 'Colors'
      icon: 'i-lucide-swatch-book'
      content: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
    - label: 'Components'
      icon: 'i-lucide-box'
      content: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
---
::

### Multiple

Đặt prop `type` thành `multiple` để cho phép nhiều mục hoạt động cùng lúc. Mặc định là `single`.

::component-code
---
ignore:
  - type
  - items
external:
  - items
externalTypes:
  - AccordionItem[]
hide:
  - class
props:
  class: 'px-4'
  type: 'multiple'
  items:
    - label: 'Icons'
      icon: 'i-lucide-smile'
      content: 'You have nothing to do, @nuxt/icon will handle it automatically.'
    - label: 'Colors'
      icon: 'i-lucide-swatch-book'
      content: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
    - label: 'Components'
      icon: 'i-lucide-box'
      content: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
---
::

### Collapsible

Khi `type` là `single`, bạn có thể đặt prop `collapsible` thành `false` để ngăn mục hoạt động thu gọn.

::component-code
---
ignore:
  - collapsible
  - items
external:
  - items
externalTypes:
  - AccordionItem[]
hide:
  - class
props:
  class: 'px-4'
  collapsible: false
  items:
    - label: 'Icons'
      icon: 'i-lucide-smile'
      content: 'You have nothing to do, @nuxt/icon will handle it automatically.'
    - label: 'Colors'
      icon: 'i-lucide-swatch-book'
      content: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
    - label: 'Components'
      icon: 'i-lucide-box'
      content: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
---
::

### Unmount

Sử dụng prop `unmount-on-hide` để ngăn nội dung bị gỡ bỏ khi accordion bị thu gọn. Mặc định là `true`.

::component-code
---
ignore:
  - items
external:
  - items
externalTypes:
  - AccordionItem[]
hide:
  - class
props:
  class: 'px-4'
  unmountOnHide: false
  items:
    - label: 'Icons'
      icon: 'i-lucide-smile'
      content: 'You have nothing to do, @nuxt/icon will handle it automatically.'
    - label: 'Colors'
      icon: 'i-lucide-swatch-book'
      content: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
    - label: 'Components'
      icon: 'i-lucide-box'
      content: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
---
::

::note
Bạn có thể kiểm tra DOM để xem nội dung của mỗi mục đang được hiển thị.
::

### Disabled

Sử dụng thuộc tính `disabled` để vô hiệu hóa Accordion.

Bạn cũng có thể vô hiệu hóa một mục cụ thể bằng cách sử dụng thuộc tính `disabled` trong đối tượng mục.

::component-code
---
ignore:
  - items
external:
  - items
externalTypes:
  - AccordionItem[]
hide:
  - class
props:
  class: 'px-4'
  disabled: true
  items:
    - label: 'Icons'
      icon: 'i-lucide-smile'
      content: 'You have nothing to do, @nuxt/icon will handle it automatically.'
    - label: 'Colors'
      icon: 'i-lucide-swatch-book'
      content: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
      disabled: true
    - label: 'Components'
      icon: 'i-lucide-box'
      content: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
---
::

### Trailing Icon

Sử dụng prop `trailing-icon` để tùy chỉnh [Icon](/components/icon) theo sau của mỗi mục. Mặc định là `i-lucide-chevron-down`.

::tip
Bạn cũng có thể đặt biểu tượng cho một mục cụ thể bằng cách sử dụng thuộc tính `trailingIcon` trong đối tượng mục.
::

::component-code
---
ignore:
  - items
external:
  - items
externalTypes:
  - AccordionItem[]
hide:
  - class
props:
  class: 'px-4'
  trailingIcon: 'i-lucide-arrow-down'
  items:
    - label: 'Icons'
      icon: 'i-lucide-smile'
      content: 'You have nothing to do, @nuxt/icon will handle it automatically.'
      trailingIcon: 'i-lucide-plus'
    - label: 'Colors'
      icon: 'i-lucide-swatch-book'
      content: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
    - label: 'Components'
      icon: 'i-lucide-box'
      content: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` dưới khóa `ui.icons.chevronDown`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` dưới khóa `ui.icons.chevronDown`.
:::
::

## Examples

### Control active item(s)

Bạn có thể kiểm soát mục hoạt động bằng cách sử dụng prop `default-value` hoặc chỉ thị `v-model` với chỉ số của mục.

::component-example
---
name: 'accordion-model-value-example'
props:
  class: 'px-4'
---
::

::tip
Bạn cũng có thể truyền `value` của một trong các mục nếu được cung cấp.
::

::caution
Khi `type="multiple"`, đảm bảo truyền một mảng cho prop `default-value` hoặc chỉ thị `v-model`.
::

### With drag and drop

Sử dụng composable [`useSortable`](https://vueuse.org/integrations/useSortable/) từ [`@vueuse/integrations`](https://vueuse.org/integrations/README.html) để bật chức năng kéo và thả trên Accordion. Tích hợp này bao bọc [Sortable.js](https://sortablejs.github.io/Sortable/) để cung cấp trải nghiệm kéo và thả liền mạch.

::component-example
---
name: 'accordion-drag-and-drop-example'
---
::

### With body slot

Sử dụng slot `#body` để tùy chỉnh thân của mỗi mục.

::component-example
---
name: 'accordion-body-slot-example'
props:
  class: 'px-4'
---
::

::tip
Slot `#body` bao gồm một số kiểu được định nghĩa trước, sử dụng slot [`#content`](#with-content-slot) nếu bạn muốn bắt đầu từ đầu.
::

### With content slot

Sử dụng slot `#content` để tùy chỉnh nội dung của mỗi mục.

::component-example
---
name: 'accordion-content-slot-example'
props:
  class: 'px-4'
---
::

### With custom slot

Sử dụng thuộc tính `slot` để tùy chỉnh một mục cụ thể.

Bạn sẽ có quyền truy cập vào các slot sau:

- `#{{ item.slot }}`{lang="ts-type"}
- `#{{ item.slot }}-body`{lang="ts-type"}

::component-example
---
name: 'accordion-custom-slot-example'
props:
  class: 'px-4'
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
