# Patterns

A Pattern answers: **does the same failure or success shape recur across
cases?**

A pattern doesn't exist because it has a good name — it must grow out of
cases. Every pattern here must be traceable to at least one `Accepted`
case (§10 Anchor-or-Demote of the protocol); if the anchor can't be
named, the claim gets demoted, no matter how well it reads.

Confidence and Status are tracked on two independent axes — see §9 of
`../protocol/open-praop-v0.1-final.md`:

- **Confidence:** Observed → Emerging → Operational → Canonical
- **Status:** Active / Contested / Deprecated

Every pattern entry also carries a **Plain-Language Version (人话版)** —
the Renhua principle in §3: if the person who owns the consequence can't
get the point in ordinary language, the pattern hasn't passed the EDTCU
Test yet, no matter how precise the formal definition is.

## Current patterns

| Pattern | Confidence / Status | Anchor case(s) | Note |
|---|---|---|---|
| Lesson-Generalization Failure | Observed / Active | Case 001 | may fold into a broader "self-knowledge ≠ enforcement" category if a second instance turns out to be same-direction repetition rather than direction-flipping |
| Control Accretion | Observed / Active | Case 002 | source case actually proposes 5 overlapping candidate shapes; this is the primary name, not a settled taxonomy |
| Transformation Boundaries | Observed / Active | Case 003 | at least 2 further independently-observed instances are known from private source material but not yet independently submitted/Accepted |
| Symbolic Success ≠ Operational Correctness | Observed / Active | Case 004 | this is a *fourth* independently-observed incident of the same shape (3 more known, see `../PLAIN_LANGUAGE_GUIDE.md` Entry 2) — unusually well-evidenced for `Observed`, but none of the other 3 have been formally submitted/Accepted yet |
| Trajectory Lock | Observed / Active | Case 005 | anchor case itself describes 2 incidents (primary + a same-week independent one); whether the second counts toward `Emerging` on its own is an open question flagged for maintainer decision — see the pattern file |
| Visibility Is Influence | Observed / Active | Case 006 | a second, independent-environment incident is known (see `../PLAIN_LANGUAGE_GUIDE.md` Entry 1) but not yet independently submitted/Accepted |

All six patterns are capped at `Observed` because each has exactly one
*Accepted* anchor case. Per §10, `Emerging` requires that anchor *plus*
additional independent evidence or a second underlying incident — a
well-written, compelling single case does not clear that bar on its
own, and unsubmitted source material (however credible) does not count
until it has itself gone through Maintainer Review and Case Admission.

## Case ↔ Pattern mapping is many-to-many

One Case can relate to several Patterns (the same incident is often
legible through more than one lens); one Pattern is often eventually
supported by several Cases. This has already happened informally more
than once in this corpus (see `../PLAIN_LANGUAGE_GUIDE.md` Entry 3,
which explicitly shares its case anchor with Entry 2 rather than
inventing a second one) — this section formalizes recording it, rather
than relying on memory or re-reading files to reconstruct the
relationship later.

**Relation vocabulary (kept deliberately small):**

- **Supports** — the case is genuine evidence for the pattern.
- **Partial** — related, but only a partial fit; doesn't fully
  establish the mechanism.
- **Challenges** — the case was considered and doesn't fit, or argues
  against the pattern as framed. Recording a considered non-fit has
  falsification value; it isn't a rejected/deleted relation.

**Which side is authoritative:** a Pattern file's own `## Case Anchors`
section is the authoritative record of which Cases actually count as
its evidence — that's a maintainer/theory judgment, not something a
Case gets to declare for itself. A Case file's own `## Pattern Mapping`
section only records *candidate* relations (what the case's author or
reviewer thinks it might relate to); it does not itself make a case an
anchor. The two are not filled in symmetrically, and that's
deliberate — don't hand-maintain both sides as equally authoritative,
or they will drift.

**Always cite a Pattern by both its display name and its file link**
(e.g. `Symbolic Success ≠ Operational Correctness
(patterns/symbolic-success.md)`), never the display name alone. The
filename is already each Pattern's stable identity — this costs
nothing extra now and is the one thing that would be genuinely
expensive to clean up later if display-name spelling drifts across a
larger corpus (the actual cost in a future RAG/graph-DB migration is
entity resolution on inconsistent names, not the choice of Markdown
over YAML — converting these bullet lists into structured relations
later is a small, one-time parsing script either way).

Every Pattern file should carry:

```markdown
## Case Anchors

- Case NNN — Primary anchor

## Related Cases

- Case NNN — Partial (or: not yet Accepted, if it's known source
  material that hasn't gone through Case Admission yet)
```

Every accepted Case file should carry:

```markdown
## Pattern Mapping

- <Pattern Name> (`patterns/<slug>.md`) — Supports / Partial /
  Challenges (candidate; the Pattern file's own Case Anchors section
  is authoritative)
```
