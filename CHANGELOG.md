# Changelog

## 0.6.0 - 2026-09-10

- Added repeated-run study orchestration with preserved raw evidence.
- Added overall-score and per-scenario descriptive statistics.
- Added privacy-conscious provenance capture with Git/spec/corpus fingerprints.
- Added self-verifying benchmark release bundles with SHA-256 file manifests.
- Added optional Ed25519 release-manifest signing and verification.
- Added provenance, statistics, and release-manifest JSON Schemas.
- Added statistics regression tests and CI coverage.

All notable CareResilience Bench milestones are documented here.

## 0.5.0 — 2026-09-10

- Added deterministic `core-v1` evaluator corpus with passing and failing reference observations.
- Added corpus regression validation using the shared evaluator core.
- Added SHA-256 evidence integrity manifests.
- Added optional Ed25519 evidence signing and independent verification tooling.
- Added local keypair generation with private-key files excluded from source control.
- Added evidence integrity documentation and manifest JSON Schema.
- Added GitHub Actions CI for corpus validation, TypeScript checks, and production build.

## 0.4.0 — 2026-09-10

- Added external application observation contract.
- Added `/api/evaluate` scenario evaluator.
- Added reference observer adapter and external observation JSON Schema.
- Added research plan for comparative application testing.

## 0.3.0 — 2026-09-10

- Added formal benchmark specification, severity weights, evidence schema, threat model, and CLI runner.

## 0.2.0 — 2026-09-10

- Added allowlisted live FHIR proxy architecture and controlled fault injection.

## 0.1.0 — 2026-09-10

- Initial synthetic benchmark prototype with six failure scenarios and JSON evidence export.
