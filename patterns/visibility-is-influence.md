# Pattern: Visibility Is Influence

**Confidence / Status:** Observed / Active
**Anchor case(s):** `../cases/accepted/006-visibility-is-influence-fiction-tool.md`

### Plain-Language Version (人话版)

Whatever an AI can see, it gets pulled along by — and that pull is
often stronger than an explicit rule you wrote. Real control isn't
"write a rule after the fact"; it's "don't let it see what it
shouldn't in the first place."

## What it is

What a model can see directly shapes what it generates next, more
strongly than an explicit instruction can override. This isn't passive
awareness the way it would be for ordinary software, where data just
sits there until logic decides to use it — for an AI, seeing something
is itself a direct input to behavior. Removing information from view
can fix a failure that an explicit rule targeting the same failure
cannot.

## Why "Visibility Is Influence" and not "the prompt instruction was
poorly worded"

The anchor case's own Anti-Mapping Question makes the narrower claim
explicit: the instruction used ("do not repeat content from earlier
chapters") was direct and unambiguous, and it still had no measurable
effect — while a purely structural change (removing the outline from
view, no instruction added) substantially fixed the problem. If a
better-worded instruction had solved it instead, that would point to
ordinary prompt-engineering rather than a distinct claim about
visibility itself. The claim this pattern makes is specifically that
control operates more reliably through what's exposed than through
what's asserted.

## Why this stays at Observed, not Emerging

One Accepted anchor. Per §10 of
`../protocol/open-praop-v0.1-final.md`, `Emerging` requires that anchor
*plus* additional independent evidence or a second underlying incident,
from a different environment. `PLAIN_LANGUAGE_GUIDE.md` Entry 1
references a second, independent-environment incident (a
mortgage-advisory chat system carrying a customer's bankruptcy
disclosure and phone numbers forward simply because they were visible
in context) — genuinely a different domain and a different specific
mechanism (retained conversational state vs. a shown outline), but it
has not yet been independently submitted and Accepted as its own Case.
Per §10's loophole protections, an anchor must already be in `Accepted`
status; a well-documented but unsubmitted incident doesn't count yet.

## What would move this to Emerging

Formally submitting and Accepting the second incident referenced in
the Guide (or any other genuinely independent instance) as its own
Case — at which point this pattern would span two different domains
(creative-writing context management and conversational-state carry-
forward), strengthening the claim that this is a general mechanism
rather than something specific to one kind of tool.

## Related practice

None yet. The anchor case's own §K ("default to minimal necessary
context, not maximal — resist the intuition that more information will
help") is a first candidate, untested as a formal Practice.
