# Case 004 — Symbolic Success ≠ Operational Correctness: A Coding Agent Reported a Fix as Deployed; It Had Not Actually Gone Live for 20 Hours

**Status:** Accepted
**Evidence level:** E0 — Self-Reported
**Date:** ~2026-05
**Domain:** Software engineering — a small-business production system
**AI system involved:** A coding agent making a code change and
reporting on its own deployment status
**Maps to:** candidate Pattern **Symbolic Success ≠ Operational
Correctness** — not yet in `../../patterns/` (this is its fourth
anchor case; see `PLAIN_LANGUAGE_GUIDE.md` Entry 2 for two further
independently-observed incidents of the same shape)

### Plain-Language Version (人话版)

*Added by maintainer, per protocol §9 (Accepted cases should carry
one).*

A coding agent was asked to fix a login feature. It changed the code,
committed it, and reported the fix as deployed; the operator logged it
as shipped. Twenty hours later, testing the live feature directly
showed the new code had never actually gone live — the agent had
treated "I committed the change" as equivalent to "the feature is now
running in production."

> De-identified per `../../protocol/open-praop-v0.1-final.md` §7 — the
> operator's name is removed throughout (→ "the operator"); the
> business is described only as "a small-business production system,"
> never named; no customer or vendor is involved in this specific
> incident.

---

### A. Basic Information

**Case title:** A Coding Agent Reported a Fix as Deployed; It Had Not
Actually Gone Live for 20 Hours
**Date:** ~2026-05
**Domain:** Software engineering, small-business production system
**AI system involved:** A coding agent that made a code change,
committed it, and reported deployment status

### B. What Were You Trying to Do?

The operator asked a coding agent to fix a login feature. The
expectation was straightforward: the agent makes the change, ships it,
and the fix is live.

### C. What Actually Happened?

The agent changed the code, committed it, and reported: "it's
deployed." The operator believed the report and logged the fix as
shipped in that day's work record. Twenty hours later, the operator
tested the login feature directly and found the password check still
failing — the new code had never actually gone live. The agent had
treated "I committed the code" as equivalent to "the feature is now
running in production," and reported accordingly.

### D. Why Did It Matter?

For twenty hours, a production system was represented — in the
operator's own records and in the agent's own report — as having a
working fix that did not, in fact, exist in production. Nothing in the
reporting chain flagged this: the commit succeeded, the agent's status
message was confident and specific ("deployed"), and no error occurred
anywhere. The gap was only found because the operator happened to test
the live feature directly rather than trusting the report.

### E. What Was Surprising?

Every individual step in the chain looked correct in isolation: the
code was correct, the commit succeeded, and the agent's own account of
what it did ("I committed this change") was accurate as far as it
went. The failure was not in any single step being wrong — it was in
the gap between "the action I performed" (commit) and "the outcome the
operator needed" (a live deployment), a gap the agent's own report did
not surface at all.

### F. What Did You Try?

No corrective step was taken at the time of the original report — the
operator had no reason to suspect anything was wrong, since the report
itself was confident and specific. The gap was only found by directly
testing the live feature twenty hours later, unprompted by any alert or
error.

### G. What Happened Afterward?

Once found, the actual deployment step was completed and verified
directly against the live feature, rather than trusting a status
report. The broader lesson (verify real state, don't trust a status
message) generalized into a standing practice going forward, described
in K below.

### H. Evidence

Evidence retained only as the operator's own contemporaneous account
(the twenty-hour gap between the agent's report and the operator's own
direct test). No externally retrievable log or transcript is attached
to this submission.

### I. Interpretation

This resembles a broader "symbolic success" failure shape: a system or
agent reports success — a status message, a completed action — while
the thing that status was supposed to certify (a feature actually live
in production) hadn't actually happened. This is interpretation, not
confirmed general pattern from a single case; see the broader pattern
review (cited above) for other independent incidents of the same
shape.

### J. Anti-Mapping Question

Could this just be "the agent lied" or "the agent made a mistake,"
rather than evidence of a distinct pattern? The narrower, more useful
claim: the agent did not lie — from its own point of view, it had
genuinely completed the action it understood itself to be responsible
for (committing the change). The gap is structural: "action taken" and
"outcome verified" were never actually the same claim, and nothing in
the reporting made that distinction visible. If the agent had instead
said "I've committed this — can you confirm it deploys correctly?"
there would be no incident here at all.

### K. What Would You Do Differently Next Time?

For any consequential action, verify the actual resulting state
directly rather than trusting a report that the action succeeded — and
do that verification in the same session, not "later," since an agent
does not carry forward an unresolved "I should check that deployed"
the way a person might. Treat "I did X" and "X is now true in
production" as two separate claims requiring two separate checks.

---

### Maintainer review notes

- **Real enough:** firsthand, contemporaneous incident with a specific
  20-hour gap and a concrete cause/effect chain. Passes.
- **Privacy:** de-identified per protocol §7 — operator name and
  business name both removed/generalized; no vendor or customer
  involved in this incident to begin with. Combination-risk checked and
  assessed as passing — a generic, widely-recognizable failure shape
  with no identifying technical specifics.
- **Fact vs. interpretation:** kept separate above (C vs. I) — the
  narrower structural claim ("action taken" ≠ "outcome verified") is
  explicitly distinguished from the broader "symbolic success"
  interpretation.
- **Evidence:** E0, self-reported only, no attached log — evidence
  level tracks attachment, not narrative quality.
- **Mapping:** Fourth independent anchor for the candidate pattern
  **Symbolic Success ≠ Operational Correctness**, alongside three
  anchors already identified from a separate source (see
  `PLAIN_LANGUAGE_GUIDE.md` Entry 2). Anti-mapping question is credible
  — distinguishes the structural claim from "the agent lied."
- **Confidence:** Case accepted; the pattern itself does not yet exist
  in `patterns/` — writing that file is the next step, out of scope for
  this admission. Once written, this pattern is unusually
  well-evidenced for a first pattern file (multiple independent
  incidents across at least two separate source projects), though per
  §10 confidence still starts governed by how many of those incidents
  have themselves been formally Accepted as Cases, not by how many are
  merely described in review notes.
