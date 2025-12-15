---
title: Learn Next.js
categories:
  - "[[Posts]]"
tags:
  - posts
  - nextjs
  - react
  - web-development
  - framework
author:
  - "[[Aes Saputra]]"
url:
created: 2025-12-15
published: 2025-12-15
date: 2025-12-15
topics:
  - web-development
  - react-framework
  - full-stack
status:
  - "[[Published]]"
feed: show
aliases:
  - Next.js
  - NextJS Framework
  - Next Framework
  - Next.js Guide
  - Next.js Tutorial
  - Next.js Development
---
Next.js adalah framework React yang powerful untuk membangun aplikasi web full-stack modern. Panduan ini akan membantu Anda memahami Next.js dari dasar hingga mahir.

## Daftar Isi

1. [[#Pengenalan Next.js|Pengenalan Next.js]]
2. [[#Instalasi dan Setup|Instalasi dan Setup]]
3. [[#Konsep Dasar|Konsep Dasar]]
4. [[#Routing System|Routing System]]
5. [[#Server vs Client Components|Server vs Client Components]]
6. [[#Data Fetching|Data Fetching]]
7. [[#Styling|Styling]]
8. [[#Optimisasi Performance|Optimisasi Performance]]
9. [[#Deployment|Deployment]]
10. [[#Resources dan Tools|Resources dan Tools]]

---

## Pengenalan Next.js

### Apa itu Next.js?

Next.js adalah **[[React Framework|framework React]]** yang menyediakan building blocks untuk membuat aplikasi web yang cepat dan user-friendly. Framework ini menangani tooling dan konfigurasi yang diperlukan untuk React, serta menyediakan struktur, fitur, dan optimisasi tambahan untuk aplikasi Anda.

### Mengapa Memilih Next.js?

- **Zero Configuration**: Setup otomatis untuk bundling, compiling, dan lainnya
- **[[SSR|Server Side Rendering]] (SSR)**: Performa loading yang lebih cepat
- **[[SSG|Static Site Generation]] (SSG)**: Pre-rendering untuk performa optimal
- **API Routes**: Backend functionality dalam satu aplikasi
- **File-based Routing**: Routing otomatis berdasarkan struktur file
- **Built-in Optimizations**: Image, font, dan script optimization

### Arsitektur Monorepo Next.js

Next.js dibangun dengan arsitektur monorepo yang terdiri dari:

```mermaid
graph TD
    A[Next.js Monorepo] --> B[Core Packages]
    A --> C[Build System]
    A --> D[Development Tools]
    A --> E[Testing Infrastructure]
    
    B --> B1[next - Core Framework]
    B --> B2[@next/swc - Compiler]
    B --> B3[@next/font - Font Optimization]
    
    C --> C1[Webpack Integration]
    C --> C2[Turbopack - Next-gen Bundler]
    C --> C3[SWC - Rust Compiler]
```

---

## Instalasi dan Setup

### Membuat Proyek Baru

```bash
# Menggunakan create-next-app (Recommended)
npx create-next-app@latest my-next-app

# Dengan TypeScript
npx create-next-app@latest my-next-app --typescript

# Dengan Tailwind CSS
npx create-next-app@latest my-next-app --tailwind

# Setup lengkap dengan semua opsi
npx create-next-app@latest my-next-app --typescript --tailwind --eslint --app
```

### Struktur Proyek

```
my-next-app/
├── app/                    # App Router (Next.js 13+)
│   ├── globals.css        # Global styles
│   ├── layout.tsx         # Root layout
│   ├── page.tsx          # Home page
│   └── loading.tsx       # Loading UI
├── components/            # Reusable components
├── lib/                  # Utility functions
├── public/               # Static assets
├── styles/               # Additional styles
├── next.config.js        # Next.js configuration
├── package.json
└── tsconfig.json         # TypeScript config
```

### Menjalankan Development Server

```bash
npm run dev
# atau
yarn dev
# atau
pnpm dev

# Server akan berjalan di http://localhost:3000
```

---

## Konsep Dasar

### 1. App Router vs Pages Router

Next.js memiliki dua sistem routing:

| Fitur | App Router (Baru) | Pages Router (Lama) |
|-------|------------------|-------------------|
| **Direktori** | `app/` | `pages/` |
| **Routing** | Folder-based | File-based |
| **Layouts** | `layout.tsx` | Custom `_app.tsx` |
| **Server Components** | ✅ Default | ❌ |
| **Streaming** | ✅ | ❌ |
| **Nested Layouts** | ✅ | ❌ |

> **Rekomendasi**: Gunakan **[[App Router]]** untuk proyek baru

Untuk detail lengkap, lihat:
- [[App Router|App Router]] - Sistem routing terbaru dengan [[RSC|React Server Components]]
- [[Pages Router|Pages Router]] - Sistem routing original yang masih didukung

### 2. File Conventions

Dalam App Router, file khusus memiliki fungsi tertentu:

- `layout.tsx` - Shared UI untuk segment dan children
- `page.tsx` - UI unik untuk route dan membuat route publicly accessible
- `loading.tsx` - Loading UI untuk segment dan children
- `not-found.tsx` - Not found UI untuk segment dan children
- `error.tsx` - Error UI untuk segment dan children
- `global-error.tsx` - Global error UI
- `route.tsx` - Server-side API endpoint

---

## Routing System

### Basic Routing

```typescript
// app/page.tsx - Home page (/)
export default function HomePage() {
  return <h1>Welcome to Next.js!</h1>
}

// app/about/page.tsx - About page (/about)
export default function AboutPage() {
  return <h1>About Us</h1>
}

// app/blog/[slug]/page.tsx - Dynamic route (/blog/my-post)
export default function BlogPost({ params }: { params: { slug: string } }) {
  return <h1>Post: {params.slug}</h1>
}
```

### Nested Routes dan Layouts

```typescript
// app/layout.tsx - Root layout
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>
        <nav>Global Navigation</nav>
        {children}
        <footer>Global Footer</footer>
      </body>
    </html>
  )
}

// app/dashboard/layout.tsx - Dashboard layout
export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <div className="dashboard">
      <aside>Dashboard Sidebar</aside>
      <main>{children}</main>
    </div>
  )
}
```

### Navigation

```typescript
'use client'
import Link from 'next/link'
import { useRouter, usePathname } from 'next/navigation'

export default function Navigation() {
  const router = useRouter()
  const pathname = usePathname()

  return (
    <nav>
      {/* Static link */}
      <Link href="/about">About</Link>
      
      {/* Dynamic link */}
      <Link href={`/blog/${slug}`}>Blog Post</Link>
      
      {/* Programmatic navigation */}
      <button onClick={() => router.push('/dashboard')}>
        Go to Dashboard
      </button>
      
      {/* Active link styling */}
      <Link 
        href="/products" 
        className={pathname === '/products' ? 'active' : ''}
      >
        Products
      </Link>
    </nav>
  )
}
```

---

## Server vs Client Components

### Server Components (Default)

Server Components render di server dan tidak dikirim ke client sebagai JavaScript.

**Keuntungan:**
- Akses langsung ke backend resources (database, file system)
- Keamanan lebih baik (API keys, tokens)
- Bundle size lebih kecil
- SEO friendly

```typescript
// app/posts/page.tsx - Server Component
import { getPosts } from '@/lib/api'

export default async function PostsPage() {
  // Data fetching di server
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

Client Components render di browser dan memungkinkan interaktivitas.

**Kapan menggunakan:**
- Event handlers (`onClick`, `onChange`)
- State dan lifecycle (`useState`, `useEffect`)
- Browser APIs (`localStorage`, `window`)
- Custom hooks

```typescript
'use client'
import { useState, useEffect } from 'react'

export default function LikeButton({ postId }: { postId: string }) {
  const [liked, setLiked] = useState(false)
  const [count, setCount] = useState(0)

  useEffect(() => {
    // Load like status from localStorage
    const savedLike = localStorage.getItem(`like-${postId}`)
    setLiked(savedLike === 'true')
  }, [postId])

  const handleLike = () => {
    setLiked(!liked)
    setCount(prev => liked ? prev - 1 : prev + 1)
    localStorage.setItem(`like-${postId}`, (!liked).toString())
  }

  return (
    <button onClick={handleLike} className="like-button">
      {liked ? '❤️' : '🤍'} {count}
    </button>
  )
}
```

### Composition Pattern

```typescript
// app/blog/[id]/page.tsx - Server Component
import LikeButton from '@/components/LikeButton'
import { getPost } from '@/lib/api'

export default async function BlogPost({ params }: { params: { id: string } }) {
  const post = await getPost(params.id) // Server-side data fetching
  
  return (
    <article>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
      
      {/* Client Component untuk interaktivitas */}
      <LikeButton postId={params.id} />
    </article>
  )
}
```

---

## Data Fetching

### Server-side Data Fetching

```typescript
// Static data fetching
async function getStaticPosts() {
  const res = await fetch('https://api.example.com/posts')
  return res.json()
}

// Dynamic data fetching
async function getDynamicPosts() {
  const res = await fetch('https://api.example.com/posts', {
    cache: 'no-store' // Disable caching
  })
  return res.json()
}

// Revalidated data fetching
async function getRevalidatedPosts() {
  const res = await fetch('https://api.example.com/posts', {
    next: { revalidate: 60 } // Revalidate every 60 seconds
  })
  return res.json()
}
```

### Client-side Data Fetching

```typescript
'use client'
import { useState, useEffect } from 'react'

export default function ClientPosts() {
  const [posts, setPosts] = useState([])
  const [loading, setLoading] = useState(true)

  useEffect(() => {
    async function fetchPosts() {
      try {
        const res = await fetch('/api/posts')
        const data = await res.json()
        setPosts(data)
      } catch (error) {
        console.error('Error fetching posts:', error)
      } finally {
        setLoading(false)
      }
    }

    fetchPosts()
  }, [])

  if (loading) return <div>Loading...</div>

  return (
    <div>
      {posts.map(post => (
        <div key={post.id}>{post.title}</div>
      ))}
    </div>
  )
}
```

### API Routes

```typescript
// app/api/posts/route.ts
import { NextRequest, NextResponse } from 'next/server'

export async function GET(request: NextRequest) {
  try {
    // Fetch data from database
    const posts = await fetchPostsFromDB()
    
    return NextResponse.json(posts)
  } catch (error) {
    return NextResponse.json(
      { error: 'Failed to fetch posts' },
      { status: 500 }
    )
  }
}

export async function POST(request: NextRequest) {
  try {
    const body = await request.json()
    const newPost = await createPost(body)
    
    return NextResponse.json(newPost, { status: 201 })
  } catch (error) {
    return NextResponse.json(
      { error: 'Failed to create post' },
      { status: 500 }
    )
  }
}
```

---

## Styling

### 1. CSS Modules

```css
/* components/Button.module.css */
.button {
  background-color: #0070f3;
  color: white;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 0.25rem;
  cursor: pointer;
}

.button:hover {
  background-color: #0051a2;
}
```

```typescript
// components/Button.tsx
import styles from './Button.module.css'

export default function Button({ children }: { children: React.ReactNode }) {
  return (
    <button className={styles.button}>
      {children}
    </button>
  )
}
```

### 2. Tailwind CSS

```typescript
// Dengan Tailwind CSS
export default function Button({ children }: { children: React.ReactNode }) {
  return (
    <button className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
      {children}
    </button>
  )
}
```

### 3. Styled Components

```typescript
'use client'
import styled from 'styled-components'

const StyledButton = styled.button`
  background-color: #0070f3;
  color: white;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 0.25rem;
  cursor: pointer;

  &:hover {
    background-color: #0051a2;
  }
`

export default function Button({ children }: { children: React.ReactNode }) {
  return <StyledButton>{children}</StyledButton>
}
```

---

## Optimisasi Performance

### 1. Image Optimization

```typescript
import Image from 'next/image'

export default function Gallery() {
  return (
    <div>
      {/* Optimized image */}
      <Image
        src="/hero.jpg"
        alt="Hero image"
        width={800}
        height={600}
        priority // Load immediately
      />
      
      {/* Responsive image */}
      <Image
        src="/gallery/photo1.jpg"
        alt="Gallery photo"
        fill
        sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
      />
    </div>
  )
}
```

### 2. Font Optimization

```typescript
// app/layout.tsx
import { Inter, Roboto_Mono } from 'next/font/google'

const inter = Inter({
  subsets: ['latin'],
  display: 'swap',
})

const robotoMono = Roboto_Mono({
  subsets: ['latin'],
  display: 'swap',
})

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en" className={inter.className}>
      <body>{children}</body>
    </html>
  )
}
```

### 3. Code Splitting dan Lazy Loading

```typescript
import dynamic from 'next/dynamic'

// Lazy load component
const DynamicChart = dynamic(() => import('@/components/Chart'), {
  loading: () => <p>Loading chart...</p>,
  ssr: false // Disable server-side rendering
})

export default function Dashboard() {
  return (
    <div>
      <h1>Dashboard</h1>
      <DynamicChart />
    </div>
  )
}
```

### 4. Caching Strategies

```typescript
// Static caching
fetch('https://api.example.com/data', {
  cache: 'force-cache' // Default behavior
})

// No caching
fetch('https://api.example.com/data', {
  cache: 'no-store'
})

// Time-based revalidation
fetch('https://api.example.com/data', {
  next: { revalidate: 3600 } // Revalidate every hour
})

// Tag-based revalidation
fetch('https://api.example.com/data', {
  next: { tags: ['posts'] }
})
```

---

## Deployment

### 1. Vercel (Recommended)

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Production deployment
vercel --prod
```

### 2. Docker

```dockerfile
# Dockerfile
FROM node:18-alpine AS base

# Install dependencies only when needed
FROM base AS deps
RUN apk add --no-cache libc6-compat
WORKDIR /app

COPY package.json yarn.lock* package-lock.json* pnpm-lock.yaml* ./
RUN \
  if [ -f yarn.lock ]; then yarn --frozen-lockfile; \
  elif [ -f package-lock.json ]; then npm ci; \
  elif [ -f pnpm-lock.yaml ]; then yarn global add pnpm && pnpm i --frozen-lockfile; \
  else echo "Lockfile not found." && exit 1; \
  fi

# Rebuild the source code only when needed
FROM base AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .

RUN yarn build

# Production image, copy all the files and run next
FROM base AS runner
WORKDIR /app

ENV NODE_ENV production

RUN addgroup --system --gid 1001 nodejs
RUN adduser --system --uid 1001 nextjs

COPY --from=builder /app/public ./public

COPY --from=builder --chown=nextjs:nodejs /app/.next/standalone ./
COPY --from=builder --chown=nextjs:nodejs /app/.next/static ./.next/static

USER nextjs

EXPOSE 3000

ENV PORT 3000

CMD ["node", "server.js"]
```

### 3. Static Export

```javascript
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  output: 'export',
  trailingSlash: true,
  images: {
    unoptimized: true
  }
}

module.exports = nextConfig
```

```bash
# Build static export
npm run build

# Files akan ada di folder 'out/'
```

---

## Resources dan Tools

### Dokumentasi dan Learning

- **Official Docs**: [[Next.js Documentation::https://nextjs.org/docs]]
- **Learn Next.js**: [[Next.js Tutorial::https://nextjs.org/learn]]
- **Examples**: [[Next.js Examples::https://github.com/vercel/next.js/tree/canary/examples]]

### Development Tools

- **Next.js DevTools**: Browser extension untuk debugging
- **Vercel Analytics**: Performance monitoring
- **Bundle Analyzer**: Analisis ukuran bundle

```bash
# Install bundle analyzer
npm install --save-dev @next/bundle-analyzer

# Analyze bundle
ANALYZE=true npm run build
```

### Useful Libraries

- **UI Components**: [[Shadcn/ui::https://ui.shadcn.com/]], [[Chakra UI::https://chakra-ui.com/]]
- **Styling**: [[Tailwind CSS::https://tailwindcss.com/]], [[Styled Components::https://styled-components.com/]]
- **State Management**: [[Zustand::https://github.com/pmndrs/zustand]], [[Redux Toolkit::https://redux-toolkit.js.org/]]
- **Forms**: [[React Hook Form::https://react-hook-form.com/]], [[Formik::https://formik.org/]]
- **Database**: [[Prisma::https://www.prisma.io/]], [[Drizzle::https://orm.drizzle.team/]]

### Community

- **Discord**: [[Next.js Discord::https://discord.gg/nextjs]]
- **GitHub**: [[Next.js Repository::https://github.com/vercel/next.js]]
- **Reddit**: [[r/nextjs::https://reddit.com/r/nextjs]]

---

## Tips dan Best Practices

### 1. Performance Tips

- Gunakan `Image` component untuk optimisasi gambar
- Implementasikan lazy loading untuk komponen berat
- Manfaatkan caching strategies yang tepat
- Gunakan Server Components sebanyak mungkin

### 2. SEO Best Practices

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
  }
}
```

### 3. Security

- Gunakan environment variables untuk sensitive data
- Implementasikan proper authentication
- Validate input di server-side
- Gunakan HTTPS di production

### 4. Code Organization

```
src/
├── app/                    # App Router pages
├── components/            # Reusable UI components
│   ├── ui/               # Basic UI components
│   └── features/         # Feature-specific components
├── lib/                  # Utility functions
│   ├── api.ts           # API functions
│   ├── auth.ts          # Authentication logic
│   └── utils.ts         # General utilities
├── hooks/                # Custom React hooks
├── types/                # TypeScript type definitions
└── constants/            # App constants
```

---

## Troubleshooting Common Issues

### 1. Hydration Mismatch

```typescript
// ❌ Problematic
function MyComponent() {
  return <div>{new Date().toLocaleString()}</div>
}

// ✅ Solution
'use client'
import { useState, useEffect } from 'react'

function MyComponent() {
  const [mounted, setMounted] = useState(false)
  
  useEffect(() => {
    setMounted(true)
  }, [])
  
  if (!mounted) return null
  
  return <div>{new Date().toLocaleString()}</div>
}
```

### 2. Import Errors

```typescript
// ❌ Wrong
import { useState } from 'react' // Di Server Component

// ✅ Correct
'use client'
import { useState } from 'react' // Di Client Component
```

### 3. API Route Issues

```typescript
// ❌ Wrong
export default function handler(req, res) {
  // Pages Router syntax di App Router
}

// ✅ Correct
export async function GET(request: NextRequest) {
  // App Router syntax
}
```

---

## Kesimpulan

Next.js adalah framework yang powerful dan fleksibel untuk membangun aplikasi web modern. Dengan memahami konsep-konsep dasar seperti Server/Client Components, routing system, dan data fetching, Anda dapat membangun aplikasi yang performant dan scalable.

**Langkah selanjutnya:**
1. Praktik dengan membuat proyek sederhana
2. Eksplorasi fitur-fitur advanced seperti Middleware dan Edge Runtime
3. Pelajari deployment strategies
4. Bergabung dengan komunitas Next.js

---

**Related Notes:**
- [[React Framework|Framework React]] - Konsep framework React
- [[App Router|App Router]] - Sistem routing terbaru dengan RSC
- [[Pages Router|Pages Router]] - Sistem routing original
- [[SSR|Server Side Rendering]] - SSR implementation
- [[SSG|Static Site Generation]] - SSG implementation  
- [[Web Performance|Performance Optimization]] - Optimasi performa web
- [[SEO Optimization|SEO]] - Search engine optimization
- [[Markdown Guide]] - Format penulisan untuk catatan
- [[deepwiki-guide]] - Tool untuk eksplorasi repository

**External Links:**
- [[Next.js Official Website::https://nextjs.org]]
- [[Vercel Platform::https://vercel.com]]
- [[React Documentation::https://react.dev]]
