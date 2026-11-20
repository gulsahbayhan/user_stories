# GitHub Issue Plan: Policy Assistant Pilot (Phase 5)

> **Status:** ✅ Approved and run on 2026-11-20. Steps 0–3 are complete; issues #1–#10 were created.

## Target and Pre-Checks (read-only, already run)

| Check | Result |
|---|---|
| Repository | `gulsahbayhan/user_stories` (issues enabled) |
| `gh auth status` | Logged in as `gulsahbayhan`. Scopes: `repo`, `workflow`, `read:org`, `gist` |
| Existing labels | GitHub defaults only. No `story` or `epic:*` labels yet. |
| Project scope | ⚠️ **Missing the `project` scope.** It isn't needed for creating issues. It *is* needed for Step 4 (adding issues to the `User Stories Workshop` project): `gh auth refresh -s project` |

## What Will Be Created

- **6 labels:** `story`, `epic:E1-traceability`, `epic:E2-human-review`,
  `epic:E3-disclaimer`, `epic:E4-pilot-evidence`, and `blocked`.
  Story quality and risk area aren't turned into labels, because they belong
  in the GitHub Project fields.
- **10 issues:** one per story. Each body is in `issue-drafts/PA-xx.md` and
  was generated from `story-backlog.md` and `acceptance-criteria.md`. Each body
  contains the story, notes, acceptance criteria, the full text of the linked
  assumptions, and its open questions.

| Issue title | Labels | Body file |
|---|---|---|
| [PA-01] Show the approved source behind each answer | story, epic:E1-traceability | `issue-drafts/PA-01.md` |
| [PA-02] Open the cited policy section from the reference | story, epic:E1-traceability | `issue-drafts/PA-02.md` |
| [PA-03] Restrict answers to approved, current documents | story, epic:E1-traceability | `issue-drafts/PA-03.md` |
| [PA-04] Warn on low-confidence answers | story, epic:E2-human-review | `issue-drafts/PA-04.md` |
| [PA-05] Flag answers on sensitive topics | story, epic:E2-human-review | `issue-drafts/PA-05.md` |
| [PA-06] Block quick-copy until a flagged answer is reviewed | story, epic:E2-human-review | `issue-drafts/PA-06.md` |
| [PA-07] Show an internal placeholder disclaimer | story, epic:E3-disclaimer | `issue-drafts/PA-07.md` |
| [PA-08] Replace the placeholder with Legal-approved wording | story, epic:E3-disclaimer, blocked | `issue-drafts/PA-08.md` |
| [PA-09] Log pilot usage events for evaluation | story, epic:E4-pilot-evidence | `issue-drafts/PA-09.md` |
| [PA-10] Let agents report a wrong or unhelpful answer | story, epic:E4-pilot-evidence | `issue-drafts/PA-10.md` |

## Commands

### Step 0: Duplicate guard (read-only)

```bash
gh issue list --state all --limit 100 | grep '\[PA-' || echo "No PA issues found"
```

Stop if any `[PA-xx]` issue already exists.

### Step 1: Labels

`--force` updates a label if it already exists, so this step can be re-run
safely.

```bash
gh label create "story"                  --color 0E8A16 --description "User story" --force
gh label create "epic:E1-traceability"   --color 4677A8 --description "Epic E1 Source Traceability" --force
gh label create "epic:E2-human-review"   --color 3B8A5A --description "Epic E2 Human Review of Risky Answers" --force
gh label create "epic:E3-disclaimer"     --color B77A1F --description "Epic E3 Internal Legal Disclaimer" --force
gh label create "epic:E4-pilot-evidence" --color 6F42C1 --description "Epic E4 Pilot Evidence" --force
gh label create "blocked"                --color B60205 --description "Blocked by an external dependency" --force
```

### Step 2: Issues

```bash
gh issue create --title "[PA-01] Show the approved source behind each answer"                --label story --label epic:E1-traceability   --body-file issue-drafts/PA-01.md
gh issue create --title "[PA-02] Open the cited policy section from the reference"           --label story --label epic:E1-traceability   --body-file issue-drafts/PA-02.md
gh issue create --title "[PA-03] Restrict answers to approved, current documents"            --label story --label epic:E1-traceability   --body-file issue-drafts/PA-03.md
gh issue create --title "[PA-04] Warn on low-confidence answers"                             --label story --label epic:E2-human-review   --body-file issue-drafts/PA-04.md
gh issue create --title "[PA-05] Flag answers on sensitive topics"                           --label story --label epic:E2-human-review   --body-file issue-drafts/PA-05.md
gh issue create --title "[PA-06] Block quick-copy until a flagged answer is reviewed"        --label story --label epic:E2-human-review   --body-file issue-drafts/PA-06.md
gh issue create --title "[PA-07] Show an internal placeholder disclaimer"                    --label story --label epic:E3-disclaimer     --body-file issue-drafts/PA-07.md
gh issue create --title "[PA-08] Replace the placeholder with Legal-approved wording"        --label story --label epic:E3-disclaimer --label blocked --body-file issue-drafts/PA-08.md
gh issue create --title "[PA-09] Log pilot usage events for evaluation"                      --label story --label epic:E4-pilot-evidence --body-file issue-drafts/PA-09.md
gh issue create --title "[PA-10] Let agents report a wrong or unhelpful answer"              --label story --label epic:E4-pilot-evidence --body-file issue-drafts/PA-10.md
```

If a command fails, the agent stops there and reports the error. It won't
retry blindly, because that could create duplicate issues.

### Step 3: Verify and record

```bash
gh issue list --limit 20
```

After this step, the agent writes each issue URL into the `GitHub issue`
column of `story-backlog.md`, compares GitHub with the backlog (missing items,
duplicates, title mismatches), and logs the result in
`ai-collaboration-log.md`.

## Not Included (needs separate approval)

- **Adding issues to the `User Stories Workshop` project and setting its
  fields** (Work type, Story quality, Risk area). This needs
  `gh auth refresh -s project` first, then `gh project list --owner
  gulsahbayhan` to find the project number.
- **Epic-level issues** for E1 to E4. They're optional, since the epic labels
  already group the stories.
- **Assignees.** No owner was set for any story.
- **Committing the backlog files to git.**

## Still Unvalidated (carried into the issues)

These appear in each affected issue body: A-1 to A-15 and OQ-3 to OQ-7.
Stories that aren't Ready yet: PA-06 (Draft) and PA-08 (blocked on Legal).
