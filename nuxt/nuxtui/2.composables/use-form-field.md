---
title: useFormField
description: 'A composable to integrate custom inputs with the Form component'
navigation: false
---

## Usage

Sử dụng composable `useFormField` được tự động nhập để tích hợp các đầu vào tùy chỉnh với một [Form](/components/form).

```vue
<script setup lang="ts">
const { id, emitFormBlur, emitFormInput, emitFormChange } = useFormField()
</script>
```
