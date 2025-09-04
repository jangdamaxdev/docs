---
title: "useState"
description: "Composable useState tạo ra một shared state reactive và SSR-friendly."
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/state.ts
    size: xs
---

## Usage

```ts
// Create a reactive state and set default value
const count = useState('counter', () => Math.round(Math.random() * 100))
```

:read-more{to="/docs/getting-started/state-management"}

::important
Vì data bên trong `useState` sẽ được serialize thành JSON, điều quan trọng là nó không chứa bất kỳ thứ gì không thể serialize, chẳng hạn như classes, functions hoặc symbols.
::

::warning
`useState` là một tên hàm reserved được transform bởi compiler, vì vậy bạn không nên đặt tên hàm riêng của bạn là `useState`.
::

:video-accordion{title="Watch a video from Alexander Lichter about why and when to use useState" videoId="mv0WcBABcIk"}

## Using `shallowRef`

Nếu bạn không cần state của bạn reactive deeply, bạn có thể kết hợp `useState` với [`shallowRef`](https://vuejs.org/api/reactivity-advanced.html#shallowref). Điều này có thể cải thiện performance khi state của bạn chứa large objects và arrays.

```ts
const state = useState('my-shallow-state', () => shallowRef({ deep: 'not reactive' }))
// isShallow(state) === true
```

## Type

```ts
useState<T>(init?: () => T | Ref<T>): Ref<T>
useState<T>(key: string, init?: () => T | Ref<T>): Ref<T>
```

- `key`: Một key duy nhất đảm bảo rằng data fetching được de-duplicate đúng cách trên các requests. Nếu bạn không cung cấp key, thì một key duy nhất với file và line number của instance [`useState`](/docs/api/composables/use-state) sẽ được generate cho bạn.
- `init`: Một hàm cung cấp giá trị ban đầu cho state khi không được initiated. Hàm này cũng có thể trả về một `Ref`.
- `T`: (chỉ typescript) Chỉ định type của state
