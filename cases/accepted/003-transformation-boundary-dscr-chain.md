# Case 003 — Transformation Boundaries: Silent Semantic Drift Across a Multi-Layer Extraction Chain

**Status:** Accepted
**Evidence level:** E0 — Self-Reported
**Date:** 2026-05-13 (discovery); underlying occurrences from 2026-05-07
**Domain:** Software engineering (multi-component AI-assisted intake
pipeline, small-business production system)
**AI system involved:** A lightweight LLM used for natural-language
extraction (one stage of a multi-stage pipeline); a separate coding
agent diagnosed the incident after the fact.
**Maps to:** `../../patterns/transformation-boundaries.md` (Observed /
Active) — this is its anchor case

### Plain-Language Version (人话版)

*Added by maintainer, per protocol §9 (Accepted cases should carry
one).*

A customer clearly stated an important fact about the kind of loan
they wanted. The step that first read the message understood it fine
— but by the time the request reached the final pricing step, that
fact had quietly vanished, and nobody's own checks ever caught it,
because each step only checked that its own answer looked complete,
not that it still matched what the customer actually said. The system
confidently returned a full, professional-looking quote — just for the
wrong kind of loan.

> De-identified per `../../protocol/open-praop-v0.1-final.md` §7 —
> the business name, the third-party rate-lookup vendor, the messaging
> platform/vendor, the operator's name, internal file paths, commit
> hashes, and internal task IDs have all been removed or generalized;
> the failure mechanism, timeline, and cause/effect chain are
> unchanged.

---

### A. Basic Information

**Case title:** Silent Semantic Drift Across a Multi-Layer Extraction
Chain
**Date:** 2026-05-13 (discovered); occurred 2026-05-07 through 2026-05-13
**Domain:** Software engineering — multi-component AI-assisted intake
pipeline in a small-business production system
**AI system involved:** A lightweight LLM performing natural-language
extraction as one stage of a larger pipeline; a coding agent that
diagnosed the incident afterward by directly querying production logs

### B. What Were You Trying to Do?

The system accepted natural-language loan inquiries through a
chat-based intake channel, used an LLM to extract structured loan
details from the free-text message, normalized the extracted data into
an internal schema, and passed the result to a third-party rate-lookup
platform to return pricing. The operator sent a routine test message
describing a loan scenario that should have been classified under a
specific loan-qualification type — DSCR (debt-service-coverage-ratio)
underwriting, an income-verification method distinct from standard
W-2/paystub underwriting, commonly used for investment-property loans —
for an investment property, expecting the system to route it to the
matching loan program and pricing.

### C. What Actually Happened?

Every individual component in the chain succeeded. The extraction step
returned valid, schema-conforming JSON. The normalization step returned
a valid, well-formed object. The rate-lookup step filled all required
fields and returned a full set of priced rate options. The messaging
webhook delivered its response successfully. Nothing errored, nothing
timed out, nothing was flagged by any component's own checks.

But the DSCR qualification the operator had explicitly stated in the
message was silently dropped at the extraction step, because the
extraction schema had no field to represent it — the extractor could
only classify the loan under a standard, unrelated program. The next
layer (normalization) had a fallback rule already written to catch
this exact qualification type given one particular input signal, but
that layer read a different, related-but-distinct signal that the
extractor never actually produced — an independent, narrower vocabulary
mismatch stacked on top of the first. Neither layer flagged anything as
uncertain, because from each layer's own local point of view, its
output was a valid, well-formed instance of its own contract. The final
rate-lookup step received this now-wrong-but-plausible request and
returned a complete, professional-looking result — for a real, common
loan product, just not the one the operator had actually described.

### D. Why Did It Matter?

For a six-day window, every message from the same intake channel
silently misclassified the same category of loan request, while a
second, parallel intake channel (a manual form used for administrative
testing) handled the identical qualification type correctly on every
occurrence. The mismatch never once produced a distinguishable error, a
failed request, or an obviously wrong-looking output — the returned
rate sheets were fully valid for the (wrong) product they described.
Had a real customer been quoted from one of the affected messages, the
quote would have been materially wrong: the two loan products this
mechanism could confuse typically differ in pricing by roughly one to
two percentage points. No customer was actually affected — the operator
caught the issue via his own test message before the affected channel
was opened to real customers — but the exposure window was real
(six days, multiple silent recurrences), and the mechanism would recur
for any future user of that same channel until fixed.

### E. What Was Surprising?

The operator's own first read of the failure — a plausible guess that
the system had reused a stale result, or that a follow-up message
hadn't parsed correctly — was reasonable and partially correct, but
pointed at surface symptoms rather than the actual mechanism.
Correctly diagnosing it required directly querying production logs
across three separate services and cross-referencing them; no single
symptom, taken alone, pointed at "a concept silently dropped three
layers upstream." Also surprising: the normalization layer's fallback
rule had *already* been written to handle this exact qualification
type via one specific signal — but the upstream extraction layer never
actually produced that signal, because its own schema had no field for
it. The two layers had drifted out of sync with each other without
either side's own tests ever catching it.

### F. What Did You Try?

The operator's own initial hypotheses (stale-result reuse; a
follow-up-message parsing bug) were tested and only partially explained
the observed behavior. Correctly diagnosing the actual mechanism
required a coding agent to directly pull raw request logs from the
messaging webhook, background-worker logs from the rate-lookup
integration, and a direct query against the production data store —
cross-referencing all three rather than trusting any single layer's own
reported status.

### G. What Happened Afterward?

Root-caused to three independently-insufficient layers — an extraction
schema missing a field for the qualification type in question; a
normalization fallback rule reading the wrong of two related-but-distinct
input signals; and no cross-check step anywhere that compared the
original message text against the final extracted result — plus one
structural cause behind why it went undetected for six days: the
affected intake channel was deliberately exercised less often in
testing than the administrative channel, because triggering the
third-party rate-lookup service too frequently risked a rate-limiting
condition on that account. That unrelated operational precaution had
the side effect of suppressing exactly the test coverage that would
have caught this. A fix was scoped across all three layers plus a new
cross-check step; the first phase (routing both intake channels through
one shared underlying pipeline, so future fixes land once for both) had
already shipped as of this write-up; the remainder was in progress.

### H. Evidence

Evidence retained privately: production webhook logs, background-worker
fill logs, and a direct production data-store query, all
cross-referenced by the coding agent that diagnosed the incident. No
independently retrievable log or transcript is attached to this
submission.

### I. Interpretation

This resembles a "transformation boundary" failure shape: whenever
information crosses from one representation to another — free text to
structured data, one internal schema to another, structured data to a
third-party system's own field set — semantics can be silently lost or
changed even when both sides of that specific boundary look locally
correct. This is one of (per private source material) at least three
independently-observed instances of the same shape within a short
window, suggesting a candidate Pattern rather than a one-off bug. This
is interpretation, not a confirmed general pattern — the fuller
Pattern write-up should be judged on its own evidence, separately from
this one case.

### J. Anti-Mapping Question

Why might this not deserve its own pattern, or be explained more
simply? Each individual layer's failure — a missing schema field; a
fallback rule reading the wrong signal — is, on its own, an ordinary,
unremarkable software bug, the kind ordinary code review or better unit
coverage might have caught given enough attention. The specific,
narrower claim being made is that *no single layer's own unit-level
correctness check could have caught this* — every layer's own tests
passed, and the failure was only visible by comparing across the
boundary, not by testing either side more thoroughly in isolation. If a
reviewer believes ordinary integration testing (rather than a
boundary-specific semantic comparison) would have caught this just as
reliably, that would weaken the claim that this is a distinct pattern
rather than plain insufficient integration testing.

### K. What Would You Do Differently Next Time?

Treat cross-layer vocabulary consistency as something checked
explicitly and periodically — a schema-diff-style audit: for every pair
of adjacent layers, does every value one layer's schema can express
have somewhere to go in the next layer's schema, and vice versa? —
rather than something only checked once a symptom happens to surface.
Separately: an operational precaution adopted for an unrelated reason
(avoiding a rate-limit condition on a third-party integration) had the
unexamined side effect of suppressing test coverage on exactly the
intake channel most likely to expose a schema gap. Worth asking
explicitly, whenever a testing shortcut is adopted for
operational-cost reasons, exactly which paths that shortcut leaves
untested.

---

## Pattern Mapping

- Transformation Boundaries (`patterns/transformation-boundaries.md`) — Supports (Primary anchor)

---

### Maintainer review notes

- **Real enough:** firsthand, contemporaneous incident with a concrete
  six-day window and a specific cause/effect chain across three named
  layers. Passes.
- **Privacy:** de-identified per protocol §7 — vendor, business,
  messaging platform, operator name, file paths, commit hashes, and
  task IDs all removed or generalized. "DSCR" kept as a standard,
  publicly-documented mortgage-industry term, not a distinguishing
  detail. Combination-risk checked and assessed as passing — the
  remaining architecture (LLM chat intake + third-party rate lookup +
  DSCR misclassification) describes a common pattern in this space, not
  a distinguishing one.
- **Fact vs. interpretation:** kept separate above (C vs. I) — the
  narrower claim (no single layer's own unit-level test could have
  caught this) is explicitly distinguished from the broader
  interpretation (a general "transformation boundary" mechanism).
- **Evidence:** E0. Diagnosis was cross-referenced across three
  production log sources by a coding agent, which is more rigorous than
  a bare self-report, but no artifact is attached to this submission —
  evidence level tracks attachment, not narrative quality.
- **Mapping:** New pattern candidate, **Transformation Boundaries**.
  Anti-mapping question is credible and specific (distinguishes from
  "just needed better integration tests").
- **Confidence:** Case accepted; the pattern now exists at
  `../../patterns/transformation-boundaries.md`, `Observed / Active`
  with this case as its anchor. Per §10, it stays at `Observed` with
  exactly one Accepted anchor, regardless of the source material's
  original claim of two further independently-observed instances —
  one of those (Case 009) has since been formally submitted and
  Accepted, but as a Partial fit, not a second anchor; see Case 009 and
  this pattern's own Related Cases section.
