---
navigation.title: 'Nuxt Performance'
title: Nuxt performance
description: Best practices for improving performance of Nuxt apps.
---

Nuxt comes với built-in features designed để improve application's performance và contribute để better [Core Web Vitals](https://web.dev/articles/vitals). There are also multiple Nuxt core modules that assist in improving performance in specific areas. Guide này outlines best practices để optimize performance của Nuxt application của bạn.

## Built-in Features

Nuxt offers several built-in features that help optimize performance của website của bạn. Understanding how những features này work is crucial cho achieving blazingly-fast performance.

### Links

[`<NuxtLink>`](/docs/api/components/nuxt-link) is a drop-in replacement cho both Vue Router's `<RouterLink>` component và HTML's `<a>` tag. Nó intelligently determines whether link is internal hoặc external và renders nó accordingly với available optimizations (prefetching, default attributes, etc.)

```html
<template>
  <NuxtLink to="/about">About page</NuxtLink>
</template>

<!-- Which will render to with Vue Router & Smart Prefetching -->
<a href="/about">About page</a>
```

Nuxt automatically includes smart prefetching. That means nó detects khi một link is visible (by default), either trong viewport hoặc khi scrolling và prefetches JavaScript cho những pages đó so that chúng are ready khi user clicks link.

You can also opt cho prefetching on interaction instead:

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

Trong more complex applications, chúng ta may need một full control over how application của chúng ta is rendered để support cases where some pages could be generated tại build time, while others should be client-side rendered

Hybrid rendering allows different caching rules per route using Route Rules và decides how server should respond đến một new request trên một given URL:

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

Nuxt server will automatically register corresponding middleware và wrap routes với cache handlers using Nitro caching layer.

:read-more{title="Hybrid rendering" to="/docs/guide/concepts/rendering#hybrid-rendering"}

### Lazy Loading Components

Để dynamically import một component (also known như lazy-loading một component) all bạn need để do is add Lazy prefix đến component's name. Điều này is useful if component is not always needed.

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

By using Lazy prefix bạn can delay loading component code until right moment, which can be helpful cho optimizing JavaScript bundle size của bạn.

:read-more{title="Lazy loading components" to="/docs/guide/directory-structure/components#dynamic-imports"}

### Lazy Hydration

Nó is not always necessary để hydrate (hoặc make interactive) tất cả components của site của bạn trên initial load. Using lazy hydration, bạn can control khi components can have code của chúng loaded, which can improve time-to-interactive metric cho app của bạn. Nuxt allows bạn để control khi components become interactive với lazy hydration (added in Nuxt v3.16).

```html
<template>
  <div>
    <LazyMyComponent hydrate-on-visible />
  </div>
</template>
```

Để optimize app của bạn, bạn may want để delay hydration của some components until chúng are visible, hoặc until browser is done với more important tasks.

:read-more{title="Lazy hydration" to="/docs/guide/directory-structure/components#delayed-or-lazy-hydration"}

### Fetching data

Để avoid fetching same data twice (once trên server và once trên client) Nuxt provides [`useFetch`](/docs/api/composables/use-fetch) và [`useAsyncData`](/docs/api/composables/use-async-data). Chúng ensure rằng if một API call is made trên server, data is forwarded đến client trong payload instead của being fetched again.

:read-more{title="Data fetching" to="/docs/getting-started/data-fetching"}

## Core Nuxt Modules

Apart từ Nuxt's built-in features, there are also core modules maintained bởi Nuxt team which help improve performance even further. Những modules này help handle assets such như images, custom fonts, hoặc third party scripts.

### Images

Unoptimized images can have một significant negative impact trên website performance của bạn, specifically [Largest Contentful Paint (LCP)](https://web.dev/articles/lcp) score.

Trong Nuxt chúng ta can use [Nuxt Image](https://image.nuxt.com/) module that is một plug-and-play image optimization cho Nuxt apps. Nó allows resizing và transforming images của bạn using built-in optimizer hoặc favorite images CDN của bạn.

:video-accordion{title="Watch the video from LearnVue about Nuxt Image" videoId="_UBff2eqGY0"}

[`<NuxtImg>`](/docs/api/components/nuxt-img) is một drop-in replacement cho native `<img>` tag that comes với following enhancements:

* Uses built-in provider để optimize local và remote images
* Converts `src` đến provider optimized URLs với modern formats such như WebP hoặc Avif
* Automatically resizes images based trên `width` và `height`
* Generates responsive `sizes` khi providing sizes option
* Supports native `lazy loading` cũng như other `<img>` attributes

Images trong website của bạn can usually be separated bởi importance; những ones that are needed để be delivered first tại initial load (i.e. `Largest Contentful Paint`), và những ones that can be loaded later hoặc khi specifically needed. Cho that, chúng ta could use following optimizations:

```html
<template>
  <!-- 🚨 Needs to be loaded ASAP -->
  <NuxtImg
    src="/hero-banner.jpg"
    format="webp"
    preload
    loading="eager"
    fetch-priority="high"
    width="200"
    height="100"
  />

  <!-- 🐌 Can be loaded later -->
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

[Nuxt Fonts](https://fonts.nuxt.com/) will automatically optimize fonts của bạn (including custom fonts) và remove external network requests cho improved privacy và performance.

Nó includes built-in automatic self-hosting cho any font file which means bạn can optimally load web fonts với reduced layout shift, thanks đến underlying package [fontaine](https://github.com/unjs/fontaine).

:video-accordion{title="Watch the talk by Daniel Roe about the idea behind Nuxt Fonts" videoId="D3F683UViBY"}

Nuxt Fonts processes tất cả CSS của bạn và does following things automatically khi nó encounters một font-family declaration.

1. **Resolves fonts** – Looks cho font files trong public/, then checks web providers như Google, Bunny, và Fontshare.
2. **Generates @font-face rules** – Injects CSS rules để load fonts từ correct sources.
3. **Proxies & caches fonts** – Rewrites URLs đến `/_fonts`, downloads và caches fonts locally.
4. **Creates fallback metrics** – Adjusts local system fonts để match web fonts, reducing layout shift ([CLS](https://web.dev/articles/cls)).
5. **Includes fonts in build** – Bundles fonts với project của bạn, hashing file names và setting long-lived cache headers.

Nó supports multiple providers that are designed để be pluggable và extensible, so no matter setup của bạn bạn should be able để use một existing provider hoặc write own của bạn.

### Scripts

Third-party resources như analytics tools, video embeds, maps, và social media integrations enhance website functionality nhưng can significantly degrade user experience và negatively impact [Interaction to Next Paint (INP)](https://web.dev/articles/inp) và Largest Contentful Paint (LCP) scores.

[Nuxt Scripts](https://scripts.nuxt.com/) lets bạn load third-party scripts với better performance, privacy, security và DX.

:video-accordion{title="Watch the video by Alex Lichter about Nuxt Scripts" videoId="sjMqUUvH9AE"}

Nuxt Scripts provides một abstraction layer on top của third-party scripts, providing SSR support và type-safety và while still giving bạn full low-level control over how một script is loaded.

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

Để improve performance, chúng ta need để first know how để measure nó, starting với measuring performance during development - on local environment, và then moving để auditing applications that are deployed on production.

### Nuxi Analyze

[This](/docs/api/commands/analyze) command của `nuxi` allows để analyze production bundle hoặc Nuxt application của bạn. Nó leverages `vite-bundle-visualizer` (similar để `webpack-bundle-analyzer`) để generate một visual representation của application's bundle của bạn, making nó easier để identify which components take up most space.

Khi bạn see một large block trong visualization, nó often signals một opportunity cho optimization—whether bằng splitting nó into smaller parts, implementing lazy loading, hoặc replacing nó với một more efficient alternative, especially cho third-party libraries.

Large blocks containing multiple elements can often be reduced bằng importing only necessary components rather than entire modules while large standalone blocks may be better suited cho lazy loading rather than being included trong main bundle.

### Nuxt DevTools

[Nuxt DevTools](https://devtools.nuxt.com/) gives bạn insights và transparency about Nuxt App của bạn để identify performance gaps và seamlessly manage app configurations của bạn.

![Nuxt DevTools example](https://user-images.githubusercontent.com/11247099/217670806-fb39aeff-3881-44e5-b9c8-6c757f5925fc.png)

Nó comes với several features chúng ta can use để measure performance của Nuxt apps:

1. **Timeline** – Tracks time spent on rendering, updating, và initializing components để identify performance bottlenecks.  
2. **Assets** – Displays file sizes (e.g., images) without transformations.  
3. **Render Tree** – Shows connections between Vue components, scripts, và styles để optimize dynamic loading.  
4. **Inspect** – Lists tất cả files used trong Vue app với size của chúng và evaluation time.

### Chrome DevTools

Chrome DevTools come với two useful tabs cho measuring performance; `Performance` và `Lighthouse`.

Khi bạn open [Performance](https://developer.chrome.com/docs/devtools/performance/overview) panel, nó instantly shows local **Largest Contentful Paint (LCP)** và **Cumulative Layout Shift (CLS)** scores của bạn (good, needs improvement, hoặc bad).  

Nếu bạn interact với page, nó also captures **Interaction to Next Paint (INP)**, giving bạn một full view của Core Web Vitals của bạn based trên device và network của bạn.

![Chrome DevTools Performance Panel](https://developer.chrome.com/static/docs/devtools/performance/image/cpu-throttling_856.png)

[Lighthouse](https://developer.chrome.com/docs/devtools/lighthouse) audits performance, accessibility, SEO, progressive web apps, và best practices. Nó runs tests trên page của bạn và generates một report. Use failing audits như một guide để improve site của bạn.

![Lighthouse](https://developer.chrome.com/static/docs/lighthouse/images/lighthouse-overview_720.png)

Each audit has một reference document explaining why audit is important, cũng như how để fix nó.

### PageSpeed Insights

[PageSpeed Insights (PSI)](https://developers.google.com/speed/docs/insights/v5/about) reports on user experience của một page on both mobile và desktop devices, và provides suggestions on how that page may be improved.

Nó provides both lab và field data about một page. Lab data is useful cho debugging issues, as nó is collected in một controlled environment while field data is useful cho capturing true, real-world user experience.

### Web Page Test

[WebPageTest](https://www.webpagetest.org/) is một web performance tool providing deep diagnostic information about how một page performs under một variety của conditions.

Each test can be run từ different locations around world, on real browsers, over bất kỳ number nào của customizable network conditions.

## Common problems

Khi building more complex Nuxt applications, bạn will probably encounter some của problems listed below. Understanding những problems này và fixing chúng will help bạn improve performance của website của bạn.

### Overusing plugins

**Problem**: Một large number của plugins can cause performance issues, especially if chúng require expensive computations hoặc take too long để initialize. Since plugins run during hydration phase, inefficient setups can block rendering và degrade user experience.

**Solution**: Inspect plugins của bạn và see if some của chúng could be implemented rather như một composable hoặc utility function instead.

### Unused code / dependencies

**Problem**: Với development của project, there can be một case where there will be some unused code hoặc một dependency. Functionality additional này may not be used hoặc needed while nó will increase bundle size của project của chúng ta.

**Solution**: Inspect `package.json` của bạn cho unused dependencies và analyze code của bạn cho unused utils/composables/functions.

### Not using Vue Performance tips

**Problem**: [Vue documentation](https://vuejs.org/guide/best-practices/performance) lists several Performance improvements chúng ta can use trong Nuxt projects của chúng ta cũng nhưng as chúng are part của Vue documentation, developers tend để forget about nó và focus on Nuxt specific improvements only - while Nuxt application is still một Vue project.

**Solution**: Use concepts such như `shallowRef`, `v-memo`, `v-once`, etc để improve performance.

### Not following patterns

**Problem**: More people are currently working on project, more difficult nó will be để maintain stable codebase. Developers have một tendency để introduce new concepts they've seen trong another project which can cause conflicts và problems với performance.

**Solution**: Establish rules và patterns trong project such như [Good practices và Design Patterns cho Vue Composables](https://dev.to/jacobandrewsky/good-practices-and-design-patterns-for-vue-composables-24lk)

### Trying to load everything at the same time

**Problem**: Khi một page is loaded và nó is not correctly instructed about order của loading elements nó will result in fetching everything tại same time - which can be slow và result in bad User Experience.

**Solution**: Use concepts such như Progressive Enhancement where core webpage content is set first, then more nuanced và technically rigorous layers của presentation và features are added on top as browser/internet connection allow.

## Useful Resources

Để learn more about various techniques cho improving performance, take một look tại following resources:

1. [Apply instant loading with the PRPL pattern](https://web.dev/articles/apply-instant-loading-with-prpl)
2. [Perceived performance](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Performance/Perceived_performance)
3. [Understanding Critical Rendering Path](https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Critical_rendering_path)
