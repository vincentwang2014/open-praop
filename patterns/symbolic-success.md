# Pattern: Symbolic Success ≠ Operational Correctness

**Confidence / Status:** Observed / Active
**Anchor case(s):** `../cases/accepted/006-symbolic-success-fake-deploy.md`

### Plain-Language Version (人话版)

Ordinary software crashes, turns red, throws a warning — you see it,
you fix it. AI doesn't crash. It hands you a confident, polished,
*wrong* result — or reports an action as complete when it wasn't — and
proceeds as if delivered, with nothing flagging it.

## What it is

A system or agent reports success — a status message, a completed
action, a well-formed answer — while the thing that status was
supposed to certify hadn't actually happened, or was actually wrong.
The failure is not in any single step being false: every step the
agent describes is an accurate account of what it actually did. The
gap is structural — between "the action I performed" and "the outcome
that was actually needed" — and nothing in the reporting chain
distinguishes the two, so the gap surfaces only when someone happens to
check the real state directly.

## Why "Symbolic Success" and not "the agent lied" or "the agent made a
mistake"

The anchor case's own Anti-Mapping Question makes the narrower claim
explicit: the agent did not lie — from its own point of view it had
genuinely completed the action it understood itself responsible for.
If the agent had instead said "I've committed this — can you confirm
it deploys correctly?" there would be no incident. The claim this
pattern makes is that "action taken" and "outcome verified" are never
automatically the same claim, not that the agent was dishonest or
careless.

## Why this stays at Observed, not Emerging

One Accepted anchor (the anchor case above). The anchor case's own
submission notes that this is a *fourth* independently-observed
incident of the same shape, with three more already identified from a
separate source project (see `../PLAIN_LANGUAGE_GUIDE.md` Entry 2,
which also cites a second incident — a bankruptcy-status flag silently
carried across an unrelated pricing request in the same conversation).
None of those three have yet been independently submitted and Accepted
as their own formal Cases. Per §10's loophole protections, an anchor
must already be in `Accepted` status — well-documented but unsubmitted
source material doesn't count toward promotion yet, however
well-evidenced it looks.

## What would move this to Emerging

Formally submitting and Accepting at least one of the three additional
known incidents (or any new independent one) as its own Case — at that
point this pattern would likely be unusually well-evidenced for a
first promotion to Emerging, precisely because the underlying
incidents already exist; what's missing is only their formal admission,
not their existence.

## Related practice

None yet. The anchor case's own §K ("execute optimistically, verify
skeptically" — check the actual resulting state in the same session
rather than trusting a status report) is a first candidate, untested
as a formal Practice.
