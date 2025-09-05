---
title: 'updateAppConfig'
description: 'Update the App Config at runtime.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/config.ts
    size: xs
---

::note
Cập nhật [`app.config`](/docs/guide/directory-structure/app-config) bằng cách sử dụng deep assignment. Các thuộc tính (nested) hiện có sẽ được bảo toàn.
::

## Usage

```js
const appConfig = useAppConfig() // { foo: 'bar' }

const newAppConfig = { foo: 'baz' }

updateAppConfig(newAppConfig)

console.log(appConfig) // { foo: 'baz' }
```

:read-more{to="/docs/guide/directory-structure/app-config"}
