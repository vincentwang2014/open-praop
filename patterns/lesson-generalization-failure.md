# Pattern: Lesson-Generalization Failure

**Confidence / Status:** Observed / Active
**Anchor case(s):** `../cases/accepted/001-lesson-generalization-failure.md`

### Plain-Language Version (人话版)

Last time you got hit, you only remembered not to touch that exact spot.
Change the shape a little, and you fall into the same hole again — not
because you forgot, but because what you remembered was too narrow.

## What it is

Remembering a correction is not the same as having learned its boundary.
A fix written immediately after a correction gets pattern-matched to the
literal symptom of that one complaint, rather than generalized to the
risk class it actually belongs to. When the same underlying fact
resurfaces in a structurally different — sometimes opposite — shape, the
existing fix doesn't fire, because it was never recognized as covering
that shape.

In the anchor case: four instances of over-narrating a standing fact
produced a fix scoped to "stop narrating this." The very next instance,
in the same session, was the opposite failure — under-applying the same
fact. The fix didn't cover it, because it had only ever addressed one
direction.

## Why this stays at Observed, not Emerging

One anchor case. Per §10 of `../protocol/open-praop-v0.1-final.md`,
`Emerging` requires that anchor *plus* additional independent evidence or
a second underlying incident. Neither exists yet.

## Distinction worth testing against a second instance

This is narrower than the general "self-knowledge ≠ enforcement" failure
mode (knowing a rule doesn't guarantee the next action obeys it). The
anchor case's recurrence is specifically *structurally opposite*
(over-narrate → under-apply), not just the same mistake repeating in the
same form. If a second instance turns out to be same-direction repetition
rather than direction-flipping, this pattern should fold into the
broader self-knowledge-vs-enforcement category rather than standing
alone — see the anchor case's Anti-Mapping Question.

## What would move this to Emerging

A second, independent case where a narrowly-scoped fix, written right
after a correction, fails specifically because the same underlying fact
recurs in a *different direction or shape* than the one the fix targeted
— not just any case where a fix turns out to be incomplete.

## Working recommendation (untested against a second instance)

When writing a standing-instruction fix immediately after a correction,
explicitly ask what the general risk class is, not just the literal
symptom of the complaint — before finalizing the wording. Test the fix
against the opposite-direction failure, not just a repeat of the
same-direction one.
