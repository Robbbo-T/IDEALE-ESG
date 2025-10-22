# IDEALE-ESG

**Information & Intelligence · Defense · Energy · Aerospace · Logistics · Economics · Environmental, Social & Governance**

> Audit‑ready ESG platform for high‑assurance programs. Security, traceability, reliability by design.

---

## Vision

IDEALE‑ESG delivers a production‑grade platform to manage, analyze, and disclose ESG data. It provides trusted insights through strict data contracts, modern engineering practice, and a secure‑by‑design approach suitable for regulated environments.

---

## Architecture Overview

* **Schema‑first**: Versioned data contracts in **`/schemas/**`** are the single source of truth for this repo. Services generate types and validators from these schemas to guarantee integrity. If used alongside IDEALE‑EU, map or import shared contracts from `IDEALEEU:/00-PROGRAM/platform/schemas`.
* **Service‑oriented**: Backend functionality is decomposed into FastAPI (Python) or Fastify (TypeScript) services behind an API Gateway; asynchronous workflows via NATS.
* **Secure by design**: OAuth2/OIDC, RBAC/ABAC, strict input validation, output encoding, least privilege, secrets in KMS/secret store.
* **Traceability**: Structured logs, metrics, and traces with correlation/subject IDs; tamper‑evident audit events; SBOM + provenance on releases.

---

## Technology Stack

| Area      | Choice                                                                  |
| --------- | ----------------------------------------------------------------------- |
| Backend   | Python 3.11+ (FastAPI) · TypeScript/Node 20+ (Fastify)                  |
| Frontend  | React 18 (Vite) · Tailwind CSS (optional shadcn/ui)                     |
| Data      | PostgreSQL (OLTP) · pgvector / Qdrant (vector)                          |
| APIs      | REST & GraphQL via API Gateway · OpenAPI/GraphQL generated from source  |
| Messaging | NATS (async events, workflows)                                          |
| Testing   | Pytest · Vitest/Jest · Playwright                                       |
| Tooling   | Ruff · Black · mypy(strict) · ESLint · Prettier · Make · Docker/Compose |

---

## Repository Layout

```
IDEALE-ESG/
├─ README.md
├─ LICENSE
├─ .gitignore
├─ .github/
│  ├─ ISSUE_TEMPLATE/
│  ├─ PULL_REQUEST_TEMPLATE.md
│  └─ workflows/ci.yml
├─ docs/                      # Guides, ADRs, mappings (GRI, SASB, CSRD/ESRS)
├─ schemas/                   # ESG data contracts (SoT for this repo)
│  └─ esg/
│     ├─ KPI.v1.json
│     ├─ Evidence.v1.json
│     └─ Report.v1.json
├─ api/
│  └─ openapi.yaml            # ESG reporting and evidence endpoints
├─ services/                  # FastAPI/Fastify microservices
├─ ui/                        # React apps (dashboards, disclosures)
├─ dashboards/                # BI configs / notebooks
├─ tools/                     # CLIs, generators, linters
├─ examples/                  # Sample payloads and API calls
└─ data/                      # Sample datasets (non‑PII)
```

> PLM/MRO content remains in product portfolios of IDEALE‑EU. This repo focuses on ESG contracts, services, and disclosures.

---

## Getting Started

> Initial bootstrap. See `/docs` for full guides.

**Prerequisites**: Python 3.11+, Node 20+, Docker & Compose, git.

```bash
# Clone
git clone https://github.com/Robbbo-T/IDEALE-ESG.git
cd IDEALE-ESG

# Install tooling (optional)
pip install -r requirements.txt || true
npm ci || npm i

# Lint + tests (if present)
npm run -s lint || true
npm test || true
pytest -q || true

# Run a local stack (example)
docker compose up -d
```

---

## Key Directories

* `schemas/esg/**` — **Source of truth** for ESG contracts. Versioned folders; backward‑compatible minor, breaking major.
* `api/openapi.yaml` — ESG endpoints; generated/updated with services.
* `services/` — Backend services. One framework per service (FastAPI **or** Fastify), consistent per service.
* `ui/` — Disclosure dashboards and admin UIs (React + Vite + Tailwind).
* `docs/` — ADRs, mappings (GRI, SASB, CSRD/ESRS), runbooks.
* `dashboards/` — BI views and KPI boards.
* `tools/` · `examples/` · `data/` — developer utilities and samples.

---

## Development Principles

* Clarity over cleverness; explicit, typed code.
* Least privilege; validate at boundaries; redact logs.
* Treat contracts as code; generate validators/types from `schemas/**`.
* Tests are mandatory: unit (logic), contract (schemas), integration (I/O). Deterministic.
* Pure domain logic; side effects at edges; dependency injection for testability.
* Keep README, docs, and OpenAPI/GraphQL in sync with code.

---

## APIs (preview)

* `POST /esg/v1/evidence` — submit evidence payloads
* `POST /esg/v1/kpis/compute` — compute KPI set for scope/period
* `GET  /esg/v1/reports/{id}` — fetch assembled report
* `POST /esg/v1/reports` — create draft report

> See `api/openapi.yaml` for the full spec once generated.

---

## Security

* OAuth2/OIDC; RBAC + ABAC. Secrets via KMS/secret store.
* Input validation, output encoding, CSRF where applicable.
* SBOM (CycloneDX) and SLSA provenance attached to releases.
* No PII in logs; redaction by default; correlation IDs for audit.

Security issues: **[security@idealeeu.eu](mailto:security@idealeeu.eu)**. Do not open public issues. See `SECURITY.md`.

---

## Contributing

Follow IDEALE‑EU coding standards (TypeScript strict, Python mypy‑strict, parameterized SQL). See `CONTRIBUTING.md`.

---

## License

Apache‑2.0 (proposed). See `LICENSE`.

---

*Last updated: 2025‑10‑22*
