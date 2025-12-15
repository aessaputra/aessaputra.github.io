---
title: Next.js Pages Router
categories:
  - "[[Posts]]"
tags:
  - posts
  - nextjs
  - pages-router
  - routing
author:
  - "[[Aes Saputra]]"
url:
created: 2025-12-15
published: 2025-12-15
date: 2025-12-15
topics:
  - nextjs-routing
  - legacy-routing
  - web-development
status: published
feed: show
aliases:
  - Pages Router
  - Next.js Pages Router
  - Pages Directory
  - Legacy Router
  - getStaticProps
  - getServerSideProps
  - getStaticPaths
---

# Next.js Pages Router

Pages Router adalah sistem routing original di [[NextJS|Next.js]] yang menggunakan direktori `pages/` untuk mendefinisikan routes. Meskipun [[App Router|App Router]] adalah sistem yang lebih baru, Pages Router masih didukung dan banyak digunakan untuk implementasi [[SSR]] dan [[SSG]].

## Apa itu Pages Router?

Pages Router menggunakan file-based routing dimana setiap file di direktori `pages/` secara otomatis menjadi route. Sistem ini sederhana dan mudah dipahami untuk developer yang baru mengenal Next.js.

### Struktur Dasar Pages Router

```
pages/
├── _app.tsx           # Custom App component
├── _document.tsx      # Custom Document
├── index.tsx          # Home page (/)
├── about.tsx          # /about
├── contact.tsx        # /contact
├── blog/
│   ├── index.tsx      # /blog
│   └── [slug].tsx     # /blog/[slug]
├── api/
│   ├── hello.ts       # /api/hello
│   └── users/
│       └── [id].ts    # /api/users/[id]
└── 404.tsx            # Custom 404 page
```

## File Conventions

### 1. Basic Pages
```typescript
// pages/index.tsx - Home Page
export default function HomePage() {
  return (
    <div>
      <h1>Welcome to Next.js</h1>
      <p>This is the home page</p>
    </div>
  )
}

// pages/about.tsx - About Page
export default function AboutPage() {
  return (
    <div>
      <h1>About Us</h1>
      <p>Learn more about our company</p>
    </div>
  )
}
```

### 2. Custom App (_app.tsx)
```typescript
// pages/_app.tsx
import type { AppProps } from 'next/app'
import '../styles/globals.css'

export default function MyApp({ Component, pageProps }: AppProps) {
  return (
    <div>
      <header>Global Header</header>
      <main>
        <Component {...pageProps} />
      </main>
      <footer>Global Footer</footer>
    </div>
  )
}
```

### 3. Custom Document (_document.tsx)
```typescript
// pages/_document.tsx
import { Html, Head, Main, NextScript } from 'next/document'

export default function Document() {
  return (
    <Html lang="en">
      <Head>
        <link rel="icon" href="/favicon.ico" />
      </Head>
      <body>
        <Main />
        <NextScript />
      </body>
    </Html>
  )
}
```

### 4. Custom 404 Page
```typescript
// pages/404.tsx
export default function Custom404() {
  return (
    <div>
      <h1>404 - Page Not Found</h1>
      <p>The page you are looking for does not exist.</p>
    </div>
  )
}
```

## Dynamic Routes

### 1. Single Dynamic Route
```typescript
// pages/blog/[slug].tsx
import { useRouter } from 'next/router'

export default function BlogPost() {
  const router = useRouter()
  const { slug } = router.query
  
  return (
    <article>
      <h1>Blog Post: {slug}</h1>
    </article>
  )
}

// Matches:
// /blog/hello-world
// /blog/nextjs-tutorial
```

### 2. Catch-all Routes
```typescript
// pages/shop/[...slug].tsx
import { useRouter } from 'next/router'

export default function ShopPage() {
  const router = useRouter()
  const { slug } = router.query
  
  return (
    <div>
      <h1>Shop</h1>
      <p>Category: {Array.isArray(slug) ? slug.join('/') : slug}</p>
    </div>
  )
}

// Matches:
// /shop/clothing
// /shop/clothing/shirts
// /shop/clothing/shirts/casual
```

### 3. Optional Catch-all Routes
```typescript
// pages/docs/[[...slug]].tsx
import { useRouter } from 'next/router'

export default function DocsPage() {
  const router = useRouter()
  const { slug } = router.query
  
  if (!slug) {
    return <div>Documentation Home</div>
  }
  
  return (
    <div>
      <h1>Docs: {Array.isArray(slug) ? slug.join('/') : slug}</h1>
    </div>
  )
}

// Matches:
// /docs (slug is undefined)
// /docs/getting-started
// /docs/api/reference
```
## Data Fetching Methods

Pages Router menyediakan tiga method utama untuk data fetching:

### 1. getStaticProps (SSG)
```typescript
// pages/blog/index.tsx
import { GetStaticProps } from 'next'

interface Props {
  posts: Post[]
}

export default function BlogPage({ posts }: Props) {
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

export const getStaticProps: GetStaticProps = async () => {
  const posts = await fetchPosts()
  
  return {
    props: {
      posts
    },
    revalidate: 3600 // ISR - revalidate every hour
  }
}
```

### 2. getServerSideProps (SSR)
```typescript
// pages/dashboard.tsx
import { GetServerSideProps } from 'next'

interface Props {
  user: User
  data: DashboardData
}

export default function DashboardPage({ user, data }: Props) {
  return (
    <div>
      <h1>Welcome, {user.name}</h1>
      <div>Last login: {data.lastLogin}</div>
    </div>
  )
}

export const getServerSideProps: GetServerSideProps = async (context) => {
  // Check authentication
  const session = await getSession(context.req)
  
  if (!session) {
    return {
      redirect: {
        destination: '/login',
        permanent: false
      }
    }
  }
  
  // Fetch user-specific data
  const [user, data] = await Promise.all([
    fetchUser(session.userId),
    fetchDashboardData(session.userId)
  ])
  
  return {
    props: {
      user,
      data
    }
  }
}
```

### 3. getStaticPaths (untuk Dynamic SSG)
```typescript
// pages/blog/[slug].tsx
import { GetStaticProps, GetStaticPaths } from 'next'

interface Props {
  post: Post
}

export default function BlogPost({ post }: Props) {
  return (
    <article>
      <h1>{post.title}</h1>
      <div dangerouslySetInnerHTML={{ __html: post.content }} />
    </article>
  )
}

export const getStaticPaths: GetStaticPaths = async () => {
  const posts = await fetchPosts()
  
  const paths = posts.map(post => ({
    params: { slug: post.slug }
  }))
  
  return {
    paths,
    fallback: 'blocking' // or false, true
  }
}

export const getStaticProps: GetStaticProps = async ({ params }) => {
  const post = await fetchPost(params?.slug as string)
  
  if (!post) {
    return {
      notFound: true
    }
  }
  
  return {
    props: {
      post
    },
    revalidate: 300 // 5 minutes
  }
}
```

## API Routes

Pages Router memungkinkan pembuatan API endpoints:

### 1. Basic API Route
```typescript
// pages/api/hello.ts
import type { NextApiRequest, NextApiResponse } from 'next'

type Data = {
  message: string
}

export default function handler(
  req: NextApiRequest,
  res: NextApiResponse<Data>
) {
  res.status(200).json({ message: 'Hello from Next.js API!' })
}
```

### 2. Dynamic API Route
```typescript
// pages/api/users/[id].ts
import type { NextApiRequest, NextApiResponse } from 'next'

export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  const { id } = req.query
  
  if (req.method === 'GET') {
    try {
      const user = await fetchUser(id as string)
      res.status(200).json(user)
    } catch (error) {
      res.status(404).json({ error: 'User not found' })
    }
  } else if (req.method === 'PUT') {
    try {
      const updatedUser = await updateUser(id as string, req.body)
      res.status(200).json(updatedUser)
    } catch (error) {
      res.status(400).json({ error: 'Failed to update user' })
    }
  } else {
    res.setHeader('Allow', ['GET', 'PUT'])
    res.status(405).end(`Method ${req.method} Not Allowed`)
  }
}
```

### 3. Catch-all API Route
```typescript
// pages/api/[...params].ts
import type { NextApiRequest, NextApiResponse } from 'next'

export default function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  const { params } = req.query
  
  // params is an array: ['users', '123', 'posts']
  // for URL: /api/users/123/posts
  
  console.log('API path:', params)
  
  res.status(200).json({
    path: params,
    method: req.method
  })
}
```

## Navigation dan Routing

### 1. Link Component
```typescript
import Link from 'next/link'

export default function Navigation() {
  return (
    <nav>
      <Link href="/">
        <a>Home</a>
      </Link>
      <Link href="/about">
        <a>About</a>
      </Link>
      <Link href="/blog/my-first-post">
        <a>My First Post</a>
      </Link>
    </nav>
  )
}
```

### 2. useRouter Hook
```typescript
import { useRouter } from 'next/router'
import { useEffect } from 'react'

export default function MyComponent() {
  const router = useRouter()
  
  // Programmatic navigation
  const handleClick = () => {
    router.push('/dashboard')
  }
  
  // Access query parameters
  useEffect(() => {
    if (router.isReady) {
      console.log('Query:', router.query)
      console.log('Pathname:', router.pathname)
    }
  }, [router.isReady, router.query])
  
  return (
    <div>
      <button onClick={handleClick}>Go to Dashboard</button>
      <p>Current path: {router.asPath}</p>
    </div>
  )
}
```

### 3. Router Events
```typescript
import { useRouter } from 'next/router'
import { useEffect } from 'react'

export default function MyApp({ Component, pageProps }) {
  const router = useRouter()
  
  useEffect(() => {
    const handleStart = (url) => {
      console.log(`Loading: ${url}`)
    }
    
    const handleComplete = (url) => {
      console.log(`Finished loading: ${url}`)
    }
    
    router.events.on('routeChangeStart', handleStart)
    router.events.on('routeChangeComplete', handleComplete)
    
    return () => {
      router.events.off('routeChangeStart', handleStart)
      router.events.off('routeChangeComplete', handleComplete)
    }
  }, [router])
  
  return <Component {...pageProps} />
}
```

## Middleware (Pages Router)

```typescript
// middleware.ts (root level)
import { NextResponse } from 'next/server'
import type { NextRequest } from 'next/server'

export function middleware(request: NextRequest) {
  // Check authentication for protected routes
  if (request.nextUrl.pathname.startsWith('/dashboard')) {
    const token = request.cookies.get('auth-token')
    
    if (!token) {
      return NextResponse.redirect(new URL('/login', request.url))
    }
  }
  
  // Add custom headers
  const response = NextResponse.next()
  response.headers.set('x-custom-header', 'my-value')
  
  return response
}

export const config = {
  matcher: ['/dashboard/:path*', '/api/:path*']
}
```

## Error Handling

### 1. Custom Error Page
```typescript
// pages/_error.tsx
import { NextPageContext } from 'next'

interface Props {
  statusCode?: number
}

function Error({ statusCode }: Props) {
  return (
    <div>
      <h1>
        {statusCode
          ? `An ${statusCode} error occurred on server`
          : 'An error occurred on client'}
      </h1>
    </div>
  )
}

Error.getInitialProps = ({ res, err }: NextPageContext) => {
  const statusCode = res ? res.statusCode : err ? err.statusCode : 404
  return { statusCode }
}

export default Error
```

### 2. Error Boundaries
```typescript
// components/ErrorBoundary.tsx
import React from 'react'

interface State {
  hasError: boolean
}

class ErrorBoundary extends React.Component<
  React.PropsWithChildren<{}>,
  State
> {
  constructor(props: React.PropsWithChildren<{}>) {
    super(props)
    this.state = { hasError: false }
  }
  
  static getDerivedStateFromError(error: Error): State {
    return { hasError: true }
  }
  
  componentDidCatch(error: Error, errorInfo: React.ErrorInfo) {
    console.error('Error caught by boundary:', error, errorInfo)
  }
  
  render() {
    if (this.state.hasError) {
      return (
        <div>
          <h2>Something went wrong.</h2>
          <button onClick={() => this.setState({ hasError: false })}>
            Try again
          </button>
        </div>
      )
    }
    
    return this.props.children
  }
}

export default ErrorBoundary
```

## Performance Optimization

### 1. Dynamic Imports
```typescript
import dynamic from 'next/dynamic'

// Lazy load component
const DynamicChart = dynamic(() => import('../components/Chart'), {
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

### 2. Image Optimization
```typescript
import Image from 'next/image'

export default function Gallery() {
  return (
    <div>
      <Image
        src="/hero.jpg"
        alt="Hero image"
        width={800}
        height={600}
        priority
        placeholder="blur"
        blurDataURL="data:image/jpeg;base64,..."
      />
    </div>
  )
}
```

### 3. Font Optimization
```typescript
// pages/_app.tsx
import { Inter } from 'next/font/google'

const inter = Inter({ subsets: ['latin'] })

export default function MyApp({ Component, pageProps }) {
  return (
    <div className={inter.className}>
      <Component {...pageProps} />
    </div>
  )
}
```

## Pages Router vs App Router

| Feature | Pages Router | [[App Router]] |
|---------|--------------|----------------|
| **Routing** | File-based | Folder-based |
| **Layouts** | `_app.tsx` | `layout.tsx` |
| **Data Fetching** | `getStaticProps`, `getServerSideProps` | `fetch()` in components |
| **Server Components** | ❌ | ✅ Default |
| **Streaming** | ❌ | ✅ |
| **Nested Layouts** | ❌ | ✅ |
| **Error Handling** | `_error.tsx` | `error.tsx` |
| **Loading States** | Custom | `loading.tsx` |

## Migration ke App Router

### 1. File Structure Migration
```typescript
// Pages Router → App Router
pages/index.tsx          → app/page.tsx
pages/about.tsx          → app/about/page.tsx
pages/blog/[slug].tsx    → app/blog/[slug]/page.tsx
pages/_app.tsx           → app/layout.tsx
pages/_document.tsx      → app/layout.tsx (merged)
```

### 2. Data Fetching Migration
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

### 1. Code Organization
```
pages/
├── api/              # API routes
├── _app.tsx         # Global app component
├── _document.tsx    # Custom document
├── index.tsx        # Home page
└── [feature]/       # Feature-based organization
    ├── index.tsx
    └── [id].tsx

components/
├── common/          # Shared components
├── layout/          # Layout components
└── [feature]/       # Feature-specific components
```

### 2. TypeScript Integration
```typescript
import type { NextPage } from 'next'
import type { GetServerSideProps } from 'next'

interface Props {
  data: MyData
}

const MyPage: NextPage<Props> = ({ data }) => {
  return <div>{data.title}</div>
}

export const getServerSideProps: GetServerSideProps<Props> = async () => {
  const data = await fetchData()
  
  return {
    props: { data }
  }
}

export default MyPage
```

## Kesimpulan

Pages Router adalah sistem routing yang mature dan stabil di Next.js. Meskipun [[App Router]] menawarkan fitur-fitur yang lebih modern, Pages Router masih:

- **Cocok untuk aplikasi existing** yang sudah stabil
- **Mudah dipahami** untuk developer baru
- **Fully supported** dan akan terus di-maintain
- **Production-ready** dengan track record yang proven

**Gunakan Pages Router ketika**:
- Migrasi dari aplikasi existing
- Tim belum familiar dengan React Server Components
- Butuh stability dan predictability
- Aplikasi tidak memerlukan fitur advanced App Router

---

**Related Notes:**
- [[NextJS|Next.js]] - Framework utama
- [[App Router|App Router]] - Sistem routing baru
- [[getServerSideProps|SSR]] - Server Side Rendering implementation
- [[getStaticProps|SSG]] - Static Site Generation implementation
- [[Web Performance|Performance]] - Optimasi performa
- [[SEO Optimization|SEO]] - Search engine optimization

**External Links:**
- [[Pages Router Documentation::https://nextjs.org/docs/pages]]
- [[Migration Guide::https://nextjs.org/docs/app/building-your-application/upgrading/app-router-migration]]
- [[Next.js API Routes::https://nextjs.org/docs/pages/building-your-application/routing/api-routes]]