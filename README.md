# CareResilience Bench v0.6.0

**Open resilience and failure testing for FHIR applications.**

CareResilience Bench asks a question that conformance testing alone does not answer: when the health-data environment around an application becomes slow, incomplete, stale, duplicated, unauthorized, or intermittently unavailable, does the consuming workflow detect and contain the problem?

## v0.6 milestone

v0.6 turns individual benchmark runs into auditable studies. It adds repeated-run orchestration, descriptive statistics, privacy-conscious provenance capture, and self-verifying release bundles that hash every published artifact.

v0.5 integrity manifests and the external-client observation contract remain supported.

## Core scenarios

1. Latency spike
2. Expired OAuth token
3. Partial result set
4. Flapping FHIR endpoint
5. Duplicate resource
6. Stale clinical data

## Architecture

```text
FHIR test server
      |
      v
CareResilience controlled fault proxy
      |
      v
Application under test
      |
      v
Observation adapter
      |
      v
CareResilience evaluator
      |
      +--> evidence.json
              |
              +--> SHA-256 manifest
                      |
                      +--> optional Ed25519 signature
```

## Deterministic benchmark corpus

The `corpus/core-v1` directory contains synthetic reference observations with fixed expected pass/fail outcomes. They provide regression protection for the evaluator and contain no clinical data.

```bash
npm run validate:corpus
```

A release should not silently change an existing corpus outcome without an explicit benchmark-methodology change.

## Evidence integrity

Generate a SHA-256 manifest for an evidence file:

```bash
npm run manifest -- artifacts/evidence/run.json artifacts/manifests/run.manifest.json
```

Verify it:

```bash
npm run verify:manifest -- artifacts/evidence/run.json artifacts/manifests/run.manifest.json
```

For attributable evidence, generate an Ed25519 key pair locally, set `CARE_SIGNING_PRIVATE_KEY`, and regenerate the manifest. See `docs/EVIDENCE_INTEGRITY.md`.


## Repeated-run study

Run five sequential benchmark executions and preserve every raw result:

```bash
npm run study
```

Override the count and destination:

```bash
CARE_RUNS=10 CARE_STUDY_DIR=artifacts/studies/demo npm run study
```

The study produces `evidence/`, `statistics.json`, `provenance.json`, and `study.json`. Statistics include overall-score mean/median/range/sample standard deviation/95% descriptive interval plus per-scenario pass rate and duration summaries.

## Provenance

```bash
npm run provenance -- artifacts/studies/provenance.json
```

Provenance records code/spec/corpus fingerprints and runtime context while intentionally excluding hostnames, usernames, tokens, and environment-variable values.

## Release bundles

```bash
npm run release:bundle -- artifacts/studies/demo artifacts/releases/demo-v0.6
npm run release:verify -- artifacts/releases/demo-v0.6
```

Every included study artifact receives a SHA-256 entry in the release manifest. Optional Ed25519 signing uses the same signing-key environment variables introduced in v0.5.

## CI

`.github/workflows/ci.yml` runs on pushes and pull requests to `main` and performs:

- corpus validation;
- TypeScript typechecking;
- production Next.js build.

## Local development

```bash
npm install
npm run dev
```

Then open `http://localhost:3000`.

## Public FHIR test targets

The reference proxy uses an explicit allowlist. The project is designed for synthetic or explicitly public test data and should not be pointed at production clinical systems without an approved, controlled deployment.

## Safety and interpretation

CareResilience Bench is a research and engineering prototype. It is not an ONC or HL7 certification result, not a medical device, and not a clinical decision-support system. A high benchmark score does not establish overall clinical safety.

## Roadmap

- **v0.1** synthetic reference benchmark — complete
- **v0.2** live allowlisted FHIR proxy + reproducible evidence — complete
- **v0.3** formal assertion model, severity weights, evidence schema, CLI runner — complete
- **v0.4** external application/client adapter and evaluation contract — complete
- **v0.5** benchmark corpus + CI + integrity manifests + optional signatures — complete
- **v0.6** provenance capture + repeat-run statistics + benchmark release bundles — complete
- **v0.7** real application study adapters + publishable comparison tables
- **v1.0** documented public benchmark methodology and comparative study

## Repository structure

```text
app/                         Next.js dashboard and API routes
lib/                         benchmark, FHIR, target, and evaluator logic
adapters/                    external-client observer adapters
corpus/core-v1/              deterministic evaluator regression corpus
docs/                        benchmark, adapter, threat, study, integrity docs
schemas/                     machine-readable evidence/observation schemas
scripts/                     CLI, repeated studies, statistics, provenance, release verification
.github/workflows/           automated CI
```

## License

MIT
