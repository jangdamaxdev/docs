---
title: ContextMenu
description: Một menu để hiển thị các hành động khi nhấp chuột phải vào một phần tử.
category: overlay
links:
  - label: ContextMenu
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/context-menu
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/ContextMenu.vue
---

## Usage

Sử dụng bất kỳ thứ gì bạn thích trong slot mặc định của ContextMenu, và nhấp chuột phải vào nó để hiển thị menu.

### Items

Sử dụng prop `items` dưới dạng mảng các đối tượng với các thuộc tính sau:

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
- `children?: ContextMenuItem[] | ContextMenuItem[][]`{lang="ts-type"}
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
  - ContextMenuItem[][]
props:
  items:
    - - label: Appearance
        children:
          - label: System
            icon: i-lucide-monitor
          - label: Light
            icon: i-lucide-sun
          - label: Dark
            icon: i-lucide-moon
    - - label: Show Sidebar
        kbds:
          - meta
          - s
      - label: Show Toolbar
        kbds:
          - shift
          - meta
          - d
      - label: Collapse Pinned Tabs
        disabled: true
    - - label: Refresh the Page
      - label: Clear Cookies and Refresh
      - label: Clear Cache and Refresh
      - type: separator
      - label: Developer
        children:
          - - label: View Source
              kbds:
                - meta
                - shift
                - u
            - label: Developer Tools
              kbds:
                - option
                - meta
                - i
            - label: Inspect Elements
              kbds:
                - option
                - meta
                - c
          - - label: JavaScript Console
              kbds:
                - option
                - meta
                - j
  ui:
    content: 'w-48'
slots:
  default: |

    <div class="flex items-center justify-center rounded-md border border-dashed border-accented text-sm aspect-video w-72">
      Right click here
    </div>
---

:div{class="flex items-center justify-center rounded-md border border-dashed border-accented text-sm aspect-video w-72"}[Right click here]
::

::note
Bạn cũng có thể truyền một mảng các mảng cho prop `items` để tạo các nhóm mục được tách biệt.
::

::tip
Mỗi mục có thể lấy mảng `children` các đối tượng với các thuộc tính giống như prop `items` để tạo menu lồng nhau có thể được kiểm soát bằng cách sử dụng các thuộc tính `open`, `defaultOpen` và `content`.
::

### Size

Sử dụng prop `size` để thay đổi kích thước của ContextMenu.

::component-code
---
prettier: true
ignore:
  - items
  - ui.content
external:
  - items
externalTypes:
  - ContextMenuItem[]
props:
  size: xl
  items:
    - label: System
      icon: i-lucide-monitor
    - label: Light
      icon: i-lucide-sun
    - label: Dark
      icon: i-lucide-moon
  ui:
    content: 'w-48'
slots:
  default: |

    <div class="flex items-center justify-center rounded-md border border-dashed border-accented text-sm aspect-video w-72">
      Right click here
    </div>
---

:div{class="flex items-center justify-center rounded-md border border-dashed border-accented text-sm aspect-video w-72"}[Right click here]
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa ContextMenu.

::component-code
---
prettier: true
ignore:
  - items
  - ui.content
external:
  - items
externalTypes:
  - ContextMenuItem[]
props:
  disabled: true
  items:
    - label: System
      icon: i-lucide-monitor
    - label: Light
      icon: i-lucide-sun
    - label: Dark
      icon: i-lucide-moon
  ui:
    content: 'w-48'
slots:
  default: |

    <div class="flex items-center justify-center rounded-md border border-dashed border-accented text-sm aspect-video w-72">
      Right click here
    </div>
---

:div{class="flex items-center justify-center rounded-md border border-dashed border-accented text-sm aspect-video w-72"}[Right click here]
::

## Examples

### With checkbox items

Bạn có thể sử dụng thuộc tính `type` với `checkbox` và sử dụng các thuộc tính `checked` / `onUpdateChecked` để kiểm soát trạng thái đã kiểm tra của mục.

::component-example
---
collapse: true
name: 'context-menu-checkbox-items-example'
---
::

::note
Để đảm bảo tính phản ứng cho trạng thái `checked` của các mục, bạn nên bao bọc mảng `items` của bạn bên trong một `computed`.
::

### With color items

Bạn có thể sử dụng thuộc tính `color` để làm nổi bật một số mục với màu sắc.

::component-example
---
name: 'context-menu-color-items-example'
---
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
name: 'context-menu-custom-slot-example'
---
::

::tip{to="#slots"}
Bạn cũng có thể sử dụng các slot `#item`, `#item-leading`, `#item-label` và `#item-trailing` để tùy chỉnh tất cả các mục.
::

### Extract shortcuts

Khi bạn có một số mục với thuộc tính `kbds` (hiển thị một số [Kbd](/components/kbd)), bạn có thể dễ dàng làm cho chúng hoạt động với composable [defineShortcuts](/composables/define-shortcuts).

Bên trong composable `defineShortcuts`, có một tiện ích `extractShortcuts` sẽ trích xuất các phím tắt đệ quy từ các mục và trả về một đối tượng mà bạn có thể truyền cho `defineShortcuts`. Nó sẽ tự động gọi hàm `select` của mục khi phím tắt được nhấn.

```vue
<script setup lang="ts">
const items = [
  [{
    label: 'Show Sidebar',
    kbds: ['meta', 'S'],
    onSelect() {
      console.log('Show Sidebar clicked')
    }
  }, {
    label: 'Show Toolbar',
    kbds: ['shift', 'meta', 'D'],
    onSelect() {
      console.log('Show Toolbar clicked')
    }
  }, {
    label: 'Collapse Pinned Tabs',
    disabled: true
  }], [{
    label: 'Refresh the Page'
  }, {
    label: 'Clear Cookies and Refresh'
  }, {
    label: 'Clear Cache and Refresh'
  }, {
    type: 'separator' as const
  }, {
    label: 'Developer',
    children: [[{
      label: 'View Source',
      kbds: ['option', 'meta', 'U'],
      onSelect() {
        console.log('View Source clicked')
      }
    }, {
      label: 'Developer Tools',
      kbds: ['option', 'meta', 'I'],
      onSelect() {
        console.log('Developer Tools clicked')
      }
    }], [{
      label: 'Inspect Elements',
      kbds: ['option', 'meta', 'C'],
      onSelect() {
        console.log('Inspect Elements clicked')
      }
    }], [{
      label: 'JavaScript Console',
      kbds: ['option', 'meta', 'J'],
      onSelect() {
        console.log('JavaScript Console clicked')
      }
    }]]
  }]
]

defineShortcuts(extractShortcuts(items))
</script>
```

::note
Trong ví dụ này, :kbd{value="meta"} :kbd{value="S"}, :kbd{value="shift"} :kbd{value="meta"} :kbd{value="D"}, :kbd{value="option"} :kbd{value="meta"} :kbd{value="U"}, :kbd{value="option"} :kbd{value="meta"} :kbd{value="I"}, :kbd{value="option"} :kbd{value="meta"} :kbd{value="C"} và :kbd{value="option"} :kbd{value="meta"} :kbd{value="J"} sẽ kích hoạt hàm `select` của mục tương ứng.
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
