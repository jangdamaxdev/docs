---
description: Một phần tử có thể thu gọn để chuyển đổi khả năng hiển thị của nội dung của nó.
category: element
links:
  - label: Collapsible
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/collapsible
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Collapsible.vue
---

## Usage

Sử dụng một [Button](/components/button) hoặc bất kỳ thành phần nào khác trong slot mặc định của Collapsible.

Sau đó, sử dụng slot `#content` để thêm nội dung được hiển thị khi Collapsible mở.

::component-code
---
prettier: true
ignore:
  - class
props:
  class: 'flex flex-col gap-2 w-48'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-down" block />

  content: |

    <Placeholder class="h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-down" block}

#content
:placeholder{class="h-48"}
::

### Unmount

Sử dụng prop `unmount-on-hide` để ngăn nội dung bị gỡ bỏ khi Collapsible bị thu gọn. Mặc định là `true`.

::component-code
---
prettier: true
ignore:
  - class
props:
  unmountOnHide: false
  class: 'flex flex-col gap-2 w-48'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-down" block />

  content: |

    <Placeholder class="h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-down" block}

#content
:placeholder{class="h-48"}
::

::note
Bạn có thể kiểm tra DOM để xem nội dung đang được hiển thị.
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa Collapsible.

::component-code
---
prettier: true
ignore:
  - class
props:
  class: 'flex flex-col gap-2 w-48'
  disabled: true
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-down" block />

  content: |

    <Placeholder class="h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-down" block}

#content
:placeholder{class="h-48"}
::

## Examples

### Control open state

Bạn có thể kiểm soát trạng thái mở bằng cách sử dụng prop `default-open` hoặc chỉ thị `v-model:open`.

::component-example
---
name: 'collapsible-open-example'
---
::

::note
Trong ví dụ này, tận dụng [`defineShortcuts`](/composables/define-shortcuts), bạn có thể chuyển đổi Collapsible bằng cách nhấn :kbd{value="O"}.
::

::tip
Điều này cho phép bạn di chuyển trigger bên ngoài Collapsible hoặc loại bỏ nó hoàn toàn.
::

### With rotating icon

Đây là một ví dụ với biểu tượng xoay trong Button cho biết trạng thái mở của Collapsible.

::component-example
---
name: 'collapsible-icon-example'
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
