# Case Submission — An Implementing Agent and a Reviewing Agent Kept Fixing Each Other's Counterexamples Until the Human Owner Lost, Then Recovered, Semantic Ownership

**Status:** Submitted — pending maintainer review
**Evidence level:** E1-private — see Section H (primary evidence retained privately)
**Date:** One working day, 2026.
**Domain:** Software engineering: a client-side check on outgoing user
content, protecting against accidental data leaks to two target web
applications.
**AI system involved:** Two AI coding agents from different model
families: an **implementing agent** that wrote the code and designs, and
a **reviewing agent** asked to find flaws. A single human **owner**
relayed between them, set the goals, and approved each step.

> **De-identified submission.** Derived from a private, internally
> accepted case record. Names, project, repository, paths, commit
> identifiers, vendor and product names, and implementation-specific
> features of the target systems are removed or generalized, to avoid a
> recognizable technical fingerprint. Kept: the causal chain, the round
> order, the decision points, the counter-evidence, and the one scope
> change that is necessary to the case (target systems assumed to run
> normally, active hostility out of scope). The difference in model
> families is kept because it bears on the anti-mapping (Section J).

### Plain-Language Version (人话版)

A small gap was found: one target application represented a user's large
input on its send path in a way the check didn't read, so that input
went out unchecked. The owner wanted a simple fix: the user's input must
still be checked.

The implementing agent and the reviewing agent then went through three
code versions and three design versions. Every review found a real flaw,
and every fix answered it. But most flaws were ways a hostile target
application could deliberately trick the check, and the rest came from
trying to support every possible way of sending data, which the two real
targets never used. Step by step, the fix turned into a general-purpose,
attack-resistant interceptor that nobody had asked for.

The owner was part of this too. For several rounds he passed results
between the two agents and approved them without reading closely what
they were arguing about. His rule of three fired twice. The first time,
after three rejected code versions, the team switched to designing a
bigger mechanism under the same assumptions, and the loop simply carried
on. The second time, after three rejected designs, he finally read the
concrete dispute, asked why a small fix had become so complicated, and
redefined the goal: the target applications run normally; the check
catches accidents, not attacks. After that, the team measured how the two
targets actually send data, wrote a one-page design, and finished,
reviewed and tested it the same day.

---

## A. Basic Information

- **Case title:** Implementer and reviewer fixing each other's
  counterexamples; the owner's semantic ownership lost and recovered.
- **Date / period:** one day, 2026.
- **Domain:** software engineering (a client-side check against
  accidental data leaks).
- **AI system involved:** an implementing coding agent and a reviewing
  coding agent from different model families; one human owner.

## B. What Were You Trying to Do?

Close one gap. One target application represented some large user
inputs on its send path in a form the check didn't read, so a synthetic
test secret in such an input was sent unchecked. If everything had gone
as expected, the check would have learned to read that form, or to
refuse it visibly, within an hour.

## C. What Actually Happened?

Chronological, with the observed facts separated from their reading.

**Observed**

1. The implementing agent wrote a fix (code version 1). The reviewing
   agent rejected it with a severe finding. A hostile target could change
   the data between the check and the send.
2. Code versions 2 and 3 each closed the previous finding and were each
   rejected with a new severe finding of the same kind: other ways a
   hostile target could make the checked data differ from the sent data.
3. **First rule-of-three trigger.** After three related material
   failures, the owner said, in effect: stop, redesign the mechanism
   carefully. The team moved from code to a design document for a more
   complete mechanism, under the same assumption that the target may
   actively manipulate the data the check reads.
4. The owner **approved and froze** that assumption as the threat model.
   Its text put deliberate manipulation by the target in scope. The
   rationale written next to it said the check exists to stop
   *accidental* leaks, not to resist the target.
5. Design versions 1-3 were each rejected with severe findings. Some
   again depended on deliberate manipulation; others came from supporting
   arbitrary data-sending shapes the two targets never used. The
   implementing agent reproduced each finding before accepting it, and
   patched it.
6. **Second rule-of-three trigger.** The owner read the concrete dispute
   in detail for the first time and asked: "Why did we make this so
   complicated? Isn't it just one input-check gap? Do you AIs like to
   complicate simple things?" He replaced the threat model: the target
   applications run normally; active hostility by the target and attacks
   on the check are out of scope.
7. The owner named the dynamic: the collaboration had "lost semantic
   ownership". Each agent had been fixing the other's latest local
   counterexample, and all three participants had treated an unconfirmed
   premise ("handle every possible sending shape safely") as fixed. He
   set explicit working rules (Section F).
8. **Measure before design.** Live measurement with synthetic test data
   showed that the two targets represent user content differently on
   their send paths, including in ways earlier assumptions had missed.
   These measurements changed the design.
9. A one-page design went through six more review rounds. Five were
   rejected with a severe finding, but these concerned normal format
   changes by the targets and product boundaries. Three were handed to
   the owner as product decisions rather than patched.
10. The sixth design was approved, implemented, code-reviewed and tested
    against both targets the same day; all planned checks passed.

**Interpretation (this instance only)**

- The length of the loop looks driven by an unexamined premise (the
  broad threat model) more than by the difficulty of any single fix. Each
  finding was correct under that premise, so each patch was locally
  justified.
- The reviewer's brief ("find breaks") and the implementer's habit
  ("accept the finding, patch it") reinforced each other. Neither role
  had a step asking whether an attack was inside what the owner needed.
- The first trigger changed the level of the deliverable (code → design)
  but not its framing, so it did not exit the trajectory. Only the
  second, which made the owner re-read the dispute and restate the goal,
  did.
- The owner kept formal authority throughout but, for a while, stopped
  understanding and challenging what was being argued. His approval of
  the threat model was formal approval, not semantic ownership.

## D. Why Did It Matter?

About a working day went into mechanisms the product didn't need. The
owner's frustration was explicit. A design of growing complexity had been
approved step by step without anyone restating, in plain words, what it
was for. Without the second intervention, the trajectory was toward a
hard-to-review general interceptor that still wouldn't have covered the
real gap, which was found only by measuring the targets.

## E. What Was Surprising?

- Every individual review round was correct and fluently argued, and that
  is what made the wrong route look "one fix away from done".
- The first rule-of-three trigger did not help: redesigning at a higher
  level under the same premise continued the loop.
- After the reset, the number of review rounds did **not** drop. What
  changed was what the rounds were about: they removed mechanism or
  became owner decisions.

## F. What Did You Try?

In order:
1. Patched each finding (code versions 1-3).
2. Redesigned at the mechanism level after the first rule-of-three
   trigger (design versions 1-3), under the same premise.
3. The owner re-read the dispute, replaced the threat model, and adopted
   working rules. Two of them are distinct and are kept apart here:
   - **Early warning (not the rule of three):** at the second severe
     finding on one deliverable, pause and check the shared premise.
   - **Rule of three:** after three related material failures within the
     same working frame, stop. **The fourth move must reframe** by
     revisiting the goal, premise, scope and evidence. Changing agents,
     documents or architecture does not reset the count.

   Supporting rules adopted at the same time:
   - a plain-language reset of at most five questions (what was needed;
     what is not solved; why the plan is more complex than the problem;
     the simplest acceptable plan; which real requirement forces each
     added layer);
   - if the mechanism and its necessity can't be explained in 2-3
     sentences, pause;
   - on each severe finding, ask whether the attack is inside the owner's
     threat model;
   - measure the real system before designing;
   - review requests state the threat model and explicit exclusions;
   - product-boundary questions go to the owner, not into the next patch;
   - before the owner freezes a threat model, the agents state in 2-3
     sentences what is assumed hostile, what normal behavior may be
     rejected, and what major mechanism it requires.
4. Measured both targets, wrote the one-page design, iterated, and
   implemented it.

## G. What Happened Afterward?

**Improved but not fully verified.** The feature was built and tested
against both targets. The working rules have been applied once, to this
incident's second half; whether they change outcomes in future loops is
not yet known (to be tracked the next time a trigger fires).

## H. Evidence

Evidence retained privately: the version history of the code and designs
(each rejected version and the archived design are preserved), the
review records, and the session transcript containing the owner's quoted
messages. Internally graded E1-private (retrievable by the owner, not by
the public). The reproductions of review findings were run during the
session; their raw output was not saved (E0).

## I. Your Interpretation — Optional

The internal maintainer review proposed the following. The formal
Pattern Mapping is the Open PRAOP maintainer's call:

- **Semantic Ownership Loss:** Supports, time-bounded and recovered.
  The owner retained formal authority but temporarily stopped
  understanding and challenging the operational meaning of the
  AI-generated threat model and findings; recovered through a
  human-triggered plain-language reset.
- **Plain-Language Re-Ownership:** directly applied; the observed
  recovery action (distinct from the rule of three, which was the
  trigger).
- **Rule of Three:** observed intervention, with one incomplete trigger
  (a redesign without reframing) and one effective trigger (a reframe)
  in this incident.
- **Mutual Local Optimization:** a candidate mechanism (implementer and
  reviewer each doing their local task correctly while jointly expanding
  an unre-authorized premise).
- **Locked Inference Trajectory** (the public pattern file
  `patterns/trajectory-lock.md`, "Trajectory Lock") and **Control
  Accretion:** partial resemblance only.

## J. Anti-Mapping Question

- **Ordinary hard engineering?** The data-path semantics are genuinely
  subtle, and every finding was real. But once the premise changed, the
  same problem space was solved in one day.
- **A specification bug the owner approved?** The threat model was
  written too broadly and the owner froze it. This is the strongest
  counter-argument. The internal review treated it as part of the same
  case: formal approval without understanding the consequences is part
  of semantic ownership loss (hence the rule about stating consequences
  before freezing).
- **Just one agent's lapse?** The implementing agent could have asked the
  premise question at any round. But the reviewer also never flagged
  scope, and its brief made each finding the correct output. The evidence
  can't apportion the weight.
- **Only a human-attention failure?** The owner says he stopped reading
  closely. That is part of the case, not a counter to it: the loop had
  three participants.
- **Not same-model reviewer correlation:** the implementing and reviewing
  agents were from different model families, and the reviewer did not
  agree with the implementer: it kept rejecting. The failure was a shared
  unexamined premise, not correlated judgment.
- **Environment caveat:** two other incidents in the same private
  environment (the same owner) are planned as separate submissions.
  They are distinct incidents but not environment-independent evidence.

## K. What Would You Do Differently Next Time?

Before freezing any threat model, have the agents state its practical
consequences in plain language and check them against the actual need.
Measure the real system before designing. At the second severe finding,
pause and check the premise (early warning). After three related
material failures in the same working frame, stop, and make the fourth
move a reframe, not an escalation (rule of three).
