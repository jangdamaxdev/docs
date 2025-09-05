---
title: 'nuxt build-module'
description: 'Lệnh Nuxt để xây dựng module Nuxt của bạn trước khi xuất bản.'
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/module-builder/blob/main/src/cli.ts
    size: xs
---

<!--build-module-cmd-->
```bash [Terminal]
npx nuxt build-module [ROOTDIR] [--cwd=<directory>] [--logLevel=<silent|info|verbose>] [--build] [--stub] [--sourcemap] [--prepare]
```
<!--/build-module-cmd-->

Lệnh `build-module` chạy `@nuxt/module-builder` để tạo thư mục `dist` trong `rootDir` của bạn chứa bản build đầy đủ cho **nuxt-module** của bạn.

## Arguments

<!--build-module-args-->
Argument | Description
--- | ---
`ROOTDIR="."` | Chỉ định thư mục làm việc (mặc định: `.`)
<!--/build-module-args-->

## Options

<!--build-module-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` |  | Chỉ định thư mục làm việc, điều này ưu tiên hơn ROOTDIR (mặc định: `.`)
`--logLevel=<silent\|info\|verbose>` |  | Chỉ định cấp độ log thời gian xây dựng
`--build` | `false` | Xây dựng module để phân phối
`--stub` | `false` | Stub dist thay vì thực sự xây dựng nó cho phát triển
`--sourcemap` | `false` | Tạo sourcemaps
`--prepare` | `false` | Chuẩn bị module cho phát triển cục bộ
<!--/build-module-opts-->

::read-more{to="https://github.com/nuxt/module-builder" icon="i-simple-icons-github" target="\_blank"}
Đọc thêm về `@nuxt/module-builder`.
::
