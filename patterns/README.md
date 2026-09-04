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

## Current patterns

| Pattern | Confidence / Status | Anchor case(s) | Note |
|---|---|---|---|
| Control Accretion | Observed / Active | Case 004 | source case actually proposes 5 overlapping candidate shapes; this is the primary name, not a settled taxonomy |
| Lesson-Generalization Failure | Observed / Active | Case 003 | may fold into a broader "self-knowledge ≠ enforcement" category if a second instance turns out to be same-direction repetition rather than direction-flipping |

Both patterns are capped at `Observed` because each has exactly one
anchor case. Per §10, `Emerging` requires that anchor *plus* additional
independent evidence or a second underlying incident — a well-written,
compelling single case does not clear that bar on its own.
