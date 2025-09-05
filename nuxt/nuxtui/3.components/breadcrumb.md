---
description: Một hệ thống phân cấp các liên kết để điều hướng qua trang web.
category: navigation
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Breadcrumb.vue
---

## Usage

### Items

Sử dụng prop `items` dưới dạng một mảng các đối tượng với các thuộc tính sau:

- `label?: string`{lang="ts-type"}
- `icon?: string`{lang="ts-type"}
- `avatar?: AvatarProps`{lang="ts-type"}
- [`slot?: string`{lang="ts-type"}](#with-custom-slot)
- `class?: any`{lang="ts-type"}
- `ui?: { item?: ClassNameValue, link?: ClassNameValue, linkLeadingIcon?: ClassNameValue, linkLeadingAvatar?: ClassNameValue, linkLabel?: ClassNameValue, separator?: ClassNameValue, separatorIcon?: ClassNameValue }`{lang="ts-type"}

Bạn có thể truyền bất kỳ thuộc tính nào từ thành phần [Link](/components/link#props) như `to`, `target`, v.v.

::component-code
---
ignore:
  - items
external:
  - items
externalTypes:
  - BreadcrumbItem[]
props:
  items:
    - label: 'Home'
      icon: 'i-lucide-house'
    - label: 'Components'
      icon: 'i-lucide-box'
      to: '/components'
    - label: 'Breadcrumb'
      icon: 'i-lucide-link'
      to: '/components/breadcrumb'
---
::

::note
Một `span` được hiển thị thay vì liên kết khi thuộc tính `to` không được định nghĩa.
::

### Separator Icon

Sử dụng prop `separator-icon` để tùy chỉnh [Icon](/components/icon) giữa mỗi mục. Mặc định là `i-lucide-chevron-right`.

::component-code
---
ignore:
  - items
external:
  - items
externalTypes:
  - BreadcrumbItem[]
props:
  separatorIcon: 'i-lucide-arrow-right'
  items:
    - label: 'Home'
      icon: 'i-lucide-house'
    - label: 'Components'
      icon: 'i-lucide-box'
      to: '/components'
    - label: 'Breadcrumb'
      icon: 'i-lucide-link'
      to: '/components/breadcrumb'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` dưới khóa `ui.icons.chevronRight`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` dưới khóa `ui.icons.chevronRight`.
:::
::

## Examples

### With separator slot

Sử dụng slot `#separator` để tùy chỉnh dấu phân cách giữa mỗi mục.

:component-example{name="breadcrumb-separator-slot-example"}

### With custom slot

Sử dụng thuộc tính `slot` để tùy chỉnh một mục cụ thể.

Bạn sẽ có quyền truy cập vào các slot sau:

- `#{{ item.slot }}`{lang="ts-type"}
- `#{{ item.slot }}-leading`{lang="ts-type"}
- `#{{ item.slot }}-label`{lang="ts-type"}
- `#{{ item.slot }}-trailing`{lang="ts-type"}

:component-example{name="breadcrumb-custom-slot-example"}

::tip{to="#slots"}
Bạn cũng có thể sử dụng slot `#item`, `#item-leading`, `#item-label` và `#item-trailing` để tùy chỉnh tất cả các mục.
::

## API

### Props

:component-props

### Slots

:component-slots

## Theme

:component-theme

## Changelog

:component-changelog
