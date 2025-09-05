---
title: "defineNuxtPlugin"
description: defineNuxtPlugin() là một hàm trợ giúp để tạo các plugin Nuxt.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/nuxt.ts
    size: xs
---

`defineNuxtPlugin` là một hàm trợ giúp để tạo các plugin Nuxt với chức năng nâng cao và an toàn kiểu. Tiện ích này chuẩn hóa các định dạng plugin khác nhau thành một cấu trúc nhất quán hoạt động liền mạch trong hệ thống plugin của Nuxt.

```ts twoslash [plugins/hello.ts]
export default defineNuxtPlugin((nuxtApp) => {
  // Doing something with nuxtApp
})
```

:read-more{to="/docs/guide/directory-structure/plugins#creating-plugins"}

## Type

```ts
defineNuxtPlugin<T extends Record<string, unknown>>(plugin: Plugin<T> | ObjectPlugin<T>): Plugin<T> & ObjectPlugin<T>

type Plugin<T> = (nuxt: [NuxtApp](/docs/guide/going-further/internals#the-nuxtapp-interface)) => Promise<void> | Promise<{ provide?: T }> | void | { provide?: T }

interface ObjectPlugin<T> {
  name?: string
  enforce?: 'pre' | 'default' | 'post'
  dependsOn?: string[]
  order?: number
  parallel?: boolean
  setup?: Plugin<T>
  hooks?: Partial<[RuntimeNuxtHooks](/docs/api/advanced/hooks#app-hooks-runtime)>
  env?: {
    islands?: boolean
  }
}
```

## Parameters

**plugin**: Một plugin có thể được định nghĩa theo hai cách:

1. **Function Plugin**: Một hàm nhận instance [`NuxtApp`](/docs/guide/going-further/internals#the-nuxtapp-interface) và có thể trả về một promise với một đối tượng tiềm năng có thuộc tính [`provide`](/docs/guide/directory-structure/plugins#providing-helpers) nếu bạn muốn cung cấp một trợ giúp trên instance [`NuxtApp`](/docs/guide/going-further/internals#the-nuxtapp-interface).

2. **Object Plugin**: Một đối tượng có thể bao gồm các thuộc tính khác nhau để cấu hình hành vi của plugin, chẳng hạn như `name`, `enforce`, `dependsOn`, `order`, `parallel`, `setup`, `hooks`, và `env`.

| Property           | Type                                                                 | Required | Description                                                                                                     |
| ------------------ | -------------------------------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------- |
| `name` | `string` | `false` | Tên tùy chọn cho plugin, hữu ích cho việc gỡ lỗi và quản lý phụ thuộc. |
| `enforce` | `'pre'` \| `'default'` \| `'post'` | `false` | Kiểm soát khi plugin chạy tương đối với các plugin khác. |
| `dependsOn` | `string[]` | `false` | Mảng tên plugin mà plugin này phụ thuộc vào. Đảm bảo thứ tự thực thi đúng. |
| `order` | `number` | `false` | Điều này cho phép kiểm soát chi tiết hơn về thứ tự plugin và chỉ nên được sử dụng bởi người dùng nâng cao. **Nó ghi đè giá trị của `enforce` và được sử dụng để sắp xếp plugin.** |
| `parallel` | `boolean` | `false` | Có thực thi plugin song song với các plugin song song khác hay không. |
| `setup` | `Plugin<T>`{lang="ts"}  | `false` | Hàm plugin chính, tương đương với một function plugin. |
| `hooks` | `Partial<RuntimeNuxtHooks>`{lang="ts"}  | `false` | Các hook runtime ứng dụng Nuxt để đăng ký trực tiếp. |
| `env` | `{ islands?: boolean }`{lang="ts"}  | `false` | Đặt giá trị này thành `false` nếu bạn không muốn plugin chạy khi kết xuất chỉ máy chủ hoặc các thành phần island. |

:video-accordion{title="Watch a video from Alexander Lichter about the Object Syntax for Nuxt plugins" videoId="2aXZyXB1QGQ"}

## Examples

### Basic Usage

Ví dụ dưới đây minh họa một plugin đơn giản thêm chức năng toàn cầu:

```ts twoslash [plugins/hello.ts]
export default defineNuxtPlugin((nuxtApp) => {
  // Add a global method
  return {
    provide: {
      hello: (name: string) => `Hello ${name}!`
    }
  }
})
```

### Object Syntax Plugin

Ví dụ dưới đây cho thấy cú pháp đối tượng với cấu hình nâng cao:

```ts twoslash [plugins/advanced.ts]
export default defineNuxtPlugin({
  name: 'my-plugin',
  enforce: 'pre',
  async setup (nuxtApp) {
    // Plugin setup logic
    const data = await $fetch('/api/config')
    
    return {
      provide: {
        config: data
      }
    }
  },
  hooks: {
    'app:created'() {
      console.log('App created!')
    }
  },
})
```
