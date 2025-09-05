---
title: "nuxt module"
description: "Tìm kiếm và thêm module vào ứng dụng Nuxt của bạn với dòng lệnh."
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/module/
    size: xs
---

Nuxt cung cấp một số tiện ích để làm việc với [Nuxt modules](/modules) một cách liền mạch.

## nuxt module add

<!--module-add-cmd-->
```bash [Terminal]
npx nuxt module add <MODULENAME> [--cwd=<directory>] [--logLevel=<silent|info|verbose>] [--skipInstall] [--skipConfig] [--dev]
```
<!--/module-add-cmd-->

<!--module-add-args-->
Argument | Description
--- | ---
`MODULENAME` | Tên module
<!--/module-add-args-->

<!--module-add-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` | `.` | Chỉ định thư mục làm việc
`--logLevel=<silent\|info\|verbose>` |  | Chỉ định cấp độ log thời gian xây dựng
`--skipInstall` |  | Bỏ qua npm install
`--skipConfig` |  | Bỏ qua cập nhật nuxt.config.ts
`--dev` |  | Cài đặt module như dev dependency
<!--/module-add-opts-->

Lệnh cho phép bạn cài đặt [Nuxt modules](/modules) trong ứng dụng của bạn mà không cần công việc thủ công.

Khi chạy lệnh, nó sẽ:

- cài đặt module như một dependency sử dụng trình quản lý gói của bạn
- thêm nó vào tệp [package.json](/docs/guide/directory-structure/package) của bạn
- cập nhật tệp [`nuxt.config`](/docs/guide/directory-structure/nuxt-config) của bạn

**Ví dụ:**

Cài đặt module [`Pinia`](/modules/pinia)

```bash [Terminal]
npx nuxt module add pinia
```

## nuxt module search

<!--module-search-cmd-->
```bash [Terminal]
npx nuxt module search <QUERY> [--cwd=<directory>] [--nuxtVersion=<2|3>]
```
<!--/module-search-cmd-->

### Arguments

<!--module-search-args-->
Argument | Description
--- | ---
`QUERY` | từ khóa để tìm kiếm
<!--/module-search-args-->

### Options

<!--module-search-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` | `.` | Chỉ định thư mục làm việc
`--nuxtVersion=<2\|3>` |  | Lọc theo phiên bản Nuxt và chỉ liệt kê các module tương thích (tự động phát hiện theo mặc định)
<!--/module-search-opts-->

Lệnh tìm kiếm các module Nuxt khớp với truy vấn của bạn mà tương thích với phiên bản Nuxt của bạn.

**Ví dụ:**

```bash [Terminal]
npx nuxt module search pinia
```
