# Approved Response Macros & Compliance Templates for JSM (`com.evidencepair.jsm.response.guard`)

Updated 10 November 2026

**Approved Response Macros & Compliance Templates for JSM** gives Jira Service Management (JSM) and Jira Cloud agents approved reply templates, with variables filled in from the issue, a locked footer the app adds to every reply it sends, and a SHA-256 checksum record of each send.

- **App ID**: `ari:cloud:ecosystem::app/2dc4b4e7-5124-47ff-a660-aa35b09ecf19`
- **App Key**: `com.evidencepair.jsm.response.guard`
- **Vendor**: EvidencePair LLC (support: <https://evidencepair.com/support/>)
- **Runtime**: Forge `nodejs24.x` (100% *Runs on Atlassian*, Zero External Egress, Zero Forge SQL/KVS)
- **Host Storage**: Sharded Jira Project Properties (`responseGuardPackIndex` + `responseGuardPack_1..N`, `<32 KB` per shard) and Jira Issue Properties (`responseGuardAudit`, `<32 KB`)

---

## Key Capabilities

1. **Sharded Response Macro Library & Locked Disclaimer Engine (`jira:projectPage` — `jsm-response-guard-admin`)**:
   - Project administrators add and remove response macros containing dynamic issue tokens (`{{issue.key}}`, `{{issue.summary}}`, `{{reporter.displayName}}`, `{{project.name}}`) and a **locked footer**. The app adds the footer when it posts a reply; agents can edit the reply's text in the issue panel, but not its footer. Once posted, a reply is an ordinary Jira comment.
   - Until a project saves its own library, it shows four example macros with neutral wording, to be replaced. Libraries saved before 10 November 2026 keep the wording they were saved with.
   - Automatically shards macro libraries across Jira Project Properties (`responseGuardPackIndex` and `responseGuardPack_1..N`), enforcing `<32 KB` (`32,768` bytes UTF-8) per property via `assertPropertyPayloadUnder32KB`.
2. **Live Variable Interpolation & JSM Public/Internal Comment Dispatch (`jira:issuePanel` — `jsm-response-guard-panel`)**:
   - Service desk agents select an approved macro on the issue they are viewing, preview live interpolated variables and the locked footer, and dispatch with 1 click as either a **Public Customer Reply** (`sd.public.comment.internal = false`) or an **Internal Agent Note** (`sd.public.comment.internal = true`) via `POST /rest/api/3/issue/{issueKey}/comment`.
   - Every dispatch generates a deterministic SHA-256 checksum (`accountId|issueKey|macroId|macroVersion|visibility|timestamp`) persisted in Jira Issue Property `responseGuardAudit`.
   - The panel works only on the issue it is opened on. If that issue, its project's library or the chosen macro cannot be read, it shows a message and posts nothing.
3. **Macro Usage Analytics & 1-Click Signed Audit CSV Export**:
   - Tracks which approved macro version was sent on which ticket, recomputes each SHA-256 checksum (`SHA256_DISPATCH_VERIFIED`), and exports an RFC-4180 CSV report.

---

## Documentation Index

- [User Guide](./USER_GUIDE.md)
- [Privacy Policy](./PRIVACY_POLICY.md)
- [Security Documentation](./SECURITY.md)
- [Privacy & Security Architecture Summary](./PRIVACY_AND_SECURITY.md)
- [End-User License Agreement (EULA)](./EULA.md)
- [Marketplace Listing Copy](./LISTING_COPY.md)
- [Progressive Cloud Pricing Table](./PRICING_TABLE.md)
