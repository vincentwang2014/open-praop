# Public Matcher Pack Schema

**Schema version:** `1`
**Normative owner:** Open PRAOP (see `../protocol/open-praop-v0.1-final.en.md` §21.2)
**Status:** Schema definition only. No generation tooling exists yet —
see `README.md` in this directory.

This file is the canonical field-by-field definition referenced by
protocol §21.2. If this file and the protocol disagree, the protocol
governs.

## Pack-level fields (once per pack file)

| Field | Required | Meaning |
|---|---|---|
| `schema_version` | yes | Version of *this* schema the pack conforms to. String, not a number, so `"1"` and `"1.0"` are never silently conflated. |
| `corpus_revision` | yes | Commit hash or release tag of the `open-praop` state this pack reflects. |
| `generated_at` | yes | ISO-8601 UTC timestamp of when the pack was produced or hand-assembled. |
| `source_commit` | yes | Same as `corpus_revision` when generated directly from a commit; kept separate in case a future release process diverges. |
| `content_digest` | recommended | A digest of the pack's own mechanism entries, so a consumer can detect silent tampering or corruption in transit. Optional while packs are hand-authored and distributed only via direct git clone. |
| `mechanisms` | yes | List of mechanism entries, one per Pattern. |

## Mechanism entry fields (one per Pattern)

| Field | Required | Meaning |
|---|---|---|
| `mechanism_id` | yes | Stable identifier, `pattern.<kebab-case-slug>`, matching the Pattern file's own name. |
| `name` | yes | Human-readable Pattern title, exactly as it appears in the Pattern's own `# Pattern: <name>` heading. |
| `aliases` | no | Alternative names or phrasings a contributor might use for the same mechanism. |
| `mechanism.trigger` | yes | The condition that sets the mechanism in motion. |
| `mechanism.substitution` | no | What gets substituted or overridden, if the mechanism has that shape (not every mechanism does). |
| `mechanism.failure_shape` | yes | The concrete, observable shape the failure takes. |
| `observed_directions` | yes | Failure direction(s) actually documented in an Accepted anchor case. |
| `possible_directions` | no | Related failure direction(s) that are a plausible risk but not yet confirmed by any Accepted anchor — must not be conflated with `observed_directions`. |
| `watch_for` | no | Concrete signals that suggest this mechanism may be present. |
| `anti_mapping` | yes | At least one concrete situation this mechanism must **not** be used to explain, drawn from the Pattern file's own "Why X and not Y" section. |
| `accepted_case_anchors` | yes | List of `{case_id, incident_cluster_id?}`. Every entry must point to a Case already in `Accepted` status per protocol §9 — never `Submitted` or `Reviewing`. |
| `confidence` | yes | Copied verbatim from the Pattern file's own `**Confidence / Status:**` line. Never independently re-assessed when building the pack. |
| `status` | yes | Same source and same rule as `confidence`. |

## Rules that follow from protocol §21

1. A pack is a reflection of the corpus, not a second source of truth for it. Every `confidence`/`status`/`accepted_case_anchors` value must trace back to the referenced Pattern and Case files as they exist at `corpus_revision` — see protocol §21.2, "must not become a separately hand-maintained doctrine source."
2. `observed_directions` vs. `possible_directions` must stay separate — collapsing them would let an unverified hypothesis read as confirmed, which is exactly what protocol §21.4 (local non-match creates no obligation) exists to prevent one layer up.
3. `accepted_case_anchors` entries referencing more than one anchor from the same underlying incident must carry the same `incident_cluster_id` (protocol §21.5) — a pack must never present clustered manifestations of one incident as independent anchors.
4. This schema says nothing about how matching itself is performed (string comparison, embeddings, manual reading, or otherwise) — that is implementation-side, per protocol §21.1, and out of scope for this document.
