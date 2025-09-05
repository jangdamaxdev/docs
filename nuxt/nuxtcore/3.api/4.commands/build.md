---
title: "nuxt build"
description: "Xây dựng ứng dụng Nuxt của bạn."
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/build.ts
    size: xs
---

<!--build-cmd-->
```bash [Terminal]
npx nuxt build [ROOTDIR] [--cwd=<directory>] [--logLevel=<silent|info|verbose>] [--prerender] [--preset] [--dotenv] [--envName]
```
<!--/build-cmd-->

Lệnh `build` tạo thư mục `.output` với tất cả ứng dụng, máy chủ và dependencies sẵn sàng cho sản xuất.

## Arguments

<!--build-args-->
Argument | Description
--- | ---
`ROOTDIR="."` | Chỉ định thư mục làm việc (mặc định: `.`)
<!--/build-args-->

## Options

<!--build-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` |  | Chỉ định thư mục làm việc, điều này ưu tiên hơn ROOTDIR (mặc định: `.`)
`--logLevel=<silent\|info\|verbose>` |  | Chỉ định cấp độ log thời gian xây dựng
`--prerender` |  | Xây dựng Nuxt và prerender các route tĩnh
`--preset` |  | Preset máy chủ Nitro
`--dotenv` |  | Đường dẫn đến tệp `.env` để tải, tương đối với thư mục gốc
`--envName` |  | Môi trường để sử dụng khi giải quyết ghi đè cấu hình (mặc định là `production` khi xây dựng, và `development` khi chạy máy chủ dev)
<!--/build-opts-->

::note
Lệnh này đặt `process.env.NODE_ENV` thành `production`.
::

::note
`--prerender` sẽ luôn đặt `preset` thành `static`
::
