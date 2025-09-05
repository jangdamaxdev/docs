---
title: "nuxt typecheck"
description: Lệnh typecheck chạy vue-tsc để kiểm tra các loại trong toàn bộ ứng dụng của bạn.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/typecheck.ts
    size: xs
---

<!--typecheck-cmd-->
```bash [Terminal]
npx nuxt typecheck [ROOTDIR] [--cwd=<directory>] [--logLevel=<silent|info|verbose>]
```
<!--/typecheck-cmd-->

Lệnh `typecheck` chạy [`vue-tsc`](https://github.com/vuejs/language-tools/tree/master/packages/tsc) để kiểm tra các loại trong toàn bộ ứng dụng của bạn.

## Arguments

<!--typecheck-args-->
Argument | Description
--- | ---
`ROOTDIR="."` | Chỉ định thư mục làm việc (mặc định: `.`)
<!--/typecheck-args-->

## Options

<!--typecheck-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` |  | Chỉ định thư mục làm việc, điều này ưu tiên hơn ROOTDIR (mặc định: `.`)
`--logLevel=<silent\|info\|verbose>` |  | Chỉ định cấp độ log thời gian xây dựng
<!--/typecheck-opts-->

::note
Lệnh này đặt `process.env.NODE_ENV` thành `production`. Để ghi đè, định nghĩa `NODE_ENV` trong tệp [`.env`](/docs/guide/directory-structure/env) hoặc như đối số dòng lệnh.
::

::read-more{to="/docs/guide/concepts/typescript#type-checking"}
Đọc thêm về cách bật kiểm tra loại tại thời gian xây dựng hoặc phát triển.
::
