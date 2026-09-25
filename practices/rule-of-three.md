# Practice: Rule of Three — Stop After Three Related Material Failures, and Make the Fourth Move a Reframe

**Confidence / Status:**
- **Review mode:** Observed / Active.
- **Diagnostic mode:** proposed / unvalidated extension (no first-party
  anchor where the rule was used and worked).
**Enforcement Level:** Guidance
**Anchor case(s):** `../cases/accepted/014-mutual-local-optimization-semantic-ownership-loss.md`

### Plain-Language Version (人话版)

If you have tried three times to make something work the same way and
it failed each time for related reasons, stop. The fourth thing you do
must be to question the way you are going about it (what you are really
trying to achieve, what you assumed, how much you are taking on, what
you actually know), not a fourth, bigger attempt. Handing it to another
agent, writing a new document, or moving to a "higher-level" design does
not count as starting over.

### Problem Addressed

A working loop that keeps producing locally correct fixes while the
premise it rests on is never re-examined. Each failure is answered by a
more elaborate attempt in the same frame, so the loop looks "one fix
from done" while it moves away from what is needed. Related patterns:
**Trajectory Lock** (a wrong premise pursued through increasingly
elaborate patches; see Case 005 for the unstopped form) and **Semantic
Ownership Loss** (the accountable human keeps approving without being
able to say whether this is still what they wanted).

This practice is the **stop-and-reframe trigger**. It is distinct from
**Plain-Language Re-Ownership**, which is one of the recovery actions a
reframe can use (see What to Do, step 4). The trigger says *when* to
stop; re-ownership is *one way* to get the goal back.

### When to Use

Two modes are covered in v0.1:

- **Review mode:** an implementer and a reviewer (human or AI, same or
  different models) iterate on a deliverable. Count revisions rejected
  with a material finding.
- **Diagnostic mode (proposed extension, unvalidated):** debugging or
  investigation. Count fixes or hypotheses under the same theory that
  fail verification or recur. There is no first-party anchor where the
  rule was used in this mode and worked; Case 005 shows only the failure
  shape. Treat this mode as a proposal until such an anchor exists (or
  drop it from v0.1 if the maintainer prefers).

**Not in v0.1:** a *multi-agent collective escalation mode* (several
agents jointly escalating a shared course of action). It is a separate
candidate and is not defined here.

### Definitions (operational tests)

- **Working frame.** The combination of four things: the **goal** (what
  "done" means for the owner), the **premise** (the assumptions and
  threat model the work rests on), the **scope** (what is in and out),
  and the **evidence standard** (what counts as verified). The frame
  changes only when at least one of the four is explicitly revised and
  the owner re-approves it in plain language.
- **Material failure.** An attempt the agreed acceptance authority
  rejects as blocking (for example, a reviewer's blocking/P1 finding, a
  claimed fix that fails verification, or a fix that recurs). Cosmetic
  or non-blocking findings don't count.
- **Related.** Failures are related only when they can be traced to the
  **same unrevised central premise or invariant** (see below), or when
  it can be shown that changing or narrowing that premise/invariant would make them disappear
  or change their nature. **A shared risk label alone ("both are security
  issues", "both are in the upload path") does not make failures
  related**, and doesn't count toward three. The test: *would this
  finding still exist if the premise or invariant were changed or
  narrowed to what the owner actually needs?* If not, it is related
  through that premise/invariant. If the
  link can't be shown, count the failure as unrelated.
- **Central premise/invariant.** The assumption that, if changed, would
  remove or reclassify most of the failures so far. Naming it is the
  first task of the reframe.

### What to Do

1. **Early warning (not the rule itself):** at the **second** related
   material failure, pause and check the shared premise. Is the latest
   finding inside what the owner actually needs? This is a check, not a
   stop.
2. **Count** related material failures within one working frame. Keep
   the count visible in the working record (for example, in the review
   request or the design's revision log), not in anyone's memory.
3. **At the third, stop.** No fourth attempt of the same kind: no
   further patch, and no escalation to a larger mechanism in the same
   frame.
4. **The fourth move must be a reframe**, recorded in writing. It
   revisits all four frame elements and ends with the owner's
   plain-language re-approval:
   - **Goal:** restate what the owner needs, in the owner's own words
     (Plain-Language Re-Ownership);
   - **Premise:** name the central premise and check it against the real
     need; drop what the need doesn't require;
   - **Scope:** narrow or split the work (for example, a small binding
     part and an informative remainder);
   - **Evidence:** measure the real system, or change the unit of work
     (for example, list every situation an invariant must hold in and
     which test covers it), instead of answering the next finding.
   A reframe may also conclude "stop the work".
5. **Reset the count only after a reframe** that changed at least one
   frame element and was re-approved by the owner.

### What Not to Do

- **Don't treat a redesign as a reframe.** Moving from patching code to
  designing a bigger mechanism under the same premise continues the
  loop (Case 014's first trigger).
- **Don't reset the count by changing hands or artifacts:** another
  agent, another reviewer, a new document, a new file or a higher
  architecture level is the same frame if the goal, premise, scope and
  evidence standard are unchanged.
- **Don't read the rule as "fewer review rounds".** After a real reframe,
  many further rounds can be legitimate if their findings are inside
  the new frame (in Case 014, five further rejections after the reset
  were in scope and ended in an approved design). The aim is
  scope alignment, mechanism restraint and owner-answerability, not a
  low round count.
- **Don't count non-material findings,** and don't use the rule to cut
  off a review whose findings are in scope.
- **Don't let the trigger replace the recovery.** Stopping without
  reframing only pauses the loop.

### Evidence

- **Case 014** (`../cases/accepted/014-mutual-local-optimization-semantic-ownership-loss.md`),
  review mode. **One incomplete trigger:** after three rejected code
  versions, the work moved to a larger design under the same premise,
  and three more design versions were rejected. **One effective
  trigger:** the owner re-read the concrete dispute and replaced the
  premise; the work then converged on an in-scope design. This is the
  evidence for "a redesign is not a reframe" and for "the fourth move
  must revisit the premise". Evidence level E1-private.
- **A second first-party incident in the same environment (not yet
  public; not counted as a public anchor here):** review mode. After two
  rounds with material failures, the owner set a stop condition for the
  third; the third failed; no fourth round of local patching followed;
  the unit of work changed to a per-invariant matrix (every situation
  each promise must hold in, and which test covers it), which found
  further gaps, including one claim false in all versions. One effective
  trigger. It will be cited by number if it is accepted into this corpus.
- **Case 005** (`../cases/accepted/005-trajectory-lock-rate-lookup-mfa.md`)
  is **not** evidence that this practice works. It shows the failure
  shape the practice targets in diagnostic mode (a three-week trajectory
  with no stop).

Both incidents above share one environment (the same owner and project).
They are distinct incidents but environmentally correlated, not
independent evidence.

### Known Limitations

- Two incidents in one environment; no independent environment yet.
- **"Three" is a convention, not a calibrated threshold.** The early
  warning at two exists because the loop can be recognized before three.
- Judging "related" and "material" still needs judgment. The tests above
  make it explicit but not mechanical.
- It doesn't specify **who counts**. Proposed: any participant may call
  it, the count lives in the working record, and the owner decides
  whether a reframe really changed the frame.
- Diagnostic mode has no first-party anchor yet and is marked as an
  unvalidated extension; it is included because the same failure shape
  appears in Case 005, not because the practice was observed working
  there.
- Untested for the multi-agent collective escalation mode (out of v0.1).

### Enforcement Level

**Guidance.** In the anchor environment it is a written project working
rule and part of the agents' standing instructions; nothing mechanically
blocks a fourth same-frame attempt.

### Confidence

- **Review mode:** **Observed / Active** (first-party intervention
  observations in one environment: Case 014, with one incomplete and one
  effective trigger, and one not-yet-public incident). Not higher until an independent environment supplies an
  anchor.
- **Diagnostic mode:** proposed / unvalidated extension; no status until
  a first-party anchor shows the rule used and working in this mode.
