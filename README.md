# Open PRAOP

*Probabilistic Reliability Operations Practice*

PRAOP is an open, case-driven practice for learning how humans and AI
systems can work together reliably.

It starts from a simple idea:

> AI is not a deterministic machine. It is a probabilistic agent.

Humans are probabilistic agents too.

But AI is not simply a faster or more knowledgeable human. It is a
different kind of probabilistic agent, with different strengths,
different failure patterns, different memory boundaries, different ways
of using context, and different ways of going wrong.

We already have thousands of years of experience learning how to work
with other humans.

We are only beginning to learn how to work with AI.

PRAOP is an attempt to learn that systematically.

## Why PRAOP Exists

When a company hires a new employee, managers do not assume they already
understand exactly how that person will behave.

They work together. They observe. They notice strengths and weaknesses.
They remember what happened. They adjust how they communicate, review,
delegate, and intervene. Over time, they learn how to work together.

Now imagine that the new employee is not human.

It can write code, analyze documents, make plans, call tools,
communicate with customers, and operate software. But its behavior is
not fully predictable. It may:

- follow a wrong assumption for hours while producing plausible work;
- remember a correction but fail to apply the lesson in a new form;
- say a task is complete before the real-world outcome has been
  verified;
- become influenced by information simply because that information is
  visible in context;
- reproduce the same blind spot across multiple agents;
- accumulate reasonable safeguards until the safeguards themselves
  become the main problem.

These are not necessarily signs that the AI is "bad." They are
observations about how this new kind of worker behaves inside real
systems.

PRAOP asks:

> Given that AI works this way, how should we work with it?

## PRAOP Is a Practice, Not a Finished Theory

PRAOP does not begin with a doctrine and search for examples that prove
it. It begins with incidents.

The basic loop is:

```text
Something happens
        ↓
Record it
        ↓
Understand what actually happened
        ↓
Compare it with other cases
        ↓
Look for recurring patterns
        ↓
Develop a working practice
        ↓
Use it
        ↓
Observe what happens next
        ↓
Revise
```

Or more simply:

> Observe → Record → Compare → Learn → Try → Revise

PRAOP is therefore expected to change. A pattern that looks important
today may later turn out to be too broad. A best practice may work in
one environment and fail in another. A previously strong claim may
become contested. A new case may reveal an entirely new failure shape.

That is not a failure of PRAOP. That is how PRAOP is supposed to work.

## Cases Before Doctrine

The fundamental unit of PRAOP is the case. A case asks:

- What were you trying to do?
- What actually happened?
- Why did it matter?
- What did you try?
- What happened afterward?
- What evidence exists?
- What might we be misunderstanding?

Cases are then used to develop:

```text
Cases
  ↓
Patterns
  ↓
Practices
  ↓
Playbooks
```

**Cases** — what actually happened?

**Patterns** — does the same failure or success shape appear across
multiple independent incidents?

**Practices** — what should a team do differently?

**Playbooks** — how can those practices become a repeatable operating
workflow?

## PRAOP Is Not an AI Failure Museum

Failures matter because they teach us something. But success matters
too.

Open PRAOP welcomes cases where something worked unusually well:

- a team found a better way to review AI-generated code;
- an agent workflow reduced errors without adding excessive control;
- a human interruption prevented a long wrong trajectory;
- removing information from context improved reliability;
- a simple verification step eliminated a recurring problem.

We want to understand both "why did this fail?" and "why did this
work?"

## Evidence Matters

A well-written story is not automatically strong evidence. Open PRAOP
distinguishes between self-reported incidents, incidents supported by
artifacts, incidents that can be reconstructed, and independently
verified incidents.

We try to separate *what happened* from *what we think it means*. This
matters because AI systems — and humans — are very good at producing
convincing explanations after the fact.

PRAOP therefore follows a simple rule:

> Artifact > Memory

And another:

> Accepting a case does not mean accepting the theory built from it.

## No Fit Is a Valid Result

Open PRAOP does not require every case to fit an existing category. A
submission may be a strong fit, a partial fit, a new pattern candidate,
genuinely outside PRAOP's scope, or evidence that an existing PRAOP idea
is wrong.

This is important. A framework that explains everything explains
nothing. We actively want cases that challenge PRAOP.

## PRAOP Evolves

Patterns and practices in Open PRAOP have both a confidence level and a
status. A pattern can become stronger as evidence accumulates. But it
can also become **Contested** — new evidence challenges it — or
**Deprecated** — it is no longer recommended or has been replaced.

Even something that was once considered strong can later become
contested. PRAOP is not intended to become a collection of permanent
commandments. It is intended to remain an evolving body of operational
knowledge.

## Speak Human

AI can generate abstraction faster than humans can absorb it. Fluency is
not understanding.

PRAOP therefore requires important claims, risks, and practices to be
explainable in ordinary language to the person who owns the consequence.
If we cannot explain it simply, we do not yet treat it as
organizationally understood.

We call this principle **Renhua (人话)** — kept in Chinese rather than
fully translated, because the phrase carries an attitude that "plain
language" alone doesn't quite capture: don't let terminology, or fluent
AI output, stand in for real understanding. Every Pattern, Practice, and
Playbook in this repo carries a Plain-Language Version for exactly this
reason.

The stress test for it goes by three interchangeable names — pick
whichever fits: **EDTCU** (Even Donald Trump Can Understand — the origin
story), **Eddie-Q** (for casual discussion — "this fails Eddie-Q"), or
**EQ** (short form for checklists and review comments — "EQ: Pass"; not
emotional intelligence). Deliberately humorous, not a political
statement: if an idea can't survive being explained that plainly, we
don't yet trust that anyone actually understands it.

## A Different Kind of Guardrail

AI safety and AI security often focus on the model or system itself:
unsafe outputs, prompt injection, data leakage, access control,
adversarial behavior.

PRAOP looks at a different layer:

> What happens to the organization when probabilistic AI agents
> participate in real work?

Examples include: wrong assumptions becoming working reality;
verification disappearing between systems; responsibility becoming
unclear; organizational memory drifting; AI agents reinforcing the same
error; human reviewers losing semantic ownership; reliability controls
becoming so complex that they displace the actual work.

A useful shorthand:

> **AI Security protects systems. PRAOP helps protect organizations
> using AI.**

The two overlap, but they are not the same problem.

## From Knowledge to Practice to Enforcement

Knowing a rule is not the same as following it. PRAOP distinguishes
three levels:

- **Knowledge** — "I know this can happen."
- **Practice** — "We have a defined way to handle it."
- **Enforcement** — "The system makes it difficult to ignore."

This distinction matters because many AI failures happen even after
everyone involved already "knows" the lesson. A future goal of PRAOP is
therefore not only to publish advice, but to help turn recurring lessons
into operational workflows and, where appropriate, mechanical
guardrails.

## Open PRAOP

This repository is the public, open version of PRAOP. It contains four
primary kinds of material:

- **Cases** — real operational incidents
- **Patterns** — recurring behavioral or organizational shapes
- **Practices** — actionable responses supported by evidence
- **Playbooks** — workflows that combine multiple practices

The full protocol (submission templates, de-identification rules,
evidence levels, promotion rules) lives in
`protocol/open-praop-v0.1-final.md`.

You do not need to understand PRAOP terminology to contribute. If
something interesting happened while you were working with AI, tell us
what happened.

> Tell us the case. We can argue about the theory later.

## Contributing

You can contribute a failure case, a success case, evidence related to
an existing case, a challenge to an existing pattern, a proposed
practice, a better explanation, or a case that does not fit PRAOP at
all.

Start with `CONTRIBUTING.md`. Before submitting a case, please use the
de-identification guidance in the protocol. The goal is:

> Redact identity, preserve causality.

Do not submit secrets, credentials, private customer information, or
material you do not have the right to share.

## Current Status

Open PRAOP is early. That is intentional.

We are not claiming that the current taxonomy is complete. We are not
claiming that the current practices are universal. We are not trying to
turn a small number of observations into a standard prematurely.

The project will earn stronger claims only through more independent
cases, better evidence, real-world use, failed practices, competing
explanations, and deliberate attempts to falsify its own ideas.

## The Goal

The goal of PRAOP is not to make AI behave like a human. It is not to
eliminate uncertainty. And it is not to create enough rules to make
probabilistic systems deterministic.

The goal is simpler:

> Learn what kind of coworker AI actually is, and learn how to work with
> it well.

We expect that understanding to change as AI changes. So PRAOP must
change too.

## One Sentence

> PRAOP is an evolving, case-driven practice for learning how humans and
> probabilistic AI agents can work together reliably.

## License

Open PRAOP documentation, public cases, patterns, practices, and
playbooks are released under
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/), unless
otherwise noted. Commercial use is explicitly permitted; publicly
distributed derivatives of the materials themselves must carry the same
license.

The PRAOP name and associated branding are not granted as trademarks by
that license.

See `LICENSE` and `CONTRIBUTING.md` for details.
