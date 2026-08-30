# 02. Context API 🌐

## createContext + Provider + useContext
```jsx
import { createContext, useContext, useMemo, useState } from 'react';

const ThemeContext = createContext(null);

export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  const value = useMemo(() => ({ theme, setTheme }), [theme]);
  return <ThemeContext.Provider value={value}>{children}</ThemeContext.Provider>;
}

export function useTheme() {
  const ctx = useContext(ThemeContext);
  if (!ctx) throw new Error('useTheme must be used inside ThemeProvider');
  return ctx;
}
```

## Context vs props drilling
Context removes repetitive pass-through props for app-wide concerns.

## Multiple contexts
Compose providers: AuthProvider + ThemeProvider + LocaleProvider.

## When to use context
- Theme, locale, auth session, feature flags

## When NOT to use
- Frequently changing deeply nested business state (can trigger broad renders)

> 💡 **Performance Tip:** Split contexts by concern and memoize provider value.

## Common mistakes
- Huge “global context” object
- Non-memoized provider values
