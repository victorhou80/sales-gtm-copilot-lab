# Open-Source and API Stack

## Principle

Use open source as infrastructure and prototype acceleration. Self-build the product core.

Do not create a closed SaaS by heavily modifying GPL/AGPL marketing tools unless the business model accepts those license obligations.

## Recommended Stack

| Layer | Recommendation | Notes |
|---|---|---|
| Frontend | Next.js, React, TanStack Table | Table workspace and app UI. |
| Backend | NestJS or FastAPI | Modular API. |
| Database | PostgreSQL | Core relational store. |
| Vector | pgvector | Embeddings, similarity, entity resolution. |
| Queue | BullMQ + Valkey/Redis, or Celery/RabbitMQ | Async enrichment and exports. |
| Workflow | Start simple; later Temporal/Hatchet | Avoid overbuilding workflow DSL in MVP. |
| Web automation | Playwright | Only for allowed public pages and controlled tasks. |
| Extraction | trafilatura, Readability, unstructured | Page/document text extraction. |
| AI gateway | LiteLLM | Provider abstraction and BYOK. |
| LLM observability | Langfuse / Helicone | Prompt/version/cost tracing. |
| Auth | Auth.js, Keycloak, Ory | Depends on deployment model. |
| Audit/metrics | OpenTelemetry, Sentry, PostHog | Product and runtime observability. |

## Prototype Helpers

Useful for internal prototyping:

- Activepieces: connector and workflow inspiration.
- Node-RED: internal event flow experiments.
- Flowise: AI workflow recipe experiments.
- Langflow: AI agent/RAG workflow experiments.
- Dittofeed: customer journey and messaging ideas.
- Chatwoot: customer conversation and support source ideas.

Move away from these as the customer-facing core once the product direction is validated.

## License Notes

Lower-risk:

- MIT: generally friendly for commercial use.
- Apache-2.0: commercial friendly, includes patent grant.
- PostgreSQL License: commercial friendly.

Watch carefully:

- GPLv3: commercial use allowed, but modified/distributed derivative works carry copyleft obligations.
- AGPLv3: network service use of modified software can require offering source code to users.
- BSL / SSPL / custom source-available licenses: not classic open source; SaaS restrictions may apply.
- Open-core projects: community edition can be usable, but enterprise code may be proprietary.

## Component Matrix

| Capability | Candidate | Fit | Recommendation |
|---|---|---:|---|
| Marketing automation | Mautic | Medium | Reference or isolated service; avoid closed-core modification. |
| Newsletter/list management | listmonk | Medium | Good product, AGPL risk for closed SaaS. |
| Workflow automation | Activepieces | High for prototype | Use core ideas; self-build production runtime. |
| Event/workflow | Node-RED | Medium | Good internal tool, not ideal customer UX. |
| AI workflow | Flowise/Langflow | Medium-high | Use for internal recipes; harden or replace for production. |
| Customer engagement | Dittofeed | High | Useful if lifecycle messaging is needed. |
| Customer conversations | Chatwoot | Medium | Good support/chat source, not the GTM table core. |
| Database | PostgreSQL | High | Use as core. |
| Vector search | pgvector | High | Use early. |
| Browser automation | Playwright | High | Use with compliance guardrails. |

## Buy or BYO Instead of Building

### Search / SERP

Buy:

- Brave Search API.
- Tavily.
- SerpAPI.
- Exa.

Reason: self-building search is expensive and low leverage.

### Commercial Data

Buy or BYO:

- People/company data.
- Email discovery.
- Funding data.
- Technographics.
- Hiring data.
- Company firmographics.

Reason: quality, freshness, and legal rights matter more than scraper code.

### Email Delivery

Buy:

- Amazon SES.
- Mailgun.
- SendGrid.
- Postmark.

Reason: deliverability, bounce, complaint, DKIM/SPF/DMARC, and AUP controls are specialized.

### Email Verification

Buy:

- ZeroBounce.
- NeverBounce.
- Dropcontact.
- Hunter-style verification.

Reason: production-grade validation requires external network and reputation signals.

### LLM

Use hybrid:

- Cloud/frontier model for hard reasoning.
- Local models for classification, extraction, translation, embeddings, drafts.
- BYOK mode for enterprise customers.

## Recommended Migration Path

1. Prototype with open-source tools to validate workflows.
2. Build first-party table, run ledger, connector SDK, usage ledger, and audit model.
3. Keep external APIs behind provider abstractions.
4. Remove GPL/AGPL dependencies from closed customer-facing core unless legally planned.
5. Invest in quality evaluation, source tracking, field lineage, cost optimization, and compliance automation.

