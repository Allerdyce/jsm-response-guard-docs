# User Guide — Approved Response Macros & Compliance Templates for JSM

Updated 10 November 2026

## 1. Getting started

1. Install **Approved Response Macros & Compliance Templates for JSM** (`com.evidencepair.jsm.response.guard`) from the Atlassian Marketplace on your Jira Service Management or Jira Cloud site.
2. Open a project and choose **Approved Response Macros & Compliance Templates for JSM** in the project's navigation. This is the project page (`jsm-response-guard-admin`), where the project's macros are managed.
3. Open any request or issue in that project and open the **Approved Response Macros & Compliance Templates for JSM** panel (`jsm-response-guard-panel`). Agents choose a macro there, check the preview and send it.

The panel always works on the issue it is opened on, and the project page on its own project. If Jira does not tell the app which issue or project that is, the app shows a message and does nothing.

---

## 2. Managing a project's macros (project page)

Anyone who can see the project can open the project page. Saving needs permission to administer the project.

- **Example macros.** Until you save a library, the project shows four example macros. They are plain examples with no compliance or legal wording. Replace them with your own: add your macros, then remove the examples you do not want.
- **Adding a macro.** Type a title and the reply text, and optionally a footer, then click **Approve & Add Macro Template**. The app saves the library straight away. If you leave the footer empty, the app uses "Sent by the {{project.name}} team."
- **Removing a macro.** Click **Remove** next to it. The app saves the library without it. The last macro cannot be removed.
- **Changing a macro.** Remove it and add it again with the new wording.
- **Variables.** Reply text and footers can use `{{issue.key}}`, `{{issue.summary}}`, `{{reporter.displayName}}` and `{{project.name}}`. They are filled in from the issue when the reply is sent. If an issue has no reporter, `{{reporter.displayName}}` becomes "Customer".
- **Locked footers.** Each macro has a footer. The app adds it below the reply when it posts it. Agents can edit a reply's text in the panel, but not its footer.
- **Saving the examples as they are.** **Sync & Shard Macro Library to Project Properties (<32 KB)** saves the list shown, including the examples.
- **Storage.** The library is saved in Jira project properties: `responseGuardPackIndex` and `responseGuardPack_1`, `responseGuardPack_2` and so on, each under Jira's 32 KB limit.

**Libraries saved before 10 November 2026** keep the wording they were saved with. Earlier versions offered different example macros, some with compliance and retention wording. The app does not change a saved library. If your project saved those examples, remove them on the project page and add your own wording.

---

## 3. Sending a reply (issue panel)

1. Open a request or issue and open **Approved Response Macros & Compliance Templates for JSM**.
2. Choose a macro from the table.
3. Check the preview. It shows the reply with the variables filled in, followed by the locked footer.
4. Optionally edit the reply text. The footer cannot be changed here.
5. Click either:
   - **Dispatch as Public Customer Reply** to post a reply the customer can see in the portal, or
   - **Dispatch as Internal Agent Note** to post an internal note. In a service project, Jira Service Management hides internal notes from customers. In other projects there is no such difference.

The app posts the comment as you, so Jira applies your permissions. It then saves a record of the send in the issue property `responseGuardAudit`, with a SHA-256 checksum of `accountId|issueKey|macroId|macroVersion|visibility|timestamp`.

The app posts nothing, and says why, when:

- the issue or the project's macro library cannot be read;
- the issue's record of sends cannot be read;
- the chosen macro is no longer an approved macro in the library (reload the panel and choose again).

The locked footer is only added to replies sent through the panel. Anyone can still post an ordinary Jira comment without the app, and a posted reply is an ordinary Jira comment that anyone Jira allows can edit or delete.

---

## 4. Exporting the record of sends

On the project page, the list of sends shows the sends recorded on the project's 15 most recently updated issues that you can see. Click **Generate & View CSV Export** to show it as CSV, with issue keys, macro IDs and versions, public or internal, agent account IDs, times, comment IDs and checksums.

---

## 5. Support and contact

- **Vendor**: EvidencePair LLC
- **Support**: <https://evidencepair.com/support/> (`support@evidencepair.com`)
- **Security reports**: `security@evidencepair.com`
- **Response time**: We reply within one business day.
