# 04. State and Events 🎛️

## useState
```jsx
import { useState } from 'react';

export default function LikeButton() {
  const [liked, setLiked] = useState(false);
  return (
    <button onClick={() => setLiked(v => !v)}>
      {liked ? '❤️ Liked' : '🤍 Like'}
    </button>
  );
}
```

## Synthetic events
React wraps browser events for consistent behavior.

## Controlled vs uncontrolled
```jsx
function ControlledInput() {
  const [value, setValue] = useState('');
  return <input value={value} onChange={e => setValue(e.target.value)} />;
}
```

## Lifting state up
Move shared state to nearest common parent for synchronized siblings.

## When to use local state
- UI-only toggles
- Temporary form state

## When NOT to use local state
- Cross-page/cross-feature shared state (use context/store)

> ⚠️ **Warning:** State updates are async; don’t expect immediate values after `setState`.

## Common mistakes
- Mutating objects/arrays directly
- Deriving state that can be calculated on render

## Real-world use case
Filter + sort panel controlling a product grid from parent state.
