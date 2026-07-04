# Legal Replication Blueprint

## Product Definition

Build an original product that helps GTM teams convert company/contact lists into actionable, evidence-backed sales and marketing intelligence.

Safe one-line scope:

> A GTM enrichment table that uses authorized data providers, public web research where allowed, and AI extraction to score accounts, create personalized insights, and sync results to business systems.

## What Can Be Replicated

These are generic capabilities and product patterns:

- Table-based GTM workspace.
- Rows as companies, contacts, accounts, leads, or events.
- Columns as raw fields, enrichment outputs, AI outputs, formulas, and action statuses.
- Waterfall enrichment with authorized providers.
- BYO API key mode.
- AI web research over allowed public pages.
- Evidence URLs and confidence scores.
- Prompt versioning, testing, and rollback.
- CRM sync.
- Webhooks and HTTP API actions.
- Ads audience sync through official APIs.
- Workflow templates and playbooks.
- Usage-based credits/actions.
- Enterprise controls such as SSO, RBAC, audit logs, and DPA.

## What Must Not Be Copied

- Clay private code.
- Clay private prompts.
- Non-public API endpoints.
- Login-only workflows.
- Exact UI, brand, icons, copy, customer case materials.
- Proprietary template wording or workflow expression.
- Data provider deals or coverage claims not actually earned.
- Any protected data.

## MVP Architecture

```text
Web App
  -> API Server
  -> PostgreSQL + pgvector
  -> Redis/Valkey Queue
  -> Object Storage
  -> Workers
       -> search worker
       -> page extraction worker
       -> AI extraction worker
       -> scoring worker
       -> CRM/export worker
```

Recommended stack:

- Frontend: Next.js + React + TanStack Table.
- Backend: NestJS or FastAPI.
- Database: PostgreSQL + pgvector.
- Queue: BullMQ/Valkey or Celery/RabbitMQ.
- AI provider abstraction: LiteLLM.
- Extraction: Playwright + trafilatura/Readability.
- Observability: OpenTelemetry + Sentry + Langfuse.
- Billing: Stripe + internal usage ledger.

## Core Modules

### Workspace / Tenant

- Organizations.
- Workspaces.
- Members and roles.
- API keys.
- Connector accounts.
- Billing owner.

### Dataset / Table

- Datasets.
- Rows.
- Columns.
- Cells.
- Cell provenance.
- Row status.
- Import/export jobs.

### Workflow Runtime

- Workflow definitions.
- Frozen workflow versions.
- Workflow runs.
- Step runs.
- Jobs.
- Retry and failure handling.
- Idempotency keys.

### Connector Framework

Every connector should declare:

- Auth type.
- Input schema.
- Output schema.
- Rate limit.
- Cost model.
- Retry policy.
- PII policy.
- Cache policy.
- Provenance output.

### AI Research

Pipeline:

```text
Normalize entity
  -> generate query plan
  -> retrieve sources
  -> extract page text
  -> rank evidence
  -> structured LLM extraction
  -> validate schema
  -> score confidence
  -> write back cells
```

### Compliance and Audit

From day one:

- Source ledger.
- Lawful basis / customer-provided source markers.
- Region strategy.
- Suppression list.
- Audit log.
- AI output history.
- Export history.
- Data deletion flow.

## Suggested Database Shape

```text
organizations
users
organization_members
workspaces

datasets
dataset_columns
dataset_rows
dataset_cells

workflows
workflow_versions
workflow_runs
workflow_step_runs
jobs

connectors
connector_accounts
connector_calls

ai_runs
research_artifacts
usage_ledger

crm_sync_jobs
suppression_list
audit_logs
```

Important fields for cells:

```text
value_json
value_text
confidence
source_refs_json
last_enriched_at
provider_key
prompt_version
cost_units
```

## First Workflow to Build

```text
Import companies CSV
  -> find official website
  -> extract homepage/pricing/careers/docs pages
  -> summarize company
  -> classify industry and ICP fit
  -> detect buying signals
  -> generate personalized opener
  -> write evidence URLs
  -> export to HubSpot/Google Sheets
```

## Example Output Schema

```json
{
  "company_summary": "string",
  "industry": "string",
  "target_persona": ["string"],
  "icp_fit_score": 0,
  "icp_fit_reason": "string",
  "buying_signals": [
    {
      "type": "hiring|pricing|integration|funding|product_launch|other",
      "description": "string",
      "source_url": "string",
      "confidence": 0.0
    }
  ],
  "personalized_opener": "string",
  "do_not_claim": ["string"]
}
```

## Engineering Constraints

- No external write action without idempotency.
- No AI output accepted without schema validation.
- No low-confidence claim inserted into email copy without review.
- No bulk execution without cost estimate.
- No connector call without audit trail.
- No scraping of login-only or prohibited sources.
- No production workflow mutation after run start; use workflow versions.

## Build Priorities

P0:

- CSV import.
- Table UI.
- Search provider.
- Page extraction.
- AI structured extraction.
- ICP scoring.
- Evidence and confidence.
- Export.

P1:

- BYO API key.
- Provider waterfall.
- Prompt versioning.
- CRM integration.
- Human review.
- Usage billing.

P2:

- Native sequencer.
- Signals.
- Ads audience sync.
- Warehouse sync.
- Enterprise deployment.

