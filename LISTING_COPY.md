# Atlassian Marketplace Listing Copy — Approved Response Macros & Compliance Templates for JSM

Updated 10 November 2026

- **App Name:** `Approved Response Macros & Compliance Templates for JSM`
- **App Key:** `com.evidencepair.jsm.response.guard`
- **Tagline / Summary (128 chars):**
  `Send approved JSM response macros with live variables, a locked footer on every reply, and a SHA-256 record of each send.`
- **Categories:** IT & Helpdesk, Compliance & Security, Workflow, Customer Support

---

## Highlight 1: Live Variable Interpolation & JSM Public/Internal Dispatch
- **Title:** `Live Variable Interpolation & JSM Public/Internal Dispatch`
- **Body:** `Preview dynamic JSM ticket tokens ({{issue.key}}, {{issue.summary}}, {{reporter.displayName}}, {{project.name}}) and dispatch 1-click Public Customer Replies or Internal Agent Notes via sd.public.comment.`

## Highlight 2: Sharded Macro Packs & Locked Footers
- **Title:** `Sharded Macro Packs & Locked Footers`
- **Body:** `Each macro has a footer the app adds when it posts the reply. Agents can edit the reply in the panel, not the footer. Libraries live in Jira project properties, under 32 KB each.`

## Highlight 3: Cryptographic SHA-256 Dispatch Audit & 1-Click CSV Export
- **Title:** `Cryptographic SHA-256 Dispatch Audit & 1-Click CSV Export`
- **Body:** `Record a deterministic SHA-256 checksum for every dispatched macro in Jira Issue Property responseGuardAudit and export the project's record of sends as RFC-4180 CSV.`

---

## Full Marketplace Description

**Give Jira Service Management agents approved replies, each with a footer your project admins set.**

**Approved Response Macros & Compliance Templates for JSM** equips service desk teams with approved response templates, a locked footer on every reply sent through the app, and a checksum record of each send:

- **1-Click JSM Public Reply vs. Internal Agent Note Routing (`jsm-response-guard-panel`)**: Interpolates `{{issue.key}}`, `{{issue.summary}}`, `{{reporter.displayName}}`, and `{{project.name}}` in real time and dispatches Atlassian Document Format (`ADF`) comments with `sd.public.comment` visibility control.
- **Sharded Macro Library & Locked Footers (`jsm-response-guard-admin`)**: Project admins add and remove macros, each with a footer, stored across sharded Jira Project Properties (`responseGuardPackIndex` and `responseGuardPack_1..N`, `<32 KB` per shard). The app adds the footer when it posts a reply; agents can edit the reply's text in the panel, but not its footer. Once posted, a reply is an ordinary Jira comment. New projects start with four neutral example macros to replace.
- **Deterministic SHA-256 Dispatch Audit & CSV Export**: Computes a SHA-256 checksum (`accountId|issueKey|macroId|macroVersion|visibility|timestamp`) stored in `responseGuardAudit` (`<32 KB`) with 1-click CSV export of the project's sends.
- **100% Runs on Atlassian (Zero Data Egress)**: Built on Forge `nodejs24.x` with zero external servers and zero Forge SQL/KVS.
