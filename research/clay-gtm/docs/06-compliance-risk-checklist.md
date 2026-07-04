# Compliance and Risk Checklist

This is a product design checklist, not legal advice.

## Main Risk Areas

Clay-like GTM tools carry risk in four places:

1. Data source legitimacy.
2. Whether data can be used for marketing.
3. How messages are sent.
4. Whether opt-out, deletion, and platform rules are respected.

## Data Source Policy

Preferred sources:

- Customer-owned CRM data.
- Form submissions and event registrations.
- Existing customer data.
- Authorized data vendors.
- Official public company pages where access is allowed.
- News, company blogs, public career pages, public registries.
- Official APIs.

High-risk or prohibited sources:

- Unknown email lists.
- Bulk social profile scraping.
- LinkedIn automated scraping.
- Email guessing or dictionary attacks.
- Email appending without lawful basis.
- Login-only data.
- Paywalled data.
- CAPTCHA bypass.
- Fake accounts.
- Proxy pools used to evade platform restrictions.

Every contact should have:

```text
source_url
source_vendor
source_time
lawful_basis
region
consent_or_objection_status
```

## CAN-SPAM Baseline

For US commercial email:

- Do not use false or misleading header information.
- Do not use deceptive subject lines.
- Identify commercial messages as advertising where required.
- Include a valid physical postal address.
- Provide a clear opt-out method.
- Keep opt-out working for at least 30 days after sending.
- Process opt-outs within 10 business days.
- Do not require login or extra personal data for opt-out.
- Do not sell or transfer opted-out emails except for compliance processing.
- Remember that both the sender and the brand can be responsible.

Product requirements:

- Force unsubscribe link.
- Force sender identity.
- Force physical address.
- Maintain global suppression list.
- Log opt-out timestamps.

## GDPR and ePrivacy Baseline

B2B contact data can still be personal data.

Required concepts:

- Lawful basis.
- Legitimate interest assessment where used.
- Consent or soft opt-in where required by local ePrivacy rules.
- Article 14 notice for third-party/public-source data.
- Right to object to direct marketing.
- Data minimization.
- Purpose limitation.
- Accuracy.
- Retention limits.
- DPA with customers when acting as processor.
- Subprocessor transparency.

Default product stance for EU/UK:

- Conservative sending rules.
- Customer must provide lawful basis.
- First-contact template can include source/privacy notice.
- Opt-out/objection stops marketing processing.
- Country-level policy configuration.

## CCPA / CPRA Baseline

For California:

- Provide notice at collection where applicable.
- Support access, deletion, correction, opt-out of sale/share.
- Respect Global Privacy Control where applicable.
- Distinguish service provider, contractor, third party roles.
- Do not treat "publicly available" as unrestricted use.

Product requirements:

- Do Not Sell/Share field.
- Deletion request workflow.
- Correction request workflow.
- Vendor contract registry.
- Suppression and retention logic.

## LinkedIn and Platform Risk

Do not build these:

- LinkedIn auto-login scraping.
- Profile scraping.
- Connection scraping.
- Auto connect/message bots.
- Browser extension scraping.
- Fake accounts.
- CAPTCHA bypass.
- Proxy evasion.

If a customer provides a LinkedIn URL, treat it as a user-provided field. Do not automatically scrape LinkedIn pages unless using an authorized API or partner route.

## Email Deliverability Requirements

Before bulk sending:

- SPF configured.
- DKIM configured.
- DMARC configured.
- From domain alignment.
- Valid reverse DNS if using direct infrastructure.
- One-click unsubscribe.
- Visible unsubscribe.
- Bounce handling.
- Complaint monitoring.
- Rate limiting.
- New domain warm-up.
- Different streams for marketing and transactional email.

Hard rules:

- No "rotate domains to avoid complaints" feature.
- No "infinite mailbox warmup" claim.
- No sending after unsubscribe.
- Pause campaigns with high bounce or complaint rate.

## AI Content Review

AI can draft, classify, and summarize. It should not make unsupervised claims.

Controls:

- Human review for new templates and campaigns.
- Facts must link to evidence.
- No fabricated funding, hiring, awards, customers, tools, or relationships.
- No fake reply chains.
- No false urgency.
- No sensitive-attribute personalization.
- No customer data training unless explicitly contracted.

## Product-Level Compliance Features

Build these in MVP:

- Region tagging.
- Source ledger.
- Lawful basis field.
- Suppression list.
- DNC list.
- Article 14 notice helper.
- One-click unsubscribe.
- Physical address requirement.
- Privacy request workflow.
- DPA and subprocessors page.
- SPF/DKIM/DMARC checker.
- Sender health dashboard.
- AI fact-check / evidence display.
- Audit logs.
- Retention rules.
- Customer acceptable use policy.

## China Outbound Notes

For China teams serving US/EU customers:

- Follow destination-market law: CAN-SPAM, GDPR/ePrivacy, CCPA/CPRA.
- Consider PIPL for personal information collected or processed in China.
- Cross-border access by China-based staff may need contract and access controls.
- Prepare English DPA, subprocessors list, SCC/UK addendum, security whitepaper, and deletion SLA.

