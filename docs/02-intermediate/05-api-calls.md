# 05. API Calls 🌍

## fetch in useEffect
```jsx
import { useEffect, useState } from 'react';

export function Users() {
  const [state, setState] = useState({ data: [], loading: true, error: null });

  useEffect(() => {
    let active = true;
    fetch('/api/users')
      .then(r => r.json())
      .then(data => active && setState({ data, loading: false, error: null }))
      .catch(error => active && setState({ data: [], loading: false, error }));
    return () => { active = false; };
  }, []);
}
```

## Axios
Interceptors for auth token refresh and global error handling.

## TanStack Query
```jsx
import { useQuery } from '@tanstack/react-query';

const { data, isLoading, error } = useQuery({
  queryKey: ['users'],
  queryFn: async () => (await fetch('/api/users')).json(),
});
```

## SWR
Great for stale-while-revalidate patterns.

## Custom hooks
Create `useUsers`, `useProjects` for reusable fetching patterns.

## When to use
- Query libraries for cache/retries/invalidation

## When NOT to use
- Hand-rolled caching for complex apps (reinventing the wheel)

> 💡 **Best Practice:** Always model loading, empty, error, and success UI states.
