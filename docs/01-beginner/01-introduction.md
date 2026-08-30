# 01. Introduction to React ⚛️

## What is React?
React is a JavaScript library for building user interfaces using reusable components.

## Why React?
- Component-driven development
- Declarative UI model
- Huge ecosystem and hiring demand

## React vs Other Frameworks
| Tool | Type | Strength |
|---|---|---|
| React | Library | Flexibility + ecosystem |
| Angular | Framework | All-in-one conventions |
| Vue | Framework | Simpler onboarding |

## How React works (Virtual DOM)
React computes a virtual tree, diffs it against previous render, and updates only changed DOM nodes.

```jsx
import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);
  return (
    <button onClick={() => setCount(c => c + 1)}>
      Clicked {count} times
    </button>
  );
}
```

## Setup options
### CRA
```bash
npx create-react-app my-app
```
### Vite (recommended)
```bash
npm create vite@latest my-app -- --template react
cd my-app && npm install && npm run dev
```

## First App
```jsx
function Welcome({ name }) {
  return <h2>Welcome, {name}! 🚀</h2>;
}
```

## When to use React
- Interactive SPAs
- Design systems and dashboards
- Apps requiring reusable UI blocks

## When NOT to use React
- Static brochure pages (plain HTML can be enough)
- Ultra-simple pages with zero interactivity

> 💡 **Tip:** Learn JavaScript deeply; React rewards strong JS fundamentals.
>
> ⚠️ **Warning:** Don’t start with advanced state libraries on day 1.

## Common mistakes
- Confusing props and state
- Mutating state directly
- Ignoring keys in lists

## Real-world use case
Product dashboard with widgets updated based on user permissions.

### Interview checkpoint
**Q:** Why is React called declarative?  
**A:** You describe desired UI for a given state; React handles DOM updates.
