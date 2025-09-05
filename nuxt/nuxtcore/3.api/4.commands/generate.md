---
title: "nuxt generate"
description: Pre-render mọi route của ứng dụng và lưu kết quả trong các tệp HTML thuần.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/generate.ts
    size: xs
---

<!--generate-cmd-->
```bash [Terminal]
npx nuxt generate [ROOTDIR] [--cwd=<directory>] [--logLevel=<silent|info|verbose>] [--preset] [--dotenv] [--envName]
```
<!--/generate-cmd-->

Lệnh `generate` pre-render mọi route của ứng dụng của bạn và lưu kết quả trong các tệp HTML thuần mà bạn có thể triển khai trên bất kỳ dịch vụ hosting tĩnh nào. Lệnh kích hoạt lệnh `nuxt build` với đối số `prerender` được đặt thành `true`

## Arguments

<!--generate-args-->
Argument | Description
--- | ---
`ROOTDIR="."` | Chỉ định thư mục làm việc (mặc định: `.`)
<!--/generate-args-->

## Options

<!--generate-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` |  | Chỉ định thư mục làm việc, điều này ưu tiên hơn ROOTDIR (mặc định: `.`)
`--logLevel=<silent\|info\|verbose>` |  | Chỉ định cấp độ log thời gian xây dựng
`--preset` |  | Preset máy chủ Nitro
`--dotenv` |  | Đường dẫn đến tệp `.env` để tải, tương đối với thư mục gốc
`--envName` |  | Môi trường để sử dụng khi giải quyết ghi đè cấu hình (mặc định là `production` khi xây dựng, và `development` khi chạy máy chủ dev)
<!--/generate-opts-->

::read-more{to="/docs/getting-started/deployment#static-hosting"}
Đọc thêm về pre-rendering và hosting tĩnh.
::
