# Roadmap

## 30-Day Prototype

Goal:

> Prove that a company list can become structured, evidence-backed GTM intelligence.

Build:

- Workspace and basic auth.
- CSV import.
- Table UI.
- Company domain discovery.
- Search API connector.
- Web page extraction.
- AI structured extraction.
- ICP scoring.
- Evidence URLs.
- Export to CSV/Google Sheets.

Do not build:

- Native email sending.
- Complex workflow builder.
- 100 connectors.
- Marketplace.
- Full enterprise permissions.

Success metric:

- 500-2,000 companies processed with useful company summary, ICP score, and evidence-backed opener.

## 60-Day MVP

Goal:

> Make the product usable by a real GTM team or agency.

Add:

- HubSpot or Pipedrive integration.
- Prompt versioning.
- 10-row test mode.
- Bulk execution with cost estimate.
- Failed row retry.
- Usage ledger.
- Human review queue.
- Basic source ledger and audit logs.
- BYO OpenAI/Anthropic key.
- First waterfall provider chain.

Success metric:

- A user can import a list, test a workflow, run it in bulk, review outputs, and export/sync to CRM.

## 90-Day Paid Pilot

Goal:

> Sell a focused pilot to a China outbound / B2B SaaS / agency customer.

Add:

- Email verification provider.
- CRM writeback.
- Feishu/WeCom/Google Sheets export.
- Multilingual sales copy.
- Template library for 5-10 common plays.
- Compliance center MVP.
- Suppression list.
- Admin review.
- Local model option for classification/translation.

Success metric:

- A customer pays for a pilot because the product reduces account research and personalization workload.

## 6-Month Product

Add:

- More connectors.
- Better waterfall routing.
- Entity resolution.
- Field-level lineage.
- AI quality evals.
- Team permissions.
- Billing.
- Audit export.
- Private deployment package.
- Agency multi-client mode.

Optional:

- Native sequencer, but only after compliance and deliverability controls mature.

## 12-Month Platform

Add:

- Durable workflow runtime.
- Connector SDK.
- Template/playbook marketplace.
- Data warehouse sync.
- Enterprise SSO/RBAC.
- DPA/subprocessors portal.
- Data retention controls.
- SOC 2 readiness.
- BYOK / local-only / hybrid AI.
- Egress allowlist for private deployments.

## Product Wedges

Recommended wedges:

1. China outbound account research.
2. HubSpot-first AI enrichment.
3. Agency edition for GTM service providers.
4. AI research for vertical B2B markets.
5. Customer success expansion/renewal signals.

Avoid starting with:

- Generic Clay clone.
- LinkedIn scraper.
- Mass cold-email sender.
- Data broker without contracts.

## Team Needed

Minimum team:

- 1 full-stack/product engineer.
- 1 backend/platform engineer.
- 1 AI/data engineer.
- 1 GTM/operator domain expert.
- 1 part-time compliance/legal advisor.

## Build Quality Gates

Before production:

- Source ledger implemented.
- AI outputs schema-validated.
- Evidence displayed.
- Cost estimate before bulk run.
- Connector secrets encrypted.
- Tenant isolation tested.
- Audit logs immutable enough for support.
- Suppression list enforced.
- High-risk platform scraping disabled.
- Acceptable use policy written.

