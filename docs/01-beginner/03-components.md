# 03. Components 🧱

## Functional vs Class Components
Functional components with hooks are current standard.

```jsx
function Greeting({ name = 'Guest', children }) {
  return (
    <section>
      <h2>Hello {name}</h2>
      {children}
    </section>
  );
}
```

## Props and children
Props are read-only inputs.

```jsx
<Greeting name="Shailesh">
  <p>Let’s build production React apps.</p>
</Greeting>
```

## PropTypes + default props
```jsx
import PropTypes from 'prop-types';

Greeting.propTypes = { name: PropTypes.string, children: PropTypes.node };
Greeting.defaultProps = { name: 'Guest' };
```

## Component tree
Think of UI as nested tree: `App -> Layout -> Pages -> Widgets`.

## When to use component extraction
- UI is repeated
- A block has its own behavior

## When NOT to split further
- Tiny one-off wrappers adding no clarity

> 💡 **Tip:** Prefer many focused components over giant monolith files.

## Common mistakes
- Passing too many unrelated props
- Hiding business logic deep in presentational components

## Real-world use case
Shared `Card`, `Button`, `Modal`, `DataTable` components in admin portals.
