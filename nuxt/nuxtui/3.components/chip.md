---
description: Một chỉ báo của giá trị số hoặc trạng thái.
category: element
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Chip.vue
---

## Usage

Bao bọc bất kỳ thành phần nào với Chip để hiển thị chỉ báo.

::component-code
---
prettier: true
slots:
  default: |

    <UButton icon="i-lucide-mail" color="neutral" variant="subtle" />
---
:u-button{icon="i-lucide-mail" color="neutral" variant="subtle"}
::

### Color

Sử dụng prop `color` để thay đổi màu sắc của Chip.

::component-code
---
prettier: true
props:
  color: neutral
slots:
  default: |

    <UButton icon="i-lucide-mail" color="neutral" variant="subtle" />
---
:u-button{icon="i-lucide-mail" color="neutral" variant="subtle"}
::

### Size

Sử dụng prop `size` để thay đổi kích thước của Chip.

::component-code
---
prettier: true
props:
  size: 3xl
slots:
  default: |

    <UButton icon="i-lucide-mail" color="neutral" variant="subtle" />
---
:u-button{icon="i-lucide-mail" color="neutral" variant="subtle"}
::

### Text

Sử dụng prop `text` để đặt văn bản của Chip.

::component-code
---
prettier: true
props:
  text: 5
  size: 3xl
slots:
  default: |

    <UButton icon="i-lucide-mail" color="neutral" variant="subtle" />
---
:u-button{icon="i-lucide-mail" color="neutral" variant="subtle"}
::

### Position

Sử dụng prop `position` để thay đổi vị trí của Chip.

::component-code
---
prettier: true
props:
  position: 'bottom-left'
slots:
  default: |

    <UButton icon="i-lucide-mail" color="neutral" variant="subtle" />
---
:u-button{icon="i-lucide-mail" color="neutral" variant="subtle"}
::

### Inset

Sử dụng prop `inset` để hiển thị Chip bên trong thành phần. Điều này hữu ích khi xử lý các thành phần bo tròn.

::component-code
---
prettier: true
props:
  inset: true
slots:
  default: |

    <UAvatar src="https://github.com/benjamincanac.png" />
---
:u-avatar{src="https://github.com/benjamincanac.png"}
::

### Standalone

Sử dụng prop `standalone` cùng với prop `inset` để hiển thị Chip nội tuyến.

::component-code
---
props:
  standalone: true
  inset: true
---
::

::note
Nó được sử dụng theo cách này trong các thành phần [`CommandPalette`](/components/command-palette), [`InputMenu`](/components/input-menu), [`Select`](/components/select) hoặc [`SelectMenu`](/components/select-menu) chẳng hạn.
::

## Examples

### Control visibility

Bạn có thể kiểm soát khả năng hiển thị của Chip bằng cách sử dụng prop `show`.

:component-example{name="chip-show-example"}

::note
Trong ví dụ này, Chip có màu cho mỗi trạng thái và được hiển thị khi trạng thái không phải là `offline`.
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
