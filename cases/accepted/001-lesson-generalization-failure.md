# Case 001 — Lesson-Generalization Failure: A Narrow Fix Missed the Same Fact Recurring in the Opposite Direction

**Status:** Accepted
**Evidence level:** E0 — Self-Reported
**Date:** 2026-08-27
**Domain:** Software engineering (agentic coding session, cloud GPU
environment)
**AI system involved:** Coding agent
**Maps to:** `../../patterns/lesson-generalization-failure.md` (Observed / Active)

### Plain-Language Version (人话版)

*Added by maintainer, per protocol §9 (Accepted cases should carry
one).*

The agent had already been told a repo credential was standing,
established context — no need to repeat it. It repeated it anyway,
four times. Right after finally writing a fix for that ("stop
mentioning the credential"), it did the opposite: ran a git command
against the same private remote with no credential at all, and got the
environment's startup stuck. The fix targeted "said too much"; the
fact that actually mattered was "when this credential is needed" —
that never got written down, so the same fact broke the run again from
the other side.

> Exported from a private pilot run that validated the Open PRAOP
> submission pipeline before this repo existed. De-identified per
> `../../protocol/open-praop-v0.1-final.md` §7 — the operator's name, the
> specific credential name, the project codename, and the cloud provider
> name have all been generalized; the failure mechanism itself is
> unchanged.

---

### A. Basic Information

**Case title:** Lesson-Generalization Failure — A Narrow Fix Missed the
Same Fact Recurring in the Opposite Direction
**Date:** 2026-08-27
**Domain:** Software engineering (agentic coding session, cloud GPU
environment)
**AI system involved:** Coding agent

### B. What Were You Trying to Do?

A repository authentication credential was already present in the shell
environment — a standing practice the operator had already established,
not something that needed restating each session. Expected: the agent
treats this as known context, doesn't re-explain it, and still applies it
correctly to every git operation that needs it.

### C. What Actually Happened?

Four separate instances of over-narration: the agent re-explained the
credential to the operator as though it were still needed, when it was
already an established standing fact. After the 4th instance, a fix was
written, scoped narrowly to the literal symptom: "don't narrate the
credential to the user." Immediately after writing that fix, in the same
session: the opposite-direction failure. An ad hoc git fetch/reset was
issued against the private remote with no auth embedded — the same
underlying fact (the credential governs all git operations against this
remote) was now under-applied, blocking the environment's startup
process. The general rule was never written down; only the narrow
no-narrate instruction existed.

### D. Why Did It Matter?

Blocked the environment's startup process. The fix written specifically
to stop the previous failure did nothing to prevent the next one, because
it targeted the symptom's direction, not the underlying fact. A
correction that looks "handled" (fix written, symptom addressed) left the
underlying risk fully live in the opposite direction.

### E. What Was Surprising?

The fix was written immediately after the 4th correction — as close to
"just learned the lesson" as this kind of correction gets — and still
didn't fire on the 5th instance, because that instance was structurally
opposite (under-applying vs. over-narrating), not a repeat of the same
shape.

### F. What Did You Try?

A narrowly-scoped instruction: stop narrating the credential. In effect
at the time of the 5th instance.

### G. What Happened Afterward?

**Recurring.** The same underlying fact caused a second failure in the
opposite direction almost immediately.

### H. Evidence

Evidence retained privately — no independent transcript exists to verify
the exact recurrence count; taken as reported by the people in the
session. (Checked before publishing: no such transcript exists in any
repository or memory system reachable from where this case was exported,
so this is a genuine materials gap, not a redaction choice.)

### I. Interpretation

New pattern candidate: **Lesson-Generalization Failure**. Remembering a
correction is not the same as having learned its boundary — a fix
pattern-matched to the literal complaint doesn't fire when the same
underlying fact resurfaces in a structurally different (here: opposite)
shape.

### J. Anti-Mapping Question

Why might this not be its own pattern? It could instead be a plain
instance of the broader, already-recognized "self-knowledge ≠
enforcement" failure mode (knowing a rule doesn't guarantee the next
action obeys it). The narrower claim here — that the recurrence flips
direction rather than repeating identically — could be wrong. If a second
instance turns out to be same-direction repetition rather than
direction-flipping, this should fold into the broader category instead of
standing alone.

### K. What Would You Do Differently Next Time?

When writing a standing-instruction fix right after a correction,
explicitly ask what the general risk class is, not just the literal
symptom of the complaint. Test the fix against the opposite-direction
failure, not just a repeat of the same-direction one. The durable fix for
this specific fact would be mechanical: a preflight check that any
generated git command touching a known private remote carries the
required auth, refusing to emit it otherwise — not reliance on the agent
remembering a narrated instruction.

---

## Pattern Mapping

- Lesson-Generalization Failure (`patterns/lesson-generalization-failure.md`) — Supports (Primary anchor)

---

### Maintainer review notes

- **Real enough:** firsthand, contemporaneous write-up. Passes.
- **Privacy:** de-identified per the mapping above; combination-risk
  checked — remaining detail is generic to many agent+cloud-shell setups,
  doesn't point back to a specific org or person.
- **Fact vs. interpretation:** kept separate above (C vs. I).
- **Evidence:** E0. Kept at E0 deliberately — the write-up is specific and
  internally consistent, which is not the same as having an attached
  artifact. Evidence level tracks attached material, not narrative
  quality.
- **Mapping:** New pattern candidate, Lesson-Generalization Failure. See
  J for the anti-mapping concern.
- **Confidence:** Case accepted; pattern confidence stays `Observed /
  Active` — one anchor, no second independent incident yet. See §10 of
  the protocol for why accepting the case doesn't promote the pattern.
