---
title: SelectMenu
description: Một phần tử select có thể tìm kiếm nâng cao.
category: form
links:
  - label: Combobox
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/combobox
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/SelectMenu.vue
---

## Usage

Sử dụng directive `v-model` để kiểm soát giá trị của SelectMenu hoặc prop `default-value` để đặt giá trị ban đầu khi bạn không cần kiểm soát trạng thái của nó.

::tip
Sử dụng điều này thay vì [`Select`](/components/select) để tận dụng thành phần [`Combobox`](https://reka-ui.com/docs/components/combobox) của Reka UI cung cấp khả năng tìm kiếm và lựa chọn nhiều.
::

::note
Thành phần này tương tự như [`InputMenu`](/components/input-menu) nhưng sử dụng Select thay vì Input với tìm kiếm bên trong menu.
::

### Items

Sử dụng prop `items` dưới dạng mảng các chuỗi, số hoặc boolean:

::component-code
---
prettier: true
ignore:
  - modelValue
  - items
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'Backlog'
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

Bạn cũng có thể truyền một mảng các đối tượng với các thuộc tính sau:

- `label?: string`{lang="ts-type"}
- [`type?: "label" | "separator" | "item"`{lang="ts-type"}](#with-items-type)
- [`icon?: string`{lang="ts-type"}](#with-icons-in-items)
- [`avatar?: AvatarProps`{lang="ts-type"}](#with-avatar-in-items)
- [`chip?: ChipProps`{lang="ts-type"}](#with-chip-in-items)
- `disabled?: boolean`{lang="ts-type"}
- `onSelect?(e: Event): void`{lang="ts-type"}
- `class?: any`{lang="ts-type"}
- `ui?: { label?: ClassNameValue, separator?: ClassNameValue, item?: ClassNameValue, itemLeadingIcon?: ClassNameValue, itemLeadingAvatarSize?: ClassNameValue, itemLeadingAvatar?: ClassNameValue, itemLeadingChipSize?: ClassNameValue, itemLeadingChip?: ClassNameValue, itemLabel?: ClassNameValue, itemTrailing?: ClassNameValue, itemTrailingIcon?: ClassNameValue }`{lang="ts-type"}

::component-code
---
ignore:
  - modelValue.label
  - items
  - class
external:
  - items
  - modelValue
props:
  modelValue:
    label: 'Todo'
  items:
    - label: 'Backlog'
    - label: 'Todo'
    - label: 'In Progress'
    - label: 'Done'
  class: 'w-48'
---
::

::caution
Không giống như thành phần [`Select`](/components/select), SelectMenu mong đợi toàn bộ đối tượng được truyền đến directive `v-model` hoặc prop `default-value` theo mặc định.
::

Bạn cũng có thể truyền một mảng các mảng để hiển thị các nhóm mục được phân tách.

::component-code
---
prettier: true
ignore:
  - modelValue
  - items
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'Apple'
  items:
    - - Apple
      - Banana
      - Blueberry
      - Grapes
      - Pineapple
    - - Aubergine
      - Broccoli
      - Carrot
      - Courgette
      - Leek
  class: 'w-48'
---
::

### Value Key

Bạn có thể chọn ràng buộc một thuộc tính duy nhất của đối tượng thay vì toàn bộ đối tượng bằng cách sử dụng prop `value-key`. Mặc định là `undefined`.

::component-code
---
collapse: true
ignore:
  - modelValue
  - valueKey
  - items
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'todo'
  valueKey: 'id'
  items:
    - label: 'Backlog'
      id: 'backlog'
    - label: 'Todo'
      id: 'todo'
    - label: 'In Progress'
      id: 'in_progress'
    - label: 'Done'
      id: 'done'
  class: 'w-48'
---
::

### Multiple

Sử dụng prop `multiple` để cho phép lựa chọn nhiều, các mục đã chọn sẽ được phân tách bằng dấu phẩy trong trigger.

::component-code
---
prettier: true
ignore:
  - modelValue
  - items
  - multiple
  - class
external:
  - items
  - modelValue
props:
  modelValue:
    - Backlog
    - Todo
  multiple: true
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

::caution
Đảm bảo truyền một mảng đến prop `default-value` hoặc directive `v-model`.
::

### Placeholder

Sử dụng prop `placeholder` để đặt văn bản placeholder.

::component-code
---
prettier: true
ignore:
  - items
  - class
external:
  - items
props:
  placeholder: 'Select status'
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

### Search Input

Sử dụng prop `search-input` để tùy chỉnh hoặc ẩn input tìm kiếm (với giá trị `false`).

Bạn có thể truyền bất kỳ thuộc tính nào từ thành phần [Input](/components/input) để tùy chỉnh nó.

::component-code
---
prettier: true
ignore:
  - modelValue.label
  - modelValue.icon
  - items
  - class
external:
  - items
  - modelValue
props:
  modelValue:
    label: 'Backlog'
    icon: 'i-lucide-circle-help'
  searchInput:
    placeholder: 'Filter...'
    icon: 'i-lucide-search'
  items:
    - label: Backlog
      icon: 'i-lucide-circle-help'
    - label: Todo
      icon: 'i-lucide-circle-plus'
    - label: In Progress
      icon: 'i-lucide-circle-arrow-up'
    - label: Done
      icon: 'i-lucide-circle-check'
  class: 'w-48'
---
::

::tip
Bạn có thể đặt prop `search-input` thành `false` để ẩn input tìm kiếm.
::

### Content

Sử dụng prop `content` để kiểm soát cách nội dung SelectMenu được hiển thị, như `align` hoặc `side` của nó.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
  - class
external:
  - items
  - modelValue
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
  modelValue: 'Backlog'
  content:
    align: center
    side: bottom
    sideOffset: 8
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

### Arrow

Sử dụng prop `arrow` để hiển thị mũi tên trên SelectMenu.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
  - class
  - arrow
external:
  - items
  - modelValue
props:
  modelValue: 'Backlog'
  arrow: true
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

### Color

Sử dụng prop `color` để thay đổi màu vòng khi SelectMenu được focus.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'Backlog'
  color: neutral
  highlight: true
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

::note
Prop `highlight` được sử dụng ở đây để hiển thị trạng thái focus. Nó được sử dụng nội bộ khi có lỗi xác thực.
::

### Variant

Sử dụng prop `variant` để thay đổi variant của SelectMenu.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'Backlog'
  color: neutral
  variant: subtle
  highlight: false
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của SelectMenu.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'Backlog'
  size: xl
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

### Icon

Sử dụng prop `icon` để hiển thị một [Icon](/components/icon) bên trong SelectMenu.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'Backlog'
  icon: 'i-lucide-search'
  size: md
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

### Trailing Icon

Sử dụng prop `trailing-icon` để tùy chỉnh [Icon](/components/icon) trailing. Mặc định là `i-lucide-chevron-down`.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'Backlog'
  trailingIcon: 'i-lucide-arrow-down'
  size: md
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.chevronDown`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.chevronDown`.
:::
::

### Selected Icon

Sử dụng prop `selected-icon` để tùy chỉnh icon khi một mục được chọn. Mặc định là `i-lucide-check`.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'Backlog'
  selectedIcon: 'i-lucide-flame'
  size: md
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.check`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.check`.
:::
::

### Avatar

Sử dụng prop `avatar` để hiển thị một [Avatar](/components/avatar) bên trong SelectMenu.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'Nuxt'
  avatar:
    src: 'https://github.com/nuxt.png'
  items:
    - Nuxt
    - NuxtHub
    - NuxtLabs
    - Nuxt Modules
    - Nuxt Community
  class: 'w-48'
---
::

### Loading

Sử dụng prop `loading` để hiển thị icon loading trên SelectMenu.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'Backlog'
  loading: true
  trailing: false
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

### Loading Icon

Sử dụng prop `loading-icon` để tùy chỉnh icon loading. Mặc định là `i-lucide-loader-circle`.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'Backlog'
  loading: true
  loadingIcon: 'i-lucide-loader'
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.loading`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.loading`.
:::
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa SelectMenu.

::component-code
---
prettier: true
ignore:
  - items
  - placeholder
  - class
external:
  - items
props:
  disabled: true
  placeholder: 'Select status'
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
  class: 'w-48'
---
::

## Examples

### With items type

Bạn có thể sử dụng thuộc tính `type` với `separator` để hiển thị một separator giữa các mục hoặc `label` để hiển thị một label.

::component-code
---
collapse: true
ignore:
  - modelValue
  - items
  - class
external:
  - items
  - modelValue
props:
  modelValue: 'Apple'
  items:
    - type: 'label'
      label: 'Fruits'
    - Apple
    - Banana
    - Blueberry
    - Grapes
    - Pineapple
    - type: 'separator'
    - type: 'label'
      label: 'Vegetables'
    - Aubergine
    - Broccoli
    - Carrot
    - Courgette
    - Leek
  class: 'w-48'
---
::

### With icon in items

Bạn có thể sử dụng thuộc tính `icon` để hiển thị một [Icon](/components/icon) bên trong các mục.

::component-example
---
collapse: true
name: 'select-menu-items-icon-example'
---
::

::tip
Bạn cũng có thể sử dụng slot `#leading` để hiển thị icon đã chọn.
::

### With avatar in items

Bạn có thể sử dụng thuộc tính `avatar` để hiển thị một [Avatar](/components/avatar) bên trong các mục.

::component-example
---
collapse: true
name: 'select-menu-items-avatar-example'
---
::

::tip
Bạn cũng có thể sử dụng slot `#leading` để hiển thị avatar đã chọn.
::

### With chip in items

Bạn có thể sử dụng thuộc tính `chip` để hiển thị một [Chip](/components/chip) bên trong các mục.

::component-example
---
collapse: true
name: 'select-menu-items-chip-example'
---
::

::note
Trong ví dụ này, slot `#leading` được sử dụng để hiển thị chip đã chọn.
::

### Control open state

Bạn có thể kiểm soát trạng thái mở bằng cách sử dụng prop `default-open` hoặc directive `v-model:open`.

::component-example
---
name: 'select-menu-open-example'
---
::

::note
Trong ví dụ này, tận dụng [`defineShortcuts`](/composables/define-shortcuts), bạn có thể chuyển đổi SelectMenu bằng cách nhấn :kbd{value="O"}.
::

### Control search term

Sử dụng directive `v-model:search-term` để kiểm soát từ khóa tìm kiếm.

::component-example
---
name: 'select-menu-search-term-example'
---
::

### With rotating icon

Đây là một ví dụ với icon xoay chỉ ra trạng thái mở của SelectMenu.

::component-example
---
name: 'select-menu-icon-example'
---
::

### With create item

Sử dụng prop `create-item` để cho phép người dùng thêm giá trị tùy chỉnh không có trong các tùy chọn được định sẵn.

::component-example
---
collapse: true
name: 'select-menu-create-item-example'
---
::

::note
Tùy chọn tạo hiển thị khi không tìm thấy kết quả phù hợp theo mặc định. Đặt nó thành `always` để hiển thị ngay cả khi có giá trị tương tự tồn tại.
::

::tip{to="#emits"}
Sử dụng sự kiện `@create` để xử lý việc tạo mục. Bạn sẽ nhận được sự kiện và mục dưới dạng đối số.
::

### With fetched items

Bạn có thể lấy các mục từ một API và sử dụng chúng trong SelectMenu.

::component-example
---
collapse: true
name: 'select-menu-fetch-example'
---
::

### With ignore filter

Đặt prop `ignore-filter` thành `true` để vô hiệu hóa tìm kiếm nội bộ và sử dụng logic tìm kiếm của riêng bạn.

::component-example
---
collapse: true
name: 'select-menu-ignore-filter-example'
---
::

::note
Ví dụ này sử dụng [`refDebounced`](https://vueuse.org/shared/refDebounced/#refdebounced) để debounce các cuộc gọi API.
::

### With filter fields

Sử dụng prop `filter-fields` với một mảng các trường để lọc trên. Mặc định là `[labelKey]`.

::component-example
---
collapse: true
name: 'select-menu-filter-fields-example'
---
::

### With full content width

Bạn có thể mở rộng nội dung đến chiều rộng đầy đủ của các mục của nó bằng cách sử dụng khóa `ui.content`.

::component-example
---
name: 'select-menu-content-width-example'
collapse: true
---
::

::tip
Bạn cũng có thể thay đổi chiều rộng nội dung toàn cục trong `app.config.ts` của bạn:

```
export default defineAppConfig({
  ui: {
    selectMenu: {
      slots: {
        content: 'min-w-fit'
      }
    }
  }
})
```
::

### As a CountryPicker

Ví dụ này minh họa việc sử dụng SelectMenu làm country picker với lazy loading - các quốc gia chỉ được lấy khi menu được mở.

::component-example
---
collapse: true
name: 'select-menu-countries-example'
---
::



## API

### Props

:component-props

### Slots

:component-slots

### Emits

:component-emits

### Expose

Khi truy cập thành phần qua template ref, bạn có thể sử dụng những thứ sau:

| Name | Type |
| ---- | ---- |
| `triggerRef`{lang="ts-type"} | `Ref<InstanceType<typeof ComboboxTrigger> \| null>`{lang="ts-type"} |

## Theme

:component-theme

## Changelog

:component-changelog