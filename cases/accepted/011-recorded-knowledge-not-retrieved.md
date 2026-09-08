# Case 011 — Recorded Knowledge Was Not Retrieved Before Acting

**Status:** Accepted
**Evidence level:** Mixed — see Section H
**Date:** 2026-09-07
**Domain:** Methodology development — an AI agent's own operating
conventions and persistent project memory, while doing meta-work on
this project's own tooling (self-referential: the agent building the
project observed making the mistake the project studies)
**AI system involved:** A coding agent operating via a persistent
per-project memory store whose index is automatically loaded into
working context
**Maps to:** no existing Pattern anchors this mechanism. Candidate
primary anchor for a not-yet-named Pattern concerning recorded
knowledge remaining available but not being retrieved before action —
not an anchor yet. Also carries candidate **Partial** resemblance to
`../../patterns/lesson-generalization-failure.md` and
`../../patterns/transformation-boundaries.md`. See Pattern Mapping
below.

### Plain-Language Version (人话版)

The project keeps a memory file that already had the answer to a
question the agent was asked — where a related repository actually
lives, and whether a certain command-line tool is installed. Instead of
reading that file first, the agent tried to find the answer by running
several commands by hand: checking the wrong folder, checking a folder
that wasn't really a different folder at all, and running a tool that
the memory file already said, in writing, wasn't installed. Only after
all of that did the agent read the file — and there was the answer,
exactly as recorded, the whole time. The same project has a second,
older example this case treats as the *same proposed failure shape*,
not a confirmed match: a rule about not adding a certain line to commit
messages was written down once, then quietly not followed in a later
session, requiring a fix; that happened a second time shortly after;
and within the very session that produced this case, it nearly happened
a third time, the agent catching itself only by reading the file at the
last moment before anything left the machine. In none of these was the
answer missing — it was sitting in a place already meant to be checked.
The problem is that having the right answer already written down didn't
reliably stop the workflow from re-discovering it the hard way, or from
almost breaking the rule again. Whether "couldn't find an answer already
on file" and "broke a rule already on file" are really the same
underlying problem, or just look similar from the outside, is what this
case tests, not something already known.

> De-identified per `../../protocol/open-praop-v0.1-final.md` §7 — the
> operator's name is removed throughout (→ "the operator"); local
> filesystem paths and the operator's machine username are removed or
> generalized. This project's own public repositories and the mechanism
> (a per-project memory store, an index file, a route-table addition, a
> new operating-kernel rule) are kept as the actual subject matter,
> consistent with how this project's other self-referential case (Case
> 010) treats its own tooling as non-identifying — unlike Case 010,
> though, specific repository names, commit hashes, and session
> identifiers are not load-bearing here and are generalized or removed
> rather than kept.

---

### A. Basic Information

**Case title:** Recorded Knowledge Was Not Retrieved Before Acting
**Date:** 2026-09-07
**Domain:** An AI coding agent's own operating conventions while
performing methodology-development work on the project's own tooling
**AI system involved:** A coding agent operating via a persistent
per-project memory store whose index is automatically loaded into
working context at the start of each session

### B. What Were You Trying to Do?

Two task types observed across several related project sessions.
First: answer a question about the current public state of a related
project's in-progress work, which required knowing where an
authoritative copy of that project's repository lives, and whether a
certain command-line tool for interacting with a code-hosting service
was installed. Second, on separate occasions spanning several days:
make routine commits to the project's public repositories, governed by
a standing project convention, recorded days earlier, about what must
not appear in a commit message.

### C. What Actually Happened?

**Incident 1.** Asked to check the current state of a related
repository, the agent ran a repository-configuration check in the
wrong local directory (correct in isolation — that specific directory
genuinely has no such configuration), then repeated an equivalent check
in a subdirectory of the same location that could not have produced a
different answer, then searched two of its own project files for a
relevant reference without success, then attempted to invoke the
code-hosting CLI tool twice, in two different shells, both times
failing because the tool was not installed. Only then did the agent
search its own separate, persistent memory store and find a file that
already recorded exactly where the authoritative repository lived and
that the CLI tool was confirmed not installed — a file whose own
recorded timestamp predates this incident, and which was reachable
through an index already loaded into the agent's working context before
any of the above began (the index itself was loaded; the file's own
content was not shown to have been loaded prior to being read).

**Incident 2, offered as recurrence evidence of the same proposed
mechanism, not a second Case.** Separately, this project's memory store
had, on an earlier date, recorded a standing rule: omit a specific
attribution line from commit messages on this project's two public
repositories. That rule was not consulted before two later post-decision
recurrences added the prohibited line anyway (the same agent, the same
project family, in closely-spaced sessions — not independent
incidents; see Anti-Mapping Question) — the first produced a public
artifact (an unwanted contributor credit) requiring a repository
history rewrite to fix; the second required an internal correction to
the affected commit — the retained evidence establishes the
pre-correction commit and its amendment, but not whether the
pre-correction version was ever pushed. In a third post-decision
recurrence, within the very session that produced this case, the same
line was added to a routine commit a third time — this time the
recorded rule was consulted and the commit corrected before push, so it
never left the local machine at all.

### D. Why Did It Matter?

No wrong answer was ultimately given in either incident — Incident 1's
final answer was correct, and Incident 2's third recurrence never left
the local machine. The cost was extra time and unnecessary tool calls
(Incident 1); in Incident 2, the first post-decision recurrence produced
a public artifact requiring a repository history rewrite to fix, and the
second required an internal correction to the affected commit. The
recurring concern is not that a wrong substantive answer reached the
project owner, but that recorded knowledge was consulted only after
unnecessary work or after an action had already violated a standing
convention.

### E. What Was Surprising?

The project already treats "a lesson being recorded is not the same as
it being retrieved at the moment it's needed" as a named, described
limitation of its own memory-and-handoff practice. This incident is a
direct, first-party instance of exactly that limitation, observed in
the same agent that is itself part of building the project describing
the limitation — not a hypothetical failure mode, but the actual
tooling failing in the specific way its own documentation already
warned it could.

### F. What Did You Try?

Two changes, deliberately scoped narrow after review:

1. A short, structured (machine-parseable) block was added to the front
   of the relevant memory file, listing the specific infrastructure
   facts (repository locations, tool availability) that had been
   missed, so the answer is faster to locate by direct lookup rather
   than requiring a full read of surrounding prose.
2. A new rule was added to the agent's own operating-conventions
   document: before running a live discovery command to answer a
   question about this project's own repository locations, tool
   availability, or similar infrastructure facts, first check whether
   the answer is already recorded, falling back to discovery only if
   the record is absent, ambiguous, stale, or contradicted by a live
   artifact.

Explicitly *not* done: no automated gate, script, or tool-level
mechanism that would actually block a discovery command from running.
The new rule is stated forcefully ("must"), but is still enforced only
by the agent choosing to follow it — it was deliberately not escalated
past that, on the reasoning that building an enforcement mechanism
before establishing whether the cheaper fix works at all would be
premature, and that a hook narrow enough to catch a read-only discovery
command would not, by itself, have caught the second incident's
write-action shape (adding a prohibited line to a commit) at all — that
would need a separate, differently-shaped control, deliberately not
built in the same pass.

### G. What Happened Afterward?

An observation window was opened rather than a claim of resolution: the
next five eligible tasks of Incident 1's shape (needing to look up this
project's own infrastructure facts) are being tracked for whether the
new check happens before, rather than after, any discovery command. Not
yet complete at the time of this case's admission. No parallel tracking
mechanism exists yet for Incident 2's shape (the standing-rule/
commit-message case) — treated, per project decision, as a separate
control problem, not folded into the same tracking window.

### H. Evidence

Evidence is genuinely mixed, and this case went through several review
rounds specifically because earlier drafts overstated or inconsistently
stated it — recorded honestly here rather than smoothed into one label:

- The memory file's own recorded content and timestamp (Incident 1): a
  currently-inspectable artifact, retrievable by anyone with access to
  the agent's own memory store.
- The specific sequence and order of tool calls in Incident 1:
  self-reported only — no independently saved session transcript or
  command log is attached to this case.
- The standing rule and its original recording date: maintainer-
  verifiable local evidence, held in the project's own memory store —
  not independently checkable by a reader of this public case alone.
- The current (post-fix) clean state of the affected public
  repository's commit history: independently, publicly verifiable by
  any reader with access to that repository's own git history.
- The exact count of commits carrying the prohibited line before the
  history rewrite, and the two later internally corrected recurrences:
  maintainer-verifiable local evidence only — verified directly by the
  maintainer against locally-retained git artifacts (a local backup
  reference and locally-retained pre-correction commits) at review
  time, but **not independently retrievable by a reader of this public
  case**, since these depend on local artifacts outside the public
  repository. The third recurrence is confirmed not to have been
  pushed; the available retained evidence does not establish whether
  the second recurrence's pre-correction commit was pushed. One class
  of this evidence (locally-retained pre-correction commits, at least
  one of which — the third recurrence's — is confirmed never pushed) is
  explicitly not permanent — it can be lost to routine local git
  maintenance. Treated as maintainer-verified, self-reported for public
  purposes, not as independently reproducible public evidence, subject
  to re-check and downgrade at any future update to this case if no
  longer retrievable.
- Confidence / Status: not assigned above the level this case's own
  disposition supports — no Pattern currently exists for this
  mechanism, and no promotion beyond a single anchor is claimed.

### I. Interpretation

Across both incidents, the agent did not lack the needed information
and did not state anything false — already-recorded, already-correct
project knowledge simply was not the first thing consulted before
acting, in one case before looking something up, and in the other
before taking an action a recorded rule already prohibited. This
project's own documentation already names the limitation this
resembles: a lesson being recorded — even being reachable through an
index already loaded into working context — is not the same as it
being retrieved at the moment it is actually needed. This case is
offered as direct evidence of that limitation, not as proof it applies
beyond this one agent, project, and reviewer.

### J. Anti-Mapping Question

Is "recorded knowledge not consulted before acting" — spanning both a
fact-lookup failure and a prohibited-action failure — a single
mechanism, or two related-but-distinct ones being grouped by
convenient vocabulary rather than a demonstrated shared cause? Reasons
to doubt a single mechanism: a fact that needs discovering and a rule
that needs remembering are arguably different cognitive demands (look
something up vs. don't do something), and treating them as one
mechanism risks the same kind of unearned generalization this project's
own admission discipline exists to catch. Reasons the grouping may
still hold: in both cases the needed content was accurate, sufficient,
and already recorded — nothing was missing or wrong with what was
written down — and the failure in both was strictly about *when*,
relative to acting, the record was consulted. The maintainer's own
disposition was to keep this as one case rather than split it, on the
explicit condition that "same mechanism" continues to be treated as
this case's own hypothesis under test, not as an already-established
fact — not settled here.

Separately: this project has also privately observed a related-but-
distinct shape (a narrow, correct check followed by an overclaimed
broader statement to the maintainer) in two other internal incidents.
That shape is explicitly *not* treated as supporting evidence for this
case, and this case is not treated as a third instance of it — the
mechanism there involves a false claim reaching the maintainer; this
case's incidents involve no false claim at all, only delayed or skipped
consultation. That other candidate is not yet part of the public case
corpus and is not cited further here.

This case also carries a candidate **Partial** resemblance to two
already-Accepted Cases in this corpus, each with a materially different
mechanism:

- **Case 001 — Lesson-Generalization Failure**: that case's mechanism
  is that the *content* of a recorded lesson was too narrow and
  over-corrected in the wrong direction. This case's mechanism is
  different — the recorded content itself was accurate and sufficient;
  the failure was retrieval timing, not content scope.
- **Case 009 — A Truncated Conversation Window Made the System Re-Ask
  Something a Customer Had Already Answered** (candidate Partial Fit to
  Transformation Boundaries): that case's mechanism is that relevant
  information became physically *unavailable* once a conversation
  window truncated it. This case's mechanism is the opposite — the
  relevant information remained fully available and retrievable the
  entire time; nothing was truncated or hidden. The failure was that
  available knowledge went unconsulted, not that it became unreachable.

### K. What Would You Do Differently Next Time?

Before running a live-discovery command to answer a question about this
project's own repository locations, tool availability, or similar
infrastructure facts, check whether the answer is already recorded in
the project's own persistent memory, falling back to discovery only if
that record is absent, ambiguous, stale, or contradicted by a live
artifact. State this explicitly as a required step in the agent's own
operating conventions, not merely a preference — while being honest
that stating it more forcefully does not, by itself, make it an
enforced control; it remains something the agent must choose to follow,
until or unless something outside the agent's own compliance actually
gates the discovery command. A harder, tool-level enforcement mechanism
was considered and deliberately deferred, pending evidence from a
defined observation window that the cheaper fix is insufficient — and,
if ever built, would need to separately address the standing-rule/
write-action shape (Incident 2), which a discovery-command gate alone
would not cover.

---

## Pattern Mapping

- No existing Pattern in this repo currently covers this mechanism.
  This Case may anchor a not-yet-named Pattern concerning recorded
  knowledge remaining available but not being retrieved before action.
  If that Pattern is admitted, it may in turn support the candidate
  Practice "Operational Memory Is Infrastructure" (currently described
  only informally in this project's own plain-language materials, with
  no Pattern or Practice file of its own) — the Pattern and the
  Practice are two separate, not-yet-formalized things; this case does
  not assign the Practice's own name to the Pattern. Whether sufficient
  basis exists to formally create that Pattern, and how the Practice
  should then enter this project's own Case → Pattern → Practice chain,
  are left as open questions for the maintainer, not settled by this
  case.
- Lesson-Generalization Failure (`../../patterns/lesson-generalization-failure.md`) — Partial (candidate; content-scope mechanism differs from this case's retrieval-timing mechanism — see Anti-Mapping Question above)
- Transformation Boundaries (`../../patterns/transformation-boundaries.md`), via Case 009's own candidate Partial Fit — Partial (candidate; physical-unavailability mechanism differs from this case's available-but-unconsulted mechanism — see Anti-Mapping Question above)

Notes: candidate mappings only, recorded per this project's own Case ↔
Pattern mapping discipline — not authoritative beyond this case's own
Accept; the maintainer confirms any future Pattern promotion
separately.

---

### Maintainer review notes

- **Real enough:** concrete, self-referential incident — the agent
  building this project observed making the exact mistake the project's
  own methodology names as a known limitation. Two related incidents
  (a fact-lookup failure and a standing-rule violation) offered within
  one case, not two.
- **Evidence honesty took several rounds to land:** an early draft
  overstated specific facts as "loaded into context" when only an index
  pointing to them was shown to be loaded; miscounted trailer
  recurrences by including pre-decision commits that predate the rule
  they're accused of violating; stated a self-contradictory
  falsification condition for its own Hypothesis; and, in the
  push-status of one recurrence specifically, resolved an unknown fact
  inconsistently in different directions across different sections
  (implying a prior push in one place, implying it stayed fully local in
  another) rather than staying uniformly agnostic where the retained
  evidence genuinely doesn't settle it. All corrected across review
  rounds; the final version is deliberately blunt about what is publicly
  verifiable (current repository state) versus maintainer-only-verifiable
  (locally-retained git artifacts, not independently checkable by a
  public reader) versus genuinely undetermined (one recurrence's push
  history).
- **Privacy:** de-identification and combination-risk both assessed as
  passing. Unlike Case 010, this case's own subject matter (specific
  repository names, commit hashes, session identifiers) is not
  load-bearing to the mechanism, so those specifics were generalized or
  removed rather than kept — a stricter treatment than Case 010's own
  precedent, appropriate given nothing here requires the specifics to
  make the mechanism legible.
- **Anti-mapping:** credible. Correctly declines to treat a related,
  still-private candidate (narrow check → overclaimed statement) as
  supporting evidence, since that candidate's mechanism involves a false
  claim reaching the maintainer and this case's does not. Partial
  resemblances to Cases 001 and 009 are each explicitly distinguished by
  mechanism, not merged.
- **No duplicate incident:** the two incidents folded into this one case
  (a fact-lookup failure; a standing-rule/commit-convention violation)
  contribute exactly one formal anchor between them, not two, per this
  project's own anchor-counting discipline — recurrence within an
  incident type strengthens the candidate mechanism's credibility, it
  does not multiply anchors.
- **Pattern/Practice naming discipline:** an early draft used the
  candidate Practice's own working name ("Operational Memory Is
  Infrastructure") as the provisional name for the new Pattern this case
  might anchor — corrected. The Pattern stays unnamed and unestablished
  by this case; naming and admitting it, and then routing the
  already-informally-described Practice through it, are separate future
  steps.
- **Plain-language check:** passes fresh-eye EQ without leaning on
  memory-system or context-window jargon — closes on the mechanism in
  ordinary language and explicitly flags the shared-mechanism question
  as untested rather than assumed.
