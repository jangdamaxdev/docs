---
title: "nuxt analyze"
description: "Phân tích gói sản xuất hoặc ứng dụng Nuxt của bạn."
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/analyze.ts
    size: xs
---

<!--analyze-cmd-->
```bash [Terminal]
npx nuxt analyze [ROOTDIR] [--cwd=<directory>] [--logLevel=<silent|info|verbose>] [--dotenv] [--name=<name>] [--no-serve]
```
<!--/analyze-cmd-->

Lệnh `analyze` xây dựng Nuxt và phân tích gói sản xuất (thử nghiệm).

## Arguments

<!--analyze-args-->
Argument | Description
--- | ---
`ROOTDIR="."` | Chỉ định thư mục làm việc (mặc định: `.`)
<!--/analyze-args-->

## Options

<!--analyze-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` |  | Chỉ định thư mục làm việc, điều này ưu tiên hơn ROOTDIR (mặc định: `.`)
`--logLevel=<silent\|info\|verbose>` |  | Chỉ định cấp độ log thời gian xây dựng
`--dotenv` |  | Đường dẫn đến tệp `.env` để tải, tương đối với thư mục gốc
`--name=<name>` | `default` | Tên của phân tích
`--no-serve` |  | Bỏ qua phục vụ kết quả phân tích
<!--/analyze-opts-->

::note
Lệnh này đặt `process.env.NODE_ENV` thành `production`.
::
