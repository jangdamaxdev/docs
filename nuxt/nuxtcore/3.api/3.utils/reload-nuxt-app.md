---
title: 'reloadNuxtApp'
description: reloadNuxtApp will perform a hard reload of the page.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/chunk.ts
    size: xs
---

::note
`reloadNuxtApp` sẽ thực hiện một hard reload của ứng dụng của bạn, re-request trang và các dependencies từ server.
::

Theo mặc định, nó cũng sẽ lưu `state` hiện tại của ứng dụng của bạn (tức là bất kỳ state nào bạn có thể truy cập với `useState`).

::read-more{to="/docs/guide/going-further/experimental-features#restorestate" icon="i-lucide-star"}
Bạn có thể bật việc khôi phục thử nghiệm của state này bằng cách bật tùy chọn `experimental.restoreState` trong file `nuxt.config` của bạn.
::

## Type

```ts
reloadNuxtApp(options?: ReloadNuxtAppOptions)

interface ReloadNuxtAppOptions {
  ttl?: number
  force?: boolean
  path?: string
  persistState?: boolean
}
```

### `options` (optional)

**Type**: `ReloadNuxtAppOptions`

Một object chấp nhận các thuộc tính sau:

- `path` (optional)

  **Type**: `string`

  **Default**: `window.location.pathname`

  Đường dẫn để reload (mặc định là đường dẫn hiện tại). Nếu khác với vị trí cửa sổ hiện tại, nó sẽ kích hoạt điều hướng và thêm một entry vào lịch sử trình duyệt.

- `ttl` (optional)

  **Type**: `number`

  **Default**: `10000`

  Số mili giây để bỏ qua các yêu cầu reload trong tương lai. Nếu được gọi lại trong khoảng thời gian này, `reloadNuxtApp` sẽ không reload ứng dụng của bạn để tránh vòng lặp reload.

- `force` (optional)

  **Type**: `boolean`

  **Default**: `false`

  Tùy chọn này cho phép bỏ qua hoàn toàn bảo vệ vòng lặp reload, buộc reload ngay cả khi đã xảy ra trong TTL đã chỉ định trước đó.

- `persistState` (optional)

  **Type**: `boolean`

  **Default**: `false`

  Có dump state Nuxt hiện tại vào sessionStorage (như `nuxt:reload:state`) hay không. Theo mặc định, điều này sẽ không có hiệu lực trên reload trừ khi `experimental.restoreState` cũng được đặt, hoặc trừ khi bạn xử lý việc khôi phục state bằng chính mình.
