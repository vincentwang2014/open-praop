# Case 008 — A Hardcoded Schema Default Silently Outranked What the Broker Actually Said

**Status:** Accepted
**Evidence level:** E0 — Self-Reported
**Date:** 2026-05-15
**Domain:** Software engineering — multi-component AI-assisted loan
intake pipeline, small-business production system (same overall system
as Cases 003 and 007)
**AI system involved:** A lightweight LLM performing natural-language
extraction as one stage of a larger pipeline
**Maps to:** no confirmed Pattern. Candidate working name "One Field
Moved On, the Other Didn't" (more formal alternative if this ever
becomes a Pattern: "Coupled Fields Can Drift Apart") — not yet reviewed
as a Pattern (one incident only). Explicitly recorded as **Challenges**
against Transformation Boundaries
(`../../patterns/transformation-boundaries.md`), not an anchor — see
Pattern Mapping below.

### Plain-Language Version (人话版)

*Added by maintainer, per protocol §9 (Accepted cases should carry
one).*

The broker clearly asked for one kind of adjustable-rate loan. The AI
actually understood that correctly in one place. But another part of
the same form was still hardcoded to an old answer. So the system
ended up saying two different things at once: "this is an
adjustable-rate loan" in one field, and "this is a 30-year fixed loan"
in another. Nothing crashed. The next system simply chose a real loan
product that made sense to it — just not the one the broker had asked
for. The problem was not that the AI failed to hear the broker. The
problem was that we updated one part of the system to listen, and
forgot that another part describing the same thing was still living
in the past.

> De-identified per `../../protocol/open-praop-v0.1-final.md` §7 — the
> business name, the third-party rate-lookup vendor, internal
> function/field names, the extraction model's specific name, the
> operator's name, and exact scenario parameters (loan amount, down
> payment, FICO, property location, citizenship/first-time-buyer
> status) not load-bearing to the mechanism have all been removed or
> generalized.

---

### A. Basic Information

**Case title:** A Hardcoded Schema Default Silently Outranked What the
Broker Actually Said
**Date:** 2026-05-15
**Domain:** Software engineering — multi-component AI-assisted loan
intake pipeline in a small-business production system
**AI system involved:** A lightweight LLM performing natural-language
extraction as one stage of a larger pipeline

### B. What Were You Trying to Do?

Same intake pipeline as Cases 003 and 007. A broker described a Jumbo
loan scenario with a specific adjustable-rate structure — a 7-year
fixed period before annual adjustment (a "7/1 ARM," distinct from other
adjustable-rate structures with different fixed periods, and distinct
from a fixed-rate loan) — expecting the system to route the request
with that exact rate structure to the rate-lookup platform.

### C. What Actually Happened?

The extraction step correctly identified the broker's stated
adjustable-rate structure in one field (a field added specifically to
capture "is this an ARM or fixed-rate loan") but a separate, related
field — meant to capture the loan's specific term/rate-structure detail
— emitted a fixed, unconditional default value that had no relationship
to what the broker actually wrote. That default value was not itself
invalid (it was a legitimate, in-vocabulary option for that field,
unlike Case 007's out-of-enum value) — it simply never changed,
regardless of input, because the extraction instructions for that
specific field had not been updated when the adjacent field was added
to capture ARM-vs-fixed status. The result was two fields describing
the same loan that contradicted each other internally: one correctly
said "adjustable rate," the other said "fixed 30-year term." The
rate-lookup platform received this internally inconsistent request,
resolved the contradiction on its own terms, and returned pricing for
a real adjustable-rate product — but with a different fixed period than
the one the broker had actually requested. A downstream validation step
checked only that the broad loan-program family matched ("Jumbo"),
which it did, so the specific-product mismatch was never flagged.

### D. Why Did It Matter?

The customer would have been quoted a real, valid loan product — just
not the one actually requested, with materially different terms (a
different period before the rate can first adjust). Nothing in the
chain flagged an error: the extraction step's own schema considered its
output complete and valid, the rate-lookup platform successfully
resolved an internally contradictory request into *something*, and the
validation step's check was too coarse-grained (loan-program family
only) to catch a mismatch at the more specific product level.

### E. What Was Surprising?

The stale field had not simply been overlooked from the start — it had
correct, working logic for a different situation, and was overridden
specifically because a *related* field had recently been improved.
Updating one half of a two-field concept (rate structure) without
updating the other half in the same change left the pair internally
inconsistent in a way that no single code review of either field in
isolation would surface — the defect only exists in the relationship
between the two fields, not in either field's own logic.

### F. What Did You Try?

The operator compared the specific request against the specific
returned result directly and noticed the rate-structure mismatch — no
automated check caught it. Diagnosis required examining the extraction
step's own field-by-field output, and separately checking whether the
prompt instructions for the stale field had been updated alongside the
related field's recent change — they had not.

### G. What Happened Afterward?

Identified same-day as one instance in a cluster of related pipeline
issues found during a single day of concentrated testing (see Cases
003 and 007, from the same source system and testing day). Fix status
at the time of this write-up: not confirmed independently in this
submission — flagged as an open item rather than assumed resolved.

### H. Evidence

Evidence retained privately: the extraction step's structured output
for this specific request, the rate-lookup platform's returned result,
and a comparison of the two related fields' extraction instructions
before and after the earlier related change. No independently
retrievable log or transcript is attached to this submission.

### I. Interpretation

This suggests a third distinct failure shape, alongside Case 003
(a concept with nowhere to go in the schema at all) and Case 007 (an
invalid, out-of-enum value defeating an absence-only safeguard): here,
the schema had a field that *could* represent the correct value, the
value it emitted was itself perfectly valid, and nothing was missing
or invalid anywhere — the field simply never listened to the actual
input, because its own extraction logic had gone stale relative to a
related field that had since changed. Candidate framing: when two
fields jointly represent one real-world concept, updating one without
updating the other in the same change leaves a hardcoded default
silently outranking real, stated evidence — not because anything
lied or fell silent, but because half of a coupled concept was frozen
in an earlier, simpler version of the schema. This is interpretation
from a single instance, not a confirmed general pattern.

### J. Anti-Mapping Question

Could this be folded into Transformation Boundaries (Case 003) or into
Case 007's candidate mechanism? Against Transformation Boundaries: that
case's mechanism is a concept with *no field to represent it at all* in
the downstream schema. Here, the field existed and successfully
emitted a value — the defect is that the value was structurally
disconnected from the actual input, not that there was nowhere for the
concept to go. Against Case 007: that case's mechanism is an *invalid*
value defeating a safeguard built only to catch absence. Here, the
emitted value was entirely valid — the failure isn't in an
enumeration/validation gap, it's in one field's extraction logic never
being wired to the same input signal a sibling field was updated to
read. If a reviewer believes "a schema field silently ignoring real
input because of stale logic" is close enough to "information failing
to cross a boundary" to be the same underlying claim, that would argue
for folding this into Transformation Boundaries instead of treating it
as distinct. The narrower claim here is specifically about two fields
representing one joint concept falling out of sync with each other
during incremental schema changes — a coupling defect, not an absence
or an invalidity.

### K. What Would You Do Differently Next Time?

When two or more fields jointly represent a single real-world concept
(here: rate-adjustment structure, split across "is it ARM" and "what's
the specific term"), treat them as a unit for change-review purposes —
any change to one field's extraction logic should trigger an explicit
check of every other field that shares its underlying concept, not just
a review of the field actually being touched. More generally: a
"default" value in an extraction schema is only safe when it's known
to be genuinely input-independent; if a field's correct value can
depend on broker-stated signal, a hardcoded default is a latent defect
waiting for exactly the related-field-updated-in-isolation scenario
that triggered this incident.

---

## Pattern Mapping

- Transformation Boundaries (`../../patterns/transformation-boundaries.md`) — **Challenges** (considered and rejected as a fit — the field existed and emitted a valid value, unlike Case 003's missing-field mechanism)

This is the mapping discipline's second recorded use of **Challenges**,
alongside Case 007. Together the two show the discipline doing real
work: neither case is discarded as noise, and each one narrows what
Transformation Boundaries actually claims by marking what it does
*not* cover. That boundary-drawing effect — not just "which cases
support X" but "which cases were seriously considered and didn't fit,
and why" — is exactly what makes this mapping useful for future
retrieval, not just bookkeeping.

---

### Maintainer review notes

- **Real enough:** the causal chain is concrete — one field correctly
  captures the broker's ARM-vs-fixed signal, a sibling field describing
  the same real-world concept still emits an unconditional stale
  default, the two fields end up internally contradictory, the
  downstream platform resolves the contradiction on its own terms and
  returns a real but wrong product, and a coarse-grained validator
  (checking only the broad loan-program family) never flags it. Passes.
- **Privacy:** business name, vendor, specific model, internal
  function/field names, operator, and specific borrower/scenario
  parameters are all removed or generalized. "Jumbo" and "7/1 ARM"
  remain only as standard mortgage-industry terminology needed to
  understand the mechanism. Combination-risk checked: the remaining
  architecture is consistent with (and no more specific than) Cases 003
  and 007 from the same underlying system — no customer, employee,
  vendor, or code-level identifier remains.
- **Evidence:** E0 — Self-Reported is accurate. Private evidence exists
  (the extraction output, the returned result, a before/after
  comparison of the two fields' extraction instructions) but none of it
  is attached as independently retrievable evidence in this submission.
- **Fact vs. interpretation:** kept separate above (C vs. I) — the
  candidate framing ("a coupling/schema-evolution defect, not an
  absence or an invalidity") is explicitly flagged as single-instance
  interpretation, not a confirmed Pattern.
- **Anti-mapping:** credible, and substantively different from both
  existing neighbors. Against Case 003: the field existed and emitted a
  value at all, unlike Case 003's missing-field mechanism. Against Case
  007: the emitted value was entirely valid, unlike Case 007's
  out-of-enum value defeating an absence-only fallback. The output was
  even internally self-contradictory here (one field said ARM, the
  other said fixed) — a distinct symptom from either neighbor.
- **No duplicate incident:** shares a system and a testing day with
  Cases 003 and 007, but is a third distinct underlying defect, not a
  repeat manifestation of either.
- **Plain-language check:** the submission's own technical prose is
  clear but assumes schema/field vocabulary a non-technical reader
  wouldn't have — it does not pass Layer-1 Renhua/EQ on its own. The
  Plain-Language Version above was written to actually clear that bar,
  in particular closing on the mechanism rather than the symptom: *the
  problem was not that the AI failed to hear the broker; it's that one
  part of the system was updated to listen, and the other, describing
  the same thing, was left behind.* Whether it clears the *harder*
  Layer-2 test (unprompted recognition in a new, unrelated situation —
  e.g. a CRM adding a preferred-contact-method field while an old
  phone-required default goes unchanged, or a workflow system updating
  one status field while a derived sibling field keeps an old default)
  can only be shown by that recognition actually happening later, not
  asserted here.
- **Confidence / promotion:** deliberately not naming a formal Pattern
  yet — one incident, however cleanly it demonstrates the mechanism,
  isn't sufficient per §10. Revisit if a genuinely independent,
  cross-domain instance of "two fields jointly describing one concept
  drifting out of sync during incremental schema changes" turns up.
