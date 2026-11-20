# Acceptance Criteria: Policy Assistant Pilot

> **Status:** Draft for PM approval. Story text, assumptions **[A-n]**, and
> open questions **[OQ-n]** are in `story-backlog.md`. **[TBD]** marks a value
> the team must set; the agent didn't invent it.

Every criterion describes **observable product or workflow behavior**. Where an
AC depends on an open decision, it's tagged and shows the *proposed* default.

---

## Cross-Cutting Criteria (apply to every story)

- **X-1** All features are available only inside the internal support tool. No
  output from PA-01 to PA-10 is sent to customers automatically.
- **X-2** New UI elements (badges, banners, references, buttons) can be used
  with the keyboard and don't rely on color alone to convey meaning.
- **X-3** New UI elements don't push the answer response time past the agreed
  internal target **[TBD]**.

---

## E1: Source Traceability

### PA-01: Show the approved source behind each answer

- **AC-01.1** Given an answer generated from one approved document, the answer
  shows that document's **title** and **section heading**. If the document has
  no section headings, it shows the page number instead.
- **AC-01.2** Given an answer generated from more than one approved document,
  **every** contributing document is listed with its title and section.
  *[OQ-1: decided]*
- **AC-01.3** The source reference appears directly with the answer. The agent
  doesn't need any extra click to see it.
- **AC-01.4** Given a question for which no approved source is retrieved, **no
  generated answer text is shown**. Instead, the agent sees "No approved
  source found" and the standard escalation guidance. *[OQ-2: decided;
  this story owns the fallback]*
- **AC-01.5** On the agreed pilot test set of **[TBD]** questions, every
  displayed reference matches the document and section that were actually
  retrieved for that answer.

### PA-02: Open the cited policy section from the reference

- **AC-02.1** Clicking a source reference opens the document in a new tab or
  side panel. The agent's current support case stays open.
- **AC-02.2** If the document supports section anchors, it opens at the cited
  section. If it doesn't, it opens at the start and the cited section name is
  shown. *[A-4]*
- **AC-02.3** The link opens the **same approved version** that was cited, not
  a newer draft or a retired version.
- **AC-02.4** If the document can't be opened (missing, moved, or no access),
  the agent sees "Source could not be opened", the reference text stays
  visible, and the failure is logged (PA-09).

### PA-03: Restrict answers to approved, current documents

- **AC-03.1** Only documents marked "approved" in the system of record
  **[TBD system, A-2]** can be retrieved by the assistant.
- **AC-03.2** When a document is marked retired or draft, it's excluded from
  retrieval within **[TBD]** hours.
- **AC-03.3** A test question that matches **only** a retired or draft
  document triggers the PA-01 "No approved source found" fallback.
- **AC-03.4** Before the pilot starts, the policy content owner has signed off
  the list of documents in the pilot set.

---

## E2: Human Review of Risky Answers

### PA-04: Warn on low-confidence answers

- **AC-04.1** Given an answer with a confidence score below the threshold
  **[TBD, OQ-3]**, a "Requires Human Review" badge is shown next to the
  answer.
- **AC-04.2** Given an answer at or above the threshold, no badge is shown.
- **AC-04.3** The badge includes a text label and the reason ("Low
  confidence"). It doesn't rely on color alone.
- **AC-04.4** An authorized admin can change the threshold in configuration
  without a code release.
- **AC-04.5** Every time an answer is flagged, the event is logged with the
  answer ID, score, and reason (PA-09).
- **AC-04.6** This story doesn't block any agent action. Blocking belongs to
  PA-06.

### PA-05: Flag answers on sensitive topics

- **AC-05.1** Given an answer whose question or source matches a topic on the
  agreed sensitive-topic list **[TBD, OQ-4]**, the "Requires Human Review"
  badge is shown with the reason "Sensitive topic".
- **AC-05.2** If an answer is both low-confidence and sensitive, the badge
  shows both reasons.
- **AC-05.3** The designated list owner can edit the topic list without a code
  release.
- **AC-05.4** Each topic on the list has at least one test question that
  triggers the flag. A control set of **[TBD]** non-sensitive questions
  triggers no topic flags.

### PA-06: Block quick-copy until a flagged answer is reviewed

> Stays at `Draft` until OQ-5 (reviewer role, turnaround, rejection path) is
> answered.

- **AC-06.1** On a flagged answer, the quick-copy button is disabled and a
  tooltip explains why.
- **AC-06.2** A user with the reviewer role **[TBD]** can approve a flagged
  answer. After approval, quick-copy is enabled for that answer.
- **AC-06.3** A user without the reviewer role can't approve flagged answers.
- **AC-06.4** Each approval is logged with the reviewer ID, timestamp, and
  answer ID.
- **AC-06.5** The agent can see the review status of a flagged answer
  (`Pending review` / `Approved`).
- **AC-06.6** What happens when a reviewer **rejects** an answer is **[TBD,
  OQ-5]**. It must be defined before this story is Ready.

---

## E3: Internal Legal Disclaimer

### PA-07: Show an internal placeholder disclaimer

- **AC-07.1** A disclaimer banner appears on every screen that shows
  AI-generated content **[TBD: list of screens]**.
- **AC-07.2** The banner shows placeholder wording that is clearly labeled
  **"DRAFT – pending Legal approval"**.
- **AC-07.3** Agents can't dismiss or hide the banner.
- **AC-07.4** The banner text is loaded from a single managed setting, so it
  can be changed without a code release.
- **AC-07.5** The disclaimer is **not** included in any text copied by
  quick-copy or otherwise prepared for customers (internal only, X-1).

### PA-08: Replace the placeholder with Legal-approved wording

- **AC-08.1** The banner text matches the Legal-approved version **[TBD
  version ID / date]** character for character.
- **AC-08.2** The "DRAFT" label is removed only after the approved version ID
  is recorded in the managed setting.
- **AC-08.3** The approved version ID can be seen by an admin or auditor.
- **AC-08.4** AC-07.3 and AC-07.5 still hold after the wording is replaced.

---

## E4: Pilot Evidence

### PA-09: Log pilot usage events for evaluation

- **AC-09.1** These events are logged: question asked, answer shown, "no
  approved source" fallback shown, source reference clicked, source open
  failed, answer flagged (with reason), flag approved, quick-copy used, and
  issue reported.
- **AC-09.2** Each event records a timestamp, answer ID, and an agent
  identifier in the form approved by privacy review **[A-12]**.
- **AC-09.3** Customer personal data is not stored in the event log beyond
  what the privacy review approves **[TBD]**.
- **AC-09.4** The AI PM can export a weekly summary covering the flag rate,
  fallback rate, source-click rate, and issue reports.
- **AC-09.5** The success measures and the baseline method are written down
  and agreed by the end of pilot week 1 **[OQ-7]**. The agent doesn't define
  them.

### PA-10: Let agents report a wrong or unhelpful answer

- **AC-10.1** Each AI answer has a "Report issue" control.
- **AC-10.2** The agent picks a reason (`Incorrect`, `Outdated source`, `Wrong
  source`, `Unhelpful`, `Other`) and can add an optional comment. Submitting
  takes no more than two clicks, not counting the comment.
- **AC-10.3** Submitted reports appear in a list that the support team lead
  and policy content owner can see.
- **AC-10.4** Each report is logged as an event (PA-09) and linked to the
  answer ID and its cited sources.
