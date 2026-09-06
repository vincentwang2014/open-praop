# Open PRAOP v0.1-final — Minimum Viable Protocol

> **Language:** English
> **Status:** Official English translation
> **Canonical source:** `open-praop-v0.1-final.md` (Chinese)
>
> This file is a faithful translation of the canonical protocol. It
> must not introduce normative rules that do not exist in the
> canonical source. If a semantic discrepancy is discovered, the
> canonical source governs until the discrepancy is resolved.
>
> Translated from canonical revision: `23608d3`

**Status:** v0.1-final
**Date:** 2026-09-04
**Purpose:** Build an open, case-driven, falsifiable, continuously
self-correcting AI-native operational practice repository.

## Changelog from v0.1 draft

v0.1 draft (2026-09-03 discussion) was reviewed and converged to four required
fixes before being treated as final. All four are structural gaps, not
wording polish — three of them repair defects that already existed in this
repo's own prior tiering system (see `README.md`), not just gaps introduced
by this draft.

1. **Confidence/Status split** (§9) — Pattern/Practice confidence was a
   single ladder that could only go up. Split into two independent axes so a
   claim can be `Operational + Contested` or `Canonical + Contested` without
   losing information.
2. **Anchor-or-demote hardened** (§10) — every promoted claim must name a
   concrete case anchor. Two loopholes closed explicitly: anchors must be
   `Accepted` cases (not `Submitted`/`Reviewing`), and "independent" means a
   different underlying incident, not a different write-up of the same one.
3. **Public-repo self-deidentification gate** (§7) — the de-identification
   protocol must be applied to Open PRAOP's own repository artifacts before
   public launch, not just to future case submissions. Recommended path is a
   clean new public repo, not flipping the internal repo public in place.
4. **Second-review gate for doctrine-changing decisions** (§13) — routine
   intake stays solo-maintainer; anything that changes PRAOP's own state
   (promotion, Contested↔Active, Deprecated, major reclassification)
   requires a second pair of eyes. Known limitation stated explicitly rather
   than solved: early-stage second-review capacity may be zero, in which
   case promotion stalls by design.

Scope for v0.1-final was deliberately held to these four items — no
committee, no automated scoring, no reviewer reputation, no certification.
Adding those now would repeat the exact failure shape (Control Accretion,
Case 002) these safeguards exist to catch.

**Post-convergence refinement pass (2026-09-04, still v0.1-final):** two
internal wording/logic gaps found on read-through, both closed without
adding new structure:

5. **Emerging threshold aligned across §9 and §10** — §9 defined `Emerging`
   as "multiple events or independent evidence," but §10 originally allowed
   promotion on a single `Accepted` anchor, which would have made the first
   real promotion a dispute about which section governs. §10 now requires
   1 anchor *plus* additional independent evidence or a second incident.
6. **"Original contributor as second reviewer" scope narrowed** — the
   original wording let a contributor's factual confirmation double as the
   second-review gate itself. Now explicit: it satisfies fact-checking only
   and never counts toward the promotion/status-change second-review
   requirement, closing a path to a single de-facto decision-maker being
   recorded as two-reviewer approval.

**Pre-launch validation (2026-09-04):** two internal pilot runs walked
existing cases through the full pipeline (raw → de-identification →
submission → evidence tag → Accepted → mapping → practice candidate)
before any public launch decision. Findings:

- Pilot 001 (Control Accretion case) confirmed the anchor-or-demote rule
  actually caps promotion — a detailed, compelling case stayed at
  `Observed/Active` because it had only one anchor, not because a reviewer
  chose caution.
- Pilot 002 (Lesson-Generalization Failure case, chosen for higher
  identity/secret density) confirmed identity and secrets can be fully
  removed while the causal chain survives intact, confirmed the evidence-
  level mechanism refuses to inflate E0 to E1 just because a write-up is
  detailed and well redacted, and — the most consequential finding —
  showed that de-identification has to be checked **repo-wide**, not
  file-by-file: sensitive terms recurring across an unrelated case's
  narrative body, outside the file actually being reviewed, would have
  shipped unnoticed under a per-file check.

No protocol changes resulted from either pilot. The repo-wide de-
identification finding shaped how the public repo's content was exported
(a repo-wide sweep at export time caught the protocol's own §7 worked
examples using real project identifiers as "before" text — fixed to use
placeholder examples instead), not the protocol text itself.

**Renhua (人话) formalized as an operating principle, tested by EDTCU
(2026-09-04, still v0.1-final).** §3's existing "Plain Language Required"
principle was renamed and elevated to **Renhua (人话)** — kept in Chinese
deliberately rather than fully translated, because the term carries an
attitude ("don't let terminology and fluent AI output stand in for real
understanding") that "Plain Language" alone doesn't fully capture. Three
layers: Renhua is the principle, a Plain-Language Version is the
practice, and the stress test is how it's checked — called **EDTCU**
(Even Donald Trump Can Understand), **Eddie-Q**, or **EQ**
interchangeably, three names for the same test (EQ here meaning the
test, not emotional intelligence). Comes with an explicit Evidence →
Interpretation →
Plain-language explanation (Renhua) → Human understanding →
Decision/ownership chain explaining *why* it matters (semantic
ownership, not writing style). It now also constrains content, not just
judgment: Pattern entries (§2.2), the Practice Template (§5), and the
Playbook Template (§6) each require a **Plain-Language Version（人话版）**
field. Not a new principle — it formalizes the Layer B (人话) convention
already used in the Case Canon, and extends it to Patterns/Practices/
Playbooks, which previously had no equivalent requirement.

**Principle formalized as a small cross-cutting layer, not a fifth
growing asset (2026-09-05).** §2 now states explicitly that Open PRAOP
stays at four growing core assets (Case → Pattern → Practice →
Playbook); Principle sits above that chain as a small, slow-growing
layer with a deliberately higher bar for new additions than Pattern
gets — this guards against Doctrine Inflation (§18) happening one
layer up, where a new Principle would otherwise get minted for every
new Pattern.

**Renhua's acceptance criterion sharpened (2026-09-05).** §3 now states
explicitly that passing Renhua means recognizing and applying an idea,
unprompted, in a later, new situation — not nodding along when it was
first explained. Same underlying principle; the two-layer distinction
between these was previously implicit.

**No New Axis Without Incidents added (2026-09-05).** A new §3
Principle, the explicit mirror of "No Fit Is Valid": that one blocks
force-fitting an event into existing taxonomy; this one blocks
force-expanding the taxonomy itself without at least two independent
incidents and one failed workaround.

**PRAOP Case Admission added (2026-09-05, §13 Step 6.5).** Closes a
gap: nothing previously specified how a maintainer's verbal or
in-conversation approval becomes an auditable transition into the
Accepted corpus. Adds an explicit state machine (Draft → Submission →
Reviewing → Accepted/Rejected/Revise), a standard Maintainer Review
checklist template with a Decision line, and a hard rule that an agent
may only promote a submission into `cases/accepted/` once that line
explicitly reads ACCEPT — never on the strength of conversation alone.
Also explicitly separates Case acceptance from Pattern promotion: an
accepted case gives its Pattern one valid anchor and triggers
eligibility recalculation, but promotion itself remains a separate,
deliberate decision under §10's Anchor-or-Demote rule.

---

## 1. What Is Open PRAOP

Open PRAOP is an open practice and case repository, used to study:

> How people and AI actually collaborate, fail, and improve in real
> work — and which practices make the next incident cheaper.

It is not:

* An AI model leaderboard;
* A collection of prompt tricks;
* An AI complaint community;
* A model safety benchmark;
* A claimed-complete AI governance standard;
* A best-practices manual for any single vendor or model.

Open PRAOP's primary object of study is not what happens inside the
model, but:

* AI-assisted work;
* Agent workflow;
* human–AI coordination;
* verification;
* organizational memory;
* escalation;
* responsibility;
* reliability controls;
* operational learning.

One-line positioning:

> **AI Security protects systems from attacks and unsafe model
> behavior. PRAOP focuses on protecting organizations from unreliable
> AI-assisted work.**

This is only a boundary statement — it doesn't mean the two are
mutually exclusive.

---

# 2. Open PRAOP's Four Core Assets

Open PRAOP v0.1 maintains only four growing knowledge assets, roughly
forming one chain:

```text
Case → Pattern → Practice → Playbook
```

* **Case** — one concrete thing that happened.
* **Pattern** — a failure (or success) shape that recurs across
  multiple Cases, with a similar mechanism.
* **Practice** — what to specifically do in response to a Pattern.
* **Playbook** — multiple Practices organized into one executable
  workflow.

Plain language: **A Case is one event. A Pattern is a recurring
playbook of failure. A Practice is specifically what to do. A Playbook
is a whole method.**

This chain isn't a strictly one-directional production line — a
Practice, for instance, can in turn cause a new Case to be observed —
but the overall direction, from "what happened" to "how do we
systematically respond," is these four steps.

**Principle is not a fifth, parallel asset.** It's a small foundational
layer sitting above this chain, and it does not keep growing the way
the other four do:

```text
        Principles
      ↙     ↓     ↘
Case → Pattern → Practice → Playbook
```

A Principle can be distilled from multiple Cases, from one or more
Patterns, or even from a Practice that has repeatedly failed
validation — but it is not the case that "every time a Pattern is
found, a new Principle gets produced." The bar for adding a new
Principle is explicitly higher than the bar for adding a new Pattern:

> A Principle is only warranted when it spans multiple
> incidents/Patterns and would change how Open PRAOP works in general.

Plain language: **Patterns can be many; Principles should stay few.**

The concrete list of Principles is in §3. It is a small, slow-growing
layer, not the kind of continuously-accumulating catalog that Case /
Pattern / Practice / Playbook are — this is deliberate, and guards
against exactly the kind of inflation §18 ("Doctrine Inflation") warns
about, just happening at the Principle layer instead of the Pattern
layer.

## 2.1 Cases

Answers:

> What actually happened?

Cases must be based on real events as much as possible, not
hypothetical stories.

---

## 2.2 Patterns

Answers:

> Do similar failure shapes or success shapes recur across multiple
> cases?

Examples might include:

* Locked Inference Trajectory
* Provenance Drift
* Lesson Generalization Failure
* Control Accretion

A Pattern doesn't hold up just because the name sounds good.

It must grow out of real cases.

Every Pattern entry must include a **Plain-Language Version (人话版)**
(see §3, the Renhua / EDTCU Test) — answering, in ordinary language,
"what does this actually mean," not only a technical definition. A
claim that can't point to a plain-language version is, just like a
claim that can't point to a case anchor, not something the
organization can be said to have actually grasped.

---

## 2.3 Practices

Answers:

> Given a problem that already has some evidentiary support, what can
> we actually do about it?

A Practice should be concrete enough for a team to execute or test.

---

## 2.4 Playbooks

Answers:

> How does a team or company combine a set of Practices into a daily
> working workflow?

Future examples might include:

* Vibe Coding Starter Playbook
* AI Incident Review Playbook
* Agent Verification Playbook

v0.1 does not aim for a large number of Playbooks — only for
establishing the format.

---

# 3. Fundamental Methods

This is Open PRAOP's **Principle layer** (see §2 for how Principle
relates to the four core assets) — small, slow-growing, with a bar for
new additions explicitly higher than Pattern's, not the kind of
continuously-accumulating catalog.

Open PRAOP follows a small number of minimal principles.

### Incident First

Record what happened first; discuss theory afterward.

Plain language:

> Say what happened first; theory can wait.

### Assert Incidents, Hedge Abstractions

Facts that have already been observed can be stated plainly.

Mechanisms, regularities, and generalizations abstracted from cases
must note their own uncertainty.

Plain language:

> What actually happened can be said flatly; a pattern you generalized
> from it should not be dressed up as a law.

### Artifact > Memory

Real evidence — logs, output, commits, screenshots, emails, run
results — takes priority over human memory, and over an AI's own
explanation of its behavior.

Plain language:

> If you can look at a log, code, or a commit, don't rely on "I
> remember."

### No Fit Is Valid

A case does not need to be forced into Open PRAOP's existing taxonomy.

Allowed:

* Fit
* Partial Fit
* No Fit
* New Pattern Candidate
* Out of Scope

A taxonomy that explains everything has no research value.

Plain language:

> Not every problem has to be crammed into one of Open PRAOP's
> existing categories.

### No New Axis Without Incidents

Don't rush to expand the classification system itself just because one
case is hard to categorize.

Before adding a new classification dimension (a new field, a new
classification axis, a new confidence dimension, etc.), you need to be
able to point to at least two independent incidents proving the
existing dimensions genuinely can't express what's needed, and to have
tried at least once to work around it using existing means, and
failed. If you can't point to both, don't add it — record the pressure
as an observation instead, and wait for the next incident.

This is the mirror of "No Fit Is Valid": that one blocks forcing an
event into an existing category; this one blocks the opposite move —
inventing a new category to fit one event.

Plain language:

> One odd case doesn't justify inventing a new category right away.

### Knowledge Is Not Enforcement

Writing something into a README, CLAUDE.md, a prompt, or a handbook
does not mean the practice is actually being executed reliably.

Practice and Enforcement must be kept distinct.

Plain language:

> Knowing the rule doesn't mean it'll actually be followed next time.

### Renhua (人话)

> **Renhua (人话) — say it so the human who owns the consequence can
> actually understand it.**

This isn't just a demand for plain wording — it's saying: don't let
terminology, abstraction, and an AI's fluent style of expression stand
in for real understanding. The closest English phrase is "Plain
Language," but "人话" (Renhua) carries an extra layer of attitude worth
keeping rather than fully translating away — Open PRAOP grew out of
real work, and doesn't need to pretend every concept originated in
English management vocabulary.

Formal statement:

> **If the person responsible for the outcome cannot explain the issue
> in ordinary language, semantic ownership has not been established.**

Plain language:

> If you can't explain it plainly, don't pretend you've understood it.

This principle isn't solving a writing-style problem — it's solving a
**semantic ownership** problem: if, in an organization, an AI can
fluently produce an entire vocabulary of terminology while the person
actually responsible for the outcome can only say "mm-hm, I guess I
get it," that organization has already lost part of its own semantic
ownership over its decisions — even if the process still looks
completely normal on the surface.

**Understanding has two layers, and only the second one truly
counts:** the first layer — someone explains it to you (or two AI
systems talk to each other in increasingly "sophisticated"
terminology, jargon flying back and forth), and you nod, "got it."
This layer can always be re-supplied on demand by an AI explaining it
again, so it's also the least reliable. The second layer — later, an
entirely new situation comes up, with nobody prompting you, and you
recognize on your own "this is that thing," and use it to make a
judgment. Only the second layer is real — and it grows the slowest,
only through repeated real events and repeated use of your own.

> Passing Renhua means a human can later recognize and apply the idea
> in a new situation without the AI prompting them — not that they
> nodded along when it was explained.

Plain language:

> Nodding along and saying "got it" in the moment doesn't count. What
> counts is: later, in a new situation, with nobody reminding you, you
> recognize this is that thing, and you use it.

PRAOP splits Renhua into three layers:

* **Renhua / 人话** — the principle itself.
* **Plain-language explanation** — the practice: see "Who Must Have a
  Plain-Language Version" below.
* **EDTCU / Eddie-Q / EQ** — the concrete stress test, three names for
  the same thing.

**Who must have a Plain-Language Version:**

* **Principle** (each principle in this section, §3) — Required.
* **Pattern** (§2.2) — Required.
* **Practice** (§5) — Required.
* **Playbook** (§6) — Required.
* **Accepted Case** (§9, Case Status) — Should, added by the
  maintainer at Accept time (see §13 Step 6), not the contributor's
  responsibility.
* **Raw case submission** (§4) — Not required. The contributor's
  responsibility is only to "report the incident" (see §4); the
  plain-language version is something the maintainer adds once it's
  been processed into a structured case — it must never become a
  submission barrier.

One additional constraint:

> **Plain-language version should explain the idea, not summarize the
> jargon.**

A plain-language version is explaining the thing clearly, not swapping
the terminology word-for-word for a shorter phrase and copying it
again. If it reads like a "translationese simplification" — just
swapping technical words for shorter equivalents — it still hasn't
actually passed the EDTCU Test.

> **EDTCU is the stress test for Renhua.**
>
> EDTCU — Even Donald Trump Can Understand. Also informally called
> **Eddie-Q**, or simply **EQ**. All three refer to the same PRAOP
> plain-language test — use whichever reads best in context: EDTCU for
> the origin story, Eddie-Q for casual discussion, EQ for checklists
> and review comments (e.g. "EQ: Pass").
>
> A deliberately humorous plain-language test: if an important idea
> cannot be explained in ordinary, concrete language, we should not
> assume it is organizationally understood.

**A note on the name:** EDTCU borrows a highly recognizable public
figure known for extremely direct, plain speech, purely as a memory
aid — it does not represent any political position, and is not a
judgment of that person. The point is always "can this be said so that
almost anyone can understand it." **Note: EQ here refers to this
plain-language test, not emotional intelligence.**

PRAOP therefore breaks "understanding" into a chain:

```text
Evidence
    ↓
Interpretation
    ↓
Plain-language explanation (Renhua)
    ↓
Human understanding
    ↓
Decision / ownership
```

If the middle link — "plain-language explanation" — breaks, the "human
understanding" and "ownership" that follow it are likely nominal only:
the decision record says "approved," but the person who approved it
never actually grasped what happened.

One practical use: when multiple AI systems agree with each other on
some abstract claim ("both models agree this is a semantic authority
topology problem"), that agreement is not itself evidence that should
be counted (see §18, "AI Consensus as Evidence"). On the contrary, this
is exactly the signal to stop and run the EDTCU Test — if nobody can
explain it, in three sentences, to the person actually responsible for
the business outcome, that itself is a risk signal, not "consensus has
been reached."

This principle is also not a new invention. The existing Layer B
(人话) restatement convention in the Case Canon already practices it —
for example, Event #003's Layer B: "Last time you got hit, you only
remembered not to touch that exact spot. Change the shape a little,
and you fall into the same hole again — not because you forgot, but
because what you remembered was too narrow." This section only
elevates that from a case-level writing convention into a formal PRAOP
operating principle, and requires Pattern / Practice / Playbook to
follow it as well, not only cases.

---

# 4. Case Submission Protocol

A contributor does not need to understand PRAOP's taxonomy first.

The contributor's responsibility is:

> **Report the incident.**

The maintainer's responsibility is:

> **Explain and classify the incident.**

This also includes the plain-language-version rule: raw submission
**does not require** a Plain-Language Version (see §3, "Who must have
a Plain-Language Version") — the contributor does not need to write
one. Once a case is Accepted, the maintainer "should" add one when
processing it into a structured case (see §9 Accepted, §13 Step 6).

## Case Submission Template

### A. Basic Information

**Case title:**
Give the event a simple title.

**Date / approximate period:**
An approximate date is fine — e.g. 2026-08, or "over several weeks."

**Domain:**
E.g. software engineering / mortgage / legal / customer service /
writing / finance.

**AI system involved:**
Optional. Anonymized or generalized naming is allowed.

---

### B. What Were You Trying to Do?

Describe the original task in a few sentences.

Should ideally answer:

> If everything had gone normally, what was supposed to happen?

---

### C. What Actually Happened?

Describe it in chronological order.

Write only the behavior you actually observed.

Try to keep separate:

* observed fact;
* interpretation;
* later hypothesis.

---

### D. Why Did It Matter?

Describe the actual impact, e.g.:

* time;
* money;
* customer experience;
* a wrong decision;
* repeated work;
* compliance risk;
* operational disruption;
* trust loss.

---

### E. What Was Surprising?

What behavior didn't match your original expectation?

This item doesn't have to prove the AI was "wrong" — it's meant to
capture a behavioral discrepancy worth studying.

---

### F. What Did You Try?

What corrective actions did you take?

Record them in the actual order they happened.

---

### G. What Happened Afterward?

The outcome falls into one of:

* Resolved and verified
* Improved but not fully verified
* Failed
* Recurring
* Pending
* Unknown

**Writing a fix rule down does not automatically make it "Resolved."**

---

### H. Evidence

What evidence exists?

* log
* screenshot
* commit
* output
* email
* ticket
* conversation
* recording
* none

If the evidence can't be made public, simply note:

> Evidence retained privately.

---

### I. Your Interpretation — Optional

What kind of problem do you think this might be?

* Existing PRAOP pattern
* Maybe related
* New pattern
* No idea

The contributor is not responsible for the final classification.

---

### J. Anti-Mapping Question

> **Why might this case *not* actually belong to the PRAOP pattern you
> think it does?**

If you don't know, you may write:

> Unknown.

This item exists to reduce confirmation bias.

---

### K. What Would You Do Differently Next Time?

Write only your current working recommendation.

You are not required to state it as a universal principle.

---

# 5. Practice Template

A Practice must be traceable to a case or other evidence.

## Practice Title

State in one sentence what it does.

### Plain-Language Version（人话版）

In one or two ordinary sentences, say plainly what this Practice is
actually about — not only a technical statement. If you can't say it
plainly, that means it hasn't passed the EDTCU Test (§3) yet — write
that sentence clearly first, then fill in the rest.

### Problem Addressed

What failure shape is this Practice trying to reduce?

### When to Use

In what environment or task does this apply?

### What to Do

Must be an executable behavior.

### What Not to Do

Describe common misuses.

### Evidence

List the cases supporting this Practice.

E.g.:

* Case 014
* Case 022
* External Case 008

### Known Limitations

Under what conditions might it not work?

### Enforcement Level

Choose one:

**Guidance**
Relies mainly on a person or agent following it voluntarily.

**Process**
Already built into an explicit workflow.

**Mechanical Enforcement**
A tool, preflight check, gate, or automated check blocks an obvious
violation.

### Confidence

See §9 — Confidence and Status are recorded separately, e.g.
`Operational / Active` or `Emerging / Contested`.

A new Practice cannot enter directly at `Canonical`.

---

# 6. Playbook Template

A Playbook is a workflow assembled from multiple Practices.

## Playbook Name

E.g.:

> Vibe Coding Team Starter Playbook

### Plain-Language Version（人话版）

In one or two ordinary sentences, say plainly what this Playbook has
the team actually do. Also bound by the §3 EDTCU Test.

### Who Is This For?

Describe the typical user.

### Problem

What operational problem does this team currently have?

### Entry Conditions

When should this Playbook be used?

### Workflow

Compress it into as few stages as possible.

E.g.:

1. Preflight
2. Execute
3. Verify
4. Escalate if needed
5. Capture incident

### Human Ownership

Make explicit which outcomes must ultimately be a human's
responsibility.

### Automation / Enforcement

Which steps can be checked mechanically?

### Evidence

Link to the cases and Practices that support each step.

### Known Failure Modes

What problems might this Playbook itself create?

E.g.:

* excessive control;
* review bottleneck;
* false confidence.

---

# 7. De-identification Protocol

Core principle:

> **Redact identity, preserve causality.**

Open PRAOP does not require a contributor to make the complete raw
material public.

Keeping two versions is recommended:

### Raw / Private Version

May contain the complete incident detail.

Does not enter the public repo by default.

### Public / Redacted Version

Keeps only the information needed to understand the failure shape.

---

## Information That Must Be Removed or Replaced

Including, but not limited to:

* names;
* email;
* phone number;
* API key;
* password;
* auth token;
* account number;
* loan number;
* customer identifier;
* private repository URL;
* private IP;
* internal endpoint;
* unauthorized-for-disclosure customer names;
* unauthorized-for-disclosure internal company information.

Secrets must not be published as a hash substitute.

Delete them outright.

---

## Recommended Generalizations

For example:

`Vincent`
→ `Operator`

`800HomeLoan`
→ `Mortgage brokerage`

`GH_TOKEN`
→ `repository authentication credential`

`RunPod`
→ `cloud GPU environment`

`repo-name`
→ `private repository`

An exact amount, if it isn't a necessary part of the failure mechanism:

`$73,482`
→ `$50k–$100k`

---

## Combination Risk Check

Even once each individual item has been anonymized, you must still
ask:

> If someone familiar with this company or industry saw the remaining
> detail, could they guess who this person or organization is?

If the answer might be yes, generalize further.

---

## Information That Must Be Preserved As Much As Possible

De-identification must not destroy:

* the original task;
* the sequence of events;
* AI/system behavior;
* the cause/effect relationship;
* impact;
* correction;
* outcome.

---

## Public Launch Gate: Repository Self-Deidentification Pass

The existence of this rule is itself a PRAOP lesson: the moment Open
PRAOP's own de-identification protocol was written, it had not yet
been applied to Open PRAOP itself — this is a live instance of §3's
"Knowledge Is Not Enforcement."

Before any Open PRAOP content is publicly launched, a complete
self-deidentification pass must first be run on **the repository
itself**, not only on newly-submitted cases.

**The check must cover:**

* the README and all documentation;
* already-included case files;
* examples;
* screenshots;
* sample logs;
* issue / PR templates;
* **git commit history** — deleting one line of text from a file does
  not clear the record from `git log -p`; this is the item most easily
  missed;
* any Claude Code session / conversation transcript that will be cited
  or linked externally — if a transcript will be publicly cited, it
  must pass the same de-identification check as the README, rather
  than being assumed safe by default as "internal discussion."

The point isn't "make each file clean" — it's that **the entire chain
of public evidence** must not, in combination, reveal identity — one
file passing does not mean the combination is still safe (see the
Combination Risk Check above).

**Recommended approach:**

It is not recommended to flip an existing internal repo public in
place. The safer path is:

> Create a clean new public repo, and migrate only reviewed,
> public-safe content into it.

The private origin repo (which retains full history and detail) and
the public Open PRAOP repo (which contains only content that has
passed the de-identification pass) should be two separate
repositories, not the same repository with its visibility toggled.

---

# 8. Evidence Levels

v0.1 does not design a complex scoring system.

Only four levels.

## E0 — Self-Reported

Only the contributor's own description.

Can still be included, but must be flagged as such.

## E1 — Supporting Artifact

At least one artifact exists supporting the key event.

E.g. a log, commit, output, or screenshot.

## E2 — Reconstructable

A third party could roughly reconstruct the event's trajectory from
the artifacts.

## E3 — Independently Verified

The key facts have been verified by another reviewer, system, or
independent reproduction.

Note:

> Evidence level is not importance level.

A very important case may still only be E0.

---

# 9. Confidence / Status / Promotion

Cases and Patterns/Practices should not use exactly the same promotion
logic.

## Case Status

### Submitted

Just received.

### Reviewing

Facts, de-identification, and evidence are being checked.

### Accepted

The incident itself is clear enough to enter the case library.

Once in this state, it should (not must, but is recommended to) have a
Plain-Language Version added, written by the maintainer during
processing — it does not need to be provided by the contributor (see
§3, "Who must have a Plain-Language Version," and §13 Step 6).

### Disputed

A key fact is under serious dispute.

### Withdrawn

The contributor or maintainer has decided to withdraw it.

---

## Pattern / Practice: Confidence × Status (two independent axes)

The v0.1 draft once wrote Pattern/Practice certainty as a single
one-directional ladder (Observed → Emerging → Operational →
Canonical), and also crammed Contested / Deprecated into that same
ladder. This implicitly assumed things can only ever become more
certain, which conflicts with PRAOP's own falsification spirit, and
also couldn't express a real state like "this used to be solid, but a
counterexample has now appeared."

v0.1-final splits this into two independent axes. **Confidence**
answers "how much has the evidence accumulated." **Status** answers
"does this claim still hold up right now." The two are orthogonal and
can combine freely.

### Confidence axis

#### Observed

Some phenomenon has been clearly observed in at least one case.

Only describes the phenomenon; does not claim generality.

#### Emerging

Multiple events or independent pieces of evidence begin to support the
same explanation.

Competing explanations are still allowed.

(The concrete anchor threshold for promotion to Emerging is in §10,
Anchor-or-Demote: at least 1 `Accepted` case anchor, **plus**
additional independent evidence or a second underlying incident — a
single Accepted case alone is not automatically sufficient; the two
sections are aligned on this point.)

#### Operational

There is already enough repeated evidence, and the related Practice
has demonstrated real value in actual work.

#### Canonical

Supported by long-term, multi-source, cross-environment evidence, and
still holds up after active attempts at falsification.

**Canonical should be very difficult to obtain.**

### Status axis

#### Active

The current judgment is still valid and can be used/cited as normal.

#### Contested

A new counterexample or serious dispute has appeared and has not yet
been resolved.

**Contested is not deletion**, and it does not require Confidence to
be downgraded first — a claim can be `Operational + Contested`, or
even `Canonical + Contested`: meaning "there used to be fairly strong
evidence, and it was actually used, but a new counterexample or
serious dispute has now appeared." "It used to be solid" does not mean
"it can't be overturned now."

#### Deprecated

No longer recommended for continued use, but the historical record is
retained, not deleted.

E.g. `Operational + Deprecated`: it once had sufficient evidence and
was actually used, but was later superseded by better understanding or
falsified — it's still retained as research material.

### Recording format

Pattern / Practice certainty is written as `Confidence / Status`, e.g.:

* `Emerging / Active`
* `Operational / Contested`
* `Canonical / Contested`
* `Operational / Deprecated`

If Status is not written, it defaults to `Active`.

---

# 10. Promotion Rules

## Anchor-or-Demote (a hard rule, not a judgment call)

> **Every promoted PRAOP claim must name at least one concrete case
> anchor. If the anchor cannot be named, demote the claim.**

This rule was written too softly in the v0.1 draft (just something
"best considered" during promotion) and has been made a hard
precondition, because it's the core mechanism preventing doctrine
inflation (a claim looking proven simply because it's been rewritten
repeatedly) — it cannot rely on people doing the right thing
voluntarily.

**Per-tier anchor requirements:**

* **Observed** — at least 1 concrete incident (the corresponding case
  itself is enough; it is not yet required to support any promotion).
* **Emerging** — at least 1 `Accepted` case anchor, **plus** additional
  independent supporting evidence, or a second independent underlying
  incident. A single Accepted case is not sufficient on its own to
  reach Emerging — this is to align with §9's definition of Emerging
  ("multiple events or independent evidence begin to support the same
  explanation"), so that "does 1 Accepted case get you to Emerging"
  doesn't become the first promotion dispute.
* **Operational** — at least 2 **independent** `Accepted` case
  anchors, and already actually used in real work.
* **Canonical** — case anchors from multiple independent environments,
  still holding up after active attempts at falsification.

**Two loophole protections that must be written in now** (not
governance complexity — this is to prevent the very first round of
promotion from gaming the rule):

1. **An anchor must be a case in `Accepted` status.** A case in
   `Submitted` or `Reviewing` status cannot be used as grounds for
   promotion — its facts and de-identification haven't finished being
   reviewed, so it can't be used to support a conclusion that has
   already been promoted.
2. **"Independent" means a distinct underlying incident, not a
   different write-up of the same incident.** Writing up the same
   event as two cases from different angles, or the same contributor
   resubmitting it with different wording, cannot count as two
   independent anchors toward the Operational threshold.

A claim that can't point to a specific incident, only an abstract
description, cannot enter the formal Pattern / Practice entries no
matter how persuasively it's written — it can only stay in Discussion.

## Other Promotion Checks (judgment calls, not hard numeric gates)

v0.1 does not set mechanical numeric gates, e.g. "fewer than 5 cases
means no promotion." Beyond Anchor-or-Demote, promotion must also
answer at least:

1. How many supporting cases are there?
2. Do they come from independent environments?
3. Is there an obvious selection bias?
4. Is there a No Fit case?
5. Is there a competing explanation?
6. Is there artifact support?
7. Has the Practice actually been run?
8. Has it ever failed?
9. Can the conclusion be explained in plain language?
10. Is this promotion happening because the evidence has actually
    grown, or because the wording has just gotten more polished?

The last question matters especially.

---

# 11. Repository Minimum Structure

v0.1 stays minimal:

```text
open-praop/
│
├── README.md
├── CONTRIBUTING.md
├── LICENSE
│
├── cases/
│   ├── README.md
│   ├── TEMPLATE.md
│   └── accepted/
│
├── patterns/
│   └── README.md
│
├── practices/
│   ├── README.md
│   └── TEMPLATE.md
│
├── playbooks/
│   ├── README.md
│   └── TEMPLATE.md
│
├── protocol/
│   ├── de-identification.md
│   ├── evidence.md
│   └── confidence-and-promotion.md
│
└── discussions/
    └── README.md
```

v0.1 will not, for now, build:

* a database;
* a web app;
* a contributor score;
* certification;
* an automated taxonomy engine;
* a complicated governance hierarchy;
* a large ontology;
* dozens of issue labels;
* a public `drafts/` or `case-drafts/` directory. A private working
  draft (e.g. the output of a tool like `praop-case-draft`) should
  never appear in this repo, reviewed or not. This repo should only
  ever see two kinds of case content: a submission that has already
  completed de-identification and a combination-risk check and is
  awaiting review (the PR itself is that review surface), and a case
  that is already `Accepted` into `cases/accepted/`. There is no
  in-between "public draft zone."

Observe real usage first.

---

# 12. Contributor Workflow

A contributor's normal path:

```text
Read short contribution guide
        ↓
Choose:
Case / Practice / Playbook
        ↓
Fill template
        ↓
Perform de-identification check
        ↓
Submit PR or Issue
        ↓
Maintainer review
```

**This order cannot be reversed.** De-identification happens before
the PR exists, not during the PR's review process. A GitHub PR (along
with its comment history) is public the moment it's opened — closing
or rejecting it afterward does not make it private again. Don't open a
PR with a draft that hasn't yet passed de-identification and the
combination-risk check just to "get feedback first" — finish that step
on the private draft, then put the already-de-identified content into
the PR.

Most important:

> A contributor does not need to use PRAOP jargon correctly.

"I don't know what this is called, but here's what happened."

This is a completely valid submission.

---

# 13. Maintainer Review Workflow

Maintainer review does only six things, plus one cross-cutting
second-review gate.

## Step 1 — Is This Real Enough to Review?

Determine:

* Is it firsthand?
* A sourced external case?
* Hypothetical?

Hypothetical content does not enter the Case Canon.

---

## Step 2 — Privacy / De-identification

This is a safety-net check, not where de-identification is actually
supposed to happen — that should already be done before the
contributor opens the PR (see §12). This step confirms it was actually
done correctly, rather than substituting for it.

Check whether there is still:

* PII;
* secrets;
* proprietary details;
* re-identification risk.

If unsafe, send it back for revision. **But the fact that the PR has
already been made public isn't undone by this** — if what this step
finds is serious enough (a real name, a credential, detail that could
locate a specific person or customer), beyond sending it back for
revision, also consider whether the contributor needs to delete the PR
and contact GitHub support to handle content that has already been
made public, rather than simply treating it as "fix it and resubmit."

---

## Step 3 — Separate Fact From Interpretation

For example:

**Fact**

> Agent attempted the same fix eight times.

**Interpretation**

> The agent was locked into an inference trajectory.

The two must not be collapsed into one sentence.

---

## Step 4 — Evidence Tag

Assign:

E0 / E1 / E2 / E3

Don't raise the evidence level just because the case fits PRAOP theory
well.

---

## Step 5 — Mapping

The maintainer may tag:

* Fits existing pattern
* Partial fit
* No fit
* New pattern candidate
* Out of scope

Must write one sentence:

> Why might this mapping be wrong?

---

## Step 6 — Accept Without Over-Promoting

A case can be Accepted.

But the Pattern does not need to be promoted in lockstep.

In other words:

> Accepting evidence ≠ accepting theory.

At the same time as Accepting, the maintainer should add a
Plain-Language Version (人话版) — one or two sentences making clear
"what this actually is," not re-proving it, and not applying a
classification to it. This is the only field an Accepted Case requires
the maintainer to actively add (see §3, "Who must have a
Plain-Language Version").

---

## Step 6.5 — PRAOP Case Admission: the ACCEPT decision must be an artifact, not a conversation

This rule closes a specific gap: a submission has already been
de-identified, a PR has already been opened, and the maintainer really
has read it — but "the maintainer said 'OK'" is not itself an
auditable record; it exists only in chat history. The Artifact >
Memory principle should not stop applying at exactly the promotion
step.

> **Human maintainer records ACCEPT in the submission artifact; only
> then may an agent promote that submission into the Accepted Case
> corpus.**

Plain language:

> You make the call, the file keeps the record, the AI moves it in.

### State machine

```text
Draft → Submission → Reviewing → Accepted / Rejected / Revise
```

* **Draft** — a private draft, not yet de-identified, not open to
  public review.
* **Submission** — de-identification and the combination-risk check
  are complete; open to public review.
* **Reviewing** — a PR is open and being discussed.
* **Accepted** — the maintainer has explicitly approved it; it enters
  the formal corpus.
* **Rejected** — does not enter the corpus.
* **Revise** — sent back to the Submission stage for changes.

### Maintainer Review block (template)

Every submission file carries a block like this at the end, editable
only by the maintainer:

```markdown
## Maintainer Review

- [ ] Incident is concrete
- [ ] De-identification is sufficient
- [ ] Combination-risk checked
- [ ] Evidence level is honest
- [ ] Interpretation is separated from observation
- [ ] Anti-mapping is credible
- [ ] No duplicate underlying incident is being counted as independent

**Decision:** [ pending ]
Reviewed by:
Review date:
```

Only once the **Decision** line explicitly reads **ACCEPT** is an
agent permitted to promote that submission into a formal Case: assign
a Case ID, move it into `cases/accepted/`, change Status to Accepted,
preserve the original submission's provenance, and commit. Before that
point, no matter how many times a conversation has said "this looks
good," an agent must not promote it on its own.

### Case Acceptance and Pattern Promotion must stay separate

Accepting a Case only means that Case itself has entered the corpus —
it does **not** mean the Pattern it corresponds to is automatically
promoted:

```text
Case accepted
      ↓
Pattern gains one valid anchor
      ↓
Pattern's promotion eligibility is recalculated
      ↓
whether it's actually promoted is a separate decision
```

The reason is that the same underlying incident can support several
different Patterns at once (this protocol has emphasized this
repeatedly: one incident can support several different mechanism
readings, but must not be quietly counted as several independent
anchors). So after a Case is Accepted, an agent may only say:

> Transformation Boundaries now has 1 Accepted anchor and is eligible
> for its Observed status to be re-evaluated.

It may not say, on its own:

> The Pattern has been promoted.

That is a separate decision, requiring its own explicit trigger,
governed by §10's Anchor-or-Demote rule — it does not happen
automatically just because a Case was accepted.

---

## Step 7 — Second-Review Gate for Doctrine-Changing Decisions

If one maintainer alone decides every step of privacy, evidence,
mapping, promotion, contested, and canonical, Open PRAOP can easily
become "one person's personal ontology" — which is itself a
relativized form of Control Accretion (at the governance level rather
than the tooling level). v0.1-final blocks this risk in the smallest
way possible, rather than introducing a committee system.

**Can be done solo (intake):**

* Case `Submitted` → `Reviewing`;
* Basic de-identification check (Step 2);
* Initial E0/E1 evidence tagging;
* Typos / formatting;
* Judging something as clearly out-of-scope.

**Requires a second pair of eyes (doctrine-changing):**

* Pattern promotion (any Confidence increase);
* Practice → `Operational` or `Canonical`;
* Switching between `Contested` ↔ `Active`;
* Marking as `Deprecated`;
* A major reclassification (e.g. overturning an existing mapping
  conclusion).

The second reviewer is not required to be a PRAOP core maintainer —
they can be:

* another maintainer;
* a domain reviewer;
* the original contributor (for factual confirmation only).

> **The original contributor may serve as a second reviewer for
> factual accuracy only; this does not satisfy the second-review
> requirement for pattern/practice promotion, status changes, or major
> reclassification.**

**Known limitation (stated now, rather than inventing a fallback
mechanism):**

> Early-stage second-review capacity may be zero. In that case
> promotion stalls by design.

An early-stage project may have only one maintainer, in which case a
doctrine-changing decision will stall for lack of a second reviewer —
this is the designed outcome, not a bug that needs to be worked
around. The stall should be read as "not enough capacity, waiting per
the rule," not interpreted as some mysterious process getting stuck.

---

# 14. Practice Review

When a Best Practice is submitted by the community, the maintainer
should additionally check:

### Is it actually actionable?

"Improve governance" doesn't count as a Practice.

"Every production deployment must have an independent endpoint
verification" does.

### Is it evidence-linked?

If there is no evidence:

It can enter Discussion.

It does not go directly into the formal Practices.

### Does it add friction?

The cost must be recorded.

Because a reliability control can itself create new operational risk.

### Can it be enforced?

If it can only rely on "remembering to do it," it must be explicitly
labeled Guidance, rather than pretending it's a strong control.

---

# 15. Success Cases

Open PRAOP does not accept only failure cases.

Submissions specifically about:

> Something worked unusually well.

are welcome. The template is basically the same, but the questions
become:

* What risk originally existed?
* What practice was adopted?
* What behavior changed?
* What evidence is there?
* Is there an alternative explanation?
* Has it been reproduced?

Purpose:

> Open PRAOP should not become an AI Failure Museum.

What we're studying is how to work better with AI.

---

# 16. External Cases

Cases sourced from Reddit, blogs, papers, news, etc. may enter Open
PRAOP, but must be clearly distinguished from firsthand cases.

Must record:

* original source;
* publication date;
* direct artifact / quotation availability;
* whether facts can be independently verified.

An AI's summary of web content is not itself provenance.

---

# 17. Minimal Governance

v0.1 needs only:

### Maintainers

Responsible for:

* privacy;
* evidence classification;
* acceptance;
* mapping;
* promotion proposals.

Doctrine-changing decisions are bound by the second-review gate in
§13 Step 7 — not every maintainer can unilaterally finalize a
promotion / contested / deprecated ruling.

### Contributors

Submit cases and practices.

### Discussion

Anyone may challenge:

* classification;
* pattern;
* practice;
* promotion.

No formal committee needs to be established.

---

# 18. What Open PRAOP Must Avoid

These safety valves are not an abstract list of risks we're worried
might happen someday — they exist because the project underlying Open
PRAOP has already really experienced some of these failure shapes. A
rule should be able to point to a specific event, not stop at "we
think this is a best practice."

### Taxonomy Capture

Distorting the facts so a new case fits an existing category.

### Doctrine Inflation

A polished-sounding claim gradually starts to look proven simply
because it's been rewritten by AI repeatedly.

→ This is the direct reason §10's Anchor-or-Demote exists: a claim
with no concrete case anchor cannot be promoted, no matter how refined
its wording is.

### Control Accretion

Continuously adding contributor friction in the name of keeping the
repo "rigorous," until eventually nobody wants to submit anything.

→ **Anchored in Case 002: The Rerun That Became a New Experiment.** A
reliability layer built to audit a rerun gradually started changing
the very state it was supposed to be auditing, and eventually inflated
a routine repeat experiment into a full engineering project — every
individual step looked reasonable on its own. Open PRAOP v0.1 itself,
while converging on these four fixes, deliberately locked its own
scope to just these four and refused to let itself expand into twenty
items of governance — specifically so as not to reproduce this same
failure shape at the governance level.

### Translationese

Translating a simple event into abstract jargon nobody actually
understands.

### AI Consensus as Evidence

Multiple LLMs agreeing with each other does not mean evidence has
increased.

### Memory as Truth

"We discussed this before" cannot substitute for an artifact.

---

# 19. Open PRAOP v0.1 Success Criteria

The first version is not measured by star count.

Only by:

1. Whether an external contributor can complete a case submission
   without training;
2. Whether de-identification can actually be completed successfully;
3. Whether any case fails to fit the existing PRAOP taxonomy;
4. Whether at least one credible Pattern candidate can be formed from
   multiple cases;
5. Whether any Practice has actually been used and produced an
   outcome;
6. Whether the repo stays simple, without governance itself blocking
   participation.

---

# 20. v0.1's One-Line Rules

For the Contributor:

> **Tell us what happened. You do not need to know what PRAOP calls
> it.**

For the Maintainer:

> **Preserve the incident before improving the theory.**

For the project as a whole:

> **Cases create patterns. Patterns suggest practices. Practices earn
> promotion through use and falsification.**

For Open PRAOP itself (new in v0.1-final):

> **Repair the state model, harden the anchor rule, clean the public
> boundary, and add one second pair of eyes for doctrine-changing
> decisions. Then stop.**
