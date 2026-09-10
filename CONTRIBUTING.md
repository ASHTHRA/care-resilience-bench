# Contributing

CareResilience Bench welcomes reproducible engineering and research contributions.

## Development principles

- Use synthetic or explicitly public test data only.
- Do not commit PHI, credentials, tokens, or private signing keys.
- New benchmark scenarios should state the failure model, observable safety requirement, expected evidence, and deterministic test cases.
- Changes that alter an existing corpus outcome should include a benchmark-spec rationale.
- Keep hosted proxy targets explicitly allowlisted; do not introduce arbitrary server-side URL fetching.

## Before opening a pull request

```bash
npm install
npm run validate:corpus
npm run typecheck
npm run build
```

Include tests or corpus cases for evaluator changes and update documentation when methodology changes.
