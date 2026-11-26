# React Coding Challenges 🧪

## 1) Debounced Search Box
```jsx
function useDebounce(value, delay = 300) {
  const [d, setD] = React.useState(value);
  React.useEffect(() => {
    const id = setTimeout(() => setD(value), delay);
    return () => clearTimeout(id);
  }, [value, delay]);
  return d;
}
```

## 2) Infinite Scroll List
Use `IntersectionObserver` with paginated API and dedupe by ID.

## 3) Modal with focus trap
Implement keyboard escape + focus return for accessibility.

## 4) Multi-step form wizard
Persist partial state and validate step transitions.

## 5) Optimistic todo updates
Update UI immediately, rollback on API failure.

## 6) Theme switcher with context
Support system preference and local persistence.

## 7) Virtualized table
Render 10k rows using `react-window`.

## 8) Protected routing
Redirect unauthenticated users preserving return URL.

## 9) Build useFetch hook
Support aborting requests and retry strategy.

## 10) Error boundary challenge
Catch render-time errors and show fallback UI.
