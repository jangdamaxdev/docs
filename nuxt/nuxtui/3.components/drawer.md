---
description: A drawer that smoothly slides in & out of the screen.
category: overlay
links:
  - label: Drawer
    icon: i-custom-reka-ui
    to: https://github.com/unovue/vaul-vue
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Drawer.vue
---

## Usage

Sử dụng một [Button](/components/button) hoặc bất kỳ thành phần nào khác trong slot mặc định của Drawer.

Sau đó, sử dụng slot `#content` để thêm nội dung hiển thị khi Drawer mở.

::component-code
---
prettier: true
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up" />

  content: |

    <Placeholder class="h-48 m-4" />
---

:u-button{label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up"}

#content
:placeholder{class="h-48 m-4"}
::

Bạn cũng có thể sử dụng các slot `#header`{lang="ts-type"}, `#body`{lang="ts-type"} và `#footer`{lang="ts-type"} để tùy chỉnh nội dung của Drawer.

### Title

Sử dụng prop `title` để đặt tiêu đề cho header của Drawer.

::component-code
---
prettier: true
props:
  title: 'Drawer with title'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up" />

  body: |

    <Placeholder class="h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up"}

#body
:placeholder{class="h-48"}
::

### Description

Sử dụng prop `description` để đặt mô tả cho header của Drawer.

::component-code
---
prettier: true
ignore:
  - title
props:
  title: 'Drawer with description'
  description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up" />

  body: |

    <Placeholder class="h-48" />
---

:u-button{label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up"}

#body
:placeholder{class="h-48"}
::

### Direction

Sử dụng prop `direction` để kiểm soát hướng của Drawer. Mặc định là `bottom`.

::component-code
---
prettier: true
props:
  direction: 'right'
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up" />

  content: |

    <Placeholder class="min-w-96 min-h-96 size-full m-4" />
---

:u-button{label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up"}

#content
:placeholder{class="min-w-96 min-h-96 size-full m-4"}
::

### Inset

Sử dụng prop `inset` để chèn Drawer từ các cạnh.

::component-code
---
prettier: true
props:
  direction: 'right'
  inset: true
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up" />

  content: |

    <Placeholder class="min-w-96 min-h-96 size-full m-4" />
---

:u-button{label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up"}

#content
:placeholder{class="min-w-96 min-h-96 size-full m-4"}
::

### Handle

Sử dụng prop `handle` để kiểm soát xem Drawer có tay nắm hay không. Mặc định là `true`.

::component-code
---
prettier: true
props:
  handle: false
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up" />

  content: |

    <Placeholder class="h-48 m-4" />
---

:u-button{label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up"}

#content
:placeholder{class="h-48 m-4"}
::

### Handle Only

Sử dụng prop `handle-only` để chỉ cho phép kéo Drawer bằng tay nắm.

::component-code
---
prettier: true
props:
  handleOnly: true
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up" />

  content: |

    <Placeholder class="h-48 m-4" />
---

:u-button{label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up"}

#content
:placeholder{class="h-48 m-4"}
::

### Overlay

Sử dụng prop `overlay` để kiểm soát xem Drawer có overlay hay không. Mặc định là `true`.

::component-code
---
prettier: true
props:
  overlay: false
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up" />

  content: |

    <Placeholder class="h-48 m-4" />
---

:u-button{label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up"}

#content
:placeholder{class="h-48 m-4"}
::

### Scale background

Sử dụng prop `should-scale-background` để thu nhỏ nền khi Drawer mở, tạo hiệu ứng chiều sâu thị giác. Bạn có thể đặt prop `set-background-color-on-scale` thành `false` để ngăn thay đổi màu nền.

::component-code
---
prettier: true
props:
  shouldScaleBackground: true
  setBackgroundColorOnScale: true
slots:
  default: |

    <UButton label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up" />

  content: |

    <Placeholder class="h-48 m-4" />
---

:u-button{label="Open" color="neutral" variant="subtle" trailing-icon="i-lucide-chevron-up"}

#content
:placeholder{class="h-screen m-4"}
::

::warning
Hãy đảm bảo thêm directive `data-vaul-drawer-wrapper` vào một phần tử cha của ứng dụng của bạn để điều này hoạt động.

```vue [app.vue]
<template>
  <UApp>
    <div class="bg-default" data-vaul-drawer-wrapper>
      <NuxtLayout>
        <NuxtPage />
      </NuxtLayout>
    </div>
  </UApp>
</template>
```

```ts [nuxt.config.ts]
export default defineNuxtConfig({
  app: {
    rootAttrs: {
      'data-vaul-drawer-wrapper': '',
      'class': 'bg-default'
    }
  }
})
```

::

## Examples

### Control open state

Bạn có thể kiểm soát trạng thái mở bằng cách sử dụng prop `default-open` hoặc directive `v-model:open`.

::component-example
---
prettier: true
name: 'drawer-open-example'
---
::

::note
Trong ví dụ này, tận dụng [`defineShortcuts`](/composables/define-shortcuts), bạn có thể chuyển đổi Drawer bằng cách nhấn :kbd{value="O"}.
::

::tip
Điều này cho phép bạn di chuyển trigger ra ngoài Drawer hoặc loại bỏ nó hoàn toàn.
::

### Disable dismissal

Đặt prop `dismissible` thành `false` để ngăn Drawer bị đóng khi nhấp bên ngoài hoặc nhấn escape.

::component-example
---
prettier: true
name: 'drawer-dismissible-example'
---
::

::note
Trong ví dụ này, slot `header` được sử dụng để thêm nút đóng mà không được thực hiện theo mặc định.
::

### With interactive background

Đặt prop `overlay` và `modal` thành `false` cùng với prop `dismissible` để làm cho nền của Drawer tương tác mà không đóng Drawer.

::component-example
---
prettier: true
name: 'drawer-modal-example'
---
::

### Responsive drawer

Bạn có thể render một thành phần [Modal](/components/modal) trên desktop và một Drawer trên mobile ví dụ.

::component-example
---
prettier: true
name: 'drawer-responsive-example'
---
::

### Nested drawers :badge{label="New" class="align-text-top"}

Bạn có thể lồng các drawer vào nhau bằng cách sử dụng prop `nested`.

::component-example
---
prettier: true
name: 'drawer-nested-example'
---
::

### With footer slot

Sử dụng slot `#footer` để thêm nội dung sau body của Drawer.

::component-example
---
prettier: true
collapse: true
name: 'drawer-footer-slot-example'
---
::

### With command palette

Bạn có thể sử dụng một thành phần [CommandPalette](/components/command-palette) bên trong nội dung của Drawer.

::component-example
---
collapse: true
name: 'drawer-command-palette-example'
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
