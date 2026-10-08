# Engage4Me (E4M) — organization context

Multi-tenant healthcare **care-coordination SaaS** by **Dedalus**.
SaaS-first; a few on-premise installs remain.

## Stack in one line

Microservices on Kubernetes (strangler fig from a monolith) · Java/Spring Boot/Maven ·
NestJS (BFF) · Angular 18+ standalone (E4P) · Flutter (C4P) · PostgreSQL (MongoDB frozen) ·
Keycloak (OIDC/JWT) + SpiceDB · TypeSpec→OpenAPI (design-first) · Mirth/HL7/FHIR ·
synchronous REST + PG LISTEN/NOTIFY (no broker) · GitHub Actions + ArgoCD.

## Non-negotiable constraints

- **Healthcare**: never log personally identifiable information (PII) or personal health
  information (PHI). Apply the safe-logging rules below; this is not a ban on useful diagnostics.
- **Multi-tenant**: discriminator-column isolation, tenant passed via HTTP header.
- **Explicit errors**: no silent failure; honor DTO/OpenAPI contracts.
- **Forbidden**: MongoDB for a new service · any message broker · raw SQL (QueryDSL is mandatory) ·
  backend implementation before the TypeSpec contract · new backend framework without an ADR.

## Safe logging

Protect sensitive values while preserving the information needed to diagnose failures.

- **Exclude personal and health data**: names, contact details, dates of birth, patient
  identifiers, diagnoses, treatments, clinical observations, and patient document contents.
- **Exclude secrets**: passwords, access/refresh tokens, session cookies, API keys, and
  authorization headers.
- **Select safe fields** instead of dumping request/response bodies, decoded identity
  claims, configuration objects, or raw errors that may contain the values above.
- **Keep useful diagnostics**: operation, error code, status, timing, and known-safe
  configuration filenames or paths, such as `agenda/rcp.json` and `pathway/pathways.json`.
  A filename, path, or UUID is not sensitive merely because of its type or variable name;
  assess what it identifies or contains. A patient identifier remains sensitive even if
  it is a UUID.
- **Redact the sensitive part, not all context**. User-supplied filenames, URL/query
  values, and error messages can contain personal data or secrets; retain their safe
  parts or use a known-safe resource name alongside the operation and status.
- **Justify diagnostic removal with evidence**: identify the sensitive value or a
  specific rule that requires its removal. Do not label harmless technical metadata a
  security defect without evidence. If classification is unclear, keep known-safe
  context and ask for clarification rather than impose blanket redaction.

## Where the detail lives (do not duplicate here)

- Context, detailed stack, conventions, glossary → repo **`Dedalus-E4M/840_ia`**, folder `context/`
- Reusable AI skills → **`Dedalus-E4M/840_ia`**, `.github/skills/`
- Architecture Decision Records → repo **`Dedalus-E4M/900_adr`**

## Expected posture

**Pragmatic, production-ready** answers. Simplicity > cleverness. No toy examples.
Make trade-offs explicit (perf, scalability, security). Clean architecture / DDD aligned.

## Language

Shared docs and code in **English**. Healthcare domain terms kept in French (RCP, FINESS…).
