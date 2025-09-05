---
title: 'nuxt dev'
description: Lệnh dev khởi động máy chủ phát triển với hot module replacement tại http://localhost:3000
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/dev.ts
    size: xs
---

<!--dev-cmd-->
```bash [Terminal]
npx nuxt dev [ROOTDIR] [--cwd=<directory>] [--logLevel=<silent|info|verbose>] [--dotenv] [--envName] [--no-clear] [--no-fork] [-p, --port] [-h, --host] [--clipboard] [-o, --open] [--https] [--publicURL] [--qr] [--public] [--tunnel] [--sslCert] [--sslKey]
```
<!--/dev-cmd-->

Lệnh `dev` khởi động máy chủ phát triển với hot module replacement tại [http://localhost:3000](https://localhost:3000)

## Arguments

<!--dev-args-->
Argument | Description
--- | ---
`ROOTDIR="."` | Chỉ định thư mục làm việc (mặc định: `.`)
<!--/dev-args-->

## Options

<!--dev-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` |  | Chỉ định thư mục làm việc, điều này ưu tiên hơn ROOTDIR (mặc định: `.`)
`--logLevel=<silent\|info\|verbose>` |  | Chỉ định cấp độ log thời gian xây dựng
`--dotenv` |  | Đường dẫn đến tệp `.env` để tải, tương đối với thư mục gốc
`--envName` |  | Môi trường để sử dụng khi giải quyết ghi đè cấu hình (mặc định là `production` khi xây dựng, và `development` khi chạy máy chủ dev)
`--no-clear` |  | Vô hiệu hóa xóa console khi khởi động lại
`--no-fork` |  | Vô hiệu hóa chế độ forked
`-p, --port` |  | Port để lắng nghe (mặc định: `NUXT_PORT \|\| NITRO_PORT \|\| PORT \|\| nuxtOptions.devServer.port`)
`-h, --host` |  | Host để lắng nghe (mặc định: `NUXT_HOST \|\| NITRO_HOST \|\| HOST \|\| nuxtOptions._layers?.[0]?.devServer?.host`)
`--clipboard` | `false` | Sao chép URL vào clipboard
`-o, --open` | `false` | Mở URL trong trình duyệt
`--https` |  | Bật HTTPS
`--publicURL` |  | URL công khai hiển thị (được sử dụng cho mã QR)
`--qr` |  | Hiển thị mã QR của URL công khai khi có sẵn
`--public` |  | Lắng nghe tất cả giao diện mạng
`--tunnel` |  | Mở tunnel sử dụng https://github.com/unjs/untun
`--sslCert` |  | (ĐÃ LỖI THỜI) Sử dụng `--https.cert` thay thế.
`--sslKey` |  | (ĐÃ LỖI THỜI) Sử dụng `--https.key` thay thế.
<!--/dev-opts-->

Port và host cũng có thể được đặt qua biến môi trường NUXT_PORT, PORT, NUXT_HOST hoặc HOST.

Ngoài các tùy chọn trên, `@nuxt/cli` có thể truyền tùy chọn qua `listhen`, ví dụ `--no-qr` để tắt mã QR máy chủ dev. Bạn có thể tìm danh sách tùy chọn `listhen` trong tài liệu [unjs/listhen](https://github.com/unjs/listhen).

Lệnh này đặt `process.env.NODE_ENV` thành `development`.

::note
Nếu bạn đang sử dụng chứng chỉ tự ký trong phát triển, bạn sẽ cần đặt `NODE_TLS_REJECT_UNAUTHORIZED=0` trong môi trường của bạn.
::
