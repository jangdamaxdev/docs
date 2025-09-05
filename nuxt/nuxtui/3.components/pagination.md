---
description: Một danh sách các buttons hoặc links để navigate qua các pages.
category: navigation
links:
  - label: Pagination
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/pagination
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Pagination.vue
---

## Usage

Sử dụng prop `default-page` hoặc directive `v-model:page` để kiểm soát page hiện tại.

::note
Component Pagination sử dụng một số [Button](/components/button) để hiển thị các pages, sử dụng props [`color`](#color), [`variant`](#variant) và [`size`](#size) để style chúng.
::

### Total

Sử dụng prop `total` để đặt tổng số items trong list.

::component-code
---
external:
  - page
model:
  - page
props:
  page: 5
  total: 100
---
::

### Items Per Page

Sử dụng prop `items-per-page` để đặt số items per page. Mặc định là `10`.

::component-code
---
ignore:
  - page
external:
  - page
model:
  - page
props:
  page: 5
  itemsPerPage: 20
  total: 100
---
::

### Sibling Count

Sử dụng prop `sibling-count` để đặt số siblings để show. Mặc định là `2`.

::component-code
---
ignore:
  - page
  - total
external:
  - page
model:
  - page
props:
  page: 5
  siblingCount: 1
  total: 100
---
::

### Show Edges

Sử dụng prop `show-edges` để luôn show ellipsis, first và last pages. Mặc định là `false`.

::component-code
---
ignore:
  - page
  - total
external:
  - page
model:
  - page
props:
  page: 5
  showEdges: true
  siblingCount: 1
  total: 100
---
::

### Show Controls

Sử dụng prop `show-controls` để show các buttons first, prev, next và last. Mặc định là `true`.

::component-code
---
ignore:
  - page
  - total
external:
  - page
model:
  - page
props:
  page: 5
  showControls: false
  showEdges: true
  total: 100
---
::

### Color

Sử dụng prop `color` để đặt màu của inactive controls. Mặc định là `neutral`.

::component-code
---
ignore:
  - page
  - total
external:
  - page
model:
  - page
items:
  color:
    - primary
    - secondary
    - success
    - info
    - warning
    - error
    - neutral
props:
  page: 5
  color: primary
  total: 100
---
::

### Variant

Sử dụng prop `variant` để đặt variant của inactive controls. Mặc định là `outline`.

::component-code
---
ignore:
  - page
  - total
external:
  - page
model:
  - page
items:
  color:
    - primary
    - secondary
    - success
    - info
    - warning
    - error
    - neutral
  variant:
    - solid
    - outline
    - soft
    - subtle
    - ghost
    - link
props:
  page: 5
  color: neutral
  variant: subtle
  total: 100
---
::

### Active Color

Sử dụng prop `active-color` để đặt màu của active control. Mặc định là `primary`.

::component-code
---
ignore:
  - page
  - total
external:
  - page
model:
  - page
items:
  activeColor:
    - primary
    - secondary
    - success
    - info
    - warning
    - error
    - neutral
props:
  page: 5
  activeColor: neutral
  total: 100
---
::

### Active Variant

Sử dụng prop `active-variant` để đặt variant của active control. Mặc định là `solid`.

::component-code
---
ignore:
  - page
  - total
external:
  - page
model:
  - page
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
  page: 5
  activeColor: primary
  activeVariant: subtle
  total: 100
---
::

### Size

Sử dụng prop `size` để đặt size của controls. Mặc định là `md`.

::component-code
---
ignore:
  - page
  - total
external:
  - page
model:
  - page
items:
  size:
    - xs
    - sm
    - md
    - lg
    - xl
props:
  page: 5
  size: xl
  total: 100
---
::

### Disabled

Sử dụng prop `disabled` để disable pagination controls.

::component-code
---
ignore:
  - page
  - total
external:
  - page
model:
  - page
props:
  page: 5
  total: 100
  disabled: true
---
::

## Examples

### With links

Sử dụng prop `to` để transform buttons thành links. Truyền một function nhận page number và trả về destination route.

::component-example
---
name: 'pagination-links-example'
---
::

::note
Trong ví dụ này chúng tôi thêm hash `#with-links` để tránh đi đến top của page.
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