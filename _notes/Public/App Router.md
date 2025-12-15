---
title: Next.js App Router
categories:
  - "[[Posts]]"
tags:
  - posts
  - nextjs
  - app-router
  - routing
author:
  - "[[Aes Saputra]]"
url:
created: 2025-12-15
published: 2025-12-15
date: 2025-12-15
topics:
  - nextjs-routing
  - react-server-components
  - web-development
status: published
feed: show
aliases:
  - App Router
  - Next.js App Router
  - App Directory
  - Next 13 Router
  - React Server Components
  - RSC
  - App Dir
---

App Router adalah sistem routing terbaru di [[NextJS]] yang diperkenalkan di versi 13, menggantikan [[Pages Router]]. App Router dibangun di atas React Server Components dan menyediakan fitur-fitur modern untuk aplikasi web.

## Apa itu App Router?

App Router menggunakan direktori `app/` untuk mendefinisikan routes dan layouts. Sistem ini mendukung:
- **React Server Components** by default
- **Nested layouts** dan **nested routing**
- **Streaming** dan **Suspense**
- **Built-in SEO support**
- **Advanced routing patterns**

### Struktur Dasar App Router

```
app/
├── layout.tsx          # Root layout (required)
├── page.tsx           # Home page (/)
├── loading.tsx        # Loading UI
├── error.tsx          # Error UI
├── not-found.tsx      # 404 page
├── about/
│   └── page.tsx       # /about
├── blog/
│   ├── layout.tsx     # Blog layout
│   ├── page.tsx       # /blog
│   └── [slug]/
│       └── page.tsx   # /blog/[slug]
└── dashboard/
    ├── layout.tsx     # Dashboard layout
    ├── page.tsx       # /dashboard
    ├── settings/
    │   └── page.tsx   # /dashboard/settings
    └── analytics/
        └── page.tsx   # /dashboard/analytics
```

## File Conventions

App Router menggunakan file khusus dengan fungsi tertentu:

### 1. layout.tsx
```typescript
// app/layout.tsx - Root Layout (Required)
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>
        <header>Global Header</header>
        <main>{children}</main>
        <footer>Global Footer</footer>
      </body>
    </html>
  )
}
```

### 2. page.tsx
```typescript
// app/page.tsx - Home Page
export default function HomePage() {
  return (
    <div>
      <h1>Welcome to Next.js App Router</h1>
      <p>This is the home page</p>
    </div>
  )
}

// app/about/page.tsx - About Page
export default function AboutPage() {
  return (
    <div>
      <h1>About Us</h1>
      <p>Learn more about our company</p>
    </div>
  )
}
```

### 3. loading.tsx
```typescript
// app/loading.tsx - Global Loading UI
export default function Loading() {
  return (
    <div className="flex items-center justify-center min-h-screen">
      <div className="animate-spin rounded-full h-32 w-32 border-b-2 border-gray-900"></div>
    </div>
  )
}

// app/dashboard/loading.tsx - Dashboard Loading UI
export default function DashboardLoading() {
  return (
    <div className="dashboard-loading">
      <div className="skeleton-header"></div>
      <div className="skeleton-content"></div>
    </div>
  )
}
```
### 4. error.tsx
```typescript
// app/error.tsx - Global Error UI
'use client'
import { useEffect } from 'react'

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string }
  reset: () => void
}) {
  useEffect(() => {
    console.error(error)
  }, [error])

  return (
    <div className="error-container">
      <h2>Something went wrong!</h2>
      <button onClick={() => reset()}>
        Try again
      </button>
    </div>
  )
}
```

### 5. not-found.tsx
```typescript
// app/not-found.tsx - 404 Page
import Link from 'next/link'

export default function NotFound() {
  return (
    <div className="not-found">
      <h2>Not Found</h2>
      <p>Could not find requested resource</p>
      <Link href="/">Return Home</Link>
    </div>
  )
}
```

## Dynamic Routes

### 1. Single Dynamic Segment
```typescript
// app/blog/[slug]/page.tsx
export default function BlogPost({ params }: { params: { slug: string } }) {
  return (
    <article>
      <h1>Blog Post: {params.slug}</h1>
    </article>
  )
}

// Generates routes like:
// /blog/hello-world
// /blog/nextjs-tutorial
```

### 2. Catch-all Routes
```typescript
// app/shop/[...slug]/page.tsx
export default function ShopPage({ params }: { params: { slug: string[] } }) {
  return (
    <div>
      <h1>Shop</h1>
      <p>Category path: {params.slug.join('/')}</p>
    </div>
  )
}

// Generates routes like:
// /shop/clothing
// /shop/clothing/shirts
// /shop/clothing/shirts/casual
```

### 3. Optional Catch-all Routes
```typescript
// app/docs/[[...slug]]/page.tsx
export default function DocsPage({ params }: { params: { slug?: string[] } }) {
  if (!params.slug) {
    return <div>Documentation Home</div>
  }
  
  return (
    <div>
      <h1>Docs: {params.slug.join('/')}</h1>
    </div>
  )
}

// Matches:
// /docs (slug is undefined)
// /docs/getting-started
// /docs/api/reference
```

## Nested Layouts

App Router memungkinkan nested layouts yang powerful:

```typescript
// app/layout.tsx - Root Layout
export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <nav>Global Navigation</nav>
        {children}
      </body>
    </html>
  )
}

// app/dashboard/layout.tsx - Dashboard Layout
export default function DashboardLayout({ children }) {
  return (
    <div className="dashboard">
      <aside>
        <nav>Dashboard Navigation</nav>
      </aside>
      <main>{children}</main>
    </div>
  )
}

// app/dashboard/settings/layout.tsx - Settings Layout
export default function SettingsLayout({ children }) {
  return (
    <div className="settings">
      <div className="settings-sidebar">
        <nav>Settings Navigation</nav>
      </div>
      <div className="settings-content">
        {children}
      </div>
    </div>
  )
}
```

## Server Components vs Client Components

### Server Components (Default)
```typescript
// app/posts/page.tsx - Server Component
async function getPosts() {
  const res = await fetch('https://api.example.com/posts')
  return res.json()
}

export default async function PostsPage() {
  const posts = await getPosts()
  
  return (
    <div>
      <h1>Blog Posts</h1>
      {posts.map(post => (
        <article key={post.id}>
          <h2>{post.title}</h2>
          <p>{post.excerpt}</p>
        </article>
      ))}
    </div>
  )
}
```

### Client Components
```typescript
// app/components/SearchBox.tsx - Client Component
'use client'
import { useState } from 'react'

export default function SearchBox() {
  const [query, setQuery] = useState('')
  
  return (
    <div>
      <input
        type="text"
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        placeholder="Search..."
      />
      <button onClick={() => console.log('Searching:', query)}>
        Search
      </button>
    </div>
  )
}
```

## Data Fetching

### 1. Server-side Data Fetching
```typescript
// app/products/page.tsx
async function getProducts() {
  const res = await fetch('https://api.example.com/products', {
    cache: 'force-cache' // Static generation
  })
  return res.json()
}

export default async function ProductsPage() {
  const products = await getProducts()
  
  return (
    <div>
      {products.map(product => (
        <div key={product.id}>{product.name}</div>
      ))}
    </div>
  )
}
```

### 2. Dynamic Data Fetching
```typescript
// app/dashboard/page.tsx
async function getDashboardData() {
  const res = await fetch('https://api.example.com/dashboard', {
    cache: 'no-store' // Always fresh data
  })
  return res.json()
}

export default async function DashboardPage() {
  const data = await getDashboardData()
  
  return (
    <div>
      <h1>Dashboard</h1>
      <p>Last updated: {data.lastUpdated}</p>
    </div>
  )
}
```

### 3. Revalidated Data Fetching
```typescript
// app/news/page.tsx
async function getNews() {
  const res = await fetch('https://api.example.com/news', {
    next: { revalidate: 300 } // Revalidate every 5 minutes
  })
  return res.json()
}

export default async function NewsPage() {
  const news = await getNews()
  
  return (
    <div>
      {news.map(article => (
        <article key={article.id}>
          <h2>{article.title}</h2>
        </article>
      ))}
    </div>
  )
}
```

## Route Groups

Route groups memungkinkan organisasi routes tanpa mempengaruhi URL:

```
app/
├── (marketing)/
│   ├── about/
│   │   └── page.tsx     # /about
│   └── contact/
│       └── page.tsx     # /contact
├── (shop)/
│   ├── products/
│   │   └── page.tsx     # /products
│   └── cart/
│       └── page.tsx     # /cart
└── (auth)/
    ├── login/
    │   └── page.tsx     # /login
    └── register/
        └── page.tsx     # /register
```

### Multiple Root Layouts
```typescript
// app/(marketing)/layout.tsx
export default function MarketingLayout({ children }) {
  return (
    <div className="marketing-layout">
      <nav>Marketing Navigation</nav>
      {children}
    </div>
  )
}

// app/(shop)/layout.tsx
export default function ShopLayout({ children }) {
  return (
    <div className="shop-layout">
      <nav>Shop Navigation</nav>
      {children}
    </div>
  )
}
```

## Parallel Routes

Parallel routes memungkinkan rendering multiple pages dalam layout yang sama:

```
app/
├── layout.tsx
├── page.tsx
├── @analytics/
│   └── page.tsx
├── @team/
│   └── page.tsx
└── @dashboard/
    └── page.tsx
```

```typescript
// app/layout.tsx
export default function Layout({
  children,
  analytics,
  team,
  dashboard,
}: {
  children: React.ReactNode
  analytics: React.ReactNode
  team: React.ReactNode
  dashboard: React.ReactNode
}) {
  return (
    <div>
      {children}
      <div className="grid grid-cols-2 gap-4">
        <div>{analytics}</div>
        <div>{team}</div>
      </div>
      <div>{dashboard}</div>
    </div>
  )
}
```

## Intercepting Routes

Intercepting routes memungkinkan loading route dalam context current page:

```
app/
├── feed/
│   ├── page.tsx
│   └── (..)photo/
│       └── [id]/
│           └── page.tsx
└── photo/
    └── [id]/
        └── page.tsx
```

```typescript
// app/feed/(..)photo/[id]/page.tsx - Modal view
export default function PhotoModal({ params }) {
  return (
    <div className="modal">
      <div className="modal-content">
        <img src={`/photos/${params.id}.jpg`} alt="Photo" />
      </div>
    </div>
  )
}

// app/photo/[id]/page.tsx - Full page view
export default function PhotoPage({ params }) {
  return (
    <div className="photo-page">
      <img src={`/photos/${params.id}.jpg`} alt="Photo" />
    </div>
  )
}
```

## Metadata API

App Router menyediakan API untuk SEO metadata:

```typescript
// app/blog/[slug]/page.tsx
import { Metadata } from 'next'

export async function generateMetadata({ params }): Promise<Metadata> {
  const post = await getPost(params.slug)
  
  return {
    title: post.title,
    description: post.excerpt,
    openGraph: {
      title: post.title,
      description: post.excerpt,
      images: [post.image],
    },
    twitter: {
      card: 'summary_large_image',
      title: post.title,
      description: post.excerpt,
      images: [post.image],
    },
  }
}

export default async function BlogPost({ params }) {
  const post = await getPost(params.slug)
  
  return (
    <article>
      <h1>{post.title}</h1>
      <div dangerouslySetInnerHTML={{ __html: post.content }} />
    </article>
  )
}
```

## Migration dari Pages Router

### 1. Struktur File
```typescript
// Pages Router
pages/
├── index.tsx          → app/page.tsx
├── about.tsx          → app/about/page.tsx
├── blog/
│   ├── index.tsx      → app/blog/page.tsx
│   └── [slug].tsx     → app/blog/[slug]/page.tsx
└── _app.tsx           → app/layout.tsx
```

### 2. Data Fetching
```typescript
// Pages Router
export async function getServerSideProps() {
  const data = await fetchData()
  return { props: { data } }
}

// App Router
async function getData() {
  const res = await fetch('...')
  return res.json()
}

export default async function Page() {
  const data = await getData()
  return <div>{data}</div>
}
```

## Best Practices

### 1. Component Organization
```
app/
├── components/        # Shared components
│   ├── ui/           # Basic UI components
│   └── features/     # Feature components
├── lib/              # Utilities
├── hooks/            # Custom hooks
└── types/            # TypeScript types
```

### 2. Error Handling
```typescript
// app/dashboard/error.tsx
'use client'

export default function DashboardError({
  error,
  reset,
}: {
  error: Error & { digest?: string }
  reset: () => void
}) {
  return (
    <div className="error-container">
      <h2>Dashboard Error</h2>
      <p>{error.message}</p>
      <button onClick={reset}>Try again</button>
    </div>
  )
}
```

### 3. Loading States
```typescript
// app/dashboard/loading.tsx
export default function DashboardLoading() {
  return (
    <div className="animate-pulse">
      <div className="h-8 bg-gray-200 rounded mb-4"></div>
      <div className="h-64 bg-gray-200 rounded"></div>
    </div>
  )
}
```

## Kesimpulan

App Router adalah evolusi besar dalam Next.js yang membawa:
- **Better developer experience** dengan file conventions
- **Improved performance** dengan Server Components
- **Enhanced SEO** dengan built-in metadata API
- **More flexible routing** dengan nested layouts

**Migrasi ke App Router direkomendasikan untuk**:
- Proyek baru
- Aplikasi yang butuh SEO optimal
- Tim yang ingin leverage React Server Components
- Aplikasi dengan complex routing needs

---

**Related Notes:**
- [[NextJS]] - Framework utama
- [[Pages Router]] - Sistem routing lama
- [[Server Side Rendering]] - Rendering strategy
- [[React Framework]] - Konsep framework React

**External Links:**
- [[App Router Documentation::https://nextjs.org/docs/app]]
- [[React Server Components::https://react.dev/blog/2023/03/22/react-labs-what-we-have-been-working-on-march-2023#react-server-components]]
- [[Next.js Migration Guide::https://nextjs.org/docs/app/building-your-application/upgrading/app-router-migration]]