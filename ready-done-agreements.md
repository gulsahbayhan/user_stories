# Ready and Done Agreements: Policy Assistant Pilot

> **Status:** Draft for team agreement. Following
> `04-ready-done-and-delivery-quality.md`, these are kept minimal and should be
> reviewed at the end of each pilot week.

## Definition of Ready (DoR)

A story can move from `Backlog` to `Ready` when:

| # | Criterion | Now / Soon |
|---|---|---|
| R-1 | Role, goal, and benefit are clear and specific. "User" on its own isn't enough. | Now |
| R-2 | Acceptance criteria are written and testable, with no AC relying on vague judgment. | Now |
| R-3 | Every **[TBD]** that blocks an AC is either decided or explicitly accepted as a default. | Now |
| R-4 | Related assumptions **[A-n]** are listed, and each has a named person to validate it. | Now |
| R-5 | Dependencies, including external ones such as Legal or engineering pipeline capabilities, are identified. | Now |
| R-6 | The story fits inside one pilot week. | Now |
| R-7 | The story stays within pilot scope: internal tool only, no customer-facing behavior. | Now |
| R-8 | Test questions or data needed to check the ACs are identified. | Soon |

Discovery work, such as checking whether a confidence score exists (A-5), can
start before a story is Ready. The DoR isn't meant to block learning.

## Definition of Done (DoD)

A story can move from `Review` to `Done` when:

| # | Criterion | Now / Soon |
|---|---|---|
| D-1 | All acceptance criteria are met and shown to the PM or the story's role owner. | Now |
| D-2 | Cross-cutting criteria X-1 to X-3 in `acceptance-criteria.md` still hold. | Now |
| D-3 | User-facing text (badges, banners, messages) has been reviewed. Disclaimer text has been reviewed by Legal or is clearly labeled DRAFT. | Now |
| D-4 | Relevant events are logged as defined in PA-09. | Soon (once PA-09 is done) |
| D-5 | Known limitations and any assumptions still unvalidated are written down in the story or issue. | Now |
| D-6 | Affected pilot agents and team leads have been told about the change. | Now |

### AI-Specific Done Criteria

| # | Criterion | Now / Soon |
|---|---|---|
| AI-1 | Only approved documents from the pilot set are used as sources. | Now |
| AI-2 | Fallback behavior ("No approved source found") has been tested on at least one no-source question. | Now |
| AI-3 | Generated outputs have been checked against the agreed pilot test questions **[TBD set]**. | Now |
| AI-4 | Human review and escalation paths work end-to-end where the story includes them. | Now |
| AI-5 | Prompt, threshold, topic-list, or model changes are recorded with the date and the reason. | Now |
| AI-6 | Evaluation results are labeled **pilot**, **mock**, or **validated**. Mock results are never presented as validated evidence. | Now |

## Current Readiness Snapshot

| Story | DoR status | Blocking items |
|---|---|---|
| PA-01 | Needs refinement | A-1 (OQ-1 and OQ-2 decided) |
| PA-02 | Needs refinement | A-3, A-4 |
| PA-03 | Needs refinement | A-2 (system of record and owner) |
| PA-04 | Needs refinement | OQ-3 threshold; A-5 |
| PA-05 | Needs refinement | OQ-4 topic list and owner; A-6 |
| PA-06 | Draft | OQ-5 reviewer role, turnaround, and rejection path |
| PA-07 | Ready (candidate) | A-9: Legal has no objection to the DRAFT placeholder; screen list [TBD] |
| PA-08 | Draft (blocked) | Legal sign-off (A-10, OQ-6) |
| PA-09 | Needs refinement | A-12 privacy approval; OQ-7 measures |
| PA-10 | Needs refinement | Depends on PA-09 |

## Review Cadence

Review both agreements at the end of each pilot week. Remove any criterion that
isn't helping, and move "Soon" items to "Now" when they're needed.
