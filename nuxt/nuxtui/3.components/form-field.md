---
title: FormField
description: A wrapper for form elements that provides validation and error handling.
category: form
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/FormField.vue
---

## Usage

Bao bọc bất kỳ thành phần form nào với FormField. Được sử dụng trong một [Form](/components/form), nó cung cấp xác thực và xử lý lỗi.

### Label

Sử dụng prop `label` để đặt nhãn cho điều khiển form.

::component-code
---
prettier: true
props:
  label: Email
slots:
  default: |

    <UInput placeholder="Enter your email" />
---

:u-input{placeholder="Enter your email"}
::

::note
Thuộc tính `for` của nhãn và điều khiển form được liên kết với một `id` duy nhất nếu không được cung cấp.
::

Khi sử dụng prop `required`, một dấu hoa thị được thêm bên cạnh nhãn.

::component-code
---
prettier: true
ignore:
  - label
props:
  label: Email
  required: true
slots:
  default: |

    <UInput placeholder="Enter your email" />
---

:u-input{placeholder="Enter your email"}
::

### Description

Sử dụng prop `description` để cung cấp thông tin bổ sung dưới nhãn.

::component-code
---
prettier: true
ignore:
  - label
props:
  label: Email
  description: We'll never share your email with anyone else.
slots:
  default: |

    <UInput placeholder="Enter your email" class="w-full" />
---

:u-input{placeholder="Enter your email" class="w-full"}
::

### Hint

Sử dụng prop `hint` để hiển thị thông báo gợi ý bên cạnh nhãn.

::component-code
---
prettier: true
ignore:
  - label
props:
  label: Email
  hint: Optional
slots:
  default: |

    <UInput placeholder="Enter your email" />
---

:u-input{placeholder="Enter your email"}
::

### Help

Sử dụng prop `help` để hiển thị thông báo trợ giúp dưới điều khiển form.

::component-code
---
prettier: true
ignore:
  - label
props:
  label: Email
  help: Please enter a valid email address.
slots:
  default: |

    <UInput placeholder="Enter your email" class="w-full" />
---

:u-input{placeholder="Enter your email" class="w-full"}
::

### Error

Sử dụng prop `error` để hiển thị thông báo lỗi dưới điều khiển form. Khi được sử dụng cùng với prop `help`, prop `error` có ưu tiên.

Khi được sử dụng bên trong một [Form](/components/form), điều này được đặt tự động khi xảy ra lỗi xác thực.

::component-code
---
prettier: true
ignore:
  - label
props:
  label: Email
  error: Please enter a valid email address.
slots:
  default: |

    <UInput placeholder="Enter your email" class="w-full" />
---

:u-input{placeholder="Enter your email" class="w-full"}
::

::tip{to="/getting-started/theme#colors"}
Điều này đặt `color` thành `error` trên điều khiển form. Bạn có thể thay đổi nó toàn cục trong `app.config.ts` của bạn.
::

### Size

Sử dụng prop `size` để thay đổi kích thước của FormField, `size` được ủy quyền cho điều khiển form.

::component-code
---
prettier: true
ignore:
  - label
  - description
  - hint
  - help
props:
  label: Email
  description: We'll never share your email with anyone else.
  hint: Optional
  help: Please enter a valid email address.
  size: xl
slots:
  default: |

    <UInput placeholder="Enter your email" class="w-full" />
---

:u-input{placeholder="Enter your email" class="w-full"}
::

## API

### Props

:component-props

### Slots

:component-slots

## Theme

:component-theme

## Changelog

:component-changelog
