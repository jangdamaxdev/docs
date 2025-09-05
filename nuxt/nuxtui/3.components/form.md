---
description: A form component with built-in validation and submission handling.
category: form
links:
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Form.vue
---

## Usage

Sử dụng thành phần Form để xác thực dữ liệu form bằng cách sử dụng các thư viện xác thực như [Valibot](https://github.com/fabian-hiller/valibot), [Zod](https://github.com/colinhacks/zod), [Yup](https://github.com/jquense/yup), [Joi](https://github.com/hapijs/joi), [Superstruct](https://github.com/ianstormtaylor/superstruct) hoặc logic xác thực của riêng bạn.

Nó hoạt động với thành phần [FormField](/components/form-field) để hiển thị thông báo lỗi xung quanh các phần tử form tự động.

### Schema Validation

Nó yêu cầu hai prop:

- `state` - một đối tượng reactive chứa trạng thái của form.
- `schema` - bất kỳ [Standard Schema](https://standardschema.dev/) nào hoặc một schema từ [Yup](https://github.com/jquense/yup), [Joi](https://github.com/hapijs/joi) hoặc [Superstruct](https://github.com/ianstormtaylor/superstruct).

::warning
**Không có thư viện xác thực nào được bao gồm** theo mặc định, đảm bảo bạn **cài đặt thư viện bạn cần**.
::

::tabs{class="gap-0"}
  ::component-example{label="Valibot"}
  ---
  name: 'form-example-valibot'
  props:
    class: 'w-60'
  ---
  ::

  ::component-example{label="Zod"}
  ---
  name: 'form-example-zod'
  props:
    class: 'w-60'
  ---
  ::

  ::component-example{label="Yup"}
  ---
  name: 'form-example-yup'
  props:
    class: 'w-60'
  ---
  ::

  ::component-example{label="Joi"}
  ---
  name: 'form-example-joi'
  props:
    class: 'w-60'
  ---
  ::

  ::component-example{label="Superstruct"}
  ---
  name: 'form-example-superstruct'
  props:
    class: 'w-60'
  ---
  ::
::

Lỗi được báo cáo trực tiếp cho thành phần [FormField](/components/form-field) dựa trên prop `name` hoặc `error-pattern`. Điều này có nghĩa là các quy tắc xác thực được định nghĩa cho thuộc tính `email` trong schema của bạn sẽ được áp dụng cho `<FormField name="email">`{lang="vue"}.

Các quy tắc xác thực lồng nhau được xử lý bằng cách sử dụng ký hiệu chấm. Ví dụ, một quy tắc như `{ user: z.object({ email: z.string() }) }`{lang="ts"} sẽ được áp dụng cho `<FormField name="user.email">`{lang="vue"}.

### Custom Validation

Sử dụng prop `validate` để áp dụng logic xác thực của riêng bạn.

Hàm xác thực phải trả về một danh sách lỗi với các thuộc tính sau:

- `message` - thông báo lỗi để hiển thị.
- `name` - `name` của `FormField` để gửi lỗi đến.

::tip
Nó có thể được sử dụng cùng với prop `schema` để xử lý các trường hợp phức tạp.
::

::component-example
---
name: 'form-example-basic'
props:
  class: 'w-60'
---
::

### Input Events

Thành phần Form tự động kích hoạt xác thực khi một input phát ra sự kiện `input`, `change`, hoặc `blur`.

- Xác thực trên `input` xảy ra **khi bạn gõ**.
- Xác thực trên `change` xảy ra khi bạn **cam kết với một giá trị**.
- Xác thực trên `blur` xảy ra khi một input **mất focus**.

Bạn có thể kiểm soát khi nào xác thực xảy ra bằng cách sử dụng prop `validate-on`.

::tip
Form luôn xác thực khi submit.
::

::component-example{label="Default"}
---
source: false
name: 'form-example-elements'
options:
  - name: 'validate-on'
    label: 'validate-on'
    items:
    - 'input'
    - 'change'
    - 'blur'
    default:
    - 'input'
    - 'change'
    - 'blur'
    multiple: true
---
::

::tip
Bạn có thể sử dụng composable [`useFormField`](/composables/use-form-field) để triển khai điều này bên trong các thành phần của riêng bạn.
::

### Error Event

Bạn có thể lắng nghe sự kiện `@error` để xử lý lỗi. Sự kiện này được kích hoạt khi form được submit và chứa một mảng các đối tượng `FormError` với các trường sau:

- `id` - `id` của input.
- `name` - `name` của `FormField`
- `message` - thông báo lỗi để hiển thị.

Đây là một ví dụ tập trung vào phần tử input đầu tiên có lỗi sau khi form được submit:

::component-example
---
name: 'form-example-on-error'
collapse: true
props:
  class: 'w-60'
---
::

### Nesting Forms

Lồng các thành phần form cho phép bạn quản lý các cấu trúc dữ liệu phức tạp, chẳng hạn như danh sách hoặc các trường có điều kiện, hiệu quả hơn.

Ví dụ, nó có thể được sử dụng để thêm động các trường dựa trên input của người dùng:
::component-example
---
collapse: true
name: 'form-example-nested'
---
::

Hoặc để xác thực các input danh sách:
::component-example
---
collapse: true
name: 'form-example-nested-list'
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

You can access the typed component instance using [`useTemplateRef`](https://vuejs.org/api/composition-api-helpers.html#usetemplateref).

```vue
<script setup lang="ts">
const form = useTemplateRef('form')
</script>

<template>
  <UForm ref="form" />
</template>
```

This will give you access to the following:

| Name | Type |
| ---- | ---- |
| `submit()`{lang="ts-type"} | `Promise<void>`{lang="ts-type"} <br> <div class="text-toned mt-1"><p>Triggers form submission.</p> |
| `validate(opts: { name?: keyof T \| (keyof T)[], silent?: boolean, nested?: boolean, transform?: boolean })`{lang="ts-type"} | `Promise<T>`{lang="ts-type"} <br> <div class="text-toned mt-1"><p>Triggers form validation. Will raise any errors unless `opts.silent` is set to true.</p> |
| `clear(path?: keyof T | RegExp)`{lang="ts-type"} | `void` <br> <div class="text-toned mt-1"><p>Clears form errors associated with a specific path. If no path is provided, clears all form errors.</p> |
| `getErrors(path?: keyof T | RegExp)`{lang="ts-type"} | `FormError[]`{lang="ts-type"} <br> <div class="text-toned mt-1"><p>Retrieves form errors associated with a specific path. If no path is provided, returns all form errors.</p></div> |
| `setErrors(errors: FormError[], name?: keyof T | RegExp)`{lang="ts-type"} | `void` <br> <div class="text-toned mt-1"><p>Sets form errors for a given path. If no path is provided, overrides all errors.</p> |
| `errors`{lang="ts-type"} | `Ref<FormError[]>`{lang="ts-type"} <br> <div class="text-toned mt-1"><p>A reference to the array containing validation errors. Use this to access or manipulate the error information.</p> |
| `disabled`{lang="ts-type"} | `Ref<boolean>`{lang="ts-type"} |
| `dirty`{lang="ts-type"} | `Ref<boolean>`{lang="ts-type"} `true` if at least one form field has been updated by the user.|
| `dirtyFields`{lang="ts-type"} | `DeepReadonly<Set<keyof T>>`{lang="ts-type"} Tracks fields that have been modified by the user. |
| `touchedFields`{lang="ts-type"} | `DeepReadonly<Set<keyof T>>`{lang="ts-type"} Tracks fields that the user interacted with. |
| `blurredFields`{lang="ts-type"} | `DeepReadonly<Set<keyof T>>`{lang="ts-type"} Tracks fields blurred by the user. |

## Theme

:component-theme

## Changelog

:component-changelog
