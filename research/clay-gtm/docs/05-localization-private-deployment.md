# Localization and Private Deployment

## Can This Be Localized?

Yes. A Clay-like GTM platform can be localized and privately deployed. In fact, localization and private deployment may be the strongest wedge against a broad incumbent.

The core system can run locally. Some capabilities still require external services:

- Search/SERP.
- Commercial contact/company data.
- Email verification.
- Email delivery.
- Ads APIs.
- Some CRM APIs.
- Frontier LLMs, unless local models are sufficient.

## Four Layers of Localization

### 1. UI and Business Workflow Localization

Can be fully localized:

- Chinese UI.
- Chinese/English/multilingual prompt templates.
- China outbound sales workflows.
- Export sales / foreign trade playbooks.
- Feishu, WeCom, DingTalk, Zoho, Pipedrive, HubSpot integrations.
- Multilingual outreach generation.
- Local ICP templates.
- Local compliance warnings.

### 2. Private Deployment

Can be privately deployed:

- Web frontend.
- API server.
- PostgreSQL.
- pgvector.
- Redis/Valkey.
- MinIO / S3-compatible storage.
- Queue workers.
- Prompt registry.
- Audit logs.
- Local model server.
- Egress gateway.
- Connector allowlist.

### 3. Local AI

Local models are suitable for:

- Summaries.
- Classification.
- ICP screening.
- Translation.
- Simple extraction.
- Email draft first pass.
- Embeddings.
- Deduplication and similarity.

Hybrid model mode is recommended:

```text
Local small/medium models
  -> classification, summary, embedding, low-risk draft

Cloud or customer-approved frontier models
  -> difficult research, high-value personalization, complex reasoning
```

Supported modes:

- Local only.
- BYOK.
- Hybrid.

### 4. China Outbound GTM Localization

High-value target use cases:

- Foreign trade lead research.
- B2B SaaS outbound research.
- Distributor / importer / reseller identification.
- Exhibition list enrichment.
- Inquiry qualification.
- Website and product catalog analysis.
- Multilingual email and WhatsApp draft generation.
- CRM enrichment for HubSpot, Pipedrive, Zoho, Feishu, WeCom.
- Sales follow-up suggestions.

## Private Deployment Architecture

```text
Customer VPC / private cloud
  |
  |-- Web App
  |-- API Server
  |-- PostgreSQL + pgvector
  |-- Redis / Valkey
  |-- MinIO
  |-- Worker Queue
  |-- Local LLM Server
  |     |-- vLLM / Ollama / llama.cpp / TGI
  |
  |-- Egress Gateway
        |-- Search API allowlist
        |-- CRM API allowlist
        |-- Email provider allowlist
        |-- Data vendor allowlist
```

## Fully Localizable Modules

- Users / organizations / permissions.
- Table workspace.
- CSV / Excel import.
- Customer and company database.
- ICP scoring rules.
- Prompt templates.
- Job queue.
- Run logs.
- Audit logs.
- Cost tracking.
- Source ledger.
- Suppression list.
- Human review queue.
- Local model inference.
- Embedding retrieval.
- Report generation.
- Email draft generation.
- Multilingual translation.

## Hard-to-Localize Modules

These are better bought as APIs or integrated through BYO keys:

- Global search/SERP.
- Commercial contact database.
- Email and phone validation.
- LinkedIn data.
- Large-scale email deliverability.
- Ads audience sync.
- Company funding, hiring, and technographic real-time feeds.
- CAPTCHA and anti-bot infrastructure.

## Best Localized MVP

Start with:

> A private-deployable AI customer research and lead scoring system.

Workflow:

```text
Upload lead/company list
  -> find company websites
  -> analyze websites/news/careers pages
  -> generate company profile
  -> score ICP fit
  -> create multilingual sales talking points
  -> human review
  -> export to CRM/spreadsheet
```

Do not start with automated mass sending.

## Product Packaging

| Package | Target Customer | Commercial Model |
|---|---|---|
| Local Lite | Small teams, agencies | Annual license or one-time setup + maintenance. |
| Private Pro | China outbound companies, sales teams | Annual private deployment subscription. |
| Enterprise VPC | Larger companies | Project fee + annual support. |
| Cloud SaaS | General users | Subscription + usage. |
| Agency Edition | GTM agencies | Multi-client workspace pricing. |

## Messaging

Good positioning:

- AI customer research.
- Private-deployable GTM automation.
- Source-traceable sales intelligence.
- China outbound GTM workspace.
- Human-reviewed compliant outreach.

Avoid:

- LinkedIn scraper.
- Cold email blasting.
- Unlimited sender/domain rotation.
- Guaranteed reply rate.
- Fully automated sales replacement.

