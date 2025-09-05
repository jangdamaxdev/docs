---
title: CommandPalette
description: Một bảng lệnh với tìm kiếm toàn văn được cung cấp bởi Fuse.js để khớp mờ hiệu quả.
category: navigation
links:
  - label: Fuse.js
    icon: i-custom-fuse-js
    to: https://fusejs.io/
    target: _blank
  - label: Listbox
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/listbox
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/CommandPalette.vue
---

## Usage

Sử dụng chỉ thị `v-model` để kiểm soát giá trị của CommandPalette hoặc prop `default-value` để đặt giá trị ban đầu khi bạn không cần kiểm soát trạng thái của nó.

::tip{to="#control-selected-items"}
Bạn cũng có thể sử dụng sự kiện `@update:model-value` để lắng nghe mục đã chọn.
::

### Groups

Thành phần CommandPalette lọc các nhóm và xếp hạng các lệnh khớp theo mức độ liên quan khi người dùng nhập. Nó cung cấp kết quả tìm kiếm động, tức thì để khám phá lệnh hiệu quả. Sử dụng prop `groups` dưới dạng mảng các đối tượng với các thuộc tính sau:

- `id: string`{lang="ts-type"}
- `label?: string`{lang="ts-type"}
- `slot?: string`{lang="ts-type"}
- `items?: CommandPaletteItem[]`{lang="ts-type"}
- [`ignoreFilter?: boolean`{lang="ts-type"}](#with-ignore-filter)
- [`postFilter?: (searchTerm: string, items: T[]) => T[]`{lang="ts-type"}](#with-post-filtered-items)
- `highlightedIcon?: string`{lang="ts-type"}

::caution
Bạn phải cung cấp `id` cho mỗi nhóm nếu không nhóm sẽ bị bỏ qua.
::

Mỗi nhóm chứa mảng `items` các đối tượng định nghĩa các lệnh. Mỗi mục có thể có các thuộc tính sau:

- `prefix?: string`{lang="ts-type"}
- `label?: string`{lang="ts-type"}
- `suffix?: string`{lang="ts-type"}
- `icon?: string`{lang="ts-type"}
- `avatar?: AvatarProps`{lang="ts-type"}
- `chip?: ChipProps`{lang="ts-type"}
- `kbds?: string[] | KbdProps[]`{lang="ts-type"}
- `active?: boolean`{lang="ts-type"}
- `loading?: boolean`{lang="ts-type"}
- `disabled?: boolean`{lang="ts-type"}
- [`slot?: string`{lang="ts-type"}](#with-custom-slot)
- `placeholder?: string`{lang="ts-type"}
- `children?: CommandPaletteItem[]`{lang="ts-type"}
- `onSelect?(e?: Event): void`{lang="ts-type"}
- `class?: any`{lang="ts-type"}
- `ui?: { item?: ClassNameValue, itemLeadingIcon?: ClassNameValue, itemLeadingAvatarSize?: ClassNameValue, itemLeadingAvatar?: ClassNameValue, itemLeadingChipSize?: ClassNameValue, itemLeadingChip?: ClassNameValue, itemLabel?: ClassNameValue, itemLabelPrefix?: ClassNameValue, itemLabelBase?: ClassNameValue, itemLabelSuffix?: ClassNameValue, itemTrailing?: ClassNameValue, itemTrailingKbds?: ClassNameValue, itemTrailingKbdsSize?: ClassNameValue, itemTrailingHighlightedIcon?: ClassNameValue, itemTrailingIcon?: ClassNameValue }`{lang="ts-type"}

Bạn có thể truyền bất kỳ thuộc tính nào từ thành phần [Link](/components/link#props) như `to`, `target`, v.v.

::component-code
---
collapse: true
hide:
  - autofocus
ignore:
  - groups
  - modelValue
  - class
external:
  - groups
  - modelValue
class: '!p-0'
props:
  modelValue: {}
  autofocus: false
  groups:
    - id: 'users'
      label: 'Users'
      items:
        - label: 'Benjamin Canac'
          suffix: 'benjamincanac'
          avatar:
            src: 'https://github.com/benjamincanac.png'
        - label: 'Sylvain Marroufin'
          suffix: 'smarroufin'
          avatar:
            src: 'https://github.com/smarroufin.png'
        - label: 'Sébastien Chopin'
          suffix: 'atinux'
          avatar:
            src: 'https://github.com/atinux.png'
        - label: 'Romain Hamel'
          suffix: 'romhml'
          avatar:
            src: 'https://github.com/romhml.png'
        - label: 'Haytham A. Salama'
          suffix: 'Haythamasalama'
          avatar:
            src: 'https://github.com/Haythamasalama.png'
        - label: 'Daniel Roe'
          suffix: 'danielroe'
          avatar:
            src: 'https://github.com/danielroe.png'
        - label: 'Neil Richter'
          suffix: 'noook'
          avatar:
            src: 'https://github.com/noook.png'
  class: 'flex-1'
---
::

::tip{to="#with-children-in-items"}
Mỗi mục có thể lấy mảng `children` các đối tượng với các thuộc tính sau để tạo menu con:
::

### Multiple

Sử dụng prop `multiple` để cho phép nhiều lựa chọn.

::component-code
---
collapse: true
hide:
  - autofocus
ignore:
  - groups
  - modelValue
  - multiple
  - class
external:
  - groups
  - modelValue
class: '!p-0'
props:
  multiple: true
  autofocus: false
  modelValue: []
  groups:
    - id: 'users'
      label: 'Users'
      items:
        - label: 'Benjamin Canac'
          suffix: 'benjamincanac'
          avatar:
            src: 'https://github.com/benjamincanac.png'
        - label: 'Sylvain Marroufin'
          suffix: 'smarroufin'
          avatar:
            src: 'https://github.com/smarroufin.png'
        - label: 'Sébastien Chopin'
          suffix: 'atinux'
          avatar:
            src: 'https://github.com/atinux.png'
        - label: 'Romain Hamel'
          suffix: 'romhml'
          avatar:
            src: 'https://github.com/romhml.png'
        - label: 'Haytham A. Salama'
          suffix: 'Haythamasalama'
          avatar:
            src: 'https://github.com/Haythamasalama.png'
        - label: 'Daniel Roe'
          suffix: 'danielroe'
          avatar:
            src: 'https://github.com/danielroe.png'
        - label: 'Neil Richter'
          suffix: 'noook'
          avatar:
            src: 'https://github.com/noook.png'
  class: 'flex-1'
---
::

::caution
Đảm bảo truyền một mảng cho prop `default-value` hoặc chỉ thị `v-model`.
::

### Placeholder

Sử dụng prop `placeholder` để thay đổi văn bản placeholder.

::component-code
---
collapse: true
hide:
  - autofocus
ignore:
  - class
  - groups
external:
  - groups
class: '!p-0'
props:
  autofocus: false
  placeholder: 'Search an app...'
  groups:
    - id: 'apps'
      items:
        - label: 'Calendar'
          icon: 'i-lucide-calendar'
        - label: 'Music'
          icon: 'i-lucide-music'
        - label: 'Maps'
          icon: 'i-lucide-map'
  class: 'flex-1'
---
::

### Icon

Sử dụng prop `icon` để tùy chỉnh [Icon](/components/icon) đầu vào. Mặc định là `i-lucide-search`.

::component-code
---
collapse: true
hide:
  - autofocus
ignore:
  - class
  - groups
external:
  - groups
class: '!p-0'
props:
  autofocus: false
  icon: 'i-lucide-box'
  groups:
    - id: 'apps'
      items:
        - label: 'Calendar'
          icon: 'i-lucide-calendar'
        - label: 'Music'
          icon: 'i-lucide-music'
        - label: 'Maps'
          icon: 'i-lucide-map'
  class: 'flex-1'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.search`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.search`.
:::
::

### Selected Icon

Sử dụng prop `selected-icon` để tùy chỉnh [Icon](/components/icon) mục đã chọn. Mặc định là `i-lucide-check`.

::component-code
---
collapse: true
hide:
  - autofocus
ignore:
  - groups
  - modelValue
  - multiple
  - class
external:
  - groups
  - modelValue
class: '!p-0'
props:
  multiple: true
  autofocus: false
  modelValue:
    - label: 'Benjamin Canac'
      suffix: 'benjamincanac'
      avatar:
        src: 'https://github.com/benjamincanac.png'
  selectedIcon: 'i-lucide-circle-check'
  groups:
    - id: 'users'
      label: 'Users'
      items:
        - label: 'Benjamin Canac'
          suffix: 'benjamincanac'
          avatar:
            src: 'https://github.com/benjamincanac.png'
        - label: 'Sylvain Marroufin'
          suffix: 'smarroufin'
          avatar:
            src: 'https://github.com/smarroufin.png'
        - label: 'Sébastien Chopin'
          suffix: 'atinux'
          avatar:
            src: 'https://github.com/atinux.png'
        - label: 'Romain Hamel'
          suffix: 'romhml'
          avatar:
            src: 'https://github.com/romhml.png'
        - label: 'Haytham A. Salama'
          suffix: 'Haythamasalama'
          avatar:
            src: 'https://github.com/Haythamasalama.png'
        - label: 'Daniel Roe'
          suffix: 'danielroe'
          avatar:
            src: 'https://github.com/danielroe.png'
        - label: 'Neil Richter'
          suffix: 'noook'
          avatar:
            src: 'https://github.com/noook.png'
  class: 'flex-1'
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

### Trailing Icon

Sử dụng prop `trailing-icon` để tùy chỉnh [Icon](/components/icon) theo sau khi một mục có con. Mặc định là `i-lucide-chevron-right`.

::component-code
---
collapse: true
prettier: true
hide:
  - autofocus
ignore:
  - groups
  - class
external:
  - groups
class: '!p-0'
props:
  autofocus: false
  trailingIcon: 'i-lucide-arrow-right'
  groups:
    - id: 'actions'
      items:
        - label: 'Share'
          icon: 'i-lucide-share'
          children:
            - label: 'Email'
              icon: 'i-lucide-mail'
            - label: 'Copy'
              icon: 'i-lucide-copy'
            - label: 'Link'
              icon: 'i-lucide-link'
  class: 'flex-1'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.chevronRight`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.chevronRight`.
:::
::

### Loading

Sử dụng prop `loading` để hiển thị biểu tượng tải trên CommandPalette.

::component-code
---
collapse: true
hide:
  - autofocus
ignore:
  - class
  - groups
external:
  - groups
class: '!p-0'
props:
  autofocus: false
  loading: true
  groups:
    - id: 'apps'
      items:
        - label: 'Calendar'
          icon: 'i-lucide-calendar'
        - label: 'Music'
          icon: 'i-lucide-music'
        - label: 'Maps'
          icon: 'i-lucide-map'
  class: 'flex-1'
---
::

### Loading Icon

Sử dụng prop `loading-icon` để tùy chỉnh biểu tượng tải. Mặc định là `i-lucide-loader-circle`.

::component-code
---
collapse: true
hide:
  - autofocus
ignore:
  - class
  - groups
external:
  - groups
class: '!p-0'
props:
  autofocus: false
  loading: true
  loadingIcon: 'i-lucide-loader'
  groups:
    - id: 'apps'
      items:
        - label: 'Calendar'
          icon: 'i-lucide-calendar'
        - label: 'Music'
          icon: 'i-lucide-music'
        - label: 'Maps'
          icon: 'i-lucide-map'
  class: 'flex-1'
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

### Close

Sử dụng prop `close` để hiển thị [Button](/components/button) để đóng CommandPalette.

::tip
Sự kiện `update:open` sẽ được phát ra khi nút đóng được nhấp.
::

::component-code
---
collapse: true
hide:
  - autofocus
ignore:
  - class
  - groups
  - close
external:
  - groups
class: '!p-0'
props:
  autofocus: false
  close: true
  groups:
    - id: 'apps'
      items:
        - label: 'Calendar'
          icon: 'i-lucide-calendar'
        - label: 'Music'
          icon: 'i-lucide-music'
        - label: 'Maps'
          icon: 'i-lucide-map'
  class: 'flex-1'
---
::

Bạn có thể truyền bất kỳ thuộc tính nào từ thành phần [Button](/components/button) để tùy chỉnh nó.

::component-code
---
collapse: true
prettier: true
hide:
  - autofocus
ignore:
  - close.color
  - close.variant
  - groups
  - class
external:
  - groups
class: '!p-0'
props:
  autofocus: false
  close:
    color: primary
    variant: outline
    class: 'rounded-full'
  groups:
    - id: 'apps'
      items:
        - label: 'Calendar'
          icon: 'i-lucide-calendar'
        - label: 'Music'
          icon: 'i-lucide-music'
        - label: 'Maps'
          icon: 'i-lucide-map'
  class: 'flex-1'
---
::

### Close Icon

Sử dụng prop `close-icon` để tùy chỉnh [Icon](/components/icon) nút đóng. Mặc định là `i-lucide-x`.

::component-code
---
collapse: true
hide:
  - autofocus
ignore:
  - class
  - groups
  - close
external:
  - groups
class: '!p-0'
props:
  autofocus: false
  close: true
  closeIcon: 'i-lucide-arrow-right'
  groups:
    - id: 'apps'
      items:
        - label: 'Calendar'
          icon: 'i-lucide-calendar'
        - label: 'Music'
          icon: 'i-lucide-music'
        - label: 'Maps'
          icon: 'i-lucide-map'
  class: 'flex-1'
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

### Back

Sử dụng prop `back` để tùy chỉnh hoặc ẩn nút quay lại (với giá trị `false`) được hiển thị khi điều hướng vào menu con.

Bạn có thể truyền bất kỳ thuộc tính nào từ thành phần [Button](/components/button) để tùy chỉnh nó.

::component-code
---
collapse: true
prettier: true
hide:
  - autofocus
ignore:
  - back.color
  - groups
  - class
external:
  - groups
class: '!p-0'
props:
  autofocus: false
  back:
    color: primary
  groups:
    - id: 'actions'
      items:
        - label: 'Share'
          icon: 'i-lucide-share'
          children:
            - label: 'Email'
              icon: 'i-lucide-mail'
            - label: 'Copy'
              icon: 'i-lucide-copy'
            - label: 'Link'
              icon: 'i-lucide-link'
  class: 'flex-1'
---
::

### Back Icon

Sử dụng prop `back-icon` để tùy chỉnh [Icon](/components/icon) nút quay lại. Mặc định là `i-lucide-arrow-left`.

::component-code
---
collapse: true
hide:
  - autofocus
ignore:
  - class
  - groups
  - back
external:
  - groups
class: '!p-0'
props:
  autofocus: false
  back: true
  backIcon: 'i-lucide-house'
  groups:
    - id: 'actions'
      items:
        - label: 'Share'
          icon: 'i-lucide-share'
          children:
            - label: 'Email'
              icon: 'i-lucide-mail'
            - label: 'Copy'
              icon: 'i-lucide-copy'
            - label: 'Link'
              icon: 'i-lucide-link'
  class: 'flex-1'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.arrowLeft`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh biểu tượng này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.arrowLeft`.
:::
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa CommandPalette.

::component-code
---
collapse: true
hide:
  - autofocus
ignore:
  - groups
  - class
external:
  - groups
class: '!p-0'
props:
  autofocus: false
  disabled: true
  groups:
    - id: 'apps'
      items:
        - label: 'Calendar'
          icon: 'i-lucide-calendar'
        - label: 'Music'
          icon: 'i-lucide-music'
        - label: 'Maps'
          icon: 'i-lucide-map'
  class: 'flex-1'
---
::

## Examples

### Control selected item(s)

Bạn có thể kiểm soát mục đã chọn bằng cách sử dụng prop `default-value` hoặc chỉ thị `v-model`, bằng cách sử dụng trường `onSelect` trên mỗi mục hoặc bằng cách sử dụng sự kiện `@update:model-value`.

::component-example
---
collapse: true
name: 'command-palette-select-example'
class: '!p-0'
props:
  autofocus: false
---
::

### Control search term

Sử dụng chỉ thị `v-model:search-term` để kiểm soát thuật ngữ tìm kiếm.

::component-example
---
collapse: true
name: 'command-palette-search-term-example'
class: '!p-0'
props:
  autofocus: false
---
::

::note
Ví dụ này sử dụng sự kiện `@update:model-value` để đặt lại thuật ngữ tìm kiếm khi một mục được chọn.
::

### With children in items

Bạn có thể tạo menu phân cấp bằng cách sử dụng thuộc tính `children` trong các mục. Khi một mục có con, nó sẽ tự động hiển thị biểu tượng chevron và cho phép điều hướng vào menu con.

::component-example
---
collapse: true
prettier: true
name: 'command-palette-items-children-example'
class: '!p-0'
props:
  autofocus: false
---
::

::note
Khi điều hướng vào menu con:
- Thuật ngữ tìm kiếm được đặt lại
- Nút quay lại xuất hiện trong đầu vào
- Bạn có thể quay lại nhóm trước bằng cách nhấn phím :kbd{value="backspace"}
::

### With fetched items

Bạn có thể lấy các mục từ API và sử dụng chúng trong CommandPalette.

::component-example
---
collapse: true
name: 'command-palette-fetch-example'
class: '!p-0'
props:
  autofocus: false
---
::

### With ignore filter

Bạn có thể đặt trường `ignoreFilter` thành `true` trên một nhóm để vô hiệu hóa tìm kiếm nội bộ và sử dụng logic tìm kiếm của riêng bạn.

::component-example
---
collapse: true
name: 'command-palette-ignore-filter-example'
class: '!p-0'
props:
  autofocus: false
---
::

::note
Ví dụ này sử dụng [`refDebounced`](https://vueuse.org/shared/refDebounced/#refdebounced) để debounce các cuộc gọi API.
::

### With post-filtered items

Bạn có thể sử dụng trường `postFilter` trên một nhóm để lọc các mục sau khi tìm kiếm xảy ra.

::component-example
---
collapse: true
name: 'command-palette-post-filter-example'
class: '!p-0'
props:
  autofocus: false
---
::

::note
Bắt đầu nhập để xem các mục có mức độ cao hơn xuất hiện.
::

### With custom fuse search

Bạn có thể sử dụng prop `fuse` để ghi đè các tùy chọn của [useFuse](https://vueuse.org/integrations/useFuse) mặc định là:

```ts
{
  fuseOptions: {
    ignoreLocation: true,
    threshold: 0.1,
    keys: ['label', 'suffix']
  },
  resultLimit: 12,
  matchAllWhenSearchEmpty: true
}
```

::tip
`fuseOptions` là các tùy chọn của [Fuse.js](https://www.fusejs.io/api/options.html), `resultLimit` là số lượng kết quả tối đa để trả về và `matchAllWhenSearchEmpty` là boolean để khớp tất cả các mục khi thuật ngữ tìm kiếm trống.
::

Ví dụ, bạn có thể đặt `{ fuseOptions: { includeMatches: true } }`{lang="ts-type"} để làm nổi bật thuật ngữ tìm kiếm trong các mục.

::component-example
---
collapse: true
name: 'command-palette-fuse-example'
class: '!p-0'
props:
  autofocus: false
---
::

### Within a Popover

Bạn có thể sử dụng thành phần CommandPalette bên trong nội dung của [Popover](/components/popover).

::component-example
---
collapse: true
name: 'popover-command-palette-example'
props:
  autofocus: false
---
::

### Within a Modal

Bạn có thể sử dụng thành phần CommandPalette bên trong nội dung của [Modal](/components/modal).

::component-example
---
collapse: true
name: 'modal-command-palette-example'
props:
  autofocus: false
---
::

### Within a Drawer

Bạn có thể sử dụng thành phần CommandPalette bên trong nội dung của [Drawer](/components/drawer).

::component-example
---
collapse: true
name: 'drawer-command-palette-example'
props:
  autofocus: false
---
::

### Listen open state

Khi sử dụng prop `close`, bạn có thể lắng nghe sự kiện `update:open` khi nút được nhấp.

::component-example
---
collapse: true
name: 'command-palette-open-example'
props:
  autofocus: false
---
::

::note
Điều này có thể hữu ích khi sử dụng CommandPalette bên trong [`Modal`](/components/modal) chẳng hạn.
::

### With footer slot :badge{label="New" class="align-text-top"}

Sử dụng slot `#footer` để thêm nội dung tùy chỉnh ở cuối CommandPalette, chẳng hạn như trợ giúp phím tắt hoặc hành động bổ sung.

::component-example
---
collapse: true
name: 'command-palette-footer-slot-example'
class: '!p-0'
props:
  autofocus: false
---
::

### With custom slot

Sử dụng thuộc tính `slot` để tùy chỉnh một mục hoặc nhóm cụ thể.

Bạn sẽ có quyền truy cập vào các slot sau:

- `#{{ item.slot }}`{lang="ts-type"}
- `#{{ item.slot }}-leading`{lang="ts-type"}
- `#{{ item.slot }}-label`{lang="ts-type"}
- `#{{ item.slot }}-trailing`{lang="ts-type"}

- `#{{ group.slot }}`{lang="ts-type"}
- `#{{ group.slot }}-leading`{lang="ts-type"}
- `#{{ group.slot }}-label`{lang="ts-type"}
- `#{{ group.slot }}-trailing`{lang="ts-type"}

::component-example
---
collapse: true
name: 'command-palette-custom-slot-example'
class: '!p-0'
props:
  autofocus: false
---
::

::tip{to="#slots"}
Bạn cũng có thể sử dụng các slot `#item`, `#item-leading`, `#item-label` và `#item-trailing` để tùy chỉnh tất cả các mục.
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
