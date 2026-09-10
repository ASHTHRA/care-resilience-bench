# CareResilience Bench

**An open resilience & failure-testing framework for FHIR health-data applications.**

CareResilience Bench complements conformance testing by asking a different question: when dependencies fail in realistic ways, does a health-data application degrade safely?

## MVP v0.1.0

The first public prototype includes a synthetic FHIR-like reference endpoint and six executable failure scenarios:

1. Latency spike
2. Expired OAuth token
3. Partial patient record
4. Flapping FHIR endpoint
5. Duplicate resource
6. Stale clinical data

The dashboard executes the scenarios, applies explicit safety assertions, produces a resilience score, and exports a machine-readable JSON evidence artifact.

## Run locally

```bash
npm install
npm run dev
```

Open `http://localhost:3000`.

## Build

```bash
npm run build
npm start
```

## Safety and scope

- Synthetic demonstration data only.
- Do not submit protected health information (PHI).
- This is a research/engineering prototype, not a clinical decision support system or certification tool.
- The current score is a prototype benchmark metric and is not an ONC or HL7 certification result.

## Next milestones

- External target URL support
- Scenario DSL / YAML manifests
- SMART/OAuth fault proxy
- FHIR Bundle semantic completeness assertions
- Repeat-run statistics and confidence intervals
- Docker/CLI runner
- CI integration and signed evidence artifacts
- Public benchmark corpus and methodology paper

## License

MIT
