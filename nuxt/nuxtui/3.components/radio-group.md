---
title: RadioGroup
description: Một set of radio buttons để select a single option từ a list.
category: form
links:
  - label: RadioGroup
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/radio-group
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/RadioGroup.vue
---

## Usage

Sử dụng directive `v-model` để kiểm soát value của RadioGroup hoặc prop `default-value` để đặt initial value khi bạn không cần kiểm soát state của nó.

### Items

Sử dụng prop `items` như một mảng of strings hoặc numbers:

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
  - RadioGroupItem[]
  - RadioGroupValue
props:
  modelValue: 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

Bạn cũng có thể truyền một mảng of objects với các thuộc tính sau:

- `label?: string`{lang="ts-type"}
- `description?: string`{lang="ts-type"}
- [`value?: string`{lang="ts-type"}](#value-key)
- `disabled?: boolean`{lang="ts-type"}
- `class?: any`{lang="ts-type"}
- `ui?: { item?: ClassNameValue, container?: ClassNameValue, base?: ClassNameValue, 'indicator'?: ClassNameValue, wrapper?: ClassNameValue, label?: ClassNameValue, description?: ClassNameValue }`{lang="ts-type"}

::component-code
---
ignore:
  - modelValue
  - items
external:
  - items
  - modelValue
externalTypes:
  - RadioGroupItem[]
  - RadioGroupValue
props:
  modelValue: 'system'
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
Khi sử dụng objects, bạn cần reference thuộc tính `value` của object trong directive `v-model` hoặc prop `default-value`.
::

### Value Key

Bạn có thể thay đổi property được sử dụng để set value bằng cách sử dụng prop `value-key`. Mặc định là `value`.

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
  - RadioGroupItem[]
  - RadioGroupValue
props:
  modelValue: 'light'
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

Sử dụng prop `legend` để đặt legend của RadioGroup.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - RadioGroupItem[]
props:
  legend: 'Theme'
  defaultValue: 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

### Color

Sử dụng prop `color` để thay đổi color của RadioGroup.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - RadioGroupItem[]
props:
  color: neutral
  defaultValue: 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

### Variant

Sử dụng prop `variant` để thay đổi variant của RadioGroup.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - RadioGroupItem[]
props:
  color: 'primary'
  variant: 'table'
  defaultValue: 'pro'
  items:
    - label: 'Pro'
      value: 'pro'
      description: 'Tailored for indie hackers, freelancers and solo founders.'
    - label: 'Startup'
      value: 'startup'
      description: 'Best suited for small teams, startups and agencies.'
    - label: 'Enterprise'
      value: 'enterprise'
      description: 'Ideal for larger teams and organizations.'
---
::

### Size

Sử dụng prop `size` để thay đổi size của RadioGroup.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - RadioGroupItem[]
props:
  size: 'xl'
  variant: 'list'
  defaultValue: 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

### Orientation

Sử dụng prop `orientation` để thay đổi orientation của RadioGroup. Mặc định là `vertical`.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - RadioGroupItem[]
props:
  orientation: 'horizontal'
  variant: 'list'
  defaultValue: 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

### Indicator

Sử dụng prop `indicator` để thay đổi position hoặc hide indicator. Mặc định là `start`.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - RadioGroupItem[]
props:
  indicator: 'end'
  variant: 'card'
  defaultValue: 'System'
  items:
    - 'System'
    - 'Light'
    - 'Dark'
---
::

### Disabled

Sử dụng prop `disabled` để disable RadioGroup.

::component-code
---
prettier: true
ignore:
  - defaultValue
  - items
external:
  - items
externalTypes:
  - RadioGroupItem[]
props:
  disabled: true
  defaultValue: 'System'
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