# Privacy policy: Approved Response Macros & Compliance Templates for JSM

Updated 10 November 2026

This policy describes the Atlassian Marketplace app **Approved Response Macros & Compliance Templates for JSM** ("the app"), made by EvidencePair LLC ("EvidencePair", "we"). EvidencePair's company privacy policy, which covers our website and email you send us, is at <https://evidencepair.com/privacy/>.

## In short

- The app runs on Atlassian Forge, inside your Jira site. It declares no external egress and no remote services, and it makes requests only to your site's Jira APIs.
- It keeps its data in Jira itself, as Jira project and issue properties, and it posts the replies agents send as ordinary Jira comments. That data is never sent to EvidencePair.
- The personal data it stores itself is the Atlassian account ID of each agent who sends a macro, the account ID of the person who last saved a project's macro library, and, for each send, the issue summary and the first 280 characters of the text posted. That text can include the reporter's display name and anything an agent typed.

## What the app stores

**Project properties, on each project where someone has saved a macro library:**

- `responseGuardPackIndex`, the library's index:
  - the project's key and ID;
  - how many parts ("shards") the library is split into, their keys, the number of macros and their total size;
  - the list of variables macros can use;
  - the Atlassian account ID of the person who last saved the library, and when;
  - a record of the property's own size.

  Libraries saved by versions before 10 November 2026 also hold a service desk ID field, always set to `1`. The app no longer reads or writes it. It disappears the next time someone saves the library.
- `responseGuardPack_1`, `responseGuardPack_2` and so on, which hold the macros. For each macro: its ID, title, category, version, whether it is approved, whether it goes out by default as a public reply or an internal note, its body template and its locked disclaimer, as typed. Each of these properties also repeats the project's key and ID, the account ID of the person who saved it and when, and its own size.

Until someone saves a library, the app stores nothing on the project and offers four built-in example macros. Their text contains no personal data.

**One issue property, `responseGuardAudit`, per issue where someone sent a macro:**

- the issue key and the project ID;
- the 25 most recent sends, newest first. For each send:
  - the ID of the comment it posted;
  - the Atlassian account ID of the agent who sent it, and when;
  - the issue key, the project ID and the issue summary at that time;
  - the macro's ID, title, version and category;
  - whether it went as a public reply or an internal note, and that the disclaimer was present;
  - the first 280 characters of the text posted;
  - a SHA-256 checksum, and the formula used to compute it;
- a copy of the latest send's time, macro, visibility and checksum, and a running count of sends;
- a record of the property's own size.

The checksum is computed from the agent's account ID, the issue key, the macro's ID and version, the visibility and the time. It adds no information of its own.

**Comments.** Each send posts a comment on the issue, as the agent who sent it. The comment holds the macro's body with its variables filled in, or the body as the agent edited it, followed by the macro's locked disclaimer. It carries Jira Service Management's `sd.public.comment` property, which marks it as a public reply or an internal note. These are ordinary Jira comments.

From Jira's user data, the app uses only the issue reporter's display name. It puts that name into a reply wherever a macro uses `{{reporter.displayName}}`, so the name can end up in the comment and in the 280 characters the audit record keeps. The app does not look up email addresses or profiles. Text that people type into macros or replies can contain personal data, and the app stores it exactly as entered.

## What the app reads from Jira

- The issue the panel is opened on: its summary, status, reporter and project (name, key and ID). From the reporter it uses only the display name.
- The project's macro library properties, and the issue's `responseGuardAudit` property.
- On the project page, the 15 most recently updated issues in the project (key, summary, status and reporter) and each one's `responseGuardAudit` property, to build the audit list and its CSV. If that search returns no issues, the list is empty.

The issue panel works only on the issue Jira opened it on, and the project page only on its own project. If Jira does not say which issue or project that is, the app shows a message and reads nothing.

It reads no issue descriptions, existing comments or attachments.

## Where the data lives

Entity properties and comments are part of your Jira site's data. Atlassian stores them with the rest of your site, in your site's data residency location, under Atlassian's own security and privacy commitments. The app has no storage of its own: it uses no Forge storage and no Forge SQL, and EvidencePair runs no servers in its path.

## Who can see it

Jira shows an entity property to anyone who can view the issue or project it belongs to, through Jira's REST API. Anyone who can see an issue can therefore read its audit record, including the agents' account IDs and the first 280 characters of each reply, internal notes included. Anyone who can see a project can read its macro library.

The app's screens show the same data. The issue panel shows the latest send on the issue, with the agent's account ID. The project page shows the audit list and a CSV, with account IDs, for whichever of the project's 15 most recently updated issues the viewer can see.

In a service project, a public reply is visible to the customer in the portal and to anyone who can see the issue. Jira Service Management hides an internal note from customers.

Jira's permissions also decide who can change things. Every request the app makes runs as the person using it. Posting a reply needs permission to comment on the issue, saving the audit record needs permission to edit the issue, and saving the macro library needs permission to administer the project.

## Retention and deletion

The app keeps its properties until someone deletes them. It has no retention setting, deletes nothing on its own schedule, and has no uninstall step. Its screens cannot delete an audit entry or a property. On the project page, someone who can administer the project can remove a macro: the app then saves the library without it.

- Each issue's audit record keeps the 25 most recent sends. When a newer one is added, the oldest entry is dropped.
- Saving a library replaces its properties. If a later save needs fewer shards than before, the extra ones stay on the project, unused.
- Comments stay on the issue until someone deletes them in Jira. Deleting a comment does not remove its entry from the audit record.

Deleting an issue deletes its properties. A Jira administrator can delete any of the app's properties at any time through Jira's REST API, and should do so before uninstalling if the data must go.

## Account closure

The app does not take part in Atlassian's personal data reporting. When an Atlassian account is closed, its account ID stays in the audit record of every issue where that person sent a macro, until that property, or the issue, is deleted. It also stays in a project's library properties if that person was the last to save the library, until someone saves it again or the properties are deleted. A display name that was filled into a reply stays in the comment and in the audit record as plain text. The comments the app posted are ordinary Jira comments, which Jira handles like any other.

## Platform logs

The app writes nothing to the Forge platform's logs. Atlassian's platform can still record errors it sees while the app runs, such as an unhandled error and its message ([Atlassian: view app logs](https://developer.atlassian.com/platform/forge/view-app-logs/)).

When something goes wrong, for example an issue or library the app cannot read, the app shows a message on screen. That message can include an issue key, a property key or a macro ID. It is not written to the logs. If posting a comment or saving a property fails, that error can reach the platform's logs, with the issue key, the property key and, for a comment, Jira's error response.

## Email and support

If you email us, our [company privacy policy](https://evidencepair.com/privacy/) describes how we handle that email, and the current restrictions on where our apps may be used. For help with the app, see <https://evidencepair.com/support/>.

## What we never do

We do not sell personal data or use it for unrelated advertising or AI training. The app's data stays in your Jira site and never reaches us.

## Changes to this policy

The date at the top changes when this policy does. Every version is kept in this repository's history.

## Contact

hello@evidencepair.com
