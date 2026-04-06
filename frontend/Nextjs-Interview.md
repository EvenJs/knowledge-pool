### Q: What makes Next.js different from a normal React app?

> React itself only handles the UI — it runs entirely in the browser. Next.js adds server-side rendering (SSR), file-based routing, and data-fetching on the server, so you can pre-render pages for SEO and speed.
>
> For example, a blog built with plain React might show a blank page until data loads. With Next.js, you can fetch that data on the server so Google and users instantly see content.
>
> In short: React handles the “how it looks,” while Next.js handles “how it loads.”

### Q: What’s the difference between Server Components and Client Components?

> Server Components run on the server — they don’t ship any JavaScript to the browser. That means faster page loads and smaller bundles.
>
> Client Components run in the browser and can use state, effects, and browser APIs.

```typescript
// Server Component
export default function Home() { return <Header /> }

// Client Component
"use client";
import { useState } from "react";
```

> Think of it like this: use Server Components by default, and only add "use client" where interactivity is needed (like a button or modal).
>
> It’s a nice balance between static and dynamic rendering — fast, but still up-to-date.

### Q: How does data fetching work in the new App Router?

> In the App Router, you can fetch data directly inside a Server Component using the built-in fetch. It feels like normal async code — no getServerSideProps or getStaticProps.

```typescript
async function Page() {
  const res = await fetch('https://api.example.com/posts', { next: { revalidate: 60 }});
  const posts = await res.json();
  return posts.map(p => <p key={p.id}>{p.title}</p>);
}
```

> The revalidate option lets Next.js automatically refresh that data every 60 seconds.

### Q: What’s the difference between SSR, SSG, and ISR in Next.js?

> - SSR (Server-Side Rendering): The page is built every time someone visits. Great for dashboards or personalized content.
> - SSG (Static Site Generation): The page is built once at build time. Best for blogs or docs.
> - ISR (Incremental Static Regeneration): A hybrid — it pre-renders like SSG but quietly rebuilds pages in the background after a certain time.
> - For example, if you set revalidate: 60, it regenerates the page every minute so users get fresh content without a full rebuild.

### Q: How do API routes work in Next.js?

> You can build backend endpoints right inside your Next.js app — no separate server needed.
>
> In the App Router, create a file like app/api/hello/route.ts:

```typescript
export async function GET() {
  return Response.json({ message: "Hello from API" });
}
```

> This gives you /api/hello. It’s handy for quick APIs, form submissions, or server actions without spinning up Express.
>
> Under the hood, it’s just a lightweight serverless function.

### Q: How would you implement authentication in Next.js?

> **There are a few patterns:**
>
> - Use NextAuth (Auth.js) for OAuth or credentials-based login.
> - Protect routes using Middleware to check cookies before rendering.
> - Fetch session data server-side for SSR pages.

```typescript
import { NextResponse } from "next/server";
export function middleware(req) {
  const token = req.cookies.get("auth");
  if (!token) return NextResponse.redirect("/login");
}
```

### Q: What are Layouts in the App Router, and why are they useful?

> Layouts let you share UI and state across pages — like navigation bars or side menus — without re-rendering them.
>
> For example, app/layout.tsx wraps everything in your app:

```typescript
export default function Layout({ children }) {
  return <html><body><Navbar />{children}</body></html>;
}
```

> You can even nest layouts (e.g., a dashboard layout that only wraps certain routes). It feels like React composition but built into the routing system — faster and cleaner than re-mounting components on every route change.

### Q: How would you handle errors and loading states in Next.js?

> Next.js has built-in file conventions for this:
>
> error.tsx → renders if something throws in that route.
>
> loading.tsx → shows while data or components are loading.
>
> Example:

```typescript
// app/dashboard/loading.tsx
export default function Loading() { return <p>Loading...</p>; }
```

### Q: How does caching work in Next.js fetch calls?

> By default, Next.js caches the response of fetch calls in Server Components for performance.
>
> You can control it using:
>
> - cache: 'no-store' → always fetch fresh data

> - next: { revalidate: 30 } → ISR caching

```typescript
await fetch("/api/data", { cache: "no-store" });
```

### Q: How would you improve performance in a large Next.js app?

> Some practical things interviewers love hearing:
>
> - Keep most components as Server Components to reduce bundle size.
> - Use next/image for automatic image optimization.
> - Split large components using next/dynamic() lazy loading.
> - Avoid heavy libraries in the client.

```typescript
const Chart = dynamic(() => import("./Chart"), { ssr: false });
```
