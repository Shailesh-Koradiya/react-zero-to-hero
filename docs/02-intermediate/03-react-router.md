# 03. React Router v6 🧭

```jsx
import { BrowserRouter, Routes, Route, Link, Navigate, Outlet } from 'react-router-dom';

function ProtectedRoute({ isAuthed }) {
  return isAuthed ? <Outlet /> : <Navigate to="/login" replace />;
}

export default function App() {
  const isAuthed = true;

  return (
    <BrowserRouter>
      <nav><Link to="/">Home</Link> | <Link to="/dashboard">Dashboard</Link></nav>
      <Routes>
        <Route path="/" element={<h1>Home</h1>} />
        <Route element={<ProtectedRoute isAuthed={isAuthed} />}>
          <Route path="/dashboard" element={<h1>Dashboard</h1>} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}
```

## Hooks
- `useNavigate` programmatic navigation
- `useParams` route params
- `useLocation` current location metadata

## Lazy routes
```jsx
import { lazy, Suspense } from 'react';
const Settings = lazy(() => import('./Settings'));
```

## When to use
- Multi-page SPA navigation and nested layouts

## When NOT to use
- Very small one-screen widgets

> ⚠️ **Mistake to avoid:** Wrapping nested routes incorrectly without `<Outlet />`.
