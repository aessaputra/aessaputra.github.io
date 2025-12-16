---
title: Web Performance Optimization
aliases:
  - Web Performance
  - Web Performance Optimization
  - Website Performance
  - Performance Optimization
  - Web Speed Optimization
categories:
  - "[[Posts]]"
tags:
  - posts
  - web-performance
  - optimization
  - user-experience
author:
  - "[[Aes Saputra]]"
url:
created: 2025-12-15
published: 2025-12-15
date: 2025-12-15
topics:
  - web-performance
  - optimization
  - user-experience
status: published
feed: show
  - Web Performance
  - Performance Optimization
  - Core Web Vitals
  - LCP
  - FID
  - CLS
  - Performance Metrics
  - Web Vitals
  - Site Speed
---

Web Performance adalah kecepatan loading dan responsivitas website yang secara langsung mempengaruhi user experience, SEO ranking, dan conversion rates. Optimasi performa web adalah aspek kritis dalam pengembangan aplikasi modern.

## Mengapa Performance Penting?

### 1. User Experience
- **53% users** meninggalkan site jika loading > 3 detik
- **1 detik delay** = 7% penurunan conversion
- **Fast loading** = better user satisfaction

### 2. SEO Impact
- Google menggunakan **Core Web Vitals** sebagai ranking factor
- **Page speed** mempengaruhi search ranking
- **Mobile performance** sangat penting untuk SEO

### 3. Business Impact
- **Amazon**: 100ms delay = 1% revenue loss
- **Walmart**: 1s improvement = 2% conversion increase
- **Pinterest**: 40% performance improvement = 15% SEO traffic increase

## Core Web Vitals

Google's Core Web Vitals adalah metrics utama untuk mengukur user experience:

### 1. Largest Contentful Paint (LCP)
**Mengukur**: Loading performance
**Target**: < 2.5 detik
**Optimasi**:
```typescript
// Preload critical resources
<link rel="preload" href="/hero-image.jpg" as="image">

// Optimize images
import Image from 'next/image'

<Image
  src="/hero.jpg"
  alt="Hero"
  width={800}
  height={600}
  priority // Load immediately
  placeholder="blur"
/>
```

### 2. First Input Delay (FID)
**Mengukur**: Interactivity
**Target**: < 100ms
**Optimasi**:
```typescript
// Code splitting untuk reduce main thread blocking
import dynamic from 'next/dynamic'

const HeavyComponent = dynamic(() => import('./HeavyComponent'), {
  loading: () => <Skeleton />,
  ssr: false
})

// Defer non-critical JavaScript
useEffect(() => {
  // Load analytics after page is interactive
  import('./analytics').then(analytics => {
    analytics.init()
  })
}, [])
```

### 3. Cumulative Layout Shift (CLS)
**Mengukur**: Visual stability
**Target**: < 0.1
**Optimasi**:
```css
/* Reserve space untuk images */
.image-container {
  aspect-ratio: 16 / 9;
  width: 100%;
}

/* Avoid layout shifts dari fonts */
@font-face {
  font-family: 'Inter';
  font-display: swap; /* Prevent invisible text */
  src: url('/fonts/inter.woff2') format('woff2');
}
```

## Performance Metrics

### Loading Metrics
- **Time to First Byte (TTFB)**: Server response time
- **First Contentful Paint (FCP)**: First content appears
- **Speed Index**: How quickly content is visually populated

### Interactivity Metrics
- **Time to Interactive (TTI)**: Page becomes fully interactive
- **Total Blocking Time (TBT)**: Main thread blocking time

### Visual Stability
- **Cumulative Layout Shift (CLS)**: Unexpected layout shifts

## Optimization Strategies

### 1. Image Optimization
```typescript
// Next.js Image component
import Image from 'next/image'

export default function Gallery() {
  return (
    <div>
      {/* Responsive images */}
      <Image
        src="/gallery/photo.jpg"
        alt="Photo"
        fill
        sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
        placeholder="blur"
        blurDataURL="data:image/jpeg;base64,..."
      />
      
      {/* WebP/AVIF format */}
      <picture>
        <source srcSet="/image.avif" type="image/avif" />
        <source srcSet="/image.webp" type="image/webp" />
        <img src="/image.jpg" alt="Fallback" />
      </picture>
    </div>
  )
}
```

### 2. Code Splitting
```typescript
// Route-based code splitting (automatic in Next.js)
// Component-based code splitting
const LazyModal = lazy(() => import('./Modal'))

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyModal />
    </Suspense>
  )
}

// Dynamic imports
const handleClick = async () => {
  const { heavyFunction } = await import('./heavyModule')
  heavyFunction()
}
```

### 3. Resource Optimization
```typescript
// Font optimization
import { Inter, Roboto } from 'next/font/google'

const inter = Inter({
  subsets: ['latin'],
  display: 'swap',
  preload: true
})

// CSS optimization
// Critical CSS inline, non-critical CSS async
<link rel="preload" href="/critical.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
```
### 4. Caching Strategies
```typescript
// Browser caching
// next.config.js
module.exports = {
  async headers() {
    return [
      {
        source: '/static/(.*)',
        headers: [
          {
            key: 'Cache-Control',
            value: 'public, max-age=31536000, immutable'
          }
        ]
      }
    ]
  }
}

// Service Worker caching
// sw.js
self.addEventListener('fetch', event => {
  if (event.request.destination === 'image') {
    event.respondWith(
      caches.open('images').then(cache => {
        return cache.match(event.request).then(response => {
          return response || fetch(event.request).then(fetchResponse => {
            cache.put(event.request, fetchResponse.clone())
            return fetchResponse
          })
        })
      })
    )
  }
})
```

### 5. Database Optimization
```typescript
// Connection pooling
import { Pool } from 'pg'

const pool = new Pool({
  connectionString: process.env.DATABASE_URL,
  max: 20, // Maximum connections
  idleTimeoutMillis: 30000,
  connectionTimeoutMillis: 2000
})

// Query optimization
// ❌ N+1 problem
const users = await User.findAll()
for (const user of users) {
  user.posts = await Post.findByUserId(user.id)
}

// ✅ Optimized with joins
const users = await User.findAll({
  include: [{ model: Post }]
})

// Database indexing
CREATE INDEX idx_posts_user_id ON posts(user_id);
CREATE INDEX idx_posts_created_at ON posts(created_at DESC);
```

## Performance Monitoring

### 1. Real User Monitoring (RUM)
```typescript
// Web Vitals tracking
import { getCLS, getFID, getFCP, getLCP, getTTFB } from 'web-vitals'

function sendToAnalytics(metric) {
  // Send to your analytics service
  fetch('/api/analytics', {
    method: 'POST',
    body: JSON.stringify({
      name: metric.name,
      value: metric.value,
      id: metric.id,
      delta: metric.delta
    })
  })
}

getCLS(sendToAnalytics)
getFID(sendToAnalytics)
getFCP(sendToAnalytics)
getLCP(sendToAnalytics)
getTTFB(sendToAnalytics)
```

### 2. Performance Observer API
```typescript
// Monitor long tasks
const observer = new PerformanceObserver(list => {
  list.getEntries().forEach(entry => {
    if (entry.duration > 50) {
      console.warn('Long task detected:', entry)
      // Send to monitoring service
    }
  })
})

observer.observe({ entryTypes: ['longtask'] })

// Monitor resource loading
const resourceObserver = new PerformanceObserver(list => {
  list.getEntries().forEach(entry => {
    if (entry.duration > 1000) {
      console.warn('Slow resource:', entry.name, entry.duration)
    }
  })
})

resourceObserver.observe({ entryTypes: ['resource'] })
```

### 3. Custom Performance Marks
```typescript
// Mark performance milestones
performance.mark('data-fetch-start')
const data = await fetchData()
performance.mark('data-fetch-end')

performance.measure('data-fetch-duration', 'data-fetch-start', 'data-fetch-end')

const measures = performance.getEntriesByType('measure')
console.log('Data fetch took:', measures[0].duration, 'ms')
```

## Next.js Specific Optimizations

### 1. [[Static Site Generation]] (SSG)
```typescript
// Pre-generate pages at build time
export async function getStaticProps() {
  const data = await fetchData()
  
  return {
    props: { data },
    revalidate: 3600 // ISR - revalidate every hour
  }
}
```

### 2. [[Server Side Rendering]] (SSR)
```typescript
// Server-side rendering for dynamic content
export async function getServerSideProps(context) {
  const data = await fetchUserData(context.req)
  
  return {
    props: { data }
  }
}
```

### 3. Edge Runtime
```typescript
// pages/api/edge-function.js
export const config = {
  runtime: 'edge'
}

export default function handler(req) {
  return new Response(
    JSON.stringify({ message: 'Hello from Edge!' }),
    {
      status: 200,
      headers: { 'Content-Type': 'application/json' }
    }
  )
}
```

### 4. Middleware Optimization
```typescript
// middleware.ts
import { NextResponse } from 'next/server'

export function middleware(request) {
  // Early return untuk static assets
  if (request.nextUrl.pathname.startsWith('/_next/static/')) {
    return NextResponse.next()
  }
  
  // Geolocation-based routing
  const country = request.geo?.country || 'US'
  
  if (country === 'ID' && !request.nextUrl.pathname.startsWith('/id')) {
    return NextResponse.redirect(new URL('/id' + request.nextUrl.pathname, request.url))
  }
  
  return NextResponse.next()
}
```

## Performance Testing Tools

### 1. Lighthouse
```bash
# CLI testing
npm install -g lighthouse
lighthouse https://example.com --output html --output-path ./report.html

# Programmatic testing
const lighthouse = require('lighthouse')
const chromeLauncher = require('chrome-launcher')

const chrome = await chromeLauncher.launch({chromeFlags: ['--headless']})
const options = {logLevel: 'info', output: 'html', port: chrome.port}
const runnerResult = await lighthouse('https://example.com', options)
```

### 2. WebPageTest
```javascript
// WebPageTest API
const WebPageTest = require('webpagetest')
const wpt = new WebPageTest('www.webpagetest.org', 'YOUR_API_KEY')

wpt.runTest('https://example.com', {
  location: 'Dulles:Chrome',
  runs: 3,
  firstViewOnly: false
}, (err, data) => {
  console.log('Test results:', data)
})
```

### 3. Bundle Analyzer
```bash
# Next.js bundle analyzer
npm install --save-dev @next/bundle-analyzer

# next.config.js
const withBundleAnalyzer = require('@next/bundle-analyzer')({
  enabled: process.env.ANALYZE === 'true'
})

module.exports = withBundleAnalyzer({
  // Next.js config
})

# Run analysis
ANALYZE=true npm run build
```

## Performance Budget

### 1. Set Performance Budgets
```json
// lighthouse-budget.json
{
  "resourceSizes": [
    {
      "resourceType": "script",
      "budget": 300
    },
    {
      "resourceType": "image",
      "budget": 500
    }
  ],
  "resourceCounts": [
    {
      "resourceType": "third-party",
      "budget": 10
    }
  ],
  "timings": [
    {
      "metric": "first-contentful-paint",
      "budget": 2000
    }
  ]
}
```

### 2. CI/CD Performance Checks
```yaml
# .github/workflows/performance.yml
name: Performance Check
on: [pull_request]

jobs:
  lighthouse:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run Lighthouse CI
        run: |
          npm install -g @lhci/cli@0.8.x
          lhci autorun
        env:
          LHCI_GITHUB_APP_TOKEN: ${{ secrets.LHCI_GITHUB_APP_TOKEN }}
```

## Advanced Optimization Techniques

### 1. Preloading Strategies
```typescript
// Critical resource preloading
export default function Layout() {
  return (
    <Head>
      {/* Preload critical fonts */}
      <link
        rel="preload"
        href="/fonts/inter-var.woff2"
        as="font"
        type="font/woff2"
        crossOrigin="anonymous"
      />
      
      {/* Preconnect to external domains */}
      <link rel="preconnect" href="https://fonts.googleapis.com" />
      <link rel="preconnect" href="https://api.example.com" />
      
      {/* DNS prefetch for later resources */}
      <link rel="dns-prefetch" href="https://analytics.google.com" />
    </Head>
  )
}
```

### 2. Service Worker Optimization
```javascript
// sw.js - Advanced caching strategies
const CACHE_NAME = 'app-v1'
const STATIC_CACHE = 'static-v1'
const DYNAMIC_CACHE = 'dynamic-v1'

// Cache strategies
const cacheFirst = async (request) => {
  const cache = await caches.open(STATIC_CACHE)
  const cached = await cache.match(request)
  return cached || fetch(request)
}

const networkFirst = async (request) => {
  const cache = await caches.open(DYNAMIC_CACHE)
  try {
    const response = await fetch(request)
    cache.put(request, response.clone())
    return response
  } catch (error) {
    return cache.match(request)
  }
}

// Route-based caching
self.addEventListener('fetch', event => {
  const { request } = event
  
  if (request.destination === 'image') {
    event.respondWith(cacheFirst(request))
  } else if (request.url.includes('/api/')) {
    event.respondWith(networkFirst(request))
  }
})
```

### 3. Memory Optimization
```typescript
// Prevent memory leaks
useEffect(() => {
  const controller = new AbortController()
  
  fetch('/api/data', {
    signal: controller.signal
  }).then(response => {
    // Handle response
  }).catch(error => {
    if (error.name !== 'AbortError') {
      console.error('Fetch error:', error)
    }
  })
  
  return () => {
    controller.abort() // Cleanup on unmount
  }
}, [])

// Optimize large lists with virtualization
import { FixedSizeList as List } from 'react-window'

const VirtualizedList = ({ items }) => (
  <List
    height={600}
    itemCount={items.length}
    itemSize={50}
    itemData={items}
  >
    {({ index, style, data }) => (
      <div style={style}>
        {data[index].name}
      </div>
    )}
  </List>
)
```

## Performance Checklist

### ✅ Loading Performance
- [ ] Optimize images (WebP/AVIF, responsive, lazy loading)
- [ ] Minimize JavaScript bundles
- [ ] Use code splitting
- [ ] Implement proper caching headers
- [ ] Optimize fonts (preload, font-display: swap)
- [ ] Minimize CSS (critical CSS inline)

### ✅ Runtime Performance
- [ ] Avoid long tasks (> 50ms)
- [ ] Optimize React rendering (memo, useMemo, useCallback)
- [ ] Implement virtualization for large lists
- [ ] Use Web Workers for heavy computations
- [ ] Optimize database queries

### ✅ Network Performance
- [ ] Use CDN for static assets
- [ ] Implement HTTP/2 server push
- [ ] Optimize API responses (compression, pagination)
- [ ] Use service workers for caching
- [ ] Minimize third-party scripts

## Kesimpulan

Web Performance optimization adalah proses berkelanjutan yang memerlukan:

1. **Measurement**: Monitor metrics secara konsisten
2. **Optimization**: Implement best practices
3. **Testing**: Regular performance audits
4. **Monitoring**: Real-time performance tracking

**Key takeaways**:
- Focus pada **Core Web Vitals** untuk user experience
- Implement **performance budgets** dalam CI/CD
- Use **[[NextJS]]** built-in optimizations
- Monitor **real user metrics**, bukan hanya lab data

Performance yang baik = Better UX = Higher conversions = Business success

---

**Related Notes:**
- [[NextJS]] - Framework dengan built-in optimizations
- [[Server Side Rendering]] - SSR untuk performance
- [[Static Site Generation]] - SSG untuk speed
- [[App Router]] - Modern routing dengan performance benefits
- [[Pages Router]] - Traditional routing
- [[React Framework]] - Framework considerations
- [[SEO Optimization]] - Performance impact pada SEO

**External Links:**
- [[Web Vitals::https://web.dev/vitals/]]
- [[Lighthouse::https://developers.google.com/web/tools/lighthouse]]
- [[WebPageTest::https://www.webpagetest.org/]]