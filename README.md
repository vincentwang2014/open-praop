# Open PRAOP

**How people and AI actually work together, fail together, and get
cheaper to fail next time.**

Open PRAOP is an open, case-driven, falsifiable, continuously-revised
repository of operational practice for AI-assisted work.

It is not:

- an AI model leaderboard
- a prompt-technique collection
- an AI-complaints community
- a model-safety benchmark
- a finished AI governance standard
- a best-practices handbook for any single vendor or model

Open PRAOP studies AI-assisted work, agent workflow, human–AI
coordination, verification, organizational memory, escalation,
responsibility, reliability controls, and operational learning — not
model internals.

> **AI Security protects systems from attacks and unsafe model behavior.
> Open PRAOP focuses on protecting organizations from unreliable
> AI-assisted work.**

That's a scope boundary, not a claim that the two are unrelated.

## Status

**v0.1-final.** Launched with the protocol, templates, and two cases
migrated from private pilot runs that validated the pipeline end-to-end
before this repo existed. Both cases sit at `Observed / Active` — the
lowest confidence tier. That's intentional: two cases is not a taxonomy,
and nothing here should read as more settled than it is.

| Pattern | Confidence / Status | Anchor case |
|---|---|---|
| Control Accretion | Observed / Active | `cases/accepted/004-control-accretion-rerun.md` |
| Lesson-Generalization Failure | Observed / Active | `cases/accepted/003-lesson-generalization-failure.md` |

## How this repo works

Read `protocol/open-praop-v0.1-final.md` for the full protocol. Short
version:

1. **Cases** answer "what actually happened." Firsthand reports of
   AI-assisted work — failures, near-misses, or things that worked
   unusually well.
2. **Patterns** answer "does the same failure or success shape recur
   across cases." A pattern must be traceable to at least one `Accepted`
   case (see the protocol's Anchor-or-Demote rule) — no pattern gets to
   exist on the strength of a good name alone.
3. **Practices** answer "given evidence, what can a team actually do about
   it." Must be concrete enough to execute or test.
4. **Playbooks** answer "how does a team combine several Practices into a
   daily workflow." v0.1 doesn't pursue volume here, just the format.

Confidence for Patterns and Practices is tracked on two independent axes
— **Confidence** (Observed → Emerging → Operational → Canonical) and
**Status** (Active / Contested / Deprecated) — so a claim can be
`Operational + Contested` without losing information. See §9–10 of the
protocol.

## Structure

```text
open-praop/
├── protocol/       the full v0.1-final protocol document
├── cases/          case submission template + accepted cases
├── patterns/       pattern candidates and their confidence/status
├── practices/      practice candidates, evidence, enforcement level
├── playbooks/       format only in v0.1, no content yet
└── discussions/     how to challenge a classification, pattern, or practice
```

## Contributing

See `CONTRIBUTING.md`. The short version: **tell us what happened, you
don't need to know what Open PRAOP calls it.** Maintainers handle
classification, not contributors.

## Where this came from

This repo's protocol and initial two cases were exported from a private
working methodology repository after two internal pilot runs walked
existing cases through the full submission → de-identification →
evidence-tagging → mapping pipeline to find real friction before anything
went public. Neither pilot required a protocol change; one of them found
that de-identification has to be checked repo-wide, not file-by-file —
which is why every file here was checked against the full export set, not
reviewed in isolation. Full pilot writeups are not part of this public
repo (they reference the private source project); the protocol document's
changelog summarizes what each one found.

## License

Content in this repository — cases, patterns, practices, playbooks, and
protocol documents — is licensed under
[Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/).
Commercial use (consulting, training, product work) is explicitly
permitted; publicly distributed derivatives of the materials themselves
must carry the same license. The "Open PRAOP" name and any logo are
**not** covered by this license — see `LICENSE` for the full scope,
including what's excluded (trademark, raw/private evidence, third-party
material) and the plan to license any future software tooling separately
under Apache-2.0.
