# React Cheatsheet ⚡

## Hooks quick reference
```jsx
const [state, setState] = useState(initial);
useEffect(() => {}, [deps]);
const ref = useRef(null);
const value = useMemo(() => compute(a), [a]);
const fn = useCallback(() => {}, [deps]);
const [s, dispatch] = useReducer(reducer, initial);
const ctx = useContext(MyContext);
```

## Patterns quick reference
- HOC: cross-cutting enhancement
- Render Props: function-as-child composition
- Compound Components: flexible API with shared context
- Container/Presentational: split data and UI

## Common snippets
```jsx
// conditional
{isLoading ? <Spinner /> : <Content />}

// list rendering
items.map(item => <Row key={item.id} item={item} />)
```

## Performance checklist
- Memoize expensive work
- Split routes/components
- Virtualize long lists
- Measure with profiler first
