---
title: NavigationMenu
description: Một danh sách các link có thể được hiển thị theo chiều ngang hoặc dọc.
category: navigation
links:
  - label: NavigationMenu
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/navigation-menu
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/NavigationMenu.vue
---

## Usage

### Items

Sử dụng prop `items` như một mảng các object với các thuộc tính sau:

- `label?: string`{lang="ts-type"}
- `icon?: string`{lang="ts-type"}
- `avatar?: AvatarProps`{lang="ts-type"}
- `badge?: string | number | BadgeProps`{lang="ts-type"}
- `tooltip?: TooltipProps`{lang="ts-type"}
- `trailingIcon?: string`{lang="ts-type"}
- `type?: 'label' | 'trigger' | 'link'`{lang="ts-type"}
- `defaultOpen?: boolean`{lang="ts-type"}
- `open?: boolean`{lang="ts-type"}
- `value?: string`{lang="ts-type"}
- `disabled?: boolean`{lang="ts-type"}
- [`slot?: string`{lang="ts-type"}](#with-custom-slot)
- `onSelect?(e: Event): void`{lang="ts-type"}
- `children?: NavigationMenuChildItem[]`{lang="ts-type"}
- `class?: any`{lang="ts-type"}
- `ui?: { linkLeadingAvatarSize?: ClassNameValue, linkLeadingAvatar?: ClassNameValue, linkLeadingIcon?: ClassNameValue, linkLabel?: ClassNameValue, linkLabelExternalIcon?: ClassNameValue, linkTrailing?: ClassNameValue, linkTrailingBadgeSize?: ClassNameValue, linkTrailingBadge?: ClassNameValue, linkTrailingIcon?: ClassNameValue, label?: ClassNameValue, link?: ClassNameValue, content?: ClassNameValue, childList?: ClassNameValue, childLabel?: ClassNameValue, childItem?: ClassNameValue, childLink?: ClassNameValue, childLinkIcon?: ClassNameValue, childLinkWrapper?: ClassNameValue, childLinkLabel?: ClassNameValue, childLinkLabelExternalIcon?: ClassNameValue, childLinkDescription?: ClassNameValue }`{lang="ts-type"}

Bạn có thể truyền bất kỳ thuộc tính nào từ component [Link](/components/link#props) như `to`, `target`, etc.

::component-code
---
collapse: true
ignore:
  - items
  - class
external:
  - items
externalTypes:
  - NavigationMenuItem[]
props:
  items:
    - label: Guide
      icon: i-lucide-book-open
      to: /getting-started
      children:
        - label: Introduction
          description: Fully styled and customizable components for Nuxt.
          icon: i-lucide-house
        - label: Installation
          description: Learn how to install and configure Nuxt UI in your application.
          icon: i-lucide-cloud-download
        - label: 'Icons'
          icon: 'i-lucide-smile'
          description: 'You have nothing to do, @nuxt/icon will handle it automatically.'
        - label: 'Colors'
          icon: 'i-lucide-swatch-book'
          description: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
        - label: 'Theme'
          icon: 'i-lucide-cog'
          description: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
    - label: Composables
      icon: i-lucide-database
      to: /composables
      children:
        - label: defineShortcuts
          icon: i-lucide-file-text
          description: Define shortcuts for your application.
          to: /composables/define-shortcuts
        - label: useOverlay
          icon: i-lucide-file-text
          description: Display a modal/slideover within your application.
          to: /composables/use-overlay
        - label: useToast
          icon: i-lucide-file-text
          description: Display a toast within your application.
          to: /composables/use-toast
    - label: Components
      icon: i-lucide-box
      to: /components
      active: true
      children:
        - label: Link
          icon: i-lucide-file-text
          description: Use NuxtLink with superpowers.
          to: /components/link
        - label: Modal
          icon: i-lucide-file-text
          description: Display a modal within your application.
          to: /components/modal
        - label: NavigationMenu
          icon: i-lucide-file-text
          description: Display a list of links.
          to: /components/navigation-menu
        - label: Pagination
          icon: i-lucide-file-text
          description: Display a list of pages.
          to: /components/pagination
        - label: Popover
          icon: i-lucide-file-text
          description: Display a non-modal dialog that floats around a trigger element.
          to: /components/popover
        - label: Progress
          icon: i-lucide-file-text
          description: Show a horizontal bar to indicate task progression.
          to: /components/progress
    - label: GitHub
      icon: i-simple-icons-github
      badge: 3.8k
      to: https://github.com/nuxt/ui
      target: _blank
    - label: Help
      icon: i-lucide-circle-help
      disabled: true
  class: 'w-full justify-center'
---
::

::note
Bạn cũng có thể truyền một mảng các mảng vào prop `items` để hiển thị các nhóm item.
::

::tip
Mỗi item có thể có một mảng `children` với các object có các thuộc tính sau để tạo submenu:

- `label: string`
- `description?: string`
- `icon?: string`
- `onSelect?(e: Event): void`
- `class?: any`

::

### Orientation

Sử dụng prop `orientation` để thay đổi orientation của NavigationMenu.

::note
Khi orientation là `vertical`, một component [Accordion](/components/accordion) được sử dụng để hiển thị mỗi nhóm. Bạn có thể kiểm soát trạng thái mở của mỗi item bằng cách sử dụng các thuộc tính `open` và `defaultOpen` và thay đổi hành vi bằng cách sử dụng các prop [`collapsible`](/components/accordion#collapsible) và [`type`](/components/accordion#multiple).
::

::component-code
---
collapse: true
ignore:
  - items
  - class
external:
  - items
externalTypes:
  - NavigationMenuItem[][]
props:
  orientation: 'vertical'
  items:
    - - label: Links
        type: 'label'
      - label: Guide
        icon: i-lucide-book-open
        children:
          - label: Introduction
            description: Fully styled and customizable components for Nuxt.
            icon: i-lucide-house
          - label: Installation
            description: Learn how to install and configure Nuxt UI in your application.
            icon: i-lucide-cloud-download
          - label: 'Icons'
            icon: 'i-lucide-smile'
            description: 'You have nothing to do, @nuxt/icon will handle it automatically.'
          - label: 'Colors'
            icon: 'i-lucide-swatch-book'
            description: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
          - label: 'Theme'
            icon: 'i-lucide-cog'
            description: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
      - label: Composables
        icon: i-lucide-database
        children:
          - label: defineShortcuts
            icon: i-lucide-file-text
            description: Define shortcuts for your application.
            to: /composables/define-shortcuts
          - label: useOverlay
            icon: i-lucide-file-text
            description: Display a modal/slideover within your application.
            to: /composables/use-overlay
          - label: useToast
            icon: i-lucide-file-text
            description: Display a toast within your application.
            to: /composables/use-toast
      - label: Components
        icon: i-lucide-box
        to: /components
        active: true
        defaultOpen: true
        children:
          - label: Link
            icon: i-lucide-file-text
            description: Use NuxtLink with superpowers.
            to: /components/link
          - label: Modal
            icon: i-lucide-file-text
            description: Display a modal within your application.
            to: /components/modal
          - label: NavigationMenu
            icon: i-lucide-file-text
            description: Display a list of links.
            to: /components/navigation-menu
          - label: Pagination
            icon: i-lucide-file-text
            description: Display a list of pages.
            to: /components/pagination
          - label: Popover
            icon: i-lucide-file-text
            description: Display a non-modal dialog that floats around a trigger element.
            to: /components/popover
          - label: Progress
            icon: i-lucide-file-text
            description: Show a horizontal bar to indicate task progression.
            to: /components/progress
    - - label: GitHub
        icon: i-simple-icons-github
        badge: 3.8k
        to: https://github.com/nuxt/ui
        target: _blank
      - label: Help
        icon: i-lucide-circle-help
        disabled: true
  class: 'data-[orientation=vertical]:w-48'
---
::

::note
Các nhóm sẽ được spaced khi orientation là `horizontal` và separated khi orientation là `vertical`.
::

### Collapsed

Trong `vertical` orientation, sử dụng prop `collapsed` để collapse NavigationMenu, điều này có thể hữu ích trong một sidebar ví dụ.

::note
Bạn có thể sử dụng các prop [`tooltip`](#with-tooltip-in-items) và [`popover`](#with-popover-in-items) để hiển thị thêm thông tin trên các item collapsed.
::

::component-code
---
collapse: true
ignore:
  - items
  - orientation
  - class
external:
  - items
externalTypes:
  - NavigationMenuItem[][]
items:
  tooltip:
    - true
    - false
  popover:
    - true
    - false
props:
  collapsed: true
  tooltip: false
  popover: false
  orientation: 'vertical'
  items:
    - - label: Links
        type: 'label'
      - label: Guide
        icon: i-lucide-book-open
        children:
          - label: Introduction
            description: Fully styled and customizable components for Nuxt.
            icon: i-lucide-house
          - label: Installation
            description: Learn how to install and configure Nuxt UI in your application.
            icon: i-lucide-cloud-download
          - label: 'Icons'
            icon: 'i-lucide-smile'
            description: 'You have nothing to do, @nuxt/icon will handle it automatically.'
          - label: 'Colors'
            icon: 'i-lucide-swatch-book'
            description: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
          - label: 'Theme'
            icon: 'i-lucide-cog'
            description: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
      - label: Composables
        icon: i-lucide-database
        children:
          - label: defineShortcuts
            icon: i-lucide-file-text
            description: Define shortcuts for your application.
            to: /composables/define-shortcuts
          - label: useOverlay
            icon: i-lucide-file-text
            description: Display a modal/slideover within your application.
            to: /composables/use-overlay
          - label: useToast
            icon: i-lucide-file-text
            description: Display a toast within your application.
            to: /composables/use-toast
      - label: Components
        icon: i-lucide-box
        to: /components
        active: true
        children:
          - label: Link
            icon: i-lucide-file-text
            description: Use NuxtLink with superpowers.
            to: /components/link
          - label: Modal
            icon: i-lucide-file-text
            description: Display a modal within your application.
            to: /components/modal
          - label: NavigationMenu
            icon: i-lucide-file-text
            description: Display a list of links.
            to: /components/navigation-menu
          - label: Pagination
            icon: i-lucide-file-text
            description: Display a list of pages.
            to: /components/pagination
          - label: Popover
            icon: i-lucide-file-text
            description: Display a non-modal dialog that floats around a trigger element.
            to: /components/popover
          - label: Progress
            icon: i-lucide-file-text
            description: Show a horizontal bar to indicate task progression.
            to: /components/progress
    - - label: GitHub
        icon: i-simple-icons-github
        badge: 3.8k
        to: https://github.com/nuxt/ui
        target: _blank
      - label: Help
        icon: i-lucide-circle-help
        disabled: true
---
::

### Highlight

Sử dụng prop `highlight` để hiển thị một border highlighted cho item active.

Sử dụng prop `highlight-color` để thay đổi màu của border. Nó mặc định là prop `color`.

::component-code
---
collapse: true
prettier: true
ignore:
  - items
  - class
external:
  - items
externalTypes:
  - NavigationMenuItem[][]
props:
  highlight: true
  highlightColor: 'primary'
  orientation: 'horizontal'
  items:
    - - label: Guide
        icon: i-lucide-book-open
        children:
          - label: Introduction
            description: Fully styled and customizable components for Nuxt.
            icon: i-lucide-house
          - label: Installation
            description: Learn how to install and configure Nuxt UI in your application.
            icon: i-lucide-cloud-download
          - label: 'Icons'
            icon: 'i-lucide-smile'
            description: 'You have nothing to do, @nuxt/icon will handle it automatically.'
          - label: 'Colors'
            icon: 'i-lucide-swatch-book'
            description: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
          - label: 'Theme'
            icon: 'i-lucide-cog'
            description: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
      - label: Composables
        icon: i-lucide-database
        children:
          - label: defineShortcuts
            icon: i-lucide-file-text
            description: Define shortcuts for your application.
            to: /composables/define-shortcuts
          - label: useOverlay
            icon: i-lucide-file-text
            description: Display a modal/slideover within your application.
            to: /composables/use-overlay
          - label: useToast
            icon: i-lucide-file-text
            description: Display a toast within your application.
            to: /composables/use-toast
      - label: Components
        icon: i-lucide-box
        to: /components
        active: true
        defaultOpen: true
        children:
          - label: Link
            icon: i-lucide-file-text
            description: Use NuxtLink with superpowers.
            to: /components/link
          - label: Modal
            icon: i-lucide-file-text
            description: Display a modal within your application.
            to: /components/modal
          - label: NavigationMenu
            icon: i-lucide-file-text
            description: Display a list of links.
            to: /components/navigation-menu
          - label: Pagination
            icon: i-lucide-file-text
            description: Display a list of pages.
            to: /components/pagination
          - label: Popover
            icon: i-lucide-file-text
            description: Display a non-modal dialog that floats around a trigger element.
            to: /components/popover
          - label: Progress
            icon: i-lucide-file-text
            description: Show a horizontal bar to indicate task progression.
            to: /components/progress
    - - label: GitHub
        icon: i-simple-icons-github
        badge: 3.8k
        to: https://github.com/nuxt/ui
        target: _blank
      - label: Help
        icon: i-lucide-circle-help
        disabled: true
  class: 'data-[orientation=horizontal]:border-b border-default data-[orientation=horizontal]:w-full data-[orientation=vertical]:w-48'
---
::

::note
Trong ví dụ này, class `border-b` được áp dụng để hiển thị một border trong `horizontal` orientation, điều này không được làm theo mặc định để để bạn có một clean slate để làm việc với.
::

::caution
Trong `vertical` orientation, prop `highlight` chỉ highlight border của children active.
::

### Color

Sử dụng prop `color` để thay đổi màu của NavigationMenu.

::component-code
---
ignore:
  - items
  - class
external:
  - items
externalTypes:
  - NavigationMenuItem[][]
props:
  color: neutral
  items:
    - - label: Guide
        icon: i-lucide-book-open
        to: /getting-started
      - label: Composables
        icon: i-lucide-database
        to: /composables
      - label: Components
        icon: i-lucide-box
        to: /components
        active: true
    - - label: GitHub
        icon: i-simple-icons-github
        badge: 3.8k
        to: https://github.com/nuxt/ui
        target: _blank
  class: 'w-full'
---
::

### Variant

Sử dụng prop `variant` để thay đổi variant của NavigationMenu.

::component-code
---
ignore:
  - items
  - class
external:
  - items
externalTypes:
  - NavigationMenuItem[][]
props:
  color: neutral
  variant: link
  highlight: false
  items:
    - - label: Guide
        icon: i-lucide-book-open
        to: /getting-started
      - label: Composables
        icon: i-lucide-database
        to: /composables
      - label: Components
        icon: i-lucide-box
        to: /components
        active: true
    - - label: GitHub
        icon: i-simple-icons-github
        badge: 3.8k
        to: https://github.com/nuxt/ui
        target: _blank
  class: 'w-full'
---
::

::note
Prop `highlight` thay đổi style item active của `pill` variant. Hãy thử nó để xem sự khác biệt.
::

### Trailing Icon

Sử dụng prop `trailing-icon` để tùy chỉnh [Icon](/components/icon) trailing của mỗi item. Mặc định là `i-lucide-chevron-down`. Icon này chỉ được hiển thị khi một item có children.

::tip
Bạn cũng có thể đặt một icon cho một item cụ thể bằng cách sử dụng thuộc tính `trailingIcon` trong object item.
::

::component-code
---
collapse: true
ignore:
  - items
  - class
external:
  - items
externalTypes:
  - NavigationMenuItem[]
props:
  trailingIcon: 'i-lucide-arrow-down'
  items:
    - label: Guide
      icon: i-lucide-book-open
      to: /getting-started
      children:
        - label: Introduction
          description: Fully styled and customizable components for Nuxt.
          icon: i-lucide-house
        - label: Installation
          description: Learn how to install and configure Nuxt UI in your application.
          icon: i-lucide-cloud-download
        - label: 'Icons'
          icon: 'i-lucide-smile'
          description: 'You have nothing to do, @nuxt/icon will handle it automatically.'
        - label: 'Colors'
          icon: 'i-lucide-swatch-book'
          description: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
        - label: 'Theme'
          icon: 'i-lucide-cog'
          description: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
    - label: Composables
      icon: i-lucide-database
      to: /composables
      children:
        - label: defineShortcuts
          icon: i-lucide-file-text
          description: Define shortcuts for your application.
          to: /composables/define-shortcuts
        - label: useOverlay
          icon: i-lucide-file-text
          description: Display a modal/slideover within your application.
          to: /composables/use-overlay
        - label: useToast
          icon: i-lucide-file-text
          description: Display a toast within your application.
          to: /composables/use-toast
    - label: Components
      icon: i-lucide-box
      to: /components
      active: true
      children:
        - label: Link
          icon: i-lucide-file-text
          description: Use NuxtLink with superpowers.
          to: /components/link
        - label: Modal
          icon: i-lucide-file-text
          description: Display a modal within your application.
          to: /components/modal
        - label: NavigationMenu
          icon: i-lucide-file-text
          description: Display a list of links.
          to: /components/navigation-menu
        - label: Pagination
          icon: i-lucide-file-text
          description: Display a list of pages.
          to: /components/pagination
        - label: Popover
          icon: i-lucide-file-text
          description: Display a non-modal dialog that floats around a trigger element.
          to: /components/popover
        - label: Progress
          icon: i-lucide-file-text
          description: Show a horizontal bar to indicate task progression.
          to: /components/progress
  class: 'w-full justify-center'
---
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `app.config.ts` dưới key `ui.icons.chevronDown`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `vite.config.ts` dưới key `ui.icons.chevronDown`.
:::
::

### Arrow

Sử dụng prop `arrow` để hiển thị một arrow trên content NavigationMenu khi items có children.

::component-code
---
collapse: true
ignore:
  - items
  - arrow
  - class
external:
  - items
externalTypes:
  - NavigationMenuItem[]
props:
  arrow: true
  items:
    - label: Guide
      icon: i-lucide-book-open
      to: /getting-started
      children:
        - label: Introduction
          description: Fully styled and customizable components for Nuxt.
          icon: i-lucide-house
        - label: Installation
          description: Learn how to install and configure Nuxt UI in your application.
          icon: i-lucide-cloud-download
        - label: 'Icons'
          icon: 'i-lucide-smile'
          description: 'You have nothing to do, @nuxt/icon will handle it automatically.'
        - label: 'Colors'
          icon: 'i-lucide-swatch-book'
          description: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
        - label: 'Theme'
          icon: 'i-lucide-cog'
          description: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
    - label: Composables
      icon: i-lucide-database
      to: /composables
      children:
        - label: defineShortcuts
          icon: i-lucide-file-text
          description: Define shortcuts for your application.
          to: /composables/define-shortcuts
        - label: useOverlay
          icon: i-lucide-file-text
          description: Display a modal/slideover within your application.
          to: /composables/use-overlay
        - label: useToast
          icon: i-lucide-file-text
          description: Display a toast within your application.
          to: /composables/use-toast
    - label: Components
      icon: i-lucide-box
      to: /components
      active: true
      children:
        - label: Link
          icon: i-lucide-file-text
          description: Use NuxtLink with superpowers.
          to: /components/link
        - label: Modal
          icon: i-lucide-file-text
          description: Display a modal within your application.
          to: /components/modal
        - label: NavigationMenu
          icon: i-lucide-file-text
          description: Display a list of links.
          to: /components/navigation-menu
        - label: Pagination
          icon: i-lucide-file-text
          description: Display a list of pages.
          to: /components/pagination
        - label: Popover
          icon: i-lucide-file-text
          description: Display a non-modal dialog that floats around a trigger element.
          to: /components/popover
        - label: Progress
          icon: i-lucide-file-text
          description: Show a horizontal bar to indicate task progression.
          to: /components/progress
  class: 'w-full justify-center'
---
::

::note
Arrow được animate để follow item active.
::

### Content Orientation

Sử dụng prop `content-orientation` để thay đổi orientation của content.

::warning
Prop này chỉ hoạt động khi `orientation` là `horizontal`.
::

::component-code
---
collapse: true
ignore:
  - items
  - arrow
  - class
external:
  - items
externalTypes:
  - NavigationMenuItem[]
props:
  arrow: true
  contentOrientation: 'vertical'
  items:
    - label: Guide
      icon: i-lucide-book-open
      to: /getting-started
      children:
        - label: Introduction
          description: Fully styled and customizable components for Nuxt.
          icon: i-lucide-house
        - label: Installation
          description: Learn how to install and configure Nuxt UI in your application.
          icon: i-lucide-cloud-download
        - label: 'Icons'
          icon: 'i-lucide-smile'
          description: 'You have nothing to do, @nuxt/icon will handle it automatically.'
    - label: Composables
      icon: i-lucide-database
      to: /composables
      children:
        - label: defineShortcuts
          icon: i-lucide-file-text
          description: Define shortcuts for your application.
          to: /composables/define-shortcuts
        - label: useOverlay
          icon: i-lucide-file-text
          description: Display a modal/slideover within your application.
          to: /composables/use-overlay
        - label: useToast
          icon: i-lucide-file-text
          description: Display a toast within your application.
          to: /composables/use-toast
    - label: Components
      icon: i-lucide-box
      to: /components
      active: true
      children:
        - label: Link
          icon: i-lucide-file-text
          description: Use NuxtLink with superpowers.
          to: /components/link
        - label: Modal
          icon: i-lucide-file-text
          description: Display a modal within your application.
          to: /components/modal
        - label: NavigationMenu
          icon: i-lucide-file-text
          description: Display a list of links.
          to: /components/navigation-menu
        - label: Pagination
          icon: i-lucide-file-text
          description: Display a list of pages.
          to: /components/pagination
  class: 'w-full justify-center'
---
::

### Unmount

Sử dụng prop `unmount-on-hide` để kiểm soát hành vi unmounting content. Mặc định là `true`.

::component-code
---
collapse: true
ignore:
  - items
  - arrow
  - class
external:
  - items
externalTypes:
  - NavigationMenuItem[]
props:
  unmountOnHide: false
  items:
    - label: Guide
      icon: i-lucide-book-open
      to: /getting-started
      children:
        - label: Introduction
          description: Fully styled and customizable components for Nuxt.
          icon: i-lucide-house
        - label: Installation
          description: Learn how to install and configure Nuxt UI in your application.
          icon: i-lucide-cloud-download
        - label: 'Icons'
          icon: 'i-lucide-smile'
          description: 'You have nothing to do, @nuxt/icon will handle it automatically.'
        - label: 'Colors'
          icon: 'i-lucide-swatch-book'
          description: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
        - label: 'Theme'
          icon: 'i-lucide-cog'
          description: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
    - label: Composables
      icon: i-lucide-database
      to: /composables
      children:
        - label: defineShortcuts
          icon: i-lucide-file-text
          description: Define shortcuts for your application.
          to: /composables/define-shortcuts
        - label: useOverlay
          icon: i-lucide-file-text
          description: Display a modal/slideover within your application.
          to: /composables/use-overlay
        - label: useToast
          icon: i-lucide-file-text
          description: Display a toast within your application.
          to: /composables/use-toast
    - label: Components
      icon: i-lucide-box
      to: /components
      active: true
      children:
        - label: Link
          icon: i-lucide-file-text
          description: Use NuxtLink with superpowers.
          to: /components/link
        - label: Modal
          icon: i-lucide-file-text
          description: Display a modal within your application.
          to: /components/modal
        - label: NavigationMenu
          icon: i-lucide-file-text
          description: Display a list of links.
          to: /components/navigation-menu
        - label: Pagination
          icon: i-lucide-file-text
          description: Display a list of pages.
          to: /components/pagination
        - label: Popover
          icon: i-lucide-file-text
          description: Display a non-modal dialog that floats around a trigger element.
          to: /components/popover
        - label: Progress
          icon: i-lucide-file-text
          description: Show a horizontal bar to indicate task progression.
          to: /components/progress
  class: 'w-full justify-center'
---
::

::note
Bạn có thể inspect DOM để xem content của mỗi item được render.
::

## Examples

### With tooltip in items

Khi orientation là `vertical` và menu là `collapsed`, bạn có thể đặt prop `tooltip` thành `true` để hiển thị một [Tooltip](/components/tooltip) xung quanh items với label của chúng nhưng bạn cũng có thể sử dụng thuộc tính `tooltip` trên mỗi item để override tooltip mặc định.

Bạn có thể truyền bất kỳ thuộc tính nào từ component [Tooltip](/components/tooltip) toàn cục hoặc trên mỗi item.

::component-code
---
collapse: true
ignore:
  - items
  - orientation
  - class
external:
  - items
externalTypes:
  - NavigationMenuItem[][]
items:
  tooltip:
    - true
    - false
props:
  tooltip: true
  collapsed: true
  orientation: 'vertical'
  items:
    - - label: Links
        type: 'label'
      - label: Guide
        icon: i-lucide-book-open
        children:
          - label: Introduction
            description: Fully styled and customizable components for Nuxt.
            icon: i-lucide-house
          - label: Installation
            description: Learn how to install and configure Nuxt UI in your application.
            icon: i-lucide-cloud-download
          - label: 'Icons'
            icon: 'i-lucide-smile'
            description: 'You have nothing to do, @nuxt/icon will handle it automatically.'
          - label: 'Colors'
            icon: 'i-lucide-swatch-book'
            description: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
          - label: 'Theme'
            icon: 'i-lucide-cog'
            description: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
      - label: Composables
        icon: i-lucide-database
        children:
          - label: defineShortcuts
            icon: i-lucide-file-text
            description: Define shortcuts for your application.
            to: /composables/define-shortcuts
          - label: useOverlay
            icon: i-lucide-file-text
            description: Display a modal/slideover within your application.
            to: /composables/use-overlay
          - label: useToast
            icon: i-lucide-file-text
            description: Display a toast within your application.
            to: /composables/use-toast
      - label: Components
        icon: i-lucide-box
        to: /components
        active: true
        children:
          - label: Link
            icon: i-lucide-file-text
            description: Use NuxtLink with superpowers.
            to: /components/link
          - label: Modal
            icon: i-lucide-file-text
            description: Display a modal within your application.
            to: /components/modal
          - label: NavigationMenu
            icon: i-lucide-file-text
            description: Display a list of links.
            to: /components/navigation-menu
          - label: Pagination
            icon: i-lucide-file-text
            description: Display a list of pages.
            to: /components/pagination
          - label: Popover
            icon: i-lucide-file-text
            description: Display a non-modal dialog that floats around a trigger element.
            to: /components/popover
          - label: Progress
            icon: i-lucide-file-text
            description: Show a horizontal bar to indicate task progression.
            to: /components/progress
    - - label: GitHub
        icon: i-simple-icons-github
        badge: 3.8k
        to: https://github.com/nuxt/ui
        target: _blank
        tooltip:
          text: 'Open on GitHub'
          kbds:
            - 3.8k
      - label: Help
        icon: i-lucide-circle-help
        disabled: true
---
::

### With popover in items

Khi orientation là `vertical` và menu là `collapsed`, bạn có thể đặt prop `popover` thành `true` để hiển thị một [Popover](/components/popover) xung quanh items với children của chúng nhưng bạn cũng có thể sử dụng thuộc tính `popover` trên mỗi item để override popover mặc định.

Bạn có thể truyền bất kỳ thuộc tính nào từ component [Popover](/components/popover) toàn cục hoặc trên mỗi item.

::component-code
---
collapse: true
ignore:
  - items
  - orientation
  - class
external:
  - items
externalTypes:
  - NavigationMenuItem[][]
items:
  popover:
    - true
    - false
props:
  popover: true
  collapsed: true
  orientation: 'vertical'
  items:
    - - label: Links
        type: 'label'
      - label: Guide
        icon: i-lucide-book-open
        children:
          - label: Introduction
            description: Fully styled and customizable components for Nuxt.
            icon: i-lucide-house
          - label: Installation
            description: Learn how to install and configure Nuxt UI in your application.
            icon: i-lucide-cloud-download
          - label: 'Icons'
            icon: 'i-lucide-smile'
            description: 'You have nothing to do, @nuxt/icon will handle it automatically.'
          - label: 'Colors'
            icon: 'i-lucide-swatch-book'
            description: 'Choose a primary and a neutral color from your Tailwind CSS theme.'
          - label: 'Theme'
            icon: 'i-lucide-cog'
            description: 'You can customize components by using the `class` / `ui` props or in your app.config.ts.'
      - label: Composables
        icon: i-lucide-database
        popover:
          mode: 'click'
        children:
          - label: defineShortcuts
            icon: i-lucide-file-text
            description: Define shortcuts for your application.
            to: /composables/define-shortcuts
          - label: useOverlay
            icon: i-lucide-file-text
            description: Display a modal/slideover within your application.
            to: /composables/use-overlay
          - label: useToast
            icon: i-lucide-file-text
            description: Display a toast within your application.
            to: /composables/use-toast
      - label: Components
        icon: i-lucide-box
        to: /components
        active: true
        children:
          - label: Link
            icon: i-lucide-file-text
            description: Use NuxtLink with superpowers.
            to: /components/link
          - label: Modal
            icon: i-lucide-file-text
            description: Display a modal within your application.
            to: /components/modal
          - label: NavigationMenu
            icon: i-lucide-file-text
            description: Display a list of links.
            to: /components/navigation-menu
          - label: Pagination
            icon: i-lucide-file-text
            description: Display a list of pages.
            to: /components/pagination
          - label: Popover
            icon: i-lucide-file-text
            description: Display a non-modal dialog that floats around a trigger element.
            to: /components/popover
          - label: Progress
            icon: i-lucide-file-text
            description: Show a horizontal bar to indicate task progression.
            to: /components/progress
    - - label: GitHub
        icon: i-simple-icons-github
        badge: 3.8k
        to: https://github.com/nuxt/ui
        target: _blank
        tooltip:
          text: 'Open on GitHub'
          kbds:
            - 3.8k
      - label: Help
        icon: i-lucide-circle-help
        disabled: true
---
::

::tip{to="#with-content-slot"}
Bạn có thể sử dụng slot `#content` để tùy chỉnh content của popover trong `vertical` orientation.
::

### Control active item

Bạn có thể kiểm soát item active bằng cách sử dụng prop `default-value` hoặc directive `v-model` với index của item.

::component-example
---
collapse: true
name: 'navigation-menu-model-value-example'
---
::

::note
Trong ví dụ này, tận dụng [`defineShortcuts`](/composables/define-shortcuts), bạn có thể switch item active bằng cách nhấn :kbd{value="1"}, :kbd{value="2"}, hoặc :kbd{value="3"}.
::

::tip
Bạn cũng có thể truyền `value` của một trong các items nếu được cung cấp.
::

### With custom slot

Sử dụng thuộc tính `slot` để tùy chỉnh một item cụ thể.

Bạn sẽ có access đến các slots sau:

- `#{{ item.slot }}`{lang="ts-type"}
- `#{{ item.slot }}-leading`{lang="ts-type"}
- `#{{ item.slot }}-label`{lang="ts-type"}
- `#{{ item.slot }}-trailing`{lang="ts-type"}
- `#{{ item.slot }}-content`{lang="ts-type"}

::component-example
---
name: 'navigation-menu-custom-slot-example'
---
::

::tip{to="#slots"}
Bạn cũng có thể sử dụng slots `#item`, `#item-leading`, `#item-label`, `#item-trailing` và `#item-content` để tùy chỉnh tất cả items.
::

### With content slot

Sử dụng slot `#item-content` hoặc thuộc tính `slot` (`#{{ item.slot }}-content`) để tùy chỉnh content của một item cụ thể.

::component-example
---
collapse: true
name: 'navigation-menu-content-slot-example'
---
::

::note
Trong ví dụ này, chúng tôi thêm class `sm:w-(--reka-navigation-menu-viewport-width)` trên `viewport` để có width động. Điều này yêu cầu đặt width trên first child của content.
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