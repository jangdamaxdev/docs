---
title: useOverlay
description: 'A composable to programmatically control overlays.'
---

## Usage

Sử dụng composable `useOverlay` được tự động nhập để kiểm soát theo chương trình các thành phần [Modal](/components/modal) và [Slideover](/components/slideover).

```vue
<script setup lang="ts">
import { LazyModalExample } from '#components'

const overlay = useOverlay()

const modal = overlay.create(LazyModalExample)

async function openModal() {
  modal.open()
}
</script>
```

- Composable `useOverlay` được tạo bằng `createSharedComposable`, đảm bảo rằng cùng một trạng thái overlay được chia sẻ trên toàn bộ ứng dụng của bạn.

::note
Để trả về một giá trị từ overlay, `overlay.open().instance` có thể được chờ đợi. Để điều này hoạt động, tuy nhiên, **thành phần overlay phải phát ra một sự kiện `close`**. Xem ví dụ bên dưới để biết chi tiết.
::


## API

### `create(component: T, options: OverlayOptions): OverlayInstance`

Tạo một overlay và trả về một instance factory.

- Parameters:
  - `component`: Thành phần overlay.
  - `options`:
    - `defaultOpen?: boolean` Mở overlay ngay sau khi được tạo. Mặc định là `false`.
    - `props?: ComponentProps`: Một đối tượng tùy chọn của props để truyền cho thành phần được render.
    - `destroyOnClose?: boolean` Loại bỏ overlay khỏi bộ nhớ khi đóng. Mặc định là `false`.

### `open(id: symbol, props?: ComponentProps<T>): OpenedOverlay<T>`

Mở một overlay theo `id` của nó.

- Parameters:
  - `id`: Mã định danh của overlay.
  - `props`: Một đối tượng tùy chọn của props để truyền cho thành phần được render.

### `close(id: symbol, value?: any): void`

Đóng một overlay theo `id` của nó.

- Parameters:
  - `id`: Mã định danh của overlay.
  - `value`: Một giá trị để giải quyết promise overlay.

### `patch(id: symbol, props: ComponentProps<T>): void`

Cập nhật một overlay theo `id` của nó.

- Parameters:
  - `id`: Mã định danh của overlay.
  - `props`: Một đối tượng của props để cập nhật trên thành phần được render.

### `unmount(id: symbol): void`

Loại bỏ một overlay khỏi DOM theo `id` của nó.

- Parameters:
  - `id`: Mã định danh của overlay.

### `isOpen(id: symbol): boolean`

Kiểm tra xem một overlay có mở không bằng `id` của nó.

- Parameters:
  - `id`: Mã định danh của overlay.

### `overlays: Overlay[]`

Danh sách trong bộ nhớ của tất cả các overlay đã được tạo.

## Instance API

### `open(props?: ComponentProps<T>): Promise<OpenedOverlay<T>>`

Mở overlay.

- Parameters:
  - `props`: Một đối tượng tùy chọn của props để truyền cho thành phần được render.

```vue
<script setup lang="ts">
import { LazyModalExample } from '#components'

const overlay = useOverlay()

const modal = overlay.create(LazyModalExample)

function openModal() {
  modal.open({
    title: 'Welcome'
  })
}
</script>
```

### `close(value?: any): void`

Đóng overlay.

- Parameters:
  - `value`: Một giá trị để giải quyết promise overlay.

### `patch(props: ComponentProps<T>)`

Cập nhật props của overlay.

- Parameters:
  - `props`: Một đối tượng của props để cập nhật trên thành phần được render.

```vue
<script setup lang="ts">
import { LazyModalExample } from '#components'

const overlay = useOverlay()

const modal = overlay.create(LazyModalExample, {
  title: 'Welcome'
})

function openModal() {
  modal.open()
}

function updateModalTitle() {
  modal.patch({ title: 'Updated Title' })
}
</script>
```

## Example

Đây là một ví dụ hoàn chỉnh về cách sử dụng composable `useOverlay`:

```vue
<script setup lang="ts">
import { ModalA, ModalB, SlideoverA } from '#components'

const overlay = useOverlay()

// Create with default props
const modalA = overlay.create(ModalA, { title: 'Welcome' })
const modalB = overlay.create(ModalB)

const slideoverA = overlay.create(SlideoverA)

const openModalA = () => {
  // Open modalA, but override the title prop
  modalA.open({ title: 'Hello' })
}

const openModalB = async () => {
  // Open modalB, and wait for its result
  const modalBInstance = modalB.open()

  const input = await modalBInstance

  // Pass the result from modalB to the slideover, and open it
  slideoverA.open({ input })
}
</script>

<template>
  <button @click="openModalA">Open Modal</button>
</template>
```

Trong ví dụ này, chúng ta đang sử dụng composable `useOverlay` để kiểm soát nhiều modal và slideover.

## Caveats

### Provide / Inject

Khi mở overlay theo chương trình (ví dụ: modal, slideover, v.v.), thành phần overlay chỉ có thể truy cập các giá trị được inject từ thành phần chứa `UApp` (thường là `app.vue` hoặc các thành phần layout). Điều này là vì overlay được mount bên ngoài ngữ cảnh trang bởi thành phần `UApp`.

Như vậy, sử dụng `provide()` trong các trang hoặc thành phần cha không được hỗ trợ trực tiếp. Để truyền các giá trị được provide cho overlay, cách tiếp cận được khuyến nghị là sử dụng props thay thế:

```vue
<script setup lang="ts">
import { LazyModalExample } from '#components'

const providedValue = inject('valueProvidedInPage')

const modal = overlay.create(LazyModalExample, {
  props: {
    providedValue,
    otherData: someValue
  }
})
</script>
```