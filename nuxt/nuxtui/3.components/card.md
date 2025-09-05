---
description: Hiển thị nội dung trong một thẻ với tiêu đề, thân và chân trang.
category: layout
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Card.vue
---

## Usage

::component-example
---
name: 'card-example'
props:
  class: 'w-full'
---
::

### Variant

Sử dụng prop `variant` để thay đổi biến thể của Card.

::component-code
---
prettier: true
hide:
  - class
props:
  variant: subtle
  class: 'w-full'
slots:
  header: |

    <Placeholder class="h-8" />

  default: |

    <Placeholder class="h-32" />

  footer: |

    <Placeholder class="h-8" />
---

#header
:placeholder{class="h-8"}

#default
:placeholder{class="h-32"}

#footer
:placeholder{class="h-8"}
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
