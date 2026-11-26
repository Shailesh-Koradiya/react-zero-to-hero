# 01. Hooks In Depth 🪝

## Core hooks
- `useState` local state
- `useEffect` side effects
- `useRef` mutable refs
- `useMemo` memoized calculations
- `useCallback` memoized function references
- `useReducer` complex state transitions
- `useContext` shared dependency injection
- `useLayoutEffect` sync after DOM mutation/before paint
- `useId` stable IDs
- `useDeferredValue` defer expensive UI updates
- `useTransition` mark non-urgent updates

```jsx
import { useEffect, useMemo, useState, useTransition } from 'react';

export function Search({ items }) {
  const [query, setQuery] = useState('');
  const [isPending, startTransition] = useTransition();

  const filtered = useMemo(
    () => items.filter(i => i.toLowerCase().includes(query.toLowerCase())),
    [items, query]
  );

  useEffect(() => {
    document.title = `${filtered.length} results`;
  }, [filtered.length]);

  return (
    <>
      <input onChange={e => startTransition(() => setQuery(e.target.value))} />
      {isPending && <p>Updating...</p>}
      <ul>{filtered.map(v => <li key={v}>{v}</li>)}</ul>
    </>
  );
}
```

## When to use hooks
- To compose stateful logic in reusable way

## When NOT to use
- Outside React function components/custom hooks
- As a replacement for clear architecture

> ⚠️ **Rule:** Hooks must be called unconditionally at top level.

## Common mistakes
- Missing dependencies in `useEffect`
- Premature overuse of `useMemo/useCallback`

## Real-world use case
Autosave editor with debounced updates, optimistic UI, and transitions.
