# Case 006 — Visibility Is Influence: A Long-Form Writing Tool Kept Repeating Earlier Scenes Once It Could See the Full Outline

**Status:** Accepted
**Evidence level:** E0 — Self-Reported
**Date:** ~2026-05 (exact date not preserved in source material)
**Domain:** Software engineering — a personal long-form creative-writing
assistance tool
**AI system involved:** An LLM used to draft narrative scenes,
one scene at a time
**Maps to:** `../../patterns/visibility-is-influence.md` (Observed /
Active) — this is its anchor case; see `PLAIN_LANGUAGE_GUIDE.md`
Entry 1

### Plain-Language Version (人话版)

*Added by maintainer, per protocol §9 (Accepted cases should carry
one).*

A long-form writing tool drafted one scene at a time, and — on the
assumption that more context helps — also showed the AI the whole
chapter outline before every scene. The AI started repeating imagery
from earlier scenes. Telling it directly not to repeat itself did
nothing. What actually worked was the opposite: stop showing it the
outline at all, and let it see only the current scene's own
boundaries. What the model could see turned out to shape what it wrote
more strongly than an explicit rule could override.

> De-identified per `../../protocol/open-praop-v0.1-final.md` §7 —
> this case involved no client, no business, and no third party; the
> only change made is removing the operator's name (→ "the operator")
> and a personal detail about who the tool was originally built for,
> neither load-bearing to the mechanism.

---

### A. Basic Information

**Case title:** A Long-Form Writing Tool Kept Repeating Earlier Scenes
Once It Could See the Full Outline
**Date:** ~2026-05
**Domain:** Personal software project — AI-assisted long-form fiction
drafting
**AI system involved:** An LLM drafting one narrative scene at a time

### B. What Were You Trying to Do?

A tool split a chapter into individual scenes and had an LLM draft one
scene at a time, to keep each generation focused and accurate. On the
assumption that a human author benefits from seeing the whole chapter
outline before writing any one part of it, the tool also showed the AI
the full chapter outline before each scene-writing step.

### C. What Actually Happened?

The AI began repeating descriptions and imagery from earlier scenes
inside later scenes it was asked to write. The first fix attempted was
an explicit instruction — "do not repeat content from earlier
chapters." **It did not work; the repetition continued.** The fix that
actually worked was the opposite of the first instinct: stop showing
the AI the full chapter outline at all, and restrict what it could see
to only the current scene's own boundaries. After that change, cross-
scene repetition dropped sharply — it still occurred occasionally, but
lightly enough to require minimal manual cleanup.

### D. Why Did It Matter?

This was the operator's first clean opportunity to isolate a
mechanism, because the system itself was unusually simple — no
database, no auth, no API, no CRM, nothing else that could plausibly be
the cause. With everything else stripped away, the AI's own
probabilistic behavior was exposed with unusual clarity, closer to a
controlled low-noise experiment than a typical production incident.
Two intuitive fixes both failed before the actual mechanism was
identified: "give it more context so it writes better" made the
problem worse, not better; "tell it not to do that" did not work at
all.

### E. What Was Surprising?

Both of the operator's first instincts were wrong, in the same
direction: more information was assumed to help, and an explicit
instruction was assumed to be enforceable. Neither held. What worked
was neither "more context" nor "a stronger rule" — it was controlling
what the model could see in the first place.

### F. What Did You Try?

First: an explicit prompt instruction forbidding repetition of earlier
chapters' content. This had no measurable effect. Second: removing the
full chapter outline from the AI's context entirely, restricting it to
only the current scene's boundaries. This substantially reduced (though
did not fully eliminate) the repetition.

### G. What Happened Afterward?

The scene-boundary restriction became the standing design for the
tool. Residual, lighter repetition still occurred occasionally and
required minor manual editing — the fix reduced the failure rate, it
did not eliminate it outright.

### H. Evidence

Evidence retained only as the operator's own contemporaneous
observation and the tool's own behavior change after the fix; no
external log or transcript is attached to this submission.

### I. Interpretation

This suggests a general mechanism, not one specific to fiction-writing:
an AI does not treat visible information as optional context it may or
may not draw on — what it can see directly shapes what it generates
next, more strongly than an explicit instruction can override. This is
interpretation, not confirmed general theory from this one case alone —
the fuller Pattern write-up should be judged on its own evidence,
separately from this one case.

### J. Anti-Mapping Question

Could this be explained more simply as "the prompt instruction was
poorly worded"? The evidence against that reading: the instruction was
direct and unambiguous ("do not repeat prior chapters"), and it still
had no effect, while a purely structural change (removing visibility,
no instruction added) worked. If a better-worded instruction had solved
it, that would point to ordinary prompt-engineering rather than a
distinct claim about visibility itself.

### K. What Would You Do Differently Next Time?

Default to minimal necessary context, not maximal — resist the
intuition that "more information will help it perform better" for any
step with a bounded scope. When an explicit instruction fails to
prevent a high-probability behavior, look at what the model can see
before writing more rules — treat "remove the source of the pull"
as the first fix to try, not the last.

---

## Pattern Mapping

- Visibility Is Influence (`patterns/visibility-is-influence.md`) — Supports (Primary anchor)

Notes: informally related to "Probabilistic, Not a Rule Engine"
(`PLAIN_LANGUAGE_GUIDE.md` Entry 6) — no formal Pattern file exists for
that idea yet, so it isn't recorded as a Pattern Mapping relation.

---

### Maintainer review notes

- **Real enough:** firsthand, contemporaneous incident with a specific,
  unusually clean (low-noise, no other plausible cause) mechanism.
  Passes.
- **Privacy:** de-identified per protocol §7 — operator name and one
  personal detail removed; no client, business, or third party was ever
  involved in this incident to begin with. Combination-risk checked and
  assessed as passing — a generic architecture (LLM drafts one scene at
  a time, given varying context) with no naming, no business context,
  no customer, and no identifying technical specifics.
- **Fact vs. interpretation:** kept separate above (C vs. I) — a
  dangling reference to a nonexistent "Open questions" section (leftover
  from an earlier draft) was found in section I during review, fixed,
  and re-confirmed clean before Accept.
- **Evidence:** E0, self-reported only, no attached log — evidence
  level tracks attachment, not narrative quality, though the
  low-noise-environment framing makes the causal claim unusually
  legible for a single E0 case.
- **Mapping:** New pattern candidate, **Visibility Is Influence**.
  Anti-mapping question is credible — distinguishes from "the prompt
  instruction was poorly worded" by noting a purely structural fix
  worked where a direct, unambiguous instruction did not.
- **Confidence:** Case accepted; the pattern now exists at
  `../../patterns/visibility-is-influence.md`, `Observed / Active`
  with this case as its anchor. A second, independent instance is
  referenced in `PLAIN_LANGUAGE_GUIDE.md` Entry 1 (a mortgage-advisory
  chat system carrying forward a customer's bankruptcy disclosure and
  phone numbers simply because they were visible in context) but has
  not yet been independently submitted and Accepted as its own Case.
