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
| Control Accretion | Observed / Active | Case 004 | source case actually proposes 5 overlapping candidate shapes; this is the primary name, not a settled taxonomy |
| Lesson-Generalization Failure | Observed / Active | Case 003 | may fold into a broader "self-knowledge ≠ enforcement" category if a second instance turns out to be same-direction repetition rather than direction-flipping |
| Transformation Boundaries | Observed / Active | Case 005 | at least 2 further independently-observed instances are known from private source material but not yet independently submitted/Accepted |
| Symbolic Success ≠ Operational Correctness | Observed / Active | Case 006 | this is a *fourth* independently-observed incident of the same shape (3 more known, see `../PLAIN_LANGUAGE_GUIDE.md` Entry 2) — unusually well-evidenced for `Observed`, but none of the other 3 have been formally submitted/Accepted yet |
| Trajectory Lock | Observed / Active | Case 007 | anchor case itself describes 2 incidents (primary + a same-week independent one); whether the second counts toward `Emerging` on its own is an open question flagged for maintainer decision — see the pattern file |

All five patterns are capped at `Observed` because each has exactly one
*Accepted* anchor case. Per §10, `Emerging` requires that anchor *plus*
additional independent evidence or a second underlying incident — a
well-written, compelling single case does not clear that bar on its
own, and unsubmitted source material (however credible) does not count
until it has itself gone through Maintainer Review and Case Admission.
