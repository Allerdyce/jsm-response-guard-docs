# Approved Response Macros & Compliance Templates for JSM (`com.evidencepair.jsm.response.guard`)

**Approved Response Macros & Compliance Templates for JSM** enforces standardized, regulator-ready agent communications across Jira Service Management (JSM) and Jira Cloud projects with dynamic variable interpolation, immutable legal/SLA disclaimer footers, and cryptographic SHA-256 dispatch audit trails.

- **App ID**: `ari:cloud:ecosystem::app/2dc4b4e7-5124-47ff-a660-aa35b09ecf19`
- **App Key**: `com.evidencepair.jsm.response.guard`
- **Vendor**: EvidencePair LLC (`support@titlecovenant.com`)
- **Runtime**: Forge `nodejs24.x` (100% *Runs on Atlassian*, Zero External Egress, Zero Forge SQL/KVS)
- **Host Storage**: Sharded Jira Project Properties (`responseGuardPackIndex` + `responseGuardPack_1..N`, `<32 KB` per shard) and Jira Issue Properties (`responseGuardAudit`, `<32 KB`)

---

## Key Capabilities

1. **Sharded Response Macro Library & Locked Disclaimer Engine (`jira:projectPage` — `jsm-response-guard-admin`)**:
   - Space administrators create and approve standardized response macros containing dynamic issue tokens (`{{issue.key}}`, `{{issue.summary}}`, `{{reporter.displayName}}`, `{{project.name}}`) and **Locked Mandatory Legal/SLA Disclaimer** blocks that agents cannot remove or alter.
   - Automatically shards macro libraries across Jira Project Properties (`responseGuardPackIndex` and `responseGuardPack_1..N`), enforcing `<32 KB` (`32,768` bytes UTF-8) per property via `assertPropertyPayloadUnder32KB`.
2. **Live Variable Interpolation & JSM Public/Internal Comment Dispatch (`jira:issuePanel` — `jsm-response-guard-panel`)**:
   - Service desk agents select an approved macro directly on JSM tickets, preview live interpolated variables and the locked compliance footer, and dispatch with 1 click as either a **Public Customer Reply** (`sd.public.comment.internal = false`) or an **Internal Agent Note** (`sd.public.comment.internal = true`) via `POST /rest/api/3/issue/{issueKey}/comment`.
   - Every dispatch generates a deterministic SHA-256 signature (`accountId|issueKey|macroId|macroVersion|visibility|timestamp`) persisted in Jira Issue Property `responseGuardAudit`.
3. **Macro Usage Analytics & 1-Click Signed Audit CSV Export**:
   - Tracks which approved macro version was sent on which ticket, verifies SHA-256 signature integrity (`SHA256_DISPATCH_VERIFIED`), and exports an RFC-4180 compliance CSV report.

---

## Documentation Index

- [User Guide](./USER_GUIDE.md)
- [Privacy & Security Policy](./PRIVACY_AND_SECURITY.md)
- [End-User License Agreement (EULA)](./EULA.md)
- [Marketplace Listing Copy](./LISTING_COPY.md)
- [Progressive Cloud Pricing Table](./PRICING_TABLE.md)
