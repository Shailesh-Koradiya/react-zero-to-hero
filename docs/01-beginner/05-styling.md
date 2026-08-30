# 05. Styling in React 🎨

## CSS Modules
```jsx
import styles from './Button.module.css';

export function Button({ children }) {
  return <button className={styles.primary}>{children}</button>;
}
```

## Inline styles
```jsx
<div style={{ color: 'tomato', fontWeight: 700 }}>Alert</div>
```

## styled-components basics
```jsx
import styled from 'styled-components';

const Card = styled.div`
  padding: 1rem;
  border-radius: 12px;
`;
```

## Tailwind with React
```jsx
<button className="px-4 py-2 rounded bg-blue-600 text-white">Save</button>
```

## When to use
- CSS Modules: local scoping
- Tailwind: fast UI iteration
- styled-components: dynamic theming-heavy apps

## When NOT to use
- Inline styles for complex pseudo selectors/media queries

> 💡 **Performance Tip:** Avoid generating massive dynamic class strings every render.

## Common mistakes
- Mixing too many styling paradigms without standards
- Ignoring design tokens/theme consistency
