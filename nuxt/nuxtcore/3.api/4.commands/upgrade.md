---
title: "nuxt upgrade"
description: Lệnh upgrade nâng cấp Nuxt lên phiên bản mới nhất.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/upgrade.ts
    size: xs
---

<!--upgrade-cmd-->
```bash [Terminal]
npx nuxt upgrade [ROOTDIR] [--cwd=<directory>] [--logLevel=<silent|info|verbose>] [--dedupe] [-f, --force] [-ch, --channel=<stable|nightly>]
```
<!--/upgrade-cmd-->

Lệnh `upgrade` nâng cấp Nuxt lên phiên bản mới nhất.

## Arguments

<!--upgrade-args-->
Argument | Description
--- | ---
`ROOTDIR="."` | Chỉ định thư mục làm việc (mặc định: `.`)
<!--/upgrade-args-->

## Options

<!--upgrade-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` |  | Chỉ định thư mục làm việc, điều này ưu tiên hơn ROOTDIR (mặc định: `.`)
`--logLevel=<silent\|info\|verbose>` |  | Chỉ định cấp độ log thời gian xây dựng
`--dedupe` |  | Sẽ loại bỏ trùng lặp dependencies nhưng không tạo lại lockfile
`-f, --force` |  | Buộc nâng cấp để tạo lại lockfile và node_modules
`-ch, --channel=<stable\|nightly>` | `stable` | Chỉ định kênh để cài đặt từ (mặc định: stable)
<!--/upgrade-opts-->
