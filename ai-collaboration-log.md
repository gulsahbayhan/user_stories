# AI Collaboration Log: Policy Assistant Pilot

This log records what the AI agent (Claude Code) suggested or produced, and
what the AI Project Manager team decided. The team owns all product
decisions.

## Decision Log

| # | Phase | Prompt or request | Accepted | Edited | Rejected | Reason |
|---|---|---|---|---|---|---|
| 1 | Phase 1 | Team wrote three draft stories manually (traceability, human review, disclaimer). | — | — | — | Human-authored baseline, written before using the agent so the team could judge its suggestions. |
| 2 | Phase 2 | Agent INVEST critique: split the deep-link view out of Story 1. | ✅ Split into PA-01 (show source) and PA-02 (open cited section). | | | Lets source display ship even if section anchors aren't available for every document. |
| 3 | Phase 2 | Agent INVEST critique: break Story 2 into 2a / 2b / 2c. | ✅ Became PA-04 (low-confidence warning), PA-05 (sensitive-topic flag), PA-06 (block quick-copy). | | | Story 2 was too large and had two different triggers. Starting with a warning only lets the pilot measure the flag rate before adding friction. |
| 4 | Phase 2 | Agent INVEST critique: start Story 3 with a placeholder disclaimer while Legal reviews the wording. | ✅ Became PA-07 (internal DRAFT placeholder) and PA-08 (Legal-approved wording). | | | Removes Legal timing as a blocker for week 1 of the pilot. |
| 5 | Phase 2 | Agent noted that Story 1's "no approved source" case and Story 2's low-confidence flag overlap, and asked the team to decide which story owns it. | | ✏️ The team assigned ownership to **Story 1 (PA-01)**. | | Avoids duplicate fallback behavior. The agent had left the owner open; the team decided. |
| 6 | Phase 2 | Agent suggested a separate story for a **customer-facing disclaimer** if Legal requires one, and an AC to "reverse if Legal decides otherwise". | | | ❌ Rejected | Scope expansion beyond the 4-week internal support-agent pilot. No customer-facing features are allowed. **This is the team's example of correcting the agent.** |
| 7 | Phase 4 | "Create the workshop backlog for the Policy Assistant Pilot" (5 files, ≥ 8 stories, epics, ACs, marked assumptions). | ✅ Accepted (see row 8) | | | Agent produced 10 stories in 4 epics. |
| 8 | Phase 4 | PM review of the agent's additions | ✅ PA-03, PA-09, PA-10 (and epic E4); ✅ OQ-1 default (list every source); ✅ OQ-2 default (hide answer when no approved source) | | | They cover scenario constraints that the team drafts didn't, and the defaults make PA-01 testable. |
| 9 | Phase 5 | "Prepare gh commands" | ✅ PM approved the plan as written | | | Agent wrote `github-issue-plan.md` and `issue-drafts/`, and ran nothing before approval. |
| 10 | Phase 5 | Run the approved plan | ✅ Duplicate check passed; 6 labels and issues #1–#10 created | | | Verified with `gh issue list`: 10/10 titles match the backlog, labels are correct, every issue has acceptance criteria, and there are no duplicates. |
| 11 | Phase 5 | Add issues #1–#10 to the `User Stories Workshop` project and set Status, Work type, Story quality, and Risk area | — | — | — | **Done by the PM, not the agent.** The agent couldn't verify it: the token still lacks `read:project`, because the device-flow refresh hadn't completed. |
| 12 | Phase 6 | Final AI Project Manager audit, then commit and push | ✅ PM requested | | | See the audit summary below. |

## Agent Additions from Phase 4

The agent added these items that weren't in the team's drafts:

| Item | Agent's rationale | Decision |
|---|---|---|
| PA-03 Restrict answers to approved, current documents (new role: *policy content owner*) | Makes the scenario constraint "approved policy documents only" testable. | ✅ Accepted |
| PA-09 Log pilot usage events for evaluation | Covers the scenario constraint "evidence that the pilot saves time without increasing answer risk". | ✅ Accepted |
| PA-10 Let agents report a wrong or unhelpful answer | Gives the pilot a direct signal about answer risk. | ✅ Accepted |
| Epic E4 Pilot Evidence | Groups PA-09 and PA-10. | ✅ Accepted |
| Proposed defaults for OQ-1 (list all sources) and OQ-2 (hide the answer when there's no approved source) | Needed to make the PA-01 ACs testable. | ✅ Accepted |
| Proposed week-by-week delivery sequence | Based on dependencies only, not effort estimates. | ⏳ Not yet reviewed |

## What the Agent Didn't Do

- **Created GitHub issues only after explicit PM approval** (#1–#10). It
  didn't add them to the GitHub Project; the PM did that.
- **No user research, metrics, baselines, or thresholds were invented.** Every
  such value is marked **[TBD]** or listed as an assumption **[A-n]**.
- **Committed and pushed only when the PM asked** (Phase 6).

## Final Verification: AI Project Manager Audit (Phase 6, 2026-11-20)

| Check | Result | Evidence | Verified by |
|---|---|---|---|
| GitHub Project has the required columns and fields | ✅ PM-confirmed · ⚠️ not agent-verified | Columns: Backlog, Ready, In progress, Review, Blocked, Done. Fields: Work type, Story quality, Risk area, Owner. | PM (the agent's token lacks `read:project`) |
| At least eight issues exist | ✅ 10 issues | #1–#10 (`[PA-01]`–`[PA-10]`), all open, no duplicates | Agent (`gh issue list`) |
| Key stories have testable acceptance criteria | ✅ All 10 stories | 47 numbered criteria in `acceptance-criteria.md` plus cross-cutting X-1 to X-3; every issue body contains its criteria | Agent |
| Epics and dependencies are mapped | ✅ | `epic-map.md`: 4 epics mapped to scenario constraints, a dependency diagram, and scope boundaries | Agent |
| Ready/Done agreements and AI behavior checks are documented | ✅ | `ready-done-agreements.md`: DoR R-1 to R-8, DoD D-1 to D-6, AI checks AI-1 to AI-6, and a readiness snapshot | Agent |
| Human-versus-agent decisions are recorded | ✅ | This log: rows 1–12, plus the rejected customer-facing disclaimer suggestion (row 6) | Agent |

**Files created:** `story-backlog.md`, `acceptance-criteria.md`, `epic-map.md`,
`ready-done-agreements.md`, `ai-collaboration-log.md`, `github-issue-plan.md`,
and `issue-drafts/PA-01.md` to `PA-10.md`.

**Commands and tools used:** `gh auth status`, `gh repo view`,
`gh label list/create`, `gh issue list/create`, and `git`. Issue bodies were
generated from the backlog files with a local script, so they match.

**Still unvalidated:** assumptions A-1 to A-15 and open questions OQ-3 to OQ-7.
The ones most likely to block delivery are the confidence score (A-5), the
sensitive-topic owner (A-6), Legal sign-off timing (A-10), and privacy approval
for logging (A-12).

**Weak stories to revisit:** PA-06 (Draft: the reviewer workflow and rejection
path are undefined) and PA-08 (blocked on Legal). The proposed week-by-week
sequence hasn't been reviewed by the PM yet.

**Deferred until human approval:** every GitHub write (issues were created only
after "approve"). The agent didn't change project items; the PM did.

