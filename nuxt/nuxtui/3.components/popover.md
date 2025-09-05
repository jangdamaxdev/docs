---
description: Một non-modal dialog that floats xung quanh a trigger element.
category: overlay
links:
  - label: HoverCard
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/hover-card
  - label: Popover
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/popover
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Popover.vue
---

## Usage

Sử dụng một [Button](/components/button) hoặc bất kỳ component nào khác trong slot mặc định của Popover.

Sau đó, sử dụng slot `#content` để thêm content được hiển thị khi Popover mở.

::component-code
---
prettier: true
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  content: |

    <Placeholder class="size-48 m-4 inline-flex" />
---
::

:u-button{label="Open" color="neutral" variant="subtle"}

#content
:placeholder{class="size-48 m-4 inline-flex"}
::

### Mode

Sử dụng prop `mode` để thay đổi mode của Popover. Mặc định là `click`.

::component-code
---
prettier: true
items:
  mode:
    - click
    - hover
props:
  mode: 'hover'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  content: |

    <Placeholder class="size-48 m-4 inline-flex" />
---
::

:u-button{label="Open" color="neutral" variant="subtle"}

#content
:placeholder{class="size-48 m-4 inline-flex"}
::

::note
Khi sử dụng `hover` mode, Reka UI [`HoverCard`](https://reka-ui.com/docs/components/hover-card) component được sử dụng thay vì [`Popover`](https://reka-ui.com/docs/components/popover).
::

### Delay

Khi sử dụng `hover` mode, bạn có thể sử dụng props `open-delay` và `close-delay` để kiểm soát delay trước khi Popover được mở hoặc đóng.

::component-code
---
prettier: true
ignore:
  - mode
props:
  mode: 'hover'
  openDelay: 500
  closeDelay: 300
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  content: |

    <Placeholder class="size-48 m-4 inline-flex" />
---
::

:u-button{label="Open" color="neutral" variant="subtle"}

#content
:placeholder{class="size-48 m-4 inline-flex"}
::

### Content

Sử dụng prop `content` để kiểm soát cách Popover content được render, như `align` hoặc `side` của nó ví dụ.

::component-code
---
prettier: true
items:
  content.align:
    - start
    - center
    - end
  content.side:
    - right
    - left
    - top
    - bottom
props:
  content:
    align: center
    side: bottom
    sideOffset: 8
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  content: |

    <Placeholder class="size-48 m-4 inline-flex" />
---
::

:u-button{label="Open" color="neutral" variant="subtle"}

#content
:placeholder{class="size-48 m-4 inline-flex"}
::

### Arrow

Sử dụng prop `arrow` để hiển thị một arrow trên Popover.

::component-code
---
prettier: true
ignore:
  - arrow
props:
  arrow: true
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  content: |

    <Placeholder class="size-48 m-4 inline-flex" />
---
::

:u-button{label="Open" color="neutral" variant="subtle"}

#content
:placeholder{class="size-48 m-4 inline-flex"}
::

## Examples

### Control open state

Bạn có thể kiểm soát open state bằng cách sử dụng prop `default-open` hoặc directive `v-model:open`.

::component-example
---
name: 'popover-open-example'
---
::

::note
Trong ví dụ này, tận dụng [`defineShortcuts`](/composables/define-shortcuts), bạn có thể toggle Popover bằng cách nhấn :kbd{value="O"}.
::

### Disable dismissal

Đặt prop `dismissible` thành `false` để ngăn Popover bị đóng khi click bên ngoài hoặc nhấn escape. Sự kiện `close:prevent` sẽ được emit khi người dùng cố gắng đóng nó.

::component-example
---
name: 'popover-dismissible-example'
---
::

### With command palette

Bạn có thể sử dụng component [CommandPalette](/components/command-palette) bên trong content của Popover.

::component-example
---
collapse: true
name: 'popover-command-palette-example'
---
::

### With following cursor :badge{label="New" class="align-text-top"}

Bạn có thể làm cho Popover follow cursor khi hovering over một element bằng cách sử dụng prop [`reference`](https://reka-ui.com/docs/components/tooltip#trigger):

::component-example
---
name: 'popover-cursor-example'
---
::

### With anchor slot

Bạn có thể sử dụng slot `#anchor` để position Popover against một custom element.

::warning
Slot này chỉ hoạt động khi `mode` là `click`.
::

::component-example
---
collapse: true
name: 'popover-anchor-slot-example'
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