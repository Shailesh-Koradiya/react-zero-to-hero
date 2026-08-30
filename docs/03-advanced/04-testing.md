# 04. Testing React ✅

## Stack
- Jest
- React Testing Library (RTL)

```jsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import Counter from './Counter';

test('increments counter', async () => {
  const user = userEvent.setup();
  render(<Counter />);
  await user.click(screen.getByRole('button', { name: /increment/i }));
  expect(screen.getByText(/count: 1/i)).toBeInTheDocument();
});
```

## What to test
- Unit: isolated logic/component
- Integration: components working together
- Async flows: loading → success/error

## Mocking
Mock APIs (`msw` preferred) instead of brittle manual fetch mocks.

## When to use snapshot tests
- Stable UI atoms/components only

## When NOT to rely on snapshots
- Complex changing UI (high noise, low signal)

> 💡 **Best Practice:** Test behavior the user sees, not implementation details.
