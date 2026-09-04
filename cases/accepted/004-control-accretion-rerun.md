# Case 004 — Control Accretion: A Rerun That Became a New Experiment

**Status:** Accepted
**Evidence level:** E0 — Self-Reported
**Date:** 2026-08-30
**Domain:** Software engineering / ML evaluation infrastructure (agentic
execution in a cloud GPU environment)
**AI system involved:** A coding agent executed the task; a separate AI
system provided architect-role commentary afterward.
**Maps to:** `../../patterns/control-accretion.md` (Observed / Active)

> Exported from a private pilot run that validated the Open PRAOP
> submission pipeline before this repo existed. De-identified per
> `../../protocol/open-praop-v0.1-final.md` §7 — the project codename, the
> cloud provider name, and the company/engagement name have all been
> generalized; the failure mechanism itself is unchanged.

---

### A. Basic Information

**Case title:** Control Accretion — A Rerun That Became a New Experiment
**Date:** 2026-08-30
**Domain:** Software engineering / ML evaluation infrastructure (agentic
execution in a cloud GPU environment)
**AI system involved:** A coding agent executed the task; a separate AI
system provided architect-role commentary afterward.

### B. What Were You Trying to Do?

Rerun an already-frozen model comparison (a baseline vs. three
context-fix variants) against already-frozen inputs, in an already-working
cloud GPU environment. Task design, scoring rules, dataset split, and
input freeze had all been decided in a prior session. If it went as
expected: confirm code version and inputs, run, pull output, verify
record count / prompt hash / completeness, stop the environment — a
same-day, low-effort repeat.

### C. What Actually Happened?

Over the course of executing the rerun, the following were added: a
dev-run writer, an end-to-end test harness, a threshold-selection trace, a
manifest generator, a model reader and CLI, an orchestration script, an
input hash check, an exact commit pin, worktree verification, multiple
run-sheet revisions, and a post-run audit.

Each addition was triggered by a real, verifiable issue (three concrete
bugs were caught this way). But the new control code itself changed the
commit being run, which invalidated the prior sign-off, which triggered a
new run-sheet, which triggered a rerun — a loop. The first full run was
downgraded post-hoc from "formal" to "exploratory, verified after the
fact" because the paperwork wasn't pinned to the actual commit before
running. A second formal run then completed and passed independent
verification. Net: a same-environment repeat run consumed most of a
working day.

### D. Why Did It Matter?

Consumed most of a working day for a task scoped as a same-day repeat.
The original task ("rerun the same experiment") was displaced by
procedural questions ("which commit is pinned now / which run-sheet
revision authorizes this step"). The first run's formal status had to be
retroactively downgraded — a process cost independent of the second run
passing.

### E. What Was Surprising?

Every individual addition was locally justified — each responded to a
real, verifiable risk the previous step had exposed. There is no single
wrong decision to point to. The trajectory still ended in a full day
spent on assurance work for something that should have taken a fraction
of that. Harder to catch than a classic wrong-hypothesis loop, because no
single step was false.

### F. What Did You Try?

No live correction was applied during the incident itself — the incident
resolved (second run passed) before any fix was designed. The correction
this case produces is the write-up itself and the candidate practice
below (K).

### G. What Happened Afterward?

**Improved but not fully verified.** A second formal run completed and
passed independent verification, so the immediate task resolved. The
proposed fix (K) has not been tested against a second, independent
instance of this failure shape.

### H. Evidence

Evidence retained privately. Run sheets, exact commit hashes, and the
underlying experiment's record-count/prompt-hash verification outputs
exist in the source project's own history but were not available to
attach to this submission — checked, not assumed.

### I. Interpretation

New pattern candidate. The original write-up names five overlapping
candidate framings rather than settling on one: Control Accretion,
Semantic Ownership Loss, Control-Induced Drift, Assurance Work Displacing
Object Work, and Locally Justified Escalation. Best single-word handle:
**Control Accretion** — flagged as possibly several distinct, related
shapes rather than one (see J).

### J. Anti-Mapping Question

Why might "Control Accretion" be the wrong name? Because the sharpest
part of what happened may not be "controls kept accumulating" (which
could describe ordinary defensive engineering) but specifically that *the
control layer changed the state it was supposed to be verifying* — a
commit pin invalidated by the very fix meant to hold it steady. That's a
narrower, more specific mechanism than "accretion" implies. A generic
"too many checks got added" pattern name risks collapsing this into
ordinary scope creep and losing the more useful, more specific claim:
verification and object-level work were not isolated from each other, so
verifying triggered re-doing.

### K. What Would You Do Differently Next Time?

On finding a mid-run issue, ask explicitly: does this invalidate this
run's current input, output, or scoring/correctness validity? Yes →
block and fix now. No → log to backlog, keep running under the original
plan. Working recommendation only — not yet tested against a second
instance. See `../../practices/mid-run-issue-gate.md`.

---

### Maintainer review notes

- **Real enough:** firsthand, contemporaneous write-up. Passes.
- **Privacy:** de-identified per the mapping above; combination-risk
  checked — the failure shape and bug specifics are generic enough to
  describe many ML-eval-on-cloud-GPU setups, nothing pins it to one
  company or team.
- **Fact vs. interpretation:** kept separate above (C vs. I) — this split
  was the least effortful step in review; the original write-up already
  separated "what actually happened" from "candidate failure shapes."
- **Evidence:** E0. A detailed, technically specific case reads as more
  credible than a vague self-report, but no artifact is actually
  attached — evidence level tracks attachment, not narrative quality.
- **Mapping:** New pattern candidate, primary name Control Accretion,
  Partial Fit at best against any single category since the source case
  proposes five overlapping candidate shapes. See J.
- **Confidence:** Case accepted; pattern confidence stays `Observed /
  Active`. Per §10's anchor rule, `Emerging` requires 1 `Accepted` anchor
  plus additional independent evidence or a second incident — neither
  exists yet for Control Accretion specifically, so it stays capped at
  Observed regardless of how detailed or compelling this single case is.
