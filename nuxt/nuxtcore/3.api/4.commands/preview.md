---
title: "nuxt preview"
description: Lệnh preview khởi động máy chủ để xem trước ứng dụng của bạn sau lệnh build.
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/preview.ts
    size: xs
---

<!--preview-cmd-->
```bash [Terminal]
npx nuxt preview [ROOTDIR] [--cwd=<directory>] [--logLevel=<silent|info|verbose>] [--envName] [--dotenv] [-p, --port]
```
<!--/preview-cmd-->

Lệnh `preview` khởi động máy chủ để xem trước ứng dụng Nuxt của bạn sau khi chạy lệnh `build`. Lệnh `start` là bí danh cho `preview`. Khi chạy ứng dụng của bạn trong sản xuất, hãy tham khảo phần [Deployment](/docs/getting-started/deployment).

## Arguments

<!--preview-args-->
Argument | Description
--- | ---
`ROOTDIR="."` | Chỉ định thư mục làm việc (mặc định: `.`)
<!--/preview-args-->

## Options

<!--preview-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` |  | Chỉ định thư mục làm việc, điều này ưu tiên hơn ROOTDIR (mặc định: `.`)
`--logLevel=<silent\|info\|verbose>` |  | Chỉ định cấp độ log thời gian xây dựng
`--envName` |  | Môi trường để sử dụng khi giải quyết ghi đè cấu hình (mặc định là `production` khi xây dựng, và `development` khi chạy máy chủ dev)
`--dotenv` |  | Đường dẫn đến tệp `.env` để tải, tương đối với thư mục gốc
`-p, --port` |  | Port để lắng nghe (mặc định: `NUXT_PORT \|\| NITRO_PORT \|\| PORT`)
<!--/preview-opts-->

Lệnh này đặt `process.env.NODE_ENV` thành `production`. Để ghi đè, định nghĩa `NODE_ENV` trong tệp `.env` hoặc như đối số dòng lệnh.

::note
Để thuận tiện, trong chế độ preview, tệp [`.env`](/docs/guide/directory-structure/env) của bạn sẽ được tải vào `process.env`. (Tuy nhiên, trong sản xuất bạn sẽ cần đảm bảo các biến môi trường được đặt bởi chính bạn. Ví dụ, với Node.js 20+ bạn có thể làm điều này bằng cách chạy `node --env-file .env .output/server/index.mjs` để khởi động máy chủ của bạn.)
::
