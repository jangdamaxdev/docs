---
title: DropdownMenu
description: A menu to display actions when clicking on an element.
category: overlay
links:
  - label: DropdownMenu
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/dropdown-menu
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/DropdownMenu.vue
---

## Usage

Sử dụng một [Button](/components/button) hoặc bất kỳ thành phần nào khác trong slot mặc định của DropdownMenu.

### Items

Sử dụng prop `items` dưới dạng một mảng các đối tượng với các thuộc tính sau:

- `label?: string`{lang="ts-type"}
- `icon?: string`{lang="ts-type"}
- `avatar?: AvatarProps`{lang="ts-type"}
- `kbds?: string[] | KbdProps[]`{lang="ts-type"}
- [`type?: "link" | "label" | "separator" | "checkbox"`{lang="ts-type"}](#with-checkbox-items)
- [`color?: "error" | "primary" | "secondary" | "success" | "info" | "warning" | "neutral"`{lang="ts-type"}](#with-color-items)
- [`checked?: boolean`{lang="ts-type"}](#with-checkbox-items)
- `disabled?: boolean`{lang="ts-type"}
- [`slot?: string`{lang="ts-type"}](#with-custom-slot)
- `onSelect?(e: Event): void`{lang="ts-type"}
- [`onUpdateChecked?(checked: boolean): void`{lang="ts-type"}](#with-checkbox-items)
- `children?: DropdownMenuItem[] | DropdownMenuItem[][]`{lang="ts-type"}
- `class?: any`{lang="ts-type"}
- `ui?: { item?: ClassNameValue, label?: ClassNameValue, separator?: ClassNameValue, itemLeadingIcon?: ClassNameValue, itemLeadingAvatarSize?: ClassNameValue, itemLeadingAvatar?: ClassNameValue, itemLabel?: ClassNameValue, itemLabelExternalIcon?: ClassNameValue, itemTrailing?: ClassNameValue, itemTrailingIcon?: ClassNameValue, itemTrailingKbds?: ClassNameValue, itemTrailingKbdsSize?: ClassNameValue }`{lang="ts-type"}

Bạn có thể truyền bất kỳ thuộc tính nào từ thành phần [Link](/components/link#props) như `to`, `target`, v.v.

::component-code
---
prettier: true
collapse: true
ignore:
  - items
  - ui.content
external:
  - items
externalTypes:
  - DropdownMenuItem[][]
props:
  items:
    - - label: Benjamin
        avatar:
          src: 'https://github.com/benjamincanac.png'
        type: label
    - - label: Profile
        icon: i-lucide-user
      - label: Billing
        icon: i-lucide-credit-card
      - label: Settings
        icon: i-lucide-cog
        kbds:
          - ','
      - label: Keyboard shortcuts
        icon: i-lucide-monitor
    - - label: Team
        icon: i-lucide-users
      - label: Invite users
        icon: i-lucide-user-plus
        children:
          - - label: Email
              icon: i-lucide-mail
            - label: Message
              icon: i-lucide-message-square
          - - label: More
              icon: i-lucide-circle-plus
      - label: New team
        icon: i-lucide-plus
        kbds:
          - meta
          - n
    - - label: GitHub
        icon: i-simple-icons-github
        to: 'https://github.com/nuxt/ui'
        target: _blank
      - label: Support
        icon: i-lucide-life-buoy
        to: '/components/dropdown-menu'
      - label: API
        icon: i-lucide-cloud
        disabled: true
    - - label: Logout
        icon: i-lucide-log-out
        kbds:
          - shift
          - meta
          - q
  ui:
    content: 'w-48'
slots:
  default: |

    <UButton icon="i-lucide-menu" color="neutral" variant="outline" />
---

:u-button{icon="i-lucide-menu" color="neutral" variant="outline"}
::

::note
Bạn cũng có thể truyền một mảng các mảng cho prop `items` để tạo các nhóm mục được tách biệt.
::

::tip
Mỗi mục có thể nhận một mảng `children` các đối tượng với các thuộc tính giống như prop `items` để tạo một menu lồng nhau có thể được kiểm soát bằng các thuộc tính `open`, `defaultOpen` và `content`.
::

### Content

Sử dụng prop `content` để kiểm soát cách nội dung DropdownMenu được render, như `align` hoặc `side` của nó ví dụ.

::component-code
---
prettier: true
ignore:
  - items
  - ui.content
external:
  - items
externalTypes:
  - DropdownMenuItem[]
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
  items:
    - label: Profile
      icon: i-lucide-user
    - label: Billing
      icon: i-lucide-credit-card
    - label: Settings
      icon: i-lucide-cog
  content:
    align: start
    side: bottom
    sideOffset: 8
  ui:
    content: 'w-48'
slots:
  default: |

    <UButton label="Open" icon="i-lucide-menu" color="neutral" variant="outline" />
---

:u-button{label="Open" icon="i-lucide-menu" color="neutral" variant="outline"}
::

### Arrow

Sử dụng prop `arrow` để hiển thị một mũi tên trên DropdownMenu.

::component-code
---
prettier: true
ignore:
  - arrow
  - items
  - ui.content
external:
  - items
externalTypes:
  - DropdownMenuItem[]
props:
  arrow: true
  items:
    - label: Profile
      icon: i-lucide-user
    - label: Billing
      icon: i-lucide-credit-card
    - label: Settings
      icon: i-lucide-cog
  ui:
    content: 'w-48'
slots:
  default: |

    <UButton label="Open" icon="i-lucide-menu" color="neutral" variant="outline" />
---

:u-button{label="Open" icon="i-lucide-menu" color="neutral" variant="outline"}
::

### Size

Sử dụng prop `size` để kiểm soát kích thước của DropdownMenu.

::component-code
---
prettier: true
ignore:
  - items
  - content.align
  - ui.content
external:
  - items
externalTypes:
  - DropdownMenuItem[]
props:
  size: xl
  items:
    - label: Profile
      icon: i-lucide-user
    - label: Billing
      icon: i-lucide-credit-card
    - label: Settings
      icon: i-lucide-cog
  content:
    align: start
  ui:
    content: 'w-48'
slots:
  default: |

    <UButton size="xl" label="Open" icon="i-lucide-menu" color="neutral" variant="outline" />
---

:u-button{size="xl" label="Open" icon="i-lucide-menu" color="neutral" variant="outline"}
::

::warning
Prop `size` sẽ không được ủy quyền cho Button, bạn cần đặt nó tự mình.
::

::note
Khi sử dụng cùng kích thước, các mục DropdownMenu sẽ được căn chỉnh hoàn hảo với Button.
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa DropdownMenu.

::component-code
---
prettier: true
ignore:
  - items
  - ui.content
external:
  - items
externalTypes:
  - DropdownMenuItem[]
props:
  disabled: true
  items:
    - label: Profile
      icon: i-lucide-user
    - label: Billing
      icon: i-lucide-credit-card
    - label: Settings
      icon: i-lucide-cog
  ui:
    content: 'w-48'
slots:
  default: |

    <UButton label="Open" icon="i-lucide-menu" color="neutral" variant="outline" />
---

:u-button{label="Open" icon="i-lucide-menu" color="neutral" variant="outline"}
::

## Examples

### With checkbox items

Bạn có thể sử dụng thuộc tính `type` với `checkbox` và sử dụng các thuộc tính `checked` / `onUpdateChecked` để kiểm soát trạng thái đã kiểm tra của mục.

::component-example
---
collapse: true
name: 'dropdown-menu-checkbox-items-example'
---
::

::note
Để đảm bảo tính phản ứng cho trạng thái `checked` của các mục, nên bọc mảng `items` của bạn bên trong một `computed`.
::

### With color items

Bạn có thể sử dụng thuộc tính `color` để làm nổi bật một số mục với một màu sắc.

::component-example
---
name: 'dropdown-menu-color-items-example'
---
::

### Control open state

Bạn có thể kiểm soát trạng thái mở bằng cách sử dụng prop `default-open` hoặc directive `v-model:open`.

::component-example
---
name: 'dropdown-menu-open-example'
---
::

::note
Trong ví dụ này, tận dụng [`defineShortcuts`](/composables/define-shortcuts), bạn có thể chuyển đổi DropdownMenu bằng cách nhấn :kbd{value="O"}.
::

### With custom slot

Sử dụng thuộc tính `slot` để tùy chỉnh một mục cụ thể.

Bạn sẽ có quyền truy cập vào các slot sau:

- `#{{ item.slot }}`{lang="ts-type"}
- `#{{ item.slot }}-leading`{lang="ts-type"}
- `#{{ item.slot }}-label`{lang="ts-type"}
- `#{{ item.slot }}-trailing`{lang="ts-type"}

::component-example
---
name: 'dropdown-menu-custom-slot-example'
---
::

::tip{to="#slots"}
Bạn cũng có thể sử dụng các slot `#item`, `#item-leading`, `#item-label` và `#item-trailing` để tùy chỉnh tất cả các mục.
::

### Extract shortcuts

Khi bạn có một số mục với thuộc tính `kbds` (hiển thị một số [Kbd](/components/kbd)), bạn có thể dễ dàng làm cho chúng hoạt động với composable [defineShortcuts](/composables/define-shortcuts).

Bên trong composable `defineShortcuts`, có một tiện ích `extractShortcuts` sẽ trích xuất các phím tắt một cách đệ quy từ các mục và trả về một đối tượng mà bạn có thể truyền cho `defineShortcuts`. Nó sẽ tự động gọi hàm `select` của mục khi phím tắt được nhấn.

```vue
<script setup lang="ts">
import type { DropdownMenuItem } from '@nuxt/ui'

const items: DropdownMenuItem[] = [{
  label: 'Invite users',
  icon: 'i-lucide-user-plus',
  children: [{
    label: 'Invite by email',
    icon: 'i-lucide-send-horizontal',
    kbds: ['meta', 'e'],
    onSelect() {
      console.log('Invite by email clicked')
    }
  }, {
    label: 'Invite by link',
    icon: 'i-lucide-link',
    kbds: ['meta', 'i'],
    onSelect() {
      console.log('Invite by link clicked')
    }
  }]
}, {
  label: 'New team',
  icon: 'i-lucide-plus',
  kbds: ['meta', 'n'],
  onSelect() {
    console.log('New team clicked')
  }
}]

defineShortcuts(extractShortcuts(items))
</script>
```

::note
Trong ví dụ này, :kbd{value="meta"} :kbd{value="E"}, :kbd{value="meta"} :kbd{value="I"} và :kbd{value="meta"} :kbd{value="N"} sẽ kích hoạt hàm `select` của mục tương ứng.
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
