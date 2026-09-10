# CareResilience Bench v0.4.0

**Open resilience and failure testing for FHIR applications.**

CareResilience Bench asks a question that conformance testing alone does not answer: when the health-data environment around an application becomes slow, incomplete, stale, duplicated, unauthorized, or intermittently unavailable, does the consuming workflow detect and contain the problem?

## v0.4 milestone

v0.4 adds an external-client observation and evaluation layer so the benchmark can score third-party FHIR-consuming applications through a normalized adapter contract. Instead of generating every response locally, the benchmark first reaches a real public FHIR R4 test endpoint and then injects deterministic transport or payload faults into the response path.

Default allowlisted targets:

- HL7 Quality R4: `https://r4.quality.hl7.org/fhir`
- SMART Bulk Data public demo: `https://bulk-data.smarthealthit.org/fhir`

The hosted demo intentionally does **not** accept arbitrary upstream URLs. This prevents it from becoming an SSRF/open-proxy surface. Self-hosted users will later be able to configure an explicit allowlist through environment configuration.

## Benchmark scenarios

1. Latency spike
2. Expired OAuth token
3. Partial result set
4. Flapping FHIR endpoint
5. Duplicate resource
6. Stale clinical data

## Architecture

```text
Reference benchmark client
        |
        v
CareResilience controlled proxy
        |
        +-- transport fault injection (latency / 401 / 503)
        +-- payload mutation (partial / duplicate / stale)
        |
        v
Allowlisted public FHIR R4 test server
```

The evidence export records the target, resource type, capability probe, fault results, timing, methodology, and aggregate score.

## Important interpretation note

The current score measures the behavior of the **CareResilience reference benchmark client** against controlled injected failures. It is not yet a certification score for an external healthcare application. External client adapters and explicit safety assertions are planned for later milestones.

## Local development

```bash
npm install
npm run dev
```

Then open `http://localhost:3000`.

## API examples

Health:

```bash
curl http://localhost:3000/api/health
```

Probe a target:

```bash
curl "http://localhost:3000/api/benchmark?target=hl7-quality-r4"
```

Live proxy without a fault:

```bash
curl "http://localhost:3000/api/proxy?target=hl7-quality-r4&resource=Patient&count=5&fault=none"
```

Inject a duplicate resource:

```bash
curl "http://localhost:3000/api/proxy?target=hl7-quality-r4&resource=Patient&count=5&fault=duplicate-resource"
```

## Safety / privacy

This research prototype is intended for synthetic or explicitly public test data only. Do not use the hosted demo with PHI or production healthcare systems. It is not a clinical device and must not be used for clinical decision-making.

## Roadmap

- **v0.1** synthetic reference benchmark — complete
- **v0.2** live allowlisted FHIR proxy + reproducible evidence — complete
- **v0.3** formal assertion model, severity weights, evidence schema, CLI runner — complete
- **v0.4** external application/client adapter and evaluation contract — complete
- **v0.5** benchmark corpus + CI integration + signed evidence manifests
- **v1.0** documented public benchmark methodology and comparative study

## License

MIT
