# 20-Round Debate Record

This document condenses the five-worker research pass into explicit decisions.

## Participants

- Worker A: company, business model, pricing, moat.
- Worker B: product workflows and public capability map.
- Worker C: engineering replication architecture.
- Worker D: compliance, data, deliverability, platform risk.
- Worker E: open-source/API stack and migration path.

## Decision Table

| Round | Debate Question | Decision |
|---:|---|---|
| 1 | Is Clay a data vendor or automation platform? | Clay is a GTM data orchestration platform, not a single data vendor. |
| 2 | Is Claygent just a chatbot? | No. It is a row-level AI web research and extraction worker for GTM tables. |
| 3 | What is the main moat? | The moat is data provider network + workflow knowledge + product embedding + compliance trust. |
| 4 | Should we copy the full 150+ provider network? | No. Start with 5-10 authorized, high-value providers. |
| 5 | Should the MVP clone all of Clay? | No. Build a focused account research and enrichment wedge. |
| 6 | Should the UI mimic Clay? | Use table and column mental model, but do not copy Clay's exact UI, copy, or brand. |
| 7 | What is hard about waterfall enrichment? | Cost routing, coverage, provider reliability, caching, confidence, error handling. |
| 8 | What is hard about AI research? | Evidence, anti-hallucination, structured outputs, page extraction, source ranking. |
| 9 | Should the MVP send cold emails directly? | Not first. Export to CRM/sequencer first; add sending after compliance and deliverability are mature. |
| 10 | When should a native sequencer be built? | After data quality, review, unsubscribe, suppression, and sender health controls exist. |
| 11 | Should LinkedIn scraping be a feature? | No. Treat LinkedIn as high-risk; use authorized APIs or customer-provided fields only. |
| 12 | Can open source assemble the product? | It can accelerate the prototype, but the core table/runtime/lineage/tenant layer should be original. |
| 13 | Should Mautic/listmonk be used as the product core? | No. Useful references or isolated services, but license and data-model fit are poor for a closed Clay-like SaaS core. |
| 14 | Should Activepieces/Flowise be used in production? | Useful for internal prototyping; production runtime should gradually move to first-party execution logic. |
| 15 | What should be bought rather than built? | Search/SERP, email delivery, email verification, commercial contact/company data, high-end LLM inference. |
| 16 | Biggest legal risk? | Data source legitimacy, electronic marketing rules, unsubscribe handling, LinkedIn/platform ToS. |
| 17 | What do enterprise customers require? | DPA, subprocessors, audit logs, SSO/RBAC, no training on customer data, security controls. |
| 18 | What is special for China outbound teams? | Need China workflows plus US/EU marketing law plus PIPL/cross-border handling. |
| 19 | What is the smallest sellable product? | Upload company list -> AI research -> ICP score -> evidence-backed opener -> CRM/spreadsheet export. |
| 20 | Final replication strategy? | Replicate Clay's public problem shape and general system capabilities, not Clay itself. |

## Final Verdict

Build a private-deployable AI GTM research and enrichment platform. Use a table-like GTM workspace, not a generic workflow canvas as the first user surface.

The first version should be:

```text
CSV/CRM import
  -> company website discovery
  -> public web research
  -> structured AI extraction
  -> ICP scoring
  -> evidence-backed personalized opener
  -> human review
  -> CRM/spreadsheet export
```

## Product Positioning Decision

Avoid "Clay clone" language.

Better positioning:

- AI account research and enrichment platform.
- Private-deployable GTM data automation platform.
- AI outbound GTM workspace for China outbound teams.
- AI customer research and sales enablement system.

## Build/Buy Decision

Build:

- GTM table model.
- Field lineage.
- Workflow run ledger.
- Connector SDK.
- Tenant and permission model.
- Usage ledger.
- Audit and compliance controls.
- AI prompt/version/test layer.

Buy or BYO:

- Search/SERP.
- Commercial contact/company data.
- Email verification.
- Email delivery.
- Some frontier LLM inference.
- Ads/CRM official APIs.

Prototype with:

- Activepieces / Node-RED for internal connector experiments.
- Flowise / Langflow for internal AI recipe experiments.
- Dittofeed for lifecycle messaging ideas.

Avoid as closed SaaS core:

- Deeply modified GPL/AGPL marketing systems.
- Unauthorized scraping tools.
- Data broker behavior without contracts and compliance.

