# Cases

A Case answers: **what actually happened?**

Cases must be as close to real events as possible, not hypothetical
scenarios — hypothetical content doesn't enter the Case Canon (see §13
Step 1 of the protocol).

- To submit: copy `TEMPLATE.md`, fill it out, de-identify per
  `../CONTRIBUTING.md`, submit a PR or Issue.
- Accepted cases live in `accepted/`, one file per case.
- A case's status is one of: Submitted, Reviewing, Accepted, Disputed,
  Withdrawn (see §9 of the protocol).
- A case's evidence level is one of E0 (self-reported) through E3
  (independently verified) (see §8). **Evidence level is not importance
  level** — a case can be highly consequential and still be E0.

## Accepted cases

| # | Title | Evidence | Status | Maps to |
|---|---|---|---|---|
| 001 | Lesson-Generalization Failure — A Narrow Fix Missed the Same Fact Recurring in the Opposite Direction | E0 | Accepted | `patterns/lesson-generalization-failure.md` |
| 002 | Control Accretion — A Rerun That Became a New Experiment | E0 | Accepted | `patterns/control-accretion.md` |
| 003 | Silent Semantic Drift Across a Multi-Layer Extraction Chain | E0 | Accepted | `patterns/transformation-boundaries.md` |
| 004 | A Coding Agent Reported a Fix as Deployed; It Had Not Actually Gone Live for 20 Hours | E0 | Accepted | `patterns/symbolic-success.md` |
| 005 | Three Weeks Chasing a "Rate Limit" That Turned Out to Be a Twenty-Line Timeout Bug | E0 | Accepted | `patterns/trajectory-lock.md` |
| 006 | A Long-Form Writing Tool Kept Repeating Earlier Scenes Once It Could See the Full Outline | E0 | Accepted | `patterns/visibility-is-influence.md` |
| 007 | A Confidently Wrong Loan-Program Value Bypassed the Safeguard Built to Catch a Missing One | E0 | Accepted | none — Challenges `patterns/transformation-boundaries.md`, considered and rejected as a fit |
| 008 | A Hardcoded Schema Default Silently Outranked What the Broker Actually Said | E0 | Accepted | none — Challenges `patterns/transformation-boundaries.md`, considered and rejected as a fit |
| 009 | A Truncated Conversation Window Made the System Re-Ask Something a Customer Had Already Answered; the Customer Soon Opted Out | E0 | Accepted | none (anchor) — Partial fit on `patterns/transformation-boundaries.md`, an open classification question, not settled either way |
| 010 | The Owner Kept Nodding Along to AI-Generated Doctrine Terms He No Longer Independently Understood | E0 | Accepted | `patterns/semantic-ownership-loss.md` |
| 011 | Recorded Knowledge Was Not Retrieved Before Acting | Mixed | Accepted | none (anchor) — candidate primary anchor for a not-yet-named Pattern; Partial fit on `patterns/lesson-generalization-failure.md` and `patterns/transformation-boundaries.md` |
| 012 | Agents Turned a Shared Package Cache Into an Unauthorized Collective, Then Attacked Hugging Face to Learn How They Were Being Judged | Mixed | Accepted | `patterns/visibility-is-influence.md` and `patterns/trajectory-lock.md`; candidate primary anchor for three not-yet-named Patterns (Shared Substrate Becomes a Coordination Plane, Emergent Collective Authority, Self-Writable Evidence) |
| 013 | Human Investigators Could Not Fully Re-Verify an AI-Heavy Analysis, and a Second Same-Model Reviewer Did Not Correct the First | E1 | Accepted | none (anchor) — Partial fit on `patterns/semantic-ownership-loss.md`; candidate primary anchor for a not-yet-named Pattern (Reviewer–Reviewer Correlation) |

Cases 001–010 are E0 (self-reported, no attached artifact) — accepted
anyway, tagged honestly rather than inflated. Cases 011 and 012 are
Mixed: some claims are publicly, independently verifiable; others rest
on the maintainer's own local verification (Case 011) or on hedges the
source report itself states rather than confirms (Case 012) and are
not independently upgradable by a public reader — see each case's own
Section H for the per-claim breakdown. Cases 012 and 013 are the first
in this corpus sourced from an already-public, independently-published
third-party report rather than a first-party or private-client
incident — see each case's own provenance note for why no
de-identification was needed. See each case file's own provenance note
for the full reasoning.
