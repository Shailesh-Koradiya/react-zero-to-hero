# 02. JSX In Depth 🧩

JSX is syntax sugar that lets you write HTML-like structures inside JavaScript.

## Rules
- Return a single parent (or fragment)
- Use `className`, `htmlFor`
- Expressions go inside `{}`

```jsx
const user = { name: 'Ava', isAdmin: true };

export function Header() {
  return (
    <>
      <h1>Hello, {user.name}</h1>
      {user.isAdmin ? <span>Admin</span> : <span>Member</span>}
    </>
  );
}
```

## Lists and keys
```jsx
const todos = [
  { id: 1, text: 'Read docs' },
  { id: 2, text: 'Build mini app' }
];

<ul>
  {todos.map(todo => <li key={todo.id}>{todo.text}</li>)}
</ul>
```

## When to use JSX
- Any React component UI declaration

## When NOT to use JSX
- Runtime-generated templates outside React render flow

> 💡 **Best Practice:** Keep JSX readable; move heavy logic to helper functions.
>
> ⚠️ **Warning:** Never use array index as key for dynamic/reordered lists.

## Common mistakes
- Writing statements inside JSX (only expressions allowed)
- Returning siblings without a wrapper/fragment

## Real-world use case
Rendering order history table with conditional status badges.
