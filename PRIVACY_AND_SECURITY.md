# Privacy & Security Policy — Approved Response Macros & Compliance Templates for JSM

**Effective Date:** October 15, 2026  
**Vendor:** EvidencePair LLC (`support@titlecovenant.com`)  
**App Key:** `com.evidencepair.jsm.response.guard`  
**App ID:** `ari:cloud:ecosystem::app/2dc4b4e7-5124-47ff-a660-aa35b09ecf19`

---

## 1. 100% Runs on Atlassian Architecture (Zero Data Egress)

**Approved Response Macros & Compliance Templates for JSM** runs exclusively inside the Atlassian Forge managed serverless runtime (`nodejs24.x`).
- **Zero External Remotes**: `manifest.yml` declares zero `remotes:`, zero external API endpoints, and zero third-party analytics trackers.
- **Zero Forge SQL / KVS Databases**: All configuration and audit metadata are stored exclusively inside your Jira Cloud instance's native Entity Properties (`responseGuardPackIndex`, `responseGuardPack_1..N`, and `responseGuardAudit`).
- **In-Memory Processing Only**: Ticket fields (`summary`, `reporter.displayName`, `project.name`) are interpolated in ephemeral Forge execution memory solely to render and dispatch comments via Jira's native REST API (`POST /rest/api/3/issue/{issueKey}/comment`).

---

## 2. Host Storage & 32 KB Sharding Guardrail

| Entity Scope | Property Key | Purpose | Size Guardrail |
| :--- | :--- | :--- | :--- |
| **Jira Project Property** | `responseGuardPackIndex` | Shard manifest index (`shardCount`, `shardKeys`, `totalMacros`) | `<32 KB` (`assertPropertyPayloadUnder32KB`) |
| **Jira Project Property** | `responseGuardPack_1..N` | Sharded approved response macros & locked legal/SLA disclaimers | `<32 KB` per shard |
| **Jira Issue Property** | `responseGuardAudit` | Bounded ring buffer of SHA-256 signed macro dispatch audit records | `<32 KB` per issue |

---

## 3. Least-Privilege Permissions (`manifest.yml`)

- `read:jira-work`: Reads issue summary, reporter display name, project metadata, and entity properties (`responseGuardPackIndex`, `responseGuardPack_1..N`, `responseGuardAudit`).
- `write:jira-work`: Dispatches verified JSM comments (`POST /rest/api/3/issue/{issueKey}/comment`) with `sd.public.comment` visibility properties and records `responseGuardAudit` issue properties.
- `manage:jira-project`: Allows project administrators to persist sharded macro packs (`responseGuardPackIndex` and `responseGuardPack_1..N`) to Jira Project Properties.

---

## 4. Data Retention, Deletion & GDPR Compliance

Because all data resides inside native Jira Project and Issue Entity Properties within the customer's Atlassian Cloud tenant:
- Deleting an issue or project automatically deletes its associated entity properties.
- Uninstalling the app immediately terminates all access. No customer data is ever copied to or retained on EvidencePair LLC infrastructure.

---

## 5. Security Contact & Vulnerability Disclosure

To report a security question or vulnerability, contact EvidencePair LLC at `support@titlecovenant.com`. All reports are acknowledged within 24 hours.
