# User Guide — Approved Response Macros & Compliance Templates for JSM

## 1. Quick Start & Installation

1. Install **Approved Response Macros & Compliance Templates for JSM** (`com.evidencepair.jsm.response.guard`) from the Atlassian Marketplace onto your Jira Service Management or Jira Cloud site.
2. Navigate to **Project Settings → Apps → Response Macro Library & Compliance Audit** (`jsm-response-guard-admin`) to review, customize, or add approved response macros and locked legal/SLA disclaimer blocks.
3. Open any JSM request or Jira issue (e.g., `ITH-1`) and click the **Approved Response Macros & Compliance Dispatch** panel (`jsm-response-guard-panel`) to preview interpolated variables and dispatch verified customer replies or internal agent notes.

---

## 2. Managing Sharded Macro Libraries & Locked Disclaimers (`jira:projectPage`)

In **Response Macro Library & Compliance Audit**, project administrators manage space-wide response templates:
- **Dynamic Variable Tokens**: Use `{{issue.key}}`, `{{issue.summary}}`, `{{reporter.displayName}}`, and `{{project.name}}` in both response bodies and locked disclaimer footers.
- **Locked Mandatory Legal/SLA Disclaimers**: Every approved macro includes an immutable compliance footer (`lockedDisclaimer`) that is automatically appended as a bold rule-separated block in the dispatched Atlassian Document Format (`ADF`) comment.
- **Zero-Cost Sharded Project Property Storage (`<32 KB`)**: Clicking **Sync & Shard Macro Library to Project Properties (<32 KB)** packs macros across `responseGuardPackIndex` and `responseGuardPack_1..N` (`/rest/api/3/project/{projectId}/properties/responseGuardPack_1`), ensuring every property stays strictly below Jira's `32,768`-byte limit.

---

## 3. Dispatching Verified JSM Responses (`jira:issuePanel`)

1. Open a JSM request (e.g., `ITH-1`) and open **Approved Response Macros & Compliance Dispatch**.
2. Select an approved macro from the table (such as *SLA Tier-1 Acknowledgment & Hardware Intake* `v1.2.0` or *Security Incident Containment & Evidence Hold* `v2.0.0`).
3. Review the **Live Variable Interpolation Preview** and verify the **Mandatory Legal / SLA Disclaimer Block [IMMUTABLE LOCK ACTIVE]**.
4. Click either:
   - **Dispatch as Public Customer Reply (`sd.public.comment: internal=false`)** — posts a customer-visible reply to the JSM portal and issue thread, or
   - **Dispatch as Internal Agent Note (`sd.public.comment: internal=true`)** — posts an internal note visible only to JSM agents.
5. The app dispatches the comment as your authenticated user (`api.asUser().requestJira(...)`), computes a deterministic SHA-256 signature over `accountId|issueKey|macroId|macroVersion|visibility|timestamp`, and records the signed audit entry in Jira Issue Property `responseGuardAudit` (`<32 KB`).

---

## 4. Exporting the Compliance Audit CSV Report

In **Response Macro Library & Compliance Audit**, inspect the **Macro Usage Analytics & Cryptographic Dispatch Audit Ledger** and click **Generate & View CSV Export** to copy the RFC-4180 CSV containing issue keys, macro IDs, semantic versions, `sd.public.comment` visibility flags, locked disclaimer verification states, agent Account IDs, UTC timestamps, comment IDs, and 64-character SHA-256 signatures.

---

## 5. Support & Contact

- **Vendor**: EvidencePair LLC
- **Support & Security Email**: `support@titlecovenant.com`
- **Response SLA**: Within 1 business day (24 hours).
