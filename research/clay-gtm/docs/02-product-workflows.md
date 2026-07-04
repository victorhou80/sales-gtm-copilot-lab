# Product Workflows

## Clay Product Mental Model

Clay works like a spreadsheet that can execute GTM actions.

```text
Source records
  -> table rows
  -> enrichment / AI / formula columns
  -> scoring and routing
  -> actions to CRM, sequencer, warehouse, Slack, ads, API
```

Each row is usually a company, person, account, lead, or event. Each column may be:

- A raw imported field.
- A provider enrichment output.
- A waterfall output.
- An AI extraction / classification.
- A formula.
- A lookup from another table.
- A status or action result.

## Input Sources

Common source types:

- CRM objects from HubSpot, Salesforce, or similar systems.
- CSV imports.
- Webhooks.
- List builders.
- Forms and inbound leads.
- Existing customer data.
- External APIs.

## Company and People Tables

Clay-style workflows often separate company and person records:

- Company table: domain, company LinkedIn/social URL, company size, industry, funding, jobs, tech stack, news, website signals.
- People table: name, role, company domain, work email, phone, LinkedIn URL, persona, seniority, outreach personalization.

The company table produces account context. The people table uses lookup logic to reuse that context for each contact.

## Waterfall Enrichment

Waterfall enrichment calls several providers in sequence:

```text
Need work email
  -> provider A
  -> if empty, provider B
  -> if empty, provider C
  -> validate email
  -> write result + successful provider + confidence
```

Why it matters:

- Higher coverage.
- Lower duplicate spend.
- Provider-level fallback.
- Better regional or field-specific routing.

For a replicated product, the first waterfall should be narrow:

- Company domain discovery.
- Work email finding.
- Email validation.
- Company firmographics.
- Jobs / hiring signals.
- Tech stack signal.

## Claygent-Style AI Research

Claygent is best understood as a row-level AI research worker.

For each row, it can:

- Search the web.
- Read a target website.
- Extract structured facts.
- Classify a company or page.
- Find non-standard GTM fields.
- Generate evidence-backed sales insights.
- Create outreach snippets.

Example outputs:

```json
{
  "company_summary": "B2B analytics platform for RevOps teams",
  "target_persona": "VP Sales / RevOps",
  "pricing_public": true,
  "has_api_docs": true,
  "recent_trigger": "Hiring SDR Manager",
  "fit_score": 82,
  "fit_reason": "Matches SaaS ICP and shows outbound scaling signal",
  "evidence_urls": ["https://example.com/careers", "https://example.com/pricing"]
}
```

## Agent Builder and Prompt Versioning

A high-value Claygent-like feature is not only "run a prompt." It is:

- Natural-language task setup.
- Input/output schema definition.
- Test rows.
- Model comparison.
- Cost estimate.
- Prompt versioning.
- Rollback.
- Bulk deployment.

This is legally replicable as a generic product pattern.

## Signals

Signals are events that trigger GTM action:

- Job changes.
- Promotions.
- New hires.
- Company news.
- Funding.
- Hiring pages.
- Web intent.
- CRM status changes.
- Product usage or support events.

For a new product, start with low-risk signals:

- Customer-owned web intent.
- CRM events.
- RSS/news APIs.
- Company careers pages where access is allowed.
- Public company blogs/news pages.
- Authorized data vendor events.

Avoid making LinkedIn scraping a core signal source.

## Personalization Workflow

A Clay-style personalized outreach workflow:

```text
company/person row
  -> basic enrichment
  -> web research
  -> ICP scoring
  -> evidence-backed insight
  -> opener / subject / email snippet
  -> human review
  -> CRM or sequencer export
```

Good personalization connects a real prospect-specific signal to the buyer's likely problem. Bad personalization simply says "I saw your website" or fabricates facts.

## CRM and Execution Integrations

The execution layer should support:

- HubSpot import, update, upsert, association.
- Salesforce import, SOQL lookup, update, upsert, lead conversion.
- Pipedrive / Zoho / Attio exports.
- Google Sheets export.
- Webhook and HTTP API.
- Smartlead / Instantly / Outreach handoff.
- Slack alerts.
- Data warehouse export later.

## Ads Audiences

ABM workflows can sync qualified accounts or hashed contacts to ad platforms such as LinkedIn, Meta, or Google, but only through official APIs and with proper consent/terms compliance.

## Templates / Playbooks

Clay's workflow library is part of the product value. A replicated system should build templates around specific GTM jobs:

- Enrich inbound demo requests.
- Score target accounts.
- Find companies hiring sales roles.
- Identify companies with public pricing pages.
- Find companies with integrations/API docs.
- Generate pre-meeting research notes.
- Detect expansion/retention risk from CRM and call notes.
- Write personalized first lines from evidence-backed signals.

