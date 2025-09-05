---
description: A popup that reveals information when hovering over an element.
category: overlay
links:
  - label: Tooltip
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/tooltip
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Tooltip.vue
---

## Usage

Sử dụng [Button](/components/button) hoặc bất kỳ thành phần nào khác trong slot mặc định của Tooltip.

::warning
Đảm bảo bao bọc ứng dụng của bạn với thành phần [`App`](/components/app) sử dụng thành phần [`TooltipProvider`](https://reka-ui.com/docs/components/tooltip#provider) từ Reka UI.
::

::tip{to="/components/app#props"}
Bạn có thể kiểm tra prop `tooltip` của thành phần `App` để xem cách cấu hình Tooltip toàn cầu.
::

### Text

Sử dụng prop `text` để đặt nội dung của Tooltip.

::component-code
---
prettier: true
props:
  text: 'Open on GitHub'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />
---

:u-button{label="Open" color="neutral" variant="subtle"}
::

### Kbds

Sử dụng prop `kbds` để hiển thị các thành phần [Kbd](/components/kbd) trong Tooltip.

::component-code
---
prettier: true
ignore:
  - text
  - kbds
props:
  text: 'Open on GitHub'
  kbds:
    - meta
    - G
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />
---

:u-button{label="Open" color="neutral" variant="subtle"}
::

::tip
Bạn có thể sử dụng các phím đặc biệt như `meta` hiển thị dưới dạng `⌘` trên macOS và `Ctrl` trên các nền tảng khác.
::

### Delay

Sử dụng prop `delay-duration` để thay đổi độ trễ trước khi Tooltip xuất hiện. Ví dụ, bạn có thể làm cho nó xuất hiện ngay lập tức bằng cách đặt thành `0`.

::component-code
---
prettier: true
ignore:
  - text
props:
  delayDuration: 0
  text: 'Open on GitHub'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />
---

:u-button{label="Open" color="neutral" variant="subtle"}
::

::tip
Điều này có thể được cấu hình toàn cầu thông qua tùy chọn `tooltip.delayDuration` trong thành phần [`App`](/components/app).
::

### Content

Sử dụng prop `content` để kiểm soát cách nội dung Tooltip được hiển thị, như `align` hoặc `side` chẳng hạn.

::component-code
---
prettier: true
ignore:
  - text
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
  text: 'Open on GitHub'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />
---

:u-button{label="Open" color="neutral" variant="subtle"}
::

### Arrow

Sử dụng prop `arrow` để hiển thị mũi tên trên Tooltip.

::component-code
---
prettier: true
ignore:
  - text
  - arrow
props:
  arrow: true
  text: 'Open on GitHub'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />
---

:u-button{label="Open" color="neutral" variant="subtle"}
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa Tooltip.

::component-code
---
prettier: true
ignore:
  - text
props:
  disabled: true
  text: 'Open on GitHub'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />
---

:u-button{label="Open" color="neutral" variant="subtle"}
::

## Examples

### Control open state

Bạn có thể kiểm soát trạng thái mở bằng cách sử dụng prop `default-open` hoặc directive `v-model:open`.

::component-example
---
name: 'tooltip-open-example'
---
::

::note
Trong ví dụ này, tận dụng [`defineShortcuts`](/composables/define-shortcuts), bạn có thể chuyển đổi Tooltip bằng cách nhấn :kbd{value="O"}.
::

### With following cursor :badge{label="New" class="align-text-top"}

Bạn có thể làm cho Tooltip theo dõi con trỏ khi di chuột qua một phần tử bằng cách sử dụng prop [`reference`](https://reka-ui.com/docs/components/tooltip#trigger):

::component-example
---
name: 'tooltip-cursor-example'
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
