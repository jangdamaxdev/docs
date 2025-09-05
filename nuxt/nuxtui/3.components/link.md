---
description: Một wrapper xung quanh <NuxtLink> với các prop bổ sung.
category: navigation
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Link.vue
---

## Usage

Link component là một wrapper xung quanh [`<NuxtLink>`](https://nuxt.com/docs/api/components/nuxt-link) sử dụng prop [`custom`](https://router.vuejs.org/api/interfaces/RouterLinkProps.html#Properties-custom). Nó cung cấp một số prop bổ sung:

- `inactive-class` prop để đặt một class khi link không hoạt động, `active-class` được sử dụng khi hoạt động.
- `exact` prop để style với `active-class` khi link hoạt động và route giống hệt với route hiện tại.
- `exact-query` và `exact-hash` props để style với `active-class` khi link hoạt động và query hoặc hash giống hệt với query hoặc hash hiện tại.
  - sử dụng `exact-query="partial"` để style với `active-class` khi link hoạt động và query khớp một phần với query hiện tại.

Lý do đằng sau là cung cấp cùng API như NuxtLink trở lại trong Nuxt 2 / Vue 2. Bạn có thể đọc thêm về nó trong hướng dẫn migration từ Vue 2 của Vue Router [migration from Vue 2](https://router.vuejs.org/guide/migration/#removal-of-the-exact-prop-in-router-link).

::note
Nó được sử dụng bởi các component [`Breadcrumb`](/components/breadcrumb), [`Button`](/components/button), [`ContextMenu`](/components/context-menu), [`DropdownMenu`](/components/dropdown-menu) và [`NavigationMenu`](/components/navigation-menu).
::

### Tag

Component Link hiển thị thẻ `<a>` khi prop `to` được cung cấp, nếu không thì hiển thị thẻ `<button>`. Bạn có thể sử dụng prop `as` để thay đổi thẻ fallback.

::component-code
---
props:
  to: ''
  as: 'button'
slots:
  default: Link
---
::

::note
Bạn có thể kiểm tra HTML được hiển thị bằng cách thay đổi prop `to`.
::

### Style

Theo mặc định, link có style active và inactive mặc định, kiểm tra phần [#theme](#theme).

::component-code
---
props:
  to: /components/link
slots:
  default: Link
---
::

::note
Thử thay đổi prop `to` để xem các trạng thái active và inactive.
::

Bạn có thể override hành vi này bằng cách sử dụng prop `raw` và cung cấp style riêng của bạn sử dụng `class`, `active-class` và `inactive-class`.

::component-code
---
ignore:
  - raw
props:
  raw: true
  to: /components/link
  activeClass: 'font-bold'
  inactiveClass: 'text-muted'
slots:
  default: Link
---

Link
::

## IntelliSense

Nếu bạn đang sử dụng VSCode và muốn có autocompletion cho các class `active-class` và `inactive-class`, bạn có thể thêm cài đặt sau vào `.vscode/settings.json`:

```json [.vscode/settings.json]
{
  "tailwindCSS.classAttributes": [
    "active-class",
    "inactive-class"
  ]
}
```

## API

### Props

::component-props
---
ignore:
  - custom
---
::

### Slots

:component-slots

## Theme

:component-theme

## Changelog

:component-changelog
