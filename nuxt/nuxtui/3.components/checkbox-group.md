---
title: CheckboxGroup
description: Một tập hợp các nút danh sách kiểm tra để chọn nhiều tùy chọn từ danh sách.
category: form
links:
  - label: CheckboxGroup
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/checkbox#group-root
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/CheckboxGroup.vue
---


## Usage

Sử dụng chỉ thị `v-model` để kiểm soát giá trị của CheckboxGroup hoặc prop `default-value` để đặt giá trị ban đầu khi bạn không cần kiểm soát trạng thái của nó.

### Items

Sử dụng prop `items` dưới dạng mảng các chuỗi hoặc số:

::component-code
---
prettier: true
ignore:
  - modelValue
  - items
external:
  - items
  - modelValue
externalTypes:
  - CheckboxGroupItem[]
  - CheckboxGroupValue[]
props:
  modelValue:
    - 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

Bạn cũng có thể truyền một mảng các đối tượng với các thuộc tính sau:

- `label?: string`{lang="ts-type"}
- `description?: string`{lang="ts-type"}
- [`value?: string`{lang="ts-type"}](#value-key)
- `disabled?: boolean`{lang="ts-type"}
- `class?: any`{lang="ts-type"}
- `ui?: { item?: ClassNameValue, container?: ClassNameValue, base?: ClassNameValue, 'indicator'?: ClassNameValue, icon?: ClassNameValue, wrapper?: ClassNameValue, label?: ClassNameValue, description?: ClassNameValue }`{lang="ts-type"}

::component-code
---
ignore:
  - modelValue
  - items
external:
  - items
  - modelValue
externalTypes:
  - CheckboxGroupItem[]
  - CheckboxGroupValue[]
props:
  modelValue:
    - 'system'
  items:
    - label: 'System'
      description: 'This is the first option.'
      value: 'system'
    - label: 'Light'
      description: 'This is the second option.'
      value: 'light'
    - label: 'Dark'
      description: 'This is the third option.'
      value: 'dark'
---
::

::caution
Khi sử dụng đối tượng, bạn cần tham chiếu thuộc tính `value` của đối tượng trong chỉ thị `v-model` hoặc prop `default-value`.
::

### Value Key

Bạn có thể thay đổi thuộc tính được sử dụng để đặt giá trị bằng cách sử dụng prop `value-key`. Mặc định là `value`.

::component-code
---
ignore:
  - modelValue
  - items
  - valueKey
external:
  - items
  - modelValue
externalTypes:
  - CheckboxGroupItem[]
  - CheckboxGroupValue[]
props:
  modelValue:
    - 'light'
  valueKey: 'id'
  items:
    - label: 'System'
      description: 'This is the first option.'
      id: 'system'
    - label: 'Light'
      description: 'This is the second option.'
      id: 'light'
    - label: 'Dark'
      description: 'This is the third option.'
      id: 'dark'
---
::

### Legend

Sử dụng prop `legend` để đặt chú thích của CheckboxGroup.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - CheckboxGroupItem[]
props:
  legend: 'Theme'
  defaultValue:
    - 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

### Color

Sử dụng prop `color` để thay đổi màu sắc của CheckboxGroup.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - CheckboxGroupItem[]
items:
  color:
    - primary
    - secondary
    - success
    - info
    - warning
    - error
    - neutral
props:
  color: neutral
  defaultValue:
    - 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

### Variant

Sử dụng prop `variant` để thay đổi biến thể của CheckboxGroup.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - CheckboxGroupItem[]
items:
  color:
    - primary
    - secondary
    - success
    - info
    - warning
    - error
    - neutral
  variant:
    - list
    - card
    - table
props:
  color: 'primary'
  variant: 'card'
  defaultValue:
    - 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của CheckboxGroup.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - CheckboxGroupItem[]
items:
  variant:
    - list
    - card
    - table
props:
  size: 'xl'
  variant: 'list'
  defaultValue:
    - 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

### Orientation

Sử dụng prop `orientation` để thay đổi hướng của CheckboxGroup. Mặc định là `vertical`.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - CheckboxGroupItem[]
items:
  variant:
    - list
    - card
    - table
props:
  orientation: 'horizontal'
  variant: 'list'
  defaultValue:
    - 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

### Indicator

Sử dụng prop `indicator` để thay đổi vị trí hoặc ẩn chỉ báo. Mặc định là `start`.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - CheckboxGroupItem[]
items:
  indicator:
    - start
    - end
    - hidden
  variant:
    - list
    - card
    - table
props:
  indicator: 'end'
  variant: 'card'
  defaultValue:
    - 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa CheckboxGroup.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - CheckboxGroupItem[]
props:
  disabled: true
  defaultValue:
    - 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
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
