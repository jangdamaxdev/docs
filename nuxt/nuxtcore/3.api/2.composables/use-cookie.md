---
title: 'useCookie'
description: useCookie là một composable thân thiện với SSR để đọc và ghi cookies.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/cookie.ts
    size: xs
---

## Usage

Trong các pages, components và plugins của bạn, bạn có thể sử dụng `useCookie` để đọc và ghi cookies trong một cách thân thiện với SSR.

```ts
const cookie = useCookie(name, options)
```

::note
`useCookie` chỉ hoạt động trong [Nuxt context](/docs/guide/going-further/nuxt-app#the-nuxt-context).
::

::tip
Ref được trả về sẽ tự động serialize và deserialize cookie values thành JSON.
::

## Type

```ts [Signature]
import type { Ref } from 'vue'
import type { CookieParseOptions, CookieSerializeOptions } from 'cookie-es'

export interface CookieOptions<T = any> extends Omit<CookieSerializeOptions & CookieParseOptions, 'decode' | 'encode'> {
  decode?(value: string): T
  encode?(value: T): string
  default?: () => T | Ref<T>
  watch?: boolean | 'shallow'
  readonly?: boolean
}

export interface CookieRef<T> extends Ref<T> {}

export function useCookie<T = string | null | undefined>(
  name: string,
  options?: CookieOptions<T>
): CookieRef<T>
```

## Parameters

`name`: Tên của cookie.

`options`: Options để control cookie behavior. Object có thể có các properties sau:

Hầu hết options sẽ được pass trực tiếp đến package [cookie](https://github.com/jshttp/cookie).

| Property | Type | Default | Description |
| --- | --- | --- | --- |
| `decode` | `(value: string) => T` | `decodeURIComponent` + [destr](https://github.com/unjs/destr). | Custom function để decode cookie value.  Vì giá trị của cookie có limited character set (và phải là simple string), function này có thể được sử dụng để decode một previously encoded cookie value thành JavaScript string hoặc object khác. <br/> **Lưu ý:** Nếu error được throw từ function này, original, non-decoded cookie value sẽ được trả về như cookie's value. |
| `encode` | `(value: T) => string` | `JSON.stringify` + `encodeURIComponent` | Custom function để encode cookie value. Vì giá trị của cookie có limited character set (và phải là simple string), function này có thể được sử dụng để encode một value thành string suited cho cookie's value. |
| `default` | `() => T \| Ref<T>` | `undefined` | Function returning giá trị mặc định nếu cookie không tồn tại.  Function cũng có thể return một `Ref`. |
| `watch` | `boolean \| 'shallow'` | `true`  | Có watch cho changes và update cookie hay không. `true` cho deep watch, `'shallow'` cho shallow watch, tức là data changes chỉ cho top level properties, `false` để disable. <br/> **Lưu ý:** Refresh `useCookie` values manually khi một cookie đã changed với [`refreshCookie`](/docs/api/utils/refresh-cookie). |
| `readonly` | `boolean` | `false` | Nếu `true`, disables writing to cookie. |
| `maxAge` | `number` | `undefined` | Max age in seconds cho cookie, tức là giá trị cho [`Max-Age` `Set-Cookie` attribute](https://tools.ietf.org/html/rfc6265#section-5.2.2). Số given sẽ được converted to integer bằng rounding down. Theo mặc định, no maximum age được set. |
| `expires` | `Date` | `undefined` | Expiration date cho cookie. Theo mặc định, no expiration được set. Hầu hết clients sẽ consider this a "non-persistent cookie" và sẽ delete nó on a condition như exiting a web browser application. <br/> **Lưu ý:** [cookie storage model specification](https://tools.ietf.org/html/rfc6265#section-5.3) states rằng nếu cả `expires` và `maxAge` được set, thì `maxAge` takes precedence, nhưng không phải tất cả clients obey this, vì vậy nếu cả hai được set, chúng nên point to cùng date và time! <br/>Nếu không `expires` và `maxAge` được set, cookie sẽ session-only và removed khi user closes browser của họ. |
| `httpOnly` | `boolean` | `false` | Sets HttpOnly attribute. <br/> **Lưu ý:** Cẩn thận khi setting this thành `true`, vì compliant clients sẽ không allow client-side JavaScript để see cookie in `document.cookie`. |
| `secure` | `boolean` | `false` | Sets [`Secure` `Set-Cookie` attribute](https://tools.ietf.org/html/rfc6265#section-5.2.5). <br/>**Lưu ý:** Cẩn thận khi setting this thành `true`, vì compliant clients sẽ không send cookie back to server trong future nếu browser không có HTTPS connection. Điều này có thể lead to hydration errors. |
| `partitioned` | `boolean` | `false` | Sets [`Partitioned` `Set-Cookie` attribute](https://datatracker.ietf.org/doc/html/draft-cutler-httpbis-partitioned-cookies#section-2.1). <br/>**Lưu ý:** Đây là một attribute chưa được fully standardized, và có thể change trong future. <br/>Điều này cũng có nghĩa là nhiều clients có thể ignore attribute này cho đến khi họ understand nó.<br/>Thông tin thêm có thể được tìm thấy trong [proposal](https://github.com/privacycg/CHIPS). |
| `domain` | `string` | `undefined` | Sets [`Domain` `Set-Cookie` attribute](https://tools.ietf.org/html/rfc6265#section-5.2.3). Theo mặc định, no domain được set, và hầu hết clients sẽ consider applying cookie chỉ to current domain. |
| `path` | `string` | `'/'` | Sets [`Path` `Set-Cookie` attribute](https://tools.ietf.org/html/rfc6265#section-5.2.4). Theo mặc định, path được considered ["default path"](https://tools.ietf.org/html/rfc6265#section-5.1.4). |
| `sameSite` | `boolean \| string` | `undefined` | Sets [`SameSite` `Set-Cookie` attribute](https://tools.ietf.org/html/draft-ietf-httpbis-rfc6265bis-03#section-4.1.2.7). <br/>- `true` sẽ set `SameSite` attribute thành `Strict` cho strict same-site enforcement.<br/>- `false` sẽ không set `SameSite` attribute.<br/>- `'lax'` sẽ set `SameSite` attribute thành `Lax` cho lax same-site enforcement.<br/>- `'none'` sẽ set `SameSite` attribute thành `None` cho một explicit cross-site cookie.<br/>- `'strict'` sẽ set `SameSite` attribute thành `Strict` cho strict same-site enforcement. |

## Return Values

Trả về một Vue `Ref<T>` representing cookie value. Updating ref sẽ update cookie (trừ khi `readonly` được set). Ref là SSR-friendly và sẽ work on cả client và server.

## Examples

### Basic Usage

Ví dụ dưới đây tạo một cookie gọi là `counter`. Nếu cookie không tồn tại, nó được initially set thành một random value. Bất cứ khi nào chúng ta update biến `counter`, cookie sẽ được update accordingly.

```vue [app.vue]
<script setup lang="ts">
const counter = useCookie('counter')

counter.value = counter.value || Math.round(Math.random() * 1000)
</script>

<template>
  <div>
    <h1>Counter: {{ counter || '-' }}</h1>
    <button @click="counter = null">reset</button>
    <button @click="counter--">-</button>
    <button @click="counter++">+</button>
  </div>
</template>
```

### Readonly Cookies

```vue
<script setup lang="ts">
const user = useCookie(
  'userInfo',
  {
    default: () => ({ score: -1 }),
    watch: false
  }
)

if (user.value) {
  // cookie `userInfo` thực tế sẽ không được updated
  user.value.score++
}
</script>

<template>
  <div>User score: {{ user?.score }}</div>
</template>
```

### Writable Cookies

```vue
<script setup lang="ts">
const list = useCookie(
  'list',
  {
    default: () => [],
    watch: 'shallow'
  }
)

function add() {
  list.value?.push(Math.round(Math.random() * 1000))
  // cookie list sẽ không được updated với change này
}

function save() {
  if (list.value) {
    // cookie `list` thực tế sẽ được updated
    list.value = [...list.value]
  }
}
</script>

<template>
  <div>
    <h1>List</h1>
    <pre>{{ list }}</pre>
    <button @click="add">Add</button>
    <button @click="save">Save</button>
  </div>
</template>
```

### Cookies in API Routes

Bạn có thể sử dụng `getCookie` và `setCookie` từ package [`h3`](https://github.com/h3js/h3) để set cookies trong server API routes.

```ts [server/api/counter.ts]
export default defineEventHandler(event => {
  // Read counter cookie
  let counter = getCookie(event, 'counter') || 0

  // Increase counter cookie by 1
  setCookie(event, 'counter', ++counter)

  // Send JSON response
  return { counter }
})
```

:link-example{to="/docs/examples/advanced/use-cookie"}
