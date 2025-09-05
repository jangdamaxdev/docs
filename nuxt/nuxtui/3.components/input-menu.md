---
title: InputMenu
description: An autocomplete input with real-time suggestions.
category: form
links:
  - label: Combobox
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/combobox
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/InputMenu.vue
---

## Usage

Sử dụng directive `v-model` để kiểm soát giá trị của InputMenu hoặc prop `default-value` để đặt giá trị ban đầu khi bạn không cần kiểm soát trạng thái của nó.

::tip
Sử dụng điều này thay cho [`Input`](/components/input) để tận dụng thành phần [`Combobox`](https://reka-ui.com/docs/components/combobox) của Reka UI cung cấp khả năng tự động hoàn thành.
::

::note
Thành phần này tương tự như [`SelectMenu`](/components/select-menu) nhưng nó sử dụng Input thay vì Select.
::

### Items

Sử dụng prop `items` dưới dạng một mảng các chuỗi, số hoặc boolean:

::component-code
---
prettier: true
ignore:
  - modelValue
  - items
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
- `ui?: { tagsItem?: ClassNameValue, tagsItemText?: ClassNameValue, tagsItemDelete?: ClassNameValue, tagsItemDeleteIcon?: ClassNameValue, label?: ClassNameValue, separator?: ClassNameValue, item?: ClassNameValue, itemLeadingIcon?: ClassNameValue, itemLeadingAvatarSize?: ClassNameValue, itemLeadingAvatar?: ClassNameValue, itemLeadingChip?: ClassNameValue, itemLeadingChipSize?: ClassNameValue, itemLabel?: ClassNameValue, itemTrailing?: ClassNameValue, itemTrailingIcon?: ClassNameValue }`{lang="ts-type"}

::component-code
---
ignore:
  - modelValue.label
  - items
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
---
::

Bạn cũng có thể truyền một mảng các mảng cho prop `items` để hiển thị các nhóm mục được tách biệt.

::component-code
---
prettier: true
ignore:
  - modelValue
  - items
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
---
::

### Multiple

Sử dụng prop `multiple` để cho phép chọn nhiều mục, các mục đã chọn sẽ được hiển thị dưới dạng thẻ.

::component-code
---
prettier: true
ignore:
  - modelValue
  - items
  - multiple
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
---
::

::caution
Đảm bảo truyền một mảng cho prop `default-value` hoặc directive `v-model`.
::

### Delete Icon

Với `multiple`, sử dụng prop `delete-icon` để tùy chỉnh [Icon](/components/icon) xóa trong các thẻ. Mặc định là `i-lucide-x`.

::component-code
---
prettier: true
ignore:
  - modelValue
  - items
  - multiple
external:
  - items
  - modelValue
props:
  modelValue:
    - Backlog
    - Todo
  multiple: true
  deleteIcon: 'i-lucide-trash'
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.close`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.close`.
:::
::

### Placeholder

Sử dụng prop `placeholder` để đặt văn bản placeholder.

::component-code
---
prettier: true
ignore:
  - items
external:
  - items
props:
  placeholder: 'Select status'
  items:
    - Backlog
    - Todo
    - In Progress
    - Done
---
::

### Content

Sử dụng prop `content` để kiểm soát cách nội dung InputMenu được render, như `align` hoặc `side` của nó ví dụ.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
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
---
::

### Arrow

Sử dụng prop `arrow` để hiển thị một mũi tên trên InputMenu.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
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
---
::

### Color

Sử dụng prop `color` để thay đổi màu vòng khi InputMenu được focus.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
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
---
::

::note
Prop `highlight` được sử dụng ở đây để hiển thị trạng thái focus. Nó được sử dụng nội bộ khi xảy ra lỗi xác thực.
::

### Variant

Sử dụng prop `variant` để thay đổi biến thể của InputMenu.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
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
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của InputMenu.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
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
---
::

### Icon

Sử dụng prop `icon` để hiển thị một [Icon](/components/icon) bên trong InputMenu.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
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
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.chevronDown`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.chevronDown`.
:::
::

### Selected Icon

Sử dụng prop `selected-icon` để tùy chỉnh biểu tượng khi một mục được chọn. Mặc định là `i-lucide-check`.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
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
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.check`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.check`.
:::
::

### Avatar

Sử dụng prop `avatar` để hiển thị một [Avatar](/components/avatar) bên trong InputMenu.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
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
---
::

### Loading

Sử dụng prop `loading` để hiển thị biểu tượng loading trên InputMenu.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
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
---
::

### Loading Icon

Sử dụng prop `loading-icon` để tùy chỉnh biểu tượng loading. Mặc định là `i-lucide-loader-circle`.

::component-code
---
prettier: true
ignore:
  - items
  - modelValue
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
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.loading`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.loading`.
:::
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa InputMenu.

::component-code
---
prettier: true
ignore:
  - items
  - placeholder
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
---
::

## Examples

### With items type

Bạn có thể sử dụng thuộc tính `type` với `separator` để hiển thị một dấu phân cách giữa các mục hoặc `label` để hiển thị một nhãn.

::component-code
---
collapse: true
ignore:
  - modelValue
  - items
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
---
::

### With icon in items

Bạn có thể sử dụng thuộc tính `icon` để hiển thị một [Icon](/components/icon) bên trong các mục.

::component-example
---
collapse: true
name: 'input-menu-items-icon-example'
---
::

::tip
Bạn cũng có thể sử dụng slot `#leading` để hiển thị biểu tượng đã chọn.
::

### With avatar in items

Bạn có thể sử dụng thuộc tính `avatar` để hiển thị một [Avatar](/components/avatar) bên trong các mục.

::component-example
---
collapse: true
name: 'input-menu-items-avatar-example'
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
name: 'input-menu-items-chip-example'
---
::

::note
Trong ví dụ này, slot `#leading` được sử dụng để hiển thị chip đã chọn.
::

### Control open state

Bạn có thể kiểm soát trạng thái mở bằng cách sử dụng prop `default-open` hoặc directive `v-model:open`.

::component-example
---
name: 'input-menu-open-example'
---
::

::note
Trong ví dụ này, tận dụng [`defineShortcuts`](/composables/define-shortcuts), bạn có thể chuyển đổi InputMenu bằng cách nhấn :kbd{value="O"}.
::

### Control open state on focus

Bạn có thể sử dụng prop `open-on-focus` hoặc `open-on-click` để mở menu khi input được focus hoặc nhấp.

::component-example
---
name: 'input-menu-open-focus-example'
---
::

### Control search term

Sử dụng directive `v-model:search-term` để kiểm soát thuật ngữ tìm kiếm.

::component-example
---
name: 'input-menu-search-term-example'
---
::

### With rotating icon

Đây là một ví dụ với biểu tượng xoay chỉ ra trạng thái mở của InputMenu.

::component-example
---
name: 'input-menu-icon-example'
---
::

### With create item

Sử dụng prop `create-item` để cho phép người dùng thêm các giá trị tùy chỉnh không có trong các tùy chọn định sẵn.

::component-example
---
collapse: true
name: 'input-menu-create-item-example'
---
::

::note
Tùy chọn tạo hiển thị khi không tìm thấy khớp theo mặc định. Đặt thành `always` để hiển thị ngay cả khi có giá trị tương tự tồn tại.
::

::tip{to="#emits"}
Sử dụng sự kiện `@create` để xử lý việc tạo mục. Bạn sẽ nhận được sự kiện và mục dưới dạng đối số.
::

### With fetched items

Bạn có thể lấy các mục từ API và sử dụng chúng trong InputMenu.

::component-example
---
collapse: true
name: 'input-menu-fetch-example'
---
::

### With ignore filter

Đặt prop `ignore-filter` thành `true` để vô hiệu hóa tìm kiếm nội bộ và sử dụng logic tìm kiếm của riêng bạn.

::component-example
---
collapse: true
name: 'input-menu-ignore-filter-example'
---
::

::note
Ví dụ này sử dụng [`refDebounced`](https://vueuse.org/shared/refDebounced/#refdebounced) để debounce các cuộc gọi API.
::

### With filter fields

Sử dụng prop `filter-fields` với một mảng các trường để lọc. Mặc định là `[labelKey]`.

::component-example
---
collapse: true
name: 'input-menu-filter-fields-example'
---
::

### With full content width

Bạn có thể mở rộng nội dung đến chiều rộng đầy đủ của các mục của nó bằng cách sử dụng khóa `ui.content`.

::component-example
---
name: 'input-menu-content-width-example'
collapse: true
---
::

::tip
Bạn cũng có thể thay đổi chiều rộng nội dung toàn cục trong `app.config.ts` của bạn:

```
export default defineAppConfig({
  ui: {
    inputMenu: {
      slots: {
        content: 'min-w-fit'
      }
    }
  }
})
```
::

### As a CountryPicker

Ví dụ này minh họa việc sử dụng InputMenu làm bộ chọn quốc gia với lazy loading - các quốc gia chỉ được lấy khi menu được mở.

::component-example
---
collapse: true
name: 'input-menu-countries-example'
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

When accessing the component via a template ref, you can use the following:

| Name | Type |
| ---- | ---- |
| `inputRef`{lang="ts-type"} | `Ref<InstanceType<typeof ComboboxTrigger> \| null>`{lang="ts-type"} |

## Theme

:component-theme

## Changelog

:component-changelog
