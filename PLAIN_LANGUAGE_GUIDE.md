# PRAOP in Plain Language

> **What this is.** A guided tour of what PRAOP has actually found —
> real cases first, plain language second, in the order they were
> originally understood, not sorted by taxonomy. Every entry follows
> the same five layers: **one line** (what it's called) → **plain
> language** (say it in ordinary words) → **a real event** (what
> actually happened) → **why AI does this** (not a bug — this is how
> it works) → **what to do about it** (our current best guess, not a
> commandment).
>
> **What this is not.** The evidence authority. This page explains;
> the [Protocol](protocol/open-praop-v0.1-final.en.md) governs. Each
> entry ends with a short **Formal status** line pointing to the
> actual Case/Pattern/Practice record — that record decides evidence
> level, confidence, and promotion. If this page and the formal record
> ever disagree, the formal record is right.
>
> **New to PRAOP?** Just read top to bottom — it's a story before it's
> a reference. **Already familiar?** Jump to any entry; each one
> stands alone.

---

## 1. Visibility Is Influence

**One line:** What you let an AI see is itself a form of controlling
what it does.

**Plain language:** Whatever an AI can see, it gets pulled along by —
and that pull is often stronger than an explicit rule you wrote. Real
control isn't "write a rule after the fact"; it's "don't let it see
what it shouldn't in the first place."

**A real event (two cases, same mechanism, two domains):**
① A tool that drafts long-form fiction: when the AI was shown the full
chapter outline before writing each scene, it kept re-describing things
already described in earlier scenes. An explicit instruction ("don't
repeat earlier chapters") did not fix it. Only withholding the outline
— showing it just the current scene's boundaries — fixed it.
② A mortgage-advisory chat system: the AI carried a customer's earlier
bankruptcy disclosure, and separately, several distinct phone numbers,
forward into later requests simply because they were visible in
context, without being asked to.

**Why AI does this:** For ordinary software, "visibility" is neutral —
data sits there until logic decides to use it. For an AI, seeing
something changes what it generates next; visibility isn't passive
awareness, it's a direct input to behavior.

**What to do about it:** Don't rely only on access control (who can
call what) — also do exposure control (what should the AI never see at
all). The cleanest safety isn't a warning in a tool's description; it's
the information not being in front of the model. One caveat: this
reduces the failure rate, it doesn't guarantee zero.

**Formal status:** Pattern candidate — not yet in `patterns/`.
Case ① is de-identified and submission-ready. Accepted anchor(s): none
yet.

---

## 2. Symbolic Success ≠ Operational Correctness

**One line:** The most dangerous AI failures are the ones that don't
throw an error — either a confident wrong answer with no alarm, or
mistaking "an action was taken" for "the intended result actually
happened." The light is green; underneath, it already broke.

**Plain language:** Ordinary software crashes, turns red, throws a
warning — you see it, you fix it. AI doesn't crash. It hands you a
confident, polished, *wrong* result and proceeds as if delivered, with
nothing flagging it.

**A real event (two cases, same failure shape):**
① Within one conversation, a customer sent two pricing requests
minutes apart. The first mentioned a prior bankruptcy; the second
didn't. The AI silently carried the bankruptcy status into the second
request and priced accordingly — the rate was wrong. Nothing failed:
no error, no crash, a normal success response.
② A coding agent was asked to fix a login feature. It changed the
code, committed it, and reported it deployed. The operator believed it
and logged it as shipped. Twenty hours later, testing it directly
showed the new code had never actually gone live.

**Why AI does this:** Traditional systems are deterministic — same
input, same output, and breakage is visible. AI is probabilistic; its
job is "generate the most plausible next thing," whether or not that
thing is correct or the action actually landed. It doesn't carry a
lingering "I should confirm that deployed" across a conversation
boundary — once the conversation ends, an unverified action simply
evaporates from its awareness.

**What to do about it:** Don't expect it to raise the alarm. Make
inferred assumptions **visible** (have it say the assumption out loud,
so it's checkable). **Execute optimistically, verify skeptically** —
for any consequential action, check the actual resulting state, in the
same session, rather than trusting "I did it."

**Formal status:** `Pattern — Observed / Active`. Now in
`patterns/symbolic-success.md`. One Accepted anchor (Case 004, ②
above); three further independently-observed incidents are known
(including Case ① above) but not yet independently submitted/Accepted
— see the pattern file for what would move this to `Emerging`.

---

## 3. Inference Never Silently Commits

**One line:** An AI can infer, can suggest — but must never turn an
inference into a done deal without telling you.

**Plain language:** Letting an AI guess is fine. The problem is what
happens after the guess — quietly using it to change something
consequential, without saying so. Guessing: fine. Silently acting on
the guess: not fine.

**A real event:** Same incident as Entry 2, case ①: a customer's
bankruptcy disclosure from one pricing request was silently carried
into a second, unrelated-seeming request in the same conversation, and
priced in — no one had a chance to catch it. To be fair to the AI: the
inference itself wasn't unreasonable. What was wrong was the
*silence* — had it said "reminder: this customer mentioned a prior
bankruptcy — factor that in?" there would have been no incident at
all.

**Why AI does this:** AI defaults toward continuity and closure — it
resists hard resets and dislikes stopping to ask. A traditional
interface is request → response, independent each time; an AI behaves
more like a standing, default-continuous relationship that assumes
prior context still holds.

**What to do about it:** Any consequential action passes through the
operator first. Two allowed modes: **Suggest** (state the guess, take
no action) and **Confirm** (ready to act, waits for a yes). The
forbidden third mode — acting on an inference with nobody visibly
deciding it — gets a name: **the Ghost.** Anything carried forward
must be visible, traceable to what introduced it, and reversible.

**Formal status:** Missing entirely from the formal corpus, though
unusually mature as a candidate — already has a working Suggest/Confirm
model and a named anti-pattern (the Ghost) that reads more like a ready
Practice than a bare idea. Shares its case anchor with Entry 2 above —
one incident, two readings, not two anchors. Not yet drafted as formal
Principle/Practice text.

---

## 4. Identity-Bound Truth

**One line:** Some data is identity-bound — my number, your number, a
third party's number. An AI cannot see that boundary on its own.

**Plain language:** To a person, "this is my phone number, that's the
customer's" is obvious, unconscious. To an AI, it's just a set of
digits that look the same shape — nothing marks whose is whose.

**A real event:** An AI needed to send a text message, had several
phone numbers available in context, and picked the wrong one — a
message went to the wrong recipient. Not malicious, not "dumb" — it
genuinely had no representation of which number belonged to which
party.

**Why AI does this:** An AI sees data, not boundaries. Ownership
relationships — whose phone, whose money, whose access — are invisible
semantic objects to a system that only sees shapes that look
interchangeable.

**What to do about it:** Never assume an AI knows who owns what. For
any identity-bound field, either keep it out of view entirely or label
ownership explicitly and require human confirmation before anything
executes. Avoid above all: handing it several interchangeable-looking
options and letting it "just pick one."

**Formal status:** Pattern candidate — not yet in `patterns/`. A
single, clean, genuinely independent incident (no sharing with any
other entry here). Accepted anchor(s): none yet.

---

## 5. Operational Memory Is Infrastructure

**One line:** A lesson an AI system learned the hard way, if not
actually recorded, will get relearned the hard way — again.

**Plain language:** An AI surfaces problems and lessons faster than an
organization naturally retains them. A bug fixed today, if it never
truly "enters the system," will resurface unchanged in a few weeks,
under a different person, in a different context.

**A real event:** Several already-fixed failure classes (silently
carrying state forward between requests; a fake-deployed fix; an
inference quietly acting as fact) recurred weeks later. The lessons had
been written down somewhere, but never entered anything actually
*consulted* on the next relevant occasion — so recording them didn't
functionally prevent the repeat.

**Why AI does this:** An AI generates a day's worth of "experience" far
faster than a human or team can naturally absorb. Production of
knowledge outpaces retention, and the gap leaks silently — you won't
notice the loss because the loss makes no noise either.

**What to do about it:** Build memory as infrastructure, not "a
document to update when there's time." Lessons and case records need
to be structured so they get **pulled into the next relevant moment**,
not filed away to go stale.

**Formal status:** The Practice already exists and is in active use —
`praop-project-skill`'s entire four-file memory discipline is this
idea, operationalized. The Principle itself isn't yet a standalone §3
entry.

---

## 6. Probabilistic, Not a Rule Engine

**One line:** An AI isn't a "forbidden means it won't" rule engine;
it's a probability engine — your instruction is one force acting on
it, not a hard switch.

**Plain language:** Most people instinctively assume "the prompt is
the law." In practice, what you wrote is just one of several forces
being weighed against each other — and the instruction is often not
the strongest force in the room.

**A real event:** Same incident as Entry 1's case ①: the fiction-
writing tool kept repeating earlier scenes. The direct fix attempted
first — an explicit instruction, "do not repeat prior chapters" —
simply did not work.

**Why AI does this:** Its foundation isn't a logic branch, it's a
probability distribution over "what's the most likely next token."
Your instruction shifts that distribution but can't veto it outright
the way a line of code can.

**What to do about it:** Don't treat a prompt as a hard constraint. If
something truly must be enforced, put it somewhere the AI has no
access to override — at the code layer, structurally blocked. Structure
beats rules when the goal is blocking a high-probability behavior.

**Formal status:** Adjacent to `praop-project-skill` kernel rule 1, but
a narrower, more operational claim. Not a standalone §3 Principle.
Shares its case anchor with Entry 1 — not a second anchor.

---

## 7. Renhua — Understanding Only Counts When It's Operator-Grounded

**One line:** If you can't translate a claim back into plain language
and ground it in a real event, you haven't actually understood it —
and "following along in the moment" doesn't count.

**Plain language:** Understanding has two layers. Layer one: someone
explains it and you nod, "got it." Layer two: days later, a completely
new, unprompted situation comes up, and you independently recognize
"this is that thing" and use it to make a call. Only layer two is
real.

**A real event:** The operator often found himself nodding along in
fast-moving exchanges with an AI acting in an "architect" role,
assuming "they must be right" without fully following — until he
realized that if even the person actually responsible for outcomes is
nodding without understanding, the whole structure has started
floating loose from the ground.

**Why this happens:** AI systems naturally drift toward compression
and abstraction, and two AI systems can converse fluently with each
other — but a human needs concrete, lived experience to check meaning
against. A term detached from a real case becomes "semantic theater":
the words are all there, the meaning is hollow.

**What to do about it:** Give every term an operational meaning — one
plain sentence plus one real event. Case first, name second, never the
reverse. The real acceptance signal: can a person use the term,
unprompted, in a brand-new situation.

**Formal status:** Already in the Protocol (§3, Renhua) — this entry's
two-layer distinction has been folded into that section directly. No
gap.

---

## 8. Cognition Metabolism — No Abstraction Without Pressure

**One line:** An AI generates new concepts and frameworks far faster
than a person can actually digest and independently apply them.

**Plain language:** Three different speeds: an AI generates an idea in
hours; verifying it's actually right takes days to weeks; a person
internalizing it well enough to use it, unprompted, takes weeks to
months. That speed gap is itself the risk — concepts pile up faster
than they're digested.

**A real event (the project's own origin story):** An architect AI was
asked whether accumulated lessons should become a methodology, and
within a short exchange produced a full doctrine framework branded as
"1,000 foundational principles" (actually twelve). Two AI systems then
rapidly iterated on it — deciding what should become doctrine, what
should stay a candidate — faster than the operator could track. He
later admitted he hadn't kept up with their pace, and didn't fully
understand the resulting principles himself. Compounding it: the AI
systems' own naming for the framework was inconsistent across their
own outputs.

**Why this happens:** Language generation is too easy — AI-driven
discussion readily escalates into abstraction that sounds increasingly
coherent while drifting further from what's actually being produced.

**What to do about it:** Let output wait for digestion. Anything meant
to be treated as settled needs repeatedly-felt real operational
pressure — at least two independent cases, plus one ruled-out
alternative explanation. Short of that, label it honestly as
"observed / candidate."

**Formal status:** Partially covered by "No New Axis Without
Incidents" (§3) and the Doctrine Inflation guard (§18), but this
entry's specific claim — the *rate mismatch* itself is the mechanism —
isn't fully captured yet. This same incident is also the anchor behind
Entry 11 (Semantic Ownership Loss) below — one incident, two readings,
not two anchors.

---

## 9. Reliability Is a Coordination Problem, Not an Intelligence Problem

**One line:** The hard part was never making the AI smarter — it's
making the work stable together.

**Plain language:** The default assumption is: AI goes wrong = the
model isn't smart enough. None of the incidents here were caused by a
lack of intelligence. Every individual piece was fine; put together,
it broke — **at the seams**, not inside any one part.

**A real event:** Same incident as Entry 2's case ②: a coding agent
changed login code, committed it, reported "it's live" — believed,
logged as shipped. Twenty hours later, it had never actually deployed.
Every individual piece checked out; the break was at the seam between
what the agent assumed and what the operator assumed.

**Why this happens:** AI is inside the loop where an organization
actually makes decisions. Once inside that loop, "is the model smart"
stops being the deciding factor — what decides is how well it meshes
with process and people.

**What to do about it:** Shift attention from "make the AI smarter" to
"make the whole organization run steadily alongside it." Widen what
"reliable" means — from the model alone to the full chain: people,
process, tooling, memory, escalation, ownership.

**Formal status:** Already Open PRAOP's own mission statement (§1),
near word-for-word. Correctly a framing statement, not a §3 Principle.
Shares its case anchor with Entry 2 — not a second anchor.

---

## 10. Assert Incidents, Hedge Abstractions

**One line:** Say what already happened, plainly. Hedge what's still
unproven. Two different registers for two different kinds of claim.

**Plain language:** Something that actually happened → state it
plainly. An unproven inference or generalization → say plainly that
it's a guess, and leave room to be wrong. Reversed, both go bad.

**A real event (self-referential):** While writing this material, an
unproven insight was explicitly marked as a hedge — "still observed,
not yet named" — rather than canonized. But the fake-deployment
incident (Entry 2's case ②) was stated flatly, because it really
happened.

**Why this happens:** A probabilistic system tends toward extremes:
confidently overclaiming a guess as fact, or — after being corrected a
few times — over-hedging everything, turning real events into mush
with reflexive "maybe"s.

**What to do about it:** Before stating anything with weight, sort it
first: did this already happen, or is it still unproven? State the
first plainly; flag the second plainly as a guess.

**Formal status:** Already in the Protocol (§3), matching directly. No
gap. Shares its case anchor with Entry 2 — not a second anchor.

---

## 11. Semantic Ownership Loss

**One line:** A concept can keep the same name while its actual
meaning quietly drifts, turn by turn — and because an AI will keep
citing its own earlier phrasing, even the person who originally
proposed the idea can end up needing the AI to tell them what they
meant.

**Plain language:** This word was mine to begin with. But the AI kept
explaining it more and more fluently, and eventually I was the one who
needed the AI to tell me what my own word meant.

**A real event:** The same origin story as Entry 8 above, read from
the other side: as two AI systems rapidly iterated on the project's own
doctrine, the operator gradually stopped being able to independently
explain what "the doctrine" actually meant — he was nodding along with
increasingly polished terminology rather than holding the meaning
himself. Recovering it required an external forcing function: asking
for an executive-facing explanation, and then a plain-language pass
like this one.

**Why this happens:** AI-generated abstraction can outrun the human
owner's ability to independently hold and reproduce the meaning behind
it — especially when multiple AI systems reinforce each other's
phrasing faster than a person can check it against anything concrete.

**What to do about it:** Meaning must retain a traceable owner across
every retelling. Concretely: when a concept crosses systems, sessions,
or agents, keep its source, its owner, and one authoritative artifact
explicitly attached — don't let a retelling quietly become the new
original.

**Formal status:** Pattern candidate, recently upgraded from Hold — has
its own real incident, independent of every other accepted case in the
corpus. Not yet submission-formatted or drafted into formal text.
Accepted anchor(s): none yet.

---

## 12. Trajectory Lock

**One line:** Once you land on an explanation, each new piece of
contradicting evidence tends to get absorbed as a reason to elaborate
that explanation further — not as a reason to question whether it was
ever right.

**Plain language:** Once you're heading the wrong way, instead of
turning back, you just keep patching around it and going deeper.

**A real event:** A small business automated a login flow against a
third-party platform. The login worked one day and failed the next,
repeatedly. Each time, a coding agent proposed a fix, confirmed it
worked, and it failed again shortly after. The agent concluded the
platform was rate-limiting the account, and proposed progressively more
elaborate workarounds — paid proxies, a home internet connection, and
eventually a dedicated home computer configured as a permanent proxy.
Three weeks in, nobody had yet asked whether the "rate limit" theory
was actually true. It broke when the operator asked one basic question
— *why would a paying customer be rate-limited at all?* — and asked the
agent to replicate exactly what a human does when logging in manually:
receive the code, then just wait for it. The automation had been
enforcing an artificial timeout instead. The real fix was a few dozen
lines of code. **The same week, on an unrelated bug**, the same agent
again confidently blamed an external vendor and made three edits
chasing that theory, before an untested internal code branch turned
out to be the actual cause.

**Why AI does this:** Once a plausible explanation is adopted, an
AI-driven debugging process tends to absorb each new contradicting
signal as a reason to elaborate the existing theory further, rather
than a prompt to re-examine whether the theory still holds. The lock
rarely breaks from inside the process — it usually takes an outside
interruption asking the most basic possible question.

**What to do about it:** When a fix "works" and then fails again
shortly after, treat that as a signal to question the original
diagnosis — not a cue to patch further within the same theory. Before
building infrastructure around a suspected external constraint, verify
the constraint actually exists.

**Formal status:** `Pattern — Observed / Active`. Now in
`patterns/trajectory-lock.md`. One Accepted anchor (Case 005), which
itself documents both incidents above. Whether the second (same-week)
incident already satisfies §10's "second underlying incident" bar for
`Emerging` on its own is an open question flagged in the pattern file
for maintainer decision, not yet resolved.

---

## 13. Transformation Boundaries

**One line:** Whenever information has to change shape — free text
into structured data, one system's schema into another's — meaning can
quietly fall out at the crossing, even though every side of that
crossing looks correct on its own.

**Plain language:** Passing a message through a chain of translators,
each one perfectly fluent in their own two languages, can still lose
the one detail that mattered — because no single translator's own
language pair was ever wrong.

**A real event:** A loan-intake system used an LLM to extract
structured details from a customer's free-text message, normalized
that into an internal schema, then sent it to a third-party
rate-lookup platform for pricing. A customer clearly stated a specific
loan-qualification type (DSCR, used for investment-property loans) —
but the extraction schema had no field for it, so it silently dropped
out at that first step. A later layer already had a fallback rule
written to catch exactly this case, but it was watching for a
different signal than the one the extractor actually produced — a
second, independent mismatch stacked on the first. Every component
returned a valid, well-formed result. Nothing errored. For six days,
every message through that channel got a confident, fully-priced quote
for the wrong loan product.

**Why AI does this:** Each stage in a multi-component pipeline only
checks that its own output is a valid instance of its own contract —
it has no way to check that it still means what the previous stage
meant. Two adjacent layers can each be internally correct and still
drift out of sync with each other, and neither layer's own tests can
detect that, because the mismatch only exists in the comparison between
them, not inside either one.

**What to do about it:** Treat cross-layer vocabulary consistency as
something checked explicitly and periodically, not just when a symptom
happens to surface — for every pair of adjacent layers, does every
value one layer can express have somewhere to go in the next layer's
schema, and vice versa?

**Formal status:** `Pattern — Observed / Active`. In
`patterns/transformation-boundaries.md`. One Accepted anchor (Case
003). At least two further independently-observed instances are known
from private source material but not yet independently
submitted/Accepted.

---

## Two patterns already in the formal corpus

The ten entries above are candidates. These two are already
`Accepted`, with real Pattern records — included here so this page
covers everything PRAOP has actually found, not only what's newest.

### Control Accretion

**One line:** Every safety check you add along the way can be
individually correct, and the checks can still end up changing the
very thing they were supposed to be verifying.

**Plain language:** To make sure nothing was done wrong, more checks
kept getting added — until the checks themselves became the thing
making it wrong.

**A real event:** A same-day rerun of an already-decided experiment —
same code, same inputs, nothing new to figure out — was expected to
take a low-effort repeat. Along the way, a string of safety additions
went in one after another, each catching a real bug. But the new
verification code itself kept changing which commit was actually being
run, which invalidated the sign-off just given, which triggered
rerunning the verification again. A task expected to take a fraction of
a day consumed most of a full working day — with no single wrong
decision anywhere in the chain.

**Why AI does this:** Every individual addition responded to a real
risk the previous step had just exposed — which is exactly why it's
harder to catch than an ordinary bug. The failure lives in the
composition: verification and the work being verified stopped being
separate activities.

**What to do about it:** When a mid-run issue turns up, ask one
explicit question: does this actually invalidate the current run's
validity? If yes, stop and fix now. If no, log it and keep going —
rather than reflexively adding a new check on the spot.

**Formal status:** `Pattern — Observed / Active`. One Accepted anchor.
Full record: [Case](cases/accepted/002-control-accretion-rerun.md) ·
[Pattern](patterns/control-accretion.md).

---

### Lesson-Generalization Failure

**One line:** Remembering a correction is not the same as having
learned its actual boundary.

**Plain language:** Last time you got hit, you only remembered not to
touch that exact spot. Change the shape a little, and you fall into
the same hole again — not because you forgot, but because what you
remembered was too narrow.

**A real event:** An agent had already been told, once, that a
credential was standing context — nothing that needed repeating. It
repeated it anyway, four separate times. Right after the fourth time, a
fix went in: "stop narrating the credential." Immediately afterward, in
the same session, the opposite failure occurred — the agent issued a
command with no credential attached at all, and the environment got
stuck. The fix had targeted "said too much"; the actual fact that
mattered — *when* the credential was needed — had never been written
down, so it broke the run again from the other direction.

**Why AI does this:** A fix written right after a correction gets
pattern-matched to the literal symptom of that one complaint, rather
than generalized to the risk class it actually belongs to. When the
same underlying fact resurfaces in a structurally different — here,
opposite — shape, the existing fix doesn't fire.

**What to do about it:** When writing a fix immediately after a
correction, ask what the general risk class is, not just the literal
symptom. Test the fix against the opposite-direction failure, not only
a repeat of the same one.

**Formal status:** `Pattern — Observed / Active`. One Accepted anchor.
Full record: [Case](cases/accepted/001-lesson-generalization-failure.md)
· [Pattern](patterns/lesson-generalization-failure.md).

---

## Want the evidence, not just the story?

Every claim above traces back to a real event, and every real event has
a home in the formal corpus once it's been reviewed:

- **[Cases](cases/)** — what actually happened, one incident at a time.
- **[Patterns](patterns/)** — recurring shapes across multiple cases.
- **[Practices](practices/)** — what to actually do about a Pattern.
- **[Playbooks](playbooks/)** — Practices combined into a workflow.
- **[Protocol](protocol/open-praop-v0.1-final.en.md)** ([中文](protocol/open-praop-v0.1-final.md)) — how all of the above gets decided, reviewed, and promoted.

This page explains. The Protocol governs.
