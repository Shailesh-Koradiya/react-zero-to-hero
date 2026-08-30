# 05. TypeScript with React 🔷

## Typing props/events/hooks
```tsx
type ButtonProps = {
  label: string;
  onClick: (event: React.MouseEvent<HTMLButtonElement>) => void;
};

export function Button({ label, onClick }: ButtonProps) {
  return <button onClick={onClick}>{label}</button>;
}
```

## useState + generics
```tsx
const [users, setUsers] = useState<Array<{ id: string; name: string }>>([]);
```

## Utility types
- `Partial<T>`, `Pick<T, K>`, `Omit<T, K>`, `Record<K, V>`

## React.FC vs function declarations
Prefer direct function declarations for clearer children control.

## When to use TS in React
- Team projects, long-lived products, large codebases

## When NOT to use strict TS from day 1
- Rapid throwaway prototypes (but migrate soon)
