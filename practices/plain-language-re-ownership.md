# Practice: Plain-Language Re-Ownership

**Confidence / Status:** Observed / Active
**Enforcement Level:** Guidance
**Anchor case(s):** `../cases/accepted/010-semantic-ownership-loss-prao-genesis.md`

### Plain-Language Version (人话版)

This isn't about getting the AI to explain it more simply. It's about
the person who's actually accountable stepping away from the AI's own
wording and saying, in their own words, what it actually means. If
they can't, it isn't understood yet — no matter how clear the AI's
version sounded going in.

### Problem Addressed

Semantic Ownership Loss — the accountable human remains the nominal
owner or reviewer of an AI-produced artifact, doctrine, or body of
terminology, but can no longer independently explain, challenge, or
reconstruct it. Verification quietly shifts from actual understanding
to a proxy for it: AI-AI agreement, fluent presentation, or the
material simply sounding coherent.

### When to Use

Any consequential AI-produced doctrine, terminology, architecture, or
conceptual discussion where a human is expected to remain the
accountable owner or approver — not routine, inconsequential exchanges
where nothing is being decided or built on top of.

### What to Do

1. Before treating AI-produced doctrine, terminology, or an
   architectural decision as adopted, require the accountable human to
   restate what it means in language they can independently explain
   and challenge — not merely confirm that they read or agreed with
   it.
2. If the AI proposes a term or formulation and the accountable human
   cannot independently restate what it means, reject it — even if it
   is accurate — and ask for or produce another. Keep rejecting
   successive proposals until the human reaches a formulation in their
   own words, rather than stopping at the first fluent-sounding
   candidate.
3. Treat two AI systems agreeing as evidence only that the systems
   agree or share a framing. Do not treat that agreement as evidence
   that the material is correct or that the accountable human has
   independently verified it.

### What Not to Do

- Don't accept "the AI explained it clearly and it sounded right" as
  equivalent to independent understanding.
- Don't treat a close paraphrase of the AI's own phrasing as
  automatically equivalent to independent restatement — but don't treat
  it as automatic failure either (see Known Limitations: this practice
  doesn't yet have a reliable test for the difference). Flag it as
  unresolved rather than assuming either direction.
- Don't apply this only to the first draft of a doctrine/term and skip
  it on later revisions — the anchor case's own recurrence (the
  mechanism reappearing after a countermeasure already existed) shows
  the gap can reopen later in the same workstream.

### Evidence

- Case 010 (`../cases/accepted/010-semantic-ownership-loss-prao-genesis.md`) — 1 anchor, E0. The same case also documents, as a distinct
  successful-defense episode (not a second incident), a positive
  observation consistent with the Practice working: an AI proposed two
  successively-refined candidate terms, the accountable human rejected
  both because they still centered on authority rather than
  understanding, and landed on his own plain-language formulation
  instead.

### Known Limitations

Untested against a second instance. This Practice does not yet provide
a reliable test for distinguishing independent reconstruction from a
close paraphrase of AI-supplied wording. Until that boundary is
supported by further evidence, a close paraphrase should be recorded
as unresolved — not automatically treated as either successful
re-ownership or failure. Also doesn't specify who judges restatement
quality when the accountable human and the only reviewer are the same
person — a self-assessment risk this practice doesn't yet guard
against.

Cost / friction: This Practice can slow adoption, require repeated
rewriting, and cause an accurate term to be rejected before an
independently usable formulation is reached. That cost may be
disproportionate for low-consequence work, which is why the Practice
is limited to consequential material.

### Enforcement Level

**Guidance.** Every instance in the anchor case was a deliberate,
manual choice by the accountable human (asking for a plain-language
layer, rejecting proposed terms) — not enforced by any tool, checklist,
or process gate. No mechanical version exists yet.

### Confidence

**Observed / Active.** Per §10 of the protocol, cannot be promoted to
Emerging without either additional independent supporting evidence or
a second underlying incident.
