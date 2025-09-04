---
navigation.title: 'Nuxt Performance'
title: Nuxt performance
description: Best practices for improving performance of Nuxt apps.
---

Nuxt đi kèm với các tính năng tích hợp được thiết kế để cải thiện hiệu suất ứng dụng của bạn và góp phần vào [Core Web Vitals](https://web.dev/articles/vitals) tốt hơn. Ngoài ra còn có nhiều module cốt lõi Nuxt giúp cải thiện hiệu suất trong các lĩnh vực cụ thể. Hướng dẫn này nêu ra các thực tiễn tốt nhất để tối ưu hóa hiệu suất ứng dụng Nuxt của bạn.

## Built-in Features

Nuxt cung cấp một số tính năng tích hợp giúp bạn tối ưu hóa hiệu suất của trang web. Hiểu cách các tính năng này hoạt động là rất quan trọng để đạt được hiệu suất nhanh như chớp.

### Links

[`<NuxtLink>`](/docs/api/components/nuxt-link) là một thay thế drop-in cho component Vue Router's `<RouterLink>` và thẻ HTML `<a>`. Nó thông minh xác định xem link là internal hay external và render tương ứng với các tối ưu hóa có sẵn (prefetching, thuộc tính mặc định, v.v.)

```html
<template>
  <NuxtLink to="/about">About page</NuxtLink>
</template>

<!-- Which will render to with Vue Router & Smart Prefetching -->
<a href="/about">About page</a>
```

Nuxt tự động bao gồm smart prefetching. Điều đó có nghĩa là nó phát hiện khi một link hiển thị (theo mặc định), trong viewport hoặc khi cuộn và prefetch JavaScript cho những trang đó để chúng sẵn sàng khi người dùng nhấp vào link.

Bạn cũng có thể chọn prefetching khi tương tác thay thế:

```ts
export default defineNuxtConfig({
  experimental: {
    defaults: {
      nuxtLink: {
        prefetchOn: 'interaction',
      },
    }
  }
})
```

:read-more{title="NuxtLink" to="/docs/api/components/nuxt-link"}

### Hybrid Rendering

Trong các ứng dụng phức tạp hơn, chúng ta có thể cần kiểm soát đầy đủ cách ứng dụng của chúng ta được render để hỗ trợ các trường hợp mà một số trang có thể được tạo tại build time, trong khi những trang khác nên được client-side rendered

Hybrid rendering cho phép các quy tắc caching khác nhau cho mỗi route bằng Route Rules và quyết định cách server phản hồi yêu cầu mới trên một URL nhất định:

```ts
export default defineNuxtConfig({
  routeRules: {
    '/': {
      prerender: true
    },
    '/products/**': {
      swr: 3600
    },
    '/blog': {
      isr: 3600
    },
    '/admin/**': {
      ssr: false
    },
  }
})
```

Server Nuxt sẽ tự động đăng ký middleware tương ứng và wrap routes với cache handlers sử dụng Nitro caching layer.

:read-more{title="Hybrid rendering" to="/docs/guide/concepts/rendering#hybrid-rendering"}

### Lazy Loading Components

Để import động một component (cũng được gọi là lazy-loading một component) tất cả những gì bạn cần làm là thêm tiền tố Lazy vào tên component. Điều này hữu ích nếu component không luôn cần thiết.

```html
<script setup lang="ts">
const show = ref(false)
</script>

<template>
  <div>
    <h1>Mountains</h1>
    <LazyMountainsList v-if="show" />
    <button v-if="!show" @click="show = true">Show List</button>
  </div>
</template>
```

Bằng cách sử dụng tiền tố Lazy bạn có thể trì hoãn tải code component cho đến thời điểm phù hợp, điều này có thể giúp tối ưu hóa kích thước bundle JavaScript của bạn.

:read-more{title="Lazy loading components" to="/docs/guide/directory-structure/components#dynamic-imports"}

### Lazy Hydration

Không phải lúc nào cũng cần hydrate (hoặc làm cho tương tác) tất cả các component của trang web của bạn khi load ban đầu. Sử dụng lazy hydration, bạn có thể kiểm soát khi code component có thể được tải, điều này có thể cải thiện metric time-to-interactive cho ứng dụng của bạn. Nuxt cho phép bạn kiểm soát khi các component trở nên tương tác với lazy hydration (được thêm vào Nuxt v3.16).

```html
<template>
  <div>
    <LazyMyComponent hydrate-on-visible />
  </div>
</template>
```

Để tối ưu hóa ứng dụng của bạn, bạn có thể trì hoãn hydration của một số component cho đến khi chúng hiển thị, hoặc cho đến khi trình duyệt hoàn thành các tác vụ quan trọng hơn.

:read-more{title="Lazy hydration" to="/docs/guide/directory-structure/components#delayed-or-lazy-hydration"}

### Fetching data

Để tránh fetch cùng dữ liệu hai lần (một lần trên server và một lần trên client) Nuxt cung cấp [`useFetch`](/docs/api/composables/use-fetch) và [`useAsyncData`](/docs/api/composables/use-async-data). Chúng đảm bảo rằng nếu một API call được thực hiện trên server, dữ liệu được chuyển tiếp đến client trong payload thay vì fetch lại.

:read-more{title="Data fetching" to="/docs/getting-started/data-fetching"}

## Core Nuxt Modules

Ngoài các tính năng tích hợp của Nuxt, còn có các module cốt lõi được duy trì bởi team Nuxt giúp cải thiện hiệu suất hơn nữa. Các module này giúp xử lý assets như hình ảnh, font tùy chỉnh, hoặc third party scripts.

### Images

Hình ảnh chưa được tối ưu hóa có thể có tác động tiêu cực đáng kể đến hiệu suất trang web, đặc biệt là điểm số [Largest Contentful Paint (LCP)](https://web.dev/articles/lcp).

Trong Nuxt chúng ta có thể sử dụng module [Nuxt Image](https://image.nuxt.com/) là một plug-and-play image optimization cho các ứng dụng Nuxt. Nó cho phép resize và transform hình ảnh của bạn bằng built-in optimizer hoặc CDN hình ảnh yêu thích của bạn.

:video-accordion{title="Watch the video by LearnVue about Nuxt Image" videoId="_UBff2eqGY0"}

[`<NuxtImg>`](/docs/api/components/nuxt-img) là một thay thế drop-in cho thẻ `<img>` native đi kèm với các enhancements sau:

* Sử dụng provider tích hợp để tối ưu hóa hình ảnh local và remote
* Chuyển `src` thành provider optimized URLs với các định dạng hiện đại như WebP hoặc Avif
* Tự động resize hình ảnh dựa trên `width` và `height`
* Tạo responsive `sizes` khi cung cấp tùy chọn sizes
* Hỗ trợ `lazy loading` native cũng như các thuộc tính `<img>` khác

Hình ảnh trong trang web của bạn thường có thể được phân tách theo tầm quan trọng; những hình ảnh cần được deliver trước tại load ban đầu (tức là `Largest Contentful Paint`), và những hình ảnh có thể được tải sau hoặc khi cần cụ thể. Vì vậy, chúng ta có thể sử dụng các tối ưu hóa sau:

```html
<template>
  <!-- 🚨 Cần được tải ASAP -->
  <NuxtImg
    src="/hero-banner.jpg"
    format="webp"
    preload
    loading="eager"
    fetch-priority="high"
    width="200"
    height="100"
  />

  <!-- 🐌 Có thể tải sau -->
  <NuxtImg
    src="/facebook-logo.jpg"
    format="webp"
    loading="lazy"
    fetch-priority="low"
    width="200"
    height="100"
  />
</template>
```

:read-more{title="Nuxt Image" to="https://image.nuxt.com/usage/nuxt-img"}

### Fonts

[Nuxt Fonts](https://fonts.nuxt.com/) sẽ tự động tối ưu hóa fonts của bạn (bao gồm custom fonts) và loại bỏ external network requests để cải thiện privacy và hiệu suất.

Nó bao gồm built-in automatic self-hosting cho bất kỳ file font nào, nghĩa là bạn có thể load web fonts một cách tối ưu với reduced layout shift, nhờ underlying package [fontaine](https://github.com/unjs/fontaine).

:video-accordion{title="Watch the talk by Daniel Roe about the idea behind Nuxt Fonts" videoId="D3F683UViBY"}

Nuxt Fonts xử lý tất cả CSS của bạn và thực hiện các việc sau khi nó gặp một font-family declaration.

1. **Resolve fonts** – Tìm kiếm file font trong public/, sau đó kiểm tra web providers như Google, Bunny, và Fontshare.
2. **Tạo @font-face rules** – Inject CSS rules để load fonts từ các nguồn chính xác.
3. **Proxy & cache fonts** – Rewrite URLs thành `/_fonts`, download và cache fonts locally.
4. **Tạo fallback metrics** – Điều chỉnh local system fonts để match web fonts, giảm layout shift ([CLS](https://web.dev/articles/cls)).
5. **Bao gồm fonts trong build** – Bundle fonts với project của bạn, hash file names và set long-lived cache headers.

Nó hỗ trợ nhiều providers được thiết kế để pluggable và extensible, vì vậy bất kể setup của bạn là gì bạn nên có thể sử dụng một provider hiện có hoặc viết provider riêng của mình.

### Scripts

Third-party resources như analytics tools, video embeds, maps, và social media integrations nâng cao chức năng trang web nhưng có thể làm giảm đáng kể trải nghiệm người dùng và tác động tiêu cực đến [Interaction to Next Paint (INP)](https://web.dev/articles/inp) và Largest Contentful Paint (LCP) scores.

[Nuxt Scripts](https://scripts.nuxt.com/) cho phép bạn load third-party scripts với hiệu suất, privacy, security và DX tốt hơn.

:video-accordion{title="Watch the video by Alex Lichter about Nuxt Scripts" videoId="sjMqUUvH9AE"}

Nuxt Scripts cung cấp một abstraction layer trên top của third-party scripts, cung cấp SSR support và type-safety đồng thời vẫn cho bạn kiểm soát low-level đầy đủ về cách một script được load.

```ts
const { onLoaded, proxy } = useScriptGoogleAnalytics(
  { 
    id: 'G-1234567',
    scriptOptions: {
      trigger: 'manual',
    },
  },
)
// queue events to be sent when ga loads
proxy.gtag('config', 'UA-123456789-1')
// or wait until ga is loaded
onLoaded((gtag) => {
  // script loaded
})
```

:read-more{title="Nuxt Scripts" to="https://scripts.nuxt.com/scripts"}

## Profiling Tools

Để cải thiện hiệu suất, chúng ta cần biết cách đo lường nó trước, bắt đầu với đo lường hiệu suất trong quá trình phát triển - trên local environment, sau đó chuyển sang audit ứng dụng được deploy trên production.

### Nuxi Analyze

Lệnh `nuxi` này cho phép analyze production bundle hoặc ứng dụng Nuxt của bạn. Nó tận dụng `vite-bundle-visualizer` (tương tự như `webpack-bundle-analyzer`) để tạo một biểu diễn visual của bundle ứng dụng của bạn, giúp dễ dàng xác định component nào chiếm nhiều không gian nhất.

Khi bạn thấy một block lớn trong visualization, nó thường báo hiệu một cơ hội tối ưu hóa—cho dù bằng cách chia nó thành các phần nhỏ hơn, implement lazy loading, hoặc thay thế bằng một thứ hiệu quả hơn, đặc biệt là cho third-party libraries.

Large blocks chứa nhiều element có thể được giảm bằng cách import chỉ các component cần thiết thay vì toàn bộ modules trong khi large standalone blocks có thể phù hợp hơn cho lazy loading thay vì được include trong main bundle.

### Nuxt DevTools

[Nuxt DevTools](https://devtools.nuxt.com/) cung cấp cho bạn insights và transparency về Nuxt App của bạn để xác định performance gaps và seamlessly manage cấu hình ứng dụng của bạn.

![Nuxt DevTools example](https://user-images.githubusercontent.com/11247099/217670806-fb39aeff-3881-44e5-b9c8-6c757f5925fc.png)

Nó đi kèm với một số tính năng chúng ta có thể sử dụng để đo lường hiệu suất của Nuxt apps:

1. **Timeline** – Theo dõi thời gian dành cho rendering, updating, và initializing components để xác định performance bottlenecks.  
2. **Assets** – Hiển thị file sizes (ví dụ: hình ảnh) mà không có transformations.  
3. **Render Tree** – Hiển thị connections giữa Vue components, scripts, và styles để tối ưu hóa dynamic loading.  
4. **Inspect** – Liệt kê tất cả files được sử dụng trong Vue app với size và evaluation time.

### Chrome DevTools

Chrome DevTools đi kèm với hai tab hữu ích để đo lường hiệu suất; `Performance` và `Lighthouse`.

Khi bạn mở panel [Performance](https://developer.chrome.com/docs/devtools/performance/overview), nó ngay lập tức hiển thị local **Largest Contentful Paint (LCP)** và **Cumulative Layout Shift (CLS)** scores của bạn (tốt, cần cải thiện, hoặc xấu).  

Nếu bạn tương tác với trang, nó cũng capture **Interaction to Next Paint (INP)**, cho bạn view đầy đủ của Core Web Vitals dựa trên thiết bị và network của bạn.

![Chrome DevTools Performance Panel](https://developer.chrome.com/static/docs/devtools/performance/image/cpu-throttling_856.png)

[Lighthouse](https://developer.chrome.com/docs/lighthouse) audits hiệu suất, accessibility, SEO, progressive web apps, và best practices. Nó chạy tests trên trang của bạn và tạo một report. Sử dụng failing audits như một guide để cải thiện site của bạn.

![Lighthouse](https://developer.chrome.com/static/docs/devtools/lighthouse/images/lighthouse-overview_720.png)

Mỗi audit có một reference document giải thích tại sao audit quan trọng, cũng như cách fix nó.

### PageSpeed Insights

[PageSpeed Insights (PSI)](https://developers.google.com/speed/docs/insights/v5/about) báo cáo về trải nghiệm người dùng của một trang trên cả mobile và desktop devices, và cung cấp gợi ý về cách trang đó có thể được cải thiện.

Nó cung cấp cả lab và field data về một trang. Lab data hữu ích cho debugging issues, vì nó được thu thập trong môi trường kiểm soát trong khi field data hữu ích cho capturing true, real-world user experience.

### Web Page Test

[WebPageTest](https://www.webpagetest.org/) là một web performance tool cung cấp diagnostic information sâu về cách một trang perform dưới nhiều điều kiện khác nhau.

Mỗi test có thể được chạy từ các location khác nhau trên thế giới, trên real browsers, qua bất kỳ số lượng customizable network conditions nào.

## Common problems

Khi xây dựng ứng dụng Nuxt phức tạp hơn, bạn sẽ có thể gặp một số vấn đề được liệt kê dưới đây. Hiểu các vấn đề này và fix chúng sẽ giúp bạn cải thiện hiệu suất của trang web.

### Overusing plugins

**Vấn đề**: Một số lượng lớn plugins có thể gây ra performance issues, đặc biệt nếu chúng yêu cầu expensive computations hoặc mất quá nhiều thời gian để initialize. Vì plugins chạy trong hydration phase, inefficient setups có thể block rendering và degrade trải nghiệm người dùng.

**Giải pháp**: Kiểm tra plugins của bạn và xem liệu một số có thể được implement thay thế như một composable hoặc utility function không.

### Unused code / dependencies

**Vấn đề**: Với development của project, có thể có trường hợp có một số unused code hoặc dependency. Chức năng bổ sung này có thể không được sử dụng hoặc cần thiết trong khi nó sẽ tăng bundle size của project của chúng ta.

**Giải pháp**: Kiểm tra `package.json` của bạn cho unused dependencies và analyze code của bạn cho unused utils/composables/functions.

### Not using Vue Performance tips

**Vấn đề**: [Vue documentation](https://vuejs.org/guide/best-practices/performance) liệt kê một số Performance improvements chúng ta có thể sử dụng trong Nuxt projects của chúng ta cũng nhưng vì chúng là một phần của Vue documentation, developers có xu hướng quên về nó và tập trung vào Nuxt specific improvements only - trong khi Nuxt application vẫn là một Vue project.

**Giải pháp**: Sử dụng concepts như `shallowRef`, `v-memo`, `v-once`, v.v để cải thiện hiệu suất.

### Not following patterns

**Vấn đề**: Càng nhiều người đang làm việc trên project, càng khó để maintain stable codebase. Developers có xu hướng giới thiệu new concepts họ thấy trong một project khác có thể gây conflicts và problems với performance.

**Giải pháp**: Thiết lập rules và patterns trong project như [Good practices and Design Patterns for Vue Composables](https://dev.to/jacobandrewsky/good-practices-and-design-patterns-for-vue-composables-24lk)

### Trying to load everything at the same time

**Vấn đề**: Khi một trang được load và nó không được hướng dẫn đúng cách về thứ tự loading elements nó sẽ dẫn đến fetching everything cùng lúc - điều này có thể chậm và dẫn đến bad User Experience.

**Giải pháp**: Sử dụng concepts như Progressive Enhancement nơi core webpage content được set first, sau đó more nuanced và technically rigorous layers of presentation và features được thêm on top khi browser/internet connection cho phép.

## Useful Resources

Để tìm hiểu thêm về các techniques khác nhau để cải thiện hiệu suất, hãy xem các resources sau:

1. [Apply instant loading with the PRPL pattern](https://web.dev/articles/apply-instant-loading-with-prpl)
2. [Perceived performance](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Performance/Perceived_performance)
3. [Understanding Critical Rendering Path](https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Critical_rendering_path)
