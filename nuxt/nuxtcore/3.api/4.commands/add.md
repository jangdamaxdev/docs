---
title: "nuxt add"
description: "Tạo khuôn mẫu một thực thể vào ứng dụng Nuxt của bạn."
links:
  - label: Source
    icon: i-simple-icons-github
    to: https://github.com/nuxt/cli/blob/main/packages/nuxi/src/commands/add.ts
    size: xs
---

<!--add-cmd-->
```bash [Terminal]
npx nuxt add <TEMPLATE> <NAME> [--cwd=<directory>] [--logLevel=<silent|info|verbose>] [--force]
```
<!--/add-cmd-->

### Arguments

<!--add-args-->
Argument | Description
--- | ---
`TEMPLATE` | Chỉ định mẫu nào để tạo (tùy chọn: <api\|plugin\|component\|composable\|middleware\|layout\|page\|layer>)
`NAME` | Chỉ định tên của tệp được tạo
<!--/add-args-->

### Options

<!--add-opts-->
Option | Default | Description
--- | --- | ---
`--cwd=<directory>` | `.` | Chỉ định thư mục làm việc
`--logLevel=<silent\|info\|verbose>` |  | Chỉ định cấp độ log thời gian xây dựng
`--force` | `false` | Buộc ghi đè tệp nếu nó đã tồn tại
<!--/add-opts-->

**Modifiers:**

Một số mẫu hỗ trợ cờ bổ ngữ bổ sung để thêm hậu tố (như `.client` hoặc `.get`) vào tên của chúng.

```bash [Terminal]
# Tạo `/plugins/sockets.client.ts`
npx nuxt add plugin sockets --client
```

## `nuxt add component`

* Cờ bổ ngữ: `--mode client|server` hoặc `--client` hoặc `--server`

```bash [Terminal]
# Tạo `components/TheHeader.vue`
npx nuxt add component TheHeader
```

## `nuxt add composable`

```bash [Terminal]
# Tạo `composables/foo.ts`
npx nuxt add composable foo
```

## `nuxt add layout`

```bash [Terminal]
# Tạo `layouts/custom.vue`
npx nuxt add layout custom
```

## `nuxt add plugin`

* Modifier flags: `--mode client|server` or `--client`or `--server`

```bash [Terminal]
# Tạo `plugins/analytics.ts`
npx nuxt add plugin analytics
```

## `nuxt add page`

```bash [Terminal]
# Tạo `pages/about.vue`
npx nuxt add page about
```

```bash [Terminal]
# Tạo `pages/category/[id].vue`
npx nuxt add page "category/[id]"
```

## `nuxt add middleware`

* Cờ bổ ngữ: `--global`

```bash [Terminal]
# Tạo `middleware/auth.ts`
npx nuxt add middleware auth
```

## `nuxt add api`

* Cờ bổ ngữ: `--method` (có thể chấp nhận `connect`, `delete`, `get`, `head`, `options`, `patch`, `post`, `put` hoặc `trace`) hoặc thay thế bạn có thể sử dụng trực tiếp `--get`, `--post`, v.v.

```bash [Terminal]
# Tạo `server/api/hello.ts`
npx nuxt add api hello
```

## `nuxt add layer`

```bash [Terminal]
# Tạo `layers/subscribe/nuxt.config.ts`
npx nuxt add layer subscribe
```
