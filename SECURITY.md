# Security: Approved Response Macros & Compliance Templates for JSM

Updated 9 November 2026

How the Atlassian Marketplace app **Approved Response Macros & Compliance Templates for JSM**, made by EvidencePair LLC, handles data, what protects it, how we handle vulnerabilities, and which certifications apply. What the app stores is listed in full in its [privacy policy](./PRIVACY_POLICY.md).

## Data handling

- **Forge only.** The app runs on Atlassian Forge (`nodejs24.x`) on Atlassian infrastructure.
- **No egress.** The manifest declares no external permissions and no remote services. The app makes requests only to your site's Jira APIs, and it loads no analytics, error-reporting services or external assets.
- **No storage of its own.** The app keeps its data in Jira entity properties on your site: `responseGuardPackIndex` and `responseGuardPack_1`, `responseGuardPack_2` and so on, on a project, for the macro library, and `responseGuardAudit` on an issue, for the record of sends. The replies it sends are ordinary Jira comments. It uses no Forge storage or Forge SQL, and EvidencePair has no copy.
- **Requests run as the user.** Every Jira request the app makes runs as the person using its screens, so Jira applies that person's own permissions. The app never calls Jira as itself, and it has no scheduled jobs, event triggers or workflow modules.
- **Permissions it asks for.**
  - `read:jira-work`: read the issue, search the project's 15 most recently updated issues, and read the macro library and audit properties.
  - `write:jira-work`: post a reply or internal note as a comment, and save the audit record to its issue.
  - `manage:jira-project`: save the project's macro library.
- **The locked disclaimer.** The app's Forge function adds each macro's disclaimer from the project's library when it posts the reply. The issue panel lets an agent edit a reply's body but not its disclaimer. Once posted, the reply is an ordinary Jira comment, and Jira's permissions decide who can edit or delete it.
- **What the checksum is.** Each audit entry carries a SHA-256 checksum of the agent's account ID, the issue key, the macro's ID and version, the visibility and the time. It does not cover the issue summary or the text posted. The app's screens call it a signature. It is not a digital signature: it uses no key, so someone with permission to edit the issue property could change an entry and recompute the checksum.
- **Order of writes.** The app posts the comment first and saves the audit entry after it. If saving the entry fails, the comment stays on the issue without one.

## Encryption

The app stores nothing outside your Jira site and sends nothing outside Atlassian's platform. Encryption in transit and at rest is provided by Atlassian as part of your site, as described in the [Atlassian Trust Center](https://www.atlassian.com/trust). The app adds no encryption of its own.

## Vulnerability management

- **Reporting.** Email security@evidencepair.com. Tell us the app, what you found and how to reproduce it. Please do not test against sites you do not own. We acknowledge every report within one business day.
- **Response.** EvidencePair adopted a written security incident response plan on 12 October 2026. It covers triage, containment, investigation, notification of Atlassian and affected customers, and recovery.
- **Dependencies.** The app's npm dependencies are pinned in its lockfile. Atlassian maintains and patches the Forge runtime.
- **Bug bounty.** We do not run a bug bounty programme.

## Certifications

EvidencePair holds no security certifications, and the app has had no independent penetration test or external audit. The infrastructure the app runs on is Atlassian's, and Atlassian's own certifications cover it: see the [Atlassian Trust Center](https://www.atlassian.com/trust).
