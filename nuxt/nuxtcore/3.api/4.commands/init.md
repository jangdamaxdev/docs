---
title: "create nuxt"
description: Lệnh init khởi tạo một dự án Nuxt mới.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/init.ts
    size: xs
---

<!--init-cmd-->
```bash [Terminal]
npm create nuxt@latest [DIR] [--cwd=<directory>] [-t, --template] [-f, --force] [--offline] [--preferOffline] [--no-install] [--gitInit] [--shell] [--packageManager] [--nightly]
```
<!--/init-cmd-->

Lệnh `create-nuxt` khởi tạo một dự án Nuxt mới sử dụng [unjs/giget](https://github.com/unjs/giget).

## Arguments

<!--init-args-->
Argument | Description
--- | ---
`DIR=""` | Thư mục dự án
<!--/init-args-->

## Options

<!--init-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` | `.` | Chỉ định thư mục làm việc
`-t, --template` |  | Tên mẫu
`-f, --force` |  | Ghi đè thư mục hiện có
`--offline` |  | Buộc chế độ offline
`--preferOffline` |  | Ưu tiên chế độ offline
`--no-install` |  | Bỏ qua cài đặt dependencies
`--gitInit` |  | Khởi tạo kho git
`--shell` |  | Khởi động shell sau cài đặt trong thư mục dự án
`--packageManager` |  | Lựa chọn trình quản lý gói (npm, pnpm, yarn, bun)
`--modules` |  | Các module Nuxt để cài đặt (phân tách bằng dấu phẩy không có khoảng trắng)
`--no-modules` |  | Bỏ qua lời nhắc cài đặt module
`--nightly` |  | Sử dụng kênh phát hành nightly của Nuxt (3x hoặc latest)
<!--/init-opts-->

## Environment variables

- `NUXI_INIT_REGISTRY`: Đặt thành registry mẫu tùy chỉnh. ([tìm hiểu thêm](https://github.com/unjs/giget#custom-registry)).
  - Registry mặc định được tải từ [nuxt/starter/templates](https://github.com/nuxt/starter/tree/templates/templates)
