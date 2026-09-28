# Final directive.md

## Objective

Design and demonstrate a focused first-run experience for an invited teammate in a fictional team-notes product. Let the teammate understand their access, complete a permitted first action and see a useful summary, with an understandable import failure and recovery path. All functionality in the linked prototype is **demo behavior only**.

## Scope

### Target user

An invited, non-admin teammate entering an existing workspace for the first time.

### Baseline

The supplied scenario describes invite-only access, unclear permissions, two confusing live-version labels, an unclear free-plan limit, a blank first screen and no recovery after failed import. There is no production baseline, user research or telemetry. Treat every outcome and estimate as unverified until tested with actual users and product data.

### Included

- A single, explicitly named release label: **First Value Preview 0.1.0 (demo)**.
- Welcome/empty state with a clear first action.
- Visible role and permission boundary.
- Create a note and generate a sample summary.
- Simulated import failure with retry and a manual-entry fallback.
- A concise permission matrix, acceptance criteria, event specification, support route, release notes and conditional go/no-go decision.

### Excluded

Real accounts and invitations; server-side permissions; stored data; real file parsing; real AI; billing/plan logic; production release; definitive version naming across an existing product; claims of measured impact.

## Requirements and acceptance criteria

1. On initial load, show workspace name, release label, user role, empty-state explanation and one primary next action.
2. The role shown is “Teammate.” The interface explains that the teammate can create notes and summaries but cannot invite members or change workspace settings.
3. “Create a note” opens an editable note form. A non-empty note can be saved and appears in the workspace list.
4. “Generate summary” is available after a note is saved and displays a clearly labeled sample summary derived from the entered text. Do not imply real AI processing.
5. “Import notes” can show a deterministic simulated failure. It explains the failure, offers retry and a manual-entry fallback, and preserves any existing note.
6. No control implies an unauthorized operation succeeds. Admin-only actions are visibly disabled or explained.
7. The layout supports keyboard navigation, visible focus, semantic buttons and readable status/error text.
8. Each journey step can be completed without an administrator. Support contact guidance is visible for access problems that the user cannot resolve.
9. Events in the specification below have explicit eligibility denominators. Any prototype event stream is simulated and must not be presented as measured usage.
10. A release recommendation must remain conditional until real access enforcement, usability, instrumentation and operational rollback are verified.

## Permission matrix

| Capability | Teammate (target role) | Workspace admin |
|---|---|---|
| View workspace and notes | Allowed | Allowed |
| Create/edit own note | Allowed | Allowed |
| Generate sample summary | Allowed in demo | Allowed in demo |
| Invite members | Not allowed | Allowed |
| Change workspace settings or plan | Not allowed | Allowed |
| Retry own failed import / use manual entry | Allowed in demo | Allowed in demo |

The prototype illustrates this matrix only. It does not enforce authorization. A production system must enforce every boundary server-side and test direct API access as well as UI state.

## Activation and measurement plan

**Proposed activation event:** `first_summary_created` — an eligible invited teammate saves their first non-empty note and completes a summary successfully.

**Time to first value:** elapsed time from `invite_accepted` to the first `first_summary_created` for the same user/workspace. Report median and p75 among users who activate, alongside the activation rate so non-activators are not hidden.

| Funnel event | Denominator / eligibility |
|---|---|
| `invite_accepted` | Accepted valid invitees in the measurement cohort; funnel entry |
| `workspace_first_viewed` | Users who accepted an invite |
| `first_note_saved` | Users who viewed the workspace; first non-empty note only |
| `first_summary_created` | Users who saved a first note; first successful summary only |
| `import_failed` | Users who attempted an import; record failure category, no file contents |
| `import_retried` | Users with a failed import who retry |
| `manual_entry_selected` | Users with a failed import who choose manual entry |
| `support_opened` | Users who encounter an access/import issue; define eligible event at issue display |

Deduplicate by user/workspace and define a fixed cohort window before launch. Do not capture note text, filenames, invite tokens or other sensitive content. The HTML demo has no analytics transport; the event names are a proposed specification, not observed events.

## Release and operations

### Release notes — First Value Preview 0.1.0 (demo)

- Added a first-run empty state and clear create-note action.
- Made teammate capabilities and admin-only boundaries visible.
- Added a simulated summary and import failure recovery with retry/manual entry.
- No real accounts, data storage, imports, analytics, or AI are connected.

### Support path

For access or permission problems, direct the user to their workspace administrator. For a failed import, offer retry or manual entry; if both fail, show the product support contact route. A real release owner must replace the demo placeholder with a monitored support destination, owner and response expectation before launch.

### Go/no-go memo

**Current decision: NO-GO for production; GO for reviewer evaluation of this local prototype.** The user journey is demonstrable, but the demo cannot establish secure access enforcement, real import recovery, actual first-value improvement, accessible behavior across supported browsers, reliable analytics, a staffed support queue or a working kill switch. A production go decision requires all of the following: server-side permission tests pass; representative invitees complete the journey without admin help; import recovery preserves data; privacy-reviewed events validate against real funnel denominators; support owner/on-call route is confirmed; rollback/disable control is exercised; and product/release owners approve the measured launch criteria.

### Monitoring and rollback

For a real staged release, monitor invite-to-view, view-to-note, note-to-summary, time-to-first-value, import failure/retry/fallback, support contact rate and permission-denied errors. Compare with a predeclared baseline and guardrails; no numeric thresholds can be set from this brief. Pause rollout if unauthorized access is possible, data is lost, events are materially miscounted, or error/support rates exceed thresholds agreed by the release owner. Disable the first-run experience via a server-controlled feature flag, preserve existing notes, route users to the previous workspace entry point, and investigate before re-enabling. The prototype itself has no deployment or rollback mechanism.

## Completion criteria

- A reviewer can open the linked prototype and follow the teammate journey from empty state to summary.
- The permission boundary and simulated import failure/recovery are visible.
- The linked intent rationale, acceptance criteria, permission matrix, event/funnel specification, release notes and go/no-go memo are present.
- At least five acceptance scenarios have actual recorded results, explicitly identified as prototype checks rather than production tests.
- AI assistance and human corrections/limitations are disclosed below.

## Results and handoff appendix

### Artifacts

- [Problem rationale and prioritization](intent.md)
- [Interactive prototype](prototype.html)
- This file: PRD, matrix, measurement, release and handoff

These are local files in the supplied output folder. For external reviewers, upload the entire folder to an accessible shared location and replace these relative links with verified share links. No public or shared URL was supplied, so reviewer access outside this environment is not claimed. No Loom video was supplied or generated; the brief requests it as the third required submission, so the package is incomplete until the candidate records and links a video of five minutes or less.

### Viewing and reproduction

Open `prototype.html` in a modern browser. Select **Create a note**, enter text and save; then select **Generate summary**. Select **Import notes** to inspect the deterministic simulated error; retry or choose manual entry. Use the role badge and disabled admin controls to inspect the boundary. No server, credentials, network access or installation is needed.

### Acceptance scenarios and actual results

The browser preview could not be opened in this environment because its security policy blocks `file:` URLs. Results below are source-inspection checks of the HTML/JavaScript, not executed browser interactions, moderated usability tests or production integration tests. Verify the click flows in a browser after downloading/opening the file in an allowed local workflow.

| # | Scenario | Expected | Actual result |
|---:|---|---|---|
| 1 | First visit | Empty state, release label and role shown | PASS by source inspection — present in initial markup |
| 2 | Create and save note | Non-empty note appears in list | PASS by source inspection — save handler adds note to list |
| 3 | Summary before note | No summary action until a note exists | PASS by source inspection — summary action starts hidden and is revealed on save |
| 4 | Generate summary | Labeled sample summary appears | PASS by source inspection — deterministic local demo text, no AI call |
| 5 | Import fails | Error, retry and manual fallback are available | PASS by source inspection — deterministic failure branch exposes all recovery actions |
| 6 | Teammate attempts admin actions | Invite/settings are unavailable and explained | PASS by source inspection — controls disabled and role boundary stated |
| 7 | Existing note during failed import | Existing note remains visible | PASS by source inspection — failure handler does not modify note list |

### AI contribution, corrections and limitations

AI assistance was used to draft and organize the rationale, requirements, event taxonomy and prototype copy/code. The candidate-selected priority, scope, weighting, assumptions and no-go decision are editorial judgments. The final output corrects for common AI overclaim risks by labeling the scenario as fictional, the scores as judgment calls, summaries/imports/analytics as simulated, and the production decision as conditional. No interviews, benchmark research, telemetry, real tests, approvals or business outcomes are claimed.

Limitations: local prototype only; no persistence/authentication/authorization enforcement; no assistive-technology audit or cross-browser testing; no real data import or summary service; no analytics collection; no external links, Loom, reviewer-accessible hosted URL, owner assignment or agreed operational thresholds. Those items remain prerequisites for a production release.

