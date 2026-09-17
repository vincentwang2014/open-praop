# Public Matcher Pack

A matcher pack packages Open PRAOP's public knowledge — Pattern
mechanisms, aliases, anti-mappings, and Accepted Case anchors — so an
implementation can bring that knowledge to a private incident and
match locally and offline, instead of sending the incident anywhere.
Normative definition: `../protocol/open-praop-v0.1-final.en.md` §21.

## What's in this directory

- **`SCHEMA.md`** — the canonical field-by-field schema. If this
  directory's own files and `SCHEMA.md` disagree, `SCHEMA.md` (and,
  above it, protocol §21.2) governs.
- **`example-pack.yaml`** — a hand-authored example pack, built from
  two real Accepted Patterns (`visibility-is-influence`,
  `trajectory-lock`). It is a worked example of the schema, **not** a
  generated release artifact, and not guaranteed to reflect the
  corpus's current state.

## No generation tooling exists yet

There is no script or process that produces a matcher pack
automatically from `patterns/` and `cases/accepted/`. Packs are
currently hand-authored, which does not scale past a small number of
entries and creates real drift risk between the pack and the corpus it
claims to reflect.

This is a deliberate, dated choice, not an oversight: per the
project's own "don't build tooling ahead of an occurred need"
precedent, a generator is a backlog candidate, to be built once
hand-maintenance actually becomes error-prone or corpus size makes it
impractical — not built speculatively now. Anyone hand-authoring or
updating a pack must re-verify every field against the current Pattern
and Case files at the stated `corpus_revision`, per `SCHEMA.md` rule 1.

## What this directory does not cover

How an implementation actually performs local matching (string
comparison, embeddings, an LLM reading the pack, or anything else),
how it stores match results, or how it gates external contribution —
all of that is operational, implementation-side scope under protocol
§21.1, and is intentionally not addressed here.
