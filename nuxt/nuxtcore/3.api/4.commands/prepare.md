---
title: 'nuxt prepare'
description: Lệnh prepare tạo thư mục .nuxt trong ứng dụng của bạn và tạo các loại.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/prepare.ts
    size: xs
---

<!--prepare-cmd-->
```bash [Terminal]
npx nuxt prepare [ROOTDIR] [--dotenv] [--cwd=<directory>] [--logLevel=<silent|info|verbose>] [--envName]
```
<!--/prepare-cmd-->

Lệnh `prepare` tạo thư mục [`.nuxt`](/docs/guide/directory-structure/nuxt) trong ứng dụng của bạn và tạo các loại. Điều này có thể hữu ích trong môi trường CI hoặc như lệnh `postinstall` trong [`package.json`](/docs/guide/directory-structure/package) của bạn.

## Arguments

<!--prepare-args-->
Argument | Description
--- | ---
`ROOTDIR="."` | Chỉ định thư mục làm việc (mặc định: `.`)
<!--/prepare-args-->

## Options

<!--prepare-opts-->
Option | Default | Description
--- | --- | ---
`--dotenv` |  | Đường dẫn đến tệp `.env` để tải, tương đối với thư mục gốc
`--cwd=<directory>` |  | Chỉ định thư mục làm việc, điều này ưu tiên hơn ROOTDIR (mặc định: `.`)
`--logLevel=<silent\|info\|verbose>` |  | Chỉ định cấp độ log thời gian xây dựng
`--envName` |  | Môi trường để sử dụng khi giải quyết ghi đè cấu hình (mặc định là `production` khi xây dựng, và `development` khi chạy máy chủ dev)
<!--/prepare-opts-->
