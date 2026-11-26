# 02. Performance Optimization ⚡

## Key tools
- `React.memo`
- `useMemo` / `useCallback`
- Code splitting with `lazy` + `Suspense`
- Profiler for measurement
- Virtualization (`react-window`)

```jsx
import { memo, useMemo } from 'react';

const ProductRow = memo(function ProductRow({ product }) {
  return <li>{product.name}</li>;
});

export function ProductList({ products, query }) {
  const filtered = useMemo(
    () => products.filter(p => p.name.toLowerCase().includes(query.toLowerCase())),
    [products, query]
  );
  return <ul>{filtered.map(p => <ProductRow key={p.id} product={p} />)}</ul>;
}
```

## When to optimize
- Confirmed slow renders, long lists, heavy calculations

## When NOT to optimize
- Without profiling evidence (premature optimization)

> 💡 **Performance Tip:** Stable props + stable callbacks = effective memoization.
