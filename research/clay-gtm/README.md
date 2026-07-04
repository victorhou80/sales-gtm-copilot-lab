# Minerva Clay GTM Research

Systematic public-source research on Clay / Claygent and a legal blueprint for building a Clay-like GTM automation platform.

Date: 2026-06-12

## Scope

This repository studies Clay / Claygent as a public product and company. It focuses on:

- What Clay is and who it serves.
- How its GTM data, enrichment, Claygent, signals, and workflow capabilities fit together.
- What can be legally replicated using original code, public information, authorized APIs, and compliant customer data.
- What should not be copied or attempted, including private code, non-public APIs, proprietary prompts, protected UI/brand assets, or unauthorized data access.
- How to build a localized / private-deployment version for China outbound and B2B GTM teams.

## Important Boundary

This research does not recommend copying Clay's private implementation. A safe product strategy is:

> Replicate the public problem shape and general system capabilities, not Clay's private code, private API, exact UI, brand, templates, customer materials, or non-public workflows.

## Repository Layout

| File | Purpose |
|---|---|
| `docs/01-company-and-business.md` | Company, positioning, customers, pricing, business model, moat. |
| `docs/02-product-workflows.md` | Product model: sources, tables, enrichment, Claygent, signals, CRM, sequencer, ads. |
| `docs/03-20-round-debate.md` | Condensed 20-round debate and decision record from the five-worker research pass. |
| `docs/04-replication-blueprint.md` | Legal replication architecture, data model, workflow runtime, AI pipeline, MVP. |
| `docs/05-localization-private-deployment.md` | Localized and private-deployment strategy. |
| `docs/06-compliance-risk-checklist.md` | CAN-SPAM, GDPR/ePrivacy, CCPA/CPRA, LinkedIn risk, deliverability, AI review. |
| `docs/07-open-source-and-api-stack.md` | Open-source components, license notes, and which capabilities should be bought as APIs. |
| `docs/08-roadmap.md` | 30/60/90-day build plan and longer commercial roadmap. |
| `docs/09-sources.md` | Key public sources used. |

## Executive Summary

Clay is best understood as a GTM data operating system:

```text
GTM tables
  -> data sources / CRM / CSV / webhooks
  -> enrichment and waterfall providers
  -> Claygent-style AI web research
  -> signals and scoring
  -> personalization
  -> CRM, sequencer, ads, warehouse, API actions
  -> usage-based billing and enterprise controls
```

The strongest legal replication opportunity is not a full Clay clone. The first product should be a focused vertical wedge:

> Upload company or lead lists, automatically research public company context, score ICP fit, generate evidence-backed outreach snippets, and write results back to CRM or spreadsheets.

That wedge captures the useful core without immediately taking on 150+ data sources, a complete workflow builder, a full sequencer, enterprise warehouse sync, or high-risk scraping.

## Recommended First Product

Build a localized, private-deployable AI GTM research platform:

- CSV/Excel/CRM import.
- Company website discovery.
- Public web research.
- Structured AI extraction.
- ICP scoring.
- Evidence URLs and confidence.
- Personalized English/multilingual opener generation.
- Human review queue.
- HubSpot / Pipedrive / Google Sheets / Feishu export.
- Local model / BYOK / hybrid model modes.
- Compliance and audit logs from day one.

## Non-Goals

Do not build or market the product as:

- A LinkedIn scraping tool.
- An email blasting tool.
- A domain-rotation deliverability bypass tool.
- A source-unknown email database.
- A system that sends AI-generated claims without review.
- A clone of Clay's private implementation.

## High-Level Build Strategy

1. Use permissive open-source infrastructure for speed: PostgreSQL, pgvector, Playwright, Next.js, NestJS/FastAPI, BullMQ/Celery, LiteLLM, Langfuse.
2. Buy or BYO the parts that are usually not worth self-building: search/SERP, commercial data, email verification, email delivery, and frontier LLM inference.
3. Self-build the product core: GTM table model, field lineage, workflow execution, connector SDK, usage ledger, tenant isolation, audit logs, compliance defaults.
4. Keep GPL/AGPL tools such as Mautic/listmonk as references or isolated services, not as the closed SaaS core.

## Suggested Product Name Direction

For a localized version, avoid "Clay clone" positioning. Better categories:

- AI outbound GTM workspace.
- AI account research and enrichment platform.
- AI customer research system for China outbound teams.
- Private-deployable GTM data automation platform.

