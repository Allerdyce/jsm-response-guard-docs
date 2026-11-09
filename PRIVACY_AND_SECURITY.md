# Privacy & Security Architecture — Approved Response Macros & Compliance Templates for JSM

> The app's privacy policy is [PRIVACY_POLICY.md](./PRIVACY_POLICY.md), and its security documentation (data handling, encryption, vulnerability management and certifications) is [SECURITY.md](./SECURITY.md). This page is the architecture summary.

**Updated:** 9 November 2026  
**Vendor:** EvidencePair LLC (support: <https://evidencepair.com/support/>)  
**Security Contact:** `security@evidencepair.com`  
**App Key:** `com.evidencepair.jsm.response.guard`  
**App ID:** `ari:cloud:ecosystem::app/2dc4b4e7-5124-47ff-a660-aa35b09ecf19`

---

## 1. 100% Runs on Atlassian Architecture (Zero Data Egress)

**Approved Response Macros & Compliance Templates for JSM** runs exclusively inside the Atlassian Forge managed serverless runtime (`nodejs24.x`).
- **Zero External Remotes**: `manifest.yml` declares zero `remotes:`, zero external API endpoints, and zero third-party analytics trackers.
- **Zero Forge SQL / KVS Databases**: All configuration and audit metadata are stored exclusively inside your Jira Cloud instance's native Entity Properties (`responseGuardPackIndex`, `responseGuardPack_1..N`, and `responseGuardAudit`).
- **Ticket Fields**: The issue summary, the reporter's display name and the project name are read to fill in macro variables, and the result is posted through Jira's native REST API (`POST /rest/api/3/issue/{issueKey}/comment`). Each dispatch's audit entry in `responseGuardAudit` also keeps the issue summary and the first 280 characters of the posted text, which can include the reporter's display name. See the [privacy policy](./PRIVACY_POLICY.md).

---

## 2. Host Storage & 32 KB Sharding Guardrail

| Entity Scope | Property Key | Purpose | Size Guardrail |
| :--- | :--- | :--- | :--- |
| **Jira Project Property** | `responseGuardPackIndex` | Shard manifest index (`shardCount`, `shardKeys`, `totalMacros`) | `<32 KB` (`assertPropertyPayloadUnder32KB`) |
| **Jira Project Property** | `responseGuardPack_1..N` | Sharded approved response macros & locked legal/SLA disclaimers | `<32 KB` per shard |
| **Jira Issue Property** | `responseGuardAudit` | Ring buffer of the 25 most recent macro dispatch audit records, each with a SHA-256 checksum | `<32 KB` per issue |

---

## 3. Least-Privilege Permissions (`manifest.yml`)

- `read:jira-work`: Reads issue summary, reporter display name, project metadata, the project's 15 most recently updated issues, and entity properties (`responseGuardPackIndex`, `responseGuardPack_1..N`, `responseGuardAudit`).
- `write:jira-work`: Dispatches verified JSM comments (`POST /rest/api/3/issue/{issueKey}/comment`) with `sd.public.comment` visibility properties and records `responseGuardAudit` issue properties.
- `manage:jira-project`: Allows project administrators to persist sharded macro packs (`responseGuardPackIndex` and `responseGuardPack_1..N`) to Jira Project Properties.

---

## 4. Data Retention & Deletion

Because all data resides inside native Jira Project and Issue Entity Properties within the customer's Atlassian Cloud tenant:
- Deleting an issue or project automatically deletes its associated entity properties.
- Uninstalling the app ends its access. It does not delete the app's properties or the comments it posted; a Jira administrator can delete the properties through Jira's REST API. No customer data is ever copied to or retained on EvidencePair LLC infrastructure.

---

## 5. Security Contact & Vulnerability Disclosure

To report a security issue, email `security@evidencepair.com`. We acknowledge every report within one business day. EvidencePair holds no security certifications; see [SECURITY.md](./SECURITY.md). For help with the app, see <https://evidencepair.com/support/>.
