# 02. React Design Patterns 🧠

## Higher-Order Component (HOC)
```jsx
const withLoading = Component => ({ isLoading, ...props }) =>
  isLoading ? <p>Loading...</p> : <Component {...props} />;
```

## Render Props
```jsx
<DataFetcher render={(data) => <Chart data={data} />} />
```

## Compound Components
`<Tabs><Tabs.List/><Tabs.Panel/></Tabs>` API with shared internal context.

## Container/Presentational
Separate data orchestration from pure UI.

## Provider, Observer, Factory patterns
Useful for dependency injection, subscriptions, and object/component creation.

## When to use patterns
- Shared architecture standards in large teams

## When NOT to use
- Forcing patterns in tiny apps (unnecessary complexity)
