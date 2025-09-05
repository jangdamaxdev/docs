---
description: Một cửa sổ dialog có thể được sử dụng để hiển thị một thông điệp hoặc yêu cầu đầu vào từ người dùng.
category: overlay
links:
  - label: Dialog
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/dialog
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Modal.vue
---

## Usage

Sử dụng một [Button](/components/button) hoặc bất kỳ component nào khác trong slot mặc định của Modal.

Sau đó, sử dụng slot `#content` để thêm nội dung được hiển thị khi Modal mở.

::component-code
---
prettier: true
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  content: |

    <Placeholder class="h-48 m-4" />
---

:u-button{label="Open" color="neutral" variant="subtle"}

#content
:placeholder{class="h-48 m-4"}
::

Bạn cũng có thể sử dụng các slot `#header`{lang="ts-type"}, `#body`{lang="ts-type"} và `#footer`{lang="ts-type"} để tùy chỉnh nội dung của Modal.

### Title

Sử dụng prop `title` để đặt tiêu đề của header Modal.

::component-code
---
prettier: true
props:
  title: 'Modal with title'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  body: |

    <Placeholder class="h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle"}

#body
:placeholder{class="h-48"}
::

### Description

Sử dụng prop `description` để đặt mô tả của header Modal.

::component-code
---
prettier: true
ignore:
  - title
props:
  title: 'Modal with description'
  description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  body: |

    <Placeholder class="h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle"}

#body
:placeholder{class="h-48"}
::

### Close

Sử dụng prop `close` để tùy chỉnh hoặc ẩn nút đóng (với giá trị `false`) được hiển thị trong header Modal.

Bạn có thể truyền bất kỳ thuộc tính nào từ component [Button](/components/button) để tùy chỉnh nó.

::component-code
---
prettier: true
ignore:
  - title
  - close.color
  - close.variant
props:
  title: 'Modal with close button'
  close:
    color: primary
    variant: outline
    class: 'rounded-full'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  body: |

    <Placeholder class="h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle"}

#body
:placeholder{class="h-48"}
::

::tip
Nút đóng không được hiển thị nếu slot `#content` được sử dụng vì nó là một phần của header.
::

### Close Icon

Sử dụng prop `close-icon` để tùy chỉnh [Icon](/components/icon) của nút đóng. Mặc định là `i-lucide-x`.

::component-code
---
prettier: true
ignore:
  - title
props:
  title: 'Modal with close button'
  closeIcon: 'i-lucide-arrow-right'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  body: |

    <Placeholder class="h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle"}

#body
:placeholder{class="h-48"}
::

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `app.config.ts` dưới key `ui.icons.close`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `vite.config.ts` dưới key `ui.icons.close`.
:::
::

### Overlay

Sử dụng prop `overlay` để kiểm soát xem Modal có overlay hay không. Mặc định là `true`.

::component-code
---
prettier: true
ignore:
  - title
props:
  overlay: false
  title: 'Modal without overlay'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  body: |

    <Placeholder class="h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle"}

#body
:placeholder{class="h-48"}
::

### Transition

Sử dụng prop `transition` để kiểm soát xem Modal có được animate hay không. Mặc định là `true`.

::component-code
---
prettier: true
ignore:
  - title
props:
  transition: false
  title: 'Modal without transition'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  body: |

    <Placeholder class="h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle"}

#body
:placeholder{class="h-48"}
::

### Fullscreen

Sử dụng prop `fullscreen` để làm cho Modal fullscreen.

::component-code
---
prettier: true
ignore:
  - title
  - fullscreen
props:
  fullscreen: true
  title: 'Modal fullscreen'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  body: |

    <Placeholder class="h-full" />
---

:u-button{label="Open" color="neutral" variant="subtle"}

#body
:placeholder{class="h-full"}
::

## Examples

### Control open state

Bạn có thể kiểm soát trạng thái mở bằng cách sử dụng prop `default-open` hoặc directive `v-model:open`.

::component-example
---
name: 'modal-open-example'
---
::

::note
Trong ví dụ này, tận dụng [`defineShortcuts`](/composables/define-shortcuts), bạn có thể toggle Modal bằng cách nhấn :kbd{value="O"}.
::

::tip
Điều này cho phép bạn di chuyển trigger bên ngoài Modal hoặc loại bỏ nó hoàn toàn.
::

### Disable dismissal

Đặt prop `dismissible` thành `false` để ngăn Modal bị đóng khi click bên ngoài hoặc nhấn escape. Sự kiện `close:prevent` sẽ được emit khi người dùng cố gắng đóng nó.

::component-code
---
prettier: true
ignore:
  - title
  - dismissible
props:
  dismissible: false
  title: 'Modal non-dismissible'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  body: |

    <Placeholder class="h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle"}

#body
:placeholder{class="h-48"}
::

### Programmatic usage

Bạn có thể sử dụng composable [`useOverlay`](/composables/use-overlay) để mở Modal theo chương trình.

::warning
Đảm bảo wrap app của bạn với component [`App`](/components/app) sử dụng component [`OverlayProvider`](https://github.com/nuxt/ui/blob/v3/src/runtime/components/OverlayProvider.vue).
::

Đầu tiên, tạo một component modal sẽ được mở theo chương trình:

::component-example
---
prettier: true
name: 'modal-example'
preview: false
---
::

::note
Chúng tôi đang emit sự kiện `close` khi modal bị đóng hoặc dismissed ở đây. Bạn có thể emit bất kỳ dữ liệu nào thông qua sự kiện `close`, tuy nhiên, sự kiện phải được emit để capture giá trị trả về.
::

Sau đó, sử dụng nó trong app của bạn:

::component-example
---
name: 'modal-programmatic-example'
---
::

::tip
Bạn có thể đóng modal trong component modal bằng cách emit `emit('close')`.
::

### Nested modals

Bạn có thể lồng các modal trong nhau.

::component-example
---
name: 'modal-nested-example'
---
::

### With footer slot

Sử dụng slot `#footer` để thêm nội dung sau body của Modal.

::component-example
---
name: 'modal-footer-slot-example'
---
::

### With command palette

Bạn có thể sử dụng component [CommandPalette](/components/command-palette) bên trong nội dung của Modal.

::component-example
---
collapse: true
name: 'modal-command-palette-example'
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