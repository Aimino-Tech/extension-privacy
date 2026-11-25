# Aimino Browser Connect BETA — Privacy Notice

**Effective:** 25 November 2026  
**Applies to:** Chrome extension 0.5.2 (Manifest V3), protocol 2.0. This is a metadata/listing beta candidate based on the BrowserSkill 0.5.0 runtime at upstream commit [feb601ca9be5c3276660b2c28ea6d3c946567d1b](https://github.com/Tencent/BrowserSkill/tree/feb601ca9be5c3276660b2c28ea6d3c946567d1b), plus Aimino's pilot overlay. It is not the planned public ChatGPT connector.

**Publisher:** Aimino Tech GmbH, Germany  
**Contact:** [info@aimino.de](mailto:info@aimino.de) · https://aimino.de/

## 1. Single purpose

The extension connects Chrome to a BrowserSkill daemon or compatible gateway explicitly selected by the user. The selected agent can perform user-directed browser tasks in task-created tabs and in tabs the user explicitly lends or selects for a Quick Action. This includes reading and interacting with the selected pages. The extension is not read-only: an agent can navigate, click, type, interact with forms and change page state within its authorized browser task.

Connection is disabled until the user enables it. The user chooses and pairs the endpoint. Before connection can be enabled, the main popup displays a disclosure card summarizing page access, data sent to the selected daemon, optional debugging/recording and links to this notice and reviewer setup. The user then explicitly enables the connection. Aimino does not operate a required hosted gateway, account service or intermediary for this pilot.

## 2. Information the extension may process

Only information available to the selected browser task and features the user starts is in scope. Depending on the task and page, this may include:

- **Page and website content:** DOM, HTML, accessibility information, visible text, screenshots, page state, URLs, titles, frame/navigation information and tab/window identifiers for task tabs. Tabs borrowed from the user's ordinary browser are subject to the extension's tab-borrow setting and confirmation controls.
- **User and agent activity in the task:** clicks, drags, keystrokes, form values, navigation and page changes needed to carry out and verify the task; bounded manual-activity and shared-control evidence used to coordinate the user and agent.
- **Website debugging evidence, only when explicitly started:** request URLs and methods, headers and bodies when available, response status and timing, errors, console messages, supported page actions, field values and performance context for the selected task tab. Credential redaction is applied to recognized patterns but cannot guarantee that every sensitive value is removed.
- **Task video, only when explicitly started:** rendered frames from the selected task tab, encoded as silent video. It does not request microphone or system audio. Visible personal information and entered text may appear in frames; video is not automatically masked by debugging redaction.
- **Screenshots and files, only when requested:** screenshots and video the user chooses to export; files explicitly supplied to a local `bsk upload` operation; and browser downloads explicitly requested by a local `bsk download` operation. Native file upload/download commands are disabled in remote mode.
- **Local settings and credentials:** a random browser-instance identifier, optional label, feature preferences, optional paired endpoint and device credentials. These are stored in extension-local storage/IndexedDB. Optional debug history and video data use extension-local IndexedDB and browser origin-private storage.
- **Notifications:** system notifications for tab-borrow approval, requests for human assistance and incompatible daemon status.

The extension does not enumerate Chrome's browsing-history database, bookmarks, saved passwords or autofill databases. It does use URLs, titles and navigation/activity evidence for task tabs and may process sensitive information visible in a page the user directs the agent to use. Depending on the selected page, this can include personal identifiers, authentication-related page content, financial or payment information, personal communications, health information or location information.

## 3. How information is used

Information is used to perform the user's browser task, keep agent actions bound to the correct page, coordinate manual and agent control, provide requested debugging/recording features, and return requested results or exports. Website debugging and video recording are separate optional features; opening or controlling a task tab does not by itself start either recording feature.

The selected agent may execute page-level JavaScript expressions through Chrome's documented Debugger / DevTools Protocol API in the authorized page context. This is not a remotely hosted script loaded into the extension's own execution context. It is part of the user-directed browser interaction capability and is subject to Chrome Web Store's specific Debugger API policy requirements. No other remotely hosted extension logic is included in this pilot.

## 4. Recipients and transfers

- **Default local mode:** the extension connects to the BrowserSkill daemon on the same computer over loopback. Task results are returned to that daemon.
- **User-selected remote mode:** after explicit pairing, automation data is sent over authenticated WSS to the remote server or compatible gateway the user chooses. The operator of that server may receive and retain task results, page content, screenshots, tab metadata, debugging evidence or recordings as applicable to the task and enabled features.
- **External AI services:** the extension does not independently call an AI provider. If the user configures the selected daemon or gateway to use an external AI service, the task data sent to that service is handled under that provider's terms and privacy policy.
- **Aimino:** Aimino does not receive browser-task payloads through a mandatory intermediary in this pilot and does not sell task data. There is no Aimino-hosted consumer gateway, account service or analytics endpoint in this build.

Do not connect to an endpoint you do not trust or use the extension on sensitive pages unless you understand who operates that endpoint and how it handles data.

## 5. Storage and retention

Retention depends on the feature and where it runs:

- Browser-instance identifiers, optional labels and preferences persist in extension storage until the user clears extension data or uninstalls the extension. Pairing credentials remain in extension-origin IndexedDB until replaced, cleared or uninstalled.
- Shared-control observations are bounded to the active task and held in memory for coordination. Observation/step JSON files are written to the CLI machine only when an explicit save path is requested; saved files remain until the user deletes them.
- Website-debugging evidence is stored locally in extension-origin IndexedDB. Stopped records expire after 30 days and are subject to limits of 50 records / 50 MiB of serialized data; individual evidence may be omitted or evicted earlier under per-capture limits. Exported copies and data already received by a gateway are not deleted by local expiry.
- Task videos and recovery fragments are stored locally. Recordings expire 24 hours after creation and are subject to per-recording limits of 10 minutes / 256 MiB and a 1 GiB temporary video budget. Users can delete retained recordings. Exported MP4 files and copies received by a gateway remain until deleted by the relevant recipient.
- Operation audit is off by default. When enabled, task/operation metadata is stored on the selected daemon, not the browser. Ended tasks are retained for 30 days and pruned by the daemon's audit maintenance. Audit metadata is distinct from website-debugging evidence.
- Local daemon file-upload staging is removed when the session ends or disconnects; download staging is removed after copying to the requested destination. Files explicitly exported or saved by the user remain on disk until deleted.
- A remote server or external service may retain data it receives under its own terms. Disconnecting, revoking a device or uninstalling the extension does not delete copies already received by that server or files already exported.

The upstream implementation's detailed feature, storage and retention documentation is available in the [pinned BrowserSkill privacy policy](https://github.com/Tencent/BrowserSkill/blob/feb601ca9be5c3276660b2c28ea6d3c946567d1b/apps/extension/PRIVACY.md).

## 6. User controls

Users can disable the connection or disconnect; close the Agent Window to stop agent automation; use manual-control hold/resume; deny tab-borrow requests; turn off optional debugging, video or operation audit; review and delete stopped debugging records and retained videos; revoke a paired device on the selected daemon; clear extension data or uninstall; and separately delete exported files and files retained by a remote operator. Disabling or uninstalling does not erase exported files or remote copies.

## 7. Security and important limitations

Remote connections require explicit pairing and authenticated encrypted WSS, except loopback development. Local pairing is available; unpaired local connections display an identity warning and carry a peer-impersonation risk. Verification failures do not automatically fall back to an unverified connection. Treat a paired daemon as trusted to operate the selected browser profile and signed-in websites.

Debugging redaction covers recognized credentials but does not guarantee that arbitrary page text, bodies, console messages or field values are free of confidential information. Video records rendered pixels and does not automatically mask visible personal data. Review evidence before exporting or sharing it.

## 8. Children, Limited Use and contact

This developer tool is not directed at children under 13.

The use of information received from Chrome APIs will adhere to the Chrome Web Store User Data Policy, including the Limited Use requirements. Information is used only for the disclosed single purpose and related user-requested operational features; it is not sold or used for advertising.

For privacy questions or requests, contact [info@aimino.de](mailto:info@aimino.de). Please do not email page contents, credentials, invoices or other confidential data. This policy applies only to this developer beta; a future hosted or ChatGPT-connected product requires a separately reviewed disclosure.
