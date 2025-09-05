---
title: Calendar
description: Một thành phần lịch để chọn ngày đơn lẻ, nhiều ngày hoặc phạm vi ngày.
category: element
links:
  - label: Calendar
    icon: i-custom-reka-ui
    to: https://reka-ui.com/docs/components/calendar
  - label: GitHub
    icon: i-simple-icons-github
    to: https://github.com/nuxt/ui/tree/v3/src/runtime/components/Calendar.vue
---

::note
Thành phần này dựa vào gói [`@internationalized/date`](https://react-spectrum.adobe.com/internationalized/date/index.html) cung cấp các đối tượng và hàm để biểu diễn và thao tác ngày tháng theo cách nhận biết ngôn ngữ.
::

## Usage

Sử dụng chỉ thị `v-model` để kiểm soát ngày đã chọn.

::component-code
---
cast:
  modelValue: DateValue
ignore:
  - modelValue
external:
  - modelValue
props:
  modelValue: [2022, 2, 3]
---
::

Sử dụng prop `default-value` để đặt giá trị ban đầu khi bạn không cần kiểm soát trạng thái của nó.

::component-code
---
cast:
  defaultValue: DateValue
ignore:
  - defaultValue
external:
  - defaultValue
props:
  defaultValue: [2022, 2, 6]
---
::

### Multiple

Sử dụng prop `multiple` để cho phép chọn nhiều.

::component-code
---
prettier: true
cast:
  modelValue: DateValue[]
ignore:
  - multiple
  - modelValue
external:
  - modelValue
props:
  multiple: true
  modelValue: [[2022, 2, 4], [2022, 2, 6], [2022, 2, 8]]
---
::

### Range

Sử dụng prop `range` để chọn một phạm vi ngày.

::component-code
---
prettier: true
cast:
  modelValue: DateRange
ignore:
  - range
  - modelValue.start
  - modelValue.end
external:
  - modelValue
props:
  range: true
  modelValue:
    start: [2022, 2, 3]
    end: [2022, 2, 20]
---
::

### Color

Sử dụng prop `color` để thay đổi màu của lịch.

::component-code
---
props:
  color: neutral
---
::

### Size

Sử dụng prop `size` để thay đổi kích thước của lịch.

::component-code
---
props:
  size: xl
---
::

### Disabled

Sử dụng prop `disabled` để vô hiệu hóa lịch.

::component-code
---
props:
  disabled: true
---
::

### Number Of Months

Sử dụng prop `numberOfMonths` để thay đổi số tháng trong lịch.

::component-code
---
props:
  numberOfMonths: 3
---
::

### Month Controls

Sử dụng prop `month-controls` để hiển thị các điều khiển tháng. Mặc định là `true`.

::component-code
---
props:
  monthControls: false
---
::

### Year Controls

Sử dụng prop `year-controls` để hiển thị các điều khiển năm. Mặc định là `true`.

::component-code
---
props:
  yearControls: false
---
::

### Fixed Weeks

Sử dụng prop `fixed-weeks` để hiển thị lịch với tuần cố định.

::component-code
---
props:
  fixedWeeks: false
---
::

## Examples

### With chip events

Sử dụng thành phần [Chip](/components/chip) để thêm sự kiện vào các ngày cụ thể.

::component-example
---
name: 'calendar-events-example'
---
::

### With disabled dates

Sử dụng prop `is-date-disabled` với một hàm để đánh dấu các ngày cụ thể là bị vô hiệu hóa.

::component-example
---
name: 'calendar-disabled-dates-example'
---
::

### With unavailable dates

Sử dụng prop `is-date-unavailable` với một hàm để đánh dấu các ngày cụ thể là không khả dụng.

::component-example
---
name: 'calendar-unavailable-dates-example'
---
::

### With min/max dates

Sử dụng các prop `min-value` và `max-value` để giới hạn các ngày.

::component-example
---
name: 'calendar-min-max-dates-example'
---
::

### With other calendar systems

Bạn có thể sử dụng các lịch khác từ `@internationalized/date` để triển khai hệ thống lịch khác. 

::component-example
---
name: 'calendar-other-system-example'
---
::

::note{to="https://react-spectrum.adobe.com/internationalized/date/Calendar.html#implementations"}
Bạn có thể kiểm tra tất cả các lịch khả dụng trên tài liệu `@internationalized/date`.
::

### With external controls

Bạn có thể kiểm soát lịch với các điều khiển bên ngoài bằng cách thao tác ngày được truyền trong `v-model`.

::component-example
---
name: 'calendar-external-controls-example'
---
::

### As a DatePicker

Sử dụng thành phần [Button](/components/button) và [Popover](/components/popover) để tạo một bộ chọn ngày.

::component-example
---
name: 'calendar-date-picker-example'
---
::

### As a DateRangePicker

Sử dụng thành phần [Button](/components/button) và [Popover](/components/popover) để tạo một bộ chọn phạm vi ngày.

::component-example
---
name: 'calendar-date-range-picker-example'
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
