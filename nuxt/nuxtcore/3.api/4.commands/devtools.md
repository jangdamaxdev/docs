---
title: "nuxt devtools"
description: Lệnh devtools cho phép bạn bật hoặc tắt Nuxt DevTools trên cơ sở từng dự án.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/devtools.ts
    size: xs
---

<!--devtools-cmd-->
```bash [Terminal]
npx nuxt devtools <COMMAND> [ROOTDIR] [--cwd=<directory>]
```
<!--/devtools-cmd-->

Chạy `nuxt devtools enable` sẽ cài đặt Nuxt DevTools toàn cầu, và cũng bật nó trong dự án cụ thể bạn đang sử dụng. Nó được lưu như một tùy chọn trong `.nuxtrc` cấp người dùng của bạn. Nếu bạn muốn xóa hỗ trợ devtools cho một dự án cụ thể, bạn có thể chạy `nuxt devtools disable`.

## Arguments

<!--devtools-args-->
Argument | Description
--- | ---
`COMMAND` | Lệnh để chạy (tùy chọn: <enable\|disable>)
`ROOTDIR="."` | Chỉ định thư mục làm việc (mặc định: `.`)
<!--/devtools-args-->

## Options

<!--devtools-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` |  | Chỉ định thư mục làm việc, điều này ưu tiên hơn ROOTDIR (mặc định: `.`)
<!--/devtools-opts-->

::read-more{icon="i-simple-icons-nuxtdotjs" to="https://devtools.nuxt.com" target="\_blank"}
Đọc thêm về **Nuxt DevTools**.
::
