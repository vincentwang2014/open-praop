# Case 009 — A Truncated Conversation Window Made the System Re-Ask Something a Customer Had Already Answered; the Customer Soon Opted Out

**Status:** Accepted
**Evidence level:** E0 — Self-Reported
**Date:** 2026-05-15
**Domain:** Software engineering — AI-assisted customer-facing SMS
intake, small-business production system (same overall business as
Cases 003, 007, and 008, different channel — customer-facing rather
than broker-facing)
**AI system involved:** A lightweight LLM handling a multi-turn
customer SMS conversation
**Maps to:** candidate **Partial Fit** to Transformation Boundaries
(`../../patterns/transformation-boundaries.md`) — not an anchor. See
Pattern Mapping below.

### Plain-Language Version (人话版)

*Added by maintainer, per protocol §9 (Accepted cases should carry
one).*

A customer had already answered a question early in an AI text
conversation. But the system only showed the AI the most recent part
of the conversation. By the time the AI needed that information
again, the earlier answer was no longer visible to it. So the AI
asked the same question again.

From the AI's point of view, the question made perfect sense. From
the customer's point of view, the system had forgotten what they had
just told it. The customer got frustrated and soon opted out of the
conversation.

Nothing was wrong with the AI's memory inside what it could see. The
problem was that we had decided what it was allowed to remember for
it.

> De-identified per `../../protocol/open-praop-v0.1-final.md` §7 —
> this incident involved an actual customer, not a self-administered
> test (unlike Cases 003, 007, and 008 from the same system). Treated
> more conservatively as a result: the customer's own message content
> is paraphrased rather than quoted, and all specific scenario
> parameters (exact loan amount, credit score, state, city, property
> type) are generalized or removed, none load-bearing to the
> mechanism.

---

### A. Basic Information

**Case title:** A Truncated Conversation Window Made the System
Re-Ask Something a Customer Had Already Answered; the Customer Soon
Opted Out
**Date:** 2026-05-15
**Domain:** AI-assisted customer-facing SMS intake, small-business
production system
**AI system involved:** A lightweight LLM handling a multi-turn
customer conversation over SMS

### B. What Were You Trying to Do?

A customer texted in with a loan inquiry, and the system conducted a
multi-turn SMS conversation to gather the details needed to route the
inquiry — including, early in the conversation, the loan purpose
(purchase vs. refinance) and other basic scenario facts. The
conversation history was passed to the LLM at each turn to maintain
context, using a fixed-size window of recent messages rather than the
full conversation.

### C. What Actually Happened?

The customer stated their loan purpose and other basic facts within
the first few turns of the conversation. Several turns later — after
enough exchange that those early turns had fallen outside the
fixed-size history window the system passed to the model — the system
asked the customer a question requesting the loan purpose again, as
if it had never been provided. From the model's point of view, this
was a reasonable question: the fact genuinely was not present anywhere
in what it could see. From the customer's point of view, they had
already answered this. The customer replied expressing frustration
that they were being asked to repeat themselves, and shortly
afterward opted out of the conversation entirely (a standard "STOP"
opt-out), ending the interaction.

### D. Why Did It Matter?

Unlike Cases 003, 007, and 008 from the same overall system (each of
which described a wrong-but-plausible outcome that a human happened to
catch before a real customer was affected), this incident directly
involved a real customer, and had a real, immediate, negative business
outcome: the customer disengaged from the conversation and opted out,
ending what may have been a legitimate lead. Nothing in the system
flagged this as an error — from every individual component's point of
view, the conversation proceeded normally: the history window was
correctly sized and correctly populated with the N most recent
messages, and the model correctly asked a sensible clarifying question
given what it could see.

### E. What Was Surprising?

The fixed conversation-history window size had been chosen for
cost-efficiency reasons — keeping the amount of conversation history
sent to the model on each turn small. But the actual per-turn cost of
including substantially more history with this class of model was
negligible; the window size was not actually constrained by a real
cost bottleneck, just an unexamined default. A cost-motivated
architectural choice, made without reference to this specific failure
mode, was immediately followed by a real customer-facing failure —
whatever savings it was chosen for were almost certainly far smaller
than the value of the lead potentially lost.

### F. What Did You Try?

The operator reviewed the conversation transcript directly and
identified that the specific facts the system re-requested had, in
fact, been stated earlier in the same conversation, in turns that had
since fallen outside the history window passed to the model at the
point of the repeated question.

### G. What Happened Afterward?

Recorded as one instance in a same-day cluster of related pipeline
issues found during a single day of concentrated testing (see Cases
003, 007, and 008 from the broker-facing side of the same system).
Fix status at the time of this write-up: not confirmed independently
in this submission — flagged as an open item rather than assumed
resolved.

### H. Evidence

Evidence retained privately: the conversation transcript, the specific
window-size configuration in effect at the time, and the specific set
of facts and turn positions that fell outside the window when the
repeated question was asked. No independently retrievable log or
transcript is attached to this submission.

### I. Interpretation

This resembles the same general shape as Cases 003, 007, and 008: a
fact that genuinely existed upstream (the customer's actual, stated
loan purpose) silently became invisible to a downstream consumer (the
model, at a later turn) without any component reporting an error. The
boundary here is different in kind from the earlier three cases,
though — it isn't a schema-to-schema translation boundary, an
enum-validation boundary, or a field-coupling boundary; it's a
*context-selection* boundary: conversation state existing in full, but
only a fixed-size recent window of it being exposed to the model at
generation time. This is interpretation, not a confirmed general
Pattern from a single instance.

### J. Anti-Mapping Question

Should this be treated as a second independent anchor for
Transformation Boundaries (whose only current Accepted anchor is Case
003 — Cases 007 and 008 Challenge it, they are not anchors), given the
shared "fact existed upstream, vanished downstream, no error reported"
shape with Case 003? The reasoning against settling this here: Case
003's mechanism is specifically a *representation/transformation*
boundary — one schema translating into another, where a concept has
nowhere to go. This case's mechanism is a *context-selection/
truncation* boundary — the same representation throughout
(conversational text), just a window-size cutoff determining what's
exposed at a given moment. Whether "any boundary where upstream fact
silently fails to reach a downstream consumer" is the right scope for
Transformation Boundaries, or whether context-truncation deserves
separate treatment, is an open classification question — treating it
as settled in either direction here would risk exactly the kind of
quiet scope-widening this project's own mapping discipline exists to
catch and flag rather than resolve unilaterally in a case write-up.

### K. What Would You Do Differently Next Time?

Treat conversation-history window sizing as a decision with a
correctness dimension, not just a cost dimension — explicitly check
whether the chosen window size can silently drop facts stated earlier
in a realistic conversation length, rather than sizing it purely for
per-turn cost. A concrete detection mechanism: track a per-conversation
"re-ask rate" — the fraction of turns that request information the
customer already provided earlier in the same conversation — and
alarm above a small threshold, rather than discovering the failure
only when a customer complains or leaves.

---

## Pattern Mapping

- Transformation Boundaries (`../../patterns/transformation-boundaries.md`) — **Partial** (shares the "upstream fact silently invisible downstream, no error" shape, but via a context-selection/truncation boundary rather than a representation/schema-translation boundary — see Anti-Mapping Question above for the open classification question this deliberately leaves unresolved)

This is the mapping discipline's first recorded use of **Partial**,
distinct from both the two existing **Supports** anchors and the two
existing **Challenges** relations (Cases 007 and 008). A clean sample
of what Partial is for: a real, non-trivial shared shape with a
Pattern's mechanism, held apart from full endorsement pending an
explicit classification question this case deliberately leaves open
rather than resolving unilaterally.

---

### Maintainer review notes

- **Real enough:** the causal chain is concrete — a customer states a
  fact early in a conversation, a fixed-size history window later
  excludes that turn, the model reasonably re-asks given what it can
  see, the customer expresses frustration and opts out shortly after.
  Passes, and is a genuinely independent incident from Cases 003/007/
  008: a different channel (customer-facing vs. broker-facing),
  different immediate mechanism (context truncation vs. schema/enum/
  coupling defects), a different affected party (a real customer), and
  a different operational consequence (direct disengagement).
- **Privacy:** treated more conservatively than Cases 003/007/008
  because it involves a real customer, not a self-administered test —
  the customer's own words are paraphrased rather than quoted, and all
  specific scenario parameters (amount, credit score, location,
  property type, exact turn count) are removed rather than merely
  generalized. Combination-risk checked and assessed as passing; given
  the real-customer involvement, a second reviewer confirming this is
  explicitly recommended, more so than for the other cases in this
  cluster.
- **Evidence:** E0 — Self-Reported. Private transcript and
  configuration evidence exist but are not attached as independently
  retrievable artifacts in this submission.
- **Fact vs. interpretation:** kept separate above (C vs. I). Causality
  around the customer's opt-out was explicitly hedged during review —
  the customer never stated the opt-out reason explicitly, so this
  case documents a strong temporal/behavioral sequence (re-ask →
  expressed frustration → opt-out), not a confirmed sole cause. Title
  and Section E were revised accordingly before Accept.
- **Anti-mapping:** credible, and the case's own Anti-Mapping Question
  correctly counts anchors — Transformation Boundaries has exactly one
  Accepted anchor (Case 003); this would be a *second* independent
  anchor if promoted, not a fourth, since Cases 007 and 008 Challenge
  the pattern rather than anchor it. An initial draft miscounted this
  and was corrected during review, precisely the kind of mistake the
  mapping discipline's Supports/Partial/Challenges vocabulary exists to
  make visible rather than let slide.
- **No duplicate incident:** confirmed independent of Cases 003, 007,
  and 008 — same overall system and testing window, but a distinct
  channel, mechanism, affected party, and consequence.
- **Plain-language check:** the original submission had no
  Plain-Language Version at all. The version above was written
  specifically to clear fresh-eye EQ without leaning on any LLM/
  context-window vocabulary — closing on the mechanism in ordinary
  terms ("we had decided what it was allowed to remember for it")
  rather than restating the technical symptom.
- **Confidence / promotion:** Transformation Boundaries stays
  `Observed / Active` with its one existing anchor (Case 003). This
  case is recorded as Partial, not Supports — it does not move the
  pattern toward `Emerging` on its own, and settling whether
  context-truncation belongs inside Transformation Boundaries' scope
  or deserves separate treatment is deliberately left open rather than
  decided here.
