---
title: ButtonGroup
description: Nhóm nhiều phần tử giống nút lại với nhau.
category: element
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/ButtonGroup.vue
---

## Usage

Bao bọc nhiều [Button](/components/button) trong một ButtonGroup để nhóm chúng lại.

::component-code
---
prettier: true
slots:
  default: |

    <UButton color="neutral" variant="subtle" label="Button" />
    <UButton color="neutral" variant="outline" icon="i-lucide-chevron-down" />
---
:u-button{color="neutral" variant="subtle" label="Button"}
:u-button{color="neutral" variant="outline" icon="i-lucide-chevron-down"}
::

### Size

Sử dụng prop `size` để thay đổi kích thước của tất cả các nút.

::component-code
---
prettier: true
props:
  size: xl
slots:
  default: |

    <UButton color="neutral" variant="subtle" label="Button" />
    <UButton color="neutral" variant="outline" icon="i-lucide-chevron-down" />
---
:u-button{color="neutral" variant="subtle" label="Button"}
:u-button{color="neutral" variant="outline" icon="i-lucide-chevron-down"}
::

### Orientation

Sử dụng prop `orientation` để thay đổi hướng của các nút. Mặc định là `horizontal`.

::component-code
---
prettier: true
props:
  orientation: vertical
slots:
  default: |

    <UButton color="neutral" variant="subtle" label="Submit" />
    <UButton color="neutral" variant="outline" label="Cancel" />
---
:u-button{color="neutral" variant="subtle" label="Submit"}
:u-button{color="neutral" variant="outline" label="Cancel"}
::

## Examples

### With input

Bạn có thể sử dụng các thành phần như [Input](/components/input), [InputMenu](/components/input-menu), [Select](/components/select) [SelectMenu](/components/select-menu), v.v. trong một nhóm nút.

::component-code
---
prettier: true
slots:
  default: |

    <UInput color="neutral" variant="outline" placeholder="Enter token" />

    <UButton color="neutral" variant="subtle" icon="i-lucide-clipboard" />
---
:u-input{color="neutral" variant="outline" placeholder="Enter token"}
:u-button{color="neutral" variant="subtle" icon="i-lucide-clipboard"}
::

### With tooltip

Bạn có thể sử dụng một [Tooltip](/components/tooltip) trong một nhóm nút.

:component-example{name="button-group-tooltip-example"}

### With dropdown

Bạn có thể sử dụng một [DropdownMenu](/components/dropdown-menu) trong một nhóm nút.

:component-example{name="button-group-dropdown-example"}

### With badge

Bạn có thể sử dụng một [Badge](/components/badge) trong một nhóm nút.

:component-example{name="button-group-badge-example"}

## API

### Props

:component-props

### Slots

:component-slots

## Theme

:component-theme

## Changelog

:component-changelog
