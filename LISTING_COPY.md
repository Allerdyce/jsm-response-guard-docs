# Atlassian Marketplace Listing Copy — Approved Response Macros & Compliance Templates for JSM

- **App Name:** `Approved Response Macros & Compliance Templates for JSM`
- **App Key:** `com.evidencepair.jsm.response.guard`
- **Tagline / Summary (128 chars):**
  `Enforce approved JSM response macros with live variable interpolation, locked legal/SLA disclaimers, and SHA-256 dispatch audit.`
- **Categories:** IT & Helpdesk, Compliance & Security, Workflow, Customer Support

---

## Highlight 1: Live Variable Interpolation & JSM Public/Internal Dispatch
- **Title:** `Live Variable Interpolation & JSM Public/Internal Dispatch`
- **Body:** `Preview dynamic JSM ticket tokens ({{issue.key}}, {{issue.summary}}, {{reporter.displayName}}, {{project.name}}) and dispatch 1-click Public Customer Replies or Internal Agent Notes via sd.public.comment.`

## Highlight 2: Sharded Macro Packs & Locked Legal/SLA Disclaimers
- **Title:** `Sharded Macro Packs & Locked Legal/SLA Disclaimers`
- **Body:** `Enforce immutable legal, HIPAA, and SLA disclaimer footers that agents cannot strip, sharded across native Jira Project Properties (responseGuardPackIndex + responseGuardPack_1..N) under 32 KB.`

## Highlight 3: Cryptographic SHA-256 Dispatch Audit & 1-Click CSV Export
- **Title:** `Cryptographic SHA-256 Dispatch Audit & 1-Click CSV Export`
- **Body:** `Record a deterministic SHA-256 signature for every dispatched macro in Jira Issue Property responseGuardAudit and export space-wide QA & compliance audit ledgers as RFC-4180 CSV.`

---

## Full Marketplace Description

**Eliminate unapproved customer promises, missing legal disclaimers, and unverified agent replies in Jira Service Management.**

**Approved Response Macros & Compliance Templates for JSM** equips service desk teams with regulator-ready response templates, immutable compliance disclaimers, and cryptographic dispatch auditing:

- **1-Click JSM Public Reply vs. Internal Agent Note Routing (`jsm-response-guard-panel`)**: Interpolates `{{issue.key}}`, `{{issue.summary}}`, `{{reporter.displayName}}`, and `{{project.name}}` in real time and dispatches Atlassian Document Format (`ADF`) comments with `sd.public.comment` visibility control.
- **Sharded Macro Library & Locked Disclaimer Engine (`jsm-response-guard-admin`)**: Space admins approve versioned macros with mandatory legal/SLA footers stored across sharded Jira Project Properties (`responseGuardPackIndex` and `responseGuardPack_1..N`, `<32 KB` per shard).
- **Deterministic SHA-256 Dispatch Audit & CSV Export**: Computes a verifiable SHA-256 signature (`accountId|issueKey|macroId|macroVersion|visibility|timestamp`) stored in `responseGuardAudit` (`<32 KB`) with 1-click space-wide CSV export.
- **100% Runs on Atlassian (Zero Data Egress)**: Built on Forge `nodejs24.x` with zero external servers and zero Forge SQL/KVS.
