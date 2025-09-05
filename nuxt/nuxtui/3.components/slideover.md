---
description: Một dialog trượt vào từ bất kỳ bên nào của màn hình.
category: overlay
links:
  - label: Dialog
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/dialog
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Slideover.vue
---

## Usage

Sử dụng một [Button](/components/button) hoặc bất kỳ component nào khác trong slot default của Slideover.

Sau đó, sử dụng slot `#content` để thêm nội dung hiển thị khi Slideover được mở.

::component-code
---
prettier: true
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  content: |

    <Placeholder class="h-full m-4" />
---

:u-button{label="Open" color="neutral" variant="subtle"}

#content
:placeholder{class="h-full m-4"}
::

Bạn cũng có thể sử dụng các slot `#header`{lang="ts-type"}, `#body`{lang="ts-type"} và `#footer`{lang="ts-type"} để tùy chỉnh nội dung của Slideover.

### Title

Sử dụng prop `title` để đặt tiêu đề của header Slideover's.

::component-code
---
prettier: true
props:
  title: 'Slideover with title'
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

### Description

Sử dụng prop `description` để đặt mô tả của header Slideover's.

::component-code
---
prettier: true
ignore:
  - title
props:
  title: 'Slideover with description'
  description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.'
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

### Close

Sử dụng prop `close` để tùy chỉnh hoặc ẩn nút close (với giá trị `false`) được hiển thị trong header Slideover's.

Bạn có thể truyền bất kỳ thuộc tính nào từ thành phần [Button](/components/button) để tùy chỉnh nó.

::component-code
---
prettier: true
ignore:
  - title
  - close.color
  - close.variant
props:
  title: 'Slideover with close button'
  close:
    color: primary
    variant: outline
    class: 'rounded-full'
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

::note
Nút close không được hiển thị nếu slot `#content` được sử dụng vì nó là một phần của header.
::

### Close Icon

Sử dụng prop `close-icon` để tùy chỉnh [Icon](/components/icon) của nút close. Mặc định là `i-lucide-x`.

::component-code
---
prettier: true
ignore:
  - title
props:
  title: 'Slideover with close button'
  closeIcon: 'i-lucide-arrow-right'
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

::framework-only
#nuxt
:::tip{to="/getting-started/icons/nuxt#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `app.config.ts` của bạn dưới khóa `ui.icons.close`.
:::

#vue
:::tip{to="/getting-started/icons/vue#theme"}
Bạn có thể tùy chỉnh icon này toàn cục trong `vite.config.ts` của bạn dưới khóa `ui.icons.close`.
:::
::

### Side

Sử dụng prop `side` để đặt bên của màn hình mà Slideover sẽ trượt vào từ đó. Mặc định là `right`.

::component-code
---
prettier: true
ignore:
  - title
props:
  side: 'left'
  title: 'Slideover with side'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" />

  body: |

    <Placeholder class="h-full min-h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle"}

#body
:placeholder{class="h-full min-h-48"}
::

### Overlay

Sử dụng prop `overlay` để kiểm soát xem Slideover có overlay hay không. Mặc định là `true`.

::component-code
---
prettier: true
ignore:
  - title
props:
  overlay: false
  title: 'Slideover without overlay'
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

### Transition

Sử dụng prop `transition` để kiểm soát xem Slideover có được animate hay không. Mặc định là `true`.

::component-code
---
prettier: true
ignore:
  - title
props:
  transition: false
  title: 'Slideover without transition'
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
name: 'slideover-open-example'
---
::

::note
Trong ví dụ này, tận dụng [`defineShortcuts`](/composables/define-shortcuts), bạn có thể chuyển đổi Slideover bằng cách nhấn :kbd{value="O"}.
::

::tip
Điều này cho phép bạn di chuyển trigger ra ngoài Slideover hoặc loại bỏ nó hoàn toàn.
::

### Disable dismissal

Đặt prop `dismissible` thành `false` để ngăn Slideover bị đóng khi nhấp bên ngoài hoặc nhấn escape. Sự kiện `close:prevent` sẽ được emit khi người dùng cố gắng đóng nó.

::component-code
---
prettier: true
ignore:
  - title
  - dismissible
props:
  dismissible: false
  title: 'Slideover non-dismissible'
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

### Programmatic usage

Bạn có thể sử dụng composable [`useOverlay`](/composables/use-overlay) để mở Slideover theo chương trình.

::warning
Hãy đảm bảo wrap app của bạn với thành phần [`App`](/components/app) sử dụng thành phần [`OverlayProvider`](https://github.com/nuxt/ui/blob/v3/src/runtime/components/OverlayProvider.vue).
::

Đầu tiên, tạo một slideover component sẽ được mở theo chương trình:

::component-example
---
prettier: true
name: 'slideover-example'
preview: false
---
::

::note
Chúng tôi đang emit sự kiện `close` khi slideover được đóng hoặc dismissed ở đây. Bạn có thể emit bất kỳ dữ liệu nào thông qua sự kiện `close`, tuy nhiên, sự kiện phải được emit để capture giá trị trả về.
::

Sau đó, sử dụng nó trong app của bạn:

::component-example
---
name: 'slideover-programmatic-example'
---
::

::tip
Bạn có thể đóng slideover trong slideover component bằng cách emit `emit('close')`.
::

### Nested slideovers

Bạn có thể lồng slideovers trong nhau.

::component-example
---
name: 'slideover-nested-example'
---
::

### With footer slot

Sử dụng slot `#footer` để thêm nội dung sau body của Slideover.

::component-example
---
name: 'slideover-footer-slot-example'
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