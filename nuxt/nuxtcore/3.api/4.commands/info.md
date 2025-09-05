---
title: "nuxt info"
description: Lệnh info ghi log thông tin về dự án Nuxt hiện tại hoặc được chỉ định.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/info.ts
    size: xs
---

<!--info-cmd-->
```bash [Terminal]
npx nuxt info [ROOTDIR] [--cwd=<directory>]
```
<!--/info-cmd-->

Lệnh `info` ghi log thông tin về dự án Nuxt hiện tại hoặc được chỉ định.

## Arguments

<!--info-args-->
Argument | Description
--- | ---
`ROOTDIR="."` | Chỉ định thư mục làm việc (mặc định: `.`)
<!--/info-args-->

## Options

<!--info-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` |  | Chỉ định thư mục làm việc, điều này ưu tiên hơn ROOTDIR (mặc định: `.`)
<!--/info-opts-->
