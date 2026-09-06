# Pattern: Control Accretion

**Confidence / Status:** Observed / Active
**Anchor case(s):** `../cases/accepted/002-control-accretion-rerun.md`

### Plain-Language Version (人话版)

To make sure nothing was done wrong, we kept adding checks — until the
checks themselves became the thing making it wrong.

## What it is

Each individual verification, check, or safeguard added mid-task is
locally justified — it responds to a real risk the previous step
exposed. But the checks keep compounding, and at some point the control
layer stops observing the work and starts *changing the state it's
supposed to be verifying*, invalidating its own prior sign-off and
triggering another round of verification. Cost and new-failure-surface
rise together. Locally correct steps produce a systemically wrong
trajectory, with no single false premise to point to — which makes this
harder to catch than a classic wrong-hypothesis loop.

## Why "Control Accretion" and not something narrower

The anchor case's own write-up names four other candidate framings —
Semantic Ownership Loss, Control-Induced Drift, Assurance Work Displacing
Object Work, Locally Justified Escalation — that may turn out to be
distinct mechanisms rather than restatements of the same one. "Control
Accretion" is the working name because it's the most legible entry
point, not because the other four have been ruled out. See the anchor
case's Anti-Mapping Question for the specific risk: "controls kept
accumulating" could just describe ordinary defensive engineering; the
sharper, more falsifiable claim is that the control layer changed the
state it was verifying.

## Why this stays at Observed, not Emerging

One anchor case. Per §10 of `../protocol/open-praop-v0.1-final.md`,
`Emerging` requires that anchor *plus* additional independent evidence or
a second underlying incident — from a different environment, not a
second write-up of the same one. Neither exists yet.

## What would move this to Emerging

A second, independent-environment case where a verification or control
step added mid-task changes the state it's meant to verify, forcing
re-verification of work already signed off — not just "more checks got
added," but specifically the checks-invalidate-their-own-basis
mechanism.

## Related practice

`../practices/mid-run-issue-gate.md` — a first candidate practice for
managing this failure mode (untested against a second instance).

## Also see

§18 of the protocol cites this pattern's anchor case directly as the
reason Open PRAOP's own governance rules are deliberately kept minimal —
the same accretion mechanism this pattern describes in engineering work
can happen to a review process instead.

## Case Anchors

- Case 002 — Primary anchor

## Related Cases

None known yet.
