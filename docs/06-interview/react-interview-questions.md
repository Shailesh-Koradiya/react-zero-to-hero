# 100+ React Interview Questions with Answers 💼

Use this page for quick revision: each question has an answer and a small example. Snippets illustrate the idea; imports, surrounding components, and application-specific functions are omitted unless needed.

## Junior Fundamentals

### 1. What is React and why is it popular?
**Answer:** React is a JavaScript library for building user interfaces from reusable components. It lets you describe what the UI should look like for the current data and updates the DOM as data changes. Its component model, ecosystem, and tooling make large UIs easier to maintain; it does not prescribe a router or server architecture.

**Example:** A shopping app can reuse a `ProductCard` component for every product while passing each card different data.

### 2. What is JSX?
**Answer:** JSX is a syntax extension that lets you write HTML-like markup in JavaScript. A build tool transforms it into React element creation calls; expressions go inside `{}` and attributes generally use JavaScript names such as `className`.

**Example:** `const heading = <h1 className="title">Hello, {name}</h1>;`.

### 3. Difference between props and state?
**Answer:** Props are inputs a component receives from its parent and must not mutate. State is data React remembers for a component; updating it with its setter schedules a render. Both are snapshots for a particular render.

**Example:** `<Counter initialCount={5} />` receives `initialCount` as a prop, while `const [count, setCount] = useState(initialCount)` holds its current count in state.

### 4. What is virtual DOM?
**Answer:** The virtual DOM is an informal name for React's in-memory representation of the UI. React compares the new rendered tree with the previous one and commits necessary DOM changes. It does not mean every update is automatically faster than handwritten DOM code.

**Example:** Changing a counter from 1 to 2 can update its text without rebuilding the entire page.

### 5. What are keys in lists?
**Answer:** Keys identify siblings across renders so React can match items when they move, appear, or disappear. Use stable IDs from the data; keys need only be unique among siblings. Avoid array indexes when a list can be reordered, inserted into, or filtered.

**Example:** `users.map(user => <UserRow key={user.id} user={user} />)`.

### 6. Controlled vs uncontrolled components?
**Answer:** A controlled input gets its current value from React state and reports edits through an event handler. An uncontrolled input keeps its value in the DOM, often read using a ref. Controlled inputs are useful for validation; uncontrolled inputs can be simpler for basic forms.

**Example:** Controlled: `<input value={name} onChange={e => setName(e.target.value)} />`. Uncontrolled: `<input ref={inputRef} defaultValue="Sam" />`, read with `inputRef.current.value`.

### 7. What is lifting state up?
**Answer:** Move shared state to the closest common ancestor of components that need it. That ancestor passes values and callbacks down, giving both children one source of truth.

**Example:** A parent stores `selectedId`, passes it to a list to highlight a row, and passes the same ID to a details panel.

### 8. What are fragments?
**Answer:** Fragments group multiple elements without adding an extra DOM wrapper. Use `<>...</>` for the short form or `<Fragment key={id}>...</Fragment>` when the fragment needs a key.

**Example:** `return <><h1>Profile</h1><p>Welcome</p></>;`.

### 9. How does event handling work in React?
**Answer:** Pass a function to a camel-cased event prop such as `onClick`. React invokes it when the event occurs; do not invoke the handler during rendering. Call `preventDefault()` when you need to stop a browser default action.

**Example:** `<button onClick={() => setCount(c => c + 1)}>Add</button>`.

### 10. What is one-way data flow?
**Answer:** Data flows from parent to child through props. A child requests a change by calling a callback provided by its parent; the parent updates state and passes new props down.

**Example:** `<SearchBox value={query} onChange={setQuery} />` lets the parent own the query.

### 11. What is component reusability?
**Answer:** A component is reusable when it encapsulates a UI responsibility and accepts data or behavior through props instead of hard-coding every use. Reuse should preserve meaningful differences rather than create a component with dozens of unrelated options.

**Example:** `<Button onClick={save}>Save</Button>` and `<Button onClick={cancel}>Cancel</Button>` share button styling.

### 12. What is conditional rendering?
**Answer:** Render different JSX based on a condition using JavaScript `if`, a ternary, or `&&`. Returning `null` renders nothing. Be careful with numeric values: `0 && <List />` renders `0`.

**Example:** `isLoggedIn ? <Dashboard /> : <Login />`.

### 13. Why avoid direct state mutation?
**Answer:** React treats state as a snapshot and can skip an update when the next value is `Object.is`-equal to the current one. Mutating an existing object can therefore leave the UI stale and also corrupt previous snapshots. Create new objects or arrays along the changed path.

**Example:** `setUser(prev => ({ ...prev, name: "Asha" }))`, not `user.name = "Asha"`.

### 14. What is prop drilling?
**Answer:** Prop drilling means passing a prop through components that do not use it themselves, only to reach a deeper descendant. It is not inherently wrong; composition or context can help when the chain becomes cumbersome.

**Example:** Passing `theme` from `App` through `Layout` and `Sidebar` to `Button` can be replaced by a theme context if many descendants need it.

### 15. What are synthetic events?
**Answer:** React exposes a cross-browser event object with a consistent interface, wrapping the underlying browser event. Access the browser event via `event.nativeEvent` when necessary. In modern React, synthetic events are not pooled.

**Example:** `<form onSubmit={event => { event.preventDefault(); save(); }}>...</form>`.

### 16. How to render lists?
**Answer:** Transform an array into elements, usually with `map`, and provide a stable key on the element returned for each item. Render an empty state when appropriate.

**Example:** `<ul>{items.map(item => <li key={item.id}>{item.name}</li>)}</ul>`.

### 17. What is a pure component conceptually?
**Answer:** A pure render returns the same UI for the same props, state, and context and does not change external values while rendering. Purity lets React safely retry or skip rendering work; side effects belong in event handlers or effects.

**Example:** `function Total({ price, quantity }) { return <span>{price * quantity}</span>; }`.

### 18. Why should components be small?
**Answer:** Components focused on one responsibility are generally easier to understand, test, and reuse. Smallness is a guideline, not a goal: splitting a simple component into many tiny pieces can make navigation harder.

**Example:** Extract a `ProfileForm` from a page that also handles navigation and an activity feed.

### 19. How to pass children?
**Answer:** JSX nested between a component's opening and closing tags becomes its `children` prop. This is useful for composition without requiring the wrapper to know the content.

**Example:** `function Card({ children }) { return <section>{children}</section>; }` used as `<Card><h2>News</h2></Card>`.

### 20. What is default props usage?
**Answer:** Defaults supply a value when a prop is missing or `undefined`; an explicit `null` is not replaced. For function components use JavaScript parameter defaults. `defaultProps` for function components was removed in React 19; class components still support it.

**Example:** `function Greeting({ name = "Guest" }) { return <p>Hello, {name}</p>; }`.

## Hooks and State

### 21. Rules of hooks?
**Answer:** Call ordinary Hooks at the top level of a React function component or custom Hook, in the same order on every render. Do not call them in loops, conditions, event handlers, or ordinary functions. React's `use` API is a special exception that may be called in loops and conditions, but must still run in a component or Hook and not inside `try`/`catch`.

**Example:** Call `useState` before `if (!user) return null`, not inside that `if`.

### 22. When to use useEffect?
**Answer:** Use an effect to synchronize a component with an external system after rendering, such as a subscription, timer, or browser API. Return cleanup to undo the setup. Do not use an effect just to calculate a value from props or handle a button click.

**Example:** `useEffect(() => { window.addEventListener("resize", handleResize); return () => window.removeEventListener("resize", handleResize); }, []);` assumes `handleResize` is defined outside the component or otherwise stable.

### 23. Difference between useEffect and useLayoutEffect?
**Answer:** `useEffect` generally runs after the browser paints; `useLayoutEffect` runs after DOM changes but before paint and blocks painting. Use layout effects only when a measurement or visual adjustment must happen before the user sees the result.

**Example:** Measure a tooltip with `useLayoutEffect` to position it before paint; use `useEffect` for a chat subscription.

### 24. When to use useRef?
**Answer:** A ref stores a mutable value across renders without triggering a render when `.current` changes. Use it for DOM access or values like timer IDs, not for data that must update the visible UI.

**Example:** `const inputRef = useRef(null);` then `<input ref={inputRef} />` and `inputRef.current?.focus()` in a click handler.

### 25. What problem does useMemo solve?
**Answer:** `useMemo` caches a calculation result between renders while dependencies remain equal. It is a performance optimization for expensive calculations or useful reference stability, not a correctness guarantee; measure before adding it.

**Example:** `const visible = useMemo(() => filterItems(items, query), [items, query]);`.

### 26. What problem does useCallback solve?
**Answer:** `useCallback` caches a function reference until its dependencies change. It can help a memoized child skip a render or stabilize another Hook dependency; it does not prevent the function from being created during rendering.

**Example:** `const handleSave = useCallback(() => save(itemId), [itemId]);` can be passed to a memoized child if `save` is stable.

### 27. useReducer vs useState?
**Answer:** Both manage local state. `useState` is concise for straightforward values; `useReducer` centralizes related transitions in a pure reducer and can make complex actions easier to test. Neither is automatically global state.

**Example:** A form reducer can handle `{ type: "changed", field: "email", value }` and `{ type: "reset" }` actions.

### 28. How to avoid stale closures?
**Answer:** A callback captures values from the render that created it. Include every reactive value used by an effect or memoized callback in its dependency list, and use functional state updates when the next value depends on previous state. Don't silence the dependency lint rule to hide the problem.

**Example:** An interval can call `setCount(c => c + 1)` rather than capturing the initial `count` in an effect with `[]`.

### 29. How to cancel async effects?
**Answer:** Return a cleanup function that aborts supported work or marks its result as obsolete. Handle aborts separately from genuine errors; cancellation prevents an old request from updating the UI after dependencies change.

**Example:** Create an `AbortController` inside the effect, pass `controller.signal` to `fetch`, and return `() => controller.abort()`; ignore only errors whose `name` is `"AbortError"`.

### 30. What is dependency array?
**Answer:** It tells React which reactive values an effect or memo depends on. React compares each with its previous value using `Object.is`. No array runs an effect after every committed render; `[]` means no reactive dependencies; `[roomId]` re-synchronizes when `roomId` changes.

**Example:** `useEffect(() => connect(roomId), [roomId])`, where `connect` returns a cleanup function and is defined outside the component.

### 31. How to create custom hooks?
**Answer:** Extract reusable stateful logic into a function whose name starts with `use`; it may call other Hooks and must follow Hook rules. Each call gets its own state unless the Hook accesses a shared store or context.

**Example:** `function useToggle(initial = false) { const [on, setOn] = useState(initial); return [on, () => setOn(v => !v)]; }`.

### 32. When to use useContext?
**Answer:** Use `useContext` to read a value provided by the nearest matching provider, especially for values needed by many descendants. Context avoids some prop drilling but is not automatically a replacement for all state management; consumers update when the provided value changes.

**Example:** A theme provider exposes `"dark"` and a nested button reads it with `useContext(ThemeContext)`.

### 33. What is useTransition?
**Answer:** `useTransition` marks state updates as non-urgent, allowing React to keep urgent interactions responsive while rendering transition work. It returns an `isPending` flag and `startTransition`. Do not use a transition to control the state of a text input.

**Example:** Update the text input immediately, then call `startTransition(() => setSearchQuery(nextValue))` for a slow results view.

### 34. What is useDeferredValue?
**Answer:** `useDeferredValue` lets a part of the UI temporarily render an older value while React prepares an update using the new value. It is useful when you receive a value rather than control the update; it does not debounce or prevent network requests.

**Example:** `const deferredQuery = useDeferredValue(query);` and pass `deferredQuery` to an expensive results component.

### 35. How does batching work?
**Answer:** React groups multiple state updates into fewer renders when possible. With `createRoot` in React 18+, automatic batching also applies to updates in promises, timers, and native event handlers. Each render still sees a state snapshot.

**Example:** `setCount(c => c + 1); setCount(c => c + 1);` increments twice in one batch; two `setCount(count + 1)` calls based on the same snapshot do not.

### 36. What causes rerenders?
**Answer:** A component renders when its state changes, a context it consumes changes, or its parent renders and React renders the child. New props matter especially when a child is memoized. Changing a ref alone does not trigger a render, and rendering does not necessarily mean a DOM change.

**Example:** Calling `setCount` renders `Counter` and may render its children, even if their displayed output is unchanged.

### 37. How to debug hooks?
**Answer:** Use React DevTools to inspect component props and Hook state, and the Profiler to investigate render costs. Enable the Hooks ESLint rules and inspect effect dependencies and cleanup; remember development Strict Mode intentionally repeats some work.

**Example:** If a subscription reconnects every render, inspect whether an object in its effect dependencies is recreated each time.

### 38. How to share stateful logic?
**Answer:** Extract a custom Hook to reuse the logic, not the state itself. For the same shared state across components, put state in a common parent, context, or an external store.

**Example:** Two calls to `useToggle()` create independent toggles; a provider can expose one toggle to multiple consumers.

### 39. When to derive state?
**Answer:** If a value can be calculated from current props or state, calculate it during rendering instead of storing a second synchronized copy. This avoids extra renders and inconsistent values. Memoize only if the calculation is measurably expensive.

**Example:** `const fullName = firstName + " " + lastName;` instead of maintaining another `fullName` state variable.

### 40. How to reset hook state?
**Answer:** Set state back to its initial value, dispatch a reset action, or change a component's `key` to make React recreate the whole subtree. Changing the key also resets child state and reruns effects.

**Example:** `<Chat key={recipient.id} recipient={recipient} />` clears the previous recipient's draft when the ID changes.

## Routing and Data

### 41. How does React Router v6 differ from v5?
**Answer:** React Router v6 replaced `<Switch>` with `<Routes>`, uses `<Route element={<Page />} />`, ranks route matches, and supports nested layouts through `<Outlet>`. `useNavigate` replaces `useHistory`. Later v6 releases also introduced data routers with loaders and actions.

**Example:** `<Routes><Route path="/users/:id" element={<UserPage />} /></Routes>`.

### 42. What is nested routing?
**Answer:** Nested routes express UI layouts that match parts of a URL. A parent route renders an `<Outlet />` where the matching child route appears; child paths can be relative to the parent.

**Example:** A `/settings` layout with child path `profile` renders the profile page at `/settings/profile` inside the settings layout.

### 43. How to implement protected routes?
**Answer:** A route wrapper can check authentication state, show a loading state while it is being determined, and redirect unauthenticated users. This is only a UI/navigation guard: the server must independently authenticate and authorize every protected request.

**Example:** `return user ? <Outlet /> : <Navigate to="/login" replace />;` after the auth loading state has resolved.

### 44. How to handle route params?
**Answer:** Declare dynamic segments in the route and read them with `useParams`. Params come from the URL as strings and should be validated before using them; handle missing or invalid records.

**Example:** Route `/users/:id` with `const { id } = useParams();` can load a user by `id`.

### 45. What is code-splitting in routing?
**Answer:** Load a route's JavaScript only when it is needed rather than including every page in the initial bundle. `React.lazy` and `Suspense` can split a component; router frameworks may provide their own lazy route APIs.

**Example:** `const Settings = lazy(() => import("./Settings"));` then render it inside `<Suspense fallback={<p>Loading...</p>}>`.

### 46. How to fetch data safely in effects?
**Answer:** Start a request for the current dependencies, handle loading and errors, and clean up or ignore obsolete requests. Check `response.ok`: `fetch` does not reject merely because the server returned HTTP 404 or 500. Framework loaders or a query library often handle caching and race conditions more conveniently.

**Example:** For a changing `userId`, create an `AbortController` in an effect with `[userId]`, pass its signal to `fetch`, check `response.ok`, and abort in cleanup.

### 47. Why use React Query?
**Answer:** TanStack Query (formerly React Query) manages asynchronous server state: caching, deduplication, background refetching, retries, and mutations. It is not needed for every app and does not replace local UI state.

**Example:** `useQuery({ queryKey: ["users"], queryFn: fetchUsers })` shares cached users among consumers of that key.

### 48. Query invalidation meaning?
**Answer:** Invalidation marks matching cached queries as stale so their data can be refreshed. In TanStack Query, active matching queries normally refetch in the background; inactive queries are refreshed when used according to their settings.

**Example:** After saving a user, call `queryClient.invalidateQueries({ queryKey: ["users"] })` to refresh the users list.

### 49. Optimistic update concept?
**Answer:** Update the UI before the server confirms the operation, then reconcile with the server response or roll back if it fails. This improves perceived speed but needs careful handling of concurrent edits and failures.

**Example:** Show a todo as completed immediately, send the update, and restore its previous status with an error message if the request fails.

### 50. Retry and backoff strategy?
**Answer:** Retry transient failures a limited number of times, increasing the delay between attempts, ideally with jitter. Avoid blindly retrying validation or authorization failures and non-idempotent operations, which could duplicate side effects.

**Example:** Retry a failed GET after roughly 1, 2, and 4 seconds; do not automatically repeat a payment POST unless the server supports an idempotency key.

### 51. How to handle loading and error states?
**Answer:** Model loading, error, empty, and success states explicitly. Preserve usable existing data during background refresh where appropriate, and offer a retry for recoverable errors. Make status messages accessible.

**Example:** Show `Loading...`, then either an error with a Retry button, `No users found`, or the user list.

### 52. SSR vs CSR impact on data?
**Answer:** With server-side rendering (SSR), the server can fetch data and send HTML containing the result; the client typically hydrates it. With client-side rendering (CSR), the browser downloads JavaScript and fetches data to render the view. SSR can improve initial content visibility but adds server and hydration complexity.

**Example:** An SSR product page can send the product name in its initial HTML; a CSR page may initially send a loading shell.

### 53. How to avoid waterfall requests?
**Answer:** Start independent requests in parallel, hoist data requirements to a route loader, or prefetch likely next data. Dependent requests cannot be parallelized until the dependency is known; consider a server endpoint that returns the needed combined data.

**Example:** `const [user, posts] = await Promise.all([fetchUser(id), fetchPosts(id)]);` when both requests only require `id`.

### 54. How to structure API layer?
**Answer:** Keep HTTP details, response/error handling, and endpoint functions separate from UI components. Group calls by domain, validate untrusted responses where appropriate, and avoid hiding failures behind default success values.

**Example:** `usersApi.getUser(id)` fetches `/api/users/${id}` and throws on a non-OK response; the component displays the returned data or an error.

### 55. How to secure API calls?
**Answer:** Use HTTPS, authenticate and authorize on the server, validate input, and avoid putting secrets in client code. For cookie-based authentication, use appropriate `Secure`, `HttpOnly`, and `SameSite` settings and CSRF protection as needed. CORS is not authorization.

**Example:** A server checks that the current user owns an order before returning `/api/orders/123`, even if the UI hides other users' orders.

### 56. What are race conditions in fetch?
**Answer:** Requests can finish in a different order than they were started, allowing an older result to overwrite a newer one. Cancel obsolete requests or ignore their results, and surface genuine errors.

**Example:** Searching `rea` then `react` may display the `rea` response last unless the earlier request is aborted or ignored.

### 57. What is SWR pattern?
**Answer:** Stale-while-revalidate returns cached data immediately, then fetches fresh data in the background and updates the UI. It improves perceived speed but temporarily shows potentially outdated information.

**Example:** Display cached profile details while refreshing them after the user revisits the page.

### 58. How to paginate data?
**Answer:** Request and render a subset of records at a time using page/offset or cursor parameters. Track loading and errors per request. Cursor pagination is often preferable for frequently changing large datasets, while offsets allow direct page numbers.

**Example:** Request `/api/products?cursor=abc&limit=20`, then use the returned `nextCursor` for the next page.

### 59. How to cache per query key?
**Answer:** A query key identifies a cached result and must include every variable that changes the fetched data. Use a consistent key structure so related queries can be invalidated together.

**Example:** `useQuery({ queryKey: ["user", userId], queryFn: () => fetchUser(userId) })` keeps different users in separate cache entries.

### 60. How to prefetch routes/data?
**Answer:** Load likely-needed code or data before navigation, for example on hover or focus, using the router or query library. Prefetch selectively to avoid wasting bandwidth, and still handle loading and errors on navigation.

**Example:** On a product link's hover, call `queryClient.prefetchQuery({ queryKey: ["product", id], queryFn: () => fetchProduct(id) })`.

## Performance and Architecture

### 61. When to use React.memo?
**Answer:** `memo` can skip rendering a component when its parent renders and its props are unchanged. It is useful for measured expensive rerenders with stable props; it does not block updates from the component's own state or consumed context.

**Example:** `const ProductRow = memo(function ProductRow({ product }) { return <li>{product.name}</li>; });`.

### 62. How to profile React app?
**Answer:** Record an interaction with the React DevTools Profiler to find expensive commits and components, then use browser performance tools for network, JavaScript, layout, and paint. Compare measurements before and after the change, preferably in a production-like build.

**Example:** Profile typing into a search box, find that a large results list dominates the commit, and optimize that list rather than memoizing every component.

### 63. What is reconciliation?
**Answer:** Reconciliation is React's process of determining how the newly rendered tree relates to the previous one. Element type, position, and keys influence whether state is preserved or a subtree is recreated; React then commits needed changes.

**Example:** Reordering keyed todo rows preserves each row's state with its todo; switching a `<Counter />` to a different component type resets that subtree.

### 64. How to prevent unnecessary rerenders?
**Answer:** Keep state close to where it is used, avoid redundant state, split large components or contexts, and use memoization selectively when profiling shows a benefit. Stable props matter for memoized children. Renders are normal; optimize expensive ones, not every render.

**Example:** Move a search input's state into a search panel so typing does not cause an unrelated dashboard subtree to render.

### 65. What are render props?
**Answer:** A render prop is a function prop a component calls to decide what to render. It lets the component share behavior while the caller controls the UI; custom Hooks often offer a simpler alternative today.

**Example:** `<MouseTracker render={position => <span>{position.x}, {position.y}</span>} />`, where `MouseTracker` supplies the current position.

### 66. What are HOCs?
**Answer:** A higher-order component is a function that takes a component and returns an enhanced component. It can share behavior such as an injected prop, but can make data flow and debugging less obvious.

**Example:** `const AdminPage = withAuth(Page);` wraps `Page` with authentication-related UI; the server must still enforce authorization.

### 67. What are compound components?
**Answer:** Compound components are related components designed to work together under a shared parent, often using context for shared state. They give consumers control over layout while encapsulating coordinated behavior.

**Example:** `<Tabs><Tabs.List>...</Tabs.List><Tabs.Panel>...</Tabs.Panel></Tabs>` lets the parent coordinate selection.

### 68. Container vs presentational?
**Answer:** A container handles data fetching or state orchestration; a presentational component receives data and callbacks and focuses on display. This separation can improve testability, though Hooks allow both concerns to coexist when a split adds no value.

**Example:** `UsersContainer` loads users and passes them to `UserList`, which renders the list.

### 69. Feature-based folder architecture?
**Answer:** Group files by business feature rather than putting every component, Hook, and test into global folders. It keeps related changes together and makes ownership clearer; shared, genuinely cross-feature code can live separately.

**Example:** `features/cart/` contains cart components, state, API calls, and tests; `shared/` contains reusable primitives.

### 70. When to use Redux Toolkit?
**Answer:** Use Redux Toolkit when an application benefits from a centralized, predictable client-state store, explicit actions, middleware, and debugging tools across many features. For small or local state, `useState`, `useReducer`, or context may be simpler.

**Example:** A multi-step checkout shared across distant screens can use a Redux slice with actions for items, address, and payment status.

### 71. What is RTK Query?
**Answer:** RTK Query is Redux Toolkit's data-fetching and caching solution. It generates hooks from endpoint definitions and manages request state, cache lifetime, and tag-based invalidation. It is optional; Redux Toolkit does not require it.

**Example:** Define a `getUsers` query endpoint and use the generated `useGetUsersQuery()` hook in a component.

### 72. When to split context providers?
**Answer:** Split contexts when values have different consumers or update frequencies, so unrelated consumers don't all react to every provider value change. This improves clarity and can reduce work, but excessive splitting adds complexity.

**Example:** Keep frequently changing notification counts separate from an infrequently changing theme context.

### 73. How to virtualize long lists?
**Answer:** Render only visible rows plus a small buffer while preserving the scrollable space for the full list, typically with a virtualization library. Consider variable row heights, keyboard navigation, and screen-reader access.

**Example:** For 10,000 products, render only the rows near the viewport instead of creating 10,000 DOM nodes.

### 74. What is hydration?
**Answer:** Hydration attaches React behavior to server-rendered HTML so it becomes interactive. The initial client render should match the server output; mismatches can cause warnings or React to regenerate parts of the UI.

**Example:** A server renders a button, then `hydrateRoot` connects its React click handler in the browser.

### 75. What is concurrent rendering?
**Answer:** Concurrent rendering lets React prepare certain updates interruptibly, pause or discard in-progress work, and prioritize urgent updates. It is a capability used by features like transitions and Suspense, not a promise that all rendering happens on multiple threads.

**Example:** Typing remains responsive while a non-urgent transition prepares a large filtered list.

### 76. How to optimize bundle size?
**Answer:** Measure bundles, remove unused dependencies, split code by route or feature, and avoid shipping unnecessary polyfills. Check the effect on actual loading performance instead of assuming a smaller package always improves the user experience.

**Example:** Lazy-load an admin charting library only on the admin route rather than importing it into the initial entry point.

### 77. Tree shaking in React builds?
**Answer:** Tree shaking is a bundler optimization that removes unused code from a production bundle, especially with static ES module imports. It depends on module structure and correct side-effect declarations; unused exports are not guaranteed to disappear.

**Example:** A bundler may remove an unused named export from `utils.js` when the module has no relevant side effects.

### 78. What is module federation?
**Answer:** Module Federation allows separately built applications to load and share modules at runtime, often for micro-frontends. It can enable independent deployments but introduces versioning, availability, and integration complexity.

**Example:** A shell application loads a separately deployed checkout module, with a plan for incompatible shared React versions or a failed remote.

### 79. Monorepo pros and cons?
**Answer:** A monorepo keeps multiple projects in one repository, making shared tooling, atomic cross-project changes, and code sharing easier. It can increase CI cost, require clear ownership, and need tooling for dependency boundaries and selective builds.

**Example:** A web app and shared component library can update in one pull request, but CI should test only affected packages where possible.

### 80. How to design scalable state model?
**Answer:** Categorize state by ownership and lifetime: local UI, shared client state, URL state, and server state. Keep a single source of truth, derive redundant values, normalize relational data where useful, and choose the simplest appropriate tool.

**Example:** Keep a modal's open state locally, search filters in the URL, and product data in a query cache instead of duplicating all three in one global store.

## Testing, Security, Leadership

### 81. Testing philosophy in React?
**Answer:** Test behavior from the user's perspective, with a mix of focused unit tests, integration tests, and a few critical end-to-end flows. Prefer accessible queries and meaningful assertions over tests tied to internal state or implementation details.

**Example:** Click “Add to cart” and assert the cart count changes, rather than asserting that a particular setter was called.

### 82. Unit vs integration tests?
**Answer:** A unit test checks a small piece of logic in isolation; an integration test checks how multiple pieces work together. Integration tests catch wiring problems, while focused unit tests make complex rules easier to diagnose.

**Example:** Unit-test a discount calculator; integration-test entering a coupon and seeing the updated total in the checkout UI.

### 83. How to test async UI?
**Answer:** Trigger the user action, then wait for the observable result using async testing utilities. Assert loading and error states when important, and avoid fixed sleeps that make tests slow and flaky.

**Example:** `await user.click(screen.getByRole("button", { name: /load users/i })); expect(await screen.findByText("Asha")).toBeInTheDocument();`.

### 84. How to mock API calls?
**Answer:** Intercept requests at the network boundary or mock the API module so tests control responses without relying on a live server. Exercise both success and failure; retain separate integration or end-to-end tests for real backend contracts.

**Example:** Mock Service Worker can return a known JSON response for `GET /api/users` while the component uses its normal fetch logic.

### 85. When snapshots are useful?
**Answer:** Small, focused snapshots can detect unintended changes to stable output. Large snapshots are easy to approve without review and rarely explain behavioral regressions; use explicit assertions for important behavior.

**Example:** Snapshot a small formatter's output, but assert that an error message appears and a submit button is disabled with explicit tests.

### 86. How to test custom hooks?
**Answer:** Test the Hook through a component that uses it, or use `renderHook` for a focused Hook API test. Trigger updates with `act` when required and assert the returned observable state, including cleanup for subscriptions.

**Example:** Render a component using `useToggle`, click its button, and assert that the displayed status changes from “off” to “on”.

### 87. Common XSS risks in React?
**Answer:** React escapes text rendered in JSX by default, but unsafe HTML insertion, untrusted URLs, or vulnerable third-party code can still introduce XSS. Avoid `dangerouslySetInnerHTML` for untrusted input; when HTML is necessary, sanitize it with a maintained HTML sanitizer and apply a suitable CSP as defense in depth.

**Example:** Render a comment as `<p>{comment}</p>` rather than inserting the comment as raw HTML.

### 88. How to avoid leaking secrets?
**Answer:** Anything shipped to the browser, including frontend environment variables and source maps, must be considered public. Keep secret keys and privileged API calls on a server, use least-privilege credentials, and rotate any exposed secret.

**Example:** The browser calls your backend, which uses a private payment API key from its server environment; the key never appears in the JavaScript bundle.

### 89. How to secure auth in SPA?
**Answer:** Use a well-established authentication protocol and server-side authorization. For cookie-based sessions, use `HttpOnly`, `Secure`, appropriate `SameSite` settings, and CSRF defenses where needed; protect against XSS regardless of token storage. Avoid building custom cryptography.

**Example:** After login, the server sets a secure session cookie and checks both the session and the user's permissions on each protected API request.

### 90. What is CSP?
**Answer:** Content Security Policy is a browser-enforced policy, usually delivered in an HTTP response header, that restricts allowed content sources and can mitigate some XSS attacks. It complements, not replaces, output escaping and sanitization.

**Example:** `Content-Security-Policy: default-src 'self'; script-src 'self'` permits scripts from the same origin; a real policy must account for the app's required resources.

### 91. How to roll out feature flags safely?
**Answer:** Release behind a flag, test both paths, gradually enable it for a defined audience, monitor errors and product metrics, and keep a rollback option. Remove the flag and obsolete code once the rollout is complete.

**Example:** Enable a new checkout for 1% of eligible users, compare payment failures, and disable the flag if errors rise.

### 92. How to review PRs effectively?
**Answer:** Understand the goal and review correctness, security, accessibility, tests, and maintainability before focusing on style. Give specific, respectful feedback and distinguish blocking defects from optional suggestions.

**Example:** Point out that a request error leaves the submit button permanently disabled, and suggest testing the failure path.

### 93. How to mentor junior React devs?
**Answer:** Set clear goals, explain trade-offs, pair on real problems, and provide actionable feedback while letting the developer own the solution. Follow up with progressively independent work.

**Example:** Pair on a form, discuss controlled inputs and accessibility, then ask the developer to implement and test the validation.

### 94. How to lead migration from class to hooks?
**Answer:** Migrate incrementally when there is a clear benefit, protect existing behavior with tests, and map lifecycle logic to the correct effects or event handlers rather than mechanically replacing lifecycle methods. Classes remain supported; do not rewrite working code solely for syntax.

**Example:** Add tests for a subscription, convert one class component to a function with an effect and cleanup, then compare behavior before migrating others.

### 95. How to plan React upgrade strategy?
**Answer:** Read release and migration notes, inventory incompatible dependencies, upgrade in a branch, run automated tests, and validate critical flows in a production-like build. Roll out gradually and retain a rollback plan.

**Example:** Before React 19, check libraries and removed APIs such as function component `defaultProps`, then update affected components and dependencies.

### 96. How to reduce flaky tests?
**Answer:** Isolate test data, control external services and clocks where appropriate, wait for observable conditions instead of fixed delays, and clean up side effects. Investigate the root cause rather than masking failures with retries.

**Example:** Replace `sleep(2000)` with `await screen.findByText("Saved")` and mock the API response consistently.

### 97. How to handle legacy code refactors?
**Answer:** First understand current behavior and add characterization tests around risky paths. Make small, reversible changes, preserve public contracts, and monitor after release instead of combining a rewrite with unrelated feature changes.

**Example:** Test existing cart totals, extract the calculation into a pure function, then refactor the UI while retaining the same totals.

### 98. What metrics define frontend success?
**Answer:** Combine user and business outcomes with reliability, accessibility, and performance metrics. Useful signals include task completion, error rates, and Core Web Vitals such as LCP, INP, and CLS; compare against an agreed baseline.

**Example:** Track checkout completion and client-side error rate alongside mobile LCP after a page redesign.

### 99. How to debug production incidents?
**Answer:** Assess impact, communicate status, mitigate or roll back, then use logs, traces, error reports, and recent changes to find the cause. Verify the fix, document the timeline and contributing factors, and add safeguards without exposing sensitive data.

**Example:** If a release breaks login, roll it back, inspect sanitized error reports and the deployment diff, reproduce the issue, then add a regression test.

### 100. How to balance speed vs quality?
**Answer:** Match the level of verification to risk, agree on scope, and protect essential correctness, security, and accessibility. Ship a smaller vertical slice rather than skipping critical safeguards; record and schedule any intentional debt.

**Example:** Release a basic checkout with server-side authorization and payment tests first, then add optional personalization later.

## More React Essentials

### 101. What is Strict Mode?
**Answer:** `<StrictMode>` enables additional development-only checks, including extra rendering and effect setup/cleanup cycles to reveal impure rendering and missing cleanup. These checks do not run in production, and the exact behavior depends on where Strict Mode is enabled.

**Example:** If a subscription is registered twice in development, ensure its effect cleanup unsubscribes before the next setup.

### 102. What is an error boundary?
**Answer:** An error boundary displays fallback UI when a descendant throws during rendering or certain React lifecycle work. A class component implements it using `getDerivedStateFromError` and/or `componentDidCatch`; event-handler and most asynchronous errors need separate handling.

**Example:** Wrap a dashboard widget in an error boundary so a render error shows “Widget unavailable” instead of breaking the entire dashboard.

### 103. What does Suspense do?
**Answer:** Suspense displays a fallback while a descendant suspends, for example while a `lazy` component's code is loading. It does not automatically detect data fetched in an effect; data fetching must use a Suspense-enabled framework or data source.

**Example:** `<Suspense fallback={<p>Loading page...</p>}><LazyPage /></Suspense>`.

### 104. What are React Server Components?
**Answer:** Server Components render in a server environment and can access server-only resources without shipping their component code to the browser. Interactive state, effects, and browser APIs belong in Client Components. They require a supporting framework or integration and are distinct from SSR.

**Example:** A server component reads a product from a database and passes serializable product data to a client-side `AddToCartButton`.

### 105. Why does state not update immediately after calling its setter?
**Answer:** State is a snapshot for the current render. A setter schedules a future render; it does not change the local variable in the currently running handler. Use the next value directly or a functional update when computing from previous state.

**Example:** After `setCount(count + 1)`, logging `count` in the same handler still shows the old render's value; the next render receives the updated value.
