# 03. Custom Hooks 🛠️

## Rules
- Prefix with `use`
- Keep responsibilities focused
- Expose stable, ergonomic API

### useDebounce
```jsx
import { useEffect, useState } from 'react';

export function useDebounce(value, delay = 300) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const id = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(id);
  }, [value, delay]);
  return debounced;
}
```

### useLocalStorage
```jsx
import { useEffect, useState } from 'react';

export function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => JSON.parse(localStorage.getItem(key)) ?? initialValue);
  useEffect(() => localStorage.setItem(key, JSON.stringify(value)), [key, value]);
  return [value, setValue];
}
```

Also build: `useFetch`, `useWindowSize`, `useOnClickOutside`, `useIntersectionObserver`.

## When to use
- Repeated stateful logic across components

## When NOT to use
- Single-use logic that adds unnecessary abstraction
