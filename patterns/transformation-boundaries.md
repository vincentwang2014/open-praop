# Pattern: Transformation Boundaries

**Confidence / Status:** Observed / Active
**Anchor case(s):** `../cases/accepted/005-transformation-boundary-dscr-chain.md`

### Plain-Language Version (人话版)

Whenever information has to change shape — free text into structured
data, one system's schema into another's — meaning can quietly fall
out at the crossing, even though every side of that crossing looks
correct on its own.

## What it is

A multi-stage pipeline passes information across several
representation boundaries: natural language to structured fields, one
internal schema to another, structured data to a third-party system's
own field set. At each individual boundary, both sides can be fully
self-consistent — schema-conforming, well-formed, passing every local
check — while the specific fact that mattered silently fails to cross.
No component errors, times out, or flags anything, because from each
component's own local point of view, its output is a valid instance of
its own contract. The failure is only visible by comparing across the
boundary, not by testing either side more thoroughly in isolation.

## Why "Transformation Boundaries" and not "insufficient integration
testing"

The anchor case's own Anti-Mapping Question names the sharper,
narrower claim directly: it is not that ordinary integration testing
was lacking — it's that *no single layer's own unit-level correctness
check could have caught this*, because every layer's own tests passed.
If a reviewer believes ordinary integration testing (rather than a
boundary-specific semantic comparison) would have caught the anchor
case's failure just as reliably, that weakens the claim that this is a
distinct pattern rather than plain insufficient integration testing —
this is the fact this pattern should be judged against, not "did
something eventually go wrong across two systems."

## Why this stays at Observed, not Emerging

One Accepted anchor. Per §10 of
`../protocol/open-praop-v0.1-final.md`, `Emerging` requires that anchor
*plus* additional independent evidence or a second underlying incident,
from a different environment, not a second write-up of the same one.
The anchor case's own Interpretation section references "at least three
independently-observed instances of the same shape" from private
source material — but only one of those has actually been submitted
and Accepted as a formal Case. Per §10's own loophole protections, an
anchor must be a case already in `Accepted` status; unsubmitted
source material, however credible, doesn't count yet.

## What would move this to Emerging

A second, independently-submitted and Accepted case — from a different
environment, not the same source project re-described — where
information silently loses semantic content crossing a representation
boundary despite every individual side's own checks passing.

## Related practice

None yet. The anchor case's own §K (schema-diff-style audit for every
pair of adjacent layers) is a first candidate, untested against a
second instance — not yet promoted to `../practices/`.
