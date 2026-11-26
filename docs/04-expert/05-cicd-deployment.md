# 05. CI/CD & Deployment 🚢

## GitHub Actions
```yaml
name: ci
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npm test -- --watch=false
      - run: npm run build
```

## Docker (React static build)
```Dockerfile
FROM node:20-alpine AS build
WORKDIR /app
COPY . .
RUN npm ci && npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
```

## Deployment targets
- Vercel: frictionless for Next.js
- Netlify: strong static hosting + previews
- AWS: ECS/S3+CloudFront for custom infra

## Performance monitoring
Use Lighthouse, Web Vitals, Sentry, Datadog/New Relic.

## When to use advanced pipelines
- Team workflows with quality gates and compliance needs

## When NOT to overcomplicate
- Solo prototypes with low deployment risk
