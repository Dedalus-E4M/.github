# Engage4Me (E4M) — organization context

Multi-tenant healthcare **care-coordination SaaS** by **Dedalus**.
SaaS-first; a few on-premise installs remain.

## Stack in one line

Microservices on Kubernetes (strangler fig from a monolith) · Java/Spring Boot/Maven ·
NestJS (BFF) · Angular 18+ standalone (E4P) · Flutter (C4P) · PostgreSQL (MongoDB frozen) ·
Keycloak (OIDC/JWT) + SpiceDB · TypeSpec→OpenAPI (design-first) · Mirth/HL7/FHIR ·
synchronous REST + PG LISTEN/NOTIFY (no broker) · GitHub Actions + ArgoCD.

## Non-negotiable constraints

- **Healthcare**: personal health data — never log PII/PHI.
- **Multi-tenant**: discriminator-column isolation, tenant passed via HTTP header.
- **Explicit errors**: no silent failure; honor DTO/OpenAPI contracts.
- **Forbidden**: MongoDB for a new service · any message broker · raw SQL (QueryDSL is mandatory) ·
  backend implementation before the TypeSpec contract · new backend framework without an ADR.

## Where the detail lives (do not duplicate here)

- Context, detailed stack, conventions, glossary → repo **`Dedalus-E4M/840_ia`**, folder `context/`
- Reusable AI skills → **`Dedalus-E4M/840_ia`**, `.github/skills/`
- Architecture Decision Records → repo **`Dedalus-E4M/900_adr`**

## Expected posture

**Pragmatic, production-ready** answers. Simplicity > cleverness. No toy examples.
Make trade-offs explicit (perf, scalability, security). Clean architecture / DDD aligned.

## Language

Shared docs and code in **English**. Healthcare domain terms kept in French (RCP, FINESS…).
