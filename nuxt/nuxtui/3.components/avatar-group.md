---
title: AvatarGroup
description: Xếp chồng nhiều avatar trong một nhóm.
category: element
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/AvatarGroup.vue
---

## Usage

Bao bọc nhiều [Avatar](/components/avatar) trong một AvatarGroup để xếp chồng chúng.

::component-code
---
prettier: true
slots:
  default: |

    <UAvatar src="https://github.com/benjamincanac.png" alt="Benjamin Canac" />
    <UAvatar src="https://github.com/romhml.png" alt="Romain Hamel" />
    <UAvatar src="https://github.com/noook.png" alt="Neil Richter" />
---
:u-avatar{src="https://github.com/benjamincanac.png" alt="Benjamin Canac"}
:u-avatar{src="https://github.com/romhml.png" alt="Romain Hamel"}
:u-avatar{src="https://github.com/noook.png" alt="Neil Richter"}
::

### Size

Sử dụng prop `size` để thay đổi kích thước của tất cả các avatar.

::component-code
---
prettier: true
props:
  size: xl
slots:
  default: |

    <UAvatar src="https://github.com/benjamincanac.png" alt="Benjamin Canac" />
    <UAvatar src="https://github.com/romhml.png" alt="Romain Hamel" />
    <UAvatar src="https://github.com/noook.png" alt="Neil Richter" />
---
:u-avatar{src="https://github.com/benjamincanac.png" alt="Benjamin Canac"}
:u-avatar{src="https://github.com/romhml.png" alt="Romain Hamel"}
:u-avatar{src="https://github.com/noook.png" alt="Neil Richter"}
::

### Max

Sử dụng prop `max` để giới hạn số lượng avatar được hiển thị. Phần còn lại được hiển thị dưới dạng avatar `+X`.

::component-code
---
prettier: true
props:
  max: 2
slots:
  default: |

    <UAvatar src="https://github.com/benjamincanac.png" alt="Benjamin Canac" />
    <UAvatar src="https://github.com/romhml.png" alt="Romain Hamel" />
    <UAvatar src="https://github.com/noook.png" alt="Neil Richter" />
---
:u-avatar{src="https://github.com/benjamincanac.png" alt="Benjamin Canac"}
:u-avatar{src="https://github.com/romhml.png" alt="Romain Hamel"}
:u-avatar{src="https://github.com/noook.png" alt="Neil Richter"}
::

## Examples

### With tooltip

Bao bọc mỗi avatar với một [Tooltip](/components/tooltip) để hiển thị chú giải khi di chuột.

:component-example{name="avatar-group-tooltip-example"}

### With chip

Bao bọc mỗi avatar với một [Chip](/components/chip) để hiển thị chip xung quanh avatar.

:component-example{name="avatar-group-chip-example"}

### With link

Bao bọc mỗi avatar với một [Link](/components/link) để làm cho chúng có thể nhấp.

:component-example{name="avatar-group-link-example"}

## API

### Props

:component-props

### Slots

:component-slots

## Theme

:component-theme

## Changelog

:component-changelog
