# Case 007 — A Confidently Wrong Loan-Program Value Bypassed the Safeguard Built to Catch a Missing One

**Status:** Accepted
**Evidence level:** E0 — Self-Reported
**Date:** 2026-05-15
**Domain:** Software engineering — multi-component AI-assisted loan
intake pipeline, small-business production system (same overall system
as Case 003)
**AI system involved:** A lightweight LLM performing natural-language
extraction as one stage of a larger pipeline
**Maps to:** no confirmed Pattern. Candidate working name "Fallback
Only Guards Against Silence, Not Lies" — not yet reviewed as a Pattern
(one incident only). Explicitly recorded as **Challenges** against
Transformation Boundaries (`../../patterns/transformation-boundaries.md`),
not an anchor — see Pattern Mapping below.

### Plain-Language Version (人话版)

*Added by maintainer, per protocol §9 (Accepted cases should carry
one).*

An extraction step produced a loan-program value that wasn't one of
the fixed options its own instructions allowed — not a missing value,
an invented one. A fallback rule existed specifically to fix wrong
loan-program values, but it only ever checked for a *missing* value,
so it never triggered. The invalid value sailed through untouched, and
the system returned a complete, polished quote for the wrong loan
program. The lesson isn't "another pipeline bug" — it's that a
safeguard built to catch silence provides zero protection against a
confident, present, wrong answer.

> De-identified per `../../protocol/open-praop-v0.1-final.md` §7 — the
> business name, the third-party rate-lookup vendor, internal
> function/field names, the extraction model's specific name, the
> operator's name, and exact scenario parameters (loan amount, FICO,
> property location, DTI, reserves, lock period) not load-bearing to
> the mechanism have all been removed or generalized.

---

### A. Basic Information

**Case title:** A Confidently Wrong Loan-Program Value Bypassed the
Safeguard Built to Catch a Missing One
**Date:** 2026-05-15
**Domain:** Software engineering — multi-component AI-assisted loan
intake pipeline in a small-business production system
**AI system involved:** A lightweight LLM performing natural-language
extraction as one stage of a larger pipeline

### B. What Were You Trying to Do?

Same intake pipeline as Case 003: a broker's free-text loan scenario
gets extracted into structured fields by an LLM, normalized into an
internal schema, and passed to a third-party rate-lookup platform for
pricing. A broker described a scenario intended to qualify under a
Bank Statement income-verification program (a documentation type where
self-employed borrowers qualify using bank deposits instead of tax
returns, distinct from standard W-2 underwriting), expecting the
system to route it to that program and return matching pricing.

### C. What Actually Happened?

The extraction step correctly identified the income-verification type
as bank-statement-based in one field, but in a separate field meant to
carry the overall loan-program classification, it emitted a value that
was not one of the fixed set of values ("conventional," "FHA," "VA,"
"jumbo," "expanded guidelines," or null) its own prompt specification
allowed it to produce — an invented, out-of-vocabulary value not
present in that fixed set. The normalization layer's fallback logic —
already built, from an earlier fix to a related issue, to derive the
correct loan program from the income-verification-type field whenever
the primary loan-program field was empty — never activated, because
its trigger condition was "the primary field is empty," and the
invented value was not empty; it was simply wrong. The invented value
propagated unchanged to the rate-lookup step, which did not recognize
it, fell back to its own default panel, and returned a complete,
professional-looking set of rates for a standard program — not the
Bank Statement program the broker had actually described. Nothing
errored anywhere in the chain.

### D. Why Did It Matter?

The returned rate sheet was fully valid for the program it described,
just not the one the broker asked about — the same "confident, wrong,
undetected" shape as Case 003, but reached through a different
mechanism. The operator caught the mismatch by comparing the request
against the result directly; no system component flagged anything. Had
this gone to an actual customer scenario without a human comparing
input to output, the customer would have been quoted for the wrong
loan program.

### E. What Was Surprising?

The fallback logic that should have provided a second chance to get
this right had, in fact, already been correctly built to consult the
right field — it had been fixed once before, for a related but
distinct instance of the same broader problem, earlier the same day.
That fix was real and correctly targeted, and it still didn't help
here, because it only activated on missing information, not on
confidently wrong information. A safeguard can be entirely correctly
built for the failure mode it was designed for and still provide zero
protection against a closely-related failure mode one inference away.

### F. What Did You Try?

The operator reviewed the specific request against the specific
returned result directly and noticed the mismatch (a Bank Statement
scenario returning a Conforming/standard-program rate sheet) — no
automated check surfaced it. Diagnosis required tracing the value from
the extraction step's own output through the normalization layer's
decision logic to establish that the invented value, not a missing
one, was what defeated the fallback.

### G. What Happened Afterward?

Identified same-day as one instance in a cluster of related pipeline
issues found during a single day of concentrated testing. Fix status
at the time of this write-up: not confirmed independently in this
submission — flagged as an open item rather than assumed resolved.

### H. Evidence

Evidence retained privately: the extraction step's structured output
for this specific request, the normalization layer's decision trace,
and the rate-lookup platform's returned result, all reviewed directly
by the operator. No independently retrievable log or transcript is
attached to this submission.

### I. Interpretation

This suggests a distinct failure shape from silent field-dropping (the
Transformation Boundary mechanism): here, the extraction step did not
stay silent about the field in question — it confidently produced a
value, just an invalid one. A safeguard built on the assumption "if
this is wrong, the field will be empty" has no coverage for "this is
wrong and non-empty." Candidate framing: a downstream safeguard that
only checks for absence provides no protection against a confident,
present-but-invalid value — a fallback built to catch silence provides
no defense against a lie. This is interpretation from a single
instance, not a confirmed general pattern.

### J. Anti-Mapping Question

Could this just be folded into the Transformation Boundary pattern,
since both involve the same overall pipeline and both result in a
confidently wrong, undetected outcome? The specific, narrower
distinction: Case 003's mechanism is information silently failing to
cross a representation boundary at all — a concept present in the
input has nowhere to go in the downstream schema, and nothing carries
it forward. This case's mechanism is different — the information did
cross the boundary, as an actively wrong value the extractor was never
supposed to be able to produce in the first place, and the safeguard
designed to catch a *different* failure mode (a missing value) had no
logic path for catching an *invalid-but-present* one. If a reviewer
believes both mechanisms reduce to "the extraction step got a field
wrong" at a level general enough to be the same claim, that would argue
against treating this as distinct from Transformation Boundaries. The
narrower claim here is that "missingness" and "confident invalidity"
are different failure shapes requiring different defenses, not the
same shape at different severities.

### K. What Would You Do Differently Next Time?

Any fallback or safeguard logic that assumes "the failure mode looks
like an empty/null value" should be explicitly tested against "the
failure mode looks like a present-but-invalid value" as a distinct
case, not assumed covered by the same trigger condition. More
generally: when an extraction step has a fixed, enumerated set of
valid outputs, validate the actual output against that set explicitly,
rather than trusting that an invalid value simply won't occur because
the prompt specified the allowed set.

---

## Pattern Mapping

- Transformation Boundaries (`../../patterns/transformation-boundaries.md`) — **Challenges** (considered and rejected as a fit — Case 003's mechanism is information silently failing to cross a boundary at all; this case's mechanism is a confidently-wrong present value defeating a fallback built only for absence. Same source system, same-day cluster, different underlying failure shape.)

This is the mapping discipline's first recorded use of **Challenges**:
not "the Pattern is wrong," but "this case was seriously considered for
the Pattern and, after Anti-Mapping, judged not to fit — and here is
why." Recording a considered non-fit has falsification value and
guards against Pattern scope creep, the same way an anchor guards
against unfounded promotion.

---

### Maintainer review notes

- **Real enough:** the causal chain is concrete and fully traceable —
  the extractor emits an out-of-enum value in a fixed field, the
  fallback's trigger condition (empty field) never fires because the
  value is present-but-invalid, the invalid value propagates unchanged
  to the rate-lookup step, which falls back to its own default panel
  and returns a complete, wrong-program quote with no error anywhere in
  the chain. Passes.
- **Privacy:** business name, vendor, specific model, internal
  function/field names, operator, and specific borrower/scenario
  parameters are all removed or generalized. "Bank Statement," "FHA,"
  "VA," and similar remain only as generic mortgage-industry
  terminology needed to understand the mechanism. Combination-risk
  checked: the remaining architecture (LLM extraction + normalization +
  fallback + third-party pricing) is not distinctive enough within
  mortgage-tech to identify a specific business, and no customer,
  employee, vendor, or code-level identifier remains.
- **Evidence:** E0 — Self-Reported is appropriate. Private structured
  output, a decision trace, and the returned result all exist, but none
  are attached as independently retrievable evidence in this
  submission, so the evidence level is not inflated.
- **Fact vs. interpretation:** kept separate above (C vs. I) — the
  interpretation ("a fallback built to catch silence provides no
  defense against a lie") is explicitly flagged as single-instance,
  not a confirmed Pattern.
- **Anti-mapping:** credible. Case 003 is "semantic content failed to
  cross a transformation boundary at all"; this case is "a value did
  cross, but it was invalid and non-empty, defeating a safeguard built
  only to catch missingness." Different causal chains, not the same
  mechanism at different severities.
- **No duplicate incident:** shares a system and a testing day with
  Case 003, but is not a repeat manifestation of the same underlying
  defect — a new request, a new immediate cause, and a new safeguard
  failure path, explicitly documented as one instance in a same-day
  cluster of otherwise-independent issues.
- **Confidence / promotion:** deliberately not naming a formal Pattern
  yet. The candidate mechanism — safeguard coverage for absence does
  not imply safeguard coverage for invalid-but-present values — is
  well-articulated by this single case, but one incident is not
  sufficient grounds per §10 regardless of how clean the mechanism
  reads. Revisit if a genuinely independent, cross-domain instance
  turns up (e.g. an agent field validator, an API parser, RAG metadata,
  or workflow-state handling exhibiting the same shape).
