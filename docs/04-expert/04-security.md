# 04. React Security 🔐

## XSS prevention
- React escapes strings by default
- Avoid `dangerouslySetInnerHTML` unless sanitized

```jsx
import DOMPurify from 'dompurify';

function SafeHtml({ html }) {
  return <div dangerouslySetInnerHTML={{ __html: DOMPurify.sanitize(html) }} />;
}
```

## CSRF
Use SameSite cookies, CSRF tokens, and server validation.

## Auth
- JWT: short-lived access + rotating refresh token strategy
- OAuth/OIDC for third-party identity providers

## Env vars
Never expose secrets in client bundles (`VITE_`/`NEXT_PUBLIC_` are public).

## CSP
Set strict Content Security Policy and avoid inline scripts.

## Input validation
Validate both client-side and server-side.

## When to use
- Always. Security is baseline, not optional.

## When NOT to skip
- Any production release.
