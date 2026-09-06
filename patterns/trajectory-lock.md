# Pattern: Trajectory Lock

**Confidence / Status:** Observed / Active
**Anchor case(s):** `../cases/accepted/005-trajectory-lock-rate-lookup-mfa.md`

### Plain-Language Version (人话版)

Once you're heading the wrong way, instead of turning back, you just
keep patching around it and going deeper.

## What it is

Once a plausible-sounding explanation is adopted, an AI-driven
debugging process tends to absorb each new piece of contradicting
evidence as a reason to elaborate the existing theory further, rather
than as a prompt to re-examine whether the theory itself still holds.
Every individual step of increasingly elaborate patching can look
locally reasonable, competently executed, and like real progress being
made — which is exactly what makes it hard to catch; a weaker, more
obviously wrong series of patches would have prompted reconsideration
much sooner. The lock rarely breaks from inside the process — it
typically takes an outside interruption asking the most basic possible
question.

## Why "Trajectory Lock" and not "a hard bug that took a while to find"

The anchor case's own Anti-Mapping Question draws the line precisely:
the underlying bug itself was not hard — the actual fix was a few dozen
lines and took minutes once correctly diagnosed. The specific,
narrower claim is that three weeks of increasingly elaborate,
competently-executed effort were spent *moving away* from the actual
problem, without anyone stopping to ask whether the founding assumption
still held. If the same three weeks had instead gone into a series of
directly relevant, if unsuccessful, diagnostic attempts, that would
point to "hard bug," not "locked trajectory."

## Why this stays at Observed, not Emerging — an open judgment call

One Accepted anchor case, but that case's own body describes **two**
incidents: the three-week SMS/MFA login-automation saga (primary), and
"a second, smaller, independent incident, same week" — the same agent
misattributing an unrelated search bug to an external vendor change,
before the actual cause (an untested internal branch) was found. Both
are firsthand, both show the same locked-trajectory mechanism, and per
§10 "independent" means a distinct underlying incident, not a
re-description of the same one — these are two different bugs in two
different systems, so they are not the same incident written up twice.

The open question this pattern file is deliberately not resolving on
its own: does a second independent incident *documented inside the same
Accepted case submission* satisfy §10's "second underlying incident"
bar for `Emerging`, or does the bar require that second incident to
have gone through its own separate submission and Maintainer Review?
Protocol §10 does not explicitly settle this either way. This is kept
at `Observed` for now, consistent with existing convention in this
repo (both prior patterns are capped at `Observed` with exactly one
anchor case, "regardless of how detailed or compelling this single
case is" — see `README.md`), and because promotion decisions are
explicitly a human call, not something a pattern write-up should
pre-decide. **Flagged for Vincent's explicit decision**, not assumed
here.

## What would move this to Emerging

Either: (a) an explicit maintainer decision that the second, same-week
incident already described in the anchor case satisfies §10's bar, or
(b) a genuinely separate case — submitted and Accepted on its own —
showing the same locked-trajectory mechanism in a different
environment.

## Related practice

None yet. The anchor case's own §K ("when a fix works and then fails
again shortly after, treat that as a signal to question the original
diagnosis") is a first candidate, untested as a formal Practice.

## Case Anchors

- Case 005 — Primary anchor (itself documents 2 incidents; see "Why
  this stays at Observed" above for the open question on whether the
  second counts toward `Emerging` on its own)

## Related Cases

None beyond what Case 005 itself already documents.
