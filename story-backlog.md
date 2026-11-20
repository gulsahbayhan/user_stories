# Story Backlog: Policy Assistant Pilot

> **Status:** Approved by the PM. GitHub issues #1–#10 were created on 2026-11-20
> (Phase 5) after PM approval.

## Scope

- **In scope:** A 4-week internal pilot. Support agents use an AI assistant
  that answers only from approved policy documents.
- **Out of scope:** Any customer-facing feature, including disclaimers in
  customer messages, customer self-service, and automated sending. The team
  rejected these as scope expansion; see `ai-collaboration-log.md`.

## Legend

| Marker | Meaning |
|---|---|
| **[A-n]** | Assumption that needs human validation. See the [Assumption Register](#assumption-register). |
| **[OQ-n]** | Open question that needs a decision. See [Open Questions](#open-questions). |
| **[TBD]** | A value or decision that hasn't been made yet. The agent left it blank on purpose rather than inventing one. |
| **Story quality** | `Draft` / `Needs refinement` / `Ready`. These match the GitHub Project field. |
| **Origin** | `Team` means a team draft refined in Phase 2. `Agent (accepted)` means the agent proposed it in Phase 4 and the PM accepted it. |

## Backlog Summary

| ID | Title | Epic | Role | Origin | Story quality | Risk area | Depends on | GitHub issue |
|---|---|---|---|---|---|---|---|---|
| PA-01 | Show the approved source behind each answer | E1 | Support agent | Team (Story 1) | Needs refinement | Source quality | — | [#1](https://github.com/gulsahbayhan/user_stories/issues/1) |
| PA-02 | Open the cited policy section from the reference | E1 | Support agent | Team (Story 1 split) | Needs refinement | Source quality | PA-01 | [#2](https://github.com/gulsahbayhan/user_stories/issues/2) |
| PA-03 | Restrict answers to approved, current documents | E1 | Policy content owner | Agent (accepted) | Needs refinement | Source quality | — | [#3](https://github.com/gulsahbayhan/user_stories/issues/3) |
| PA-04 | Warn on low-confidence answers | E2 | Support agent | Team (Story 2a) | Needs refinement | Human review | — | [#4](https://github.com/gulsahbayhan/user_stories/issues/4) |
| PA-05 | Flag answers on sensitive topics | E2 | Support team lead | Team (Story 2b) | Needs refinement | Human review | PA-04 (shared badge) | [#5](https://github.com/gulsahbayhan/user_stories/issues/5) |
| PA-06 | Block quick-copy until a flagged answer is reviewed | E2 | Support team lead | Team (Story 2c) | Draft | Human review | PA-04, PA-05 | [#6](https://github.com/gulsahbayhan/user_stories/issues/6) |
| PA-07 | Show an internal placeholder disclaimer | E3 | Legal compliance officer | Team (Story 3) | Ready (candidate) | Legal | — | [#7](https://github.com/gulsahbayhan/user_stories/issues/7) |
| PA-08 | Replace the placeholder with Legal-approved wording | E3 | Legal compliance officer | Team (Story 3) | Draft (blocked) | Legal | PA-07, Legal sign-off | [#8](https://github.com/gulsahbayhan/user_stories/issues/8) |
| PA-09 | Log pilot usage events for evaluation | E4 | AI Project Manager | Agent (accepted) | Needs refinement | Privacy | — | [#9](https://github.com/gulsahbayhan/user_stories/issues/9) |
| PA-10 | Let agents report a wrong or unhelpful answer | E4 | Support agent | Agent (accepted) | Needs refinement | Source quality | PA-09 | [#10](https://github.com/gulsahbayhan/user_stories/issues/10) |

The acceptance criteria for every story are in `acceptance-criteria.md`.

---

## E1: Source Traceability

### PA-01: Show the approved source behind each answer

```text
As a support agent,
I want each AI answer to show the title and section of the approved policy
document(s) it is based on,
so that I can verify the source before replying to a customer.
```

- **Notes:** The team decided that this story owns the **"no approved source
  found" fallback**, so PA-04 does not duplicate it. The deep link was split
  out into PA-02.
- **Decisions:** [OQ-1] list every contributing document; [OQ-2] hide the
  generated answer when no approved source is found. Both decided by the PM.
- **Assumptions:** [A-1], [A-14].

### PA-02: Open the cited policy section from the reference

```text
As a support agent,
I want to click a source reference and land on the cited section of the
approved document,
so that I can check the exact wording without searching for it.
```

- **Notes:** Split out of the original Story 1 so that PA-01 can ship even if
  section anchors aren't available for every document.
- **Assumptions:** [A-3], [A-4].

### PA-03: Restrict answers to approved, current documents

```text
As a policy content owner,
I want the assistant to use only documents currently marked as approved,
so that agents never see answers based on draft or retired policy.
```

- **Notes:** Proposed by the agent and accepted by the PM. It turns the
  scenario constraint "approved policy documents only" into a testable story.
- **Assumptions:** [A-2]. The role "policy content owner" exists and someone
  is named in it, which is also part of [A-2].

---

## E2: Human Review of Risky Answers

### PA-04: Warn on low-confidence answers (Story 2a)

```text
As a support agent,
I want AI answers below the agreed confidence threshold to show a
"Requires Human Review" warning,
so that I know not to send them to a customer without checking.
```

- **Notes:** This story only warns. It doesn't block quick-copy. The pilot
  measures the flag rate before deciding whether blocking (PA-06) is worth the
  friction.
- **Open questions:** [OQ-3] threshold value.
- **Assumptions:** [A-5], [A-15].

### PA-05: Flag answers on sensitive topics (Story 2b)

```text
As a support team lead,
I want answers about agreed sensitive topics to be flagged for review,
so that risky information is not sent to customers unchecked.
```

- **Open questions:** [OQ-4] topic list and owner.
- **Assumptions:** [A-6].

### PA-06: Block quick-copy until a flagged answer is reviewed (Story 2c)

```text
As a support team lead,
I want flagged answers to be blocked from quick-copy until an authorized
reviewer approves them,
so that unreviewed answers cannot be sent by accident.
```

- **Notes:** Stays at `Draft` until the review workflow is defined.
- **Open questions:** [OQ-5] reviewer role, turnaround target, rejection path.
- **Assumptions:** [A-7], [A-8].

---

## E3: Internal Legal Disclaimer

### PA-07: Show an internal placeholder disclaimer

```text
As a legal compliance officer,
I want a clearly labeled placeholder disclaimer on every screen where agents
see AI-generated content,
so that agents treat AI output as assistive, not binding legal advice, from
day one of the pilot.
```

- **Notes:** The team chose a placeholder so that the pilot isn't blocked while
  Legal reviews the wording. The disclaimer is internal only and never appears
  in customer messages.
- **Assumptions:** [A-9], [A-11].

### PA-08: Replace the placeholder with Legal-approved wording

```text
As a legal compliance officer,
I want the placeholder replaced with the exact Legal-approved disclaimer
wording,
so that the internal tool carries the signed-off text.
```

- **Notes:** Blocked until Legal signs off.
- **Open questions:** [OQ-6] sign-off date and what to do if it's missed.
- **Assumptions:** [A-10].

---

## E4: Pilot Evidence

### PA-09: Log pilot usage events for evaluation

```text
As the AI Project Manager,
I want key assistant interactions logged,
so that I can report whether the pilot saves agent time without increasing
answer risk.
```

- **Notes:** Proposed by the agent and accepted by the PM. It covers the scenario constraint
  "evidence that the pilot saves time without increasing answer risk". **The
  agent doesn't assume any baseline data exists.** The team must agree on how
  the baseline will be measured.
- **Open questions:** [OQ-7] success measures and baseline method.
- **Assumptions:** [A-12], [A-13].

### PA-10: Let agents report a wrong or unhelpful answer

```text
As a support agent,
I want to report an AI answer as wrong, outdated, or unhelpful in one step,
so that problems reach the team lead and policy owner quickly.
```

- **Notes:** Proposed by the agent and accepted by the PM. It gives the pilot a direct signal
  about answer risk, alongside PA-09.
- **Assumptions:** [A-2] (the policy owner who receives reports exists).

---

## Proposed Delivery Sequence

> This sequence is a **proposal** for the PM to confirm. It's based on
> dependencies, not on effort estimates.

| Pilot week | Stories | Why |
|---|---|---|
| Week 1 | PA-03, PA-01, PA-07, PA-09 | Foundations first: approved-only sources, visible traceability, placeholder disclaimer, and evidence logging from day one. |
| Week 2 | PA-02, PA-04, PA-10 | Adds the deep link and the warning-only flag, and starts collecting flag-rate and issue-report data. |
| Week 3 | PA-05, PA-08 (if Legal has signed off) | Depends on the sensitive-topic list and Legal timing. |
| Week 4 | PA-06 (only if the review workflow is defined and the flag rate is acceptable) | The highest-friction control is decided last, using pilot data. |

---

## Assumption Register

These are **unvalidated**. Each one needs a named person to confirm or reject
it.

| ID | Assumption | Stories | Validate with | Status |
|---|---|---|---|---|
| A-1 | All approved policy documents in the pilot set are digitized and indexed with section metadata. | PA-01, PA-02 | Policy content owner / engineering | Open |
| A-2 | There is a single system of record for document approval status and version, with a named policy content owner. | PA-03, PA-10 | Policy / knowledge management | Open |
| A-3 | Pilot agents already have read access to the system that stores the source documents. | PA-02 | IT / access management | Open |
| A-4 | Source documents support section-level deep links (anchors) for at least some formats. | PA-02 | Engineering | Open |
| A-5 | The retrieval or model pipeline produces a confidence score reliable enough to set a threshold on. | PA-04 | Engineering / ML | Open |
| A-6 | Someone owns the definition of "sensitive topic" and can provide a list within the pilot window. | PA-05 | Support leadership / Compliance | Open |
| A-7 | Reviewers have enough capacity to keep review turnaround acceptable. | PA-06 | Support team lead | Open |
| A-8 | Blocking quick-copy is a meaningful control even though agents can still retype the text. | PA-06 | Support team lead / Compliance | Open |
| A-9 | Running the pilot with a clearly labeled DRAFT disclaimer is acceptable to Legal and Compliance. *(The PM team accepted this; Legal hasn't confirmed it yet.)* | PA-07 | Legal | Open |
| A-10 | Legal can sign off on the disclaimer wording within the 4-week pilot. | PA-08 | Legal | Open |
| A-11 | An internal-only disclaimer is enough for this pilot. *(This follows from the scope decision, but Legal should confirm it.)* | PA-07, PA-08 | Legal | Open |
| A-12 | Logging agent interactions is allowed under internal privacy or employee-monitoring policy. | PA-09 | Privacy / HR / works council (if applicable) | Open |
| A-13 | A time baseline can be measured. No existing baseline data is assumed. | PA-09 | AI PM / support team lead | Open |
| A-14 | Agents will check sources before replying. This is a behavior assumption, not established evidence. | PA-01 | Pilot observation (PA-09 click data) | Open |
| A-15 | The flag rate will be low enough that agents aren't slowed down more than the pilot gains. | PA-04, PA-06 | Pilot data (PA-09) | Open |

## Open Questions

| ID | Question | Default or decision | Owner | Blocks |
|---|---|---|---|---|
| OQ-1 | What happens if an answer relies on multiple policy documents? | ✅ **Decided:** list every contributing document. | PM + support team lead | — |
| OQ-2 | When no approved source is found, should the answer be hidden or shown with a warning label? | ✅ **Decided:** hide the generated answer and show a "No approved source found" message. | PM + Compliance | — |
| OQ-3 | What confidence threshold triggers a warning? | [TBD]. Must be configurable. | Engineering / ML + PM | PA-04 |
| OQ-4 | Which topics are "sensitive", and who maintains the list? | [TBD] | Support leadership / Compliance | PA-05 |
| OQ-5 | Who reviews flagged answers, what's the turnaround target, and what happens when an answer is rejected? | [TBD] | Support team lead | PA-06 |
| OQ-6 | When will Legal sign off, and what's the fallback if it's after the pilot? | Keep the DRAFT placeholder for the rest of the pilot. | Legal + PM | PA-08 |
| OQ-7 | Which measures show "saves time without increasing risk", and how is the baseline captured? | [TBD] | AI PM | PA-09 |
