# Practice: Mid-Run Issue Gate — Block vs. Backlog

**Confidence / Status:** Observed / Active
**Enforcement Level:** Guidance
**Anchor case(s):** `../cases/accepted/002-control-accretion-rerun.md`

### Plain-Language Version (人话版)

If you find a problem mid-run, ask one question first: does this break
the run you're already doing? Yes → stop and fix it now. No → write it
down and keep going.

### Problem Addressed

Control Accretion / Control-Induced Drift — a verification or fix
applied mid-run changes the state being verified, triggering an
unbounded loop of re-verification.

### When to Use

Any "repeat an already-designed run" task: rerunning a frozen
experiment, redeploying a frozen config, re-executing a signed-off
pipeline — any point where a new issue might surface mid-execution.

### What to Do

On finding an issue mid-run, classify it explicitly before acting: does
this invalidate the current run's input, output, or scoring/correctness
validity?

- **Yes** → block, fix now, then continue.
- **No** → log to a backlog, keep running under the original plan.

Never let "found a real issue" default automatically to "fix now, then
re-verify everything."

### What Not to Do

Don't let a fix change something a prior verification step already
signed off on (e.g. a commit pin) without explicitly re-triggering
*that specific check* — not the whole verification chain.

### Evidence

- Case 002 (`../cases/accepted/002-control-accretion-rerun.md`) — 1
  anchor, E0.

### Known Limitations

Untested against a second instance. Doesn't yet specify who makes the
block/backlog call under time pressure, or what happens when a
"doesn't invalidate" judgment turns out to be wrong later.

### Enforcement Level

**Guidance.** Currently relies on the operator or agent asking the
question explicitly; no mechanical check exists yet. A future
mechanical version might be a checklist prompt or a script gate that
requires an explicit yes/no answer before continuing a "repeat" task
after any mid-run change.

### Confidence

**Observed / Active.** Per §10 of the protocol, cannot be promoted to
Emerging without either additional independent supporting evidence or a
second underlying incident.
