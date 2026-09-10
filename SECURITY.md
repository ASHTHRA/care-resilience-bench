# Security policy

CareResilience Bench is a research prototype for synthetic or explicitly public FHIR test data.

## Do not report real patient data

Never include PHI, credentials, bearer tokens, production endpoint secrets, or private signing keys in an issue, pull request, benchmark artifact, or security report.

## Security-sensitive areas

Changes to proxy target validation, URL handling, request forwarding, authentication simulation, evidence signing, and artifact verification deserve additional review.

The hosted implementation should use explicit upstream allowlists and must not become a general-purpose HTTP proxy.

## Reporting

For now, use a private repository-owner contact channel for security-sensitive reports rather than posting exploit details publicly. A dedicated security contact can be published in a later release.
