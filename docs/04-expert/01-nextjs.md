# 01. Next.js 14+ 🧠

## App Router concepts
- Server Components by default
- Client Components with `'use client'`
- Nested layouts
- Route handlers + server actions

```tsx
// app/page.tsx (Server Component)
export default async function Page() {
  const data = await fetch('https://api.example.com/stats', { cache: 'no-store' }).then(r => r.json());
  return <pre>{JSON.stringify(data, null, 2)}</pre>;
}
```

```tsx
'use client';
import { useState } from 'react';

export function Counter() {
  const [n, setN] = useState(0);
  return <button onClick={() => setN(n + 1)}>{n}</button>;
}
```

## SSR / SSG / ISR
Pick rendering mode by freshness and SEO requirements.

## Image optimization + metadata
Use `next/image` and `generateMetadata` for performance + discoverability.

## When to use Next.js
- Full-stack React apps, SEO-heavy products, hybrid rendering

## When NOT to use
- Pure client-only apps with no SEO/server needs
