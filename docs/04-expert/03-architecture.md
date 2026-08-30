# 03. React Architecture 🏗️

## Feature-based folder structure
```txt
src/
  features/
    auth/
      components/
      hooks/
      api/
      store/
```

## Atomic Design
Atoms → Molecules → Organisms → Templates → Pages.

## Clean Architecture in React
UI layer depends on use-cases/interfaces, not concrete services.

## Monorepos
- Turborepo/Nx for shared packages and coordinated builds

## Micro-frontends
- Module Federation for independent deployability

## When to use
- Multi-team products with bounded contexts

## When NOT to use
- Small team/single app where monolith is easier

> ⚠️ **Pitfall:** Micro-frontends without strict contracts cause runtime chaos.
